# 1st Notebook example: Keyword and Topic modelling



```python
<img src="xx.png" width="50%">
```

# How-to-use

## Installation

First Check installation has been made, as per the [READme](https://github.com/lawrencerowland/Data-Model-for-Project-Frameworks/blob/master/Project-frameworks-by-using-NLP-with-Python-libraries/README.md)

## Import Gensim

```python
import gensim
from gensim.summarization import summarize
from gensim.summarization import keywords
from gensim.parsing.preprocessing import strip_multiple_whitespaces
from gensim import corpora, models, similarities
# Note that Smart_open.gcs may not import successfully depending on Gensim set up. This doesnt matter. 
```

    unable to import 'smart_open.gcs', disabling that module


## Change Directory to find the portfolio text files

This outputs the names of the 16 text files.

```python
import os
directory = '/Users/lawrence/Documents/GitHub/Data-Model-for-Project-Frameworks/Project-frameworks-by-using-NLP-with-Python-libraries/Text-files-as-generated-by-PDF-Miner'
print (os.listdir(directory))
# Change directory location for your particular set-up. Or if you want to just re-run this nuclear example, then you just need to change the reference to the high-level directories
# If a mac, can copy the directory location by opening the Inspector for the folder
```

    ['Commissioning of security systems and infrastructure cns-tast-gd-4.4 cns-tast-gd-4.4.pdf.txt', 'Construction Assurance ns-tast-gd-076.pdf.txt', 'Control of processes involving nuclear matter ns-tast-gd-023.pdf.txt', 'Decommissioning ns-tast-gd-026.txt', 'Design Safety Assurance ns-tast-gd-057.pdf.txt', 'Fundamental Principles ns-tast-gd-004.pdf.txt', 'Guidance on the Demonstration of ALARP ns-tast-gd-005.pdf.txt', 'Management of Radioactive material ns-tast-gd-024.pdf.txt', 'nuclear construction sites cns-tast-gd-6.6.pdf.txt', 'Organisational Change ns-tast-gd-048.pdf.txt', 'oversight of items or services cns-tast-gd-4.3.pdf.txt', 'PM_guidance_for_Energy_Projects.txt', 'Probabilistic Safety Analysis.pdf.txt', 'Procedure Design and Administrative Controls.pdf.txt', 'Procurement cns-tast-gd-4.1 cns-tast-gd-4.1.pdf.txt', 'Reliability and resilience of the security system cns-tast-gd-5.1 cns-tast-gd-5.1.pdf.txt', 'Supplier capability cns-tast-gd-4.2.pdf.txt']


## Collect any Internet pages 

This is an option. 

In order to compare the results with the Orange results, I have not run this block of code. 

In addition to the text files you have collected, there may be one or two internet pages which you want to add to the analysis. 
I have added this partly to show what happens when a document is added which is about the same subject, but comes at the subject from a very different angle. 

If you wish to collect many Internet pages, you will need to construct a loop.  You also will need to check how well the text is extracted from  particular sources, and consult the Python Requests module documentation if it needs adjustment. 


```python
import requests
text = requests.get('https://archive.org/stream/ProjectManagementForTheOilAndGasIndustry/ProjectManagementForTheOilAndGasIndustry_djvu.txt').text
text=text[70000:300000] #here I have stripped the front text by inspection only.
#text=strip_multiple_whitespaces(text)  #may wish to turn this off for readability
filename="PM_guidance_for_Energy_Projects"
f= open(filename+".txt","w+") 
f.write(filename+"\n"+text)
f.close()
```

```python
#GENSIM summary, keywords
Corpus_of_Summaries =[]

for filename in os.listdir(directory):
    if filename.endswith('.txt'):
        with open(os.path.join(directory, filename)) as f:
            
            content = f.read()
            
            summary=(filename+'Summary\n'+summarize(content, ratio=0.01)) #word_count=20
            key_words=keywords(content, ratio=0.007)
            
            print ('\n\nFile',filename)
            print ('\nSummary:',summary,"\n")
            print ('\nKeywords:',key_words)
            
            Corpus_of_Summaries.append(summary)
            
            #print (content[0:100]) # testing the content is coming through
            # print(repr(summary)) #alternate version showing line breaks etc
    
            f.close()
```

```python
print(Corpus_of_Summaries[2]) # Could equally do this w full content, but starting simple
```

**IDENTIFY TOKENS AND MAKE-UP DICTIONARY**

```python
# remove common words and tokenize.# Here we can add in some odd words we find in the output, or use the NLTK list
stoplist = set('for a of the and to in \uf06e  • \uf0b7 \uf0b7 \uf06e uf09 \uf09f'.split())
Tokens_in_Corpus = [[word for word in summary.lower().split() if word not in stoplist]
         for summary in Corpus_of_Summaries]
```

```python
# remove words that appear only once
from collections import defaultdict
frequency = defaultdict(int)
for text in Tokens_in_Corpus:
    for token in text:
        frequency[token] += 1

Frequent_Tokens_in_Corpus= [[token for token in text if frequency[token] > 1] for text in Tokens_in_Corpus]

from pprint import pprint  # pretty-printer
pprint(Frequent_Tokens_in_Corpus[4:5]) #these slices of lists go up to before the higher number. 
```

```python
#create dictionary, then map from ids to dictionary
dictionary = corpora.Dictionary(Frequent_Tokens_in_Corpus)
print(dictionary,"\n\n")
print(dictionary.token2id)
```

**CREATE BAG OF WORDS MODEL**

```python
#ie. a list of a list. For each document, we have a list of word frequency for each dictionary item
BAG_OF_WORDS_MODEL = [dictionary.doc2bow(text) for text in Frequent_Tokens_in_Corpus]
for c in BAG_OF_WORDS_MODEL:
    print(c)
```

From Quick start tutorial. 
"Now that we have vectorized our corpus we can begin to transform it using models. We use model as an abstract term referring to a transformation from one document representation to another. In gensim documents are represented as vectors so a model can be thought of as a transformation between two vector spaces. The details of this transformation are learned from the training corpus."

**CREATE TF-IDF MODEL**
One simple example of a model is tf-idf. The tf-idf model transforms vectors from the bag-of-words representation to a vector space where the frequency counts are weighted according to the relative rarity of each word in the corpus.
Let's initialize the tf-idf model, training it on our corpus.

```python
# train the model
TFIDF_MODEL= models.TfidfModel(BAG_OF_WORDS_MODEL)
```

**CREATE TOPIC MODEL via LSI** via CBOW AND TFIDF

```python
# LSI APPLIED ON TOP ON TFIDF
#now applying an LSI to the first corpus, by working on top of its representation as a TFIDF
# here we have created a two dim LSI space, like Deerwesters 1990 example
#Presumably we could create one on top of just the CBOW too
lsi_from_TFIDF= models.LsiModel(TFIDF_APPLIED_TO_TRAINING_CORPUS, id2word=dictionary, num_topics=3) # initialize an LSI transformation

#It is correct how it has this odd double-barrelled structure: 
#model = LsiModel(common_corpus, id2word=common_dictionary)
# >>> vectorized_corpus = model[common_corpus]  # vectorize input copus in BoW format
```

```python
#inspect the topics
lsi_from_TFIDF.print_topics(num_topics=-1, num_words=20) #-1 means show all topics .In significance order. Remember also _ve Contribs
```

```python
#Get a single topic as a formatted string with print_topic(topicno, topn=10)
```

```python
#to get as array use lsi.get_topics()
```

```python
# can Update model with new corpus using add_documents(corpus, chunksize=None, decay=None)
#can also save the LSI model
```

**FINDING VECTOR REPRESENTATION OF A WHOLE OLD OR NEW CORPUS**
To prepare for similarity queries, we need to enter all documents which we want to compare against subsequent queries. In our case, they are the same documents used for training LSI, converted to 3-D LSA space. But that’s only incidental, we might also be indexing a different corpus altogether.

   **REPRESENTATION OF OLD CORPUS: TFIDF**

```python
#now moved onto Topic and Transformations tutorial
#apply tfidf to the trained corpus
TFIDF_APPLIED_TO_TRAINING_CORPUS = TFIDF_MODEL[BAG_OF_WORDS_MODEL]
for doc in TFIDF_APPLIED_TO_TRAINING_CORPUS:
    print(doc)
```

   **REPRESENTATION OF OLD CORPUS: LSI FROM TFIDF**

```python
# create a double wrapper over the original corpus: bow->tfidf->fold-in-lsi
TOPIC_MODEL_LSI_from_TFIDF_APPLIED_TO_CORPUS = lsi_from_TFIDF[TFIDF_APPLIED_TO_TRAINING_CORPUS] 

#particular documents aligned to particular topics
for doc in TOPIC_MODEL_LSI_from_TFIDF_APPLIED_TO_CORPUS: # both bow->tfidf and tfidf->lsi transformations are actually executed here, on the fly
    print(doc)
```

```python
#OPTIONAL
#this model can now be applied to another corpus other than the training one, not just individaul documents
#i have not pulled in a second corpus but this is how you would do it. Note you pull in a corpus (processed as above), not just docs. 
#corpus2nd_tfidf = TFIDF_MODEL[corpus2nd]
# for doc in corpus2nd_tfidf:
#   print(doc)
```

**FINDING VECTOR REPRESENTATION OF A SINGLE NEW DOCUMENT**

```python
# Up above, we had a CBOW representation of each document
#We can convert documents to that vector space,once tokenized

# eg.This is the announcement of the Sellafield partner programme. https://www.gov.uk/government/news/sellafield-ltd-awards-20-year-project-partnership
#Which ONR document is most relevant to this contract ?
```

```python
page = requests.get("https://www.gov.uk/government/news/sellafield-ltd-awards-20-year-project-partnership")
from bs4 import BeautifulSoup
soup = BeautifulSoup(page.content, 'html.parser')
new_doc=strip_multiple_whitespaces(soup.get_text())
print(new_doc)

#page = requests.get("https://www.gov.uk/government/news/nda-sets-out-its-grand-challenges")
#page.content[1:300]
# need to find which tag works well with this approach. p does not work well with this NEC text 
#soup.find_all('p')[5].get_text()
```

```python
new_doc=new_doc[0:5487]
print(new_doc)
```

In addition, we will be considering cosine similarity to determine the similarity of two vectors. Cosine similarity is a standard measure in Vector Space Modeling, but wherever the vectors represent probability distributions, different similarity measures may be more appropriate.

   **REPRESENTATION OF NEW DOCUMENT: CBOW ONLY**

```python
#convert tokenized documents to vector
new_vec_CBOW = dictionary.doc2bow(new_doc.lower().split())
```

```python
print(new_vec_CBOW)  # only those words that match up are given a dimension
```

   **REPRESENTATION OF NEW DOCUMENT: TFIDF**

```python
#convert the query to LSI space (based on TFIDF) 
new_vec_TFIDF=TFIDF_MODEL[new_vec_CBOW]
```

   **REPRESENTATION OF NEW DOCUMENT: LSI via TFIDF**

```python
new_vec_lsi_fromTFIDF = lsi_from_TFIDF[new_vec_TFIDF]
print(new_vec_lsi_fromTFIDF)  
```

**COSINE SIMILARITY**

moved onto Similarity search tutorial.
Based on this new doc query,we would like to sort our corpus documents in decreasing order of relevance to this query. Unlike modern search engines, here we only concentrate on a single aspect of possible similarities—on apparent semantic relatedness of their texts (words). No hyperlinks, no random-walk static ranks, just a semantic extension overthe boolean keyword match:

   **LSI VIA TFIDF**

```python
# LSI APPLIED ON TOP ON TFIDF
index = similarities.MatrixSimilarity(lsi_from_TFIDF[TFIDF_APPLIED_TO_TRAINING_CORPUS]) # transform corpus to LSI space and index it
```

```python
sims = index[new_vec_lsi_fromTFIDF] # perform a similarity query against the corpus BASED ON LSI - TDFIDF
print(list(enumerate(sims))) # print (document_number, document_similarity) 2-tuples
```

Cosine measure returns similarities in the range <-1, 1> (the greater, the more similar), so that the first document has a score of 0.99809301 etc.

With some standard Python magic we sort these similarities into descending order, and obtain the final answer to the query for Sellafield PPP:

```python
sims = sorted(enumerate(sims), key=lambda item: -item[1])
print(sims) # print sorted (document number, similarity score) 2-tuples
```

```python
#Most like
print (Corpus_of_Summaries[15])
```

```python
print (Corpus_of_Summaries[12])
```

```python
print (Corpus_of_Summaries[9])
```

```python
#Least like
print (Corpus_of_Summaries[11])
```

```python
print (Corpus_of_Summaries[10])
```

   **TFIDF ONLY**

```python
#Now the same but with TFIDF model
index = similarities.MatrixSimilarity(TFIDF_APPLIED_TO_TRAINING_CORPUS)
new_vec_TFIDF = TFIDF_MODEL[new_vec_CBOW] # convert the query to LSI space (based on TFIDF)
print(new_vec_TFIDF)  
```

```python
sims = index[new_vec_TFIDF] 
print(list(enumerate(sims)))
sims = sorted(enumerate(sims), key=lambda item: -item[1])
print ("\n")
print (sims)
```


**Using keywords into Neo4j concurrence...**


# Acknowledgements

This project relies extensively on the Gensim library, and the [examples](https://radimrehurek.com/gensim/auto_examples/index.html) provided by its creator Radim Hurek. I have done nothing more than apply a little of this to Portfolio management. The examples cited above would be the best way to get a full introduction to the capabilities of Gensim


@inproceedings{rehurek_lrec,
      title = {{Software Framework for Topic Modelling with Large Corpora}},
      author = {Radim {\v R}eh{\r u}{\v r}ek and Petr Sojka},
      booktitle = {{Proceedings of the LREC 2010 Workshop on New
           Challenges for NLP Frameworks}},
      pages = {45--50},
      year = 2010,
      month = May,
      day = 22,
      publisher = {ELRA},
      address = {Valletta, Malta},
      note={\url{http://is.muni.cz/publication/884893/en}},
      language={English}
}

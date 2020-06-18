# 1st Notebook example: Keyword and Topic modelling

<img src="xx.png" width="50%">

**[Purpose](#Purpose)** | **[Motivation](#Motivation)** |**[Features](#Features)** |**[Prerequisites](#Prerequisites)** |**[Quick start](#Quick-start)** |**[How-to-use](#How-to-use)**|

# Purpose 

**For any set of portfolio documents, automatically generate keywords and summaries per document, and generate a set of the main topics found. Accordingly, generate a data-model for the portfolio** 


# Motivation

Projects have different business and function aspects. These notebooks can be used to run simple code on a set of pdf and text files that the user has collected for their particular business domain. 

Below is basic code that can be applied directly to  any portfolio documents. Here this code is worked through with an example of understanding the implications of the regulatory environment on project delivery in the nuclear sector.This can be replaced as the user generates her own results. 

For simplicity, this one starts from documents as text files and internet pages. Additional features can be sought in the other notebooks once first results have been generated for your portfolio documents. 

# Features
- Summarises each document
- finds keywords for each document
- creates a similarity-search: for any new paragraph, it finds the most similar documents from the library
- (propose a data-model for the portfolio, based upon these findings) ***(Status: incomplete)***

# Prerequisites 

The following Python libraries are needed: Gensim, BS4, NetworkX, Matplotlib, Pandas. Also NLTK and SpaCy. Gensim requires NumPy and SciPy. NLTK requires Pandas.

For example, if one chooses to do it in Conda:

1. Install Miniconda

1. Create GENSIM_ENV environment with an appropriate Python version

1. Install Gensim dependencies. Currently these are NumPy then SciPy and then Gensim 

1. conda activate GENSIM_ENV . Then jupyter lab

(one may need to also activate the Env again once in Jupyter lab)

From Step 8 onwards, it is recommended you install Neo4j.
Although it can be done on cloud versions of Neo4j, or on YEd, or YEd live, or on Gephi. 

# Quick-start

It is suggested to move straight down to **[How-to-use](#How-to-use)**| to get started.

(Attributes and adjustments are included immediately below for ease of reference, but best consulted after using the notebook).

The user can start from the markdown file (xx) showing and explaining the code, or can work through the notebook directly (xx). Some minor detail is hidden in the markdown file, but shown in the notebook.

## Attributes

- Uses GENSIM library
- Starts from Text file rather than PDF
- also starts from Internet page
- creates corpus at Document level rather than paragraph level
- for Topic model, starts from Bag of Words model, as an interim step only
- It uses TFIDF model only as an interim step to LSI only
- for similarity-search, it uses cosine similarity, based upon LSI model

# Attributes you can find in the other notebooks
- Using other libraries than Gensim
- Starting from Text file
- creates corpus at paragraph level
- uses Bag of Words model to generate results directly for similarity search

# Easy adjustments that can be made, but have not been shown
- for Topic model, uses only Bag of Words model 
- for similarity-search, using cosine similarity, based upon TFIDF model
- for topic model, uses methods other than LSI. 

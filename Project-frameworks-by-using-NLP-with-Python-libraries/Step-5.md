# Step-5: Compile a single library



|**[Overview](#Overview)** |**[Installation](#Installation)||**[Prior-steps](#Prior-steps)**|**[How-to-use](#How-to-use)**|**[Next-steps](#Next-steps)**|

# Overview
This pulls the Corpus together as one text string. 

# How-to-use

# Installation

Check installation has been made, as per the [READme](https://github.com/lawrencerowland/Data-Model-for-Project-Frameworks/blob/master/Project-frameworks-by-using-NLP-with-Python-libraries/README.md)

## Prior-steps
Either Step 1 or Step 2 if you are loading new documents. 

Or if documents are already text files, then they can just be copied to the folder.

Steps 3 and 4 are optional.

# How-to-use

## Change Directory to find the portfolio text files

This code uses the OS module to select the file with the user's text-files.

## Create 1 whole Corpus
This pulls the Corpus together as one text string. 

## Save interim results to a single document
This code saves this new text files to the folder:
- Corpus_as_one_string


```python
directory= "/Users/lawrence/Documents/GitHub/Data-Model-for-Project-Frameworks/Project-frameworks-by-using-NLP-with-Python-libraries/Interim-results/"
```

```python
#e.g.
filename="Corpus_as_one_string"
f= open(directory+filename+".txt","w+") 
f.write(Corpus_as_one_string)
f.close()
```

# Next steps
Go to [Step 6](https://github.com/lawrencerowland/Data-Model-for-Project-Frameworks/blob/master/Project-frameworks-by-using-NLP-with-Python-libraries/Jupyter-notebooks/Step-6-Discover-keywords-whole-library.ipynb) to generate keywords for the whole corpus. 

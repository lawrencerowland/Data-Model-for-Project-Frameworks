# OBJECTIVE
The purpose of this repository is to provide:

1. a starting point for a usable portfolio framework with deployable working practices
2. the knowledge tools to adapt any portfolio framework for a particular business area.

## MOTIVATION
It is helpful to have a practice framework for project portfolio management that meets the needs of the organisation. This sets out how the portfolio is managed. There are several excellent standard frameworks to begin from (Praxis, Axelos MoP etc) but they are often quite general. It is recommended that your preferred framework is adapted to:

1. reflect how the portfolio is currently managed in reality
2. goes into more detail on working practices
3. is tailored to suit the particular business domain
4. is regularly updated as lessons are learned.


## Getting Started

This repository is structured as a series of independent frameworks and tool options, by folder. 

0. Nuclear project data is our example of documents from a specific project domain. You will be able to replace them with your own company documents

1. P3M Content first framework is a Project, Programme and Portfolio Framework that I prefer to use for standard portfolios, based upon building portfolios in various sectors. 

1. Orange NLP folder allows the construction of topic models for your business domain, based upon your own documents, working in No Code environment. 

2. Python NLP folder does the same, but does it by providing a low code environment using Jupyter notebooks

3. 'Project Frameworks from Example' folder shows how to take a Portfolio best practice structure, in this case from hundreds of Wikipedia project pages, and generate an initial portfolio framework hierarchy. This is useful if you have a favourite portfolio management text and you wish to use that to create a portfolio practice framework from it

4. 'Related work from others' is useful publically available material on portfolio frameworks from other people /organisations, which may be useful for reference. 

## Usage

### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```

### Installing

A step by step series of examples that tell you how to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```
## Example: Setting up a project management framework in a nuclear context
...

<img src="https://github.com/lawrencerowland/Data-Model-for-Project-Frameworks/blob/master/Project%20frameworks%20by%20using%20NLP%20in%20Orange%20Datamining/Screenshot%202020-03-01%20at%2018.26.00.png" title="Topic modelling a particular business domain" alt="FVCproductions"></a>

### Document clustering and Topic modelling for a project library

From the Regulator's library, We machine-read all the different words in each document, and uncover clusters of similar documents, document outliers, and the main topics covered. 

### Why do this? 
This is a first, simple, project-management application of what is called Natural language processing. Machine-learning now allows us to can analyse words as much as we can numbers. This allows us to work with a client to understand whether what is being worked on within project libraries is the same as what Management thinks it is, or the same as what status reports say. 

### What we would be trying to achieve:

By asking a machine to understand the details of what is in this SharePoint, we gain an overview of every word written about a client. We want to see clusters of similar documents, which is another way of saying: we want to see what detailed sub-folder structure should we apply, to reflect what is actually in the documents. We also want to find unusual documents, different to all the other ones. We also want to see what topics occur frequently across all documents.

### Data:

We took 16 project-management related guidance documents from the Office of Nuclear regulation. 

This can also be applied to Excel, text and PowerPoint files, but it takes more pre-processing. 

### Outcome:  

- We found xx large main document clusters.

- We found several document outliers that look different to all the other documents and would be worth special review. 

- When we knew which clusters were of most interest to the nuclear project managers, then we would analyse that cluster in the same way.

- The model also highlighted the top ten themes across the documentation

- these, we noticed two themes (xx) which would be first topics we would explore with a client, if we were checking the health and balance of the work represented by all the documents. 

### Conclusion for project businesses

As a team gets familiar with these techniques , they can scale up ten thousand and then to a hundred thousand documents. They could apply it to all project documents at a client and so understand their whole portfolio.

The team will be able to combine machine-reading their own assessment of the portfolio issues. 

It is also a natural first step towards being able to write the first draft of a proposal automatically, and towards having chat-bots that can support customers based upon our own project body of knowledge. 

### How it is done

- Extract, transform and load the data: We turned the 422 documents into 422 text documents. We counted how many different words of every type there are in each document.

- Run Unsupervised learning: For document clusters, we identified how similar each document is to each other, and how different, depending on the count of these words per document. 

- For example, two documents that each include the words “risk, issue, challenge, delay” are likely to be similar documents. 

- In addition, an unsupervised machine learning technique called Hierarchical Dirichlet Analysis was applied, which generates a probabilistic model of what the most common topics or themes are across the documents.

- Apply the model: For document clusters, we visualised each cluster and inspected which documents are in which cluster. 

Some documents can be seen as not within any cluster- and these are the document outliers. For topic modelling, we looked at each topic to see which documents and which words are captured per topic. 

We tuned the model until we got the number of clusters and topics that made sense for a first pass from a human perspective. This would then be worked with the client and machine together, down to as much detail as needed in the areas of interest to the  portfolio team.  

## Using Open Source Tools for Project Services</span>

### Motivation for using such tools

The idea is that by using a tool within one of your existing work-flows, you will be able to do your job more quickly, accurately and effectively. I use these tools in four main ways:

better implementing a project capability improvement at the client

assisting my client to operate her portfolio , programme or project more effectively

linking up our service offerings with general and specific client challenges for sales

recording, testing, repeating, improving and sharing our own work-flows and methods.

I also find that it helps me understand better what my own current work-flow actually is, even as I try to improve it.

### Orange data-mining demonstration: natural language processing

We will use it to analyse some project documents. These documents could be client documents at the start of an assignment, or successful proposals that we have written. For client documents the purpose would be to understand what topics and project types are covered within the client, and to start to categorise each document for later use. For our proposals, the purpose would be to understand some of the characteristics of successful proposals and identify documents which are good for answering certain proposal questions. This demonstrates one way of getting started with what is called “natural language processing”. ![](/images/image1.png)

We look at which words are used within your documents, and how you can select a word that you are interested in from a word cloud, and then how you can find a list of every way that word is used in your documents, including context. You can then select the best wording you find and save it for later use.

We look for what main topics the documents cover, and which documents cover which topics. Then we look to see if different documents are associated with positive or negative sentiment.

Other things Orange is good for

Orange can also do:

some types of statistical analysis

network analysis

supervised machine learning

unsupervised machine learning

model testing and creating ensembles of models.

There are plenty of examples and documentation at their website, as well as example models from within the application.

### YEd graph editor: Portfolio exploration and programme definition

We use YEd to look at the relationships between a portfolio of programmes and projects. We see how the portfolio appears to be linked to strategy, and how outputs are intended to support the Target Operating Model for the business. We see how we only need focus on the one or two relationships at any one time. This is possible because we have used YEd to visualise the portfolio as a network of projects and relationships between projects, or other things. Where there is a lot of structure, we can visualise the hierarchical tree structure. Where things are undefined and more confusing, then we can ask YEd to visualise this as a more organic network of relationships.

![](/images/image2.png)

We have some more information about one project within one of the programmes, including its work packages. We take this from Excel into YEd and add it to our existing visualisation. We show how we can wire up some relationships to strategy and known programme risks and see this in the visualisation.

YEd is compatible with Excel: we can do all our work in Excel, using full project descriptions, and then have a look at what it looks like within YEd, and then carry on working in Excel.

We also have a quick look at a portfolio service catalogue and see whether any of these services can help our client on this programme.

### Other things YEd is good for

YEd has various example graphs you can download from the app. Or you can generate different types of dummy graph straight away to get started. YEd is a graph editor, by which it means anything which is a graph or network, with nodes connected by edges. This covers a lot of things, from folder structures and concept trees to swim lanes and process maps, to customer stories and use cases, to business operating models in UML. There are palettes for each of these.

The good thing about working in YEd is that you don’t lose the relationships you prepare when you are creating a diagram. E.g. if you prepare a diagram showing a programme structure with 20 projects and 100 work packages, then you can use what you have done in Excel, or to create a complete project folder structure, or a report.

There are many different types of layout you can apply: hierarchical, organic, circular, orthogonal, flowchart etc. And when you click on a project (or any other node), there is a separate window which shows you all projects (or other nodes) that project is related to. So, you explore your data or your design or your programme, tracing the logic step by step, to check if there is anything missing. You can also group nodes together into what is called a named graph. So, if you don’t want to see all the risks for example, then they can all be collapsed into a tidy group.

There are good export services, to pdf and image etc, and you can only show the bits of the graph that are relevant to the stakeholder you are talking to. Because there is also a web app, your client can also open a graph on their browser and interact with it, as well as just look at a static pdf.

The ideal assignment using this stuff...

Observe and record your workflow during the start of an assignment

For things you constantly re-use, find out how to make it repeatable as a set of modules

Spend 20% of your effort on assignment generating 80% of content, by using these modules

Then you have 80% of the time to figure out the hard, new client problems

At the end, turn the hard stuff into a new module, and update the other modules a bit.

### Getting Started: good books.

Structural changes in business

|                                                                                            |                                  |      |
| ------------------------------------------------------------------------------------------ | -------------------------------- | ---- |
| The WTF?\! Economy (What’s the Future and why is it up to us ?)                            | Tim O’Reilly                     | 2017 |
| The second machine age: work, progress, and prosperity in a time of brilliant technologies | Erik Brynjolfsson, Andrew McAfee | 2014 |
| Average Is Over: Powering America Beyond the Age of the Great Stagnation                   | Cowen, Tyler                     | 2013 |
| The Inevitable: Understanding the 12 Technological Forces That Will Shape Our Future       | Kevin Kelly                      | 2017 |

Enterprise work-flows

|                                                                                                                    |                 |      |
| ------------------------------------------------------------------------------------------------------------------ | --------------- | ---- |
| Accelerate: The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organizations | Nicole Forsgren | 2018 |
| The Checklist Manifesto: How to Get Things Right.                                                                  | Atul Gawande    | 2011 |

Machine learning & data science

|                                                                |                                |      |
| -------------------------------------------------------------- | ------------------------------ | ---- |
| The master algorithm                                           | Pedro Domingos                 | 2017 |
| Algorithms to Live By: The Computer Science of Human Decisions | Brian Christian, Tom Griffiths | 2017 |
| The Signal and the Noise: The Art and Science of Prediction    | Nate Silver                    | 2012 |

Innovation

|                                                               |                |        |
| ------------------------------------------------------------- | -------------- | ------ |
| The nature of technology: what it is and how it evolves       | Brian W Arthur | 2010\. |
| Where Good Ideas Come From: The Natural History of Innovation | Steven Johnson | 2010   |

Learning and development

|                                                                           |                |      |
| ------------------------------------------------------------------------- | -------------- | ---- |
| The organized mind : thinking straight in the age of information overload | Daniel Levitin | 2015 |


## Built With

* [ORANGE](//https://orange.biolab.si/) - Orange Data Mining. Fruitful and fun
* [GENSIM](https://radimrehurek.com/gensim/) - Topic modelling for humans

## Contributing

I welcome any thoughts or contributions. Please raise an issue, or get in touch. 

## Authors
* Lawrence Rowland

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* The spirit of the thing is well captured at https://doriantaylor.com/skeleton-organs-circulation-sinew-skin



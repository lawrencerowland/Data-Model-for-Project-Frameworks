# 0. Set-up data and method
- clone repository.
- apply Jupyter notebooks to your documents
- use notebook 1 to convert pdfs to text
- use notebook 5 to create library as 1 file
# 1. Automated Keyword extraction
-from ONR library
-apply notebooks 6-8,15
## Extract highest scoring words from ONR library
- scored with TextRank algorithm
/images/Keywords-for-whole-library.png
## Extract relationships between keywords
- start a few top-scoring words
- remove unhelpful words like 'include'
- algorithm also shows relationships between keywords
- show these relationships
/images/Knowledge-graph-from-keywords-1.png
## View the graph for useful patterns
- reinforce patterns by changing nodes and edges and labels.
- here,keywords were grouped into three meaningful clusters
/images/knowledge-graph-2.png
- this is the schema view of the same
/images/graph-schema-2.png
- it shows that we have added three labels for these clusters
	- e.g. we have used the orange label 'requirement' to cluster:
		- safety
		- security
## Add some second tier keywords
- now we have recognised some patterns at the highest level
- bring in other keywords, slightly lower in score
- e.g. we look down rows like this:

| Keyword          | Score               |
| ---------------- | ------------------- |
| planned          | 0.08974434485175725 |
| plans            | 0.08974434485175725 |
| plan             | 0.08974434485175725 |
| planning         | 0.08974434485175725 |
| levels           | 0.08898310012595033 |
| level            | 0.08898310012595033 |

## Use 'human-in-the-loop' filtering of keywords and topics
- e.g. here, we select 'plan' as concept, but discard 'level'
- we add the new concepts into the Knowledge Graph
/images/Keyword-graph-3.png
- we reinforce patterns: here deciding that
	- several concepts are part of the OpModel
	- two concepts are requirements
	- one concept is site/stakeholder related
- this time have decided to retain the same labels
- so the schema view is the same
/images/graph-schema-2.png
+++
# 2. Automated Topic Modelling
-Applying to ONR library
-apply notebooks 9,12,13
## Apply LDA algorithm
- Apply the following transformations to the library
	- Bag of Words model
	- TFIDF model
	- LDA model
- This generates three topics across the library
- Inspect and discard third topic for simplicity
- Each topic has certain words closely associated with the topic
- Draw out the highest scoring words for each topic
## Inspect topic results
*Topic 0 words*
- This topic is focussed around supply chain, security and operations
/images/topic0.png

*Topic 1 words*
- This topic is focussed around technology, change and safety
/images/topic 1.png

-In this case, documents partition strongly between topics

<img src="images/spread-of-topic-by-document.png" width="150">

## Reinforce topic patterns by adding edges
 - each topic was sketched on paper in a way that made sense at the time
 - obvious links were made between the topic words
/images/topic-graph.png
+++
# 3. Knowledge graph creation.
-install Neo4j Desktop or set up a Neo4j sandbox
-apply notebooks 14,16
## Bring in the Success Factors paper
- create a new graph in Neo4j
- add success factors and project services as nodes
- Groups of similar nodes have the same 'labels'.
	-i.e.'success_factor','project_service'.
## Add edges
where there are:
-  relationships between success factors
-  between project services
-  between a success factor and a project task
/images/Step-14-KG-comparator.png
- nodes are labelled accordingly
- this is the schema for the above graph
/images/schema-for-Success-paper.png
+++
## Combine the graphs
- for the ONR library, two graphs have already been created
	- one from keywords
	- one from topic model
- These are added, so there are three separate graphs
- these are three similar but different representations of projects in the sector
/images/3-graphs-together-1.png
- this is the schema for the above graph
- the labels are the same as from the input graphs

<img src="images/Combined_graph_schema.png" width="250">

+++
## View the graph for useful patterns
- seek acceptable interpretations of the knowledge graph
- reinforce these patterns by changing nodes, edges and labels.
- rationalise the graph, as a team where possible
	 - Look for useful clusters
	 - combine duplicate concepts
	 - relabel concepts 
	 - lose direct relationships where there already is an indirect relationship.
In this case, for example, we remove topics as a label, and decide that stakeholders would understand the graph best as a hierarchy in this order:

> (requirements)-->(success_factor)-->(project_service)-->(site or stakeholder) 

We arrived at that by moving nodes around until it looked like this: 
/images/strategic-view.png
+++
## Reaching Output 1: Project plan
A project-management view focusses on tasks needed. Each node was reviewed, and given a boolean property as to whether the node was a task(or implied a task). For those which are tasks - another property was added, which described that task. Displaying this sub-graph looks like this:
/images/combined_graph_WBS_linear_view.png
-this view has been organised by success-factor.
When a Cypher query is run to find only these tasks- then this becomes a work breakdown structure
+++
## Reaching Output 2: Project documentation list
In just the same way, we identify which nodes are also associated with a project document. We add a boolean property flagging this, and we also add a node property for these nodes which is a document description.
The image below shows all the documents. It is the result of running a query for all nodes where the boolean property is 1. 
/images/project_data_items-4way-view.png
The way the documents are spread out below shows how the user interacts with query results, moving nodes around, looking for project-like patterns. 
In this particular case, the user has identified a meaningful pattern by pulling apart the documents into four clusters:
1. high level definitions
2. site specific 
3. design and system descriptions
4. stakeholder and controls documents. 
+++
## Reaching Output 3: Feature list for project work-packages
This exercise has highlighted a number of features relevant to successful DeCom projects within an ONR environment. These can be identified by running a query asking for all nodes which are neighbours to project_service nodes. 

| Work-package feature           | Work-package 1 | Work-package 2 |
| ------------------------------ | -------------- | -------------- |
| Facilities affected            |                |                |
| Waste type, mass, and location |                |                |
| Radioactivity                  |                |                |
|                                |                |                |
| Relevant regulations           |                |                |
| Related specification          |                |                |
|                                |                |                |
| Licensee                       |                |                |
| Related Dutyholders            |                |                |
| Supply chain list to date      |                |                |
| Local Community Groups         |                |                |
|                                |                |                |
| Agreed ALARP level             |                |                |
| Safety performance             |                |                |
| Resilience score               |                |                |
| Security performance           |                |                |

 *What are these?*
 The attributes should be recorded and tracked per work-package.
 
 *Where should they go ?* 
 They will be captured in project records. These may be in:
- a spreadsheet or project database
- a project folder
- an Enterprise or cloud Project Management tool
Some of these features will appear in reports and dashboards.

*Why?* 
These features are a key element of the data model for the project, to represent the special characteristics of projects in this business domain. 
+++
## Reaching Output 4: Table of Contents for the Project Strategy
Many different slices of the project strategy can be proposed. For instance, if we are interested in 'Waste route' strategy, then we can run a query that asks for all nodes that are one or two 'hops' away from that node. That provides a starting point:

<img src="images/2-hop-view-partial-for-waste-routes.png" width="250">

As noted above, we have already decided the simplest overall strategy which all stakeholders will understand in this case will be one which asserts this hierarchy:
 1. requirements
 2. Success-factors
 3. project-services
 4. site

We run a Cypher query for this hierarchy and it looks like this.

 <img src="images/Strategy_TOC.png" width="120">
 
 Alternative strategy structures could have been:
1. one for finance with the business/financial'requirement' nodes at top level
2. one for Ops Directors starting from the 'site/stakeholder' nodes
 


 

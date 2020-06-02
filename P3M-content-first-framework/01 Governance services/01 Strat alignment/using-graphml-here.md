

<img src="xxx.png" width="50%">

# Viewing and editing these graphs

**[Which-Graph-app](#Which-Graph-app)** | **[How-to-view-Graph](#How-to-view-Graph)** |
**[Which-Graph-app]** 

# Which-Graph-app ?

## YEd 

YEd is best for :

- toggling between graph views (e.g. circular or organic)
- forcing a tree view
- exploring a knowledge graph for understanding of individual relationships
- making small edits to node descriptions
- removing links
- creating groups of nodes for convenience
- quick opening and inspection of grapheme files

YEd desktop is most convenient for all of the above
YEd live is great for sharing a graph

## Gephi 

Gephi is best for:

- dragging nodes around to understand the whole graph
- looking for natural groups -
- fast graph analytics -
- spreadsheet like editing of nodes and edges

## Neo4j

Best for 

- long term graph storage and management
- arranging for CSV exports of some /all data
- distinguishing clearly between database schema and instances
- seeing implied data schema
- handling attributes other than node label



# How-to-view-Graph

## YEd
Click on 'Fit node to label'


## Neo4j
CALL apoc.import.graphml("https://raw.githubusercontent.com/lawrencerowland/Data-Model-for-Project-Frameworks/master/P3M-content-first-framework/01%20Governance%20services/01%20Strat%20alignment/3-alternate-views-of-Project-management0.graphml", {})

You will need this added to the settings file (different location in 3.5 or 4.0)

apoc.import.file.enabled=true

https://neo4j.com/docs/labs/apoc/current/import/graphml/

## Gephi

Will need to change config at bottom of screen, to show d5 as the label
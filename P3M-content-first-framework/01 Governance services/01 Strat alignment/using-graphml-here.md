
# YEd
Click on 'Fit node to label'


# Neo4j
CALL apoc.import.graphml("https://raw.githubusercontent.com/lawrencerowland/Data-Model-for-Project-Frameworks/master/P3M-content-first-framework/01%20Governance%20services/01%20Strat%20alignment/3-alternate-views-of-Project-management0.graphml", {})

You will need this added to the settings file (different location in 3.5 or 4.0)

apoc.import.file.enabled=true

https://neo4j.com/docs/labs/apoc/current/import/graphml/

# Gephi

Will need to change config at bottom of screen, to show d5 as the label
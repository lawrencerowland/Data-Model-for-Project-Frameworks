<!-- wp:paragraph -->
<p>There is an excellent <a href="https://jbarrasa.com/2017/04/26/quickgraph6-building-the-wikipedia-knowledge-graph-in-neo4j-qg2-revisited/#more-4705">post</a> from <a href="https://jbarrasa.com/">Jesús Barrasa</a> showing how to add Wikidata and DBPedia information to a Neo4j graph. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>This would be a way to get started with building a knowledge graph for any topic. e.g. a knowledge base of team operations. Start from the Wikidata structure, then combine it with special team knowledge and practice. </p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>I have taken Project Management information from wikidata, placed it in Neo4j, and then visualised it in the  YfilesNeo4j Explorer. </p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":179,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="https://i1.wp.com/atmiddlenight.com/wp-content/uploads/2020/02/2020-02-P3M-categories-in-Wikipedia-Higher-structure-LR-Neo4j.png?fit=629%2C743&amp;ssl=1" alt="" class="wp-image-179"/><figcaption>Project Management categories in Wikipedia, shown in Neo4j</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>When you get down to page level, there are hundreds of nodes, so I have zoomed into one part of the graph below, by visualising the results in the excellent Yfiles Neo4j Explorer application.</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":180,"sizeSlug":"large"} -->
<figure class="wp-block-image size-large"><img src="https://i2.wp.com/atmiddlenight.com/wp-content/uploads/2020/02/2020-02-P3M-categories-in-Wikipedia-neo4j-LR.png?fit=629%2C432&amp;ssl=1" alt="" class="wp-image-180"/><figcaption>Zooming into a part of the graph with YFiles</figcaption></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>To create your own, just follow the instructions, but as per the comment at the bottom of the post change the cypher code from "doit" to 'doIt' where necessary. </p>
<!-- /wp:paragraph -->

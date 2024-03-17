# Database_Mining_BirdStrike_Incidents

[15 hrs] BUILD: Practicum II / Mine a Database
Due May 3, 2022 by 11:59pm Points 100 Submitting a file upload File Types rmd Available until May 5, 2022 at 11:59pm
This assignment was locked May 5, 2022 at 11:59pm.
Motivation
In this practicum you will extract data from an XML document and then store the data relationally in a SQLite database. That database represents a "transactional" database. Then you will extract data from the transactional database and create an "analytical" database using a star schema in MySQL. Finally, you will query facts from the MySQL analytical database. This will require that you connect to two different databases simultaneously -- a common occurrence in practice.

Format
Method: Individual or in pairs (two)
Materials: RStudio or RStudio.cloud; SQLite; MySQL (optional)

Before you begin, download the PubMed catalog (pubmed_sample.xml Download pubmed_sample.xml), save the XML file locally in the same folder as your R Notebook, and then inspect the file to familiarize yourself with its content and structure. 

Part 1 (40 pts) Load XML
In Part 1 you create a normalized relational OLTP database and populate it with data from an XML document. In Part 2 you will add to the normalized schema fact tables and turn the normalized schema into a denormalized schema suitable for OLAP. In Part 3 you'll use the OLAP star/snowflake schema to do some (simple) data mining. The parenthesis contain the maximum number of points that can be earned for that question and an estimate of the time in hours.

(0 pts / 0.1 hrs) Create an R Notebook for Part 1; Part 2 will be done in a different notebook.
(3 pts / 1 hr) Create a normalized relational schema that contains the following entities/tables: Articles, Journals, Authors. Use the XML document to determine the appropriate attributes (fields/columns) for the entities (tables). While there may be other types of publications in the XML, you only need to deal with articles in journals. Create appropriate primary and foreign keys. Where necessary, add synthetic surrogate keys. For articles you should minimally store the article title (<ArticleTitle>) and month and year created (<DateCreated>); for journals store the journal name/title, volume, issue, and publication date. For authors you should store last name, first name, initial, and affiliation.
(2 pts / 0.5 hrs) Include an image of an ERD showing your model in your R Notebook. 
(10 pts / 1 hr) Realize the relational schema in SQLite (place the CREATE TABLE statements into SQL chunks in your R Notebook). You may not use MySQL for this step.
(25 pts / 4 hrs) Extract and transform the data from the XML and then load into the appropriate tables in the database. You cannot (directly and solely) use xmlToDataFrame but instead must parse the XML using a combination of node-by-node tree traversal and XPath. It is not feasible to use XPath to extract all journals, then all authors, etc. as some are missing and won't match up. You will need to iterate through the top-level nodes. While outside the scope of the course, this task could also be done through XSLT. Do not store duplicate authors or journals. For dates, you need to devise a conversion scheme, document your decision, and convert all dates to your encoding scheme. Links to an external site.Use the appropriate tag for publication date. See this linkLinks to an external site. for information.
Part 2 (40 pts) Create Star/Snowflake Schema
(0 pts / 0.1 hrs) Create a new R Notebook for Part 2.
(10 pts / 1 hr) Create a MySQL database using either a local or a cloud MySQL instance. Connect to the database. If you use SQLite for this step, no credit will be awarded for this question.
(30 pts / 4 hrs) Create and populate a star schema for author facts. Each row in this fact table will represent one author fact. It must include the authors id, author name, number of articles by that author, the average number of articles published per year. Load the data from the SQLite Database created in Part 1 and populate the fact table using SQL commands issued from R. Do not load the entire tables from SQLite into R as that does not scale. Use SQL to get the data you need. Note that there is not a single way to create the fact table -- you may use dimension tables or you may collapse the dimensions into the fact table. Remember that the goal of fact tables is to make interactive analytical queries fast through pre-computation and storage -- more storage but better performance. This requires thinking and creativity -- there is not a single best solution. Make sure your code scales -- imagine that your transactional database (the SQLite database) contains hundreds of millions of rows per table -- would your code still work and still performance well? ETL code is not always the fastest but it must scale.
Part 3 (20 pts) Explore and Mine Data
(20 pts / 4 hrs) Write queries using your MySQL data warehouse to populate a fictitious dashboard that would allow an analyst to explore whether the number of publications show a seasonal pattern or to understand more about the publication cycle. We will, of course, not implement this dashboard fully; we'll focus on just one possible panel: the top authors. So, to test your fact table by writing a query that finds the top ten authors in terms of numbers of publications. If, for some reason, you need to update the fact table, document your changes and your reasons why the changes are needed. This requires thinking and creativity -- there is not a single best solution.  If you use SQLite for this step, maximum half the credit will be awarded for this question. Do not use any SQL GROUP BY or COUNT(*) statement -- the "facts" should already be in your tables.
Hints
if you cannot connect to a local MySQL, be sure that the MySQL Server is actually running and that you do not have firewall software running that blocks port 3306
if you cannot batch save data with dbWriteTable(), then you need to enable the setting with 
dbSendQuery(db, "SET GLOBAL local_infile = true")
if you cannot install MySQL locally, use AWS RDS or db4free.net -- see instructions on how to use these services in Practicum I; note the restriction on db4free.net that you cannot write data with dbWriteTable(); see Practicum I on tutorials for bulk loading
Submission
Submit the .Rmd files. One submission per group is sufficient; list all members of the group in all submission files and in a submission comment. Your code must run. Do not use any paths for your XML file or the database; place them in the same folder as the R Notebook so we can run it on our computers.

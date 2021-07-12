# SAGE Instructions

## What is SAGE?

SAGE is a platform that leverages the use of Linked Data and AI in order to provide Automatic Enrichments on metadata, along with a validation functionality.

## Data flow inside SAGE

`Import from source -> Map metadata to RDF -> Publish on triplestore -> Enrich metadata with the use of Annotators -> Validate the Results -> Export the results`

## How SAGE treats data

Using SAGE, you can import data from multiple sources in various formats, in order to later perform operations on them. The data is harvested from remote APIs, mapped to RDF triples, and then stored in a triple store.

The procedure that involves harvesting (gathering) data from remote APIs and converting (mapping) them to RDF triples is called the “**EXECUTION**” step of the importation of a dataset. After the execution step, the data is mapped to RDF and stored to our servers as RDF files, but not yet uploaded to the triple store (database). In this step, the user can double check to see that the operation was successful before proceeding to the actual publication.

The procedure that involves uploading RDF files to the triplestore is called the “**PUBLICATION**” procedure. After publishing, the metadata is available in the triplestore and SAGE can perform enrichments on it.

## Data Importation 

In this example, we are going to go step-by-step on how to import data from europeana to the SAGE platform

1. Go to the “Collections Import” Tab
   
<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image9.png" width="auto">

On this tab, the user has an overview of the datasets that they have already created. 

2. Click on the “+” sign next to “Dataset” in order to create a new Dataset. This opens the “Create Dataset” modal, shown below:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image12.png" width="auto">

Here, the user defines a name for the dataset they are going to create, and selects which import method to use. In our case, we will choose “Europeana Import”.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image8.png" width="auto">

Then click OK.

3. After creation, the dataset is now available in the list on the left, which as we mentioned, contains the datasets that the user has created. Click on the name of the dataset that you just created.

4. The Dataset overview window appears

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image6.png" width="auto">

Information about the dataset is appearing on the top, like if the dataset is published, the dataset name, id etc.

5. Right now the dataset is empty. It is created, but not populated with data. In order to populate it with data, the user has two different methods of import to choose from (on the case of Europeana Import):

    i) Import by QUERY </br>
    The data that will be imported will be the results of a query performed against the Europeana API

    ii) Import by COLLECTION name </br>
    Will import a whole collection from Europeana based on the name of that collection

6. <p>The user selects “Add COLLECTION” <img style="vertical-align: middle;" src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image4.png" width="auto">
 or “Add QUERY” <img style="vertical-align: middle;" src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image13.png" width="auto">
 button and the “Define parameters” section apperas</p>

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image14.png" width="auto">

Here, the user inputs a collection name (in case of collection) or a query (in case of query), plus an api key that can be obtained from europeana.

As you can see, there is a “load key” dropdown appearing, enabling the user to use one of his predefined API keys (keys can be defined in the profile section)

7. After the user inputs the parameters, the dataset is ready to be **EXECUTED**:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image7.png" width="auto">

Note: The user can use a combination of both QUERY and COLLECTION methods to create a dataset containing data from various Europeana Collections, or Europeana Queries. You just have to click again and define the new parameters. Example:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image15.png" width="auto">

8. After we have defined the parameters, we can now execute our Dataset. We click on the Actions button on our instance (the parameter set) that we want to execute, and select “Execute Instance”:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image3.png" width="auto">

9. A Status Report is opening, showing us how many items are processed:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image10.png" width="auto">


10. When the execute finishes, the output is like this:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image1.png" width="auto">

11. After the execution is completed successfully, we can now publish the dataset. To do that, we hit `Dataset Actions -> Publish` in the top right of the window:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image2.png" width="auto">

12. When the publish is over, the output is like this:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image5.png" width="auto">

13. Now that the dataset is published, we can now see its content from the “Published Collections” Tab:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image11.png" width="auto">

# SAGE Introduction

## What is SAGE?

SAGE is a platform that leverages the use of Linked Data and AI in order to provide Automatic Enrichments on metadata, along with a validation functionality.

## Data flow inside SAGE

`Import from source -> Map metadata to RDF -> Publish on triplestore -> Enrich metadata with the use of Annotators -> Validate the Results -> Export the results`

## How SAGE treats data

In SAGE, every operation on metadata is separated into 2 distinct steps: 

"**EXECUTION**": During the Execution step, the metadata is processed, enriched etc and the result is stored as RDF files, without uploading anything to the triplestore.

"**PUBLICATION**": During the Publication step, the RDF files containing the result of the execution are uploaded to the triplestore, so that further stages of the metadata processing pipeline can occur.

You will see this pattern appearing in every aspect of SAGE interaction with metadata, eg Metadata Importation, Annotator execution etc.

# Data Importation 

## Introduction

Using SAGE, you can import data from multiple sources in various formats, in order to later perform operations on them. The data is harvested from remote APIs, mapped to RDF triples, and then stored in a triple store.

During the "**EXECUTION**" step, the data is harvested and mapped to RDF triples. Those triples are stored in our servers as RDF files, but are not yet uploaded to the database (triplestore).

During the “**PUBLICATION**” step, the RDF files are uploaded to the triplestore. After publishing, the metadata is available in the triplestore and SAGE can perform enrichments and other operations on it.

## Step by step
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

6. <p>The user selects the “Add COLLECTION” <img style="vertical-align: middle;" src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image13.png" width="auto">
 or “Add QUERY” <img style="vertical-align: middle;" src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image4.png" width="auto">
 button and the “Define parameters” section is appearing</p>

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

<img  class="full-width-image" src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/image11.png" width="auto">

# Creating Enrichments

## Introduction

After the **Importation** step, the data is loaded into sage and ready to be processed by the platform.

In SAGE, the modules that are responsible for data processing and enrichment creation are called **Annotators**.

Each Annotator gets a number of metadata entries as Input, performs a specific operation, and produces Annotations (Enrichments) on the output.

Also, SAGE gives the user the option to perform **preprocess operations** on the input data (decapitalization, regex match and replace etc) in order to improve the quality of the result.

Each annotator has a specific set of properties that need to be defined.

As every data operation in SAGE, the Annotators execution operation is separated in two steps:

1. The **EXECUTION** step, where the annotator results are produced and stored as RDF files

2. The **PUBLISH** step, where the already created annotator results (enrichments) are uploaded in the triplestore database, so the next steps of the data pipeline can be performed (eg Validation)

## Available Annotators

In SAGE, the most important Annotators are:

1. AIDA Place Wikidata Annotator

2. AIDA Place Geonames Annotator

3. AIDA Wikidata Annotator

4. InThesaurus Annotator

5. Generic SPARQL Query Annotator

## Step by step

### 1. Select a Collection

Head to the *Published Collections* tab and select the Collection you want to annotate from the list on the left. Here, for example, we selected *ARME - EuropeanaFashion*.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-1.png" width="auto">

Once one of the available collection is selected from the *Published Collections* list,

### 2. View Collection Data

Once you have chosen which one of the collection’s fields you want to annotate, click on “*Actions*” the right side of that row and select “*View Values*” (image below) to get an idea of what the data looks like. Here we selected the “dc:creator” field, which contains 2022 entries represented by the number on its right.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-2.png" width="auto">

The values are sorted according to appearance frequency, as seen in the “Values” screenshot below.

### 3. Understand your Data

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-3.png" width="auto">

In order to select or create the best annotator for the task, you need to have an idea of what the data looks like. In this case we have creator names, which the annotator service will have to discover and connect to the appropriate URIs. Other times we may have plain dates, colors, numbers or even plain text like descriptions of items and sometimes (or most of the times) we will have to deal with non-normalized data - like in our case here.

We see, for example, that some names have an occupation in parentheses next to the name (e.g. “(Curator)” and other), or include a slash “/” followed by further information.

We will see how we deal with those on the Preprocessing step below, using Regular Expressions (Regex).

### 4. Add an Annotator
Now that you know what kind of data you are dealing with and what annotation method you are going to use, it’s time to add an annotator to the category.

Under the “Actions” drop-down, select the “Add Annotator” option and the New Annotator box will pop open, as seen below.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-4.png" width="auto">

#### 4.1. Select Annotator

You have many different options here, but here we’ll discuss the “Ambiverse Annotator”, “Generic SPARQL Query Annotator” and “inThesaurus Annotator".

The “**Ambiverse Annotator**” is your best bet when dealing with named entities contextualized within rich text, such as “description” fields that contain the name you want to query for. E.g. “Paris is beautifully lit during nighttime” instead of only “Paris”. Even in cases where the context is irrelevant to the named entity, this annotator tends to do better than no context at all. 

The Ambiverse Annotator employs what are referred to as Named Entity Recognition and Disambiguation tools (NERD tools). That is, methods that extract the named entities from a body of text (Recognition) and to successfully connect those entities to the corresponding entries within a knowledge base, such as Wikidata (Disambiguation). Additionally, such annotators don’t require manual pre-processing since they internally employ Named Entity Recognition tools to automatically extract the named entities, and no additional data is required to help them disambiguate the terms, making them a plug-n-play solution for general purpose enrichments.

The “**Generic SPARQL Query Annotator**” on the other hand is for occasions where you need to make more specific queries. For example: the given label needs to be of the concept “human” and have a role “occupation” and this occupation needs to be of concept “creator”, if we need our annotator to match only creators of some kind.

The "**inThesaurus Annotator**" matches terms in the text with terms of a given thesaurus/vocabulary, employing lemmatizers in order to detect variants of the thesaurus terms in the text.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-5.png" width="auto">

#### 4.2. Fill in the Details
At this point you need to fill in some details depending on the annotator you selected:

##### Ambiverse Annotator

1. **Variant**
    * “**serial execution**” (slower) - The system will execute a query for each value in the data, even if the value re-appears multiple times. If, for example, the creator “Mikael Akerfeldt” appears 20 times, twenty single identical queries will be executed.
    * “**grouped execution**” (faster) - All replications of the same value will be recognised and grouped as a single value, for which value a single query will be executed.
2. **View as** - your options are “term”, “place” and “time”. Choose accordingly, in our case we are looking for creator names so “term” is the appropriate choice.
3. **Language** - The language encoding of your input values (helps with special characters). Choose between English, German, Spanish, Russian, Czech, Chinese and others.

##### Generic SPARQL Query Annotator

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-6.png" width="auto">

1. **Variant**
    * “**serial execution”** (slower) - The system will execute a query for each value in the data, even if the value re-appears multiple times. If, for example, the creator “Mikael Akerfeldt” appears 20 times, twenty single identical queries will be executed.
    * “**grouped execution**” (faster) - All replications of the same value will be recognised and grouped as a single value, for which value a single query will be executed.
2. **View as** - your options are “**term**”, “**place**” and “**time**”. Choose accordingly, in our case we are looking for creator names so “term” is the appropriate choice.
3. **Endpoint** - The endpoint that the annotator will iconnect to for querying. In most cases you will use Wikidata’s endpoint https://query.wikidata.org/bigdata/namespace/wdq/sparql
4. **SPARQL-query-** This is where you add your custom query if you are using an annotation method that supports it, for example the Generic SPARQL Query Annotator. The SPARQL query accepts two possible variables for the SELECT function. The first one being the `?uri` and the optional variable `?score`. `?uri` is a reserved variable name for the actual enrichment/uri that the record/text will be linked too, and `?score` is another reserved name for the “confidence score” of the respective enrichment. In the example below we use `?uri` to denote the URIs connected to photographer names and we define `?score` as the fraction of 1 over the total number of all returned `?uris`. In other words, we use this `?score` variable as a gauge for how likely a returned `?uri` is to be the correct one. For example, if we get a single `?uri` as an answer, the score will be 1/1 = 1 (or 100%) that this is the right URI. But if a `?uri` is returned along with 4 others, then the likelihood of each one being the correct one is only 1/5 = 0.2 (25%).

**SPARQL-query example**
The following query, for example, returns the URIs of the entities that have an english label with the value of a Creator’s name, and furthermore that this creator has the occupation of “photographer”.

The BIND part is where we define the ?score, which represents the possibility of each returned URI being the correct one.

```
prefix rdfs:<http://www.w3.org/2000/01/rdf-schema#>
prefix wd:<http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
prefix skos:<http://www.w3.org/2004/02/skos/core#>

SELECT DISTINCT ?uri ?score WHERE {
  ?uri skos:altLabel|skos:prefLabel|rdfs:label "{@@lexicalValue@@}"@en.
  ?uri wdt:P106 wd:Q33231.

  BIND (1/?count AS ?score) {
    SELECT (COUNT(DISTINCT ?inneruri) AS ?count) WHERE {
      ?inneruri skos:altLabel|skos:prefLabel|rdfs:label "{@@lexicalValue@@}"@en.
      ?inneruri wdt:P106 wd:Q33231.
    }
  }
}
```

##### inThesaurus Annotator

1. **Variant**
    * “serial execution” (slower) - The system will execute a query for each value in the data, even if the value re-appears multiple times. If, for example, the creator “Mikael Akerfeldt” appears 20 times, twenty single identical queries will be executed.
    * “grouped execution” (usually faster) - All replications of the same value will be recognised and grouped as a single value, for which value a single query will be executed. (This option is slightly slower than the “serial execution” option only in cases where there are no duplicate values in the data, because of the overhead of the grouping task that is performed ahead of the execution.)
2. **View as** - your only option is “term” for the time being, it could also be “place” or  “time”. Choose according to what you are querying for.
3. **Thesaurus** - This is where you select the Thesaurus you want to use. The imported Thesauruses are under the “Vocabulary Import” tab, where you can add more Thesauruses if you wish.
4. **Language** - Depending on the Thesaurus you chose, here you will see the languages that this Thesaurus contains. Leave it blank if you want to search through all available languages, otherwise select one specific language that you will restrict your search into.
5. **Scheme** - Search under a specific subset of the Thesaurus only, e.g. “http://thesaurus.europeanafashion.eu/thesaurus/Colours” if you need only colors. Leave it blank to search all possible schemes.
6. **Default-text-language** - If “Autodetect-text-language” below fails or is set to False, this is the language that the query will default to.
7. **Autodetect-text-language**
    * False - No autodetection language is initiated, the query runs with the default language set above.
    * True - The tool looks for any language labels accompanying the query values and uses them as a language. If no language labels are found, it tries to parse the text and uses NLP to auto detect the language used.
    * Force - The tool will now check for language labels, instead it will try to use NLP to automatically detect what language of the text.
8. **Lemmatize** - Lemmatization uses the stem of the words in order to query. For example “red” and “reddish” or “redder” have the same stem and the tool will understand them as the same word, returning the URI for “red”. You should generally turn the lemmatizer to True, unless you want to query names or any other time you need the values to be parsed exactly as they are worded.
9. **Mode** - this is the URI schema you want to use
    * Thesaurus URI - Keeps the default URI path of the selected Thesaurus.
    * Exact match URI - Uses a custom URI path, for example if you want to use Wikidata URI or a custom Thesaurus URI - this usually applies when using custom/temporary thesauri/vocabularies that the URI of the terms is not the URI that we want for the enrichment
10. **Full-text-match**
    * True - Input the full string of the value in the query, e.g. “Elvish Priestley” would be either found as a whole or not at all.
    * False - Check the string word-by-word for possible matches, e.g. in a name Thesaurus “Elvish” and “Priestly” would be queried separately if they both existed as entities in a Thesaurus of names.

### 4.3. Preprocessing (optional)
As mentioned above, sometimes the data will need a bit of a clean-up in order to successfully return results - like in our case where some of the names we need to query are accompanied by work titles and/or special symbols like slashes.

In those cases, executing a preprocessing step in order to extract the relevant parts of the string with the use of Regular Expressions before adding them to the query, can help immensely.

In order to do this, scroll down to the “Preprocessing” section and click on the plus “+” icon in order to add a new Regex.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-7.png" width="auto">

Before adding the Regex itself, you’ll need to choose what the function will be. For example, do you need to return an “exact match” of your Regex? Do you need to “replace” it with another string or maybe make it “lowercase”?

Choose the option you need. In our case, we need to return the “exact match” or the Regex we will provide.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-8.png" width="auto">

Now add the Regular Expression and hit “Create Annotator”.

Our Regex keeps only the text before a left parenthesis `(` or a slash `/`.

⚠️ NOTE: Due to a backend issue, you need to always use **double backslash** `\\` instead of single ones when trying to escape characters.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-9.png" width="auto">

### 5. Execute the Annotator
Now that your new annotator is added to the list below, head to the “Actions” drop-down on that annotator’s row and click on “Execute”.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-10.png" width="auto">

⚠️ NOTE: Execution status does not update live. Refresh the Collection by clicking on it’s name in the Collections list on the left.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-11.png" width="auto">

During execution the notification text will write “Executing” and once the annotator is “Executed” you will also see the number of results it returned.

In our case it found “405” URIs that matched our query.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-12.png" width="auto">

If the annotator fails, it means that there is a problem with the syntax and the query cannot get executed.

If the annotator returns zero results, try another query or another annotator altogether.

### 6.  Review Annotations
Before publishing your annotations, it is advised to have a look at what your annotator actually returned. To do this, click on the “Actions” drop-down of your annotator and select “Preview Annotations”.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-13.png" width="auto">

In our example, we see that the first few URIs actually do match what seems to be the appropriate person and, on top of that, due to our Preprocessing the annotator realized that the first two entries are the same person despite the “(Designer)” suffix on the latter string.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-14.png" width="auto">

### 7. Publish Annotations
Once you have checked your annotations and everything seems as expected, it’s time to publish the annotations to the triplestore.

To do this you need to select the checkmark next to your annotator’s name, click on actions and then select the “Publish Selected Annotations” option.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-15.png" width="auto">

After the annotations are published, the notification text will read “Published” accompanied by the publication date.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/annotation-16.png" width="auto">

# Validating Enrichments

## Introduction

Once enrichments have been made, the next step is the process of validation in order to endure that the enrichments are correct and address the ones that aren't. The validation workflow goes as follows.

## Step by step

### 1. Select Editor
When you enter the Validation Dashboard for the first time you will have no Editors on your My editors list on the left.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-1.png" width="auto">

Becoming a Validator for an Editor requires you to request access from them, either you do this on your first login or later on. To do so, click on the Join Editor button and select the desired Editor.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-2.png" width="auto">

Once you select an Editor, he will be added to your My editors list, like so:

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-3.png" width="auto">

Note that, each Editor you select will get a notification of your inquiry to become a Validator for them and will decide if and which of their datasets they wish to assign to you. This process can take time, since the access and the assignments are not granted automatically.

In our case, we have already been approved by an Editor and we can see their assigned datasets by clicking on them in the My editors list.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-4.png" width="auto">

### 2. Selecting a Dataset
When the datasets that have been assigned to you have published annotations that are waiting to be validated, a Published Collections tab will appear which will take you to the main page of the validation process. In this page, you will see all your assigned datasets on the left.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-5.png" width="auto">

When clicking on the desired dataset, all information about it’s annotations and the validation process will appear on the right. For example the V&A Europeana Fashion dataset contains the fields [creator, description, title], which contain 5640, 9793 and 1206 values, respectively. Furthermore, we can see that about 35% of the creator field values have been validated.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-6.png" width="auto">

### 3. Accessing a Field
To perform a validation on a specific field, you need to click on the red window-looking icon to its right. Once you do, the Validation modal window will appear.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-7.png" width="auto">

### 4. Understanding the Validation Window

#### a. Values and Annotations

When the Validation modal window pops up it shows the values that have been annotated on the left, their annotated URI(s) on the right, along with the URI’s corresponding label underneath. For example, for the second value, the annotator found the words “wax” and “print” in its text where it highlighted them in red color, and connected them on the right with their corresponding URIs, labeled correctly “wax” and “print”.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-8.png" width="auto">

#### b. Value Frequency

The number in the center column indicates how many times this specific value appears throughout the selected field (i.e. the description field in this case). Here, the first value appears 12 times, the second 10 times and so on. The values that appear more frequently are sorted to the top of the list because, once you validate the specific annotation, your validation will automatically be applied to all those 12 instances of that value. Thus, the validation of more frequent values is considered of higher priority.

#### c. Annotation Quality

As you can also see, the annotation suggestions on the right are color coded. The meaning of these colors are:

***Green*** &rarr; More users have accepted this annotation, than rejected it

***Gray*** &rarr; No validations yet or same number of acceptances and rejections

***Red*** &rarr; The majority of the validations are rejections


#### d. Pages & Timer
On the bottom of the page you can see the total **number of pages**, as well as the number of the page you are currently on. The system takes care of allowing only a single user on each individual page.

**Note**: there is no way to manually sort the contents of each page so **pages are fixed** regarding their content. For example, “page 1” will always have those specific values in that specific order. Content from page 1 can never overflow the page and be moved to page 2 and this is true for all pages.

The **countdown timer** on the top left is just a precaution to make sure that, if a user leaves his computer with the Validation modal open, the modal will be saved and closed automatically once the time runs out. This way other validators will be allowed access to that page.

#### e. Statistics

**Statistics** about the validation process of the whole dataset (not just the field you are currently accessing) are shown on the top center. In this case, the V&A dataset has more than 50,000 annotations, 70 of which are validated (a 0.13% completion rate).

#### f. Filters
A useful tool for validating fields is the annotation filters on the top right.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-9.png" width="auto">

There are two modes on the filter **Annotated** and **Non Annotated**.

The first mode, **Annotated**, which is activated by default (blue), returns all the values that the annotators have successfully found annotations for - which is what we’ve seen until now.

Only in the Annotated mode, you have the option to select pages based on if they’ve been partially validated or fully unvalidated, by clicking on the **All** drop down button.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-10.png" width="auto">

Those three options will each return the following type of pages:

**All** - All pages, sorted by value frequency (default)
**Not Validated** - Only the pages that don’t have any validation at all. Remember that pages are fixed.
**Partially Validated** - Pages that have at least one validated annotation and at least one non-validated annotation.

*Note: by selecting any of the above filter options, the amount of pages seen on the page navigation in the bottom will not change. What will happen, is that we will be directly transferred to the first page that satisfies the selected criterion and, when clicking the “next page” button, we will be navigated to the next page that satisfies that same criterion. E.g. while looking for “Partially Validated” pages we may go from page 4, to page 7, to page 23.*

The second mode, **Non Annotated**, on the other hand, will return the values for which the annotators didn’t manage to find a relevant URI. When entering this mode, we will still see the number of appearances of each value in the center column, but the right part of the page will be empty as no annotations exist yet for it.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-11.png" width="auto">

We will show you how to add your own annotation, for both annotated and non annotated values, later on.

### 5. Validating a Value
Validating a value by Accepting or Rejecting it is quite intuitive. You simply click on the “**Check**” or the “**X**” mark on the beginning of each URI, respectively. On the screenshot below, for example, we just clicked the “accept” icon for the first value and the “reject” one for the second.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-12.png" width="auto">

As you can see, you can validate multiple values at once, before saving the page.

You can also change your validation by clicking again the same icon - to leave the annotation unvalidated, or by clicking the opposite icon to switch your validation.

In records that the same annotation target appears more than once, and thus has been annotated with the same URI on each appearance, validating one of the URIs will automatically apply the same validation to the other. Like in the example of the repeating word “Plastic” below.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-13.png" width="auto">

### 6. Adding an Annotation
If you want to add a new annotation for a value, whether this value already has an annotation or not, the process is the same. Click on the plus “+” icon on the far right of the line you want to add the annotation to.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-14.png" width="auto">

A new input field will appear, where you can paste the full URI of the annotation you want to suggest.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-15.png" width="auto">

You also have the option to delete the annotation you have added, by clicking the “bin” icon, but only if no other user has had time to validate your entry. Once an annotation is validated, you cannot delete it.

Another thing to note is that if you add a URI that this value is already annotated with, you will get an error notification pointing out that the connection of the value with that URI already exists.

*Check the Appendix if you need help on how to search manually for URIs.*

6. Saving before exiting
Once you’ve made all the desired changes to a page, you’ll need to save them by hitting “Save” on the bottom right.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-16.png" width="auto">

If you try to close the modal, by clicking the “X” button on the top right, without saving, you will receive an alert notifying you that if you close the modal, all changes will be lost.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-17.png" width="auto">

### APPENDIX - Finding Wikidata URIs Manually
Let’s say you visited a Non Annotated page and you want to start adding missing annotations on it.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-18.png" width="auto">

The logical first step is to start with the most frequent value, in this example “Madame Elizabeth Handley-Seymour”.

Let’s assume that we want to annotate using Wikidata. We can simply copy the name and paste it in a Google search, along with the keyword “wikidata” next to it, or by directly searching it in wikidata.org.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-19.png" width="auto">

Knowing that the Field we are annotating contains fashion designer names, this wikidata entry seems to be the correct one - a British fashion designer. Sometimes the signs will not be this obvious, but being validators usually implies that we have some domain expertise. So, more often than not, skimming through the Wikidata entry will reveal enough details to verify if this is the right entry.

Once we decide on the Wikidata entry, we copy it’s URL from the address bar but we also have to change the URL to a URI by changing “https” to “http” (without the ‘s’) and also changing the “wiki” to “entity”. So the URL https://www.wikidata.org/wiki/Q19873890 shown below has the URI: http://www.wikidata.org/entity/Q19873890.Then we can paste it in the annotation input of the appropriate value, as described in “Adding an Annotation” chapter above.

<img src="https://raw.githubusercontent.com/ails-lab/SAGE_Documentation/main/docs/_media/validation-20.png" width="auto">
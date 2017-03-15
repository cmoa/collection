[![DOI](https://zenodo.org/badge/9060/cmoa/collection.svg)](https://zenodo.org/badge/latestdoi/9060/cmoa/collection)

#Welcome to the Carnegie Museum of Art’s Collection Dataset. 
In celebration of our 120th anniversary, Carnegie Museum of Art is making public the collections records of all of its accessioned artworks. This release contains data on approximately 28269 objects across all departments of the museum; fine arts, decorative arts, photography, contemporary art, and the Heinz Architectural Center.  

Additionally, the metadata for the Teenie Harris Archive has been included.  For ease of use, they are contained within their own files, but it includes approximately 59031 records using the same structure and format.

In this repository, you will find the files containing all of the records, as well as a description of the data, the data structure, and some guidelines on using the data. Please take a minute to familiarize yourself with the structure and guidelines below. 

Your feedback and input is always welcome. If you’ve got questions or suggestions, please [send them our way](mailto:"webmaster@cmoa.org") with “GitHub Dataset” in the subject header. 

## Data Structure

This data release includes nearly all accessioned works in our database. It contains basic data for each work.   

The data is released in two forms, as a CSV dump (``cmoa.csv`` & ``teenie.csv``) and as a JSON dump (``cmoa.json`` & ``teenie.json``).   The data contained in both formats are identical—you may choose the form that makes most sense to you.  Please note that both the CSV and the JSON may contain newlines (``\n``) within any text field, and they often appear within the ``provenance``, ``medium`` and ``credit_line`` fields.  

For ease of use, we also provide individual JSON files for each work in the `cmoa` and `teenie` directories.  These follow the same metadata format as the bulk file download, but are smaller and easier to read. Each file is named with the GUID portion of the object's ID. We have also included an `index.json` file within that directory that lists the ID, title, and first image (when available) for each object.

## Metadata Format

### Artwork Information

Header/JSON object Key | Type           | Required?    | Description  | Example
-----------------------|----------------|--------------|--------------|------------
title                  | String         |  Mandatory   | The main title that identifies the object or artwork. No multiples. | Portrait of A Boy **OR** Wheatfields After the Rain.
creation_date          | String         |  Optional    | The human readable date of creation for the object.  Note that this is a string and may not be a valid date. | c. 1950” **OR** date unknown
creation_date_earliest | ISO_8601 date  |  Optional    | This is the earliest date the object could have been created. May be null if no date known. *May be the same as creation_date_latest, which indicates an exact date known.* | 1990-10-17 
creation_date_latest   | ISO_8601 date  |  Optional    | This is the latest date the object could have been created. May be null if no date known. *May be the same as creation_date_earliest, which indicates an exact date known.*  | 1990-10-17
medium                 | String         |  Optional    | Material of which this is this object/artwork is made. | Oil on canvas **OR** Acrylic on board **OR** Plastic, glass, and rubber
accession_number       | String         |  Mandatory   | This is a number assigned by the museum when it takes official ownership of an object. <sup>[1](#acq_note)</sup>  | 2001.45.3 **OR** 2013.29.1A-B **OR** 96.1
id                     | String (GUID)  |  Mandatory   | A unique string that identifies the record of the object in the collections database.  | 692a68c5-af1e-4124-80f1-cbf38be51abe
credit_line            | String         |  Mandatory   | Identifies and gives credit to the person, foundation, or method by which the object was acquired. | Gift of John Doe **OR**  Museum Purchase, by Exchange. 
date_acquired          | ISO_8601 date  |  Mandatory   | The date the object became the legal property of the museum. |  1990-10-17
department             | String         |  Optional    | The department within the museum that is responsible for the item. | Fine Arts *OR* Decorative Arts *OR* Photography *OR* Contemporary Art
physical_location      | String         |  Optional    | The location of the object/artwork within the museum. When an object is on view in the galleries, a specific gallery location is given. When an object is in storage, the location will only say Not on View. If an object is on loan to another institution, it will say on loan.  | Scaife Gallery 8 **OR** On loan **OR** Not on view. 
item_width             | Number         |  Optional    | The maximum width of the artwork/object in inches. | 11.5 
item_height            | Number         |  Optional    | The maximum height of the artwork/object in inches. | 11.5 
item_depth             | Number         |  Optional    | The maximum depth of the artwork/object in inches. | 14.5 
item_diameter          | Number         |  Optional    | The maximum diameter of the artwork/object in inches. | 180.53
web_url                | String         |  Optional    | The URL of the collection page for this item.  
provenance_text        | String         |  Optional    | The ownership history of an object/artwork.  <sup>[2](#prov_note)</sup>  | Mary Cassatt [1844-1926], France; Galeries Durand-Ruel, Paris, France, by August 1892 [1]; Durand-Ruel Galleries, New York, NY, 1895; purchased by Department of Fine Arts, Carnegie Institute, Pittsburgh, PA, October 1922.  NOTES: [1] Recorded in stock book in August 1892.
classification         | String         |  Optional    | The name of a group to which the work belongs within the museum's classification scheme, based on similar characteristics.| Prints OR Photographs

### Image Information

There may be more than one image associated with an artwork.  In the CSV, each column for the images *may* contain a pipe-separated list of values.  For the JSON, there will be a ``images`` key containing a nested array of objects—one for each image.

*Note that the image linked from this URL is __NOT__ released under CCO at this time.*

Header/JSON object Key | Type           | Required?    | Description  | Example
-----------------------|----------------|--------------|--------------|------------
image_url              | Array of Strings |  Optional  | The URL of a thumbnail image of the artwork.  
image_rights           | Array of Strings |  Optional  | The rights text associated with the linked image. *(not currently exported)* 

### Artist Information

Note that there may be more than one creator associated with an artwork.  In the CSV, each column for the creator *may* contain a pipe-separated list of values. For the JSON, there will be a ``creator`` key containing a nested array of objects—one for each creator.

Header/JSON object Key | Type           | Required?    | Description  | Example
-----------------------|----------------|--------------|--------------|------------
artist_id              |  String        | Mandatory    | This is a unique identifier for the artist. | 123456
party_type             |  String        | Mandatory    | This is the type of entity represented.  Possible values are: | Organization OR Person OR Collaboration
full_name              |  String        | Mandatory    | The full name of the artist, creator, or creators, who made the object. |  John Singer Sargent.
cited_name             |  String        | Mandatory    | The name of the artist as used in a standard citation, with surname first, and forename last. | Cassatt, Mary.
role                   |  String        | Optional     | Describes a person’s involvement with this object.  | designer, manufacturer, artist.
nationality            |  String        | Optional     | The nationality of the artist/creator. | French, American, Italian. 
birth_date             |  ISO_8601 date | Optional     | The birthdate of the artist/creator. Precision may vary based on how much is known about the artist | 1959-01-01 **OR** 1959
death_date             |  ISO_8601 date | Optional     | The death date of the artist/creator. Precision may vary based on how much is known about the artist | 1959-01-01 **OR** 1959
birth_place            |  String        | Optional     | Name of place of birth, with as much specificity as possible, preference is for City, Country if known. If city is unknown, then list only country. | Paris, France. 
death_place            |  String        | Optional     | Name of place of death, with as much specificity as possible, preference is for City, Country if known. If city is unknown, then list only country. | Paris, France. 



<a name="acq_note">1: Accession Number Details:</a> It is in two or more parts, each part separated by a period. The first number indicates the year it was acquired (yy or yyyyy), the middle part generally identifies the lot in which it was given, and the third number identifies the specific item within the lot. Letters are also used to identify removable parts of a specific item, such as a coffee pot(A) and the lid to the coffee pot(B). Items acquired before 1996 begin with a 2 digit year identifier, so 96.1 refers to 1896. After 1996, four digit numbers were used.

<a name="prov_note">2: Provenance Text Details:</a> The provenance is listed in chronological order, beginning with the earliest known owner. Life dates of owners, if known, are enclosed in brackets. Uncertain information is indicated by the terms “possibly” or “probably” and explained in footnotes. Dealers, auction houses, or agents are enclosed in parentheses to distinguish them from private owners. Relationships between owners and methods of transactions are indicated by punctuation: a semicolon is used to indicate that the work passed directly between two owners (including dealers, auction houses, or agents), and a period is used to separate two owners (including dealers, auction houses, or agents) if a direct transfer did not occur or is not known to have occurred. Footnotes are used to document or clarify information.


---


## Usage Guidelines 
The dataset contains the data and metadata of approximately 28269 objects in the collection of [Carnegie Museum of Art](http://www.cmoa.org) and another approximately 59031 records from the Teenie Harris Archive in Pittsburgh, PA, USA. We are providing this data without restrictions for all to enjoy. We've got a few guidelines, but we've worked hard to make this dataset as open and explorable as possible. 

Please [contact us](mailto:webmaster@cmoa.org) if you have any questions. 


### Image usage
The dataset provides links to collections images on CMOA’s [collections search page](http://www.cmoa.org/collection/), but does not provide the images themselves. 

__Images are not covered under the same license as the dataset.__

If you would like to license images of artworks in CMOA’s collection, please contact the [Rights and Reproduction Department](http://www.cmoa.org/Collection.aspx?id=17514). 


### Dataset Integrity

Collections data is provided for the purposes of exploration, education, experimentation, and fun, but it is to be used at your own risk.

Please be aware that the dataset contains incomplete data and/or errors. CMOA staff does not guarantee or provide curatorial approval for these records. 

At CMOA, research is always ongoing, and so our understanding of these objects and their metadata are subject to change. This dataset will be updated on a regular basis to reflect our current best understanding of the object. You are advised to use, or update to, the most current version of the dataset for best accuracy. 

If you have identified errors in the dataset, or have additional information to add, we welcome your feedback! Please contact us at <mailto:webmaster@cmoa.org>. 

Thanks! 

### Pull Requests

Please note that we will *not* accept pull requests for the **data** in this repository.  If you have corrections, please email them to us at <mailto:webmaster@cmoa.org> and we will forward them to the appropriate department for correction and inclusion in a future release.  We will, however, review issues and pull requests for **documentation** or other non-data content here, as well as issues or suggestions of how we could improve these releases. 

### Attribution
Our dataset is being offered under [CC0 1.0 Universal license](https://creativecommons.org/publicdomain/zero/1.0/). 

We respectfully ask that you acknowledge CMOA as a source wherever possible, in order to preserve a link to the dataset. If this data is to be cited in a publication, please cite it using this DOI: [![DOI](https://zenodo.org/badge/9060/cmoa/collection.svg)](https://zenodo.org/badge/latestdoi/9060/cmoa/collection).  By providing acknowledgement or citation, you enable others to verify, replicate, and further explore your presentation and interpretation of our data. And it’s just nice. 

### No Endorsement/Representation

Use of this dataset __does not__ grant or imply CMOA’s approval, commission, or support of your work.  CMOA retains the rights to all of its trademarks, and they are not part of the dataset. If you transform or modify to the dataset, you must clearly distinguish the resulting work as having been modified from the CMOA dataset. If you create a derivative dataset from the CMOA dataset, we ask that you consider releasing the derivative under a CC0 license, which mirrors the licensing of the CMOA dataset.

### Acknowledgement
The writers owe a debt to [MoMA](http://www.moma.org), [Tate](http://www.tate.org.uk/), and [Cooper Hewitt](http:www.cooperhewitt.org) for their help in shaping these guidelines, and their leadership in this area. Cheers! 


# SAEF_OCR
Handwriting transcription (HTR) throughput, for processing the contents of handwritten documents associated with the "Enhancing Slavery, Abolition, Emancipation, and Freedom: Primary Sources from Houghton Library for Deeper Research" grant and preparing them for deposit in [Dataverse](https://dataverse.harvard.edu/). 

![](http://matt.share.library.harvard.edu/blog/wp-content/uploads/2021/11/hou00201c00132_0001.handprint-microsoft-1.png)

## Background
### About the grant
This python notebook represents the internal (to Harvard Library) lifecycle of the OCR (Optical Character Recognition)-related component of Houghton Library’s ["Enhancing Slavery, Abolition, Emancipation, and Freedom: Primary Sources from Houghton Library (SAEF) project](https://wiki.harvard.edu/confluence/display/HoughtonTechnicalServices/FY+21+Digital+Project+-+Slavery%2C+Abolition%2C+Emancipation%2C+and+Freedom%3A+Primary+Sources+from+Houghton+Library). Regarding the grant itself, PI Dorothy Berry had this to say:

> "In the Summer of 2020 Houghton Library committed to focusing our project digitization for the upcoming year on a curated set of 2000+ rare and unique materials illustrating African American history from the 18th century through the turn of the 20th century. The project, in process with an internal Houghton team and colleagues in Imaging Services, is planned to culminate with two primary deliverables besides hundreds of newly cataloged and digitized primary sources: a DublinCore based dataset on the digitized records available through DataVerse, and an easy to access curated CURIOsity site. The project is guided by a trifecta of Harvard Library Values; Seek collaboration, Embrace diverse perspectives, Champion access".

A key sub-goal of the larger AOK SAEF grant effort is to provide researchers with usable OCR from our digitized collections material, to open possibilities for the full-text analysis of the collection at scale. While the bulk of the materials to be digitized are printed 19th century documents, which can be transcribed quite accurately by current OCR software without human oversight, there are many key documents that are resistant to traditional technologies-- particularly those documents comprising hand-written material. 

Handwritten material in our collection includes letters from famed Black abolitionists, letters from formerly enslaved peoples to the Freedmen’s Bureau, personal recollections of Gullah-Geechee sacred music, and more. Library collections, like SAEF, represent test beds for tools and systems that transcend discipline and media.


## Prior work
### Newspaper Navigator
Philosophically, the SAEF OCR workflow documented here is influenced by Ben Lee's ["Newspaper Navigator"](https://github.com/LibraryOfCongress/newspaper-navigator) project. 

Working with more than 16 million pages of digitized American newspapers, Lee, and his colleagues at the Library of Congress (where he developed this project as _Innovator in Residence_), deployed machine learning to effectively identify the content of illustrations, photographs, maps, and more. The project is notable both for its streamlined end user interface, whereby users can "train my AI" and manually curate new sub-sets of images from the collection to initiate a similarity search using [pre-trained image classification models](https://github.com/facebookresearch/detectron2/blob/main/INSTALL.md), and for the thoroughness with which Lee and company documented the origin and limitations of their source data and associated AI technologies ("See Compounded Mediation: A Data Archaeology of the Newspaper Navigator Dataset", in the Further Reading section, below). 

Where the SAEF OCR project differs from Newspaper Navigator is in 1) the lack of ground truth data and 2) the use of 3rd party, "big tech" vendor solutions for generating transcriptions of handwritten documents. As Lee and others haved noted (See: "Further Reading" section, below), bias enters machine learning workflows at multiple points, beginning with the original digitization and proceeding to the algorithmic bias that influences . It's therefore important to note, as Lee (et al. 2020) did, that 
> "[A]ny use of machine learning and artificial intelligence in the context of cultural heritage must be done with an understanding of broader socio-technical ecosystems in which the algorithms have been developed, trained, and deployed"(1).

In this way, it's useful to think about the transcriptions derived through this SAEF OCR workflow as more akin to the ["Pre-Packaged" datasets](https://news-navigator.labs.loc.gov/), which were made available as part of the Newspaper Navigator project - assuming specific caveats and limitations - for the benefit of non-technical researchers who may be seeking to get a feel for the shape of, and patterns in, unwieldy datasets. So, the workflows and technologies documented here and elswhere, while fraught, represent a low-cost, mostly automated way to begin exploring the contents of large, handwritten document collections. 

## The Code
### Inputs
The SAEF_OCR python notebook takes a comma separated value (CSV) file and associated image set, originating in the Harvard DRS (See: "Associated Tools", below). As written, the notebook requires that the CSV include at least one prexisting column, "FILE-OSN", which HL librarians identified as cannonical, for these purposes, based on batch metadata returned along with images from the DRS (see: below, for more info). 

### Outputs
The SAEF_OCR notebook returns annotated images (with transcriptions), via the HandPrint software - the core technical component of the workflow (see: "Included Technologies" section, below) -, outputs from which includes json-type transciptions (per-image), and .txt transcriptions (per image). The notebook also returns a new "OCR_LookupTable" CSV file correlatting the cannonical "FILE-OSN" image identifier string with the absolute location of each transcription output  as well as the input image location (in NextCloud). 

## Included Technologies
The iPython Notebook here moves handwritten document transcription data associated with the SAEF project between three primary platforms: Harvard's [Digital Repository Service (DRS)](https://wiki.harvard.edu/confluence/pages/viewpage.action?pageId=204385879), where the source material is archived; [NextCloud](https://nextcloud.com/), our secure, medium-term storage solution, where document image data (and metadata) are staged, and (using their desktop client), absolute filepaths are simulated for us in the Python notebook; and the [Harvard Dataverse](https://dataverse.harvard.edu/), a discipline-agnostic data hosting platform for distributing scholarship. Central to the SAEF_OCR throughput notebook is Mike Hucka's [*HandPrint*](https://github.com/caltechlibrary/handprint) library, which automates the batch loading of images to various 3rd party cloud servieces (Google, Amazon, Microsoft) for handwriting transcription. Fuzzy-search (included in the notebook), provides a means to circumvent limitations associated with low confidence results. Finally, the OCR lookup table output, used for data management, was generated through the use of the Pandas Python library. Other required python libraries include:

* [pathlib](https://docs.python.org/3/library/pathlib.html)
* [fuzzy-search](https://github.com/marijnkoolen/fuzzy-search)
* [spacy](https://spacy.io/) (See: "Downstream Applications" section, below)
* [matplotplib](https://matplotlib.org/stable/index.html)

## HTR (Handwriting Transcription) Alternatives
* [Transkribus](https://readcoop.eu/transkribus/)
* [Simple HTR](https://github.com/githubharald/SimpleHTR)

## Downstream applications
* Named Entity Recognition
  * [Introduction to Named Entity Recognition with Python](https://github.com/mchesterkadwell/named-entity-recognition)
* Topic Modeling
  * [InPho](https://inpho.github.io/topic-explorer/index.html)

## Further reading
* [“Compounded Mediation: A Data Archaeology of the Newspaper Navigator Dataset”](https://hcommons.org/deposits/item/hc:32415/) - Lee et al., 2020.
* ["The Equivalence of "Close" and "Distant" Reading; or, Toward a New OBject for Data-Rich Literary History"](https://read.dukeupress.edu/modern-language-quarterly/article/78/1/77/19924) - Katherine Bode
* ["Machine Learning + Libraries: A Report on the State of the Field"(Machine Learning + Libraries: A Report on the State of the Field"](https://apo.org.au/node/307049) - Ryan Cordell
* ["Towards Knowledge Discovery from the Vatican Secret Archives. In Codice Ratio - Episode 1: Machine Transcription of the Manuscripts"](https://dl.acm.org/doi/abs/10.1145/3219819.3219879) - Firmani et al. 2018
* [""Q i-jtb the Raven: Taking Dirty OCR Seriously"](https://muse.jhu.edu/article/674968) - Cordell 2017

## Acknowledgements
This work was funded by an internal, Harvard Library’s [Advancing Open Knowledge Grants Program], "...which seeks to advance open knowledge and foster innovation to further diversity, inclusion, belonging and anti-racism", and the code was developed in collaboration with Harvard Library's [*Research Data Management Program*](https://hlrdm.library.harvard.edu/)

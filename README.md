# SAEF_OCR
Handwriting transcriptions (HTR) throughput automation, for processing and accessing the contents of handwritten documents associated with the "Enhancing Slavery, Abolition, Emancipation, and Freedom: Primary Sources from Houghton Library for Deeper Research" grantand preparing them for deposit in [Dataverse](https://dataverse.harvard.edu/). 

## Background
### About the grant
This notebook represents the internal (to Harvard Library) lifecycle of the OCR (Optical Character Recognition) component of Houghton Library’s ["Enhancing Slavery, Abolition, Emancipation, and Freedom: Primary Sources from Houghton Library (SAEF) project](https://wiki.harvard.edu/confluence/display/HoughtonTechnicalServices/FY+21+Digital+Project+-+Slavery%2C+Abolition%2C+Emancipation%2C+and+Freedom%3A+Primary+Sources+from+Houghton+Library). Regarding the grant itself, PI Dorothy Berry had this to say:

*"In the Summer of 2020 Houghton Library committed to focusing our project digitization for the upcoming year on a curated set of 2000+ rare and unique materials illustrating African American history from the 18th century through the turn of the 20th century. The project, in process with an internal Houghton team and colleagues in Imaging Services, is planned to culminate with two primary deliverables besides hundreds of newly cataloged and digitized primary sources: a DublinCore based dataset on the digitized records available through DataVerse, and an easy to access curated CURIOsity site. The project is guided by a trifecta of Harvard Library Values; Seek collaboration, Embrace diverse perspectives, Champion access".*

A key sub-goal of the AOK SAEF grant is to provide researchers with usable OCR from our digitized objects, to open research possibilities for analysis of the collection at scale. While the bulk of the materials to be digitized are 19th century published materials which can be transcribed accurately without human oversight, there are many key documents that are resistant to traditional technologies-- particularly hand-written material. Handwritten material in our collection includes letters from famed Black abolitionists, letters from formerly enslaved peoples to the Freedmen’s Bureau, personal recollections of Gullah-Geechee sacred music, and more. Library collections, like SAEF, represent test beds for tools and systems that transcend discipline and media.


### Prior work
### Newspaper Navigator
The SAEF OCR workflow documented here takes multiple queues from Ben Lee's ["Newspaper Navigator"](https://github.com/LibraryOfCongress/newspaper-navigator) project. Working with more than 16 million pages of digitized American newspapers, Lee, and his colleagues at the Library of Congress (where he developed this project as _Innovator in Residence_), Lee deployed machine learning to effectively identify the content of illustrations, photographs, maps, and more. The project is notable both for its streamlined end user interface, whereby users can "train my AI" and manually curate new sub-sets of images from the collection and initiate a cross-collection similarity search using [pre-trained image classification models](https://github.com/facebookresearch/detectron2/blob/main/INSTALL.md). 

Where the SAEF OCR project differs from Newspaper Navigator is in 1) the lack of ground truth data and 2) the use of 3rd party, "big tech" vendor solutions for generating transcriptions of handwritten documents. As Lee (et al. 2020) suggest, In this way, it's useful to think about the transcriptions derived through this SAEF OCR workflow as more akin to the ["Pre-Packaged"] datasets

## The Code
### Inputs
The SAEF_OCR python notebook takes a comma separated value (CSV) file and associated image set. As written, the notebook requires that the CSV include at least one prexisting column, "FILE-
OSN", which we identified as cannonical based on batch metadata returned along with images from the DRS (see: below, for more info). 

### Outputs
The SAEF_OCR notebook returns annotated images (with transcriptions), .json-type transciptions (per-image), and .txt transcriptions (per image). The notebook also returns an "OCR_LookupTable" CSV file listing the location the absolute location of each output file as well as the input identifier (FILE-OSN) and input image location (in NextCloud). 

### Customizations
The project team considered engaging the "

## Associated technologies
The handwritten document transcription data associated with the SAEF project moves between three primary platforms: Harvard's [Digital Repository Service (DRS)](https://wiki.harvard.edu/confluence/pages/viewpage.action?pageId=204385879), where the source material is archived; [NextCloud](https://nextcloud.com/), our secure, medium-term storage solution, where document image data (and metadata) are staged, and the [Harvard Dataverse](https://dataverse.harvard.edu/), a discipline-agnostic data hosting platform for distributing scholarship. Central to the SAEF_OCR throughput notebook is Mike Hucka's [*HandPrint*](https://github.com/caltechlibrary/handprint) library, which automates the batch loading of images to various 3rd party cloud servieces (Google, Amazon, Microsoft) for handwriting transcription. Finally, OCR lookup table used for data management was generated through the use of the Pandas Python library.

## HTR Alternatives
*Transkribus
*Simple HTR

## Downstream applications

## Further reading
* ["The Equivalence of "Close" and "Distant" Reading; or, Toward a New OBject for Data-Rich Literary History"](https://read.dukeupress.edu/modern-language-quarterly/article/78/1/77/19924) - Katherine Bode
* ["Machine Learning + Libraries: A Report on the State of the Field"(Machine Learning + Libraries: A Report on the State of the Field"](https://apo.org.au/node/307049) - Ryan Cordell
* 

## Acknowledgements
This work was funded by an internal, Harvard Library’s [Advancing Open Knowledge Grants Program], "...which seeks to advance open knowledge and foster innovation to further diversity, inclusion, belonging and anti-racism", and the code was developed in collaboration with Harvard Library's [*Research Data Management Program*](https://hlrdm.library.harvard.edu/)

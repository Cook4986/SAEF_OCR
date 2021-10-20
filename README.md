# SAEF_OCR
Handwriting transcriptions (HTR) throughput autmation, for processing and accessing the contents of handwritten documents in "Enhancing Slavery, Abolition, Emancipation, and Freedom: Primary Sources from Houghton Library for Deeper Research" grant
## Background
### About the grant
This notebook represents the OCR (Optical Character Recognition) component of Houghton Library’s Slavery, Abolition, Emancipation, and Freedom: Primary Sources from Houghton Library (SAEF) project. Regarding the grant itself, PI Dorothy Berry had this to say:

*"In the Summer of 2020 Houghton Library committed to focusing our project digitization for the upcoming year on a curated set of 2000+ rare and unique materials illustrating African American history from the 18th century through the turn of the 20th century. The project, in process with an internal Houghton team and colleagues in Imaging Services, is planned to culminate with two primary deliverables besides hundreds of newly cataloged and digitized primary sources: a DublinCore based dataset on the digitized records available through DataVerse, and an easy to access curated CURIOsity site. The project is guided by a trifecta of Harvard Library Values; Seek collaboration, Embrace diverse perspectives, Champion access".*

A key sub-goal of the AOK SAEF grant is to provide researchers with the OCR from our digitized objects, to open research possibilities up beyond human capability. The bulk of the materials to be digitized are 19th century published materials which OCR relatively well. There are, however, many key documents that fare less well-- particularly hand-written material. Handwritten material in our collection includes letters from famed Black abolitionists, letters from formerly enslaved peoples to the Freedmen’s Bureau, personal recollections of Gullah-Geechee sacred music, and more. Library collections, like SAEF, represent test beds for tools and systems that transcend discipline and media.


### Prior work
### Newspaper Navigator

## The Code


### Inputs
The SAEF_OCR python notebook takes a comma separated value (CSV) file and associated image set. As written, the notebook requires that the CSV include at least one prexisting column, "FILE-
OSN", which we identified as cannonical based on batch metadata returned along with images from the DRS (see: below, for more info). 

### Outputs
and returns annotated images (with transcriptions), .json-type transciptions (per-image), and .txt transcriptions (per image)

### Customizations
The project team considered engaging the "

## Associated technologies
The handwritten document transcription data associated with the SAEF project moves between three primary platforms: Harvard's [Digital Repository Service (DRS)](https://wiki.harvard.edu/confluence/pages/viewpage.action?pageId=204385879); [NextCloud](https://nextcloud.com/), our secure, medium-term storage solution, where document image data (and metadata) are staged, and the [Harvard Dataverse](https://dataverse.harvard.edu/), a discipline-agnostic data hosting platform for distributing scholarship. Central to the SAEF_OCR throughput notebook is Mike Hucka's [*HandPrint*](https://github.com/caltechlibrary/handprint) library, which automates the batch loading of images to various 3rd party cloud servieces (Google, Amazon, Microsoft) for handwriting transcription. Finally, OCR lookup table used for data management was generated through the use of the Pandas Python library.

## HTR Alternatives
*Transkribus
*Simple HTR

## Downstream applications

## Further reading

## Acknowledgements
This work was funded by an internal, Harvard Library’s [Advancing Open Knowledge Grants Program], "...which seeks to advance open knowledge and foster innovation to further diversity, inclusion, belonging and anti-racism", and the code was developed in collaboration with Harvard Library's [*Research Data Management Program*](https://hlrdm.library.harvard.edu/)

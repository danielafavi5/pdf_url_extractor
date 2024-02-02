I made a 3 stage pipeline for extracting threat references from threat reports and explored two optional paths for collecting more data:

Important: Distinction from threat references and URLs
Threat references are URls that match our research criterion which is to point to non-government related resources. 

Stage 1: Data extraction

This stage is a simple combination of textlink and hyperlink extraction methods that is looped over the entire pdfs that were given initially. Textlinks are defined as URLs found in plain text and hyperlinks as URLs formatted in text. I tested this on the 4 pdfs found in the folder "threat_reports": one from ENISA , one from CISA and the las 2 from the French and British cyber authorities.The results of this stage are a csv for every threat report and are located in the "extraction_phase" folder. 

Stage 2: Data cleaning

Duplicates and incomplete URLs are ommited in this stage.Input data made of CSVs is taken from previous stage , more exacly from the "extraction_phase" folder. Results are outputed as CSVs in the "cleaning_phase" folder.

Stage 3: Data labeling

The final preprocessing stage is adding a few labels to make the filtering and analysis process easier. A few variables were created to better decide which URLs are actually threat references. The variable "Domain" is used in combination with the "is_government_domain" method in order to decide which URLs are threat references. This stage also tests if URLs are functional by means of executing a HTTP request for every URL and returns their resource type using MIME types if the request was successful. For government related domain names (domain names of URLs that return true with "is_government_domain" method) the following optional paths (which are for collecting more data to run the already made pipeline on it) might be taken:

Option 1: Extraction of more threat reports using URLs that point to pdfs

URLs that return mime_type as PDF from previous step are acessed to download the PDF. Downloaded PDFs are found in the "downloaded_threat_reports" folder. CSVs that contain information which explains from where each pdf was downloaded for every original threat report are also created.

Option 2: Extraction of more threat references using URLs that point to websites

URLs that return mime_type as HTML from previous step (file type that allows easy URL extraction) are acessed and all URLs found are extracted in a CSV file for every acessed URL.As URLs can be long a Hash function was used to create unique and valid file names for every URL.For every ectracted link its origin is mentioned in a column inside the file.
 
TODO: 
Improve the "is_government_domain" method to better decide which domain names are government related or from public institutions to better identify threat references from private institutions. Is assumed that there are less government institutions than private ones , so is better to filter out government institutions before analysis phase.

Stage 4: Data analysis 
Here simple statistics and visualisation techniques will be applied to better answer the research question 3, of whether there is an oligopoly of private companies in the public cybersecurity sector. 
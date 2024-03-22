# elicitation-using-automation-and-ai <img src='./Power Automate Cloud/Documentation/1200px-ProCredit_Holding_logo.png' width="12%" alt="Company logo" align="right"> 

## Power Automate Cloud
### Overview
This project was made on the quarterly financial reports released by the ProCredit Holding group on their website.
The main goal here was to design a use case involving Microsft and Azure solutions i.e. Power Platform and AI Builder.

Project Demonstration Video: https://drive.google.com/file/d/1DGkdSPhIYVD8KbfD3Y13AsbJXgIlO_Od/view?usp=drive_link

<img src='./Power Automate Cloud/Documentation/flow-detailed.svg' alt="Project Flow Diagram">

### Description
<ul>
  <li>The 6 PDF files present in the folder '.PDFs\Train' were used to train the AI models 'Extract custom information from the document' (this model uses Azure Form Recognizer neural model under the hood) to extract 'Consolidated statement of profit or loss' table and 'Course of business operations' text paragraph.</li>
  <li>Another pre-trained AI model for Text translation was used to translate the information extracted in English from the previous step to some of the main languages of the countries where the ProCredit Group operates i.e. German, Ukrainian, Romanian, Bosnian, and Bulgarian.</li>
  <li>The whole process of picking up the PDF files then running the AI models on it and finally saving the results as CSVs was automated using Power Automate.</li>
  <li>Azure Board was also integrated into the Power Automate flow to create a Work Item with the necessary parameters whenever the flow gets executed.</li>
  <li>The flow was tested on the 3 files present in the folder '.PDFs\Test' and the subsequent 6 CSVs generated (1 for the table and 1 for the text paragraph per PDF) are present in the folder '.CSVs'.</li>
  <li>The automation flow is present inside the folder 'Power Automate' in the zipped and unzipped format.</li>
  <li>After performing some ETL operations in Power Query on the CSVs extracted, they were then visualized in PowerBI (ProCredit Dashboard.pbix).</li>
  <li>The documentation of the flow was generated in PowerDocu (technical documentation tool for Power Automate flows and Power Apps canvas apps) that is present in the folder 'Documentation'.</li>
  <li>Project Outline.pdf contains a summary presentation of the project.</li>
</ul>

## Power Automate Desktop
### Overview
<p>The goal here was to extract the same tables using RPA that were extracted using AI Builder in Power Automate Cloud. Apart from that the Procredit website was scraped to save in Excel the Bank's location info in various countries, all the links of the Articles posted, and the total links the website has divided into categories and sub-categories.</p>
<img src='./Power Automate Desktop/Flow.png' alt="PA_Desktop Flows Image">

### Description
<p>Extraction of Table</p>
<ul>
<li>Various sets of rules were used to extract the 'Consolidated statement of profit or loss' tables from the different PDFs.</li>
<li>Firstly new instances of Excel and Chrome were launched and the PDF files were read and looped through. Then each PDF file was opened up inside Chrome and the action of searching the text 'Consolidated statement of profit or loss ' was simulated using RPA to search for the exact number of times the phrase occurs inside the PDF.</li>
<li>Using the number from above as the limit, an inner For loop was run along with the necessary simulated actions to capture the Page numbers where this phrase occurred. The goal here was to capture the correct table as it usually existed on the same page where the searched phrase was present.</li>
<li>To make the capturing of the table more accurate, some other rules were used like not considering the first 10 pages if the phrase was present there as in all of the cases this indicated the presence of the phrase in the index or a text paragraph without the table. Also, if the phrase occurred more than once on the same page where the table was present, a rule was set so that the table was not written into Excel more than once.</li>
<li>The table was then captured using the 'Extract Tables from PDF' action and was written in a new Excel Worksheet with its name taken out from the PDF file name. After extracting the necessary tables from all the PDF files, the Excel file was then saved along with the timestamp in its name to avoid overriding when the flow is run again.</li>
</ul>

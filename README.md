# cell_def_project

This repo covers two separate, but related projects, led by students that resulted in two separate posters presented in May 2026. They both relate to [PhysiCell](https://physicell.org) Cell Definitions. One project focuses on validating the XML that define Cell Definitions; the other focuses on obtaining relevant parameters (from PubMed) for Cell Definitions.

---
To get started, either clone or download this repo, or better yet, "fork" this repo into your own GitHub account and run it from there. 

In your VSCode, use `File -> Open folder` to open the directory where you cloned it.  Then in your VSCode Terminal, try running these 3 commands (we are assuming you're on Windows):
```
(base) PS C:\Users\randy\git\cell_def_project> python .\get_studio.py
...
(base) PS C:\Users\randy\git\cell_def_project> python .\download_binary_here.py template

(base) PS C:\Users\randy\git\cell_def_project> python .\studio\bin\studio.py -c .\pred_prey.xml
```
<img src="./images/vscode1.png"  width="80%">

If it all runs correctly, you should be able to click on the "Run" tab of the Studio and click "Run Simulation" (should just take a few secs to complete). Then in the "Plot" tab, click the "Play" button to play the simulation results. And click the "Population plot" (lower-left) to see how the population of both the predator and prey cells change over time.

<img src="./images/pred_prey_12h_model0.png"  width="60%">
<img src="./images/pop_plot_model0.png"  width="50%">

We will start by taking a closer look at the XML, specifically the `<cell_definition ...` contents of the model and see how those parameters map into the Studio.

<img src="./images/vscode_cell_defs.png"  width="50%">

## MultiCellDS

Multicellular Data Standard was an earlier project that was a joint effort from several modeling frameworks. It is relevant for this project.

https://www.biorxiv.org/content/10.1101/090456v2 

https://www.biorxiv.org/content/10.1101/090696v1 

## Validating XML via xmllint

```
xmllint --schema schema.xsd model_good_1.xml
xmllint --schema schema.xsd model_bad_1.xml
xmllint --schema schema.xsd model_good_1.xml
xmllint --schema schema.xsd model_bad_1.xml
```

## Validating XML via Schematron

```
pip install pyschematron
(base) M1P~/git/cell_def_project/config$ pyschematron --svrl-out results.txt book_invalid.xml lib_book_rules.sch
```

## Validating XML via XML Schema and lxml

```
# In /config, try to run and experiment with:
python validate_model.py model_bad_1.xml
python validate_model.py model_good_1.xml
```

---
# Searching PubMed for cell parameters

```
$ pip install metapub
$ python pubmed_1.py
→ possible to get: “Too Many Requests for url: https://eutils.ncbi.nlm.nih.gov”
Create/use an API key (in your NCBI account)
$ export NCBI_API_KEY="60152f7c0539bbc0…"
```

```
$ python pubmed_2.py 
Found 2 papers with accessible PDFs
[{'title': 'Generalized Lévy walks and the role of chemokines in migration of effector CD8+ T cells.', 'journal': 'Nature', 'pdf_url': 'https://www.nature.com/articles/nature11098.pdf '}, {'title': 'M2 bone marrow-derived macrophage-derived exosomes shuffle microRNA-21 to accelerate immune escape of glioma by modulating PEG3.', 'journal': 'Cancer Cell Int', 'pdf_url': 'http://www.biomedcentral.com/content/pdf/s12935-020-1163-9.pdf '}]
```

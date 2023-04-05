# Data Package

This is a data package description. See also https://docs.google.com/document/d/1rlHQ4JdwoBIS2YNCjQga1OdeMc7jLvoxs0xC3Ask7eE/edit for context. 

The sources used are [Preston et al. 2012](https://doi.org/10.1890/11-2194.1) (see also [GloBI's review of Preston et al. 2012](https://depot.globalbioticinteractions.org/reviews/globalbioticinteractions/preston2012/README.txt)). We used the NCBI Taxonomy version XYZ to align the names, and selected parasites (insert taxononic range) and hosts (insert taxonomic range) from Illinois and Wisconsin. 

To help avoid taxonomic misaligment, we adjusted the taxonomic resolution of the parasite names to be (XYZ, genus level). 

The format of the published foodweb is a table with the following columns

edgelist 

1. subject
2. kind of interaction
2. object


For example: 

subject,interactionType,object
Mosquito,eats,human


We got the interactions from 

https://depot.globalbioticinteractions.org/reviews/globalbioticinteractions/preston2012/indexed-interactions.tsv.gz

and then, only selected the "targetTaxonName" and "sourceTaxonName" columns

An example of how to create this network.csv is shown below using "bash" on a linux terminal. Similar workflows can be created using R, python, excel, whatever suits. 


```bash
curl "https://depot.globalbioticinteractions.org/reviews/globalbioticinteractions/preston2012/indexed-interactions.tsv.gz"\
 | gunzip\
 | mlr --itsvlite --ocsv cut -f sourceTaxonName,interactionTypeName,targetTaxonName\
 | mlr --csv rename sourceTaxonName,subject,targetTaxonName,object\
 > network.csv
```

with first 10 rows being:

| subject | interactionTypeName | object |
| --- | --- | --- |
| meiofauna | eats | detritus |
| Bacteria | eats | detritus |
| Dero | eats | detritus |
| Tubificidae | eats | detritus |
| Physa | eats | detritus |
| Helisoma | eats | detritus |
| Hyalella | eats | detritus |
| Simocephalus | eats | detritus |


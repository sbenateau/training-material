---
layout: tutorial_hands_on
topic_name: ecology
tutorial_name: Regional GAM
---

# Introduction
{:.no_toc}

⚠️ You might be willing to follow this tutorial if you are interested in working on a multispecies file.

❗Please be aware that this tutorial is only a complement to [refence_tutorial on regionalGAM](training-material/topics/ecology/tutorials/regionalGAM/Reference_tutorial.md) and that therefore there are some missing parts. 
Follow the steps bellow and then when indicated, you will be redirected to the complete tutorial. 

This tutorial will show how to study species phenology through the computation of abundance index and trends. It will explain you how to use different [regionalGAM](https://github.com/RetoSchmucki/regionalGAM) tools on Galaxy-E allowing you to deal with datasets containing occurences informations for various species per site and per date through a couple of years.
After a certain numbers of steps, you will be able to extract single species data and study related phenology through the years. The goal of this exercise is to be able to create abundance trend over time and biodiversity indicators. Following these indicators allow to follow trends in terms of population dynamics. You could for example try to predict the occurences of one specific species in a certain type of environnement using the prediction model of climate evolution. Based on charts that you will generate, you could try to explain the evolution of a species with environmental data (temperatures variations, modifications of the environmental conditions).
You will basically learn how to create a file on the basis of which you can create a visual material that can be quite easily understood and therefore be efficient for a large audience.


> ### Agenda
> In this tutorial, we will cover:
1. Pre-processing
> {:pre-processing}
2. Selectionning one specific species and show all corresponding data
> {:selectionning one specific species and show all corresponding data}
3. Displaying the occurence of the chosen species through the years
> {:Displaying the occurence of the chosen species through the years}
4. Conclusion 
> {:conclusion}

# Step 1: Pre-processing

The goal of the first step is to upload and prepare the file so that it will be usable for the *regional GAM* analysis (See [this warning](#inputdatawarning) for more information about the input file.
First of all, you will have to upload the files on Galaxy-E and then you might have to use some data handling tools to be able to use *regional GAM* tools.

>  ### {% icon hands_on %} Hands-on: Data upload
>
> 1. Create a new history for this tutorial and give it a proper name.
> 2. Import the following files from [Zenodo](https://zenodo.org/record/1324204#.W2BmRn7fNE4) or from a data
>    library named `regional GAM data tutorial`
>
>    ```
>    CSV dataset with several species: 
>    https://zenodo.org/record/1324204/files/Dataset%20multispecies%20Regional%20GAM.csv?download=1
>    ```
>   
> ### {% icon tip %} Tip: Importing data via links
>    >
>    > * Copy the link location
>    > * Open the Galaxy Upload Manager
>    > * Select **Paste/Fetch data**
>    > * Paste the link into the text field
>    > * Press **Start** and **Close** the window
>    {: .tip}
>
> ### {% icon comment %} Comment
>
> ⚠️ <a name="inputdatawarning"></a>Please note that the file must contain a header corresponding to: ```"SITES","SPECIES","YEAR","MONTH","DAY","COUNT"```, and that all the non numeric content must be between double quotes as "x" and that separators have to be ",". 

>    > ## Re-sampling. 
When the dataset contains many details, it lengthens the file processing time therefore it can be very useful to learn how to hide the informations you don't need. For example, the list of SITE of the dataset you are using is really long and the SITES are classified into sub-sites. Here, we will assume that your file doesn't really need be as precise and this is the reason why you have to specify you don't want the sub-sites. To create a new "down-sampled" file, you can follow these steps:   

> ### {% icon hands_on %} Hands-on: hiding some informations
>    > 1. Search for the tool `trouver et remplacer des patterns dans des colonnes` on the file on CSV with the following  parameters.
>    >  * Click on`insert checks`
>    >  * "Trouver l'expression suivante": `(\.[0-9]+)` which specifies that you don't want the sub-sites (all suites of digits following a "." character) to be taken into account.
>    >  * "Remplacement":`leave it empty`.
>    > 3. Search for the tool `tabular to CSV`and select the ouptut from **trouver et remplacer des patterns dans des colonnes**.
>    
{: .hands_on}

# Step 2: Selectionning one specific species and showing all the data corresponding to it

The second step of any Regional GAM data analysis is making sure to have one dataset of only one specific species that you will then be able to use. If you want to create a graph showing abundance evolution by years of several species, you will have to superimpose the graphs on one another. 

> ### {% icon hands_on %} Hands-on: How many species are taken into account in this dataset
>
> As the dataset is quite big and countains heterogeneous informations, you want to know wether the data are about one species or more.
> 1. Search for the tool `compter le nombre d'occurence de chaque enrégistrement`with the following parameters:
> * "Sur le jeu de données": `output`from **tabular to CSV**
> * "Compter les occurrences des valeurs présentes dans la(les) colonne(s)": `column 1`
> * "Délimité par": `tabulation`.
> * "Comment les résultats doivent t'ils être triés ?": `Avec la valeur la plus présente en premier`.
> 2. Inspect the file by clicking on the `eye` icon to check how many species are taken into account.
> > If there is only one species you can skip the following steps and go directly to the file datatype convertion step using the tool `tabular to CSV`
>
>    > ### Creating a new file concerning only the data of one species
>    > 1. Copy the name of the species you are interested in from the CSV file (for example: "Pyronia tithonus").
>    > 2. Search for the tool`filtrer des données dur une colonne en utilisant des expressions simples`with the following   parameters.
>    > * En utilisant la condition suivante: `c1=='habitat2'` replacing 'habitat2' with the name of the species (for example: `c1=='"Pyronia tithonus"'`)  
>    > * Nombre de lignes d'en-tête à passer: `1`.
>    > * You can repeat this set of actions as much as necessary, changing only the name of the species taken into account.
>    > 3. Search for the tool `tabular to CSV` with the following parameters 
>    > * Select the file you've just created 
>    > * Separators: `","`.
>    > 4. Repeat this last operation on all files if you want to work on different species. 
>    
>   > {: .comment}
>
>   > ### {% icon question %} Questions
>   >
>    > 1. How many species does your dataset take into account ?
>    > 2. What are their names ? 
>    >
>    >    <details>
>    >    <summary>Click to view answers</summary>
>    >    <ol type="1">
>    >    <li>The dataset contains informations on 2 different species. </li>
>    >    <li>Their names are "Pyronia tithonus" and	"Aglais io".</li>
>    >    </ol>
>    >    </details>
>    {: .question}

{: .hands_on}

❗❗ Now that you have done the specific steps with your multispecies dataset, you can follow this link and directly go to 


[Step 2 - Displaying the occurrence of a chosen species through the years]( training-material/topics/ecology/tutorials/regionalGAM/Reference_tutorial.md) {:target="_blank"}
https://github.com/Claraurf/training-material/blob/ecology/topics/ecology/tutorials/regionalGAM/Reference_tutorial.md#Displaying

 https://github.com/usegalaxy-eu/website/blob/master/index-metagenomics.md#tutorials
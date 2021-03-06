There are a few ways to annotate predicted TEs in a genome \
One of these relies on detection of structural TE elements (STRUCTURAL) \
Another looks for sequences with similarity to known TE elements (HOMOLOGY) 

In both cases, there are repetitive sequences called that are not necessarily TEs \
and there may be overlapping features called 

Zhikai ran EDTA to get a list of STRUCTURAL and HOMOLOGY based repetitive sequences \
I'm splitting these into the two categories to provide some summary statistics 

File used for analysis = Struct_Hom_TE_analysis.xlsx 

## STRUCTURAL
In total, 9,459 elements were identified (see image for summary) \
I'm using Bedtools subtract to determine how many Mb of the genome this represents \
To do this I am creating a .bed file of the Structural TEs and a .bed file that has the full length chromosomes \

````
#bedtools
````
![image](https://user-images.githubusercontent.com/43852873/140173354-0113f7c0-9b5e-4191-9543-b78ca9ab5fa0.png)

## STRUCTURAL_MINIMAL
Because the above includes some repetitive and/or TE elements, I am filtering a few categories \
After filtering I am left with 6,369 elements (see image below) \
Using bedtools again to determine how many Mb of the genome this represents \

````
#bedtools
bedtools subtract -a Svm_Chrs.bed -b Svm_STRUCT_TE_MINIMAL.bed > Svm_Chrs_minusSTRUCT_TEs.bed
````

![image](https://user-images.githubusercontent.com/43852873/143952866-de427389-58a5-438b-b5dd-6299b05106e9.png)


## HOMOLOGY
In total, 262,976 elements were identified (see image)
The homology based detection/annotation method identifies many addtitional genomic loci of interest\
Using bedtools again to determine how many Mb of the genome this represents \

````
#bedtools
````

![image](https://user-images.githubusercontent.com/43852873/140174719-b08cfcf9-9f91-4df8-9240-62043cb8d794.png)

## HOMOLOGY_MINIMAL
Because the above includes some repetitive and/or TE elements, I am filtering a few categories \
After filtering I am left with 188,707 elements (see image below) \
Using bedtools again to determine how many Mb of the genome this represents \

````
#bedtools
bedtools subtract -a Svm_Chrs.bed -b Svm_HomologyTE_MINIMAL.bed > Svm_Chrs_minusHomology_TEs.bed
````

![image](https://user-images.githubusercontent.com/43852873/140175165-8fcd72a9-03a0-45f6-aae3-317066032057.png)

To determine the total bp and percent homology and structural TEs I just summed the output of the bedtools subtract \
and divided this by the total length of the genome \
summarized below \
it looks like ~4% of the genome is annotated as STRUCTURAL TEs and ~29% annotated as HOMOLOGY TEs \
**I'm pretty sure this was an iterative annotation.  First Structural TEs were identified and then Homology TEs - this \
means that the sum of the two is the total amount of the genome annotated as TE (in other words, I don't think there is \
overlap in the two annotations)**

![image](https://user-images.githubusercontent.com/43852873/140373438-cb942db9-2b64-47d6-9983-873c5ca1e9b5.png)


````

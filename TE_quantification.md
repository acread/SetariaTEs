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
After filtering I am left with 6,445 elements (see image below) \
Using bedtools again to determine how many Mb of the genome this represents \

````
#bedtools
````

![image](https://user-images.githubusercontent.com/43852873/140174571-3ccb72de-5874-489e-9ec4-027491e64505.png)

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
````

![image](https://user-images.githubusercontent.com/43852873/140175165-8fcd72a9-03a0-45f6-aae3-317066032057.png)

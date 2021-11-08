**How far are TEs to differentially methylated tiles (DMTs)?**

To answer this I am taking 5 lists of DRM dependent losses \
    1.  CG-loss\
    2.  CHG-loss\
    3.  CHH-loss\
    4.  CHH-loss (includes minimal loss)\
    5.  Very high CHH sites
    
I am finding distance from either:\
    A1.  All Homology TEs (includes DE status)\
    A2.  All Milhouse TEs\
    A3.  All non-Milhouse DSTs
    
![image](https://user-images.githubusercontent.com/43852873/140659893-50b7e9e4-f23a-45a1-97bd-d6698de2f2b1.png)

**A1 - All Homology TEs to each of the DRM dep loss tiles**

````
bedtools closest -a Minimal_HomTEs.bed -b HighCGTiles_DrmDep.bed HighCHGTiles_DrmDep.bed HighCHH_DrmDep.bed HighCHH_DrmDep_and_DrmInter.bed VeryHighCHH_Tiles.bed -D a -t first -names CG CHG CHH CHH_Intermediate HyperCHH >Minimal_HomTEs.CLOSEST_DMT.txt

head Minimal_HomTEs.CLOSEST_DMT.txt 

Chr01	82346	82464	DTTSvm1G00178	CG	Chr01	123300	123400	HighCG_DrmDep	40837
Chr01	82346	82464	DTTSvm1G00178	CHG	Chr01	89600	89700	CHG_DRM_Dep	7137
Chr01	82346	82464	DTTSvm1G00178	CHH	Chr01	122700	122800	HighCHH_DrmDep	40237
Chr01	82346	82464	DTTSvm1G00178	CHH_Intermediate	Chr01	82600	82700	HighCHH_DrmIntermediate	137
Chr01	82346	82464	DTTSvm1G00178	HyperCHH	Chr01	243800	243900	98.78984652	161337
Chr01	159764	160020	DTTSvm1G00019	CG	Chr01	159800	159900	HighCG_DrmDep	0
Chr01	159764	160020	DTTSvm1G00019	CHG	Chr01	159800	159900	CHG_DRM_Dep	0
Chr01	159764	160020	DTTSvm1G00019	CHH	Chr01	157200	157300	HighCHH_DrmDep	-2465
Chr01	159764	160020	DTTSvm1G00019	CHH_Intermediate	Chr01	157300	157400	HighCHH_DrmIntermediate	-2365
Chr01	159764	160020	DTTSvm1G00019	HyperCHH	Chr01	243800	243900	98.78984652	83781
````

**A2 - All non-Milhouse DSTs TEs to each of the DRM dep loss tiles**
**Note that I'll need to bring Milhouse back for any DST summary**

````
bedtools closest -a DSTs.bed -b HighCGTiles_DrmDep.bed HighCHGTiles_DrmDep.bed HighCHH_DrmDep.bed HighCHH_DrmDep_and_DrmInter.bed VeryHighCHH_Tiles.bed -D a -t first -names CG CHG CHH CHH_Intermediate HyperCHH >DSTs.CLOSEST_DMT.txt

head DSTs.CLOSEST_DMT.txt

Chr01	6898796	6909485	DST-3	CG	Chr01	6901100	6901200	HighCG_DrmDep	0
Chr01	6898796	6909485	DST-3	CHG	Chr01	6901100	6901200	CHG_DRM_Dep	0
Chr01	6898796	6909485	DST-3	CHH	Chr01	6901100	6901200	HighCHH_DrmDep	0
Chr01	6898796	6909485	DST-3	CHH_Intermediate	Chr01	6901100	6901200	HighCHH_DrmDep	0
Chr01	6898796	6909485	DST-3	HyperCHH	Chr01	6928700	6928800	98.23485693	19216
Chr02	1303627	1312901	DST-2	CG	Chr02	1304800	1304900	HighCG_DrmDep	0
Chr02	1303627	1312901	DST-2	CHG	Chr02	1320600	1320700	CHG_DRM_Dep	7700
Chr02	1303627	1312901	DST-2	CHH	Chr02	1320400	1320500	HighCHH_DrmDep	7500
Chr02	1303627	1312901	DST-2	CHH_Intermediate	Chr02	1320400	1320500	HighCHH_DrmDep	7500
Chr02	1303627	1312901	DST-2	HyperCHH	Chr02	1265000	1265100	99.59446909	-38528

````

**A3 - All Milhouse TEs to each of the DRM dep loss tiles**

````
bedtools closest -a Milhouses.bed -b HighCGTiles_DrmDep.bed HighCHGTiles_DrmDep.bed HighCHH_DrmDep.bed HighCHH_DrmDep_and_DrmInter.bed VeryHighCHH_Tiles.bed -D a -t first -names CG CHG CHH CHH_Intermediate HyperCHH >Milhouses.CLOSEST_DMT.txt

head Milhouses.CLOSEST_DMT.txt 

Chr01	28176578	28188093	Milhouse-12	CG	Chr01	28176600	28176700	HighCG_DrmDep	0
Chr01	28176578	28188093	Milhouse-12	CHG	Chr01	28176600	28176700	CHG_DRM_Dep	0
Chr01	28176578	28188093	Milhouse-12	CHH	Chr01	28176600	28176700	HighCHH_DrmDep	0
Chr01	28176578	28188093	Milhouse-12	CHH_Intermediate	Chr01	28176600	28176700	HighCHH_DrmDep	0
Chr01	28176578	28188093	Milhouse-12	HyperCHH	Chr01	28176600	28176700	97.40672275	0
Chr01	35139743	35151209	Milhouse-11	CG	Chr01	35165600	35165700	HighCG_DrmDep	14392
Chr01	35139743	35151209	Milhouse-11	CHG	Chr01	35152400	35152500	CHG_DRM_Dep	1192
Chr01	35139743	35151209	Milhouse-11	CHH	Chr01	35150500	35150600	HighCHH_DrmDep	0
Chr01	35139743	35151209	Milhouse-11	CHH_Intermediate	Chr01	35150500	35150600	HighCHH_DrmDep	0
Chr01	35139743	35151209	Milhouse-11	HyperCHH	Chr01	35176300	35176400	97.82063113	25092

````

Using R to parse the list by context:

````R

setwd("/Users/read0094/Desktop/DMRs/MinimalTEs_DistancetoHypoDMT/")

#bedtools closest was used to find the closest CG, CHG, CHH differentially
#methylated tile to 1. all structural TEs 2. The DST transcripts identified
#by de novo transcriptome analysis 3. The Milhouse (DST1) family of TEs
#The output has 5 distances - closest to CG, CHG, CHH DMTs, a more permissive
#CHH DMT cut-off, a more restrictive CHH (hyperCHH) cut-off

Struct_TE_Closest=read.table("Minimal_HomTEs.CLOSEST_DMT.txt", sep="\t", header=FALSE)
DST_Closest=read.table("DSTs.CLOSEST_DMT.txt", sep="\t", header=FALSE)
Milhouse_Closest=read.table("Milhouses.CLOSEST_DMT.txt", sep="\t", header=FALSE)

Struct_TE_Closest_CG=subset(Struct_TE_Closest, V5 == "CG")
Struct_TE_Closest_CHG=subset(Struct_TE_Closest, V5 == "CHG")
Struct_TE_Closest_CHH=subset(Struct_TE_Closest, V5 == "CHH")
Struct_TE_Closest_CHH_Intermediate=subset(Struct_TE_Closest, V5 == "CHH_Intermediate")
Struct_TE_Closest_CHH_Hyper=subset(Struct_TE_Closest, V5 == "HyperCHH")

DST_Closest_CG=subset(DST_Closest, V5 == "CG")
DST_Closest_CHG=subset(DST_Closest, V5 == "CHG")
DST_Closest_CHH=subset(DST_Closest, V5 == "CHH")
DST_Closest_CHH_Intermediate=subset(DST_Closest, V5 == "CHH_Intermediate")
DST_Closest_CHH_Hyper=subset(DST_Closest, V5 == "HyperCHH")

Milhouse_Closest_CG=subset(Milhouse_Closest, V5 == "CG")
Milhouse_Closest_CHG=subset(Milhouse_Closest, V5 == "CHG")
Milhouse_Closest_CHH=subset(Milhouse_Closest, V5 == "CHH")
Milhouse_Closest_CHH_Intermediate=subset(Milhouse_Closest, V5 == "CHH_Intermediate")
Milhouse_Closest_CHH_Hyper=subset(Milhouse_Closest, V5 == "HyperCHH")

#I'm actually going back to the initially imported sheets and summarizing by sub-category
#Getting counts of how many of each list have elements within 500 bp, 1000 bp...
table(Struct_TE_Closest$V5, Struct_TE_Closest$V11<500)
table(Struct_TE_Closest$V5, Struct_TE_Closest$V11<1000)
table(Struct_TE_Closest$V5, Struct_TE_Closest$V11<2000)

table(Struct_TE_UP_Closest$V5, Struct_TE_UP_Closest$V11<500)
table(Struct_TE_UP_Closest$V5, Struct_TE_UP_Closest$V11<1000)
table(Struct_TE_UP_Closest$V5, Struct_TE_UP_Closest$V11<2000)

table(DST_Closest$V5, DST_Closest$V11<500)
table(DST_Closest$V5, DST_Closest$V11<1000)
table(DST_Closest$V5, DST_Closest$V11<2000)
````

I'm a little bit surprised by the results of this analysis -- it seems that relatively few homology TEs have CHH DMTs in or near the element \
**I'm wondering if this is based on the filters I've put in place - in other words, how many of these elements had the potential to be \
classified as CHH-DMTs? (they need data in both TC and Mutant)**

As an example here are the counts for within 2kb of all Struct TEs followed by within 2kb of DE-Up TEs\
`````
StructTEs w/in 2kb
                   FALSE TRUE
  CG                3742 2290
  CHG               3189 2843
  CHH               4124 1908
  CHH_Intermediate  3813 2219
  HyperCHH          5619  413
`````

`````
 DE-UP TEs w/in 2kb
                    FALSE TRUE
  CG                  15    9
  CHG                 13   11
  CHH                 20    4
  CHH_Intermediate    19    5
  HyperCHH            23    1
`````

The numbers make a bit more sense for all DSTs and all Milhouse Family

````
DSTs w/in 2kb
                   FALSE TRUE
  CG                   4    3
  CHG                  2    5
  CHH                  2    5
  CHH_Intermediate     1    6
  HyperCHH             5    2

Milhouse w/in 2kb
                   FALSE TRUE
  CG                   8    7
  CHG                  3   12
  CHH                  5   10
  CHH_Intermediate     5   10
  HyperCHH             8    7
````

To figure out how much of the Homology TEs are made up of 'missing data' in TC or MUT, I generated a file containing all 'missing data' tiles for /
each context/
These were used in bedtools subtract to determine how much of the TEs is NOT missing data
I summed this by chromosome and divided by the total Hom TE length per chromosome to determine what percent of the Hom TE annotation is 'missing data'

````
bedtools subtract -a Minimal_HomTEs.bed -b TC_missing_data.bed > Minimal_HomTEs_minus_TC_missing.txt  
bedtools subtract -a Minimal_HomTEs.bed -b MUT_missing_data.bed > Minimal_HomTEs_minus_MUT_missing.txt
````

````R
###I'm creating bed files for tiles classed as missing data in TC and MUT
TC_missing_data=subset(Complete_DRM_S_R, TC_Class=='Missing_Data')
TC_missing_data=TC_missing_data[,c("Tile","TC_Class")]

TC_missing_data.bed <- data.frame(do.call('rbind', strsplit(as.character(TC_missing_data$Tile),':',fixed=TRUE)))
TC_missing_data.bed = TC_missing_data.bed$X1
TC_missing_data2.bed = data.frame(do.call('rbind', strsplit(as.character(TC_missing_data.bed$X2),'-',fixed=TRUE)))
TC_missing_data3.bed = dplyr::bind_cols(TC_missing_data.bed,TC_missing_data2.bed,TC_missing_data)
TC_missing_data.bed=dplyr::select(TC_missing_data3.bed, "...1","X1","X2","TC_Class" )
write.table(TC_missing_data.bed,"TC_missing_data.bed",quote=FALSE,row.names=FALSE,col.names=FALSE,sep="\t")

MUT_missing_data.bed <- data.frame(do.call('rbind', strsplit(as.character(MUT_missing_data$Tile),':',fixed=TRUE)))
MUT_missing_data2.bed = data.frame(do.call('rbind', strsplit(as.character(MUT_missing_data.bed$X2),'-',fixed=TRUE)))
MUT_missing_data3.bed = dplyr::bind_cols(MUT_missing_data.bed,MUT_missing_data2.bed,MUT_missing_data)
#MUT_missing_data.bed = MUT_missing_data.bed$X1
MUT_missing_data.bed=dplyr::select(MUT_missing_data3.bed, "X1...1","X1...3","X2...4","MUT_Class" )
write.table(MUT_missing_data.bed,"MUT_missing_data.bed",quote=FALSE,row.names=FALSE,col.names=FALSE,sep="\t")

#I used bedtools to subtract the missing data from the Homology TE annotation
TE_less_TC_missing=read.table("Minimal_HomTEs_minus_TC_missing.txt",header=FALSE, sep="\t")
TE_less_TC_missing$len=TE_less_TC_missing$V3-TE_less_TC_missing$V2+1
TE_less_TC_missingtable=aggregate(TE_less_TC_missing$len, by=list(Category=TE_less_TC_missing$V1), FUN=sum)

TE_less_MUT_missing=read.table("Minimal_HomTEs_minus_MUT_missing.txt",header=FALSE, sep="\t")
TE_less_MUT_missing$len=TE_less_MUT_missing$V3-TE_less_MUT_missing$V2+1
TE_less_MUT_missingtable=aggregate(TE_less_MUT_missing$len, by=list(Category=TE_less_MUT_missing$V1), FUN=sum)

##read in TE by chromosome file
TE_len_byChr=read.table("Len_Annot_HomTE.txt",header=FALSE, sep="\t")

TE_less_TC_missingtable$len=TE_len_byChr$V1
TE_less_TC_missingtable$percentmissing=(1-(TE_less_TC_missingtable$x/TE_less_TC_missingtable$len))*100

TE_less_MUT_missingtable$len=TE_len_byChr$V1
TE_less_MUT_missingtable$percentmissing=(1-(TE_less_MUT_missingtable$x/TE_less_MUT_missingtable$len))*100
````

TC
````
  Category       x     len percentmissing
1    Chr01 1150684 1540108       25.28550
2    Chr02 1756723 2287856       23.21532
3    Chr03 1693599 2273608       25.51051
4    Chr04 1262381 1674914       24.63010
5    Chr05 1340038 1786372       24.98550
6    Chr06 1134988 1542670       26.42704
7    Chr07  962026 1350649       28.77306
8    Chr08 1414941 2069019       31.61295
9    Chr09 1842116 2358367       21.89019
````
MUT
````
  Category       x     len percentmissing
1    Chr01 1152647 1540108       25.15804
2    Chr02 1757153 2287856       23.19652
3    Chr03 1696237 2273608       25.39448
4    Chr04 1269568 1674914       24.20100
5    Chr05 1337578 1786372       25.12321
6    Chr06 1137349 1542670       26.27399
7    Chr07  955727 1350649       29.23942
8    Chr08 1415664 2069019       31.57801
9    Chr09 1850686 2358367       21.52680
````


**In summary - about 25% of the homology TE annotation is 'missing data' -- I haven't extended this to the region surrounding \
the TEs - which might make sense given that this is where I'm looking for the closest DMT...**

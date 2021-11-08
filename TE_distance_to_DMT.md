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
````

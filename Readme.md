## BINP29 Population Genetic Projects 
### Topic: Write a software that calculates the minor allele frequency data over time for ancient DNA data.   

#### Download data and software
Environment setting：   
```
Windows system
conda version : 4.13.0  
Python: 3.10.4  
```

```
 mkdir BINP29_Project
 cd BINP29_Project
 
 # download data 
 wget https://github.com/sarabehnamian/Origins-of-Ancient-Eurasian-Genomes/raw/main/steps/Step%200/DataS1.bed
 wget https://github.com/sarabehnamian/Origins-of-Ancient-Eurasian-Genomes/raw/main/steps/Step%200/DataS1.bim
 wget https://github.com/sarabehnamian/Origins-of-Ancient-Eurasian-Genomes/raw/main/steps/Step%200/DataS1.fam 
 
 #download software "plink"
 wget https://s3.amazonaws.com/plink1-assets/plink_win64_20220402.zip                                                                    
 sudo apt-get install unzip
 unzip plink_win64_20220402.zip
 ```

Now we will get these files below:  
```
DataS1.bed  DataS1.bim  DataS1.fam  LICENSE  plink.exe  plink_win64_20220402.zip  prettify.exe  toy.map  toy.ped
```

#### Preparing data
Converting format from `.bed/.bim/.fam` into `.ped` and `.map`, using plink. Obtain `DataS1.ped` and `DataS1.map`. 
Open command line in windows, and type the command below:  
```
plink --bfile DataS1 --recode --out DataS1 
```
We will get three new file: `DataS1.ped`, `DataS1.map`,`DataS1.log`  

Extract list of rs IDs from bim file. Obtain `SNP_list.txt`
```
cut -f2 DataS1.bim > SNP_list.txt 
```


确认.ped文件列数 `awk -F' ' '{print NF; exit}' DataS1.ped `   等于147299*2+6  

 
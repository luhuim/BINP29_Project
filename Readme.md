## BINP29 Population Genetic Projects 
### Topic: Write a software that calculates the minor allele frequency data over time for ancient DNA data.   

#### Download data and software
Environment setting：   
```
Windows system（改成Linux系统）
conda version : 4.13.0  
Python: 3.10.4  
```

```
 mkdir BINP29_Project
 cd BINP29_Project
 
 # download data （这部分两个系统是一样的）
 wget https://github.com/sarabehnamian/Origins-of-Ancient-Eurasian-Genomes/raw/main/steps/Step%200/DataS1.bed
 wget https://github.com/sarabehnamian/Origins-of-Ancient-Eurasian-Genomes/raw/main/steps/Step%200/DataS1.bim
 wget https://github.com/sarabehnamian/Origins-of-Ancient-Eurasian-Genomes/raw/main/steps/Step%200/DataS1.fam 
 wget https://github.com/sarabehnamian/Origins-of-Ancient-Eurasian-Genomes/raw/main/steps/Step%203/mergq.xlsx 
 
 #download software "plink"（改成linux系统）
 wget https://s3.amazonaws.com/plink1-assets/plink_win64_20220402.zip                                                                    
 sudo apt-get install unzip （改成linux系统）
 unzip plink_win64_20220402.zip
 ```

Now we will get these files below:  （改成linux系统）
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
P.S. 确认.ped文件列数 `awk -F' ' '{print NF; exit}' DataS1.ped `   等于147299*2+6  

#### 
Convert `.xlsx` into `.csv`
```
#这一步是在Linux系统上做的
for i  in *.xlsx; do  libreoffice --headless --convert-to csv "$i" ; done 
```
Obtaining file `mergq.csv`
extract the column of time, and remove the first row.
```
cut -d, -f11 mergq.csv >time.csv
sed '1d' time.csv >time_1.csv
```

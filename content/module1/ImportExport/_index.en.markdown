---
date: "2016-04-09T16:50:16+02:00"
title: Import Data to R
output: 
  learnr::tutorial
weight: 8
---

It’s the first big hurdle to dealing with data in R. 

You are most likely to have looked at, organised and examined your data files in Excel.

Opening data in R is fairly simply, but organising it for analysis might take some thought and consideration. You'll guess that it is possible to use the **File | Import Dataset** menu option in RStudio to import your data (to learn more see [Importing Data with RStudio](https://support.rstudio.com/hc/en-us/articles/218611977-Importing-Data-with-RStudio)), however we’re going to do it the proper way with a command.

R can import all types of data:

- (Tab, Blank space) Delimited Text
- CSV files
- Excel files
- JSON 
- SAS
- STATA
- MiniTab
- SPSS...

In this section we will show you how to access most commonly used data types. Once you start playing with the data and wrangling it in the way it suits you for your analytical manipulations you might find it interesting to explore the options for writing data. Here, we are not going to show you how to do it, but rather focus on basic `read` data functionality in R. 

### the R base

The simplest data form is a [text file](https://en.wikipedia.org/wiki/Text_file). Text files can be read by any computer operating system and by almost all different kind of statistical programs. Saving data as a text file makes your data highly accessible. If you have a text data file you wish to use, you can easily import it with **the R base** functions `read.table()`

This reads a file in table format and creates a data frame from it

```
# Read tabular data into R
df_txt <- read.table(file_name.txt, header = FALSE)
```

There are many packages that let R import all types of data, and we will start by focusing on `CSV` files as they are the most frequent type.

Comma separated files are the most common way to save spreadsheets that don’t require a licenced, usually not free program to open. Importing `CSV` is part of base R and you can use `read.csv()` function to do so. 


##### `read.csv()`

Let us go to <https://data.gov.rs/> Serbian open data portal. In particular, let us try to access [Kvalitet vazduha 2017: pm2.5_2017.csv](https://data.gov.rs/sr/datasets/kvalitet-vazduha-2017/) and import this data to R.

We are not going to download it onto our local computers, but rather we will import it to R directly from the web using the link provided.


```r
df_csv <- read.csv("http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/62983880-6fcd-4c65-b57c-fd4de5c367c8/download/pm2.5_2017.csv", stringsAsFactors = FALSE)
head(df_csv, 10)
```

```
##        Datum Nis_IZJZ.Nis
## 1   1.1.2017    132.04583
## 2   2.1.2017    124.95417
## 3   3.1.2017     79.92500
## 4   4.1.2017    107.22500
## 5   5.1.2017     42.14583
## 6   6.1.2017     18.12500
## 7   7.1.2017     25.14167
## 8   8.1.2017     67.86667
## 9   9.1.2017     41.41667
## 10 10.1.2017     55.75417
```
The other way is to download it and to save it to your working directory.

Let us download ["Kvalitet vazduha 2017-SO2: 2017-SO2.csv"](https://data.gov.rs/sr/datasets/r/f425e6a5-95ae-4e2b-ab73-1d0b293b4522)
Make sure you save the file into your R-Project working directory before you ask R to execute the following

```
df_csv <- read.csv("2017-so2.csv", stringsAsFactors = FALSE, fileEncoding = "latin1")
```

{{% notice info %}}
Run the above code again, but remove `stringsAsFactors` argument from the `read.csv` function or set it to TRUE. Can you tell the difference between now and before? Why do you think we had to use `fileEncoding` argument?
{{% /notice %}}

What do you think about this dataset? 🤔

#### Using readr::read_csv()

`readr` is a package that reads rectangular data more quickly than **base R** `read.cdv()`. Another difference from the `read.csv()` function is that it assumes characters are strings and not factors by default.

Just so you can see how easy it is to use other packages for importing data into R, the code below illustrates the use of read_csv().

```
## If you don't have readr installed yet, uncomment and run the line below
# install.packages("readr")
library(readr)
df_csv <- read_csv("air_quality_by_station.csv")
df_csv
```

{{% notice note %}}
Check the `readr::read_delim()` function for more efficient delimited data file reading.
{{% /notice %}}

### Importing Excel files with `readxl`

Importing Excel data files is not straightforward as it might contain multiple sheets. We will focus on using the `readxl` package as it is the most efficient so far.  

{{% notice warning %}}
To access the data from an Excel sheet you can’t just copy and paste the URL for the file. You have to download the file first.
{{% /notice %}}

Let us download an Excel data file from [data.gov.rs](https://data.gov.rs/) about traffic accidents [Подаци о саобраћајним незгодама до 31.08.2019. године за територију свих ПОЛИЦИЈСКИХ УПРАВА и ОПШТИНА](https://data.gov.rs/sr/datasets/r/134b2867-8a35-4f00-ac48-1610dca177ec). 

If you are unable to open the file in Excel to examine how many sheets the file has, try to read the file in R accessing the first one by specifying it in the `read_excel()` function as required. As previously, make sure you save the file into your R-Project working directory before you ask R to execute the following:

```
## If you don't have readxl installed yet, uncomment the line below and run it 
#install.packages("readxl")
library(readxl)
df_xl <- read_excel("nez-opendata-20199-20190925.xlsx", sheet = 1)
```

What do you think?

{{% notice warning %}}
People like to make their Excel spreadsheets look 'pretty' with 'fancy' formatting, which could create difficulty when reading them in R.
{{% /notice %}}

Explore the arguments of the `read_excel()` function, such as the `skip` argument through which you can specify a minimum number of rows to skip before reading anything.

### Importing data using `jsonlite`

When accessing JSON file in R using the `jsonlite` package you need to point to the file by providing the local path if the file is downloaded or by the URL from where it could be accessed. 


```r
## If you don't have readxl installed yet, uncomment the line below and run it 
#install.packages("jsonlite")
library(jsonlite)
my_url <-"https://data.gov.rs/sr/datasets/r/41c2fe91-4ea1-4a64-b33c-183665ea6ab3"
polen <- fromJSON(my_url)
```

Check the structure of the `polen`! 😰


```r
str(polen)
```

```
## List of 4
##  $ count   : int 26419
##  $ next    : chr "http://polen.sepa.gov.rs/api/opendata/pollens/?page=2"
##  $ previous: NULL
##  $ results :'data.frame':	500 obs. of  4 variables:
##   ..$ id            : int [1:500] 539 805 1078 1351 1624 1897 2170 2686 2965 3238 ...
##   ..$ location      : int [1:500] 12 3 4 20 5 10 14 13 17 9 ...
##   ..$ date          : chr [1:500] "2016-02-01" "2016-02-01" "2016-02-01" "2016-02-01" ...
##   ..$ concentrations:List of 500
##   .. ..$ : int [1:4] 3002 3003 3004 3005
##   .. ..$ : int [1:3] 4649 4650 4651
##   .. ..$ : int [1:3] 6126 6127 6128
##   .. ..$ : int(0) 
##   .. ..$ : int(0) 
##   .. ..$ : int [1:2] 10767 10768
##   .. ..$ : int [1:3] 12370 12371 12372
##   .. ..$ : int [1:2] 15518 15519
##   .. ..$ : int [1:4] 17422 17423 17424 17425
##   .. ..$ : int [1:2] 19339 19340
##   .. ..$ : int [1:4] 21104 21105 21106 21107
##   .. ..$ : int [1:3] 24123 24124 24125
##   .. ..$ : int [1:2] 26010 26011
##   .. ..$ : int 29460
##   .. ..$ : int [1:2] 1480 1481
##   .. ..$ : int [1:4] 3006 3007 3008 3009
##   .. ..$ : int 4652
##   .. ..$ : int [1:2] 6129 6130
##   .. ..$ : int(0) 
##   .. ..$ : int(0) 
##   .. ..$ : int [1:4] 10769 10770 10771 10772
##   .. ..$ : int [1:3] 12373 12374 12375
##   .. ..$ : int [1:5] 15520 15521 15522 15523 15524
##   .. ..$ : int [1:5] 17426 17427 17428 17429 17430
##   .. ..$ : int [1:3] 19341 19342 19343
##   .. ..$ : int [1:3] 21108 21109 21110
##   .. ..$ : int [1:3] 24126 24127 24128
##   .. ..$ : int [1:3] 26012 26013 26014
##   .. ..$ : int [1:3] 29461 29462 29463
##   .. ..$ : int [1:5] 1482 1483 1484 1485 1486
##   .. ..$ : int [1:3] 3010 3011 3012
##   .. ..$ : int [1:3] 4653 4654 4655
##   .. ..$ : int [1:2] 6131 6132
##   .. ..$ : int(0) 
##   .. ..$ : int(0) 
##   .. ..$ : int [1:3] 10773 10774 10775
##   .. ..$ : int [1:3] 12376 12377 12378
##   .. ..$ : int [1:3] 15525 15526 15527
##   .. ..$ : int [1:4] 17431 17432 17433 17434
##   .. ..$ : int [1:3] 19344 19345 19346
##   .. ..$ : int [1:5] 21111 21112 21113 21114 21115
##   .. ..$ : int [1:6] 24129 24130 24131 24132 24133 24134
##   .. ..$ : int [1:4] 26015 26016 26017 26018
##   .. ..$ : int [1:3] 29464 29465 29466
##   .. ..$ : int [1:3] 1487 1488 1489
##   .. ..$ : int 3013
##   .. ..$ : int [1:3] 4656 4657 4658
##   .. ..$ : int [1:3] 6133 6134 6135
##   .. ..$ : int(0) 
##   .. ..$ : int 9357
##   .. ..$ : int [1:5] 10776 10777 10778 10779 10780
##   .. ..$ : int [1:3] 12379 12380 12381
##   .. ..$ : int [1:3] 15528 15529 15530
##   .. ..$ : int [1:2] 17435 17436
##   .. ..$ : int [1:3] 19347 19348 19349
##   .. ..$ : int [1:2] 21116 21117
##   .. ..$ : int [1:3] 24135 24136 24137
##   .. ..$ : int [1:3] 26019 26020 26021
##   .. ..$ : int [1:3] 29467 29468 29469
##   .. ..$ : int [1:3] 1490 1491 1492
##   .. ..$ : int 3014
##   .. ..$ : int [1:2] 4659 4660
##   .. ..$ : int [1:3] 6136 6137 6138
##   .. ..$ : int(0) 
##   .. ..$ : int 9358
##   .. ..$ : int [1:3] 10781 10782 10783
##   .. ..$ : int [1:3] 12382 12383 12384
##   .. ..$ : int 15531
##   .. ..$ : int [1:3] 17437 17438 17439
##   .. ..$ : int [1:2] 19350 19351
##   .. ..$ : int [1:5] 21118 21119 21120 21121 21122
##   .. ..$ : int [1:3] 24138 24139 24140
##   .. ..$ : int [1:3] 26022 26023 26024
##   .. ..$ : int [1:4] 29470 29471 29472 29473
##   .. ..$ : int [1:3] 1493 1494 1495
##   .. ..$ : int [1:2] 3015 3016
##   .. ..$ : int 4661
##   .. ..$ : int [1:3] 6139 6140 6141
##   .. ..$ : int 7747
##   .. ..$ : int 9359
##   .. ..$ : int [1:3] 10784 10785 10786
##   .. ..$ : int [1:3] 12385 12386 12387
##   .. ..$ : int [1:3] 15532 15533 15534
##   .. ..$ : int [1:3] 17440 17441 17442
##   .. ..$ : int [1:3] 19352 19353 19354
##   .. ..$ : int [1:3] 21123 21124 21125
##   .. ..$ : int [1:4] 24141 24142 24143 24144
##   .. ..$ : int [1:3] 26025 26026 26027
##   .. ..$ : int [1:3] 29474 29475 29476
##   .. ..$ : int [1:5] 1496 1497 1498 1499 1500
##   .. ..$ : int [1:2] 3017 3018
##   .. ..$ : int 4662
##   .. ..$ : int [1:3] 6142 6143 6144
##   .. ..$ : int(0) 
##   .. ..$ : int [1:2] 9360 9361
##   .. ..$ : int [1:3] 10787 10788 10789
##   .. ..$ : int 12388
##   .. ..$ : int [1:5] 15535 15536 15537 15538 15539
##   .. ..$ : int [1:3] 17443 17444 17445
##   .. .. [list output truncated]
```

```r
names(polen)
```

```
## [1] "count"    "next"     "previous" "results"
```

Note that the `polen$results` is a data frame with a list `concentrations` inside as its element.

Ouch! 😳 JSON files are not very neat 😱 They are more than often nested, chained -> you’ve got it: Very Messy! 😫 So, we will leave it there. 😬 If you do need to learn more about reading JSON files in R you can explore the functionality of the `jsonlite` package further by reading [Getting started with JSON and jsonlite](https://cran.r-project.org/web/packages/jsonlite/vignettes/json-aaquickstart.html). Blog post [Working with JSON data in very simple way](https://blog.exploratory.io/working-with-json-data-in-very-simple-way-ad7ebcc0bb89) by [Kan Nishida](https://blog.exploratory.io/@kanaugust) provides a great example of how this data format can be used in R. 

### Other data formats

To speed up the reading process of txt, csv data files you can use the `data.table::fread()` function. You should only pass to the function the name of the data file you want to import, and `fread()` will try to work out the appropriate data structure. Check out this blog post [Getting Data From An Online Source](https://www.r-bloggers.com/getting-data-from-an-online-source/) for some more ideas. 

You can use R with appropriate packages to access other data formats. The `haven` package provides functions for importing SAS, SPSS and Stata file formats or you can use the `foreign` package for MiniTab portable worksheet data files. Try to look through the help section of the packages you've been introduced to and discover other options.


## YOUR TURN 👇

1) See if you can find data from <https://data.gov.rs/> about a topic you’re interested in.

2) Have a look at this data set: [saobracaj](https://data.gov.rs/sr/datasets/podatsi-o-saobratshajnim-nezgodama-po-politsijskim-upravama-i-opshtinama/). Think about the questions you can answer based on this data.

-----------------------------
© 2019 [Siste Analyst](https://sisteranalyst.org)

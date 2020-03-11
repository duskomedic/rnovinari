---
date: "2016-04-09T16:50:16+02:00"
title: Učitavanje podataka u R
output: 
  learnr::tutorial
weight: 8
---

Učitavanje podataka je prva velika stvar u upravljanju podacima u R-u. 

Najverovatnije je da već imate iskustvo u pregledanju, organizovanju i istraživanju podataka u Excel-u.

Otvaranje podataka u R-u je prilično jednostavno, ali njihova priprema za analizu  iziskuje više truda i promišljanja. Dobro pretpostavljate da pomoću komandi iz glavnog menija **File | Import Dataset**  u R studiju možete učitati vaše podatke (za više pogledajte [Importing Data with RStudio](https://support.rstudio.com/hc/en-us/articles/218611977-Importing-Data-with-RStudio)), međutim mi ćemo to uraditi na pravi način upotrebom komande.

U R možete učitati sledeće tipove podataka:

- (Tab, Blank space) Delimited Text
- CSV fajlove
- Excel fajlove
- JSON 
- SAS
- STATA
- MiniTab
- SPSS...

U ovom poglavlju, pokazaćemo vam kako da pristupite uobičajenim tipovima podataka. Jednom kada počnete da se igrate sa podacima i da ih menjate na način koji vam odgovara za vašu analizu, biće vam takođe zanimljivo da istražite mogućnost da sami kreirate različite tipove podataka. Ovde, ćemo se ipak fokusirati na osnovnu funkcionalnost funkcije `read` u R-u. 

### Osnovne funkcije u R-u (Base R)

Najednostavnija forma podataka je [text file](https://en.wikipedia.org/wiki/Text_file). Text fajl može da pročita bilo koji operativni sistem kao i veliki broj različitih statističkih programa. Čuvanje vaših podataka u tekst fajlu čini vaše podatke lako dostupnim svima. Ukoliko imate tekst fajl sa podacima koje želite da koristite, možete ih jednostavno učitati uz pomoć osnovne funkcije iz **baze R ** - `read.table()`

Sledeća naredba čita fajl u tabelarnom formatu i kreira data frame:

```
# Read tabular data into R
df_txt <- read.table(file_name.txt, header = FALSE)
```

Postoji mnogo paketa koji vam omogućavaju učitavanje podataka u R, a mi ćemo početi od `CSV` fajlova, jer su oni najčešći.

Zarezom odvojeni fajlovi je najčešći način snimanja podataka u tabelama, jer oni nisu zaštićeni i ne traže licencirane programe za njihovo otvaranje. Uvoz `CSV` fajla je deo osnovnih funkcija u R-u  i to je funkcija `read.csv()`. 


##### `read.csv()`

Idite na internet stranicu <https://data.gov.rs/> otvorenih podataka Srbije. Obratićemo posebnu pažnju na fajl [Kvalitet vazduha 2017: pm2.5_2017.csv](https://data.gov.rs/sr/datasets/kvalitet-vazduha-2017/) i njega ćemo učitati u R.

Ovaj fajl nećemo snimiti na naše računare, već ćemo ga učitati u R direktno sa interneta koristeći sledeći link.


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
Možete uvesti ove podatke i na drugi način, tako što ćete ih snimiti u svoj radni direktorijum.

Preuzećemo fajl ["Kvalitet vazduha 2017-SO2: 2017-SO2.csv"](https://data.gov.rs/sr/datasets/r/f425e6a5-95ae-4e2b-ab73-1d0b293b4522)
Vodite računa da snimite fajl u radni direktorijum vašeg R projekta pre nego što izvršite sledeći kod:

```
df_csv <- read.csv("2017-so2.csv", stringsAsFactors = FALSE, fileEncoding = "latin1")
```

{{% notice info %}}
Ponovo pokrenite kod prikazan gore, ali ovog puta bez argumenta `stringsAsFactors` tako što ćete ga ukloniti ili staviti posle znaka jednakosti TRUE. Recite nam kakva je razlika pre i posle? Šta mislite zašto koristimo argument `fileEncoding`?
{{% /notice %}}

Šta mislite o setu podataka koji ste učitali? 🤔

#### Upotreba readr::read_csv()

`readr` je paket koji čita pravougaone podatke znatno brže od `read.csv()` funkcije u base R-u. Druga razlika u odnosu na `read.csv()` funkciju je da učitava karaktere kao stringove, a ne kao faktore.

Da biste videli kako je lako koristiti druge pakete za učitavanje podataka u R-u, ilustrovaćemo to upotrebom read_csv() funkcije.

```
## If you don't have readr installed yet, uncomment and run the line below
# install.packages("readr")
library(readr)
df_csv <- read_csv("air_quality_by_station.csv")
df_csv
```

{{% notice note %}}
Proverite `readr::read_delim()` funkciju za efikasnije ograđivanje podataka iz fajlova.
{{% /notice %}}

### Učitavanje excel fajlova sa `readxl`

Učitavanje podataka iz Excel fajlova nije tako jednostavno, s obzirom da ti fajlovi mogu sadržati više šitova (sheets). Fokusiraćemo se na upotrebu readxl paketa s obzirom da se on do sada pokazao kao najefikasniji.

{{% notice warning %}}
Da biste pristupili podacima iz Excel shita ne možete jednostavno samo kopirati i umetnuti URL tog fajla. Taj fajl morate prethodno snimiti.
{{% /notice %}}

Sada ćemo snimiti podatke iz Excel fajla sa stranice otvorenih podataka [data.gov.rs](https://data.gov.rs/) o saobraćajnim nesrećama [Подаци о саобраћајним незгодама до 31.08.2019. године за територију свих ПОЛИЦИЈСКИХ УПРАВА и ОПШТИНА](https://data.gov.rs/sr/datasets/r/134b2867-8a35-4f00-ac48-1610dca177ec). 

Ukoliko ne možete da otvorite fajl u Excelu da vidite koliko šitova ima taj fajl, pokušajte pročitati fajl iz R-a tako što ćete pristupiti prvom šitu uz pomoć funkcije `read_excel()`. Pre toga, proverite da li ste snimili taj fajl u radni direktorijum vašeg R projekta, i to pre nego što izvršite sledeći kod:

```
## If you don't have readxl installed yet, uncomment the line below and run it 
#install.packages("readxl")
library(readxl)
df_xl <- read_excel("nez-opendata-20199-20190925.xlsx", sheet = 1)
```

Kako vam se čini?

{{% notice warning %}}
Ljudi obično ulepšavaju i formatiraju svoje excel fajlove, a to može prouzrokovati probleme kada se učitavaju u R.
{{% /notice %}}

Istražite argumente funkcije `read_excel()` poput `skip` argumenta sa kojim možete da specifikujete minimalni broj redova koje ne želite da učitate iz fajla.

### Učitavanje podataka upotrebom `jsonlite`

Ukoliko želite da učitate JSON fajl u R koristićete `jsonlite` paket. Potrebno je da ovoj funkciji obezbedite lokalnu putanju do fajla, ukoliko se on već nalazi na vašem računaru ili jednostavno koristeći URL ukoliko želite da ga učitate sa interneta. 


```r
## If you don't have readxl installed yet, uncomment the line below and run it 
#install.packages("jsonlite")
library(jsonlite)
my_url <-"https://data.gov.rs/sr/datasets/r/41c2fe91-4ea1-4a64-b33c-183665ea6ab3"
polen <- fromJSON(my_url)
```

Pogledajte sad strukturu `polen`! 😰


```r
str(polen)
```

```
## List of 4
##  $ count   : int 26541
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

Napomena: komanda `polen$results` je data frame koji sadrži listu koncentracija (concentrations) kao svoj element.

Uf! 😳 JSON fajlovi nisu baš uredni 😱 Oni su često ugnježdeni, povezani -> Shvatili ste: Ovo je vrlo neuredno! 😫 Dakle, ostavićemo ih takve kakvi jesu. 😬 IAko vam je potrebno da saznate više o učitavanju JSON fajlova u R to možete dodatno da istražite preko funckionalnosti paketa jsonlite ili da pronađete stranicu [Getting started with JSON and jsonlite](https://cran.r-project.org/web/packages/jsonlite/vignettes/json-aaquickstart.html). Blog post [Working with JSON data in very simple way](https://blog.exploratory.io/working-with-json-data-in-very-simple-way-ad7ebcc0bb89) autora [Kan Nishida](https://blog.exploratory.io/@kanaugust) ima odlične primere kako možete da koristite ovaj format u R-u. 

### Drugi formati podataka

Da biste ubrzali proces učitavanja txt, csv fajlova možete da koristite `data.table::fread()` funkciju. Potrebno je da za ovu funkciju samo unesete ime fajla u kome se nalaze podaci koje želite da učitate, a  `fread()` će pokušati da ih učita na odgovarajući način. Pogledajte ovaj blog [Getting Data From An Online Source](https://www.r-bloggers.com/getting-data-from-an-online-source/) da biste videli još neke ideje za učitavanje podataka. 

R zajedno sa odgovarajućim paketima možete koristiti i za učitavanje drugih formata podataka. Paket haven ima funkcije za učitavanje SAS, SPSS i Stata fajlova ili možete da koristite foreign paket za MiniTab fajlove. Pregledajte help sekciju paketa koje smo pominjali da biste više saznali o njima i o drugim opcijama.


## ZADACI 👇

1) Pregledajte stranicu otvorenih podataka <https://data.gov.rs/> i pronađite temu koja vas zanima.

2) Pogledajte setove podataka na ovoj stranici koja se nalazi u odeljku: [saobracaj](https://data.gov.rs/sr/datasets/podatsi-o-saobratshajnim-nezgodama-po-politsijskim-upravama-i-opshtinama/). Razmislite koja pitanja možete postaviti na osnovu ovih podataka.

-----------------------------
© 2019 [Siste Analyst](https://sisteranalyst.org)

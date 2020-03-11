---
date: "2016-04-09T16:50:16+02:00"
title: Organizacija podataka
output: 
  learnr::tutorial
weight: 1
---

### Kako to radimo? 🤔

![Red variant](/day2/DataWrangling/images/Program_HW.png?width=40pc)

Ovaj dijagram preuzet je iz knjige [R for Data Science](https://r4ds.had.co.nz/) autora [Garrett Grolemund](https://twitter.com/statgarrett) i [Hadley Wickham](https://twitter.com/hadleywickham), inače odličnog izvora da naučite R. Takođe, bitno je da znate da postoji i velika zajednica okupljena oko R-a, i ne bi bilo loše da im se pridružite na: [R4DS online learning community](https://www.rfordatasci.com/).

### Skupovi podataka

Da biste naučili kako da organizujete podatke koristićemo `gapminder` skup podataka koji nam je dostupan preko `gapminder` paketa u R-u. Ovaj skup podataka je u R postavila [Jennifer Bryan](https://jennybryan.org/) iz prave riznice skupova podataka koji se nalaze na [Gapminder-u](https://www.gapminder.org).

[Gapminder](https://www.gapminder.org) je nezavisna Švedska fondacija koja promoviše održivi razvoj na globalnom nivou tako što sakuplja i analizira relevantne podatke ali i razvija i kreira materijale za učenje. [Gapminder](https://en.wikipedia.org/wiki/Gapminder_Foundation) je osnovao u Švedskoj [Hans Rosling](https://en.wikipedia.org/wiki/Hans_Rosling) koji je rukovodio objavljivanje sveobuhvatne i pronicljive priče o globalnom razvoju uz pomoć vizuelnih animacija.

Hansa u akciji možete videti u [BBC dokumentarcu](https://www.bbc.co.uk/programmes/p02q33dg) [The joy of Stats](https://www.youtube.com/watch?v=cdf0k545yDA) dostupnom na [YouTube](https://www.youtube.com).

##### Gapminder podaci

Za svaku od 142 svetske države, u ovom paketu date su vrednosti za životni vek, Bruto domaći proizvod (BDP ili GDP) po glavi stanovnika i broj stanovnika na svakih pet godina počevši od 1952. godine do 2007. godine.

Kako biste pregledali ove podatke, startujte sledeći kod

```
# install necessary packages:
install.packages("dplyr", repos = "http://cran.us.r-project.org")
install.packages("ggplot2", repos = "http://cran.us.r-project.org")
install.packages("gapminder", repos = "http://cran.us.r-project.org")
```


```r
# have a look at the data 
head(gapminder::gapminder)
```

```
## # A tibble: 6 x 6
##   country     continent  year lifeExp      pop gdpPercap
##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Afghanistan Asia       1952    28.8  8425333      779.
## 2 Afghanistan Asia       1957    30.3  9240934      821.
## 3 Afghanistan Asia       1962    32.0 10267083      853.
## 4 Afghanistan Asia       1967    34.0 11537966      836.
## 5 Afghanistan Asia       1972    36.1 13079460      740.
## 6 Afghanistan Asia       1977    38.4 14880372      786.
```

{{% notice note %}}
💡Obratite pažnju da ovde imamo 6 kolona, i svaku od njih ćemo zvati varijablom.
{{% /notice %}}

**Opis**: Deo podataka iz skupa Gapminder koji sadrži informacije o životnom veku, BDP po glavi stanovnika i broju stanovnika za svaku državu.

Glavni data frame u u Gapminder-u ima **1704 redova** i **6 varijabli**:
- **country**: faktor sa 142 nivoa
- **continent**: faktor sa 5 nivoa
- **year**: raspon od 1952. do 2007. godine sa uvećanjem od 5 godina
- **lifeExp**: životni vek po rođenju, u godinama
- **pop**: broj stanovnika
- **gdpPercap**: BDP po glavi stanovnika


```r
gapminder::gapminder[1:3,]
```

```
## # A tibble: 3 x 6
##   country     continent  year lifeExp      pop gdpPercap
##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Afghanistan Asia       1952    28.8  8425333      779.
## 2 Afghanistan Asia       1957    30.3  9240934      821.
## 3 Afghanistan Asia       1962    32.0 10267083      853.
```

Prvo pregledaćemo ove podatke upotrebom sledećih funkcija:: <span style="color:red">`dim()`</span> i <span style="color:dim">`head()`</span>


```r
library(gapminder)
dim(gapminder)
```

```
## [1] 1704    6
```

```r
head(gapminder, n=10)
```

```
## # A tibble: 10 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       1957    30.3  9240934      821.
##  3 Afghanistan Asia       1962    32.0 10267083      853.
##  4 Afghanistan Asia       1967    34.0 11537966      836.
##  5 Afghanistan Asia       1972    36.1 13079460      740.
##  6 Afghanistan Asia       1977    38.4 14880372      786.
##  7 Afghanistan Asia       1982    39.9 12881816      978.
##  8 Afghanistan Asia       1987    40.8 13867957      852.
##  9 Afghanistan Asia       1992    41.7 16317921      649.
## 10 Afghanistan Asia       1997    41.8 22227415      635.
```

Šta mislite šta svaka od ove dve funkcije tačno radi⁉️

Da li imate informaciju o strukturi podataka? 🤔 Možemo istražiti strukturu upotrebom <span style="color:red">`str()`</span> funkcije, ali rezultat može izgledati neuredno i teško ga je pratiti ako je skup podataka veliki. 🤪


```r
str(gapminder) 
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	1704 obs. of  6 variables:
##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
##  $ gdpPercap: num  779 821 853 836 740 ...
```

#### Paket `dplyr`

Paket <span style="color:red">**`dplyr`**</span> nam donosi gramatiku (glagole/funkcije) za upravljanje i za operacije nad okvirom podataka (data frame) na uredan način. Ključni operatori i nazaobilazne funkcije ovog paketa su:

<span style="color:red">%>%</span>: operator “cev” koja se koristi za povezivanje više funkcija u jedan proces.

<span style="color:red">select()</span>: kreira podskup sa odabranim kolonama iz originalnog data frame-a.

<span style="color:red">mutate()</span>: dodaje nove varijable/kolone ili transformiše postojeće varijable.

<span style="color:red">filter()</span>: kreira podskup redova iz originalnog data frame-a  na osnovu logičkih uslova.

<span style="color:red">arrange()</span>: reorganizuje redove iz data frame-a  na osnovu jedne ili više varijabli.

<span style="color:red">summarise() / summarize()</span>: svodi svaku grupu u jedan red tako što obračunava zbirne mere.

Hajde da pogledamo podatke i njihovu strukturu pomoću funkcije <span style="color:red">`glimpse()`</span> iz `dplyr` paketa.


```r
suppressPackageStartupMessages(library(dplyr))
glimpse(gapminder) 
```

```
## Observations: 1,704
## Variables: 6
## $ country   <fct> Afghanistan, Afghanistan, Afghanistan, Afghanistan, Afgha...
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asi...
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 199...
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 4...
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372,...
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.113...
```

{{% notice note %}}
🤓💡: Vidite kako možemo da sprečimo da se poruke koje se pojavljuju prilikom aploadovanja paketa ne prikazuju, upotrebom u ovom slučaju naredbe `suppressPackageStartupMessages()`!
{{% /notice %}}

Sada kada smo uploadovali `dplyr` paket, pogledajmo neke od funkcija. 😇

#### Operator cev: <span style="color:red">`%>%`</span>

**Leva strana (LVS)**   <span style="color:red">`%>%`</span>    **Desna strana (DSS)**

<span style="color:red">x %>% f(..., y)</span> 

<span style="color:red">    f(x,y)</span>

„Cev“ **prosleđuje rezultat LVS kao prvi argument operatora funkcije DSS**.

<pre>
<span style="color:red">3 %>% sum(4)</span>      <==>      <span style="color:red">  sum(3, 4)</span>
</pre>

<span style="color:red">`%>%`</span> je vrlo praktičan za povezivanje više <span style="color:red">`dplyr`</span> funkcija u niz operacija.

#### Izaberite varijable prema njihovim imenima uz pomoć funkcije: <span style="color:red">`select()`</span>,

<img src="images/select().png" width="450px" />

- <span style="color:red">`starts_with("X")`</span> svako ime koje počinje sa “X”.

- <span style="color:red">`ends_with("X")`</span> svako ime koje se završava sa “X”.

- <span style="color:red">`contains("X")`</span> svako ime koje sadrži “X”.

- <span style="color:red">`matches("X")`</span> svako ime koje se poklapa sa “X”, gde “X” može biti regularni izraz.

- <span style="color:red">`num_range("x", 1:5)`</span>  varijable imenovane x01, x02, x03, x04, x05.

- <span style="color:red">`one_of(x)`</span> => svako ime koje se pojavljuje u x, koji bi trebalo da bude vektor klase karakter.

##### 👉 Vežbajte ⏰💻: Selektujte vaše varijable

1) koje se završavaju sa slovom `p`

2) koje počinju sa slovima `co`. Pokušajte da izvršite ovaj zadatak koristeći osnovni paket base R.  

##### 😃🙌 Resenje:


```r
gm_pop_gdp <- select(gapminder, ends_with("p"))
head(gm_pop_gdp, n = 1)
```

```
## # A tibble: 1 x 3
##   lifeExp     pop gdpPercap
##     <dbl>   <int>     <dbl>
## 1    28.8 8425333      779.
```

```r
gm_cc <- select(gapminder, starts_with("co"))
head(gm_cc, n = 1)
```

```
## # A tibble: 1 x 2
##   country     continent
##   <fct>       <fct>    
## 1 Afghanistan Asia
```

Naravno ovo možemo da uradimo koristeći osnovni paket-base R, na primer:


```r
gm_cc <- gapminder[c("country", "continent")]
```

ali je ovaj način manje intuitivan i obično je potrebno više kucanja. 

#### Kreirajte nove varijable od postojećih: <span style="color:red">`mutate()`</span>

<img src="images/mutate().png" width="400px" />

Omogućiće vam da dodate u data frame `df` novu kolonu, `z`, koja će sadržati rezultat množenja kolona `x` i `y`: `mutate(df, z = x * y)`.
Ukoliko želimo da imamo `lifeExp` u mesecima umesto u godinama, možemo napraviti novu kolonu `lifeExp_month`: 

```r
gapminder2 <- mutate(gapminder, LifeExp_month = lifeExp * 12) 
head(gapminder2, n = 2)
```

```
## # A tibble: 2 x 7
##   country     continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>       <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Afghanistan Asia       1952    28.8 8425333      779.          346.
## 2 Afghanistan Asia       1957    30.3 9240934      821.          364.
```

#### Izaberite opažanja prema njihovim vrednostima: <span style="color:red">`filter()`</span>
<img src="images/filter().png" width="450px" />

Postoji skup logičkih operatora u **R-u** koje možete koristiti unutar  `filter()` funkcije:

- `x < y`: `TRUE` ukoliko `x` je manje od `y`
- `x <= y`: `TRUE` ukoliko `x` je manje od ili jednako sa `y`
- `x == y`: `TRUE` ukoliko `x` je jednako sa `y`
- `x != y`: `TRUE` ukoliko `x` nije jednako sa `y`
- `x >= y`: `TRUE` ukoliko `x` je vece od ili jednako sa `y`
- `x > y`: `TRUE` ukoliko `x` je vece od `y`
- `x %in% c(a, b, c)`: `TRUE` ukoliko `x` je vektor `c(a, b, c)`
- `is.na(x)`:  je `NA`
- `!is.na(x)`: nije `NA`

##### 👉 Vezbajte ⏰💻: Filtrirajte vaše podatke

Upotrebite `gapminder2` `df` da filtirate:

1) samo evropske države i snimite ih kao `gapmEU`

2) samo evropske države od 2000 godine pa nadalje i snimite ih kao `gapmEU21c`

3) redove u kojima je životni vek veći od 80

Ne zaboravite da  **koristite `==` umesto `=`**! i
ne zaboravite da koristite znake navoda **`""`**


##### 😃🙌 Rešenja:

```r
gapmEU <- filter(gapminder2, continent == "Europe") 
head(gapmEU, 2)
```

```
## # A tibble: 2 x 7
##   country continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>   <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Albania Europe     1952    55.2 1282697     1601.          663.
## 2 Albania Europe     1957    59.3 1476505     1942.          711.
```


```r
gapmEU21c <- filter(gapminder2, continent == "Europe" & year >= 2000)
head(gapmEU21c, 2)
```

```
## # A tibble: 2 x 7
##   country continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>   <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Albania Europe     2002    75.7 3508512     4604.          908.
## 2 Albania Europe     2007    76.4 3600523     5937.          917.
```


```r
filter(gapminder2, lifeExp > 80)
```

#### Promenite redosled redova: <span style="color:red">`arrange()`</span>
Ukoliko želite da promenite redosled redova **d**ata **f**rame-a (df) prema jednoj od varijabli/kolona.

<img src="images/arrange().png" width="300px" />

- Ukoliko u funkciju `arrange()` stavite varijablu klase karakter, **R** će promeniti poređati vrednosti redova po alfabetu. 

- Ukoliko, pak, stavite faktorsku varijablu, **R** će poređati redove po redosledu nivoa u vašem faktoru (funkcija `levels()` na toj varijabli će vam prikazati redosled).

##### 👉 Vežbajte ⏰💻: ArUdite vaše podatke
1) Poređajte države u podacima `gapmEU21c` `df` prema životnom veku od najmanjeg ka najvećem i obrnuto.

2) Upotrebom `gapminder df`
  - Pronađite zapise sa najmanjom populacijom
  
  - Pronađite zapise sa najvećim životnim vekom.

##### 😃🙌 Rešenje 1):

```r
gapmEU21c_h2l <- arrange(gapmEU21c, lifeExp)
head(gapmEU21c_h2l, 2)
```

```
## # A tibble: 2 x 7
##   country continent  year lifeExp      pop gdpPercap LifeExp_month
##   <fct>   <fct>     <int>   <dbl>    <int>     <dbl>         <dbl>
## 1 Turkey  Europe     2002    70.8 67308928     6508.          850.
## 2 Romania Europe     2002    71.3 22404337     7885.          856.
```

```r
gapmEU21c_l2h <- arrange(gapmEU21c, desc(lifeExp)) # note the use of desc()
head(gapmEU21c_l2h, 2)
```

```
## # A tibble: 2 x 7
##   country     continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>       <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Iceland     Europe     2007    81.8  301931    36181.          981.
## 2 Switzerland Europe     2007    81.7 7554661    37506.          980.
```

##### 😃🙌 Rešenje  2):

```r
arrange(gapminder, pop)
```

```
## # A tibble: 1,704 x 6
##    country               continent  year lifeExp   pop gdpPercap
##    <fct>                 <fct>     <int>   <dbl> <int>     <dbl>
##  1 Sao Tome and Principe Africa     1952    46.5 60011      880.
##  2 Sao Tome and Principe Africa     1957    48.9 61325      861.
##  3 Djibouti              Africa     1952    34.8 63149     2670.
##  4 Sao Tome and Principe Africa     1962    51.9 65345     1072.
##  5 Sao Tome and Principe Africa     1967    54.4 70787     1385.
##  6 Djibouti              Africa     1957    37.3 71851     2865.
##  7 Sao Tome and Principe Africa     1972    56.5 76595     1533.
##  8 Sao Tome and Principe Africa     1977    58.6 86796     1738.
##  9 Djibouti              Africa     1962    39.7 89898     3021.
## 10 Sao Tome and Principe Africa     1982    60.4 98593     1890.
## # ... with 1,694 more rows
```


```r
arrange(gapminder, desc(lifeExp))
```

```
## # A tibble: 1,704 x 6
##    country          continent  year lifeExp       pop gdpPercap
##    <fct>            <fct>     <int>   <dbl>     <int>     <dbl>
##  1 Japan            Asia       2007    82.6 127467972    31656.
##  2 Hong Kong, China Asia       2007    82.2   6980412    39725.
##  3 Japan            Asia       2002    82   127065841    28605.
##  4 Iceland          Europe     2007    81.8    301931    36181.
##  5 Switzerland      Europe     2007    81.7   7554661    37506.
##  6 Hong Kong, China Asia       2002    81.5   6762476    30209.
##  7 Australia        Oceania    2007    81.2  20434176    34435.
##  8 Spain            Europe     2007    80.9  40448191    28821.
##  9 Sweden           Europe     2007    80.9   9031088    33860.
## 10 Israel           Asia       2007    80.7   6426679    25523.
## # ... with 1,694 more rows
```

#### Sumirajte vrednosti: <span style="color:red">`summarise()`</span>

<img src="images/summarise().png" width="450px" />

Sintaksa summarise() je jednostavna i sastoji se od  više funkcija koji su uključene u `dplyr` paket.

- koristi istu sintaksu kao i `mutate()`, ali se rezultat prikazaju u jednom redu, umesto u novoj koloni što je slučaj kod upotrebe `mutate()`. 

- gradi novi skup podataka koji sadrži samo zbirne statistike.

| Cilj      | Fukcija                 | Description                    |
| --------- | ----------------------- | ------------------------------ |
| basic     | `sum(x)`                | Sum of vector x                |
| centre    | `mean(x)`               | Mean (average) of vector x     |
|           | `median(x)`             | Median of vector x             | 
| spread    | `sd(x)`                 | Standard deviation of vector x |
|           | `quantile(x, probs)`    | Quantile of vector x           |
|           | `range(x)`              | Range of vector x              |
|           | `diff(range(x)))`       | Width of the range of vector x |
|           | `min(x)`                | Min of vector x                |
|           | `max(x)`                | Max of vector x                |
|           | `abs(x)`                | Absolute value of a number x   | 

##### 👉 Vežbajte  ⏰💻: Usetrebite summarise()`:

1) prikažite sumiranje  podataka u tabeli gapminder koje sadrži dve varijable: max_lifeExp and max_gdpPercap.

2) prikažite sumiranje podataka gapminder koje sadrži dve varijable: mean_lifeExp and mean_gdpPercap.

##### 😃🙌 Solution: Summarise your data


```r
summarise(gapminder, max_lifeExp = max(lifeExp), max_gdpPercap = max(gdpPercap))
```

```
## # A tibble: 1 x 2
##   max_lifeExp max_gdpPercap
##         <dbl>         <dbl>
## 1        82.6       113523.
```


```r
summarise(gapminder, mean_lifeExp = mean(lifeExp), mean_gdpPercap = mean(gdpPercap))
```

```
## # A tibble: 1 x 2
##   mean_lifeExp mean_gdpPercap
##          <dbl>          <dbl>
## 1         59.5          7215.
```

#### Podgrupisanje: <span style="color:red">`group_by()`</span>

Funkcija iz dplyr paketa `group_by()` omogućava vam da grupišete vaše podatke. Omogućava vam zapravo da kreirate poseban data frame df koji razdvaja orginalni df po varijablama.

Funkcija `summarise()` može da se kombinuje sa `group_by()`.

| Objective | Function                | Description                               |
| --------- | ----------------------- | ----------------------------------------- |
| Position	| first()	                | First observation of the group            |
|           | last()	                | Last observation of the group             |
|           | nth()	                  | n-th observation of the group             |
| Count	    | n()	                    | Count the number of rows                  |
|           | n_distinct()	          | Count the number of distinct observations |


##### 👉 Vežbajte  ⏰💻: SuGrupišite vaše podatke

1) Identifikujte koliko se država nalazi u  gapminder-u za svaki kontinent.

##### 😃🙌 Solution: 


```r
gapminder %>%
     group_by(continent) %>%
     summarise(n_distinct(country))
```

```
## # A tibble: 5 x 2
##   continent `n_distinct(country)`
##   <fct>                     <int>
## 1 Africa                       52
## 2 Americas                     25
## 3 Asia                         33
## 4 Europe                       30
## 5 Oceania                       2
```

#### Povežimo sve sa`%>%`!

Naučite da na brži način ukucate (shortcut) operator “cev“ 
<img src="images/pipe_short_cut.png" width="450px" style="display: block; margin: auto;" />

##### 🗣👥 Popričajte sa osobom do vas: 
Kakav odnos očekujete da postoji između broja stanovnika (`pop`) i životnog veka (`lifeExp`)?

**Pogledajte šta će sledeći kod da napravi**


```r
gapminder_pipe <- gapminder %>%
  filter(continent == "Europe" & year ==  2007) %>%
  mutate(pop_e6 = pop / 1000000)
plot(gapminder_pipe$pop_e6, gapminder_pipe$lifeExp, cex = 0.5, col = "red")
```

<img src="/module2/DataWrangling/_index.sr_files/figure-html/unnamed-chunk-24-1.png" width="576" style="display: block; margin: auto;" />

#### `tidyr`

Paket `tidyr` može da vam pomogne da kreirate **uredne podatke**. Uredni podaci su podaci u kojima.

- Je svaka **kolona** **varijabla**
- Je svaki **red** **opzervacija**
- Je svaka **ćelija** **pojedinačna vrednost**

<img src="images/tidyr.png" width="450px" />

Paket`tidyr` vodi se principima **uređenih podataka** i obezbeđuje vam standardne ključne funkcionalnosti kako biste organizovali vrednosti u setu podataka.

[Hadley Wickham](http://hadley.nz/) autor `tidyr` paketa u svom tekstu [Tidy Data](https://vita.had.co.nz/papers/tidy-data.pdf) govori o važnosti procesa čišćenja podataka i njihovog strukturisanja za dalju analize.

Stvarni skupovi podataka koje možete da skinete sa sajta <https://data.gov.rs/> ili sa bilo koje druge otvorene platforme, najčešće će prekršiti tri pravila uređenih podataka na različite načine:

- Varijable neće imati svoje nazive i umesto zaglavlja kolona imaćete vrednosti.
-	Jedna kolona će sadržati veći broj varijabli.
-	Jedna varijabla će se nalaziti u više kolona. 
-	Iste informacije su sačuvane više puta kao različite varijable.
 
Ovo su samo neki primeri.

Da bismo ovo ilustrovali idite na portal <https://data.gov.rs/> i potražite [Kvalitet Vazduha 2017](https://data.gov.rs/sr/datasets/kvalitet-vazduha-2017/). Preuzećemo sledeće podatke [2017-NO2.csv](http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-becc-6b6e31a24d80/download/2017-no2.csv) data.


```r
## If you don't have tidyr installed yet, uncomment and run the line below
#install.packeges("tidyr")
library(tidyr)
# access 2017-NO2.csv data
no2 <- read.csv("http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-becc-6b6e31a24d80/download/2017-no2.csv",
                stringsAsFactors = FALSE, 
                fileEncoding = "latin1")
```

```
## Warning in read.table(file = file, header = header, sep = sep, quote =
## quote, : invalid input found on input connection 'http://data.sepa.gov.rs/
## dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-
## becc-6b6e31a24d80/download/2017-no2.csv'
```

```
## Warning in read.table(file = file, header = header, sep = sep, quote = quote, :
## incomplete final line found by readTableHeader on 'http://data.sepa.gov.rs/
## dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-
## becc-6b6e31a24d80/download/2017-no2.csv'
```

```r
# have a look at the data
glimpse(no2)
```

```
## Observations: 0
## Variables: 7
## $ Datum                   <lgl> 
## $ Novi.Sad.SPENS.NO2      <lgl> 
## $ Beograd.Mostar.NO2      <lgl> 
## $ Beograd.Vraèar.NO2      <lgl> 
## $ Beograd.Zeleno.brdo.NO2 <lgl> 
## $ Kragujevac..NO2         <lgl> 
## $ U                       <lgl>
```

Podaci nam govore da set podataka ima `365` obzervacija i `8` varijabli. Bez obzira na to, treba da vidimo koji sve tipovi infomacija postoje::

- `date` datum kada su NO2 merenja izvršena: nalaze se u jednoj koloni -> ✅ tidy🙁
- `places` mesta na kojima je NO2 meren: nalaze se u nekoliko kolona -> ❎ tidy🙁
- `NO2` NO2 merenja: nalaze se u nekoliko kolona -> ❎ tidy🙁

Hmmm… 🤔 Da li nam ovo izgleda uredno? 😳

Ovi podaci odnose se na merenje nivoa NO2(µg/m3) u nekoliko različitih gradova/mesta, što znači da je naša glavna odzivna varijabla NO2. Način na koji je ona prikazana u ovim podacima je definitivno neuredan. Ovaj set podataka krši principe uređenih podataka da je svaka kolona varijabla i  u ovom slučaju svaki red NIJE obzervacija.

Ispostavlja se da ovi podaci sadrže 8 varijabli, a zapravo ih ima samo tri: date, place i no2. Da bismo uredili ovaj set podataka, neophodno je da kolone pretvorimo u redove. Zadovoljni smo sa varijablom date  i ona treba da ostane u koloni, međutim drugih 7 kolona treba da pretvorimo u dve varijable: place i no2.

Da pretvorimo podatke širokog formata u dugački format neophodno je da pretvorimo kolone u redove upotrebom funkcije `gather()`.

<img src="images/gather.png" width="450px" />

Kreiraćemo varijablu place u kojoj ćemo sakupiti sva zaglavlja data u kolonama 2:8. Vrednosti unutar tih kolona biće snimljene u novu varijablu no2.


```r
new_no2 <- no2 %>%
  gather("place", "no2", -Datum, factor_key = TRUE) # stack all columns apart from `Datum`
glimpse(new_no2)
```

```
## Observations: 0
## Variables: 3
## $ Datum <lgl> 
## $ place <fct> 
## $ no2   <lgl>
```

Da vidimo imena mesta


```r
new_no2 %>%
     group_by(place) %>%
     summarise(n())
```

```
## Warning: Factor `place` contains implicit NA, consider using
## `forcats::fct_explicit_na`
```

```
## # A tibble: 1 x 2
##   place `n()`
##   <fct> <int>
## 1 <NA>      0
```

Ova imena izgledaju vrlo neuredno. Možemo da iskoristimo funkciju iz [`stringr`](https://stringr.tidyverse.org) paketa `str_sub()`. Za početak hajde da uklonimo .NO2 na kraju svakog imena.


```r
## If you don't have stringr installed yet, uncomment and run the line below
#install.packeges("stringr")
library(stringr)
new_no2$place <- new_no2$place %>% 
    str_sub(end = -5)
glimpse(new_no2)
```

```
## Observations: 0
## Variables: 3
## $ Datum <lgl> 
## $ place <chr> 
## $ no2   <lgl>
```

```r
new_no2 %>%
    group_by(place) %>%
    summarise(n())
```

```
## # A tibble: 0 x 2
## # ... with 2 variables: place <chr>, `n()` <int>
```

I dalje ne izgleda kako treba. 😟 Ovo je izgleda naporan posao. 😥 Nije ni čudo zašto se mnogi analitičari žale oko vremena koji potroše na proces čišćenja i pripreme podataka. To bi mogao biti veoma dug i zamoran proces, ali što ga više radite i više iskustva stičete sve postaje lakše i manje bolno.


Možda, možete pokušati da pogledate i druge pakete R-a koji će vam pomoći u organizaciji podataka da biste dobili idealan format. Pokazaćemo vam kako se to lako možete učiniti upotrebom funkcije `forcats::fct_recode()`.


```r
## If you don't have forcats installed yet, uncomment and run the line below
#install.packages("forcats")
library(forcats)
new_no2 <- no2 %>%
  gather("place", "no2", -Datum, factor_key = TRUE) %>% # stack all columns apart from `Datum`
  mutate(place = fct_recode(place, 
                            "NS_Spens" = "Novi.Sad.SPENS.NO2",
                            "BG_Most" = "Beograd.Mostar.NO2",
                            "BG_Vracar" = "Beograd.Vraèar.NO2", 
                            "BG_ZelenoBrdo" = "Beograd.Zeleno.brdo.NO2", 
                            "KG" = "Kragujevac..NO2", 
                            "NI" = "Ni..IZJZ.Ni...NO2",
                            "UZ" = "U.ice..NO2"))
```

```
## Warning: Unknown levels in `f`: Ni..IZJZ.Ni...NO2, U.ice..NO2
```

```r
glimpse(new_no2)
```

```
## Observations: 0
## Variables: 3
## $ Datum <lgl> 
## $ place <fct> 
## $ no2   <lgl>
```

{{% notice note %}}
Do sada je trebalo da ste stekli dovoljno znanja o upotrebi R-a  i sigurnost da počnete da istražujete ostale funkcije paketa [`tidyr`](https://tidyr.tidyverse.org/). Ne treba da se tu zaustavite, već da idete dalje i istražite celu kolekciju [`tidyverse`](https://www.tidyverse.org/) R paketa. 😇🎶
{{% /notice %}}

Da biste saznali više o urednim podacima u R-u proverite glavu [Data Tidying](https://garrettgman.ithuthe b.io/tidying/) čuvene knjige [Data Science with R](https://garrettgman.github.io) autora [Garrett Grolemund](https://resources.rstudio.com/authors/garrett-grolemund)

{{% notice tip %}}
Da li ste pokušali da naučite nauku o podacima (data science)  tako što biste postovali pitanja i diskutovali o njima sa drugima iz R zajednice? 👥💻📊📈🗣 [RStudio Community](https://community.rstudio.com)
{{% /notice %}}

## ZADACI 👇

Vežbajte na sledećem setu zadataka:

1) Instalirajte i unesite poslednju verzija paketa `rattle` i pogledajte šta su njegove karakteristike.

2) Kreirajte novi R script fajl da istražite set podataka `weatherAUS`. 

  i) `select()` varijable: `MinTemp`, `MaxTemp`, `Rainfall` i `Sunshine` tako što ćete preko **operatora cev** povezati set podataka `dplyr::select() funkciju.
  
  ii) sumirajte podatke upotrebom `base::summary()` funkcije ovih numeričkih vrednosti.
  
  iii) u okviru ove selekcije filtrirajte samo one opservacije u kojima je `Rainfall >= 1` i snimite rezultate u memoriju kompjutera (tj. sačuvajte rezultate u objektu).
  
  iv) Razmislite kako biste još mogli da upotrebljavate i druge dplyr funkcije da istražite `weatherAUS` set podataka. Zapišite pitanja na početku, pa onda kodirajte.
  
  v) Napišite kratak izveštaj koja bi vizuelizacija bila zanimljiva za set podataka `weatherAUS` i zašto?

##### Korisni linkovi

[Data Wrangling cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)

[Data Transformation with dplyr cheat sheet](https://4.files.edl.io/b9e2/07/12/19/142839-a23788fb-1d3a-4665-9dc4-33bfd442c296.pdf)

-----------------------------
© 2019 [Sister Analyst](https://sisteranalyst.org)

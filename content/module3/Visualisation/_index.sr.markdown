---
date: "2016-04-09T16:50:16+02:00"
title: Vizuelizacija podataka
output: 
  learnr::tutorial
weight: 2
---

Većina vas ste, ako ne i svi, upoznati sa kreiranjem grafikona u Excelu. Softver poput Excel-a ima predefinisan set opcija za grafičko prikazivanje podataka. Ove opcije date u meniju pretpostavljaju da su podaci već pripremljeni za iscrtavanje, što u slučaju sirovih podataka nije slučaj. Biće neophodno da ovakve podatke morate organizovati i promeniti svoje podatke kako biste bili spremni za efikasnu vizulezaciju. 

### Gramatika grafike

Gramatika grafike [grammar of graphics](http://vita.had.co.nz/papers/layered-grammar.html) omogućava struktuirani način kreiranja grafikona dodavanjem komponenti kao slojeva, i na taj način su grafikoni efektniji i atraktivniji. 

Ona vam omogućava da odredite elemente grafikona i da ih kombinujete kako biste stvorili prikaz koji želite. Postoji osam elemenata:

- podaci (data)

-	estetsko mapiranje (aesthetic mapping)

-	geometrijski objekti (geometric object) 

-	statstičke transformacije (statistical transformations)

-	skale (scales)

-	koordinatni sistem (coordinate system)

-	podešavanje položaja (position adjustments)

-	oblaganje  (faceting)


Zamislite da pričamo o pečenju torte i dodavanju višnje na njen vrh. 🎂🍒 Ova filozofija ugrađena je u [`ggplot`](https://ggplot2.tidyverse.org/reference/) paket koji je razvio [Hadle Wickham](http://hadley.nz) za kreiranje elegantnih i kompleksnih grafikona u R-u.


#### ggplot2

Učenje kako da koristite paket `ggplot2` može biti izazov, ali će vam se na kraju isplatiti i kao i u R-u, biće vam lakše što ga više budete upotrebljavali.

{{% notice warning %}}
Za razliku od osnovne grafike, ggplot radi sa dataframe-ovima, a ne sa pojedinačnim vektorima.
{{% /notice %}}

Najbolji način da usvojite znanje je da vežbate. Zato napravimo prvi `ggplot`. 😃
Ono što potrebno da uradimo je sledeće:

- i) Podatke preuredite u format pogodan za vizuelizaciju.

- ii) “Pokrenite” grafikon sa `ggplot()`:
  
**ggplot(<span style="color:blue">dataframe</span>, aes(<span style="color:orangered">x = explanatory variable</span>, <span style="color:green">y = resposne variable</span>))**

Ova naredba će iscrtati prazan grafikon (`ggplot`), iako su postoje x i y vrednosti. Ggplot ne može da iscrta grafikon (na primer xy grafikon) jer ne zna na koji grafikon tačno mislite. U ovom koraku ste samo definisali koji se set podataka koristi i kolone tj. v ariable. Obratite takođe pažnju da se funkcija `aes( )` koristi za specifikaciju x i y osa.. 
  
- iii) Dodajte slojeve sa funkcijom `geom_`:

**geom_point()**

 Dodaćemo tačke na grafikonu uz pomoć **geom sloja** preko funkcije `geom_point`.


```r
# load the packages
suppressPackageStartupMessages(library(dplyr))
suppressPackageStartupMessages(library(gapminder))
suppressPackageStartupMessages(library(ggplot2))
```

```
## Warning: package 'ggplot2' was built under R version 3.6.2
```

```r
# wrangle the data (Can you remember what this code do?)
gapminder_pipe <- gapminder %>%
  filter(continent == "Europe" & year ==  2007) %>%
  mutate(pop_e6 = pop / 1000000)

# plot the data
ggplot(gapminder_pipe, aes(x = pop_e6, y = lifeExp)) +
  geom_point(col ="red")
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-1-1.png" width="768" style="display: block; margin: auto;" />

{{% notice tip %}}
🤓💡 **Tip**: Za izradu grafova možete koristiti sledeći obrazac koda **ggplot2**:
{{% /notice %}}

```
ggplot(data = <DATA>, (mapping = aes(<MAPPINGS>)) + 
      <GEOM_FUNCTION>()
```

##### <span style="color:red">ggplot()</span> galerija
Pokrenite sledeći kod kako biste videli koji će se grafikoni pokazati.


```r
ggplot(data = gapminder, mapping = aes(x = lifeExp), binwidth = 10) +
  geom_histogram()
#
ggplot(data = gapminder, mapping = aes(x = lifeExp)) +
  geom_density()
#
ggplot(data = gapminder, mapping = aes(x = continent, color = continent)) +
  geom_bar()
#
ggplot(data = gapminder, mapping = aes(x = continent, fill = continent)) +
  geom_bar()
```

##### 🗣👥 Porazgovarajte sa osobama pored vas: 
Da li životni vek zavisi od broja stanovnika?

`y = b_0 + b_1 x + e`

Startujte ovaj kod u konzoli da biste napravili linearni model `pop` sa `lifeExp`.

Obratite pažnju na pravopis, velika i mala slova, i na zagrade!

```r
m1 <- lm(gapminder_pipe$lifeExp ~ gapminder_pipe$pop_e6)
summary(m1)
```

**Možete li odgovoriti na pitanje koristeći rezultat postavljenog modela?**

```r
m1 <- lm(gapminder_pipe$lifeExp ~ gapminder_pipe$pop_e6)
summary(m1)
```

```
## 
## Call:
## lm(formula = gapminder_pipe$lifeExp ~ gapminder_pipe$pop_e6)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -6.324 -2.562  1.007  2.245  4.277 
## 
## Coefficients:
##                        Estimate Std. Error t value Pr(>|t|)    
## (Intercept)           77.477421   0.721723 107.351   <2e-16 ***
## gapminder_pipe$pop_e6  0.008762   0.023779   0.368    0.715    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.025 on 28 degrees of freedom
## Multiple R-squared:  0.004826,	Adjusted R-squared:  -0.03072 
## F-statistic: 0.1358 on 1 and 28 DF,  p-value: 0.7153
```

##### 👉 Vežbajte  ⏰💻: UsKoristite gapminder podatke.

Da li životni vek zavisi od bruto nacionalnog dohotka po glavi stanovnika?

1) Bacite pogled na podatke (tip: `sample_n(df, n)`)

2) Napravite xy  grafikon: šta vam on govori?

3) Napravite regresioni model: da li tu postoji neka veza? Koliko je jaka? Da li je veza linearna? Šta možemo zaključiti iz grafikona?

4) Koja se još pitanja otvaraju; možete li dati odgovor na njih?

##### 😃🙌 SRešenje: kod za prvo pitanje; primer

```r
sample_n(gapminder, 30)
```

```
## # A tibble: 30 x 6
##    country        continent  year lifeExp       pop gdpPercap
##    <fct>          <fct>     <int>   <dbl>     <int>     <dbl>
##  1 United States  Americas   1952    68.4 157553000    13990.
##  2 Honduras       Americas   1997    67.7   5867957     3160.
##  3 Rwanda         Africa     1962    43     3051242      597.
##  4 Egypt          Africa     1957    44.4  25009741     1459.
##  5 Panama         Americas   1952    55.2    940080     2480.
##  6 United States  Americas   1972    71.3 209896000    21806.
##  7 United Kingdom Europe     1962    70.8  53292000    12477.
##  8 Italy          Europe     1997    78.8  57479469    24675.
##  9 Puerto Rico    Americas   2002    77.8   3859606    18856.
## 10 Nepal          Asia       1952    36.2   9182536      546.
## # ... with 20 more rows
```

Dodaćemo slojeve na ovaj xy grafikon: uporedićemo `liveExp` sa `gdpPercap`. Iscrtaćemo regresionu liniju i neparemetarsku lusovu liniju (loess line) koja će nam pokazati moguću vezu između ove dve varijable. Ovo znači da ćemo imati:

- Prvi sloj: **xy grafikon** (scatterplot)
-	Drugi sloj: **regresiona linija** koja najpribližnije odgovara podacima  
-	Treći sloj: **lusova kriva** (loess curve)


##### 😃🙌 Rešenje: kod za drugo pitanje; kreiranje grafikona uz pomoć podataka;

```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.2, shape = 21, fill = "blue", colour="black", size = 5) + # set transparency, shape, colour and size for points
  geom_smooth(method = "lm", se = F, col = "maroon3") + # change the colour of line
  geom_smooth(method = "loess", se = F, col = "limegreen") # change the colour of line
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-6-1.png" width="768" style="display: block; margin: auto;" />

##### 😃🙌 SRešenje: kod za treće pitanje; jednostavni regresioni model

```r
my.model <- lm(gapminder_pipe$lifeExp ~ gapminder_pipe$gdpPercap)
summary(my.model)
```

```
## 
## Call:
## lm(formula = gapminder_pipe$lifeExp ~ gapminder_pipe$gdpPercap)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -2.79839 -1.30472  0.00807  1.33443  2.87766 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              7.227e+01  6.942e-01 104.113  < 2e-16 ***
## gapminder_pipe$gdpPercap 2.146e-04  2.514e-05   8.537  2.8e-09 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.598 on 28 degrees of freedom
## Multiple R-squared:  0.7225,	Adjusted R-squared:  0.7125 
## F-statistic: 72.88 on 1 and 28 DF,  p-value: 2.795e-09
```

### Rad sa estetikom: dodajte još slojeva na vaš <span style="color:red">`ggplot()`</span>

Kadgod je to moguće treba da se trudite da vaš grafikon bude vizuelno privlačan i informativan, kao što je rečeno u prethodnom odeljku *Principi vizuelizacije*. 

#### Da biste promenili naziv grafikona ili oznake osa koristite sloj <span style="color:orangered">layer **labs**</span>

**labs(<span style="color:blue">title =</span> <span style="color:orangered"> “your title”</span>, <span style="color:blue">subtitle =</span> <span style="color:orangered"> “your subtitle”</span>, <span style="color:blue">y =</span> <span style="color:orangered"> “y label”</span>, <span style="color:blue">x =</span> <span style="color:orangered"> “x label”</span>, <span style="color:blue">caption =</span> <span style="color:orangered"> “graph's caption”</span>)** 
 


```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.2, shape = 20, col = "steelblue", size = 5) + 
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "limegreen") + 
 
  # give a title an label axes
  labs(title = "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  
  # modify the appearance
  theme(legend.position = "none", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  
  # add the description
  geom_text(x = 80000, y = 125, label = "regression line", col = "maroon3") +
  geom_text(x = 90000, y = 75, label = "smooth line", col = "limegreen") 
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-8-1.png" width="768" style="display: block; margin: auto;" />

Obratite pažnju da smo dodali tekst na grafikon koji označava dve linije i da smo uredili grafikon tako da se legenda ne prikazuje.

Takođe, mogli smo da dobijemo ovaj tekst na grafikonu i uz pomoć sledeće naredbe:
```
annotate("text", x = 80000, y = 125 label = "regression line", color = "maroon3")
```

Da biste saznali više o promeni teme grafikona pogledajte sledeću internet stranicu [ggplot’s theme page](https://ggplot2.tidyverse.org/reference/theme.html).

#### Promenite boju tačaka tako da odražavaju treću promenljivu.


```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  
  # change the colour of the points to reflect continent it belongs to; set transparency, shape, and size for points
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "dodgerblue3") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 80000, y = 125, label = "regression line", col = "maroon3") + 
  geom_text(x = 90000, y = 75, label = "smooth line", col = "dodgerblue3")
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-9-1.png" width="768" style="display: block; margin: auto;" />

{{% notice note %}}
Imajte na umu da se legenda dodaje automatski. Možete je ukloniti tako što ćete postaviti atribut `none` na *legend.position* unutar funkcije `theme()`.
{{% /notice %}}


#### Podesite granice X i Y osa i promenite tekst X ose i polozaj crtica na x osi


```r
  ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "dodgerblue3") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 48000, y = 90, label = "regression line", col = "maroon3") + 
  geom_text(x = 70000, y = 75, label = "smooth line", col = "dodgerblue3") +
  
  # change the limits of the x & y axis
  xlim(c(0, 90000)) + 
  ylim(c(25, 100)) 
```

```
## Warning: Removed 5 rows containing non-finite values (stat_smooth).

## Warning: Removed 5 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 5 rows containing missing values (geom_point).
```

```
## Warning: Removed 33 rows containing missing values (geom_smooth).
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-10-1.png" width="768" style="display: block; margin: auto;" />
  
Obratite pažnju da su regresiona linija i kriva promenile svoje oblik 😳…Toliko mnogo upozorenja ste dobili. Šta se desilo?! 😲
  
{{% notice warning %}}
Kada koristite xlim() i ylim(), brišu se tačke izvan navedenog raspona i ne uzimaju se u obzir pri crtanju krive upotrebom `geom_smooth()`. Ova osobina vam može biti korisna kada želite da saznate da li bi se korelaciona linija  promenila ako bi se uklonile ekstremne vrednosti iz podataka. 
{{% /notice %}}
  
Srećom, postoji još jedan način da promenite granice na osama a da se ne brišu tačke izvan prikaza, i to tako što ćete zumirati region koji vam je zanimljiv. Ovo možete uraditi upotrebom funkcije `coord_cartesian()`. Probajte da zamenite komande `xlim()` i `ylim()` iz prethodnog koda sa kodom koji je prikazan dole da vidite šta će se desiti.

```
coord_cartesian(xlim = c(0, 90000), ylim = c(25, 100))  # zooming in specified limits of the x & y axis
```

Razmake na x osi možete postaviti i obeležiti upotrebom `scale_x_continuous()`? Isto to možete uraditi i na y osi? 

Pokušajte da menjate palete boja. Za dodatne opcije pogledajte [Sequential, diverging and qualitative colour scales from colorbrewer.org](https://ggplot2.tidyverse.org/reference/scale_brewer.html).

Ovo su ugrađene teme koje kontrolišu sve prikaze ne-podataka. Treba da koristite `theme_bw()` da biste imali belu pozadinu ili `theme_dark()` za tamno sivu. Za više o temama pogledajte [ovde](https://ggplot2.tidyverse.org/reference/ggtheme.html).



```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "dodgerblue3") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 80000, y = 125, label = "regression line", col = "maroon3") + 
  geom_text(x = 90000, y = 75, label = "smooth line", col = "dodgerblue3") +
  
  # change breaks and label them 
  scale_x_continuous(breaks = seq(0, 120000, 20000), labels = c("0", "20K", "40K", "60K", "80K", "10K", "12K")) +

  # change color palette
  scale_colour_brewer(palette = "Set1") + 

  # white background theme
  theme_bw()
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-11-1.png" width="768" style="display: block; margin: auto;" />

Postoji biblioteka `ggthemes` koja će vam pomoći da napravite elegantne grafikone koje koriste mediji kao što su Wall Street Journal ili Economist. Pogledajte koje još teme možete koristiti na sledećoj [vebstranici]( https://yutannihilation.github.io/allYourFigureAreBelongToUs/ggthemes/)


```r
## If you don't have ggthemes installed yet, uncomment and run the line below
#install.packeges("ggthemes")
library(ggthemes)
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "darkred") + 
  geom_smooth(method = "loess", se = F, col = "darkgreen") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 80000, y = 125, label = "regression line", col = "darkred") + 
  geom_text(x = 90000, y = 75, label = "smooth line", col = "darkgreen") +
  scale_x_continuous(breaks = seq(0, 120000, 20000), labels = c("0", "20K", "40K", "60K", "80K", "10K", "12K")) +

  # Wall Street Journal theme
  scale_colour_wsj() +
  theme_wsj()
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-12-1.png" width="768" style="display: block; margin: auto;" />

Spremni ste da pravite vizualizacije u R-u koje možete da objavite. 😎 Nastavite da  istražujete i dalje i vidite da li možete da napravite grafikone u stilu BBC-ja. Pogledajte kako BBC uređuje svoje tekstove zasnovane na podacima [BBC Visual and Data Journalism cookbook for R graphics]( https://bbc.github.io/rcookbook/).

##### Postavite više grafikona na koordinatnu mrežu

Ponekad je teško da vidite sve što je važno na jednom grafikonu, poput ovog koji smo već napravili gde nije najjasnije koja je tačno tačka za koji kontinent. Da biste lakše sagledali i razumeli informacije koje želite da prikažete, nekad je efikasnije da različite kategorije o istoj informaciji predstavite u više grafikona jedan pored drugog. Ovo je vrlo jednostavno uraditi uz pomoć moćnih funkcija `ggplot2`: `facet_wrap()` and `facet_grid()`.
  

```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "darkred") + 
  geom_smooth(method = "loess", se = F, col = "black") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  scale_x_continuous(breaks = seq(0, 120000, 20000), labels = c("0", "20K", "40K", "60K", "80K", "10K", "12K")) +
  scale_colour_wsj() +
  theme_wsj() +
  
  # forms a matrix of scatterplots for each continet
  facet_grid(rows = vars(continent))
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-13-1.png" width="768" style="display: block; margin: auto;" />
 
Glavna razlika između funkcije `facet_wrap()` i  `facet_grid()` je da prva može da spoji grafikone  jedne pored drugih za jednu varijablu, dok druga može to da uradi za više od jedne varijable.

{{% notice warning %}}
Pokušajte da istražite ove dve funckije sami i vidite kuda će vas to odvesti.
{{% /notice %}}
 
#### 💪 Pokušajte sledeće: 

- `Dplyr-ova` `group_by()` funkcija vam omogućava da grupišete svoje podatke. Dozvoljava vam da kreirate posebne df koji razdvaja orginalni df po varijabli.

- `boxplot()` funkcija proizvodi boxplot grafikone od datih (grupisanih) vrednosti.

Pošto znate za funkcije `group_by()` i `boxplot()` i već ste koristili `gapminder` podatke, možete li da izračunate medijanu životnog veka u 2007. godini po kontinentima i da vizuelizujete vaše rezultate?

##### 😃🙌 Rešenje: kod

Pogledajmo medijanu životnog veka za svaki kontinent

```r
gapminder %>%
    group_by(continent) %>%
    summarise(lifeExp = median(lifeExp))
```

```
## # A tibble: 5 x 2
##   continent lifeExp
##   <fct>       <dbl>
## 1 Africa       47.8
## 2 Americas     67.0
## 3 Asia         61.8
## 4 Europe       72.2
## 5 Oceania      73.7
```

**Imamo sreće što živimo u Srbiji, tj. u Evropi!!!** 😅

##### 😃🙌 SRešenje: grafikon

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-15-1.png" width="768" style="display: block; margin: auto;" />
##### Studija slučaja: NO2 2017 😁

Hajde da sad pokušamo da iskombinujemo sve što smo do sada naučili i da vežbamo na već dobro poznatim podacima [2017-NO2.csv](http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-becc-6b6e31a24d80/download/2017-no2.csv) data. 

Sećate se ovoga?

```r
library(tidyr)
library(forcats)
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


```r
new_no2 %>% 
  group_by(place) %>% 
  summarise(mean_no2 = mean(!is.na(no2))) %>% # !is.na(): is not NA; omits the missing values
  ggplot(aes(x = place, y = mean_no2, fill = place)) + # fill: colours each bar differently   
    geom_bar(stat = "identity") +
    xlab("Place") + 
    scale_fill_brewer(palette = "Dark2") + # colour scheme "Dark2"
    theme(legend.position="bottom", 
          axis.text.x = element_blank(),
          axis.ticks.x = element_blank()) # 
```

```
## Warning: Factor `place` contains implicit NA, consider using
## `forcats::fct_explicit_na`
```

```
## Warning: Removed 1 rows containing missing values (position_stack).
```

<img src="/module3/Visualisation/_index.sr_files/figure-html/unnamed-chunk-17-1.png" width="672" />

## Sad je red na vas 👇

Vežbajte na sledećem setu zadataka:

1) Odaberite podatke koji su vam zanimljivi sa portala otvorenih podataka <https://data.gov.rs>. Učitajte set podataka u R i pregledajte koje sve varijable postoje. Razmislite kakve biste  grafikone koristili da biste te podatke prikazali vašoj publici?

2) Vratite se na studiju slučaja NO2 2017:

  i)	Koja sva pitanja možete postaviti na osnovu informacija koje su vam dostupne u ovom setu podataka?

  ii)	Koje biste grafikone predložili kako bi vam pomogli da odgovorite na ova pitanja?

  iii) Kreirajte odgovarajuće vizuelizacije za i) i ii)



##### korisni linkovi: 

[tidyverse, visualization, and manipulation basics](https://www.rstudio.com/resources/webinars/tidyverse-visualization-and-manipulation-basics/)

[Introduction to R graphics with ggplot2](http://tutorials.iq.harvard.edu/R/Rgraphics/Rgraphics.html#introduction)

[`gglopt` cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)

[from Data to Viz](https://www.data-to-viz.com/)

[An example from the Financial Times](http://johnburnmurdoch.github.io/slides/r-ggplot/#/)

[BBC Visual and Data Journalism cookbook for R graphics](https://bbc.github.io/rcookbook/)

[ggplot as a creativity engine](http://johnburnmurdoch.github.io/slides/r-ggplot/#/)

-----------------------------
© 2019 [Sister Analyst](https://sisteranalyst.org)

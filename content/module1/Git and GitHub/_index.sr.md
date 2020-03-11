---
date: "2016-04-09T16:50:16+02:00"
title: Git i GitHub
weight: 3
---

## Zašto su potrebni i šta je to? 🤔

Kada radite na projektima obrade podataka kreiraćete velik broj dokumenata koje biste voleli da menjate i da ih uredite na određen način. Takođe, može vam biti korisno da drugi koji su zaniteresovani mogu da dodatno doteruju i razvijaju vaš rad.  Da bi im to omogućili neophodno je da on bude negde dostupan. Ovaj posao možete prepustiti besplatnom i otvorenom sistemu za kontrolu verzija vašeg rada (version control system) koji se zove Git. Git je alat koji prati sve vaše verzije rada, promene u njemu, ali vam pruža i mogućnost da delite ove promene sa svima koji su zainteresovani. Ove Git konfigurisane verzije vašeg rada nalaze se u setovima koje nazivamo repozitoriji ili repos, a oni su organizovani na jedan visoko strukturisan način. 

Da bi obezbedili mesto na internetu gde ćete postavljati vaš rad i projekte neohpodno je da ga „hostujete“ (postavite) na veb stranici GitHub. Ta stranica će akumulirati sva vaša dokumenta i fajlove koje razvijate.

## Setovanje Git-a

Ukoliko niste do sada koristili Git ili GitHub, započećemo sa njihovom instalacijom i otvaranjem naloga na GitHub-u. Zatim ćemo ih povezati.

1) Prvo, instalirajte Git sa [git-scm](https://git-scm.com/downloads)
Napomena: Git-scm će automatski otkriti vaš operativni sistem i ponudiće vam odgovarajuću verziju za preuzimanje.

2) Recite Git-u svoje ime i email adresu. Tako ćete povezati svoj Git sa GitHub-om što će vam omogućiti da započnete saradnju sa drugima, i svima će biti jasno koje ste promene napravili. 

### Instalacija Git-a na Mac-u

Pre nego što napravite prvi korak proverite da eventualno već nemate instaliran Git na vašem računaru (Napomena: Git bi trebalo da je već instaliran na Mac uređajima).

Otvorite vaš terminal i ukucajte

```
git --version
```
Trebao bi dobijete nešto poput ovoga dole

```
git version 2.18.0
```

U slučaju da imate stariju verziju od trenutno dostupne ili nemate git instaliran idite na sledeću veb stranicu: [git-scm.com](https://git-scm.com).

Kada instalirate poslednju verziju Git-a na svom Mac-u identifikujte se tako što ćete ukucati sledeće komande u svoj terminal:

```
git config --global user.email "your@email.com"
git config --global user.name "your name"
```


### Instalacija Git-a na PC-u

Pokrenite CMD program tako što ćete ukucati CMD u prozoru za pretragu (search). Tako će se otvoriti command prompt prozor u kojem trebate da ubacite sledeću naredbu, da biste proverili da li Git već postoji na vašem računaru:

```
git --version
```

Ukoliko Git nije prepoznat, to znači da treba da ga instalirate sa sledeće stranice <https://gitforwindows.org>. Skinite sa sajta neophodan file i započnite instalaciju tako što ćete odabrati osnovnu (default) instalaciju. Zatvorite svoj command prompt prozor da omogućite promenu na vašem sistemu i otvorite ga ponovo. Kada to uradite ponovite gore navedenu komandu, da proverite da li ste ispravno instalirali Git i koja je verzija.

Pošto ste ispravno instalirali Git potrebno je da registrujete svoju email adresu i vaše ime:

```
git config --global user.email "your@email.com"
git config --global user.name "your name"
```


U command promt-u ili shell-u, pokrenite:


<http://rstudio-pubs-static.s3.amazonaws.com/272737_7d6178a0e50043528d9ba636fdde209e.html>

## Povežite Rstudio sa GitHub-om 🤓

RStudio sadrži integrisane mogućnosti da vam obezbedi lakšu upotrebu Git-a. Ovo setovanje treba da prođete samo jednom.

Kada kreirate u Rstudiju novi projekat, potrebno je da uradite sledeće kako biste omogućili komunikaciju između RStudija i GitHub-a:

- Odredite direktorijum (ili folder) na vašem računaru na kome će se nalaziti projekat.
- Otvorite novi projekat u RStudiju.
- Otvorite novi Git repozitorijum.

{{% notice note %}}
Možda će vam biti teško da pravilno koristite Git na početku, ali kao i sa drugim alatima koje budete koristili biće vam mnogo lakše kako budete više vežbali. Vežbom do savršenstva!  
{{% /notice %}}

Više detalja kako da povežete GitHub sa RStudijom možete naći na sledećoj internet stranici [RStuio's website](https://support.rstudio.com/hc/en-us/articles/200532077-Version-Control-with-Git-and-SVN). 

Prvo ćemo setovati SSH ključ koji će nam omogućiti sigurnu komunikaciju sa GitHub veb stranicom tako da nam neće trebati svaki put lozinka. Da bi ovo uradili pratite instrukcije iz [`Git and GitHub`](http://r-pkgs.had.co.nz/git.html) sekcije knjige [Hadle's](http://hadley.nz) book [R Packages](http://r-pkgs.had.co.nz).

Više o detaljima upotrebe GitHub-a i njegovo dalje istraživanje možete naći u poglavlju 9 [`Chapter 9: Connect to GitHub`](https://happygitwithr.com/push-pull-github.html) knjige [Jenny's](https://jennybryan.org) book [Happy Git and GitHub for the useR](https://happygitwithr.com/index.html).

{{% notice tip %}}
Možda možete da zabeležite (bookmarkujete) sledeći link [GitHub Cheet Sheet](https://education.github.com/git-cheat-sheet-education.pdf)!
{{% /notice %}}

-----------------------------
© 2019 [Sister Analyst](https://sisteranalyst.org)

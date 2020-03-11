---
date: "2016-04-09T16:50:16+02:00"
title: blogdown
output: 
  learnr::tutorial
weight: 3
---

## blogdown: Kreiranje veb stranica sa R Markdown-om

“Dobro dizajniran i održavan vebsajt može biti od velike koristi da vas ljudi upoznaju i nema potrebe da čekate priliku da se lično predstavite na nekoj od konferencija ili u nekoj drugoj situaciji. Sa druge strane, internet prezentacije su takođe korisne da biste pratili šta ste radili ili o čemu ste razmišljali. Nekad ćete se vratiti na neki stari vaše tekst da biste se podsetili trikova ili metoda koje ste već ranije savladali, ali ste ih u međivremenu zaboravili.“ [Yihui Xie](https://yihui.name/en/)[blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/)

U ovom delu naučićete kako da kreirate statičke veb stranice upotrebom paketa [blogdown](https://cran.r-project.org/web/packages/blogdown/index.html) i [HUGO](https://gohugo.io).  


<img src="images/rmd_hugo_blogdown.png" width="600px" />

#### Šta je blogdown?

From Yihui: <https://slides.yihui.name/2017-rmarkdown-UNL-Yihui-Xie.html#35>.

- [R Markdown](https://rmarkdown.rstudio.com) <img src="https://www.rstudio.com/wp-content/uploads/2015/12/RStudio_Hex_rmarkdown.png" width="10%" align="right" />
    - (relativno) jednostavna sintaksa za pisanje dokumenata
    
    - što je jednostavniji, prenosiviji je (više izlaznih formata)
    
    - ne samo da je zgodan (za održavanje), već je moguće i da se reprodukuje
    
    - većina karakteristika _i_ [**bookdown**](https://bookdown.org) (podrazumeva tehničko pisanje)!!



- [Hugo](https://gohugo.io) <img src="https://gohugo.io/img/hugo.png" width="10%" align="right" />

    - Slobodan, otvorenog koda, i lak za instalaciju
    
    - Munjevito brz (generiše stranicu u milisekundi)
    
    - Opšte je namene (ne samo za blogove)

##### Zašto ne WordPress, Tumblr, Medium.com, Blogger.com, etc?

From Yihui: <https://slides.yihui.name/2017-rmarkdown-UNL-Yihui-Xie.html#36>.

- Ne postoji R Markdown podrška (sama podrška za matematiku ili ne postoji ili nije baš od velike koristi)

- Ogromne su prednosti statičkih vebsajtova u poređenju sa dinamičkim
    - Svi fajlovi su statični, nema PHP-a ili baza podataka, nema logovanja/šifri, radi bilo gde (čak i bez internet veze, offline)
    
    - obično se vrlo brzo pristupa sajtu (nije potrebno računjanje koje pokreće server), a jednostavan da se dodatno ubrza preko CDN-a.


### Napravite vaš vebsajt

Krenućemo korak po korak. Počećemo sa postavljanjem GitHub repozitorijuma za naš veb sajt projekat.

##### Priprema GitHub-a

Već smo upoznati sa osnovama rada u GitHub-u, a možete još jednom pogledati i proučiti na [Happy Git with R](http://happygitwithr.com) kako da povežete RStudio sa svojim GitHub nalogom.


<img 
src="http://happygitwithr.com/img/watch-me-diff-watch-me-rebase-smaller.png" align="middle" img width="60%"  
/>

Pretpostavljamo da ste već:

☑️ Capter 5: [Registrovali GitHub nalog ](http://happygitwithr.com/github-acct.html)

☑️ Chapter 6: [Instalirali ili apgrejdovali R i RStudio ](http://happygitwithr.com/install-r-rstudio.html)

* Idite na svoj GitHub nalog i kreirajte novi repozitorijum

<img src="images/New_Repo.png" width="200px" style="display: block; margin: auto auto auto 0;" />

* Dajte mu odgovarajuće ime  
<img src="images/Create_New_Repo.png" width="300px" style="display: block; margin: auto auto auto 0;" />

* Kopirajte **HTTPS adresu** repozitorijuma
<img src="images/HTTPS_GitHub.png" width="350px" style="display: block; margin: auto auto auto 0;" />

##### U RStudiju

* Otvorite novi projekat u RStudiju: **File** ➡️ **New Project...**
<img src="images/RS_New_Project.png" width="250px" style="display: block; margin: auto auto auto 0;" />

* Izaberite **Version Control** ➡️ **Git**
<img src="images/Select_Version_Control.png" width="250px" style="display: block; margin: auto auto auto 0;" />

* Kopirajte adresu vašeg Git repozitorijuma
<img src="images/set_up_git_connection.png" width="250px" style="display: block; margin: auto auto auto 0;" />

#### Instalirajte paket

* Instalirajte <span style="color:red">**blogdown**</span>

`install.packages("blogdown")`


* Instalirajte **Hugo** uz pomoć blogdown-a

`blogdown::install_hugo()`


💡! Ukoliko imate ove pakete već instalirane, možete proveriti da li imate najnoviju verziju <span style="color:red">Hugo</span> paketa.

`blogdown::hugo_version() # check version`

`blogdown::update_hugo() # force an update`

💡! Ukoliko imate problema sa instalacijom pokušajte sa sledećim kodom:

`install.packages("blogdown", repos = "http://cran.us.r-project.org")` 🤞

#### Napravite vebsajt

Usvojićemo pristup jednostavno je lepo i napravićemo vebsajt uz pomoć osnovne teme.

`blogdown::new_site()`

💡!Ukoliko vam se osnovna tema ne sviđa, probajte da instalirate neku drugu (**na primer: hugo-academic**):

`blogdown::new_site(theme = "gcushen/hugo-academic", theme_example = TRUE)`


Kako biste videli koje su vam sve **Hugo themes** dostupne idite na  <https://themes.gohugo.io/>.

Prvo se upoznajte sa blogdown-om i Hugo-m .🧐 Jednom kada to uradite sa blogdown i Hugo lako ćete prelaziti sa teme na temu, i lako ćete ih menjati. 💇 <https://bookdown.org/yihui/blogdown/other-themes.html>

#### Struktura HUGO sajtova

<img src="images/Site_Structure.png" width="200px" style="display: block; margin: auto;" />

<img src="images/main_structure.png" width="200px" style="display: block; margin: auto;" />

<https://gohugo.io/getting-started/directory-structure/>

#### Pokrenite server sajta

* U konzoli ukucajte:

`blogdown::serve_site()` 

or, from `Addins` menu select `servesite` 

<img src="images/Serve_Site.png" width="200px" style="display: block; margin: auto;" />

Nemojte da gledate vaš sajt u RStudio-u jer je prozor mali, umesto toga kliknite na opciju Show in new window.

<img src="images/show_in_new_window.png" width="250px" style="display: block; margin: auto;" />

#### Izrazi koje ćemo usvojiti

- **Kosa crta (trailing slash)** na kraju imena direktorijuma `content/` znači da se referišete na direktorijum koji se zove content, a ne na fajl imena content na koji biste se referisali ukoliko ne biste stavili kosu crtu na kraju imena direktorijuma.

<img src="images/trailing_slash.png" width="150px" style="display: block; margin: auto auto auto 0;" />

- **Vodeća kosa crta (leading slash)** označava osnovni direktorijum u kojem se nalazi vaš project website, na primer `/content/about.md` podrazumeva da se referišete na fajl `about.md` koji se nalazi u osnovnom (root) direktorijumu vašeg vebsajt projekta.  

<img src="images/leading_slash.png" width="150px" style="display: block; margin: auto auto auto 0;" />

### Izgradite stranicu korak po korak

#### 👉 Idite na sledeći link da biste preuzeli radni materijal: <https://github.com/TanjaKec/BlogdownWS>

##### Odavde ćemo pratiti  korake koji se nalaze u Xaringan prezantaciji koja nam je dostupna [ 👉 ovde](https://tanjakec.github.io/BlogdownWS/Blogdown_WS_Slides/blogdown_workshop.html)

### Sretno blogovanje! 📢 



-----------------------------
© 2019 [Sister Analyst](https://sisteranalyst.org)

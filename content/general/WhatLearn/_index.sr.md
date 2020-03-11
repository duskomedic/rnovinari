---
date: "2016-04-09T16:50:16+02:00"
title: Opšti pregled
weight: 1
---

Živimo u digitalnom svetu u kojem su nam informacije na domak ruke, a, da nam pritom nije olakšana komunikacija… upravo suprotno, komunikacija nam je otežana. Kada pogledamo bilo koju gomilu podataka videćemo da ona sadrži neograničen broj skrivenih priča i zaključaka, neke manje uočljive, druge emotivno naglašene, ali sve one  biće van vašeg domašaja ukoliko ne posedujete veštine potrebne za otkrivanje istine koja se skriva iza njih. Za otkrivanje skrivenih istina iz tih podataka i za njihovu prezentaciju neophodna je znatiželja, odlučnost i veština. Razumevanje osnovnih pojmova, alata i postupaka nauke o podacima ključno je za dešifrovanje i otkrivanje glavnih činjenica te priče. Da bi se to desilo, neophodno je da znatiželjni koji žele da ih otkriju primene i usvoje upravo te prakse i alate . Kreiranje priča na osnovu podataka postaje sve važnije u digitalnom svetu u kojem podaci neprestano nastaju, kao i naša želja da donosimo odluke na osnovu podataka.

Najprimereniji softver za izveštavanje o savremenoj analizi podataka svakako je [**R**](https://www.r-project.org), s obzirom da su svi korišćeni podaci i kod za njihovo razumevanje dostupni i korisni i drugim istraživačima; ali i proverljivi. **R** je lingua franca kvantitativnog istraživanja i kao takav važan je i nezamenjiv jezik za svaki postupak provere podataka. Kroz upotrebu gramatike grafikona u **R-u**, njegovog paketa [Shiny](https://shiny.rstudio.com) i okvira za **R** web aplikacije biće vam lako da razvijete interaktivne grafičke vizuelizacije podataka. Tako što ćete predstaviti nalaze vašeg istraživanja interaktivno, uz pomoć dostupnih metoda vizualizacije doći ćete do svoje publike koja sama ne bi mogla da shvati značaj teme ili značaj podataka koje predstavljate.

Ovaj kurs vam donosi pregled ključnih koncepata za sprovođenje efikasnog naučno-istraživačkog projekta; upoznaće vas sa alatima i tehnikama za obradu podataka, vizuelizaciju i dinamičko izveštavanja koje može da se reprodukuje kroz korišćenje **R** jezika za analizu podataka. **R** jezik je bogato i fleksibilno okruženje za rad sa podacima, posebno sa podacima koji će se koristiti za statističko modelovanje ili grafiku.

**R** sistem poseduje opsežnu biblioteku paketa koji će vam omogućiti vrhunsko istraživanje. Mnoge analize, koji te biblioteke nude, nisu dostupne ni u jednom standardnom paketu. **R** vam omogućava da izbegnete restriktivna okruženja koja vam nude „sterilne“ analize najčešće korištenih statističkih softverskih paketa. R vam omogućava lako eksperimentisanje i istraživanje, što poboljšava analizu podataka. Deljenje vaših nalaza o istraživanim podacima neophodno je da bi bilo korisno i za druge. **R** je alat koji omogućava izveštavanje o savremenim analizama podataka koje mogu da se reprodukuju. Na taj način analizu čini korisnijom za druge, jer su podaci i kod kojim se vrši analiza dostupni i mogu se lako deliti. U skladu sa tim, ovaj kurs će vas podučiti o paketima koji će vam pomoći da uradite analizu podataka, njihovu vizuelizaciju i komunikaciju sa širom publikom.

Kurs počinje sa upoznavanjem osnovnih koncepata **R** jezika, osnovnom upotrebom **R** konzole u integrisanom razvojnom okruženju [**RStudija**](https://www.rstudio.com) (RStudio IDE), postavljanjem i uvozom podataka, njihovim čuvanjem i dobroj praksi korišćenja okruženja **R** projekta. Nakon toga, upoznaćemo vas sa osnovnim konceptima statističke analize koja se može smatrati kompleksnom, ali na način da vama bude pristupačnija objašnjavajući je kroz grafikone i vizuelizaciju podataka. Formalnu apstraktnu prirodu statistike demistifikovaćemo vizualizacijom njene primene, zbog čega smo fokus usmerili na izradu odgovarajuće vizuelizacije datih problema analize podataka.
Na kraju kursa, nakon što polaznici razumeju podatke koje analiziraju, naučiće da upotrebljavaju R na interaktivan način koji može da se reprodukuje, kako bi prezentovali jasnu i konciznu priču, kroz kreiranje [RMarkdown dokumenata](https://rmarkdown.rstudio.com/) i [Shiny](https://shiny.rstudio.com) web aplikacija. Kurs će se završiti kreiranjem internet stranice koju ćete moći da koristite na vašim portalima ili blogovima, a koja će vam služiti da  prestavite vaše priče uz pomoć paketa [HUGO](https://gohugo.io/) i [blogdown](https://bookdown.org/yihui/blogdown/).

Kontrola verzije (version control) postao je nezamenjiv alat za čuvanje vaših verzija istraživačkih projekata, ali i alat koji vam omogućuje saradnju sa drugima. Sam **RStudio** podržava rad sa **Git-om**, otvorenim kodom za sistem kontrole vaših verzija, pogotovo u kombinaciji sa **GitHub-om**,  internet uslugom za čuvanje vaših **Git** repozitorija. U nastavku upoznaćemo vas sa **GitHub-om** i sa dobrom praksom da uključite upotrebu **Git-a** u svoj **R** projekat.

Potražnja za otvorenim i transparentim izvorima podataka svakodnevno raste, za njih su zainteresovani kako vlade tako i građanske organizacije kako bi poboljšali živote građana. Zajedno ćemo istražiti važnost otvorenog koda i identifikovaćemo gde se podaci otvorenog koda mogu lako naći na internetu. Radićete na studijama slučajeva koji su inspirisani stvarnim problemima i koji su dostupni putem **otvorenih podataka**.

## Ciljevi:

-	Da naučite kako da pristupite i pripremite podatke za analizu, 

-	Da upoznate osnovne principe efektivne vizuelizacije podataka,

-	Da naučite osnovne tehnike za sumiranje podataka,

-	Da vizuelizujete podatke tako da vam vizuelizacije pomognu u pronalaženju onoga što je značajno za objašnjenje podataka,

-	Da upotrebljavate R biblioteke da vizuelizujete geoprostorne probleme,

-	Da dizajnirate reporducibilne izveštaje automatizovanjem procesa izveštavanja,

-	Da delite rezultate analize kao interaktivne, privlačne veb aplikacije, koje su jasne ne-programerima,

- Da se upoznate sa mogućnostima R/R studija za obradu podataka koje će vam proširiti područje problema analize podataka.


## Kako je organizovan kurs

Kurs je organizovan u tri dnevna modula. Svaki modul traje ukupno tri i po sata, i podeljen je na dva i po sata interaktivne radionice i na poslednji sat koji je rezervisan za pitanja i diskusiju.

Kurs vode [Tatjana Kecojević](https://www.linkedin.com/in/tatjana-kecojevic-803704143/) i [Duško Medić](https://www.linkedin.com/in/duskomedic/) koji će pokriti različite teme kroz odgovarajuće studije slučaja, prezentacije i materijale za čitanje. Koncepti će zaživeti kroz praktičnu primenu **R-a**, a od polaznika se očekuje i da nastave da vežbaju i ponavljaju znanja koja su usvojila na kursu.

Od polaznika se očekuje da prođu sve delove kursa bez izuzetka, a posebno da pokušaju da reše bilo koji unapred postavljen zadatak, da budu spremni da razgovaraju o problemima sa kojima su se susreli i da diskutuju o idejama i bilo kojim drugim pitanjima. 

{{% notice tip %}}Na kraju svakog modula, preporučujemo da uradite sledeće:

* Pročitajte preporučenu literaturu i prođite kroz postavljene zadatke,
* Učestvujte u diskusiji,
* Dodatno vežbajte naučeno iz preporučenih tutorijala i materijala za čitanje. 
{{% /notice %}}


## Za koga je ovaj kurs

Ovaj kurs je namenjen svima koji nameravaju da prenose informacije zasnovane na podacima. Biće od koristi svima koji su zainteresovani i imaju želju da uđu u svet analize podatka. Trudićemo se da razumete ovaj svet i da vas naučimo da efikasno i na atraktivan način vizuelizujete svoje analize i uspešno ih iskomunicirate. Sa znanjem stečenim na ovom kursu, bićete spremni da otpočnete svoju prvu analizu podataka.

**Nauka o podacima** (Data Science) nije samo reč koja je u trendu, već disciplina koja sadrži alate koji osnažuju svakodnevni život bogat raznim podacima, tako da bez obzira iz kog sektora ili industrije dolazite, kurs će vam biti relevantan.

Za uspešno pohađanje kursa, prethodno iskustvo nije neophodno.

Kurs će se održati na BHSC i engleskom jeziku!


-----------------------------
© 2019 [Sister Analyst](https://sisteranalyst.org)


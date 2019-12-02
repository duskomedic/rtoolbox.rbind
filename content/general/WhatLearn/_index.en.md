---
date: "2019-11-29T16:50:16+02:00"
title: OPŠTI PREGLED
weight: 1
---

Živimo u digitalnom svetu u kojem su nam informacije na domak ruke, a, da nam pritom nije olakšana komunikacija… upravo suprotno, komunikacija nam je otežana. Kada pogledamo bilo koji paket podataka videćemo da on sadrži neograničen broj skrivenih narativa ali i mogućnosti da zaključujete iz njih; narativi mogu biti skriveni ili naglašeni, ali svakako su izvan vašeg domašaja ukoliko ne posedujete veštine potrebne za njihovo čitanje. Otkrivanje skrivenih istina iz paketa podataka i njihovo kasnije saopštavanje zahteva znatiželju, odlučnost i veštinu. Razumevanje osnovnih pojmova, alata i povezanih postupaka nauke o podacima ključno je za dešifrovanje i otkrivanje glavnih činjenica te priče, ali da bi se to i desilo, neophodno je i da se te prakse i alati primene i usvoje od onih znatiželjnih koji žele da ih otkriju. Generisanje priča iz podataka postaje sve važnije u digitalnom svetu u kojem podaci neprestano nastaju, ali i naše želje da donosimo odluke na osnovu podataka.

Najprimereniji softver za izveštavanje modernom analizom podataka svakako je [**R**](https://www.r-project.org),s obzirom da njegovom upotrebom svi korišteni podaci i kod za njihovo razumevanje dostupni su i korisni i drugim istraživačima; ali i proverljivi. **R** je lingua franca kvantitativnog istraživanja i kao takav važan je i nezamenjiv jezik za svaki postupak provere podataka. Strukturisanom upotrebom jezika **R**, njegovog paketa [Shiny](https://shiny.rstudio.com), i okvira za  **R** web aplikacije biće vam lako da razvijete interaktivne grafičke vizuelizacije podataka, ali i predstavljanje nalaza vašeg istraživanja interaktivno; pomoću dostupnih metoda vizualizacije doći ćete do svoje publike koja sama ne bi mogla shvatiti značaj teme ili značaj podataka koje predstavljate.

Ovaj kurs donosi vam pregled ključnih koncepata za sprovođenje efikasnog naučno-istraživačkog projekta; upoznaće vas sa alatima i tehnikama za obradu podataka, vizuelizaciju i dinamičko reproduktibilnog (ponovljivog) izveštavanja upotrebom **R** jezika za analizu podataka. **R** jezik je bogato i fleksibilno okruženje za rad sa podacima, posebno sa podacima koji će se koristiti za statističko modelovanje ili grafiku. 

**R** sistem poseduje opsežnu biblioteku paketa koji će vam omogućiti vrhunsko istraživanje. Mnoge analize, koji te biblioteke nude, nisu dostupne ni u jednom standardnom paketu. **R** vam omogućava da izbegnete restriktivna okruženja koja vam nude „sterilne“ analize najčešće korištenih statističkih softverskih paketa. **R** vam omogućava lako eksperimentisanje i istraživanje, što poboljšava analizu podataka. Deljenje vaših nalaza o istraživanim podacima neophodno je da bi bilo korisno i za druge. **R** je alat koji omogućava izveštavanje savremenih analiza podataka na ponovljiv način. Analizu čini korisnijom za druge, s obzirom da se podaci i kod koji zapravo vrši analiza mogu učiniti dostupnim i lako se deliti. U skladu sa tim, ovaj kurs podučiće vas o paketima koji će vam pomoći da uradite analizu podataka, njihovu vizuelizaciju i komunikaciju sa širom publikom.

Kurs počinje sa upoznavanjem osnovnih konceptima **R** jezika: osnovnom upotrebom **R** konzole u integrisanom razvojnom okruženju [**RStudio**](https://www.rstudio.com) IDE, postavljanjem i uvozom podataka, njihovom čuvanju i uopšteno o radu u okruženju R projekta. Nakon toga, upoznaće vas sa osnovnim konceptima statističke analize za koju se može smatrati da je kompleksna, ali na način da vama bude pristupačnija objašnjavajući je kroz grafikone i vizuelizaciju podataka. Formalnu apstraktnu prirodu statistike demistifikovaćemo vizualizacijom njene primene, zbog čega smo fokus usmerili na izradu odgovarajuće vizuelizacije datih problema analize podataka. Na kraju kursa, nakon što polaznici shvate svoje podatke koje analiziraju, oni će upotrebiti R na interaktivan i reproduktibilan (ponovljiv) način koji će sažeti priču o podacima, i naravno, ih predstaviti kroz kreiranje [RMarkdown](https://rmarkdown.rstudio.com/) dokumenata i  [Shiny](https://shiny.rstudio.com) web aplikacija. . Kurs će se završiti kreiranjem internet stranica koje će te moći koristiti na vašim portalima ili blogovima, a koje će vam prestaviti vaše priče uz pomoć paketa [HUGO](https://gohugo.io/) i [blogdown](https://bookdown.org/yihui/blogdown/).

Kontrola izdanja (version control) postao je nezamenjiv alat za čuvanje vaših verzija istraživačkih projekata, ali i alat koji vam omogućuje saradnju sa drugima. Sam **RStudio** podržava rad sa **Git-om**, otvorenim izvorom za sistem kontrole vaših izdanja, pogotovo u kombinaciji sa **GitHub-om**, internet uslugom za čuvanje vaših **Git** repozitorija. U nastavku upoznaćemo vas sa **GitHub-om** i sa dobrom praksom da uključite upotrebu **Git-a** u svoj **R** projekat. 

Svakodnevno, potražnja za otvorenim i transparentim izvorima podataka raste, za njih su jednako zainteresovani kako vlade tako i građani kako bi poboljšali svoje životne uslove. Zajedno ćemo istražiti važnost otvorenog koda i identifikovaćemo gde se podaci otvorenog koda mogu lako naći na internetu. Radićete na studijama slučajeva koji su inspirasani stvarnim problemima i na onima koji su nam dostupni putem **otvorenih podataka**. 

## Ciljevi:

-	Da naučite kako pristupiti i pripremiti podatke za analizu. 

-	Da upoznate osnovne principe efektivne vizuelizacije podataka.

-	Da naučite osnovne tehnike za sumiranje podataka.

-	Da vizuelizujete podatke tako da vam ona pomogne u pronalaženju onoga što je značajno za objašnjenje podataka.

-	Da upotrebljavate R biblioteke alata da vizuelizujete geoprostorne probleme.

-	Da dizajnirate ponovljiva izveštavanja automatizovanjem procesa izveštavanja.

-	Da delite rezultate analize kao interaktivne, privlačne veb aplikacije koje su prijateljski ne-programerima.

- Da se upoznate sa mogućnostima R/R studija za obradu podataka koje će vam proširiti područje problema analize podataka koje će uspešno moći analizirati.


## Kako je organizovan kurs

Kurs je organizovan u tri dnevna modula. Svaki modul traje ukupno po tri i po sata, a podeljen je na dva i po sata interaktivne radionice i na poslednji sat koji je rezervisan za pitanja i diskusiju.

Kurs vode [Tatjana Kecojevic](https://www.linkedin.com/in/tatjana-kecojevic-803704143/) i [Dusko Medic](https://www.linkedin.com/in/duskomedic/) koji će pokriti različite teme kroz odgovarajuće studije slučaja, prezentacije i čitanja. Konceptualni modeli zaživeće kroz praktičnu primenu **R-a**, a od polaznika se očekuje da nastave da vežbaju i ponavljaju znanja koja su usvojila na kursu.

Od polaznika se očekuje da prođu sve delove kursa bez izuzetka, a posebno da pokušaju da reše bilo koji unapred predstavljen zadatak i da budu spremni da razgovaraju sa problemima sa kojim se susreću i da raspravljaju o idejama i bilo kojim postavljenim pitanjima. 

{{% notice tip %}}Na kraju svakog modula, preporučujemo da uradite sledeće:

* Pročitate preporučenu literaturu i prođete kroz postavljene zadatke,
* Učestvujete u diskusiji,
* Dodatno uvežbavate naučeno iz preporučenih tutorijala i izvora.
{{% /notice %}}


## Za koga je ovaj kurs

Ovaj kurs namenjen je svima koji nameravaju da komuniciraju koristeći podatke. Biće od koristi svima koji su zainteresovani i imaju želju da uđu u svet analize podatka. Trudićemo se da shvatite ovaj svet i da vas naučimo da efikasno i na atraktivan način vizuelizujete svoje analize i uspešno ih komunicirate. Sa znanjem stečenim na ovom kursu, bićete spremni da otpočnete svoju prvu analizu podataka.

**Nauka o podacima** nije samo reč koja je u trendu, već disciplina koja sadrži alate koji osnažuju svakodnevni život raznim podacima, tako da bez obzira iz kog sektora ili industrije dolazite, kurs će vam biti relevantan!

Za uspešno pohađanje kursa, prethodno iskustvo nije neophodno.

Kurs će biti održavan na BHSC i engleskom jeziku!


-----------------------------
© 2019 Tatjana Kecojevic

---
date: "2016-04-09T16:50:16+02:00"
title: Git i GitHub
weight: 3
---

## Zašto ih trebamo i o čemu je reč? 🤔

Kada radite na projektima obrade podataka kreiraćete velik broj dokumenata koje bi voleli da možete da menjate i da ih uredite u određenu strukturu. Takođe, vaš rad može biti dodatno doterivan i razvijan od strane drugih koji su zainteresovani za njega, da bi im to omogućili neophodno je da im on bude negde dostupan na uvid. Ovaj posao možete prepustiti besplatnom i otvorenom podrškom sistema za kontrolu verzija vašeg rada (version control system) integracijom Git-a u vaš projekat. Git je alat koji prati sve vaše verzije rada, promene u njemu, ali i omoguću je vam da delite ove promene svim zainteresovanim. Ove Git konfigurisane verzije vašeg rada nalaze se u setovima koje nazivamo repozitoriji ili repos, a oni su organizovani na visoko strukturisan način. 

Da bi obezbedili mesto na internetu gde će te postavljati vaš rad i projekte neohpodno je da ga „hostujete“ (postavite) na veb stranici GitHub. Ta stranica će akumulirati sva vaša dokumenta i fajlove koje razvijate.

## Setovanje Git-a

Ukoliko niste do sada koristili Git ili GitHub, počnite sa njihovom instalacijom i otvaranjem naloga na GitHub-u. Zatim ih povežite.

1)	Otvorite nalog na GitHub-u i zapamtite vašu korisnički nalog i lozinku.

2) Zatim, instalirajte Git sa [git-scm-a](https://git-scm.com/downloads). Napomena: Git-scm će automatski otkriti vaš operativni sistem i ponuditi vam odgovarajuću verziju za preuzimanje.

3) Recite Git-u svoje ime i email adresu. Tako ćete povezati svoj Git sa GitHub-om što će vam omogućiti da počnete saradnju sa drugima, biće jasno svima koje promene ste napravili. 

### Instalacija Git-a na Mac-u

Pre nego što napraviti prvi korak proverite da eventualno već nemate instaliran Git na vašem računaru (Napomena: Git bi trebalo da je već instaliran na Mac-ovima).

Otvorite vaš terminal i ukucajte

```
git --version
```
Trebao bi dobijete nešto poput ovoga dole

```
git version 2.18.0
```

U slučaju da imate stariju verziju od trenutno dostupne ili nemate git instaliran otidite na veb stranicu: [git-scm.com](https://git-scm.com).

Kada instalirate poslednju verziju Git-a na svom Mac-u identifikujte se kucajući sledeće komande u svoj terminal:

```
git config --global user.email "your@email.com"
git config --global user.name "your name"
```


### Instalacija Git-a na PC-u

Pokrenite CMD program tako što ćete kucati CMD u prozoru za pretragu (search). Tako ćete otvoriti command prompt prozor u kojem trebate da ukucate sledeću naredbu, prvo da proverite da li Git već postoji na vašem računaru:

```
git --version
```

Ukoliko Git nije prepoznat, to znači da treba da ga instalirate sa sledeće stranice <https://gitforwindows.org>. Skinite sa sajta neophodan file i startujte instalaciju tako što ćete odabrati osnovnu (default) instalaciju. Zatvorite svoj command prompt prozor da omogućite promenu na vašem sistemu i otvorite ga ponovo. Kada to uradite ponovite prethodno gore navedenu komandu, da proverite da li ste ispravno instalirali Git i koja mu je verzija.

Pošto ste ispravno instalirali Git potrebno je da registrujete svoju email adresu i vaše ime:

```
git config --global user.email "your@email.com"
git config --global user.name "your name"
```


<http://rstudio-pubs-static.s3.amazonaws.com/272737_7d6178a0e50043528d9ba636fdde209e.html>

## Povežite vaš Rstudio da komunicira sa GitHub-om 🤓

RStudio sadrži integrisane mogućnosti da vam obezbedi lakšu upotrebu Git-a. Treba da jednom prođete kroz ovo setovanje.

Kada otvarate u Rstudiju novi projekat, da biste omogućili komunikaciju između RStudija i GitHub-a, potrebno je da uradite sledeće:

- Odredite direktorij (ili folder) na vašem računaru na kom će se projekat nalaziti.
- Otvorite novi projekat u RStudiju.
- Otvorite novi Git repozitorijum.

{{% notice note %}}
Možda će vam biti teško da pravilno koristite Git is početka, ali kao i sa drugim alatima koje budete koristili biće vam mnogo lakše kako budete više vežbali. Vežbom do savršenstva!  
{{% /notice %}}

Kako da povežete GitHub sa RStudijom možete više naći u materijalu koji je dostupan na sledećoj internet stranici [RStudio's website](https://support.rstudio.com/hc/en-us/articles/200532077-Version-Control-with-Git-and-SVN). 

Prvo ćemo setovati SSH ključ koji će nam omogućiti sigurnu komunikaciju sa GitHub veb stranicom za koju nam neće trebati svaki put lozinka. Da bi ovo uradili sledite instrukcije [`Git and GitHub`](http://r-pkgs.had.co.nz/git.html) sekcije [Hadle's](http://hadley.nz) knjige [R Packages](http://r-pkgs.had.co.nz).

Više o detaljima upotrebe GitHub-a i njegovo dalje istraživanje možete naći u [`Chapter 9: Connect to GitHub`](https://happygitwithr.com/push-pull-github.html) poglavlju [Jenny's](https://jennybryan.org) knjige [Happy Git and GitHub for the useR](https://happygitwithr.com/index.html).

{{% notice tip %}}
Možda će vamj biti od koristi da bookmarkujete sledeći link [GitHub Cheet Sheet](https://education.github.com/git-cheat-sheet-education.pdf)!
{{% /notice %}}

-----------------------------
© 2019 Tatjana Kecojevic

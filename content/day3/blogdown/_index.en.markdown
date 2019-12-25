---
date: "2016-04-09T16:50:16+02:00"
title: blogdown
output: 
  learnr::tutorial
weight: 3
---

## blogdown: Kreiranje veb stranica sa R Markdown-om

"Dobro dizajniran i održavan veb sajt može biti od velike koristi da se predstavite i da vas ljudi upoznaju, nema potrebe da čekate svoju šansu da na nekoj od konferencija ili na nekoj drugoj prilici se lično predstavite. S druge strane, internet prezentacije takođe su korisne da čuvate informacije o onome šta ste radili ili o čemu ste razmišljali. Nekad ćete se vratiti na izvesni stari vaše tekst da se podsetite trikova ili metoda koje ste već ranije savladali, ali i zaboravili." [Yihui Xie](https://yihui.name/en/)[blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/)

 

U ovom odeljku naučićete kako da kreirate statičke veb stranice upotrebom paketa [HUGO](https://gohugo.io) i [R Markdown](https://bookdown.org/yihui/rmarkdown/)

<img src="images/rmd_hugo_blogdown.png" width="600px" />

#### Šta je blogdown?

Od Yihui-ja: <https://slides.yihui.name/2017-rmarkdown-UNL-Yihui-Xie.html#35>.

- [R Markdown](https://rmarkdown.rstudio.com) <img src="https://www.rstudio.com/wp-content/uploads/2015/12/RStudio_Hex_rmarkdown.png" width="10%" align="right" />
    - (relativno) jednostavna sintaksa za pisanje dokumenata
    
    - što je jednostavniji, prenosiviji je (više izlaznih formata)
    
    - ne samo da je zgodan (za održavanje), već i ponovljiv (reproducible)
    
    - većina karakteristika R Markdown-a  _i_ [**bookdown-a**](https://bookdown.org) (podrazumeva tehničko pisanje)!!



- [Hugo](https://gohugo.io) <img src="https://gohugo.io/img/hugo.png" width="10%" align="right" />

    - slobodan, otvorenog koda, i lak za instalaciju
    
    - munjevito brz (generiše stranicu u milisekundi)
    
    - opšte je namene (ne samo za blogove)

##### Zašto ne WordPress, Tumblr, Medium.com, Blogger.com, itd?

Od Yihui-ja: <https://slides.yihui.name/2017-rmarkdown-UNL-Yihui-Xie.html#36>.

- Ne postoji R Markdown podrška (sama podrška za matematiku ili ne postoji ili nije baš od velike koristi)

- Ogromne su prednosti statičkih veb stranica u poređenju sa dinamičkim
    - o	Svi fajlovi su statični, nema PHP-a ili baza podataka, nema logovanja/šifri, rad bilo gde (čak i bez internet veze, offline)
    
    - o	obično se vrlo brzo pristupa sajtu (nema potrebnih računjanja koje pokreće server), a jednostavan da se dodatno ubrza preko CDN-a.


### Napravite vašu veb stranicu

Krenućemo korak po korak. Počećemo sa postavljanjem GitHub repozitorijuma za naš veb sajt projekat.

##### Priprema GitHub-a

Već smo upoznati sa osnovama rada u GitHub-u, a možete to još jednom pogledati i proučiti na [Happy Git with R](http://happygitwithr.com) kako da povežete RStudio sa svojim GitHub nalogom.


<img 
src="http://happygitwithr.com/img/watch-me-diff-watch-me-rebase-smaller.png" align="middle" img width="60%"  
/>

Pretpostavljamo da ste već upoznati sa i da jeste:

☑️ Capter 5: [Registrovali GitHub nalog ](http://happygitwithr.com/github-acct.html)

☑️ Chapter 6: [Instalirali ili osvežili najnoviju verziju R-a i RStudija ](http://happygitwithr.com/install-r-rstudio.html)

* Otidite na svoj GitHub nalog i kreirajte novi repozitorijum

<img src="images/New_Repo.png" width="200px" style="display: block; margin: auto auto auto 0;" />

* Dajte mu odgovarajuće ime 
<img src="images/Create_New_Repo.png" width="300px" style="display: block; margin: auto auto auto 0;" />

* Kopirajte **HTTPS** adresu repozitorijuma
<img src="images/HTTPS_GitHub.png" width="350px" style="display: block; margin: auto auto auto 0;" />

##### U RStudiju

* Otvorite novi projekat u RStudiju: **File** ➡️ **New Project...**
<img src="images/RS_New_Project.png" width="250px" style="display: block; margin: auto auto auto 0;" />

* Selektujte **Version Control** ➡️ **Git**
<img src="images/Select_Version_Control.png" width="250px" style="display: block; margin: auto auto auto 0;" />

* Umetnite adresu vašeg Git repozitorijuma  
<img src="images/set_up_git_connection.png" width="250px" style="display: block; margin: auto auto auto 0;" />

#### Instalirajte paket

* Instalirajte <span style="color:red">**blogdown**</span>

`install.packages("blogdown")`


* Instalirajte <span style="color:red">**Hugo**</span> upotrebom blogdown-a

`blogdown::install_hugo()`


💡!Ukoliko ste već instalirali ove pakete, možete proveriti da li imate najnoviju verziju <span style="color:red">Hugo</span> paketa

`blogdown::hugo_version() # check version`

`blogdown::update_hugo() # force an update`

💡! Ukoliko imate problema sa instalacijom probajte je uraditi na ovaj način:

`install.packages("blogdown", repos = "http://cran.us.r-project.org")` 🤞

#### Napravite vebsajt

Usvojićemo pristup *jednostavno je lepo* i počećemo praviti vebsajt upotrebljavajući <span style="color:red">osnovnu temu</span>.

`blogdown::new_site()`

💡! Ukoliko vam se osnovna tema ne sviđa, probajte da instalirate neku drugu (na primer: *hugo-academic*):

`blogdown::new_site(theme = "gcushen/hugo-academic", theme_example = TRUE)`


Da vidite koje su vam sve **Hugo teme** dostupne idite na <https://themes.gohugo.io/>.

Prvo se upoznajte sa i familizirajte sa `blogdown-om` i `Hugom`.🧐 Jednom kada to uradite sa `blogdown` i `Hugo` lako ćete prelaziti sa teme na temu, lako ćete ih menjati. 💇 <https://bookdown.org/yihui/blogdown/other-themes.html>

#### Struktura HUGO sajtova

<img src="images/Site_Structure.png" width="200px" style="display: block; margin: auto;" />

<img src="images/main_structure.png" width="200px" style="display: block; margin: auto;" />

<https://gohugo.io/getting-started/directory-structure/>

#### Pokrenite server sajta

* U konzoli ukucajte:

`blogdown::serve_site()` 

ili, u meniju `Addins` izaberite `servesite` 

<img src="images/Serve_Site.png" width="200px" style="display: block; margin: auto;" />

Nemojte gledate vaš sajt u malenom RStudio pregledaču, umesto toga kliknite na opciju <span style="color:red">Show in new window</span>.

<img src="images/show_in_new_window.png" width="250px" style="display: block; margin: auto;" />

#### Notacija koju ćemo usvojiti

- **Kosa crta (trailing slash)** na kraju imena direktorija omogućiće vam referencu na taj direktorijum tj. `content/` znači da se referišete na direktorijum koji se zove *content*, a ne na fajl imena *content*, na koji biste se referisali ukoliko ne biste stavili kosu crtu na kraju imena direktorijuma.

<img src="images/trailing_slash.png" width="150px" style="display: block; margin: auto auto auto 0;" />

- **Vodeća kosa crta (leading slash)** ukazaće vam na osnovni direktorijum u kojem se nalazi vaš *projekt vebsajt*, tj. `/content/about.md` podrazumeva da se referišete na fajl `about.md` koji se nalazi u osnovnom (root) direktorijumu vaše vebsajt projekta.  

<img src="images/leading_slash.png" width="150px" style="display: block; margin: auto auto auto 0;" />

### Izgradite stranicu korak po korak

#### 👉 Otidite na sledeći link da biste preuzeli radni materijal: <https://github.com/TanjaKec/BlogdownWS>

##### Odavde sledićemo korake koji su nam dati u Xaringan prezantaciji koja nam je dostupna  [ 👉 ovde](https://tanjakec.github.io/BlogdownWS/Blogdown_WS_Slides/blogdown_workshop.html)

### Sretno blogovanje! 📢 



-----------------------------
© 2019 Tatjana Kecojevic

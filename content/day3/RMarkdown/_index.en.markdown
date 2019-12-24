---
date: "2016-04-09T16:50:16+02:00"
title: RMarkdown
output: 
  learnr::tutorial
weight: 1
---

R Markdown vam može pomoći u kreiranju:

- HTML dokumenata
- Beležnice (Notebooks) u kojima pojedinačno izvodite delove koda
- PDFs datoteke koje možete isprintati da biste fizički pratili ovaj kurs
- Ovih veb stranica iz kojih pratite ovaj R kurs

On vam omogućava da:

- Snimite i izvršite kod i prikažete njegove rezultate
- Kreirate visoko kvalitetne izveštaje koje mogu da uključe i [LaTeX](https://www.latex-project.org/) jednačine

Ono što je posebno dobro kod [R Markdown](https://rmarkdown.rstudio.com/) dokumenata je da su oni u potpunosti ponovljivi i da podržavaju mnoge statičke i dinamičke formate izlaza, da nabrojimo samo neke: PDF, HTML, MS Word, Beamer… Možete ugraditi narativni tekst i kod svoje analize da  biste proizveli elegatno oblikovano uputstvo za vaše čitaoce.

Postoji varijanta [Markdown-a](https://daringfireball.net/projects/markdown/) koja embeduje **R kod delove** (označene sa tri apostrofa), koje možete koristiti sa [knitr-om](https://yihui.name/knitr/) da proizvedete ponovljive izveštaje koje će biti na internetu. 

R Markdown je osnovni text fajl koji se završava sa ekstenzijom <span style="color:red">.Rmd</span>

Da bi koristili **R Markdown** neophodno je da instalirate paket sa [CRAN](https://cran.r-project.org/) i da ga učitate na sledeći način:


```r
install.packages("rmakdown", repos = "http://cran.us.r-project.org")
suppressPackageStartupMessages(library(rmarkdown))
```

#### 👉 Otidite na sledeći GitHub repozitorijum da skinete materijal: <https://github.com/TanjaKec/RMarkdown_Intro>

### Kako početi RMarkdown

**<span style="color:red">Zadatak 1</span>:**
Otvorite sledeći fajl `RMarkdown_Intro.Rmd`

- Promenite naslov Markdown dokumenta iz `My First Markdown Document` u `RMarkdown Introduction`.

- Kliknite dugme **"Knit"** da vidite vaš kod.


##### Čestitamo! Upravo ste knitovali svoj prvi Rmd dokument!!!! 👍😃

#### Osnovno editovanje teksta

**<span style="color:red">Zadatak 2</span>:**
Formatirajmo dalje ovaj dokument tako što ćemo

- Promenite ime autora dokumenta i upišite svoje ime

- Prepravite prvu rečenicu dokumenta i napišite “Ovo je moj prvi R Markdown dokument.”

- Prekoponujte dokument kako biste mogli da vidite svoje izmene

#### Dodavanje linka

Pojedinu reč možete pretvoriti u link tako što ćete je umetnuti u **uglaste zagrade: [ ]** a zatim ćete sam link postaviti iza u **zagrade: ( )**, kako je to prikazano dole:

`[RStudio](www.rstudio.com)`

**<span style="color:red">Zadatak 3</span>:**
Napravite GitHub link u sledećem paragrafu https://github.com/DataTeka

#### Formatiranje teksta 

Da biste formatirali određeni tekst u vašem dokumentu sa Markdown-om, treba da ga postavite tako da bude okružen:

- sa jednim asteriksom da bi bio kurziv: *italic*

- sa dva asteriksa da bi bio bold: **bold** and

- apostrofima da bi bio podvučen: `monospaced`.

Da biste napravili list nabrajanja potrebno je da svaku stavku u listi postavite u novu liniju i da ispred nje stavite broj, tačku posle njega i razmak (space):
1. order list
2. second item

💡! Zapazite da je neophodno da ostavite prazan red između liste i paragrafa koji joj prethodi.

**<span style="color:red">Zadatak 4</span>:**

- Napravite da sledeći paragraf u vašem Rmd dokumentu liči na sledeći:

When analysing data,... The variables can be one of two broad types:

1) **Attribute variable**: has its outcomes described in terms of its characteristics or
attributes;

2) **Measured variable**: has the resulting outcome expressed in numerical terms.

- Napravite da reč Knit u sldedeć paragrafu bude italic.


#### Embedovanje `R` koda 
Da biste emdedovali R kod u vašem dokumentu treba da koristite tri apostrofa:

<p><code  class="r"> ```{r} </code>

` chunk of code`

<p><code  class="r"> ``` </code>

**<span style="color:red">Zadatak 5</span>**: Zamenite set podataka `cars` sa `gapminder` setom podataka. Ne zaboravite da učitate `gapminder` paket upotrebom komande `library(gapminder)`.


#### Zaštite `R` kod od njegovog štampanja

Vaš kod možete embedovati postavljaći `echo = FALSE` da se on ne bi štampao kod koji treba da vam generiše grafik:

<p><code  class="r"> ```{r, echo=FALSE} </code>

` chunk of code`

<p><code  class="r"> ``` </code>

**<span style="color:red">Task 6</span>**: Zamenite osnovni grafikon koji uporećuje varijable `mpg` i `cyl` sa `ggplot`-ovim grafikon da istražite povezanost varijabli `continent` i `lifeExp` (ne zaboravite da koristite i neke druge `dplyr` funkcije!).



```r
suppressPackageStartupMessages(library(dplyr))
library(ggplot2)
# ggplot boxplot
ggplot(gapminder, aes(x = continent, y = lifeExp)) +
  geom_boxplot(outlier.colour = "hotpink") +
  geom_jitter(position = position_jitter(width = 0.1, height = 0), 
              alpha = .2) +
  labs (title= "Life Exp. vs. Continent", 
        x = "Continent", y = "Life Exp.") +
  theme(legend.position = "none", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5))    
```

#### Dodavanje **LaTex** jednačina

Konačno, ako želite da dodate matematičke jednačine u vaš Markdown dokument to možete uraditi embedovanjem [LaTeX]( LaTeX ) matematičkih jednačina u svoj izveštaj.

Da biste *prikazali jednačinu* **odvojenu u svom redu** neophodno je da je okružite sa dvostrukim simbolom dolara

`$$` `y = a + bx` `$$`, 

Ili ukoliko želite da *prikažete jednačinu* **u liniji zajedno sa tekstom** onda ćete jednačinu okružiti sa jednim dolar simbolom: `$y = a + bx$`.

**<span style="color:red">Zadatak 7</span>**: Prikažite jednačinu u *Including Mathematical Equations* paragrafu u svojoj posebnoj liniji.


#### Čestitamo! Usvojili ste osnove za kreiranje elegantnih dinamičkih dokumenata… !!!! 👍😃


Sledeće stranice naćićete vrlo korisne za vaše dalje učenje:

- [RMarkdown cheatsheet](https://www.rstudio.com/wp-content/uploads/2016/03/rmarkdown-cheatsheet-2.0.pdf)

- [The R Markdown Reference Guide](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf)

- Knjiga: [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/)

- [Getting started with R Markdown](https://www.rstudio.com/resources/webinars/getting-started-with-r-markdown/)

- [R Markdown Quick Tour](https://rmarkdown.rstudio.com/authoring_quick_tour.html)

- [Advanced R Markdown – Tutorial::RStudio Conference 2017](https://www.rstudio.com/resources/videos/advanced-r-markdown-tutorial/)



-----------------------------
© 2019 Tatjana Kecojevic

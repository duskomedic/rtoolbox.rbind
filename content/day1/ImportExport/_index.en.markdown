---
date: "2016-04-09T16:50:16+02:00"
title: Uvoz podataka u R
output: 
  learnr::tutorial
weight: 8
---

Prva je velika stvar u upravljanju podacima u R-u. 

Najverovatnije je da imate iskustvo u pregledanju, organizovanju i istraživanju vaših podataka u Excel-u.

Otvaranje podataka u R-u prilično je jednostavno, ali njihovo organizovanje za analizu potrebno je da se oni prethodno i promisle. Pretpostavljate da pomoću komandi iz glavnog menija **File | Import Dataset** u R studiju možete uvesti vaše podatke (za više pogledajte [Importing Data with RStudio](https://support.rstudio.com/hc/en-us/articles/218611977-Importing-Data-with-RStudio)), međutim mi ćemo to uraditi na pravi način upotrebom komande.

U R možete uvesti sledeće tipove podataka:

- (Tab, Blank space) Delimited Text
- CSV files
- Excel files
- JSON 
- SAS
- STATA
- MiniTab
- SPSS...

U ovom poglavlju pokazaćemo vam kako da pristupite uobičajene tipove podataka. Jednom kada počnete da se igrate sa podacima i menjati ih na način koji vam odgovara za vašu analizu, biće vam zanimljivo istražiti kako možete podatke sami pisati. Ovde, međutim, nećemo vam pokazati kako to da uradite, već ćemo se fokusirati na osnovnu funkcionalnost funkcije `read` u R-u. 

### R baza

Najednostavnija forma podataka je [text file](https://en.wikipedia.org/wiki/Text_file). Text fajl može da pročita bilo koji operativni sistem kao i velik broj različitih statističkih programa. Čuvanje vaših podataka u tekst fajlu čini vaše podatke lako dostupnim svima. Ukoliko imate tekst fajl sa podacima koje želite da koristite, možete ih jednostavno uvesti sa funkcijom **R Baze (R base)** `read.table()`

Sledeća naredba čita fajl u tabelarnom formatu i kreira data okvir

```
# Read tabular data into R
df_txt <- read.table(file_name.txt, header = FALSE)
```

Postoji mnogo paketa koji vam omogućuju uvoz podataka u R, a mi ćemo početi od `CSV` fajlova s obzirom da su oni najčešći.

Zarezom odvojeni fajlovi najčešći je način snimanja podatake u tabelama, jer oni nisu zaštićeni niti traže licencirane programe za njihovo otvaranje. Uvoz `CSV` fajla je deo baze R i možete to uraditi pomoću funkcije `read.csv()`. 


##### `read.csv()`

Pogledajmo sad internet stranicu <https://data.gov.rs/> otvorenih podataka Srbije. Posebno, obratićemo pažnju na fajl [Kvalitet vazduha 2017: pm2.5_2017.csv](https://data.gov.rs/sr/datasets/kvalitet-vazduha-2017/) i njega ćemo uvesti u R.

Ovaj fajl neće snimiti na naše računare, već ćemo ih uvesti u R direktno sa interneta koristeći dati link.


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

Na drugi način možete uvesti ove podatke tako što ćete ih snimiti u svoj radni direktorijum.

Preuzmimo sad fajl ["Kvalitet vazduha 2017-SO2: 2017-SO2.csv"](https://data.gov.rs/sr/datasets/r/f425e6a5-95ae-4e2b-ab73-1d0b293b4522)
i snimimo ga u naš radni direktorijum našeg R projekta pre nego što počnemo da ga koristimo

```
df_csv <- read.csv("2017-so2.csv", stringsAsFactors = FALSE, fileEncoding = "latin1")
```

{{% notice info %}}
Ponovo pokrenite kode prikazan gore, ali ovog puta bez argumenta `stringsAsFactors`, tako što ćemo ga ukloniti ili mu staviti znak jednakosti sa TRUE. Možete li nam reći kakva je razlika pre i posle? Šta mislite zašto koristimo argument  `fileEncoding`?
{{% /notice %}}

Kako vam se čine ovaj set podataka koji ste uvezli? 🤔

#### Upotreba readr::read_csv()

`readr` je paket koji čita pravougaone podatke znatno brže od **baze R** `read.cdv()`. Pored toga ovaj paket i njegova `read.csv()` funkcija pretpostavlja karaktere kao stringove, a ne kao faktore.

Da biste videli kako je lako koristiti druge pakete za uvoz podataka u R, ilustrovaćemo to upotrebom read.csv() funkcije.

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

### Uvoz excel fajlova sa `readxl`

Uvoz podataka iz Excel fajlova nije tako jednostavno, s obzirom da ti fajlovi mogu sadržavati više šitova. Fokusiraćemo se na upotrebu `readxl` paketa s obzirom da se on do sada pokazao kao najefikasniji za taj posao.  

{{% notice warning %}}
Da biste pristupili podacima iz Excel shita možete jednostavno samo kopitari i umetnuti URL fajla. Međutim taj fajl trebate prethodno snimiti.
{{% /notice %}}

Sada ćemo snimiti podatke iz Excel fajla sa stranice otvorenih podataka [data.gov.rs](https://data.gov.rs/) podatke o saobraćajnim nesrećama [Подаци о саобраћајним незгодама до 31.08.2019. године за територију свих ПОЛИЦИЈСКИХ УПРАВА и ОПШТИНА](https://data.gov.rs/sr/datasets/r/134b2867-8a35-4f00-ac48-1610dca177ec). 

Ukoliko ne možete da otvorite fajl u Excelu da vidite koliko šitova taj fajl ima, pokušajte pročitati fajl iz R-a tako što ćete pristupiti prvom šitu funkcijom `read_excel()`. Pre toga, uverite se da ste snimili taj fajl u radni direktorijum vašeg R projekta, i to pre nego što ga pokušate izvršiti sledeći prikazan kod:

```
## If you don't have readxl installed yet, uncomment the line below and run it 
#install.packages("readxl")
library(readxl)
df_xl <- read_excel("nez-opendata-20199-20190925.xlsx", sheet = 1)
```

Šta mislite?

{{% notice warning %}}
Ljudi uobičajeno ulepšavaju i formatiraju svoje excel fajlove, a to može prouzrokovati probleme u njihov uvoz u R.
{{% /notice %}}

Istražite argumente funkcije `read_excel()`, poput `skip` argumenta sa kojim možete da specifikujete minimalni broj redova koje ne želite da učitate iz fajla.

### Uvoz podataka upotrebom `jsonlite`

Ukoliko želite da uvezete JSON fajl u R upotrebljavaćete `jsonlite` paket. Potrebno je da ukažete na fajl tako što ćete ovoj funkciji obezbediti lokalnu putanju do njega, ukoliko se on već nalazi na vašem računaru ili jednostavno samo URL ukoliko želite da uveze sa interneta. 


```r
## If you don't have readxl installed yet, uncomment the line below and run it 
#install.packages("jsonlite")
library(jsonlite)
my_url <-"https://data.gov.rs/sr/datasets/r/41c2fe91-4ea1-4a64-b33c-183665ea6ab3"
polen <- fromJSON(my_url)
```

Pogledajte sad strukturu `polen-a`! 😰


```r
str(polen)
```

```
## List of 4
##  $ count   : int 26419
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

Napomena: komanda `polen$results` je okvir podataka koji sadrži listu `koncentracija (concentrations)` kao svoj element.

Ouch! 😳 JSON fajlovi nisu baš uredni 😱 Oni su često ugnježđeni, povezani -> shvatili ste: Vrlo neuredno! 😫 Dakle, ostavićemo ih takvim. 😬 IAko vam je potrebno da saznate više o čitanju JSON fajlova u R-u možete dodatno istražiti funckionalnost paketa `jsonlite` ili pronađite na stranici [Getting started with JSON and jsonlite](https://cran.r-project.org/web/packages/jsonlite/vignettes/json-aaquickstart.html). Blog [Working with JSON data in very simple way](https://blog.exploratory.io/working-with-json-data-in-very-simple-way-ad7ebcc0bb89) autora [Kan Nishida](https://blog.exploratory.io/@kanaugust) u njemu ćete naći odlične primere kako možete koristiti ove podatke u R-u. 

### Drugi formati podataka

Da biste ubrzali procesa čitanja txt, csv fajlova možete koristiti `data.table::fread()` funkciju. Potrebno je da ovoj funkciju samo obezbedite ime fajla u kom se nalaze podaci koje želite da uvezete, a `fread()` će pokušati da vam uveze odgovarajuću njihovu strukturu. Pogledajte ovaj blog [Getting Data From An Online Source](https://www.r-bloggers.com/getting-data-from-an-online-source/) da vidite još neke ideje za uvoz podataka. 

R zajedno sa odgovarajućim paketima možete koristiti i za uvoz drugih formata podataka. Paket `haven` omogućuje vam funkcije za uvoz SAS, SPSS i Stata fajlova ili možete upotrebljavati `foreign` paket za MiniTab fajlova. Pregledajte help sekciju paketa sa kojim želite da se upoznate ali i da otkrijete koje sve druge opcije on poseduje.


## ZADACI 👇

1) Pregledajte stranicu otvorenih podataka <https://data.gov.rs/> i pronađite temu koja vas zanima.

2) Pogledajte setove podataka na ovoj stranici koja se nalazi u odeljku:  [saobracaj](https://data.gov.rs/sr/datasets/podatsi-o-saobratshajnim-nezgodama-po-politsijskim-upravama-i-opshtinama/). Razmislite koje pitanja možete postaviti na osnovu tih podataka.



-----------------------------
© 2019 Tatjana Kecojevic

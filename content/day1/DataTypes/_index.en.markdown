---
date: "2016-04-09T16:50:16+02:00"
title: Tipovi podataka
output: 
  learnr::tutorial
weight: 7
---

U primerima koje smo koristili u poglavlju „Kako da koristimo R“ radili smo sa brojevima (kvantitativnim numeričkim podacima). Oni koji imaju iskustva u programiranju znaće da se numerički objekti mogu klasifikovati kao realni (real), celi (integer), dupli (double) ili kompleksni (complex). Da biste proverili da li je reč o numeričkom objektu i kom tipu je reč, upotrebljavate funkciju `mode()` i `class()`, respektivno.

Vratimo se našem R projektu i ukucajmo sledeće funkcije u otvorenom script file i pokrenimo kod.😃


```r
x <- 1:10
mode(x)
```

```
## [1] "numeric"
```

```r
class(x)
```

```
## [1] "integer"
```

Da biste u R-u uneli nizove znakova kao objekte trebate to da uradite tako što će te ih uneti pomoću znakove navodnika. Podrazumevano se očekuje da će svi unosi biti numerički ukoliko ne koristite navodnike, ako ih unosite zajedno sa znakovima, oni će se smatrati brojevima i nakon toga R će vam vratiti poruku o grešci.


```r
x <- c("UK", "Spain", "Serbia", "France", "Germany", "Italy")
mode(x)
```

```
## [1] "character"
```

Uobičajeno je da u statističkim podacima imate atribute poznate kao kategoričke varijable. U R-u takve varijable specifikujemo kao **factore**. Atributske varijable poseduju set nivoa koji indikuju moguće rezultate. Dakle, ukoliko želimo da nam x bude atributska varijabla sa pet nivoa, potrebno je da ga predstavimo kao faktor R-u.


```r
x <- c("UK", "Spain", "Serbia", "France", "Germany", "Italy")
x <- factor(x)
x
```

```
## [1] UK      Spain   Serbia  France  Germany Italy  
## Levels: France Germany Italy Serbia Spain UK
```

{{% notice note %}}
💡: Imajte na umu da R označava nivo faktora prema abecednom redu. Međutim, promenljive atributa se obično kodiraju i obično biste ih uneli kao takve.
{{% /notice %}}


```r
quality <- factor(c(3, 3, 4, 2, 2, 4, 0, 1))
levels(quality)
```

```
## [1] "0" "1" "2" "3" "4"
```

```r
quality
```

```
## [1] 3 3 4 2 2 4 0 1
## Levels: 0 1 2 3 4
```

Povremeno upotrebljavaćete **logičke** tipove podataka. Ovo ćete raditi kada nešto želite da zabeležite kao TAČNO ili NETAČNO. Najverovantnije je da ćete ovaj tip podataka upotrebljavati kada želite da proverite da li određena varijabla je određeni tip podaka. Na primer


```r
x <- c("UK", "Spain", "Serbia", "France", "Germany", "Italy")
is.numeric(x)
```

```
## [1] FALSE
```

```r
is.factor(x)
```

```
## [1] FALSE
```

### Okviri podataka

Statistički podaci uobičajeno se sastoje od nekoliko vektora iste dužine i različitih tipova koje ćete predstaviti tabelarno. Ovi vektori su međusobno povezani tako da podaci u istoj poziciji dolaze iz iste eksperimentalne jedinice tj. osmatranja. R koristi okvire podataka za beleženje takve vrste tabelarnih podataka i oni se smatraju kao deo primarne strukture podataka.

Razmotrimo studija cena akcija kompanija iz tri različita sektora poslovanja. Kao deo studije odabran je slučajan uzorak (n=15) kompanija i prikupljeni su sledeći podaci:


```r
share_price <- c(880, 862, 850, 840, 838, 799, 783, 777, 767, 746, 692, 689, 683, 661, 658)
profit <- c(161.3, 170.5, 140.7, 115.7, 107.9, 135.2, 142.7, 114.9, 110.4, 98.9, 90.2, 80.6, 85.4, 91.7, 137.8)
sector <- factor(c(3, 3, 3, 3, 3, 2, 2, 2, 2, 2, 1, 1, 1, + 1, 1)) # 1:IT, 2:Finance, 3:Pharmaceutical
#
share_price
```

```
##  [1] 880 862 850 840 838 799 783 777 767 746 692 689 683 661 658
```

```r
profit
```

```
##  [1] 161.3 170.5 140.7 115.7 107.9 135.2 142.7 114.9 110.4  98.9  90.2
## [12]  80.6  85.4  91.7 137.8
```

```r
sector
```

```
##  [1] 3 3 3 3 3 2 2 2 2 2 1 1 1 1 1
## Levels: 1 2 3
```

Umesto da ove setove podataka čuvate kao pojedinačne vektore u R, bilo bi bolje da ih sve zajedno čuvate u jednom objektu tj. u okviru podataka

```
share.data <- data.frame(share_price, profit, sector)
share.data
```

Do pojedinačnog vektora iz ovog okvira podataka možete doći upotrebom `$` simbola:

```
share.data$sector
```

Sada, pošto smo naučili osnovne stvari o tipovima podaka i njihovoj organiziji možemo preći na deo u kome ćemo govoriti kako ćete pristupati postojeći podacima iz R-a.




-----------------------------
© 2019 Tatjana Kecojevic

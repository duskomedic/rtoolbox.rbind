---
date: "2016-04-09T16:50:16+02:00"
title: Upravljanje podacima
output: 
  learnr::tutorial
weight: 1
---

### Kako to radimo? 🤔

![Red variant](/day2/DataWrangling/images/Program_HW.png?width=40pc)

Ovaj dijagram preuzet je iz knjige [R for Data Science](https://r4ds.had.co.nz/) autora [Garrett Grolemund](https://twitter.com/statgarrett
) i [Hadley Wickham](https://twitter.com/hadleywickham), inače odličnog izvora za učenje R-a. Takođe, bitno je da znate i da postoji velika zajednica okupljena oko R-a, i ne bi bilo loše da im se pridružite na: [R4DS online learning community](https://www.rfordatasci.com/).

### Skupovi podataka

Da biste naučili kako da organizujete podatke koristićemo alat `gapminder` skup podataka koji nam je omogućen preko gapminder paketa u R-u. Ovaj skup podataka u R je postavila [Jennifer Bryan](https://jennybryan.org/) iz rezervaoara skupova podataka koji su nam dati zahvaljujući [Gapminder-u](https://www.gapminder.org).

[Gapminder](https://www.gapminder.org) je nezavisna Švedska fondacija koja pomaže svetski održivi razvoj tako što sakuplja i analizira relevantne podatke ali i razvojem i kreiranjem raznog materijala za učenje. [Gapminder](https://en.wikipedia.org/wiki/Gapminder_Foundation) je osnovao u Švedskoj [Hans Rosling](https://en.wikipedia.org/wiki/Hans_Rosling) koji je rukovodio objavljivanju sveobuhvatne i pronicljive priče o globalnom razvoju upotrebom vizuelnih animacija.

Hansa u akciji možete videti u [BBC dokumentarcu](https://www.bbc.co.uk/programmes/p02q33dg) [The joy of Stats](https://www.youtube.com/watch?v=cdf0k545yDA) koji je dostupan na kanalu [YouTube](https://www.youtube.com).

##### Gapminder podaci

Za svaku od 142 svetske države, u ovom paketu date su vrednosti očekivanih godina starenja, Bruto domaći proizvod (BDP ili GDP) po glavi stanovnika, broj stanovnika svakih pet godina počevši od 1952. godine do 2007. godine.

Pre nego što počnete da pregledate ove podatke, pokrenite sledeći kod

```
# install necessary packages:
install.packages("dplyr", repos = "http://cran.us.r-project.org")
install.packages("ggplot2", repos = "http://cran.us.r-project.org")
install.packages("gapminder", repos = "http://cran.us.r-project.org")
```


```r
# have a look at the data 
head(gapminder::gapminder)
```

```
## # A tibble: 6 x 6
##   country     continent  year lifeExp      pop gdpPercap
##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Afghanistan Asia       1952    28.8  8425333      779.
## 2 Afghanistan Asia       1957    30.3  9240934      821.
## 3 Afghanistan Asia       1962    32.0 10267083      853.
## 4 Afghanistan Asia       1967    34.0 11537966      836.
## 5 Afghanistan Asia       1972    36.1 13079460      740.
## 6 Afghanistan Asia       1977    38.4 14880372      786.
```

{{% notice note %}}
💡Zapazite da ovde imamo 6 kolona, svaku od njih možemo nazivati varijablom.
{{% /notice %}}

**Opis**: Izvod podataka Gapminder-a koji sadrže informacije o očekivanoj godini života, BDP po glavi stanovnika i broj stanovnika po državi.

Glavni okvir podataka u gapminder-u ima **1704 reda** i **6 varijabli**:
- **država**: faktor ima 142 nivoa
- **kontinent**: faktor sa 5 nivoa
- **godina**: rasponi od 1952. do 2007. godine sa uvećanjem od 5 godina
- **lifeExp**: životni vek po rođenju, u godinama
- **pop**: broj stanovnika
- **gdpPercap**: BDP po glavi stanovnika


```r
gapminder::gapminder[1:3,]
```

```
## # A tibble: 3 x 6
##   country     continent  year lifeExp      pop gdpPercap
##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Afghanistan Asia       1952    28.8  8425333      779.
## 2 Afghanistan Asia       1957    30.3  9240934      821.
## 3 Afghanistan Asia       1962    32.0 10267083      853.
```

Prvo pogledajmo ove podatke upotrebom sledećih funkcija: <span style="color:red">`dim()`</span> & <span style="color:dim">`head()`</span>


```r
library(gapminder)
dim(gapminder)
```

```
## [1] 1704    6
```

```r
head(gapminder, n=10)
```

```
## # A tibble: 10 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       1957    30.3  9240934      821.
##  3 Afghanistan Asia       1962    32.0 10267083      853.
##  4 Afghanistan Asia       1967    34.0 11537966      836.
##  5 Afghanistan Asia       1972    36.1 13079460      740.
##  6 Afghanistan Asia       1977    38.4 14880372      786.
##  7 Afghanistan Asia       1982    39.9 12881816      978.
##  8 Afghanistan Asia       1987    40.8 13867957      852.
##  9 Afghanistan Asia       1992    41.7 16317921      649.
## 10 Afghanistan Asia       1997    41.8 22227415      635.
```

Možete nam reći šta svaka od ove dve funkcije radi⁉️

Da li nam je data informacija o strukturi podataka? 🤔 Možemo istražiti strukturu upotrebom <span style="color:red">`str()`</span> funkcije, ali rezultat može izgledati neuredno i teško je ga pratiti ako je skup podataka velik. 🤪


```r
str(gapminder) 
```

```
## Classes 'tbl_df', 'tbl' and 'data.frame':	1704 obs. of  6 variables:
##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
##  $ gdpPercap: num  779 821 853 836 740 ...
```

#### Paket `dplyr`

Paket <span style="color:red">**`dplyr`**</span> nam donosi gramatiku (reči) za upravljanje i za operacije nad okvirom podataka na tidy način. Ključni operatori i nazaobilazne reči ovog paketa su:

<span style="color:red">%>%</span>: operator “cevi” koristi se za povezivanje više glagolskih radnji u jedan cevodod.

<span style="color:red">select()</span>: vraća podskup kolona traženog okvira podataka.

<span style="color:red">mutate()</span>: dodaje nove varijable/kolone ili transformiše postojeće varijable.

<span style="color:red">filter()</span>: izdvaja podskup redova iz okvira podataka na osnovu logičkih uslova.

<span style="color:red">arrange()</span>: reorganizacija redova okvira podataka prema jednoj ili više varijabli.

<span style="color:red">summarise() / summarize()</span>: smanjite svaku grupu u jedan red izračunavanjem zbirnih mera.

Možemo da pogledamo podatke i njihovu strukturu pomoću funkcije <span style="color:red">`glimpse()`</span> iz `dplyr` paketa.


```r
suppressPackageStartupMessages(library(dplyr))
glimpse(gapminder) 
```

```
## Observations: 1,704
## Variables: 6
## $ country   <fct> Afghanistan, Afghanistan, Afghanistan, Afghanistan, Af…
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, …
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, …
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854…
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 148803…
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.…
```

{{% notice note %}}
🤓💡: Uočite da možemo da sprečimo prikazivanje poruka koje se pojavljuju prilikom aploadovanja paketa, upotrebom u ovom slučaju naredbe, `suppressPackageStartupMessages()`!
{{% /notice %}}

Sada kada smo uploadovali `dplyr` paket, pogledajmo neke od glagola. 😇

#### Operator cevi (pipeline operator): <span style="color:red">`%>%`</span>

**Leva strana (LVS)**   <span style="color:red">`%>%`</span>    **Desna strana (DSS)**

<span style="color:red">x %>% f(..., y)</span> 

<span style="color:red">    f(x,y)</span>

„Cevi“ **prosleđuju rezultat *LVS kao prvi argument operatora funkcije DSS**.

<pre>
<span style="color:red">3 %>% sum(4)</span>      <==>      <span style="color:red">  sum(3, 4)</span>
</pre>

<span style="color:red">`%>%`</span> je vrlo praktičan za vezivanje više <span style="color:red">`dplyr`</span> funkcija u niz operacija.

#### Izaberite promenjive prema njihovim imenima: <span style="color:red">`select()`</span>,

<img src="images/select().png" width="450px" />

- <span style="color:red">`starts_with("X")`</span> svako ime koje počinje sa "X".

- <span style="color:red">`ends_with("X")`</span> svako ime koje završava sa "X".

- <span style="color:red">`contains("X")`</span> svako ime koje sadrži "X".

- <span style="color:red">`matches("X")`</span> svako ime koje se poklapa sa “X”, gde “X” može biti regularni izraz.

- <span style="color:red">`num_range("x", 1:5)`</span>  varijable imenovane x01, x02, x03, x04, x05.

- <span style="color:red">`one_of(x)`</span> => svako ime koje se pojavljuje u x, koji bi trebalo da bude vektor karaktera.

##### 👉 Vežbajte ⏰💻: Selektujte vaše varijable

1) koje se završavaju sa slovom `p`

2) počinju sa slovima `co`. Pokušajte da izvršite ovaj zadatak koristići bazu R.  

##### 😃🙌 Rešenje:


```r
gm_pop_gdp <- select(gapminder, ends_with("p"))
head(gm_pop_gdp, n = 1)
```

```
## # A tibble: 1 x 3
##   lifeExp     pop gdpPercap
##     <dbl>   <int>     <dbl>
## 1    28.8 8425333      779.
```

```r
gm_cc <- select(gapminder, starts_with("co"))
head(gm_cc, n = 1)
```

```
## # A tibble: 1 x 2
##   country     continent
##   <fct>       <fct>    
## 1 Afghanistan Asia
```

Naravno ovo možemo uraditi i upotrebom **base R**, na primer:


```r
gm_cc <- gapminder[c("country", "continent")]
```

ali je ovaj način manje intuitivan i uobičajeno uključuje i više kucanja. 

#### Kreirajte nove varijable od postojećih: <span style="color:red">`mutate()`</span>

<img src="images/mutate().png" width="400px" />

Omogućiće vam da dodate u okvir podataka `df` novu kolonu, `z`, koja će biti rezultat množenja kolona `x` and `y`: `mutate(df, z = x * y)`.
Ukoliko želimo da posmatramo `lifeExp` dat u mesecima umesto u godinama, možemo napraviti novu kolonu `lifeExp_month`: 

```r
gapminder2 <- mutate(gapminder, LifeExp_month = lifeExp * 12) 
head(gapminder2, n = 2)
```

```
## # A tibble: 2 x 7
##   country     continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>       <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Afghanistan Asia       1952    28.8 8425333      779.          346.
## 2 Afghanistan Asia       1957    30.3 9240934      821.          364.
```

#### Izaberite opažanja prema njihovim vrednostima: <span style="color:red">`filter()`</span>
<img src="images/filter().png" width="450px" />

Postoji skup logičkih operatora u **R-u** koje možete koristiti unutar `filter()`:

- `x < y`: `TRUE` ukoliko `x` je manje od `y`
- `x <= y`: `TRUE` ukoliko `x` je manje ili jednako sa `y`
- `x == y`: `TRUE` ukoliko `x` je jednako sa `y`
- `x != y`: `TRUE` ukoliko `x` nije jednako sa `y`
- `x >= y`: `TRUE` ukoliko `x` je veće ili jednako sa `y`
- `x > y`: `TRUE` ukoliko `x` je veće od `y`
- `x %in% c(a, b, c)`: `TRUE` ukoliko `x` je vektor  `c(a, b, c)`
- `is.na(x)`:  je `NA`
- `!is.na(x)`: nije `NA`

##### 👉 Vežbajte ⏰💻: Filtrirajte vaše podatke

Upotrebite `gapminder2` `df` da filtrirate:

1) samo evropske države i snimite ih kao `gapmEU`

2) samo evropske države od 2000 pa nadalje i snimite ih kao `gapmEU21c`

3) redove u kojima je očekivani životni vek već od 80

Ne zaboravite ta **koristite `==` umesto `=`**! i ne zaboravite da koristite znake navoda **`""`**


##### 😃🙌 Rešenja:

```r
gapmEU <- filter(gapminder2, continent == "Europe") 
head(gapmEU, 2)
```

```
## # A tibble: 2 x 7
##   country continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>   <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Albania Europe     1952    55.2 1282697     1601.          663.
## 2 Albania Europe     1957    59.3 1476505     1942.          711.
```


```r
gapmEU21c <- filter(gapminder2, continent == "Europe" & year >= 2000)
head(gapmEU21c, 2)
```

```
## # A tibble: 2 x 7
##   country continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>   <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Albania Europe     2002    75.7 3508512     4604.          908.
## 2 Albania Europe     2007    76.4 3600523     5937.          917.
```


```r
filter(gapminder2, lifeExp > 80)
```

#### Promenite redosled redova: <span style="color:red">`arrange()`</span>
Ukoliko želite da promenite redosled redova data okvira, **d**ata **f**rame (df), prema jednoj od varijabli/kolona.

<img src="images/arrange().png" width="300px" />

- Ukoliko prosledite funkciji `arrange()` slovnu varijablu, **R** će promeniti redove vrednosti u varijablama poređane po alfabetu. 

- Ukoliko, pak, prosledite faktorsku varijablu, **R** će promeniti redove po redu nivoa u vašem faktoru (kada se upotrebi funkcija `levels()` na varijabli taj redosled će se obrnuti).

##### 👉 Vežbajte ⏰💻: ArUredite vaše podatke 
1) Poređajte države u podacima `gapmEU21c` `df` po očekivanom životnom veku u rastuće i padajućem redu.

2) Upotrebom `gapminder df`
  - Pronađite zapise sa najmanjom populacijom
  
  - Pronađite zapise sa najvećim očekivanim životnim vekom.

##### 😃🙌 Rešenje 1):

```r
gapmEU21c_h2l <- arrange(gapmEU21c, lifeExp)
head(gapmEU21c_h2l, 2)
```

```
## # A tibble: 2 x 7
##   country continent  year lifeExp      pop gdpPercap LifeExp_month
##   <fct>   <fct>     <int>   <dbl>    <int>     <dbl>         <dbl>
## 1 Turkey  Europe     2002    70.8 67308928     6508.          850.
## 2 Romania Europe     2002    71.3 22404337     7885.          856.
```

```r
gapmEU21c_l2h <- arrange(gapmEU21c, desc(lifeExp)) # note the use of desc()
head(gapmEU21c_l2h, 2)
```

```
## # A tibble: 2 x 7
##   country     continent  year lifeExp     pop gdpPercap LifeExp_month
##   <fct>       <fct>     <int>   <dbl>   <int>     <dbl>         <dbl>
## 1 Iceland     Europe     2007    81.8  301931    36181.          981.
## 2 Switzerland Europe     2007    81.7 7554661    37506.          980.
```

##### 😃🙌 Rešenje 2):

```r
arrange(gapminder, pop)
```

```
## # A tibble: 1,704 x 6
##    country               continent  year lifeExp   pop gdpPercap
##    <fct>                 <fct>     <int>   <dbl> <int>     <dbl>
##  1 Sao Tome and Principe Africa     1952    46.5 60011      880.
##  2 Sao Tome and Principe Africa     1957    48.9 61325      861.
##  3 Djibouti              Africa     1952    34.8 63149     2670.
##  4 Sao Tome and Principe Africa     1962    51.9 65345     1072.
##  5 Sao Tome and Principe Africa     1967    54.4 70787     1385.
##  6 Djibouti              Africa     1957    37.3 71851     2865.
##  7 Sao Tome and Principe Africa     1972    56.5 76595     1533.
##  8 Sao Tome and Principe Africa     1977    58.6 86796     1738.
##  9 Djibouti              Africa     1962    39.7 89898     3021.
## 10 Sao Tome and Principe Africa     1982    60.4 98593     1890.
## # … with 1,694 more rows
```


```r
arrange(gapminder, desc(lifeExp))
```

```
## # A tibble: 1,704 x 6
##    country          continent  year lifeExp       pop gdpPercap
##    <fct>            <fct>     <int>   <dbl>     <int>     <dbl>
##  1 Japan            Asia       2007    82.6 127467972    31656.
##  2 Hong Kong, China Asia       2007    82.2   6980412    39725.
##  3 Japan            Asia       2002    82   127065841    28605.
##  4 Iceland          Europe     2007    81.8    301931    36181.
##  5 Switzerland      Europe     2007    81.7   7554661    37506.
##  6 Hong Kong, China Asia       2002    81.5   6762476    30209.
##  7 Australia        Oceania    2007    81.2  20434176    34435.
##  8 Spain            Europe     2007    80.9  40448191    28821.
##  9 Sweden           Europe     2007    80.9   9031088    33860.
## 10 Israel           Asia       2007    80.7   6426679    25523.
## # … with 1,694 more rows
```

#### Sažmite više vrednosti u jednu sumu: <span style="color:red">`summarise()`</span>

<img src="images/summarise().png" width="450px" />

Sintaksa summarise() jednostavna je i sastoji se od  više glagola koji su uključeni u `dplyr` paket.

- koristi istu sintaksu kao i `mutate()`, ali se rezultat prikazaju u pojedinačnom redu, umesto u novoj koloni što je slučaj kod upotrebe `mutate()`. 

- gradi novi skup podataka koji sadrži samo zbirne statistike.

| Objective | Function                | Description                    |
| --------- | ----------------------- | ------------------------------ |
| basic     | `sum(x)`                | Sum of vector x                |
| centre    | `mean(x)`               | Mean (average) of vector x     |
|           | `median(x)`             | Median of vector x             | 
| spread    | `sd(x)`                 | Standard deviation of vector x |
|           | `quantile(x, probs)`    | Quantile of vector x           |
|           | `range(x)`              | Range of vector x              |
|           | `diff(range(x)))`       | Width of the range of vector x |
|           | `min(x)`                | Min of vector x                |
|           | `max(x)`                | Max of vector x                |
|           | `abs(x)`                | Absolute value of a number x   | 

##### 👉 Vežbajte ⏰💻: Use `summarise()`:

1) odštampajte sažetak podataka u tabeli gapminder koji se odnose na dve varijable: max_lifeExp and max_gdpPercap.

2) odštampajte sažetak podataka gapminder koji sadrži dve varijable: mean_lifeExp and mean_gdpPercap.

##### 😃🙌 Sažetak vaših podataka 


```r
summarise(gapminder, max_lifeExp = max(lifeExp), max_gdpPercap = max(gdpPercap))
```

```
## # A tibble: 1 x 2
##   max_lifeExp max_gdpPercap
##         <dbl>         <dbl>
## 1        82.6       113523.
```


```r
summarise(gapminder, mean_lifeExp = mean(lifeExp), mean_gdpPercap = mean(gdpPercap))
```

```
## # A tibble: 1 x 2
##   mean_lifeExp mean_gdpPercap
##          <dbl>          <dbl>
## 1         59.5          7215.
```

#### Podgrupisanje: <span style="color:red">`group_by()`</span>

Funkcija dplyr's `group_by()` omogućuje vam da grupišete vaše podatke. Omogućuje vam da kreirate poseban df koji će odvojiti orginali df po varijablama.

Funkcija `summarise()` može se kombinovati sa `group_by()`.

| Objective | Function                | Description                               |
| --------- | ----------------------- | ----------------------------------------- |
| Position	| first()	                | First observation of the group            |
|           | last()	                | Last observation of the group             |
|           | nth()	                  | n-th observation of the group             |
| Count	    | n()	                    | Count the number of rows                  |
|           | n_distinct()	          | Count the number of distinct observations |


##### 👉 Vežbajte ⏰💻: SuGrupišite vaše podatke

1) Identifikujte koliko je država dato u  gapminder-u za svaki kontinent.

##### 😃🙌 SRešenje 


```r
gapminder %>%
     group_by(continent) %>%
     summarise(n_distinct(country))
```

```
## # A tibble: 5 x 2
##   continent `n_distinct(country)`
##   <fct>                     <int>
## 1 Africa                       52
## 2 Americas                     25
## 3 Asia                         33
## 4 Europe                       30
## 5 Oceania                       2
```

#### Povežimo sa `%>%` sve gore!

Naučite da koristite skraćenicu (shortcut) za pipe operator (operator cevi) 
<img src="images/pipe_short_cut.png" width="450px" style="display: block; margin: auto;" />

##### 🗣👥 Pregovarajte sa komšijama: 
Kakvu relaciju očekujete da nađete između broja stanovnika (`pop`) i očekivanog životnog veka (`lifeExp`)?

**Pogledajte šta će vam proizvesti sledeći kod**


```r
gapminder_pipe <- gapminder %>%
  filter(continent == "Europe" & year ==  2007) %>%
  mutate(pop_e6 = pop / 1000000)
plot(gapminder_pipe$pop_e6, gapminder_pipe$lifeExp, cex = 0.5, col = "red")
```

<img src="/day2/DataWrangling/_index.en_files/figure-html/unnamed-chunk-24-1.png" width="576" style="display: block; margin: auto;" />

#### `tidyr`

Paket `tidyr` može vam pomoći da kreirate uredne podatke **tidy data**. Uredni podaci su podaci u kojima:

- Svaka **kolona** je **varijabla**
- Svaki **red** je **observacija**
- Svaka **ćelija** je **pojedinačna vrednost**

<img src="images/tidyr.png" width="450px" />

Paket `tidyr` package obuhvata principe uređenih podataka **principles of tidy data** i obezbeđuje vam standardne ključne funkcionalnosti da organizujete vrednosti podataka u setu podataka.

[Hadley Wickham](http://hadley.nz/) autor diskutuje o `tidyr` paketu u svom tekstu [Tidy Data](https://vita.had.co.nz/papers/tidy-data.pdf) i važnosti procesa pročišćavanja podataka i njihovog strukturisanja za dalju analize.

Pravi skupovi podataka iz kojih vam se budu svideli sa sajta <https://data.gov.rs/> ili bilo kojeg otvorenog izvora podataka na drugim platformama, često neće biti uređeni po principima uređenih podataka i te razlike mogu biti različite:

- Varijable mogu da nemaju svoja imena a umesto zaglavalja kolona da imate vrednosti.
-	Veći broj varijabli mogu biti sačuvani u jednoj koloni
-	Pojedinačna varijabla može biti sačuvana u nekoliko kolona 
-	Iste informacije su snimljene više puta kao različite varijable
 
samo da navedemo neke.

Da bismo ovo ilustrovali otidite na portal <https://data.gov.rs/> i potražite [Kvalitet Vazduha 2017](https://data.gov.rs/sr/datasets/kvalitet-vazduha-2017/). Pre svega, uzećemo sledeće podatke [2017-NO2.csv](http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-becc-6b6e31a24d80/download/2017-no2.csv).


```r
## If you don't have tidyr installed yet, uncomment and run the line below
#install.packeges("tidyr")
library(tidyr)
# access 2017-NO2.csv data
no2 <- read.csv("http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-becc-6b6e31a24d80/download/2017-no2.csv",
                stringsAsFactors = FALSE, 
                fileEncoding = "latin1")
# have a look at the data
glimpse(no2)
```

```
## Observations: 365
## Variables: 8
## $ Datum                   <chr> "01.01.2017", "02.01.2017", "03.01.2017"…
## $ Novi.Sad.SPENS.NO2      <dbl> 22.89, 32.94, 14.86, 22.73, 20.89, 10.47…
## $ Beograd.Mostar.NO2      <dbl> 28.83, 39.12, 25.20, 28.48, 27.82, 41.91…
## $ Beograd.Vraèar.NO2      <dbl> 182.84, 244.56, 147.49, 159.12, 124.16, …
## $ Beograd.Zeleno.brdo.NO2 <dbl> 36.32, 36.68, 27.00, 35.15, 24.92, 8.27,…
## $ Kragujevac..NO2         <dbl> 38.92, 43.50, 40.17, 45.44, 43.04, 34.55…
## $ U.ice..NO2              <dbl> 49.84, 50.34, 36.35, 49.07, 33.33, 39.88…
## $ Ni..IZJZ.Ni...NO2       <dbl> 18.61, 22.87, 15.68, 21.97, 21.68, 12.11…
```

Podaci nam govore da tabela ima `365` observacija i `8` varijabli. Bezobzira, treba da razmotrimo koje tipove infomacija mi ovde imamo:

- `date` NO2 vreme u kom su merenja izvršena: data su u jedinstvenoj koloni -> ✅ čisto (tidy) 
- `places` mesta na kojima je NO2 meren: data su u nekoliko kolona -> ❎ čisto (tidy)🙁
- `NO2` merenja: data su u nekoliko kolona -> ❎ čisto (tidy)🙁

Hmmm… 🤔 Da li nam ovo izgleda čisto (tidy) 😳

Ovi podaci odnose se na merenje nivoa NO2(µg/m3) u nekoliko različitih gradova/mesta, što znači da je naša glavna odzivna varijabla NO2. Način na koji je ona prikazana u ovu podacima sigurno nije čist (tidy). Ne oslikavaju principe uređenih podataka: **svaka kolona je varijabla** je i dalje, **svaki red <span style="color:orangered">NIJE</span> opservacija**.

Ispostavlja se da ovi podaci sadrže 8 varijabli, a misli shvatili da ih je samo `3`: `date`, `place` i `no2`. Da bi ih uredili, neophodno je da ih složimo pretvarajući kolone u redove. Zadovoljni smo sa varijablom  `date` i ona treba da ostane u pojedinačnoj koloni, međutim drugih 7 kolona treba da prebacimo u dve varijable: `place` and `no2`.

Da pretvorimo podatke širokog formata u visoki format neophodno je da pretvorimo kolone u redove upotrebom funkcije `gather()`.

<img src="images/gather.png" width="450px" />

Kreiraćemo varijablu `place` u kojoj ćemo sakupiti sva zaglavlja data u kolonama 2:8. Vrednosti unutar tih kolona biće snimljene u novu varijablu `no2`.


```r
new_no2 <- no2 %>%
  gather("place", "no2", -Datum, factor_key = TRUE) # stack all columns apart from `Datum`
glimpse(new_no2)
```

```
## Observations: 2,555
## Variables: 3
## $ Datum <chr> "01.01.2017", "02.01.2017", "03.01.2017", "04.01.2017", "0…
## $ place <fct> Novi.Sad.SPENS.NO2, Novi.Sad.SPENS.NO2, Novi.Sad.SPENS.NO2…
## $ no2   <dbl> 22.89, 32.94, 14.86, 22.73, 20.89, 10.47, 9.58, 15.99, 14.…
```

Da vidimo imena mesta


```r
new_no2 %>%
     group_by(place) %>%
     summarise(n())
```

```
## # A tibble: 7 x 2
##   place                   `n()`
##   <fct>                   <int>
## 1 Novi.Sad.SPENS.NO2        365
## 2 Beograd.Mostar.NO2        365
## 3 Beograd.Vraèar.NO2        365
## 4 Beograd.Zeleno.brdo.NO2   365
## 5 Kragujevac..NO2           365
## 6 U.ice..NO2                365
## 7 Ni..IZJZ.Ni...NO2         365
```

Ta imena izgledaju vrlo neuredno. Mogli bismo koristiti funkciju iz [`stringr`](https://stringr.tidyverse.org) paketa `str_sub()`. Za početak uklonimo <span style="color:orangered">.NO2</span> na kraju svakog imena.


```r
## If you don't have stringr installed yet, uncomment and run the line below
#install.packeges("stringr")
library(stringr)
new_no2$place <- new_no2$place %>% 
    str_sub(end = -5)
glimpse(new_no2)
```

```
## Observations: 2,555
## Variables: 3
## $ Datum <chr> "01.01.2017", "02.01.2017", "03.01.2017", "04.01.2017", "0…
## $ place <chr> "Novi.Sad.SPENS", "Novi.Sad.SPENS", "Novi.Sad.SPENS", "Nov…
## $ no2   <dbl> 22.89, 32.94, 14.86, 22.73, 20.89, 10.47, 9.58, 15.99, 14.…
```

```r
new_no2 %>%
    group_by(place) %>%
    summarise(n())
```

```
## # A tibble: 7 x 2
##   place               `n()`
##   <chr>               <int>
## 1 Beograd.Mostar        365
## 2 Beograd.Vraèar        365
## 3 Beograd.Zeleno.brdo   365
## 4 Kragujevac.           365
## 5 Ni..IZJZ.Ni..         365
## 6 Novi.Sad.SPENS        365
## 7 U.ice.                365
```

I dalje ne izgleda kako treba. 😟 Ovo bi mogao biti naporan posao. 😥 Nije čudo zašto se mnogi analitičari žale oko vremena utrošenog na proces čišćenja i pripreme podataka. To bi mogao biti veoma dug i dugotrajan proces, ali što više radite i više iskustva dobijate sve je lakše i manje bolno.


Možda, možete pokušati da istražite i druge pakete R koji će vam pomoći u organizaciji podataka da biste dobili idealan format. Pokazaćemo vam kako se to lako možete učiniti upotrebom funkcije `forcats::fct_recode()` function.


```r
## If you don't have forcats installed yet, uncomment and run the line below
#install.packages("forcats")
library(forcats)
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
glimpse(new_no2)
```

```
## Observations: 2,555
## Variables: 3
## $ Datum <chr> "01.01.2017", "02.01.2017", "03.01.2017", "04.01.2017", "0…
## $ place <fct> NS_Spens, NS_Spens, NS_Spens, NS_Spens, NS_Spens, NS_Spens…
## $ no2   <dbl> 22.89, 32.94, 14.86, 22.73, 20.89, 10.47, 9.58, 15.99, 14.…
```

{{% notice note %}}
Do sad ste trebali steći dovoljno znanja o upotrebi R-a da imate potrebno samopouzdanje da započnete sa istraživanjem ostalih funkcija paketa [`tidyr`](https://tidyr.tidyverse.org/) Ne treba se tu zaustaviti, već otići dalje i istražiti celu kolekciju [`tidyverse`](https://www.tidyverse.org/) R paketa. 😇🎶
{{% /notice %}}

Da biste saznali više o urednim podacima (tidy data) u R-u proverite glavu [Data Tidying](https://garrettgman.ithuthe b.io/tidying/) čuvene knjige [Data Science with R](https://garrettgman.github.io) autora [Garrett Grolemund](https://resources.rstudio.com/authors/garrett-grolemund)

{{% notice tip %}}
Da li ste pokušali učiniti nauku o podacima iz odgovora na pitanja i diskusiju sa drugima iz R zajednice? 👥💻📊📈🗣 [RStudio Community](https://community.rstudio.com)
{{% /notice %}}

## ZADACI 👇

Provežbajte sledeći set vežbi:

1) Instalirajte i proverite da li je to poslednja verzija paketa `rattle` i pogledajte šta nam on donosi.

2) Kreirajte novi R script fajl da istražite set podataka `weatherAUS`. 

  i) `select()` varijable: `MinTemp`, `MaxTemp`, `Rainfall` i `Sunshine` *povezivanjem u cevi* set podataka u ``dplyr::select() funkciju.
  
  ii) proizvedite *rezime*  upotrebom `base::summary()` funkcije ovih numeričkih vrednosti.
  
  iii) u okviru ove selekcije filtrirajte samo one opservacije u kojima je `Rainfall >= 1` i snimite rezultate u memoriju kompjutera (tj. snimite rezultate u objektu).
  
  iv) Promislite kako biste još mogli da upotrebljavate i druge `dplyr` glagole da istražite `weatherAUS` set podataka. Zapišite sebi pitanja na početku, pa onda krenite sa unosom koda.
  
  v) Napišite kratak izveštaj koja bi vizuelizacija bila zanimljiva za set podataka `weatherAUS` i zašto?

##### Korisni linkovi

[Data Wrangling cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)

[Data Transformation with dplyr cheat sheet](https://4.files.edl.io/b9e2/07/12/19/142839-a23788fb-1d3a-4665-9dc4-33bfd442c296.pdf)

-----------------------------
© 2019 Tatjana Kecojevic

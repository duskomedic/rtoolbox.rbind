---
date: "2016-04-09T16:50:16+02:00"
title: Vizuelizacija podataka
output: 
  learnr::tutorial
weight: 2
---

Većina vas, ako ne svi, upoznati su sa kreiranjem grafikona u Excelu. Softver poput Excel-a ima predefinisan set opcija za iscrtavanje podataka. Ove opcije date u meniju pretpostavljaju da su podaci već pripremljeni za iscrtavanje, što u slučaju sirovih podataka nije slučaj. Biće neophodno da ovakve podatke morate organizovati i promeniti svoje podatke kako biste bili spremni za efikasnu vizulezaciju. 

### Gramatika grafike

Gramatika grafike [grammar of graphics](http://vita.had.co.nz/papers/layered-grammar.html) omogućava strukturirani način kreiranja grafikona dodavanjem komponenti kao slojeva, i čini grafikone efikasnijim i atraktivnijim. 

Ona vam omogućava da odredite blokove grafikona i da ih kombinujete kako biste stvorili prikaz koji želite. Postoji osam tipova ovih blokova:

- podaci (data)

- estetsko mapiranje (aesthetic mapping)

- geometrijski objekti (geometric object)

- stastičke transformacije (statistical transformations)

- skale (scales)

- koorinatni sistem (coordinate system)

- podešavanje položaja (position adjustments)

- oblaganje (faceting)

Zamislite da razgovarate o pečenju torte i dodavanju višnje na njen vrh. 🎂🍒 TOva filozofija ugrađena je u [`ggplot`](https://ggplot2.tidyverse.org/reference/) paket koji je razvio [Hadle Wickham](http://hadley.nz) za kreiranje elegantnih i kompleksnih grafikona u R-u.


#### ggplot2

Učeči kako da koristite `ggplot2` paket može biti izazov, ali su rezultati veoma korisni i kao i u R-u, biće vam lakše da ga koristite što više to budete radili.

{{% notice warning %}}
Za razliku od osnovne grafike ggplot radi sa okvirima podataka (dataframes), a ne sa pojedinačnim vektorima.
{{% /notice %}}

Najbolji način da usvojite znanje je da vežbate. Zato napravimo prvi `ggplot`. 😃
Ono što trebamo da učinimo je sledeće:

- i) Podatke rasporedite u format pogodan za vizuelizaciju.

- ii) “Pokrenite” grafikon sa `ggplot()`:
  
**ggplot(<span style="color:blue">dataframe</span>, aes(<span style="color:orangered">x = explanatory variable</span>, <span style="color:green">y = resposne variable</span>))**

Ovom naredbom iscrtaće se prazan grafikon (ggplot), iako su zadani x i y `ggplot` još vam neće iscrtati grafikon, s obzirom da još niste specifikovali set podataka već samo varijable koje ćete koristiti. Primetite ovde da funkcija `aes( )` koristi se za specifikaciju x i y osa. 
  
- iii) Dodajte lejere sa funkcijom `geom_`:

**geom_point()**

 Tačke na grafikonu dodaćemo upotrebom **geom lajera** pozivom `geom_point`.


```r
# load the packages
suppressPackageStartupMessages(library(dplyr))
suppressPackageStartupMessages(library(gapminder))
suppressPackageStartupMessages(library(ggplot2))

# wrangle the data (Can you remember what this code do?)
gapminder_pipe <- gapminder %>%
  filter(continent == "Europe" & year ==  2007) %>%
  mutate(pop_e6 = pop / 1000000)

# plot the data
ggplot(gapminder_pipe, aes(x = pop_e6, y = lifeExp)) +
  geom_point(col ="red")
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-1-1.png" width="768" style="display: block; margin: auto;" />

{{% notice tip %}}
🤓💡 **Tip**: Za izradu grafova možete koristiti sledeći obrazac koda **ggplot2**:
{{% /notice %}}

```
ggplot(data = <DATA>, (mapping = aes(<MAPPINGS>)) + 
      <GEOM_FUNCTION>()
```

##### <span style="color:red">ggplot()</span> galerija
Pokrenite sledeći kod da biste videli koje će grafove proizvesti.


```r
ggplot(data = gapminder, mapping = aes(x = lifeExp), binwidth = 10) +
  geom_histogram()
#
ggplot(data = gapminder, mapping = aes(x = lifeExp)) +
  geom_density()
#
ggplot(data = gapminder, mapping = aes(x = continent, color = continent)) +
  geom_bar()
#
ggplot(data = gapminder, mapping = aes(x = continent, fill = continent)) +
  geom_bar()
```

##### 🗣👥 Pregovarajte sa komšijama: 
Da li životni vek zavisi od broja stanovnika?

`y = b_0 + b_1 x + e`

Startujte ovaj kod u konzoli da biste uporedili `pop` sa `lifeExp`.

Obratite pažnju na reči, velika i mala slova, i na zagrade!

```r
m1 <- lm(gapminder_pipe$lifeExp ~ gapminder_pipe$pop_e6)
summary(m1)
```

**Možete li odgovoriti na pitanje koristeći izlaz napravljenog modela?**

```r
m1 <- lm(gapminder_pipe$lifeExp ~ gapminder_pipe$pop_e6)
summary(m1)
```

```
## 
## Call:
## lm(formula = gapminder_pipe$lifeExp ~ gapminder_pipe$pop_e6)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -6.324 -2.562  1.007  2.245  4.277 
## 
## Coefficients:
##                        Estimate Std. Error t value Pr(>|t|)    
## (Intercept)           77.477421   0.721723 107.351   <2e-16 ***
## gapminder_pipe$pop_e6  0.008762   0.023779   0.368    0.715    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.025 on 28 degrees of freedom
## Multiple R-squared:  0.004826,	Adjusted R-squared:  -0.03072 
## F-statistic: 0.1358 on 1 and 28 DF,  p-value: 0.7153
```

##### 👉 Vežbajte ⏰💻: UsKoristite  gagapminder  podatke

Da li životni vek zavisi od bruto nacionalnog dohotka po glavi stanovnika?

1) Bacite pogled na podatke. (tip: `sample_n(df, n)`)

2) Napravite tačkasti grafikon: šta vam on govori?

3) Napravite regresionu analizu: da li tu postoji relacija? Koliko je jaka? Da li je relacija linearna? Šta možemo zaključiti iz grafikona?

4) Koja se još pitanja otvaraju; možete li dati odgovor na njih?

##### 😃🙌 SRešenje: kod Q1; primer

```r
sample_n(gapminder, 30)
```

```
## # A tibble: 30 x 6
##    country      continent  year lifeExp      pop gdpPercap
##    <fct>        <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Iraq         Asia       1987    65.0 16543189    11644.
##  2 Myanmar      Asia       1962    45.1 23634436      388 
##  3 Italy        Europe     1957    67.8 49182000     6249.
##  4 Netherlands  Europe     2007    79.8 16570613    36798.
##  5 Djibouti     Africa     1972    44.4   178848     3694.
##  6 Iraq         Asia       1992    59.5 17861905     3746.
##  7 South Africa Africa     1997    60.2 42835005     7479.
##  8 El Salvador  Americas   1967    55.9  3232927     4359.
##  9 Burkina Faso Africa     1957    34.9  4713416      617.
## 10 Korea, Rep.  Asia       2002    77.0 47969150    19234.
## # … with 20 more rows
```

Dodaćemo lejere na ovaj tačkasti grafikon: uporedićemo: `liveExp` sa `gdpPercap`. Iscrtaćemo regresionu linuju koja će nam pomoći da vidimo relaciju ove dve varijable, ali i neparemtričku lusovu linuju (loess line) koja će prikazati moguću relaciju između ove dve varijable. Što znači da ćemo imati:

- Prvi lejer: tačkasti grafikon **scatterplot**
- Drugi lejer: regresionu liniju koja najpribližnije odgovara podacima **line of the best fit**
- Treći lejer: lusovu krivu (**loess curve**)


##### 😃🙌 SRešenje: kod Q2; Iscrtava podatke

```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.2, shape = 21, fill = "blue", colour="black", size = 5) + # set transparency, shape, colour and size for points
  geom_smooth(method = "lm", se = F, col = "maroon3") + # change the colour of line
  geom_smooth(method = "loess", se = F, col = "limegreen") # change the colour of line
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-6-1.png" width="768" style="display: block; margin: auto;" />

##### 😃🙌 Rešenje: kod Q3; jednostavni regresioni model

```r
my.model <- lm(gapminder_pipe$lifeExp ~ gapminder_pipe$gdpPercap)
summary(my.model)
```

```
## 
## Call:
## lm(formula = gapminder_pipe$lifeExp ~ gapminder_pipe$gdpPercap)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -2.79839 -1.30472  0.00807  1.33443  2.87766 
## 
## Coefficients:
##                           Estimate Std. Error t value Pr(>|t|)    
## (Intercept)              7.227e+01  6.942e-01 104.113  < 2e-16 ***
## gapminder_pipe$gdpPercap 2.146e-04  2.514e-05   8.537  2.8e-09 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.598 on 28 degrees of freedom
## Multiple R-squared:  0.7225,	Adjusted R-squared:  0.7125 
## F-statistic: 72.88 on 1 and 28 DF,  p-value: 2.795e-09
```

### Koristite estetsko mapiranje: dodajte još lejera na vaš <span style="color:red">`ggplot()`</span>

Kad god je to moguće treba da se trudite da vaš grafikon bude vizuelno privlačan i informativan, kao što je rečeno u prethodnom odeljku *Principi vizuelizacije*. 

#### Da biste promenili naziv grafikona ili oznake osa koristite <span style="color:orangered">lejer **labs**</span>

**labs(<span style="color:blue">title =</span> <span style="color:orangered"> “your title”</span>, <span style="color:blue">subtitle =</span> <span style="color:orangered"> “your subtitle”</span>, <span style="color:blue">y =</span> <span style="color:orangered"> “y label”</span>, <span style="color:blue">x =</span> <span style="color:orangered"> “x label”</span>, <span style="color:blue">caption =</span> <span style="color:orangered"> “graph's caption”</span>)** 
 


```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.2, shape = 20, col = "steelblue", size = 5) + 
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "limegreen") + 
 
  # give a title an label axes
  labs(title = "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  
  # modify the appearance
  theme(legend.position = "none", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  
  # add the description
  geom_text(x = 80000, y = 125, label = "regression line", col = "maroon3") +
  geom_text(x = 90000, y = 75, label = "smooth line", col = "limegreen") 
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-8-1.png" width="768" style="display: block; margin: auto;" />

Primetite da smo dodali tekst na grafikon koji označava dve linije i da smo uredili grafikon tako da se legenda ne prikazuje.

Takođe, mogli smo da dobijemo ovaj tekst na grafikonu i sledećom naredbom:
```
annotate("text", x = 80000, y = 125 label = "regression line", color = "maroon3")
```

Da biste saznali više o izmeni teme grafikona pogledajte sledeću internet stranicu [ggplot’s theme page](https://ggplot2.tidyverse.org/reference/theme.html).

#### Promenite boju tačaka tako da odražavaju treću promenljivu.


```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  
  # change the colour of the points to reflect continent it belongs to; set transparency, shape, and size for points
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "dodgerblue3") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 80000, y = 125, label = "regression line", col = "maroon3") + 
  geom_text(x = 90000, y = 75, label = "smooth line", col = "dodgerblue3")
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-9-1.png" width="768" style="display: block; margin: auto;" />

{{% notice note %}}
Imajte na umu da se legenda dodaje automatski. Možete je ukloniti tako što ćete postaviti atribut `none` na **legend.position** unutar funkcije `theme()`.
{{% /notice %}}


#### Podesite ograničenja X i Y osa i promenite tekst X ose i njegovu lokaciju


```r
  ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "dodgerblue3") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 48000, y = 90, label = "regression line", col = "maroon3") + 
  geom_text(x = 70000, y = 75, label = "smooth line", col = "dodgerblue3") +
  
  # change the limits of the x & y axis
  xlim(c(0, 90000)) + 
  ylim(c(25, 100)) 
```

```
## Warning: Removed 5 rows containing non-finite values (stat_smooth).

## Warning: Removed 5 rows containing non-finite values (stat_smooth).
```

```
## Warning: Removed 5 rows containing missing values (geom_point).
```

```
## Warning: Removed 33 rows containing missing values (geom_smooth).
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-10-1.png" width="768" style="display: block; margin: auto;" />
  
Primetite da regresiona linija i kriva su promenile svoje oblik 😳… Šta se desilo?! 😲
  
{{% notice warning %}}
Kada koristite xlim() i ylim(), tačke izvan navedenog raspona se brišu i ne uzimaju se u obzir pri crtanju krive upotrebom `geom_smooth()`. Ova osobina vam može biti pri ruci kada želite da saznate da li bi se korelaciona linije promenila ako bi se uklonile ekstremne vrednosti iz podataka.
{{% /notice %}}
  
Srećom, postoji još jedan način da promenite granice na osama a da se ne brišu tačke izvan prikaza, to možete uraditi zumirajući region koji vam je zanimljiv. Ovo možete uraditi upotrebom funkcije `coord_cartesian()`. Probajte da zamenite komande `xlim()` and `ylim()` iz prethodnog koda sa kodom koji je prikazan dole da vidite šta bi se desilo.

```
coord_cartesian(xlim = c(0, 90000), ylim = c(25, 100))  # zooming in specified limits of the x & y axis
```

Pauze možete postaviti na x osi i obeležiti ih upotrebom `scale_x_continuous()`. Slično, možete to uraditi i na y osi? 

Pokušajte da se igrate promenom palete boja. Za dodatne opcije proverite [Sequential, diverging and qualitative colour scales from colorbrewer.org](https://ggplot2.tidyverse.org/reference/scale_brewer.html).

Ovo su ugrađene teme koje kontrolišu sve prikaze ne-podataka. Treba da koristite `theme_bw()` da biste imali belu pozadinu ili `theme_dark()` za tamno sivu. Za više o temama pogledajte [ovde](https://ggplot2.tidyverse.org/reference/ggtheme.html).



```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "maroon3") + 
  geom_smooth(method = "loess", se = F, col = "dodgerblue3") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 80000, y = 125, label = "regression line", col = "maroon3") + 
  geom_text(x = 90000, y = 75, label = "smooth line", col = "dodgerblue3") +
  
  # change breaks and label them 
  scale_x_continuous(breaks = seq(0, 120000, 20000), labels = c("0", "20K", "40K", "60K", "80K", "10K", "12K")) +

  # change color palette
  scale_colour_brewer(palette = "Set1") + 

  # white background theme
  theme_bw()
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-11-1.png" width="768" style="display: block; margin: auto;" />

Postoji biblioteka `ggthemes` koja će vam pomoći da napravite elegantne grafikone koje koriste mediji kao što su Wall Street Journal ili Economist. Pogledajte koje još teme možete koristiti na sledećoj  [veb stranici]( https://yutannihilation.github.io/allYourFigureAreBelongToUs/ggthemes/)


```r
## If you don't have ggthemes installed yet, uncomment and run the line below
#install.packeges("ggthemes")
library(ggthemes)
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "darkred") + 
  geom_smooth(method = "loess", se = F, col = "darkgreen") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  geom_text(x = 80000, y = 125, label = "regression line", col = "darkred") + 
  geom_text(x = 90000, y = 75, label = "smooth line", col = "darkgreen") +
  scale_x_continuous(breaks = seq(0, 120000, 20000), labels = c("0", "20K", "40K", "60K", "80K", "10K", "12K")) +

  # Wall Street Journal theme
  scale_colour_wsj() +
  theme_wsj()
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-12-1.png" width="768" style="display: block; margin: auto;" />

Spremni ste da napravite vizualizacije u R-u spremne za publikovanje. 😎 Možete istraživati i dalje i pokušati da proizvede grafikone u stilu BBC-ja. Proverite kako BBC uređuje svoje tekstove zasnovane na podacima [BBC Visual and Data Journalism cookbook for R graphics]( https://bbc.github.io/rcookbook/).

##### Položite panele na mrežu 

Ponekad je teško sve važno na prikazu jednog panela, poput ovog kojeg smo kreirali a u kojem nije jasno koja je koja tačka za svaki od kontinenata. Da biste lakše sagledali i razumeli informacije koje želite da prikažete, nekad je efikasnije ih predstaviti različite kategorije podeljene u više panela. Ovo je jednostavno da se uradi aplikacijom moćnim funkcijama `ggplot2`: `facet_wrap()` and `facet_grid()`.
  

```r
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(aes(col = continent), alpha = 0.5, shape = 20, size = 3) + 
  geom_smooth(method = "lm", se = F, col = "darkred") + 
  geom_smooth(method = "loess", se = F, col = "black") + 
  labs (title= "Life Exp. vs. Population Size", 
        x = "population", y = "Life Exp.") + 
  theme(legend.position = "right", 
        panel.border = element_rect(fill = NA, 
                                    colour = "black",
                                    size = .75),
        plot.title=element_text(hjust=0.5)) + 
  scale_x_continuous(breaks = seq(0, 120000, 20000), labels = c("0", "20K", "40K", "60K", "80K", "10K", "12K")) +
  scale_colour_wsj() +
  theme_wsj() +
  
  # forms a matrix of scatterplots for each continet
  facet_grid(rows = vars(continent))
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-13-1.png" width="768" style="display: block; margin: auto;" />
 
Glavna distinkcija funkcija `facet_wrap()` i  `facet_grid()` je da prva može da spoji ggplots u različite kategorije pojedinačne varijable, dok druga može to da uradi na više od jedne varijable.

{{% notice warning %}}
Pokušajte da istražite dve funckije sami i vidite kuda će vas to odvesti.
{{% /notice %}}
 
#### 💪 Pokušajte sledeće: 

- `dplyr`-ova `group_by()` funkcija omogućava vam da grupišete svoje podatke. Dozvoljava vam da kreirate posebne df koje dele orginalnu df po varijabli.

- `boxplot()` funkcija proizvodi boxplot grafike od datih (gropiranih) vrednosti.

Znajući funkcije `group_by()` i `boxplot()` i korišćenjem `gapminder` podataka, možete li izračunati srednju (medijanu) očekivanog životnog veka u 2007. godini po kontinentima i da vizuelizujete vaše podatke?

##### 😃🙌 Rešenje: kod

Pogledajmo srednji (medijanu) očekivanog životnog veka za svaki kontinent

```r
gapminder %>%
    group_by(continent) %>%
    summarise(lifeExp = median(lifeExp))
```

```
## # A tibble: 5 x 2
##   continent lifeExp
##   <fct>       <dbl>
## 1 Africa       47.8
## 2 Americas     67.0
## 3 Asia         61.8
## 4 Europe       72.2
## 5 Oceania      73.7
```

**Sretni smo što živimo u Srbiji, tj. u Evropi!!!** 😅

##### 😃🙌 Rešenje: grafikon

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-15-1.png" width="768" style="display: block; margin: auto;" />
##### Studija slučaja: NO2 2017 😁

Pokušajmmo sad da kombinujemo sve što smo do sada naučili i vežbali na nama dobro poznatim podacima [2017-NO2.csv](http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-becc-6b6e31a24d80/download/2017-no2.csv) data. 

Zapamtite ovo?

```r
library(tidyr)
library(forcats)
no2 <- read.csv("http://data.sepa.gov.rs/dataset/ca463c44-fbfa-4de9-9a75-790995bf2830/resource/74516688-5fb5-47b2-becc-6b6e31a24d80/download/2017-no2.csv",
                stringsAsFactors = FALSE, 
                fileEncoding = "latin1")
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


```r
new_no2 %>% 
  group_by(place) %>% 
  summarise(mean_no2 = mean(!is.na(no2))) %>% # !is.na(): is not NA; omits the missing values
  ggplot(aes(x = place, y = mean_no2, fill = place)) + # fill: colours each bar differently   
    geom_bar(stat = "identity") +
    xlab("Place") + 
    scale_fill_brewer(palette = "Dark2") + # colour scheme "Dark2"
    theme(legend.position="bottom", 
          axis.text.x = element_blank(),
          axis.ticks.x = element_blank()) # 
```

<img src="/day2/Visualisation/_index.en_files/figure-html/unnamed-chunk-17-1.png" width="672" />

## ZADACI 👇

Provežbajte sledeći set vežbi:

1) Odaberite vam zanimljive podatke sa portala otvorenih podataka <https://data.gov.rs> Uvezite set podataka u R i pregledajte koje sve varijable tu imate. Promislite kakve grafikone bi trebalo da koristete da biste te podatke prikazali vašoj publici?

2) Vratite se na studiju slučaja  NO2 2017:

  i)	Koja sva pitanja možete postaviti na dostupnim informacijama u ovom setu podataka?

  ii)	Koje grafikone predlažete da se upotrebe kao odgovori na ova pitanja?

  iii)	Kreirajte odgovarajuće vizuelizacije za i) i ii)



##### korisni linkovi: 

[tidyverse, visualization, and manipulation basics](https://www.rstudio.com/resources/webinars/tidyverse-visualization-and-manipulation-basics/)

[Introduction to R graphics with ggplot2](http://tutorials.iq.harvard.edu/R/Rgraphics/Rgraphics.html#introduction)

[`gglopt` cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)

[from Data to Viz](https://www.data-to-viz.com/)

[An example from the Financial Times](http://johnburnmurdoch.github.io/slides/r-ggplot/#/)

[BBC Visual and Data Journalism cookbook for R graphics](https://bbc.github.io/rcookbook/)

[ggplot as a creativity engine](http://johnburnmurdoch.github.io/slides/r-ggplot/#/)

-----------------------------
© 2019 Tatjana Kecojevic

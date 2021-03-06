---
date: "2016-04-09T16:50:16+02:00"
title: Osnovni koncepti statistike
output: 
  learnr::tutorial
weight: 6
---


U ovom odeljku upoznaćemo vas sa nizom važnih koncepata koji vam omogućuju da istražujete svoje podatke tako da budete **objektivni** 

* u sumiranju i razumevanju glavnih karakteristika varijabli (promenjivih) sadržanim u podacima, i, 
* u istraživanju prirode međusobnih odnosa između varijabli (promenjivih) koje postoje.

Za početak važno je da razumete **prirodu podataka**, da razumete: 

* Šta je **populacija**?
* Zašto koristimo **uzorke**?

Znate li koje su definicije populacije i uzorka? 😁

*Populacija je skup svih članova koji imaju određenu, zajedničku karakteristiku; skup svih ljudi ili stvari koji su od interesa u određenom istraživanju.*  

U statistici termin za skup svih podataka naziva se **populacija**. Ovo podrazumeva **“Savršenu informaciju”**, tj. da ima informacije o svim članovima skupa koji istražujemo, međutim, u stvarni istraživanjima do gotovo nikad nije tačno, vrlo je teško doći do podataka o celoj populaciji. Zato analitičari uzimaju uzorak iz populacije i istražujući uzorak dolaze do zaključaka (**inferences**) važnih za celu populaciju.

Prvo analiziraju rezultate podataka koje su zasnovane na **podacima iz uzorka populacije**, potom ukoliko uzorak ima nekog smisla, ima validnost, to je zato što je uzorak izabran na način da ukazuju i korespondira sa strukturom populacije.

Proces uzorkovanja koji do reprezentativnog uzorka veliko je područje stastičke nauke. Najednostavniji model reprezativnog uzorka je „nasumični izbor“ uzorka **"random sample"**:

*Uzorak izabran na način da svaki od elemenata u populaciji ima iste šanse da bude uključen u uzorak.*

Uzorkovanjem, informacije sagledane su *“nesavršene”* i zavise od pojedinačnih odabranih uzoraka. **Ključni problem** upotrebe uzoraka podataka da se donose validni zaključci o samoj populaciji podrazumeva znanje da se mora uzeti u obzir i sama '*greška uzorkovanja*'.

Rad sa reprezentativnim uzorcima ne sme se potcenjivati, treba ga ozbiljno razmotriti; dobar način da se proceni ovaj značaj se sagledavanje posledica upotrebe nereprezentativnih uzoraka. Knjiga autora [Darrell Huff](https://en.wikipedia.org/wiki/Darrell_Huff) called [How to Lie with Statistics](https://en.wikipedia.org/wiki/How_to_Lie_with_Statistics), koju je objavio  [Penguin](https://www.penguin.co.uk/) sadrži nekoliko anegdota o nereprezentativnim uzorcima i posledicama ako se oni tretiraju kao reprezentativni.

#### Analiza podataka uzorka 

Uobičajeno podaci se sakupljanju zato što je prethodno uočen nekakav problem, a u nadi da će sakupljeni podaci ukazati i biti od koristi u analizi tog problema. Uobičajeno je da se istraživačima uočen problem predstavi i da se od njih traži da ih oni izuče i analiziraju.

Na početku svog rada, ili analize bilo kog podatka, analitičari bi trebalo da:

i) Se uvere da se dat problem dobro razume, i da su ciljevi istraživanja jasno postavljeni. 

ii) Pre bilo kakve analize, se analitičari uvere da su pojedinačne promenjive (varijable) dobro postavljene i da su jasno sagledane. 

 <span style="color:red">Analitičar more razumeti podatke pre nego što krene u bilo kakvu analizu.</span>

Da sumirano, kada počinjete sa analizom morate <span style="color:blue">upitati sebe</span>:

i) **Da li razumem problem** koji se istražuje i da li su mi ciljevi istraživanja jasni?  
*Jedini način da se uverite da li je to tako jeste da sebi postavljate pitanja i to nastavite sve dok ne dođete do zadovoljavajući odgovara koje želite da dobijete.*

ii) Da li razumem tačno šta **svaka od varijabli (promenjivih) meri ili beleži?**


### Opisivanje promenjivih (varijabli)

Na početku treba da istražite karakteristike svake pojedinačne varijable u setu podataka. 

Nastavak rada zavisi do tipa varijabli (promenjivih) koje želite istražiti.

**Klasifikacija tipova varijabli**

Varijable (promenjive) mogu pripadati u sledeće dve široke grupe tipova:

-	**•	Kategoričke varijable (Attribute variables)**: ): sadrže podatke kategorisane u jasno razgraničene grupe po određenoj karakteristici ili osobini (atributu). 
  * pol
  * dani u nedelji
  
Uobičajeno da svakom osobini (atributu) date svoj numerički kod. S obzirom da ih tako lako možemo upotrebljavati u kodu pripremljenog za njihovo razumevanje. Na primer ukoliko je reč o muškom polu njega ćemo obeležiti na primer sa brojem 1, ženski pol sa brojem 2, itd.

-	**•	Numeričke varijable (Measured variables)**: sadrže podatke koji nastaju kao rezultat merenja ili prebrojavanja, nalaze se na nekoj numeričkoj skali: rezultuju u numeričke izraze.  
  * težina,
  * visina,
  * starost u godinama,…

Kad govorio o numeričkim varijablama govorimo o dve vrste numeričkih varijabli, kontinuirane promenjive, one koje su merene na kontinuiranoj skali merenja, na primer određena visina. Ove varijable zovemo  *kontinuirane varijable (continuous variable)*.  Drugu vrstu varijabli zovemo *diskretne varijable (discrete variable)*. One mogu imati samo određeni skup vrednosti, međusobno razdvojenih. One su, na primer, rezultat brojanja putnika u određenom autobusu. 


### Koncept statističke distribucije

**Koncept statističke distribucije ključan je za svaku statističku analizu.**

Ovaj koncept se odnosi na populaciju i pretpostavlja da imamo savršene informacije, najbolju moguću prezentaciju populacije. 

Ideje i koncepti istraživanja podataka populacije daju nam smernice na koji način treba da istražimo podatke koje imamo iz uzorka. Analitičari podataka treba da klasifikuju varijable (promenjive) ili kao kategoričke (attribute) ili kao numeričke (measured) i da istraže statističku distribuciju pojedinačnih varijabli iz podataka uzorka.  
U slučaju kategoričkih (attribute) varijabli potrebno je da istražimo broj pojedinačnih pojava svakog atributa, dok kod numeričkih varijabli računamo glavne pokazatelje deskriptivne statistike, srednju vrednost, širinu i simetriju distribucije podataka. 

**kategoričke:**
<img src="/day1/StatsConcepts/_index.en_files/figure-html/unnamed-chunk-1-1.png" width="672" />

**numeričke:**
<img src="/day1/StatsConcepts/_index.en_files/figure-html/unnamed-chunk-2-1.png" width="672" />

#### Šta nam distribucija pokazuje?

Lako je kategoričkim varijablama. Posmatramo frekvenciju (učestalost), tj. broj pojavljivanja nekog podatka u svakoj pojedinačnoj varijabli, kao što je prikazano na slici gore.

Kod numeričkih (merljivih) varijabli površina ispod krive od jedne do druge vrednosti meri relativni udeo podataka populacije koji imaju vrednost rezultata u tom rasponu. 

Statistička distribucija (raspodela) za numeričku varijablu može se sumirati sa sledeća tri ključna opisa:

-	<span style="color:red">centar</span> distribucije;
-	<span style="color:red">širina</span> distribucije;
-	<span style="color:red">simetrija</span> distribucije

<span style="color:red">**Uobičajene mere centra**</span> distribucije su **Srednja vrednost** (aritmetička sredina) i **Medijana**. Vrednost *Medijane* varijable definiše posebnu vrednost raspodele tako da je polovina vrednosti podataka manje od srednje vrednosti, a polovina veće.  

<span style="color:red">**Uobičajena mera širine**</span> distribucije su **Standardna devijacija (odstupanje) - Standard Deviation** i **interkvartalna razlika (Inter-Quartile Range)**. <span style="color:red">Standardna devijacija</span> je koren srednje vrednosti kvadratnih odstupanja od aritmetičke sredine. Konačno, standardno odstupanje je relativna mera raširenja (širine), što je veće standardno odstupanje, to je distribucija šira. <span style="color:red">Interkvartalna razlika </span> je opseg u kojem varira srednjih 50% vrednosti podataka.

Analogno medijani, moguće je definisati sledeće <span style="color:red">kvartile</span>. Oni dele set merenja u četiri grupe:

* Q1	je broj koji deli dati set tako da se ispod njega nalazi 25%, a iznad njega 75% od ukupnog broja pojedinačnih merenja koja pripadaju tom setu.
* Q2 	je broj koji deli dati set tako da se ispod njega nalazi 50%, a iznad njega 50% od ukupnog broja pojedinačnih merenja koja pripadaju tom setu. A to je upravo medijana po definiciji.
* Q3 	je broj koji deli dati set tako da se ispod njega nalazi 75%, a iznad njega 25% od ukupnog broja pojedinačnih merenja koja pripadaju tom setu.
* •	Interkartalna razlika je područje omeđeno vrednostima Q3 - Q1.

Dijagram ispod prikazuje to slikovito:

<img src="/day1/StatsConcepts/_index.en_files/figure-html/unnamed-chunk-3-1.png" width="672" />

🤓💡 Uobičajeno **srednja vrednost i standardna devijacija** dati su zajedno kao jedan par mera lokacije i širenja, a **medijana i kvartalna razlika** kao drugi par mera.

Postoji niz mera simetrije; najjednostavniji način za <span style="color:red">**merenje simetrije**</span>; poređenje je srednje (aritmetičke) vrednosti i medijane. Za savršeno simetričnu distribuciju srednja vrednost i medijana biće potpuno iste. Ova ideja vodi nas definisanju Pearsonovog koeficijenta Zakrivljenosti (Skewness) kao:

 `Pearson's coefficient of Skewness = 3(mean - median) / standard deviation`

Alternativna mera Zakrivljenosti (Skewness) je kvartalna mera Zakrivljenosti definisano kao:

`Quartile Measure of Skewness  = [(Q1 - Q3) - (Q2 - Q1)]/(Q3 - Q1)`

### Važna ključna mesta:

- Šta su podaci?
- Varijable
- Dve vrste varijabli:
	* Kategoričke varijable 
  * Numeričke varijable

- Koncept statističke distribucije:
	* Primenjen na kategoričke varijable
	* Primenjen na numeričke varijable
- Deskriptivna statistika numeričke varijable:
	* Mere centra
		- Srednja (aritmetička) vrednost, Medijana
	* Mere širine:
		- Standardna devijacija
		- Kvartilna razlika

Deskriptivna statistika omogućuje numerički opis ključnih parametara distribucije uzorka numeričke varijable.

### Istraživanje odnosa između varijabli

Jedan od ključnih koraka analize podataka je istraživanje odnosa između varijabli. Da bi to uradili potrebno je dodatno **klasifikujemo promenjive** sadržane u podacima, da ih klasifikujemo kao <span style="color:red">**odzivne (response)**</span> varijable ili kao <span style="color:red">**eksplanatorne**</span> varijable.  

**Odzivne (response)** varijable su nepromenjive koje mere direktno ili inderektno ciljeve analize.

**Eksplanatorne** varijable su one koje utiču na odzivne varijable.

#### Bivarijantni odnosi

Uopšteno postoje četiri različite kombinacije odzivnih i eksplanatornih varijabli. Ove četiri kombinacije su prikazane na slici dole:

![Red variant](/day1/StatsConcepts/images/RelationshipMatrix.png?width=30pc)

Polazna tačka <span style="color:red">istraživanja odnosa</span> između **odzivne** varijable i **ekaplanorne** varijable počinje sa istraživanjem varijabli, definicijom odzivne varijable, ili odzivne i eksplanatorne varijable.

🤓💡: U velikim empirijskim istraživanjima može postojati veći broj ciljeva samog istraživanja, i sledstveno tome i više odzivnih varijabli.

Metod za istraživanje odnosa između odzivne varijable i eksplanatorne zavisa od tipova varijabli. Metodologija se razlikuje u zavisnosti od kombinacije ovog odnosa kao što smo već videli na prethodnoj slici. Primena neodgovarajuće metode stvara probleme. 💡⚡️😩  

### Metodologija analize podataka (DA metodologija)

Na početku trebate da imate jasnu ideju šta je to odnos između odzivne i eksplanatorne varijable. To će vam pomoću da postavite okvir za definisanje <span style="color:red">procesa analize podataka</span> koji će istražiti vezu i odnos između ove dve varijable, i proveriti ideju sa kojom ste počeli. 

Sledeći korak je da <span style="color:red">*upotrebite osnovnu deskriptivnu statistiku kako biste ocenili prirodu povezanosti između varijabli*</span>. Ovaj osnovni pristup omogućiće vam da zaključite da li se na osnovu analize uzorka može govoriti o povezanosti, ili postojanju dokaza o nepovezanosti varijabli, ili da je osnovni pristup neupitan i da je potrebna dalja osetljivija analiza podataka. Ovaj korak se naziva <span style="color:red">**Početna analiza podataka (Initial Data Analysis)**</span> i ponekad skraćeno <span style="color:red">**IDA**</span>.

Ukoliko Početna analiza podataka potvrdi da je <span style="color:red">**Dalja analiza podataka (Further Data Analysis, FDA)**</span> (<span style="color:red">**FDA**</span>) potrebna, onda ovaj korak traži jedno od sledeće dva zaključka:

i) Analiza uzorka pokazuje da ne postoji veza između odzivne i eksplanatorne varijable.

ili

ii)	Analiza uzorka pokazuje da postoji veza između odzivne i eksplanatorne varijable.

Rezultat analize je jedna od dve alternative date gore. Ukoliko je rezultat da ne postoji dokaz o povezanosti, onda dalji nastavak nije potreban, s obzirom da je analiza završena.

Međutim, ukoliko se pokaže suprotno tj. da je rezultat da povezanost ipak postoji, onda priroda te povezanosti između dve varijable treba da bude opisana i objašnjena.

🤓💡 <span style="color:red">**Metodologija analize podataka **</span> opisana gore zahteva odgovor na sledeća ključna pitanja:

Na osnovu uzorka da li postoji veza između odzivne i eksplanatorne varijable?
 
Odgovor može biti jedan od sledeća dva 

i)	Nema dokaza o povezanosti

ii)	Da, postoji povezanost, a ona treba dalje da se opiše.

Ovaj proces može se prestaviti dijagramom:

![Red variant](/day1/StatsConcepts/images/DAMethodology.png?width=40pc)

Za bilo koju od četiri navedene situacije, analitičar/ka treba da zna šta će biti sadržano u Početnoj analizi podataka (IDA) i kako da je sprovede i objasni. Ukoliko se traži Dalja analiza podataka, onda analitičar/ka treba da zna kako će sprovesti i opisati Dalju analizu podataka.

#### Numeričke Vs kategoričke (2-nivoa)

Postoji povezanost između numeričke odzivne i kategoričke eksplanatorne varijable ukoliko srednja vrednost odzivne je zavisna od nivoa kategoričke eksplanatorne varibjable.

Dajemo numeričkoj odzivnoj i kategoričkoj eksplanatornoj varijabli dva nivoa, "<span style="color:red">crveni</span>" & "<span style="color:blue">plavi</span>". Ukoliko su statistička distribucija (raspodela) odzivne varijable obojene "<span style="color:red">crveno</span>" a kategoričke "<span style="color:blue">plavo</span>" i potpuno su iste onda nivo kategoričke varijable nama uticaj na vrednosti odzivne, tada nema povezanosti.  

Ovo možemo ilustrovati slikom dole:

![Red variant](/day1/StatsConcepts/images/MvAMethodology.png?width=40pc)


#### Numerička Vs Numerička

Na početku treba da imamo jasnu ideju šta znači povezanost između numeričkih vrednosti odzivne varijable i numeričke vrednosti ekplanatorne varijable. Zamislite populaciju koju istražujemo da je sastavljena od velikih brojeva članova populacije, i da je na svakom članu populacije su merene dva merenja, vrednost Y za odzivnu varijablu i vrednost X za eksplanatornu. Za celu populaciju, napravimo grafikon koji će prikazati vrednosti Y na y-osi i vrednosti vrednosti X na x-osi. 

Ukoliko se na grafikonu prikaže savršena linija, onda je vrlo jasna povezanost između Y i X. Tada ako znamo vrednost X lako možemo naći vrednost Y na grafikonu. Ovo nije mnogo verovatno da će se prikazati u kontekstu analize podataka, s obzirom na prirodu povezanosti koja je *deterministička povezanost*. Deterministička znači da ukoliko je vrednost X poznata da se onda Y može precizno determinisati iz povezanosti Y i X. Ono što će češće biti slučaj jeste da će i druge varijable, ne samo X, takođe imati uticaj na Y. 

Ukoliko istražujemo prirodu povezanosti između Y i X, onda je možemo predstaviti na sledeći način:

`Y = f(X) + effect` svih drugih varijabli [efekti svih ostalih varijabli uobičajeno se obeležavaju skraćeno sa e]

Razmotrite model:

`Y = f(X) + e`		[e predstavlja effekat svih ostalih varijabli]

Uticaj na odzivnu varijablu Y može se predstaviti da se sastoji od sledeće dve komponente:

i) komponente Y mogu se objasniti promenama u vrednostima X, [delom i zbog toga što promene X idu preko f(X)] 

ii)	komponente Y mogu se objasniti promenama u vrednostima drugih faktora [deo koji nije objašnjen promenama u X]

To možemo predstaviti u kraćoj formi kao '<span style="color:red">Varijacije u Y objašnjene su promenama X</span>' ili '<span style="color:red">**Objašnjene varijacije**</span>' and the '<span style="color:red">Varijacije u Y nisu objašnjenje promenama u X</span>' ili '<span style="color:red">**Neobjašnjene varijacije**</span>'. 

Zaključno, *Ukupna varijacija u Y* sastavljena je od sledeće dve komponente:

- 'Promene u Y objašnjene su promenama u X' i  
- 'Promene u Y nisu objašnjene promenema u X' 

A to se može napasati na sledeći način:

	`'The Total Variation in Y' = 'Explained Variation' + 'Unexplained Variation'`

🤓💡 Diskusija je počela sledećom idejom:

Y = f(X) + e

Potom, da bismo kvantifikovali jačinu uticaja na Y podelili smo uticaj na dve komponente:

	'The Total Variation in Y' = 'Explained Variation' + 'Unexplained Variation'

Ovo nam predstavlja dva pitanja koja moramo sebi postaviti:
A:	Da li se može model povezanosti napraviti?
B.	Mogu li se „Ukupna varijacija u Y“, „Objašnjenja varijacija“ i „Neobjašnjenja varijacija“ meriti?

Šta nam govore ove količine?  

Možda možemo posmatrati proporciju „Objašnjenje varijacije u Y“ u „Ukupnoj varijaciji u Y“. Ovaj odnos uvek je na skali od 0 do 1, ali se on uobičajeno iskazuje kao procenat tj. na skali od 0 do 100%. On se naziva „R Squared (R kvadrat)“ i definiše se  na sledeći način:

  R_sq: 0% (no link) <--------------- 50% (Statistical Link) ---------------> 100% (Perfect Link) 

Definicija i objašenjenje `R_sq` veoma je važan alat za analitičare za praćenje povezanosti između numeričke odzivne i numeričke eksplanatorne varijable.

Ove ideje možemo postaviti u okvir DA metodologije onako kako je to prikazano dole.

![Red variant](/day1/StatsConcepts/images/MvMMethodology.png?width=40pc)

🤓💡 Napomena: Teško ćete biti u situaciji u kojoj je R_sq toliko blizu nuli da ćete moći da zaključite na osnovu uzorka, u fazi Početne analize (IDA istraživanja), da ne postoji povezanosti ove dve varijable. Ukoliko je R_sq je veoma mali (na primer oko 2%) to onda treba dodatno da se testira da bi se zaključilo da li je to statistički značajno na osnovu uzorka upotrebom Dalje analize podataka (FDA).

#### Dalja analiza podataka (FDA)

Ukoliko je <span style="color:red">'**Početna analiza podataka (IDA)**'</span><span style="color:red">*neubedljiva*</span>, onda je potrebno uraditi <span style="color:red">'**Dalju analizu podataka**'</span>. 

„Dalja analiza podataka“ je procedura koja vam omogućuje da donesete odluku, na osnovu uzorka, o sledeća dva rezultata:  
- Ne postoji povezanost 
-	Postoji povezanost

Ove statističke procedure nazivaju se <span style="color:red">**testiranje hipoteza**</span>, koji vam u suštini <span style="color:red">*omogućuju da odlučite između sledeća dva rezultata:*</span>: “Ne postoji povezanost ” ili “Postoji povezanost” na osnovu uzorka.

Svi testovi hipoteza se sprovode u četiri faze:

- Faza 1:		Određivanje hipoteze.

- Faza 2:		Definisanje parametara testa i pravilo zaključivanja.

- Faza 3:		Istraživanje uzorka.

- Faza 4:		Zaključivanje.

##### Statistički modeli koji se upotrebljavaju u FDA

* Numerička odzivna varijabla vs Kategorička eksplanatorna varijabla sa tačno dva nivoa:
  
  - t-test

* Numerička odzivna varijabla vs Kategorička eksplanatorna varijabla sa više od dva nivoa:
  
  - One-Way ANOVA
  
* Numerička odzivna vs Numerička eksplanatorna varijabla
  
  - Jednostavni model regresije (Simple Regression Model)
  
* Numerička odzivna vs Numeričke eksplanatorne varijabl**e**
  - Multifaktorni model regresije (Multifactor Regression Model)

* Kategorička odzivna varijabča vs Numerička eksplanatorna varijabla
  - Chi-Square test nezavisnosti

## ZADACI 👇

Proverite vaše znanje odgovarajuću na sledeća pitanja:

1) Koje su osnovne ideje koje omogućavaju da se istraži odnos između dve varijable (promenljive)?

2) Koja je svrha zbrine statistike?

3)	Koja metodologija i kako se koristi za istraživanje povezanosti između:

  i) Numeričke odzivne varijable i kategoričke eksplanatorne varijable?
  
  ii) Numeričke odzivne varijable i numeričke eksplanatorne varijable?





-----------------------------
© 2019 Tatjana Kecojevic

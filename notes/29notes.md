# Innhold
- [Forelesning 1 - Problemer og algoritmer](#forelesning-1---problemer-og-algoritmer)
    - [Kapittel 1 - Rollen til algoritmer i utregning](#kapittel-1---rollen-til-algoritmer-i-utregning)
        - [1.1 Algoritmer](#11-algoritmer)
        - [1.2 Algoritmer som en teknologi](#12-algoritmer-som-en-teknologi)
    - [Kapittel 2 - Komme i gang](#kapittel-2---komme-i-gang)
        - [2.1 Innsettingssortering](#21-innsettingssortering)
        - [2.2 Analysering av algoritmer](#22-analysering-av-algoritmer)
    - [Kapittel 3 - Funksjonsvekst](#kapittel-3---funksjonsvekst)
        - [3.1 Asymptotisk notasjon](#31-asymptotisk-notasjon)
    - [Forelesning 1](#forelesning-1)
        - [Innsettingssortering](#innsettingssortering)
        - [Asymptotisk notasjon](#asymptotisk-notasjon)
        - [Kjøretid](#kjøretid)
        - [Dekomponering - induksjon og rekursjon](#dekomponering---induksjon-og-rekursjon)
        - [Loop - rekursjon og induksjon](#loop---rekursjon-og-induksjon)
        - [Sum - rekursiv løsning](#sum---rekursiv-løsning)
        - [Sum - iterativ løsning](#sum---iterativ-løsning)
        - [Rekursjon vs iterasjon](#rekursjon-vs-iterasjon)
        - [Insertion-sort](#insertion-sort)
        - [Induksjonseksempel](#induksjonseksempel)
        - [Noen vanlige dekomponeringer](#noen-vanlige-dekomponeringer)

# Forelesning 1 - Problemer og algoritmer

- Ide bak induksjon og rekursjon er viktig
    - Kun trenger å se på neste trinn og anta resten er greit
- Læringsmål:
    - Forstå bokas pseudokode-konvensjoner
    - Kjenne egenskapene til random-access machine-modellen (RAM)
    - Kunne definere problem, instans og problemstørrelse
    - Kunne definere asymptotisk notasjon,	store O, store Omega, theta, lille o og lille omega.
    - Kunne definere best-case, average-case og worst-case
    - Forstå løkkeinvarianter og induksjon
    - Forstå rekursiv dekomponering og induksjon over delproblemer
    - Forstå INSERTION-SORT
    

## Kapittel 1 - Rollen til algoritmer i utregning

### 1.1 Algoritmer

- Algoritme: veldefinert beregningsmetode som tar en eller fler verdier som input og produserer en eller fler verdier som output
    - Input → sekvens av beregninger → output
- Formell definisjon sorteringsproblemet:
    - Input: sekvens av *n* tall: $<a_1, a_2, …, a_3>$
    - Output: permutasjon (omordning) av input sekvensen så elementene ordnes i økende verdi: $<a_1’, a_2’,…, a_n’>$
    - Eksempel: $<31,41,59,26>$ → $<26,31,42,59>$
- Inputsekvens kalles instans
- Algoritme er korrekt om den gir riktig output for hver inputinstans

#### Parallellisme

- Lurt å designe algoritmer som tar utgangspunkt i parallellisme, da datamaskiner idag lages med fler prosessorer

### 1.2 Algoritmer som en teknologi

- Beregningstid og minneplass er begrenset, så trenger tids- og romeffektive algoritmer

#### Effektivitet

- Forskjell i effektivitet er ofte viktigere enn forskjell på maskiners egenskaper

#### Algoritmer og andre teknologier

- Total ytelse av et system avhenger av algoritme, kan derfor telles som teknologi
- Algoritmer er ofte også i kjernen til andre teknologier

## Kapittel 2 - Komme i gang

- I kapittelet skal vi se på:
    - Innsettingssortering for å løse sorteringsproblemet
    - Hvordan pseudokode kan brukes for å spesifisere algoritmer
    - Argumentere for at spesifisert algoritme er korrekt
    - Analysere kjøretiden til spesifisert algoritme

### 2.1 Innsettingssortering

- Insertion sort
- Formell definisjon sorteringsproblemet:
    - Input: sekvens av *n* tall: $<a_1, a_2, …, a_3>$
    - Output: permutasjon (omordning) av input sekvensen så elementene ordnes i økende verdi: $<a_1’, a_2’,…, a_n’>$
- Keys: Tallene som skal sorteres
- Input: array av *n* elementer
- Innsettingssortering er effektiv ved små inputarrays
- Kortstokkanalogi:
    - Har kortene $[3,5,2,9,4]$ i høyre hånd. I venstre hånd skal sorterte kort plasseres.
    - Plasserer først $3$ i venstre hånd, sortert uansett
        - Venstre hånd: $[3]$
        - Høyre hånd: $[5,2,9,4]$
    - Plasserer neste element ($5$) i venstre hånd, på sortert posisjon
        - Venstre hånd: $[3,5]$
        - Høyre hånd: $[2,9,4]$
    - Plasserer neste element ($2$) i venstre hånd, på sortert posisjon
        - Venstre hånd: $[2,3,5]$
        - Høyre hånd: $[9,4]$
    - Plasserer neste element ($9$) i venstre hånd, på sortert posisjon
        - Venstre hånd: $[2,3,5,9]$
        - Høyre hånd: $[4]$
    - Plasserer neste element ($4$) i venstre hånd, på sortert posisjon
        - Venstre hånd: $[2,3,4,5,9]$
        - Høyre hånd: $[]$
- INSERTION-SORT: tar inn array $A[1,...,n]$ med lengde $n$. Antall elementer i $A$ gis ved $A.length = n$
    
    ```
    INSERTION-SORT(A)
    1 for j = 2 to A.length
    2     key = A[j]
    3     // Insert A[j] into the sorted sequence A[1..j-1]
    4     i = j-1
    5     while i > 0 and A[i] > key
    6         A[i+1] = A[i]
    7         i = i-1
    8         A[i+1] = key
    ```
    
    - $j$ er nåværende kort, blir innsatt i sortert kortsekvens $A[1,...,j-1]$
    - I begynnelsen av iterasjon av for-løkke vil submatrise $A[1,...,j-1]$ bestå av elementer fra den opprinnelige matrisen, i sortert rekkefølge
- Loop invariant:
    - Et krav som er sant før og etter iterasjon av en loop.
    - Må vise tre ting ved loop invarianten:
        - Initialisering: det er sant før første iterasjon av loopen
        - Vedlikeholde: det er sant før en iterasjon av loopen, og fortsetter å være sant før neste iterasjon
        - Terminering: når loopen terminerer vil invarianten gi oss en nyttig egenskap som hjelper oss vise at algoritmen er korrekt
    - Når to første egenskaper holder vil loop invarianten være sann før alle iterasjoner av loopen
        - Første egenskap viser grunntilfellet
        - Andre egenskap viser induktivt steg
    - Tredje egenskapen sier hva som terminerer loopen og at induksjonen stopper
    - Loop invariant i innsettingssortering:
        - Initialisering: se om loop invariant holder første iterasjon, $j=2$
            - Submatrisen $A[1,...,j-1]$ vil inneholde $A[i]$, som er første element i original matrise. Submatrisen er sortert.
        - Vedlikehold: se om loop invarant holder for alle iterasjoner
            - Loop vil flytte element ved posisjon $j$ mot venstre helt til den finner riktig posisjon, der den vil sette elementet. Submatrisen $A[1,...,j]$ vil dermed inneholde de originale elementene, i sortert rekkefølge.
        - Terminering: betingelsen for loopen er: $j>A.length=n$
            - $j$ øker med 1 for hver iterasjon vil man tilslutt $j>n+1$. Om man setter det i formel for submatrisen for man $A[1,...,n]$, hele matrisen er sortert
        - Alle tre egenskapene stemmer, algoritmen er korrekt

#### Pseudokode konvensjoner

- Innrykk indikerer blokkstruktur
- Loop teller holder sin verdi etter loop er terminert
- Bruker “to” i loops når de teller up, “downto” når de teller ned. “by” når det endres med mer enn 1
- Variabler er lokale
- Aksesserer arrays slik: A[i]
- Sammensatt data organiseres i objekter, henter attributter ved feks $A.length$
- Return overfører kontroll til kallende punkt i kallende prosedyre
- Bruker “and” og “or”

### 2.2 Analysering av algoritmer

- Analyse av algoritmer hjelper å forutse ressurser algoritmen krever, kjøretid er viktigste ressurs
- Bruker generisk, enprosessor RAM (random-access maskin) modell, så algoritmer implementeres som dataprogram og instruksjoner blir utført en etter en
- RAM har instruksjoner for aritmetikk (addisjon, subtraksjon, divisjon, rest, osv), data (load, lagre, kopiere) og kontroll (return, osv)
- Instruksjoner tar konstant tid
- Bruker int og float
- Begrensning på størrelsen til hvert ord med data

#### Analyse av innsettingssortering

- Beskriver kjøretid som funksjon av inputsørrelsen
- Inputstørrelse: antall enheter i input, antall bits som trengs for å representere input, osv. Størrelsen oppgis ved hvert problem.
- Kjøretid: antall primitive operasjoner/steg som utføres. Hver linje i pseudokode krever konstant mengde tid å utføre
    - En linje kan ta mer tid enn annen, men linje $i$ tar $c_i$ tid, hvor $c_i$ er konstant
- Tidskostnad per påstand og antall ganger linjer utføres
    - $t_j$ er antall ganger while loop testen (linje 5) utføres for denne verdien av

|  | INSERTION-SORT(A) | Cost | Times |
| --- | --- | --- | --- |
| 1 | for j = 2 to A.length | $c_1$ | $n$ |
| 2 |     key = A[j] | $c_2$ | $n-1$ |
| 3 |     // Insert A[j] into the sorted sequence A[1..j-1] | $0$ | $n-1$ |
| 4 |     i = j-1  | $c_4$ | $n-1$ |
| 5 |     while i > 0 and A[i] > key | $c_5$ | $\sum_{j=2}^n t_j$ |
| 6 |         A[i+1] = A[i] | $c_6$ | $\sum_{j=2}^n (t_j-1)$ |
| 7 |         i = i-1 | $c_7$ | $\sum_{j=2}^n (t_j-1)$ |
| 8 |     A[i+1] = key  | $c_8$ | $n-1$ |

#### Good to know
>$$
\sum_{j=2}^2j=\frac{n(n+1)}{2}-1
$$

>$$
\sum_{j=2}^n(j-1)=\frac{n(n-1)}{2}
$$

- Kjøretid til algoritme er summen av hver påstand som blir utført
- $T(n)=c_1n+c_2(n-1)+c_4(n-1)+c_5\sum_{j=2}^nt_j+c_6\sum_{j=2}^n(t_j-1)+c_7\sum_{j=2}^n(t_j-1)+c_8(n-1)$
- Er i best-case allerede sortert, $A[i]\leq key$ for alle elementer, while-løkke vil ikke utføres. $t_j=1$ for alle $j$
    - Best-case blir: $T(n)=c_1n+c_2(n-1)+c_4(n-1)+c_5(n-1)+c_8(n-1)$
    - Kan skrives som $an+b$, lineær funksjon av $n$
- I worst-case er matrisen sortert motsatt, hvert element $A[j]$ sammenlignes med hele sorterte submatrisen $A[1,...,j-1]$ så $t_j=j$.
    - Worst case blir: $T(n)=c_1n+c_2(n-1)+c_4(n-1)+c_5(\frac{n(n+1)}{2}-1)+c_6\frac{n(n-1)}{2}+c_7\frac{n(n-1)}{2}+c_8(n-1)$
    - Kan skrives som $an^2+bn+c$, kvadratisk funksjon av $n$
    

#### Worst-case analyse

- Fokuserer som regel på worst-case kjøretid
    - Worst-case kjøretid for algoritme gir øvre grense på kjøretiden for enhver input. Garanterer at algoritmen ikke tar lenger tid.
    - Worst-case kan forekomme ofte
    - Average-case er ofte nesten like dårlig som worst-case

#### Vekstraten

- Ser kun på ledende begrep i formel og ignorerer konstanter
- Worst case insertion sort: $\Theta(n^2)$

## Kapittel 3 - Funksjonsvekst

- Vekstrate til algoritmens kjøretid er karakterisering av algoritmens effektivitet, lar oss sammenligne relative ytelser til alternative algoritmer
- Asymptotisk effektivitet: når inputstørrelse er så stor at kun vekstraten til kjøretid er relevant
- Algoritmer som er asymptotisk mer effektive vil være best for alt annet enn små input

### 3.1 Asymptotisk notasjon

- Notasjon brukt for asymptotisk kjøretid er definert som funksjoner der domene er sett av naturlige tall, $\mathbb{N}=\{0,1,2,...\}$

#### Asymptotisk notasjon, funksjoner og kjøretider

<img src="assets/thetaGraph.png" alt="Theta explained" height="200px"></img>
<img src="assets/oGraph.png" alt="Big O explained" height="200px"></img>
<img src="assets/omegaGraph.png" alt="Omega explained" height="200px"></img>


#### $\Theta$-notasjon - asymptotisk øvre og nedre grense


> $\Theta(g(n))=\{f(n): \text{det eksisterer positivt konstanter } c_1, c_2 \text{ og } n_0 \text{ så } 0\leq c_1g(n)\leq f(n)\leq c_2g(n) \text{ for alle }n\geq n_0\}$

- Funksjon $f(n)$ hører til settet $\Theta(g(n))$ om det eksisterer positive konstanter som gjør at $f(n)$ blir “sandwiched” mellom $c_1g(n)$ og $c_2g(n)$ for tilstrekkelig stor n
    - Rar settnotasjon, but oh well: $f(n)=\Theta(g(n))$
- $f(n)$ er lik $g(n)$ innenfor en konstant faktor, $g(n)$ er asymptotisk tett grense for $f(n)$. Asymptotisk tett grense betyr øvre og nedre grense.
    - $f(n)\in \Theta(g(n))$  er asymptotisk ikke-negativ, altså at $f(n)$ ikke er negativ når $n$ er tilstrekkelig stor
- Eksempel: $f(n)=\frac{1}{2}n^2-3n$ har kjøretid $\Theta(n^2)$ ($g(n)=n^2$)
    - Neglisjerer ledd av lavere orden og koeffisienter til ledd med høyeste orden. Begynner med å finne positive konstanter $c_1, c_2$ og $n_0$:
        
        $$
        c_1n^2\leq\frac{1}{2} n^2-3n\leq c_2n^2
        $$
        
        for alle $n\geq n_0$. Om man deler på $n^2$:
        
        $$
        c_1\leq \frac{1}{2}-\frac{3}{n}\leq c_2
        $$
        
    - Høyre ulikhet: $\frac{1}{2}-\frac{3}{n}\leq c_2$
        - Holder for $n\geq 1$ ved å velge $c_2\geq 1/2$
    - Venstre ulikhet: $c_1\leq\frac{1}{2}-\frac{3}{n}$
        - Holder for $n\geq 7$ ved å velge $c_1\leq \frac{1}{14}$
    - $c_1=\frac{1}{14}, c_2\frac{1}{2}, n_0=7$

#### $O$-notasjon - asymptotisk øvre grense

>$O(g(n))=\{f(n): \text{det eksisterer positivt konstanter } c \text{ og } n_0 \text{ så } 0\leq  f(n)\leq cg(n) \text{ for alle }n\geq n_0\}$


- Om $f(n)=\Theta(n)$ må også $f(n)=O(n)$
- Dobbel løkke gir ofte kjøretid på $O(n^2)$

#### $\Omega$-notasjon - asymptotisk nedre grense

>$\Omega(g(n))=\{f(n): \text{det eksisterer positivt konstanter } c \text{ og } n_0 \text{ så } 0\leq  cg(n)\leq f(n) \text{ for alle }n\geq n_0\}$

##### Teorem 3.1

For to funksjoner $f(n)$ og $g(n)$ har vi at $f(n)=\Theta(g(n))$ hvis og bare hvis $f(n)=O(g(n))$ og $f(n)=\Omega(g(n))$

#### Asymptotisk notasjon i ligninger og ulikheter

- Når asymptotisk notasjon står alene på høyre side av ligningen ($n=O(n^2)$) betyr det at $n\in O(n^2)$
- Når asymptotisk notasjon står i formel ($2n^2+3n+1=2n^2+\Theta(n)$) betyr det at den representerer anonym funksjon vi ikke nevner
- Ulikt om asymptotisk notasjon er på høyre eller venstre side av likhet
    - $2n^2+3n+1=2n^2+\Theta(n)$
    - $2n^2+\Theta(n)=\Theta(n^2)$

#### $o$-notasjon - asymptotisk, ikke-tett øvre grense

- Asymptotisk øvre grense gitt av $O$-notasjon kan være asymptotisk tett eller ikke (asymptotisk tett = nøyaktig grense for store $n$)
- $o$-notasjon er ikke asymptotisk tett
    - $2n=o(n^2)$, $2n^2\neq o(n^2)$
- $\log_{n\to\infty}\frac{f(n)}{g(n)}=0$

#### $\omega$-notasjon - asymptotisk, ikke-tett nedre grense

- $\omega$-notasjon er ikke asymptotisk tett
- $\log_{n\to\infty}\frac{f(n)}{g(n)}=\infty$

#### Regler for asymptotisk notasjon

- Transitivitet: $f(n)=\Theta(g(n))$ og $g(n)=\Theta(h(n))$ gir at $f(n)=\Theta(h(n))$ (gjelder også for $O, \Omega, o, \omega$)
- Refleksivitet: $f(n)=\Theta(f(n))$, $f(n)=O(f(n))$ og $f(n)=\Omega(f(n))$
- Symmetri: $f(n)=\Theta(g(n))$ hvis og bare hvis $g(n)=\Omega(f(n))$
- Transpose symmetri: $f(n)=O(g(n))$ hvis og bare hvis $g(n)=\Omega(f(n))$ (gjelder også for $o, \omega$)
    - $f(n)=O(g(n))::a\leq b$
    - $f(n)=\Omega(g(n))::a\geq b$
    - $f(n)=\Theta(g(n))::a=b$
    - $f(n)=o(g(n))::a<b$ ($f(n)$ er asymptotisk mindre enn $g(n)$)
    - $f(n)=\omega(g(n))::a>b$ ($f(n)$ er asymptotisk større enn $g(n)$)

## Forelesning 1

- Bogo-sort = bad

### Innsettingssortering

- Setter inn neste kort og bygger trinnvis på forrige del-løsning

### Asymptotisk notasjon

- Problem: relasjon mellom input og output
- Instans: bestemt input
- Problemstørrelse ($n$): lagringsplass som trengs for en instans

<img src="assets/oOmegaTheta.png" alt="Theta explained" height="200px"></img>

<img src="assets/asymptoticNotationSymbols.png" alt="Theta explained" height="200px"></img>

### Kjøretid

- Best case: best mulig kjøretid for gitt størrelse
- Worst case: verste mulig kjøretid for gitt størrelse
- Average case: forventet kjøretid, gitt sannsynlighetsfordeling. Hvis ikke fordelingen er gitt antar man alle inputs er like sannsynlige.
- Bruker som regel worst case

#### Brute force

- 8 kort skal sorteres
- Første posisjon har 8 muligheter, andre 7, osv
- Antall muligheter: $8\cdot7\cdot6\cdot5\cdot4\cdot3\cdot2\cdot1=8!$
- Kjøretid: $\Theta(n!)=\text{BAD}$

#### Innsettingssortering

- Worst case er array sortert i motsatt rekkefølge. Da må $A[j]$ flyttes forbi $A[1,...,j-1]$ andre elementer.
- Må totalt $1+2+3+4+5+6+7+8=28$ flyttinger til
- $\sum_{i=1}^{n-1}=\frac{n(n-1)}{2}=\Theta(n^2)$

### Dekomponering - induksjon og rekursjon

- Induksjon kombinerer konseptene på figuren under
    - Venstre: $P(a)$ er sann for vilkårlig $a$, derfor er vil $P(x)$ være sann for alle $x$
    - Midten: antar midlertidig at $P$ er sann og viser deretter at $Q$ er sann. Hvis P, så Q
    - Høyre: kalles modus ponens, og går ut på at hvis $P$, så $Q$ kompinert med at $P$ er sann betyr at $Q$ er sann
        
<img src="assets/complicatedInductionExplination.png" alt="Dude I don't get this" height="200px"></img>
        

- Introduserer og eliminerer mange implikasjoner og generell induksjon kan foregå i et nettverk av utsagn. Kan likevel alltid ordne dem i serie med trinn. Grunntilfellet baserer seg igkke på noen andre, resten er induktive (følger tidligere trinn)
- Vise induksjon:
    - Må sjekke at grunntilfelle gjelder
    - Beskriver alle induktive trinn og sjekker om et vilgårlig tilfelle gjelder
    - Vil vise implikasjonen $(P\to Q)$ som vi gjør ved å anta at forrige trinn gjelder og at dette gjør at neste trinn også gjelder (induksjonshypotesen)
    - Vet at grunntilfellet stemmer, gjør at alle induktive tilfeller stemmer

<img src="assets/complicatedLadderInductionExplination.png" alt="Yet another induction explained with a ladder" height="300px"></img>

- Et problem er en relasjon mellom instans og riktig svar. Algoritmer finner ett riktig svar for hver instans og må løse alle instanser
- Ser på en instans vi ikke vet hvordan vi løser. Spalter instansen i en eller fler delinstanser og antar vi kan løse delinstansene. Kan til slutt samle delsvarene til endelig svar og ha løsning på instanse
    - Fungerer fordi det er basert på induksjon. Viser grunntilfelle, antar delløsning og viser at spaltingen/samlingen er korrekt. Om disse er riktige vil alle svarene være riktige og løsningen er riktig.
        
        <img src="assets/dekomponering.png" alt='"Dekomponering" at its finest' height="400px"></img>
        <img src="assets/dekomponeringWithLadder.png" alt='"Dekomponering" at its finest, with a ladder this time' height="200px"></img>

- Kjerneprinsippet går ut på å bryte problemet ned så det kan løses trinn for trinn. Prinsippet lar oss fokusere på ett representativt trinn. Vanlig teknikk ved induksjon er rekursive prosedyrer, som er prosedyrer som kaller seg selv. Når vi skal løse et problem med en algoritme må vi:
    - Dele problemet opp i mindre problem
    - Anta at vi kan løse de mindre problemene = induktiv premiss
    - Konstruere en fullstendig løsning ut fra delløsningene = induksjonstrinn
    - Sørge for at ting terminerer (evig while-loop = bad)

### Loop - rekursjon og induksjon

- Loop invarianter er egenskaper som er sann før og etter hver iterasjon
- Tre ting å sørge for når man lager loop:
    - Initialisering: invarianten er sann før den første iterasjonen
    - Vedlikehold i hver iterasjon: skiller mellom
        - Det induktive premisset er at vi antar at invarianten er sann før iterasjon
        - Induksjonstrinnet er at vi viser at det er sant etter iterasjonen
    - Terminering: løkka stopper

### Sum - rekursiv løsning

- Ønsker å summere elementene i tabell vha rekursjon
- Får funksjon til å kalle op seg selv for alle elementer unntatt det siste (det blir lagt til i initielle kjøring av funksjonen)
- Invariant er at vi har summert riktig så langt. Grunntilfellet er summen av en tom sekvens (0). Sjekker via if-setning. Induktive premiss er at summen er rett ($SUM(A,i-1)$ er summen av  $A[1,…,i-1]$. Induksjonstrinnet er å legge til det siste elementet så den endelige summen blir rett (returnsetningen som sikrer at $SUM(A,i)$ er summen av $A[1,…,i]$)

```
SUM(A,i)
1 if i < 1
2     return 0
3 tmp = SUM(A,i-1)
4 return tmp + A[i]
```
Gjennomgang av rekursiv løsning av sum:
- SUM([1,2,3],3) = 6
    - i < 1 (false)
    - tmp = SUM([1,2,3],2) = 3
        - i < 1 (false)
        - tmp = SUM([1,2,3],1) = 1
            - i < 1 (false)
            - tmp = SUM([1,2,3],0) = 0
                - i < 1 (true) → return 0
            - return tmp + A[1] → return 1
        - return tmp + A[2] → return 3
    - return tmp + A[3] → return 6

### Sum - iterativ løsning

- Ønsker å summere elementene vha induksjon
- Invarianten er at vi har summert riktig så langt og grunntilfellet (initialiseringen) er at en tom sum er 0
- Induktivt premiss er at summen er rett før iterasjon, mens induksjonstrinnet er at vi legger til neste element
- Termineringen er at vi til slutt har summert alle elementene
- Initialiseringen er at summen så langt er null (res = 0). Induksjonshypotesen er at res er summen av $A[1,...,j-1]$. Induktivt trinn er at res er summen av $A[1,...,j]$ (at siste element blir lagt til). Terminering er når $j=n$, så res er summen av $A[1,...,n]$ der $n$ er lengden til tabellen.

```
SUM(A)
1 res = 0
2 for j = 1 to A.length
3     res = res + A[j]
4 return res
```
Løsning av iterativ løsning av sum:
- SUM([1,2,3])
    - res = 0
    - j = 1 to 3
        - res = 0 + 1 = 1
    - j = 2 to 3
        - res = 1 + 2 = 3
    - j = 3 to 3
        - res = 3 + 3 = 6
    - return 6

### Rekursjon vs iterasjon

- Rekursjon og iterasjon er på en måte ekvivalente, men skal sammenligne hvordan de oppfører seg
    - Begge har induktivt premiss: “tidligere” delen allerede er summert
    - Rekursiv variant: gjør det rekursivt før siste element legges til
    - Iterativ variant: har allerede gjort det iterativt når siste element legges til
- Begge metoder bygger på at det er rett for $n-1$ elementene og bygger videre til $n$ ved å gjøre noe med siste element

### Insertion-sort

- Dekomponeringen er omtrent samme som SUM, men bytter ut sum med sortering
- Rekursiv dekomponering: sorterer alle unntatt det siste elementet. Invarianten er at sortering er rett så langt. Induktivt premiss er at $n-1$ elementer er sortert riktig, induksjonstrinn er å sette inn siste elementet
- Iterativ dekomponering: invarianten er at sorteringen er rett så langt, initialisering er at tom sekvens er sortert. Induktivt premiss er at sortering er rett før iterasjon, induksjonstrinn er å sette inn neste element. Termineringen er at alle elementer er sortert.
- Bruker induksjon til å lage algoritmen
    - Induksjonshypotese: $A[1,...,j-1]$ er sortert rett (gis av for-løkken)
    - Induksjonstrinn: neste element blir satt på rett plass (sikres av at elementet lagres som key og settes på riktig plass vha sammenligning med andre elementer)
    - Bruker i for å betegne elementet foran (så lenge det er et element foran som er større enn key skal elementet foran flytte til høyre of key til venstre. Oppdaterer så i, og repeterer prosessen)

### Induksjonseksempel

- Eksempel: bruker induksjon til å vise at $n!>2^n$ for vilkårlig heltall $n\geq 4$
    - Grunntilfellet: $n=4$, $P(4)=4!=24>16=2^4$
    - Induksjonshypotese (premiss): antar forrige element er sant ($P(n-1)$). Gir $(n-1)!>2^{n-1}$
    - Induksjonstrinn: antar $P(n-1)$, vil utlede $P(n)$
        - Bryter ned $n!$ og $2^n$ vha rekursjon
            - $n!=n\cdot(n-1)$
            - $2^n=2\cdot 2^{n-1}$
        - Antatt at $(n-1)!>2^{n-1}$ og vet at $n>2$. Derfor: $P(n-1)\to P(n)$

### Noen vanlige dekomponeringer
<img src="assets/dekomponeringExamples.png" alt='Some normal "dekomponering" examples' height="200px">
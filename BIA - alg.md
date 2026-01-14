# 📘 BIA: Skriptá na skúšku (Cheat Sheet)

## 🎯 1. Testovacie funkcie a Blind Search
Predtým, než začneš optimalizovať, musíš vedieť, čo optimalizuješ a s čím porovnávaš.

### Testovacie funkcie (Benchmarky)
Slúžia na otestovanie kvality algoritmu. Delíme ich podľa vlastností:
*   **Unimodálne (Jednovrcholové):** Majú len jedno globálne minimum, žiadne lokálne pasce. Ideálne na testovanie rýchlosti konvergencie (napr. *Sphere*).
*   **Multimodálne (Viacvrcholové):** Majú veľa lokálnych miním (pascí). Testujú schopnosť algoritmu "utiecť" z lokálneho optima (napr. *Rastrigin, Ackley, Schwefel, Griewangk*).
*   **Separabilné vs. Neseparabilné:** Či sa dajú premenné optimalizovať nezávisle (napr. *Rosenbrock* je neseparabilný – "banánové údolie", ťažké pre algoritmy).


## 2. Prehľad konkrétnych funkcií (Zoznam zo zadania)

### 🥣 Sphere (Guľa)
*   **Tvar:** Hladká miska.
*   **Typ:** Unimodálna, Separabilná, Spojitá.
*   **Obtiažnosť:** ⭐ (Najľahšia).
*   **Použitie:** Na ladenie algoritmu. Ak algoritmus nevie vyriešiť Sphere, je pokazený.
*   **Minimum:** V bode [0, 0, ... 0] je hodnota 0.

### 🍌 Rosenbrock (Banana function)
*   **Tvar:** Dlhé, úzke, zakrivené údolie v tvare paraboly.
*   **Typ:** Unimodálna (ale veľmi ťažká), **Neseparabilná**.
*   **Obtiažnosť:** ⭐⭐⭐⭐
*   **Zákernosť:** Nájsť údolie je ľahké. Ale nájsť najnižší bod v tom plochom údolí je ťažké (algoritmy tam blúdia pomaly sem a tam).

### 🥚 Rastrigin
*   **Tvar:** Ako Sphere, ale niekto po nej pobúchal kladivom (je celá zvlnená). Vyzerá ako "obal na vajíčka".
*   **Typ:** **Multimodálna**, Separabilná.
*   **Obtiažnosť:** ⭐⭐⭐
*   **Zákernosť:** Má obrovské množstvo lokálnych miním. Algoritmus ľahko spadne do nesprávnej jamky blízko stredu.
*   **Rovnica:** Obsahuje **kosínus** ($cos$), ktorý robí tie vlny.

### ⛺ Ackley
*   **Tvar:** Takmer úplne plochá rovina, ale uprostred je zrazu hlboká jama (ako kráter po meteorite alebo stan). Navyše je povrch jemne zvlnený.
*   **Typ:** **Multimodálna**.
*   **Obtiažnosť:** ⭐⭐⭐
*   **Zákernosť:** Keď si ďaleko od stredu, povrch je takmer rovný (gradient je skoro nulový), takže algoritmus "nevie, kam má ísť".

### 🎢 Schwefel
*   **Tvar:** Divoké hory a doliny.
*   **Typ:** **Multimodálna**.
*   **Obtiažnosť:** ⭐⭐⭐⭐
*   **Zákernosť:** Globálne minimum je **úplne na kraji** priestoru (v rohu), ďaleko od stredu. A druhé najlepšie minimum je úplne na opačnom konci.
*   **Rovnica:** Obsahuje sínus ($\sin(\sqrt{|x|})$).

### 🧊 Griewangk
*   **Tvar:** Podobné ako Rastrigin (drsný povrch), ale tie "hrbolčeky" sú jemnejšie. Pri pohľade z diaľky vyzerá ako Sphere.
*   **Zákernosť:** Čím viac dimenzií máš, tým je ľahšia (paradox).

---

## 🧠 Praktická otázka na skúšku

**Otázka:** *"Prečo testujeme algoritmy na funkcii Rastrigin a nie len na Sphere?"*

**Odpoveď:**
*   Pretože Sphere je príliš jednoduchá (Unimodálna). Vyriešil by ju aj Hill Climbing (horolezec).
*   Rastrigin je **Multimodálna** (má veľa pascí). Na nej zistíme, či má náš algoritmus (napr. DE alebo GA) dobrú **diverzitu** a či dokáže vyskočiť z lokálneho minima (Explorácia).
*   Ak by sme testovali len na Sphere, nevedeli by sme, či náš algoritmus nie je len "hlúpy Hill Climbing".

**Otázka:** *"Čo znamená, že je funkcia Rosenbrock neseparabilná?"*
**Odpoveď:**
*   Znamená to, že nemôžem nájsť najlepšie $x$ a potom hľadať najlepšie $y$. Musím ich meniť naraz, pretože sú navzájom previazané.

---

**Môžeme ísť ďalej?** Ďalšia téma zo zoznamu je **Hill Climbing** (Horolezec) a **Simulated Annealing** (Žíhanie). Chceš to spojiť? Sú to "bratia".

***

# 🕶️ Blind Search (Slepé hľadanie) - Cheat Sheet

**Čo to je:** Metóda optimalizácie bez akejkoľvek "inteligencie".
**Analógia:** Hľadáš kľúče v tmavej miestnosti. Nevidíš nič, nevieš, či si "teplo" alebo "zima". Len náhodne šmátraš rukami alebo systematicky prechádzaš centimeter po centimetri.

**Hlavný účel:** Slúži ako **Baseline (Základná čiara)**.
*   *Pravidlo:* Akýkoľvek BIA algoritmus **musí** byť lepší a rýchlejší ako Blind Search. Inak nemá zmysel ho používať.

---

## 🛠️ Dve hlavné techniky

### 1. Random Search (Náhodné hľadanie) 🎲
Generujeme riešenia úplne náhodne (Monte Carlo metóda).
*   **Postup:**
    1.  Vygeneruj náhodný bod $x$ v priestore.
    2.  Vypočítaj fitness $f(x)$.
    3.  Je lepší ako najlepší doteraz? $\to$ Ulož si ho.
    4.  Opakuj $N$-krát.
*   **Analógia:** Výsadkári skáču z lietadla v noci do hmly. Kto dopadne na najvyšší kopec, vyhráva. Nevedia sa navzájom navigovať.
*   **Vlastnosť:** Prekvapivo, vo vysokých dimenziách býva často **lepší** než Grid Search.

### 2. Grid Search (Mriežkové hľadanie) 📐
Systematicky prehľadávame priestor s určitým krokom (rozostupom).
*   **Postup:**
    1.  Rozdeľ priestor na mriežku (napr. každých 1.0 metra).
    2.  Prejdi **každý jeden bod** mriežky (cyklus v cykle).
    3.  Nájdi ten najlepší.
*   **Analógia:** Oranie poľa. Traktor ide riadok po riadku. Nevynechá nič.
*   **Problém:** Funguje len pre malé problémy (1D, 2D). Pri veľa dimenziách okamžite zlyháva.

---

## ⚠️ Prekliatie dimenzionality (Curse of Dimensionality)
Toto je **najdôležitejšia otázka**, ktorú môžeš dostať k Blind Search.

**Otázka:** *"Prečo nemôžem použiť Grid Search na problém so 100 dimenziami?"*

**Odpoveď:** Pretože počet bodov, ktoré musíš skontrolovať, rastie **exponenciálne**.

*   **1 Dimenzia (čiara):** Skúšam 10 bodov $\to$ 10 výpočtov. (Pohoda).
*   **2 Dimenzie (štvorec):** 10 bodov na osi X $\times$ 10 bodov na osi Y $\to$ $10^2 = 100$ výpočtov.
*   **3 Dimenzie (kocka):** $10 \times 10 \times 10 \to$ $10^3 = 1000$ výpočtov.
*   **100 Dimenzií:** $10^{100}$ výpočtov.
    *   *Pointa:* $10^{100}$ je viac, než je atómov vo vesmíre. Počítač by to rátal miliardy rokov.
    *   Preto potrebujeme BIA algoritmy (GA, DE, PSO), ktoré nepozerajú všetko, ale "hádajú" smer.

---

## ⚡ Výhody a Nevýhody (Na skúšku)

### ✅ Výhody
1.  **Jednoduchosť:** Naprogramuješ to na 3 riadky.
2.  **Paralelizácia:** Môžeš to spustiť na 1000 počítačoch naraz, nemusia spolu komunikovať.
3.  **Globálne optimum:** Ak (teoreticky) prehľadáš Grid Searchom nekonečne hustú mriežku, máš **100% istotu**, že nájdeš to najlepšie riešenie. (BIA algoritmy túto istotu nikdy nedávajú!).

### ❌ Nevýhody
1.  **Pomalosť:** Extrémne neefektívne.
2.  **Nepoužiteľnosť:** Pri zložitých problémoch (veľa dimenzií) je šanca na úspech mizivá.
3.  **Žiadna pamäť:** Algoritmus sa "neučí". Aj keď nájde super kopec, v ďalšom kroku hľadá úplne inde.

---

## 🎓 Praktická otázka od učiteľa

**Otázka:** *"Mám funkciu Sphere (jednoduchá jama). Ktorý algoritmus ju nájde rýchlejšie? Blind Search alebo Diferenciálna evolúcia?"*

**Tvoja odpoveď:**
*   S vysokou pravdepodobnosťou **Diferenciálna evolúcia (DE)**.
*   Pretože DE sa pozerá na sklon kopca a "padá" do jamy. Blind Search len strieľa naslepo.
*   *Výnimka:* Ak mám obrovské šťastie, Blind Search môže trafiť stred hneď v prvom kroku. Ale štatisticky je DE oveľa efektívnejšia.

**Otázka:** *"Kedy by ste použili Blind Search v praxi?"*
**Tvoja odpoveď:**
1.  Keď mám veľmi malý problém (napr. len 2 parametre).
2.  Keď chcem otestovať, či môj zložitý algoritmus vôbec funguje (porovnávacia metóda).
3.  Keď o probléme neviem absolútne nič a fitness funkcia je totálny chaos (White noise).
---

## 🏔️ 2. Algoritmy založené na jednom riešení (Trajectory Methods)
Pracujú len s **jedným** agentom/bodom v priestore, ktorý sa v každom kroku posúva.

Jasné, poďme sa pozrieť "pod kapotu". Toto je presne tá časť, ktorú musíš vedieť, ak máš napísať pseudokód alebo vysvetliť, ako sa ten bod v priestore reálne pohne.

Rozoberiem to na príklade **spojitého problému** (hľadáme čísla, nie mestá), lebo to je v BIA najčastejšie (napr. funkcia Sphere).

Predstav si, že máme problém s **2 dimenziami** ($x, y$).

---

# ⚙️ Hill Climbing: Detailný anatomický rozbor

Algoritmus sa točí v cykle. Tu je presne to, čo sa deje v každom kroku.

### 1. Fáza: Reprezentácia a Inicializácia (Len raz na začiatku)
Predtým, než začneme liezť, musíme "vyrobiť" horolezca.
*   **Jedinec (Riešenie):** Je to pole čísel (vektor).
    *   Napríklad: $X_{current} = [10.5, -4.2]$
*   **Inicializácia:** Tieto čísla vygenerujeme náhodne v rámci povolených hraníc (napr. od -100 do 100).
*   **Prvý výpočet:** Hneď mu vypočítame fitness. Povedzme, že $f(X_{current}) = 150$.

---

### 2. Fáza: Generovanie suseda (Perturbácia / Zmena)
Toto je to najdôležitejšie. Ako vznikne $X_{new}$?
Horolezec nemôže skociť na druhý koniec mapy. Musí urobiť **malý krok** do okolia.

**Matematicky (Pre každú dimenziu):**
$$x_{new} = x_{current} + \text{náhoda}$$

Kde "náhoda" je malé číslo z intervalu, napríklad $(-0.1, +0.1)$. Tomuto intervalu hovoríme **Step Size (Veľkosť kroku)** alebo $\epsilon$ (epsilon).

**Praktický výpočet:**
Máme bod: $[10.5, -4.2]$
Nastavíme maximálny krok: $0.5$

1.  **Dimenzia 1:** K $10.5$ pripočítame náhodné číslo medzi $-0.5$ a $0.5$.
    *   Padlo nám $+0.3$.
    *   Nové $x = 10.8$.
2.  **Dimenzia 2:** K $-4.2$ pripočítame náhodné číslo.
    *   Padlo nám $-0.1$.
    *   Nové $y = -4.3$.

**Výsledok:** Náš "Sused" (kandidát) je bod $X_{new} = [10.8, -4.3]$.

> **Pozor na hranice:** Tu sa musí skontrolovať, či sme nevyšli z mapy. Ak je povolené max 100 a nám vyšlo 101, musíme to orezať (clip) späť na 100.

---

### 3. Fáza: Evaluácia (Hodnotenie)
Teraz musíme zistiť, či sme stúpili na pevnejšiu zem alebo do blata.
Dosadíme nové súradnice do Fitness funkcie.

*   Máme $X_{new} = [10.8, -4.3]$.
*   Vypočítame $f(X_{new})$.
*   Povedzme, že výsledok je **140**.

---

### 4. Fáza: Selekcia (Rozhodovanie)
Porovnávame staré a nové fitness. V BIA zvyčajne **minimalizujeme** (hľadáme jamu).

*   Staré fitness ($X_{current}$): **150**
*   Nové fitness ($X_{new}$): **140**

**Logika rozhodovania (Greedy - Pažravá):**
*   Je $140 < 150$? **ÁNO (Je to lepšie).**
    *   **Akcia:** Prijímame zmenu.
    *   Prepíšeme pamäť: $X_{current}$ sa stáva $[10.8, -4.3]$ a jeho fitness je 140.
    *   Horolezec sa fyzicky posunul.

*   *Scenár B (Keby to vyšlo horšie):*
    *   Keby nové fitness bolo **160**.
    *   Je $160 < 150$? **NIE.**
    *   **Akcia:** Zahadzujeme $X_{new}$.
    *   $X_{current}$ ostáva nezmenené ($[10.5, -4.2]$).
    *   Horolezec ostáva stáť a v ďalšom kole skúsi iný náhodný krok iným smerom.

---

### 5. Fáza: Ukončenie (Termination)
Kedy to skončí?
Máme dve možnosti:
1.  **Počet iterácií:** Urobíme to 1000-krát a skončíme.
2.  **Konvergencia:** Ak sme napríklad 50-krát po sebe nenašli lepšieho suseda, prehlásime, že sme na vrchole (lokálnom optime) a končíme.

---

### 🧩 Variant pre Diskrétny problém (napr. TSP - Mestá)
Ak neriešiš čísla, ale poradie miest (Traveling Salesman), tak "Zmena" (Fáza 2) vyzerá inak. Nemôžeš k mestu "Košice" pripočítať číslo 0.5.

**Zmena (Perturbácia) v TSP:**
*   Máš trasu: `[Košice, Prešov, Poprad, Žilina]`
*   **Operácia Swap (Výmena):** Náhodne vyberieš dve mestá a vymeníš ich.
*   Nová trasa (Sused): `[Košice, Poprad, Prešov, Žilina]`
*   Zvyšok (Evaluácia, Selekcia) je rovnaký.

---

### 💡 Zhrnutie pre "Hlboké pochopenie"

Ak sa ťa učiteľ opýta **"Čo definuje správanie Hill Climbingu?"**, odpoveď je:
1.  **Spôsob generovania suseda (Neighborhood function):** Ak robíš príliš malé kroky (malé epsilon), ideš pomaly. Ak robíš veľké kroky, preskakuješ vrchol.
2.  **Pažravosť (Greediness):** Nikdy, za žiadnych okolností neprijme horšie riešenie. To je jeho najväčšia slabina (zasekne sa) aj sila (je rýchly).

Je tento detailný popis (hlavne tá Fáza 2 s pripočítaním náhody) to, čo si potreboval?


Paráda, ideme na to. **Simulated Annealing (SA)** alebo po slovensky **Simulované žíhanie**.

Je to priamy nástupca Hill Climbingu. Ak si pochopil HC, tak SA pochopíš za minútu, pretože je to len **Hill Climbing s jednou "chybou" navyše**, ktorá je tam naschvál.

***

# 🔥 Simulated Annealing (SA) - Cheat Sheet

**Čo to je:** Algoritmus inšpirovaný metalurgiou (spracovaním kovov).
**Analógia (Fyzikálna):** Keď kováč kuje meč, nahreje ho na vysokú teplotu. Atómy v kove vtedy šialene skáču (vysoká energia). Potom meč pomaly ochladzuje. Atómy sa postupne upokojujú a usporadúvajú sa do dokonalej kryštalickej mriežky (najpevnejší stav).
**Analógia (Opitý horolezec):**
*   Máme horolezca, ktorý chce zísť do najhlbšej doliny (Globálne minimum).
*   Na začiatku je "opitý" (Vysoká Teplota). Robí bláznivé kroky. Keď vidí kopec smerom nahor (zlé riešenie), aj tak tam občas vybehne, lebo mu to je jedno. **To mu pomôže vyskočiť z malej jamky.**
*   Časom triezvie (Teplota klesá). Začína byť opatrný. Ku koncu už prijíma len kroky, ktoré idú dole (k lepšiemu).

---

## ⚙️ Ako to funguje (Algoritmus)

Je to na 90 % zhodné s Hill Climbingom.
Rozdiel je len v bode **Selekcia** (keď sa rozhoduje, či prijme nový bod).

1.  **Inicializácia:** Vygeneruj bod $x$, nastav počiatočnú Teplotu $T$ (napr. 1000).
2.  **Cyklus (Kým $T > 0$):**
    *   Vygeneruj suseda $x_{new}$ (rovnako ako v HC - cez epsilon).
    *   Vypočítaj rozdiel fitness: $\Delta E = f(x_{new}) - f(x_{current})$.
    *   **Rozhodovanie:**
        1.  Je $x_{new}$ **LEPŠIE**? (Teda $\Delta E < 0$, ideme "dole")
            *   **ÁNO:** Prijmi ho VŽDY. ($x = x_{new}$).
        2.  Je $x_{new}$ **HORŠIE**? (Teda $\Delta E > 0$, ideme "hore")
            *   **Hill Climbing by povedal:** NIE, zahodiť!
            *   **Simulated Annealing povie:** Prijmi ho s pravdepodobnosťou $P$.
3.  **Ochladzovanie (Cooling):** Zníž teplotu $T$.
    *   Napr. $T = T \cdot 0.99$ (Geometrické chladenie).

---

## 🎲 Kľúčový vzorec (Metropolis Criterion)
Toto je jediná matematika, ktorú musíš vedieť.
Ak je riešenie horšie, pravdepodobnosť prijatia $P$ je:

$$P = e^{-\frac{\Delta E}{T}}$$
*(Kde $e$ je Eulerovo číslo cca 2.718)*

**Čo ten vzorec hovorí "sedliackym rozumom":**
1.  **Vysoká Teplota ($T$ je veľké):** Číslo v menovateli je veľké $\to$ exponent je blízky nule $\to$ $P$ je blízke 1 (100 %).
    *   *Výsledok:* Na začiatku prijímame skoro všetko, aj strašne zlé kroky. (Explorácia).
2.  **Nízka Teplota ($T$ je malé):** Číslo v menovateli je malé $\to$ exponent je veľké záporné číslo $\to$ $P$ je blízke 0.
    *   *Výsledok:* Na konci neprijímame skoro žiadne zhoršenie. Správa sa to ako Hill Climbing.
3.  **Malé zhoršenie ($\Delta E$ je malé):** Ľahšie prijmeme malé zhoršenie (malý kopček) ako obrovské zhoršenie (strmú stenu).

---

## ❄️ Cooling Schedule (Schéma ochladzovania)
Ako rýchlo znižujeme teplotu?
*   **Lineárne:** $T = T - k$ (Odčítame konštantu).
*   **Geometrické (Najčastejšie):** $T = T \cdot \alpha$ (Násobíme číslom napr. 0.9, 0.95, 0.99).
    *   Ak ochladzuješ **príliš rýchlo** (Quenching): Algoritmus "zamrzne" v lokálnom optime (nestihne z neho vyskočiť).
    *   Ak ochladzuješ **príliš pomaly**: Trvá to večnosť.

---

## 🎓 Praktické otázky na skúšku

**Otázka:** *"Aký je hlavný rozdiel medzi HC a SA?"*
**Odpoveď:** HC je greedy (nikdy neberie horšie). SA dokáže prijať aj horšie riešenie, aby uniklo z lokálneho optima.

**Otázka:** *"Čo sa stane, keď je Teplota = 0?"*
**Odpoveď:** Algoritmus sa zmení na čistý Hill Climbing. Prijíma už len lepšie riešenia.

**Otázka:** *"Prečo nepoužívame stále vysokú teplotu?"*
**Odpoveď:** Lebo vtedy sa algoritmus správa ako **Random Search** (náhodná prechádzka). Skáče hore-dole a nikdy nekonverguje (neustáli sa) v najlepšom bode. Musíme ho "upokojiť" znižovaním teploty.

---

### Chceš príklad "na papier"?
Predstav si, že sme v bode s Fitness **100**.
Vygenerujeme nový bod s Fitness **110** (čiže zhoršenie o 10).
Teplota $T = 100$.

1.  Je lepší? Nie.
2.  Máme ho prijať?
    *   Dosadíme do vzorca: $e^{-10 / 100} = e^{-0.1} \approx 0.90$
    *   Máme **90 % šancu**, že tento horší krok prijmeme.
    *   Algoritmus si "hodí kockou" (vygeneruje náhodné číslo 0-1). Ak padne menej ako 0.90, posunie sa tam.

---

## 🧬 3. Evolučné algoritmy (Population based)
Inšpirované Darwinovou teóriou. Pracujú s **populáciou** riešení naraz.


Nech sa páči. Toto je **finálna verzia skrípt pre Genetický Algoritmus na TSP**. Je v tom zhrnuté všetko, o čom sme hovorili – od kódovania až po ten cyklus generácií.

Skopíruj si to do svojich poznámok.

***

# 🧬 Genetic Algorithm (GA) pre TSP - Ultimate Cheat Sheet

**Čo to je:** Evolučný optimalizačný algoritmus inšpirovaný Darwinovou teóriou (prežitie najsilnejšieho), upravený pre kombinatorický problém (poradie miest).
**Cieľ:** Nájsť permutáciu miest s najkratšou celkovou vzdialenosťou.

---

## 1. Reprezentácia (Kódovanie)
Pri TSP nemôžeme použiť binárne (0101) ani reálne (float) čísla.
*   **Permutačné kódovanie:** Chromozóm je zoznam celých čísel (miest).
*   **Podmienka validity:** Každé mesto sa musí vyskytovať **práve raz**. Žiadne duplicity.
*   *Príklad:* `[1, 5, 3, 2, 4]` (Cesta: 1 $\to$ 5 $\to$ 3 $\to$ 2 $\to$ 4 $\to$ 1).

---

## 2. Fitness Funkcia
GA prirodzene hľadá maximum (najsilnejšieho jedinca), ale v TSP hľadáme minimum (najkratšiu cestu).
*   **Vzorec:** $$Fitness = \frac{1}{\text{Celková dĺžka trasy}}$$
*   *Logika:* Čím kratšia trasa (menšie číslo v menovateli), tým vyššia Fitness (lepšie riešenie).

---

## 3. Cyklus novej generácie (Algoritmus)

Veľkosť populácie ($NP$) musí ostať konštantná (napr. 100 jedincov).

### Krok A: Elitizmus (VIP vstupenka)
*   Skôr než začneme čokoľvek robiť, skopírujeme **najlepšieho jedinca** (alebo top 2) zo starej generácie priamo do novej.
*   *Dôvod:* Aby sme nikdy nestratili najlepšie doteraz nájdené riešenie (poistka proti degenerácii).

### Krok B: Selekcia (Výber rodičov)
Vyberáme 2 rodičov, ktorí splodia potomkov.
1.  **Tournament Selection (Turnaj):** Náhodne vyber $k$ jedincov (napr. 3). Porovnaj ich. Najlepší vyhráva a stáva sa rodičom. (Najčastejšie používané).
2.  **Roulette Wheel (Ruleta):** Pravdepodobnosť výberu je úmerná veľkosti fitness (koláčový graf).

### Krok C: Kríženie (Crossover) ⚠️
Klasické *One-point crossover* je zakázané (vytvorilo by duplicity miest).
*   **Používame:** **Order Crossover (OX1)**.
*   **Princíp:**
    1.  Vyber náhodný úsek (okno) z **Rodiča 1** a skopíruj ho do dieťaťa na rovnaké miesto.
    2.  Zvyšné prázdne miesta doplň mestami z **Rodiča 2**.
    3.  *Pravidlo:* Ber mestá z Rodiča 2 v poradí, v akom idú za sebou, ale **preskoč tie, ktoré už v dieťati sú**.

### Krok D: Mutácia (Mutation)
Slúži na udržanie diverzity a únik z lokálnych miním.
*   **Kedy:** Až po krížení, na hotovom dieťati.
*   **Pravdepodobnosť ($P_m$):** Veľmi nízka (napr. 1 %). Pre každé dieťa sa hodí "kockou" (0-1). Ak padne $< P_m$, vykoná sa zmena.
*   **Operátory:**
    1.  **Swap:** Výmena dvoch náhodných miest.
    2.  **Inversion (Obrátenie):** Vyberie sa úsek a zrkadlovo sa otočí. (Efektívne na rozmotanie "slučiek" v trase).

### Krok E: Náhrada
*   Deti postupne plnia novú populáciu.
*   Keď je nová populácia plná (100 ks), stará generácia sa kompletne zmaže.

---

## 🛑 Zastavovacie podmienky (Stopping Criteria)
Kedy cyklus skončí?
1.  **Max Generations:** Dosiahli sme pevný počet iterácií (napr. 1000).
2.  **Stagnácia:** Fitness najlepšieho jedinca sa nezlepšila posledných $X$ generácií.
3.  **Target Fitness:** Našli sme trasu kratšiu ako cieľová hodnota.

---

## 🆚 Kľúčové rozdiely: GA vs. DE (Na skúšku)

| Vlastnosť | Genetický Algoritmus (GA) | Diferenciálna Evolúcia (DE) |
| :--- | :--- | :--- |
| **Dátový typ** | Diskrétne (Mestá/Permutácie) | Spojité (Reálne čísla/Vektory) |
| **Mutácia** | Zriedkavá udalosť (1%), deje sa po krížení. Je to len poistka. | Hlavný motor pohybu ($F$), deje sa vždy na začiatku. |
| **Kríženie** | Primárny operátor (OX1), tvorí štruktúru riešenia. | Sekundárny ($CR$), mieša parametre. |
| **Selekcia** | Vyberáme rodičov (Turnaj/Ruleta). | Vyberáme, kto prežije (Súboj Dieťa vs. Rodič). |

---

## 🧠 Praktický príklad operátorov (Pre ťahák)

**Rodič 1:** `[1, 2, 3, 4, 5, 6]` | **Rodič 2:** `[6, 5, 4, 3, 2, 1]`

**1. Kríženie (OX1):** Fixujeme stred `[3, 4]` z R1.
*   Dopĺňame z R2 (od konca rezu): `2, 1, 6, 5`.
*   Výsledok (Wrap-around): `[6, 5, 3, 4, 2, 1]`

**2. Mutácia (Swap):**
*   Vstup: `[1, 2, 3, 4, 5, 6]`
*   Swap(2, 5): `[1, 5, 3, 4, 2, 6]`

**3. Mutácia (Inversion):**
*   Vstup: `[1, | 2, 3, 4, 5 | 6]`
*   Invert: `[1, | 5, 4, 3, 2 | 6]`

***

# 🧬 Differential Evolution (DE) - Cheat Sheet

**Čo to je:** Evolučný algoritmus na optimalizáciu spojitých funkcií (čísla, vektory).
**Analógia:** "Tuning áut" – Skladáš nové auto tak, že vezmeš staré a vymeníš na ňom pár súčiastok podľa rozdielov medzi inými autami v garáži.

---

## 🔑 Kľúčové parametre
*   **$NP$ (Population Size):** Počet jedincov v populácii (napr. 50).
*   **$D$ (Dimensions):** Počet premenných problému (dĺžka vektora).
*   **$F$ (Scaling Factor):** Váha mutácie (zvyčajne $0.5$ až $0.9$). Určuje dĺžku kroku ("tlmič").
*   **$CR$ (Crossover Rate):** Pravdepodobnosť kríženia ($0.0$ až $1.0$). Určuje, koľko génov sa vymení.
*   **$G$ (Generations):** Počet opakovaní cyklu.

---

## 🔄 5 Fáz Algoritmu (Cyklus)

Algoritmus prechádza celú populáciu jedinca po jedincovi (Target vector $x_i$).

### 1. Inicializácia (Initialization)
*   **Kedy:** Len raz na začiatku ($G=0$).
*   **Čo:** Vygenerujeme $NP$ náhodných jedincov v celom prehľadávanom priestore.
*   **Výstup:** Pôvodná tabuľka náhodných riešení.

### 2. Mutácia (Mutation)
*   **Cieľ:** Vytvoriť **Mutant vektor ($v$)**.
*   **Princíp:** Pre aktuálneho jedinca ($x_i$) vyberieme z populácie 3 iných **náhodných** jedincov ($r1, r2, r3$).
*   **Vzorec (základný):**
    $$v = r1 + F \cdot (r2 - r3)$$
*   **Poznámka:** Počítame to pre každú dimenziu zvlášť (vektorová matematika). $F$ škáluje rozdiel ("určuje, ako agresívny je skok").

### 3. Kríženie (Crossover)
*   **Cieľ:** Vytvoriť **Pokusný vektor ($u$)** – Trial Vector.
*   **Princíp:** Miešame starého otca ($x_i$) a nového Mutanta ($v$).
*   **Mechanizmus:** Pre každú dimenziu $j$ vygenerujeme náhodné číslo $rand(0, 1)$.
    *   Ak $rand \le CR$ $\to$ Beriem z Mutanta ($v$).
    *   Ak $rand > CR$ $\to$ Beriem z Otca ($x_i$).
*   **Poistka:** Vždy sa garantuje výmena aspoň 1 dimenzie (náhodný index $j_{rand}$), aby kópia nebola 1:1.

### 4. Evaluácia (Evaluation)
*   **Cieľ:** Zistiť kvalitu nového riešenia.
*   **Akcia 1 (Boundary Check):** Ak je niektorá hodnota v $u$ mimo hraníc, orežeme ju (clip) alebo odrazíme späť.
*   **Akcia 2 (Fitness):** Dosadíme $u$ do fitness funkcie a vypočítame skóre: $cost = f(u)$.

### 5. Selekcia (Selection)
*   **Cieľ:** Rozhodnúť, kto prežije do ďalšej generácie.
*   **Princíp:** "One-to-One Survival of the Fittest" (Súboj).
*   **Podmienka:**
    *   Ak $f(u) \le f(x_i)$ (Pokusný je lepší alebo rovnaký) $\to$ **Nahrádza otca**.
    *   Inak $\to$ **Otec ostáva**.
*   *Poznámka:* DE je "Greedy" (pažravá) – nikdy neprijme horšie riešenie.

---

## 🧠 Stratégie Mutácie (DE / x / y / z)

Názov stratégie určuje, aký vzorec použijeme v kroku Mutácia.
Formát: **DE / Kto je základ / Počet rozdielových vektorů / Typ kríženia**

### 1. DE / rand / 1 / bin (Klasika - Explorácia)
*   **Vzorec:** $v = r1 + F \cdot (r2 - r3)$
*   **Základ:** Náhodný jedinec ($r1$).
*   **Výhoda:** Vysoká diverzita, robustné, dobré pre globálne hľadanie.
*   **Nevýhoda:** Pomalšia konvergencia.

### 2. DE / best / 1 / bin (Rýchlik - Exploitácia)
*   **Vzorec:** $v = x_{best} + F \cdot (r1 - r2)$
*   **Základ:** Najlepší jedinec v populácii ($x_{best}$).
*   **Výhoda:** Veľmi rýchla konvergencia k riešeniu.
*   **Nevýhoda:** Riziko predčasnej konvergencie (uviaznutie v lokálnom optime), strata diverzity.

---

## ⚡ Rýchle otázky a odpovede (Na skúšku)

*   **Prečo je dôležité F?**
    *   Reguluje veľkosť kroku mutácie. Veľké $F$ = skáčeme ďaleko (explorácia). Malé $F$ = ladíme detaily (exploitácia).
*   **Na čo slúži CR?**
    *   Riadi, ako veľmi sa nový jedinec líši od rodiča. Vyššie $CR$ = väčšia zmena (viac génov z mutanta).
*   **Čo je to diverzita v DE?**
    *   Rozmanitosť populácie. Ak sú vektory $r1, r2, r3$ blízko seba, rozdiel $(r2-r3)$ je malý $\to$ mutácia robí malé kroky. Ak sú ďaleko, robí veľké kroky. **DE sa sama adaptuje podľa rozptylu populácie!**
*   **Rozdiel oproti Genetickému algoritmu?**
    *   GA: Mutácia je malá náhodná zmena.
    *   DE: Mutácia je riadená rozdielmi v populácii (vektorová).
    *   DE je jednoduchšia na implementáciu a často lepšia na spojité funkcie.

---

## 🐝 4. Rojová inteligencia (Swarm Intelligence)
Inšpirované správaním zvierat (kolektívna inteligencia).


Nech sa páči. Toto je **finálny Cheat Sheet pre PSO**.
Je v ňom zahrnutá teória, vzorce aj tá stratégia s meniacim sa $w$, ktorú si tak dobre pochopil.

Skopíruj si to do skrípt.

***

# 🐝 Particle Swarm Optimization (PSO) - Ultimate Cheat Sheet

**Čo to je:** Algoritmus rojovej inteligencie (Swarm Intelligence) pre spojitú optimalizáciu (hľadanie čísel/súradníc).
**Inšpirácia:** Kŕdeľ vtákov alebo húf rýb hľadajúcich potravu.
**Analógia:** Vtáky v tme nevidia jedlo, ale vedia, ako sú od neho ďaleko. Každý vták letí tam, kde on sám našiel niečo dobré (pamäť), ale zároveň ho priťahuje miesto, kde našiel potravu najúspešnejší vták z kŕdľa (napodobňovanie).

---

## 🔑 Kľúčové pojmy
*   **Particle (Častica):** Jeden agent (riešenie). Má polohu $x$ a rýchlosť $v$.
*   **pBest (Personal Best):** Najlepšia pozícia, kde sa táto konkrétna častica kedy vyskytla (Osobná pamäť).
*   **gBest (Global Best):** Najlepšia pozícia, ktorú objavil **ktokoľvek** z celého kŕdľa (Zdieľaná vedomosť).

---

## ⚙️ Matematika pohybu (Jadro algoritmu)
Toto sa počíta v každom kroku pre **každú dimenziu** zvlášť.

### 1. Aktualizácia Rýchlosti ($v_{new}$)
Vektor rýchlosti sa skladá z 3 zložiek:
$$v_{new} = \underbrace{w \cdot v_{old}}_{\text{Inertia}} + \underbrace{c_1 \cdot r_1 \cdot (pBest - x)}_{\text{Cognitive}} + \underbrace{c_2 \cdot r_2 \cdot (gBest - x)}_{\text{Social}}$$

*   **Inertia (Zotrvačnosť):** "Letím tam, kam som letel doteraz." ($w$ = váha zotrvačnosti).
*   **Cognitive (Kognitívna):** "Vraciam sa k svojmu najlepšiemu nálezu." ($c_1$ = váha nostalgie/egoizmu).
*   **Social (Sociálna):** "Letím k lídrovi stáda." ($c_2$ = váha stádovosti).
*   **$r_1, r_2$:** Náhodné čísla $(0, 1)$. Slúžia ako "vietor", zavádzajú chaos, aby častica neletela roboticky rovno, ale kľučkovala.

### 2. Aktualizácia Polohy ($x_{new}$)
Keď máme rýchlosť, pohneme sa:
$$x_{new} = x_{old} + v_{new}$$

---

## 🧠 Stratégia Inertia Weight ($w$)
Parameter $w$ riadi rovnováhu medzi hľadaním a ladením.

*   **Vysoké $w$ (napr. 0.9):** Častica ťažko mení smer $\to$ lieta rýchlo cez celú mapu $\to$ **Explorácia**.
*   **Nízke $w$ (napr. 0.4):** Častica nemá energiu, brzdí $\to$ motá sa len lokálne $\to$ **Exploitácia**.

### 🔥 LDIW (Linear Decreasing Inertia Weight)
V praxi sa $w$ nemení konštantne, ale dynamicky klesá počas behu algoritmu.
*   **Začiatok:** $w=0.9$ (Prehľadaj celé Tatry, nájdi dolinu).
*   **Koniec:** $w=0.4$ (Pristáň presne na tom kameni v doline).
*   *Vzorec v kóde:* `w = w_max - (w_max - w_min) * (iteracia / max_iter)`

---

## 🔄 Algoritmus (Cyklus)

1.  **Inicializácia:**
    *   Vygeneruj $N$ častíc s náhodnou polohou $x$ a rýchlosťou $v$.
    *   Fitness každej častice ulož ako jej $pBest$.
    *   Najlepšiu zo všetkých označ ako $gBest$.
2.  **Iteračný cyklus:**
    *   Pre každú časticu:
        1.  Vypočítaj **novú rýchlosť $v$** (podľa vzorca).
            *   *Wall detection:* Ak narazí do steny, odraz ju alebo zastav.
        2.  Vypočítaj **novú polohu $x$**.
        3.  Vypočítaj **Fitness $f(x)$**.
        4.  **Update pBest:** Ak je $f(x)$ lepšie ako $pBest$, prepíš ho.
        5.  **Update gBest:** Ak je $f(x)$ lepšie ako celkové $gBest$, prepíš ho.
3.  **Koniec:** Keď prejdú generácie, vráť $gBest$.

---

## 🆚 PSO vs. Genetický Algoritmus (GA)

| Vlastnosť | PSO | GA |
| :--- | :--- | :--- |
| **Pamäť** | **ÁNO ($pBest$)**. Častica vie, kde bola. | **NIE**. Jedinec nemá pamäť (okrem elít). |
| **Zdieľanie info** | Všetci vedia o $gBest$ (vysielačka). | Info sa šíri len medzi pármi pri krížení. |
| **Pohyb** | Spojitý let (úprava rýchlosti). | Diskrétne skoky (Kríženie/Mutácia). |
| **Populácia** | Tie isté častice od začiatku do konca. | Rodičia umierajú, rodia sa nové deti. |

---

## 🎓 Praktické otázky (FAQ)

*   **Čo ak dám $w=0$?**
    *   Častica stratí hybnosť. Bude len skákať medzi pBest a gBest. Ľahko uviazne.
*   **Čo ak dám $c_1=0$ (žiadne pBest)?**
    *   "Social-only" model. Všetci sa bezhlavo vrhnú na gBest. Rýchla konvergencia, ale obrovské riziko uviaznutia v lokálnom optime (strata diverzity).
*   **Čo ak dám $c_2=0$ (žiadne gBest)?**
    *   "Cognitive-only" model. Častice sa ignorujú. Každá si hľadá svoje. Je to ako mať 50 nezávislých Hill Climberov.

***


**Áno, presne tak to je!** Pochopil si to úplne správne.

Pri stratégii **All-To-All** nebežíš postupne "štafetu" (že by si dobehol k prvému, ostal tam a odtiaľ bežal k druhému).

Funguje to takto (Predstav si, že si Jedinec č. 1):

1.  **Stojíš na štarte** (svojej aktuálnej pozícii).
2.  **Simulácia 1:** Pozrieš sa na Jedinca 2. Prebehneš si cvične celú cestu k nemu (skenuješ fitness po krokoch). Nájdeš na tej ceste super bod A. Zapamätáš si ho.
3.  **Vrátiš sa na štart** (v hlave/virtuálne).
4.  **Simulácia 2:** Pozrieš sa na Jedinca 3. Prebehneš si cestu k nemu. Nájdeš na tej ceste super bod B. Zapamätáš si ho.
5.  ... takto to zopakuješ pre všetkých 99 ostatných kolegov.
6.  **Finále:** Máš v denníčku 99 "najlepších bodov" z každej cesty. Pozrieš sa, ktorý z nich je **absolútne najlepší** (má najlepšie fitness zo všetkých).
7.  **Pohyb:** Až teraz sa fyzicky presunieš na ten jeden víťazný bod.

**Preto je to také náročné na výpočet.**
Jeden jedinec musí urobiť 99 kompletných behov (a v každom behu napr. 20 krokov/výpočtov fitness), len aby sa **raz** pohol.

---

Keďže SOMA máš zmáknutú, tu je **SOMA Cheat Sheet**, aby si to mal v skriptách kompletné, a potom môžeme ísť na tie Mravce (ACO).

***

# 🐺 SOMA (Self-Organizing Migration Algorithm) - Cheat Sheet

**Čo to je:** Algoritmus sociálnej inteligencie, inšpirovaný správaním svorky šeliem pri love.
**Stratégia:** **All-To-One** (Všetci bežia k Vodcovi).
**Unikátnosť:** Jedinec neskáče priamo do cieľa. Prejde celú trajektóriu (cestu) k lídrovi, "ochutnáva" fitness v každom kroku a nakoniec sa vráti na to najlepšie miesto, ktoré cestou našiel.

---

## 🔑 Kľúčové pojmy
*   **Migrácia:** To isté ako Generácia. Jeden cyklus, kedy sa celá populácia pohne.
*   **Leader (Vodca):** Jedinec s najlepším fitness v aktuálnej migrácii. V stratégii *All-To-One* sa nehýbe, slúži ako maják pre ostatných.
*   **PathLength:** Dĺžka cesty (typicky $> 1$, napr. 3.0). Určuje, že jedinec má lídra nielen dobehnúť, ale aj predbehnúť (**Overshooting**), aby preskúmal priestor za ním.
*   **Step:** Dĺžka kroku vzorkovania (napr. 0.11). Určuje, ako husto jedinec "skenuje" cestu.
*   **PRT (Perturbation):** Parameter, ktorý určuje pravdepodobnosť zmeny dimenzie. Slúži na tvorbu oblúkov (kľučkovanie) namiesto priameho pohybu.

---

## ⚙️ Algoritmus (Pohyb jedinca)

V každej migrácii sa pre každého jedinca (okrem Leadera) vykoná tento proces:

1.  **PRT Vektor:**
    *   Pre každú dimenziu sa vygeneruje náhodné číslo.
    *   Ak $rand < PRT \to 1$ (Hýb sa).
    *   Ak $rand > PRT \to 0$ (Stoj).
    *   *Výsledok:* Vektor núl a jednotiek, ktorý hovorí, v ktorých osiach sa pohneme.

2.  **Beh po trajektórii (Sampling):**
    *   Začíname na $t = 0$ (Start).
    *   Postupne zvyšujeme $t$ o $Step$ (0.11, 0.22, ...), až kým nedosiahneme $PathLength$ (3.0).
    *   V každom kroku vypočítame novú polohu:
        $$X_{new} = X_{start} + (X_{leader} - X_{start}) \cdot t \cdot PRTVector$$
    *   Vypočítame Fitness tohto bodu.
    *   Ak je fitness lepšie ako najlepšie zatiaľ nájdené na tejto ceste, uložíme si ho.

3.  **Finálny presun:**
    *   Keď jedinec dobehne na koniec cesty ($t=3.0$), pozrie sa do pamäte: *"Kde to bolo najlepšie?"*
    *   Presunie sa na túto najlepšiu súradnicu.

---

## 🧠 Stratégie Migrácie (Kto beží kam?)

1.  **All-To-One (Štandard):**
    *   Všetci bežia k Lídrovi.
    *   Rýchle, dobrá konvergencia.
2.  **All-To-All (Chaos):**
    *   Každý beží ku každému (simuluje cesty ku všetkým kolegom a vyberie tú najlepšiu).
    *   Extrémna explorácia, ale výpočtovo veľmi náročné (pomalé).
3.  **All-To-Random:**
    *   Každý beží k náhodne vybranému jedincovi.
    *   Udržuje diverzitu.

---

## 🎓 Otázky na skúšku

*   **Aký je rozdiel medzi SOMA a PSO?**
    *   PSO robí jeden skok v každej generácii (na základe rýchlosti).
    *   SOMA robí "vzorkovanie" celej cesty (sériu testov) a vyberie najlepší bod z tejto cesty.
*   **Prečo Leader stojí?**
    *   Líder je referenčný bod. Ak by sa hýbal aj on, ostatní by bežali za pohyblivým cieľom, čo by bolo chaotické. Líder sa pohne až v ďalšej migrácii, ak ho niekto iný predbehne vo fitness.
*   **Čo robí PRT Vektor?**
    *   Zabezpečuje, že pohyb nie je priamočiary, ale prebieha po krivkách (niektoré dimenzie sa menia, iné stoja). Zvyšuje to šancu nájsť optimum mimo hlavnej uhlopriečky.

***
Nech sa páči. Tu je kompletný **ACO Cheat Sheet** pripravený do tvojich skrípt. Je tam zhrnuté všetko dôležité, vrátane vzorcov, ktoré učitelia radi vidia.

***

# 🐜 Ant Colony Optimization (ACO) - Ultimate Cheat Sheet

**Čo to je:** Konštruktívny algoritmus rojovej inteligencie inšpirovaný mravcami.
**Aplikácia:** Primárne pre diskrétne problémy na grafoch (TSP - Obchodný cestujúci, Logistika, Siete).
**Analógia:**
*   Mravce hľadajú cestu od hniezda k jedlu.
*   Sú slepé, komunikujú cez chemickú stopu – **Feromón ($\tau$)**.
*   **Princíp spätnej väzby:** Kratšia cesta $\to$ Mravec sa vráti skôr $\to$ Zanechá čerstvú stopu skôr $\to$ Cesta vonia silnejšie $\to$ Ostatní sa pridajú.

---

## 🔑 Kľúčové parametre
*   **$\tau_{ij}$ (Tau):** Množstvo feromónu na hrane medzi mestom $i$ a $j$ (Pamäť kolónie).
*   **$\eta_{ij}$ (Eta):** Heuristická informácia (Viditeľnosť). Pre TSP je to prevrátená hodnota vzdialenosti: $\eta = 1 / d_{ij}$. (Čím bližšie, tým lepšie).
*   **$\alpha$ (Alpha):** Váha feromónu (Ako veľmi mravec verí "davu").
*   **$\beta$ (Beta):** Váha heuristiky (Ako veľmi mravec verí "vlastným očiam").
*   **$\rho$ (Rho):** Koeficient vyparovania ($0 < \rho < 1$).
*   **$Q$:** Konštanta pre silu feromónu (zvyčajne 1).

---

## ⚙️ Matematika (Jadro)

### 1. Rozhodovanie (Pravdepodobnosť prechodu)
Mravec stojí v meste $i$ a vyberá si mesto $j$ (ktoré ešte nenavštívil).
Pravdepodobnosť, že pôjde práve tam:

$$P_{ij} = \frac{(\tau_{ij})^\alpha \cdot (\eta_{ij})^\beta}{\sum (\text{všetky dostupné cesty})}$$

*   **Vysvetlenie:** Mravec kombinuje vôňu ($\tau$) a vzdialenosť ($\eta$).
    *   Ak $\alpha$ je veľké $\to$ Mravec ignoruje vzdialenosť a ide len po najvoňavejšej ceste (Riziko uviaznutia).
    *   Ak $\beta$ je veľké $\to$ Mravec ignoruje feromón a ide vždy len do najbližšieho mesta (Greedy algoritmus).

### 2. Vyparovanie (Evaporation)
Na konci cyklu sa feromón na **všetkých** cestách zníži.
$$\tau_{new} = (1 - \rho) \cdot \tau_{old}$$
*   **Cieľ:** Zabrániť, aby sa feromón hromadil donekonečna. Umožňuje algoritmu "zabudnúť" staré zlé cesty a skúšať nové.

### 3. Ukladanie feromónu (Deposit)
Každý mravec prejde svoju trasu a pridá na ňu feromón.
$$\tau_{new} = \tau_{old} + \Delta \tau$$
Kde prídavok $\Delta \tau$ je:
$$\Delta \tau = \frac{Q}{\text{Dĺžka celej trasy ($L$)}}$$
*   **Cieľ:** Kratšia trasa (malé $L$) $\to$ Väčšie číslo $\to$ Viac pridaného feromónu.

---

## 🔄 Algoritmus (Cyklus)

1.  **Inicializácia:**
    *   Na všetky hrany grafu nanesieme malé počiatočné množstvo feromónu (napr. $\tau_0 = 0.1$).
2.  **Generácia (Iterácia):**
    *   **Krok A (Konštrukcia):** Vypustíme $N$ mravcov (napr. do náhodných miest).
    *   **Krok B (Pohyb):** Každý mravec si postaví kompletnú trasu (mesto po meste) pomocou vzorca pravdepodobnosti.
    *   **Krok C (Vyparovanie):** Globálne znížime feromón na celom grafe ($(1-\rho)$).
    *   **Krok D (Deposit):** Každý mravec prejde svoju trasu a pridá feromón podľa toho, aká bola krátka ($Q/L$).
3.  **Koniec:** Opakujeme X-krát alebo kým mravce nechodia stále po tej istej trase (stagnácia).

---

## 🆚 ACO vs. Genetický Algoritmus (TSP)

| Vlastnosť | **Ant Colony (ACO)** | **Genetický Algoritmus (GA)** |
| :--- | :--- | :--- |
| **Prístup** | **Konštruktívny.** Trasa sa stavia od nuly v každom kroku. | **Evolučný.** Hotové trasy sa upravujú a krížia. |
| **Pamäť** | Feromónová matica (zdieľaná pamäť v prostredí). | Génová populácia (pamäť v jedincoch). |
| **Spätná väzba** | Pozitívna (viac feromónu láka viac mravcov). | Selekcia (lepší prežijú). |
| **Vhodnosť** | Najlepšie na grafy a hľadanie ciest. | Univerzálne, ale potrebuje špeciálne operátory (OX1). |

---

## 🎓 Praktické otázky (FAQ)

*   **Prečo mravce na začiatku nechodia rovnako?**
    *   Pretože na začiatku je feromón všade rovnaký, takže sa rozhodujú podľa vzdialenosti ($\eta$) a **náhody** (pravdepodobnostný výber). Tá náhoda zabezpečí prvotnú exploráciu.
*   **Čo sa stane, ak je $\rho$ (vyparovanie) príliš malé (blízke 0)?**
    *   Feromón takmer nemizne. Staré (zlé) cesty zostanú voňavé navždy. Algoritmus sa "zahltí" a nevie nájsť novú, lepšiu cestu.
*   **Čo sa stane, ak je $\rho$ príliš veľké (blízke 1)?**
    *   Feromón zmizne okamžite. Mravce sa nestihnú "dohodnúť" na spoločnej ceste. Správa sa to ako náhodné hľadanie.

***

Nie úplne. Tu ťa musím trochu opraviť, pretože si to pletieš s PSO alebo SOMA (All-To-One).

V algoritme svetlušiek (Firefly) nebežíš len za tým **jedným najsilnejším** (globálnym lídrom).
Tam platí pravidlo: **"Porovnávam sa s KAŽDÝM."**

### ⚠️ Rozdiel v logike (Chyták)

*   **PSO:** Pozriem sa, kde je **gBest** (najlepší z celého kŕdľa) a letím tam. (Ignorujem ostatných priemerných).
*   **Firefly:** Pozriem sa na všetkých kolegov okolo seba.
    *   Je Fero jasnejší? Pohnem sa k Ferovi.
    *   Je Jožo jasnejší? Pohnem sa aj k Jožovi.
    *   Je Jana tmavšia? Janu ignorujem.

Teda v jednej iterácii sa jedna svetluška môže pohnúť viackrát (smerom k viacerým lepším jedincom), alebo sa pohne smerom k "výslednici" týchto síl.

---

### 🔄 Priebeh algoritmu (Krok za krokom)

Tu je presný postup, ako to beží v kóde (to sa volá **Dvojitý cyklus**):

1.  **Inicializácia:**
    *   Máš $N$ svetlušiek.
    *   Nastavíš parametre $\beta_0$ (napr. 1.0), $\gamma$ (napr. 1.0), $\alpha$ (napr. 0.2).
    *   Vypočítaš im Fitness (Intenzitu $I$).

2.  **Hlavný cyklus (Iterácie):**
    *   **Vonkajší cyklus (Ty):** Pre každú svetlušku $i$ (od 1 do $N$).
        *   **Vnútorný cyklus (Ostatní):** Pre každú svetlušku $j$ (od 1 do $N$).
            *   **Podmienka:** Je svetluška $j$ jasnejšia ako $i$? ($I_j > I_i$)
                *   **ÁNO:**
                    1.  Vypočítaj vzdialenosť $r_{ij}$.
                    2.  Vypočítaj atraktivitu $\beta = \beta_0 \cdot e^{-\gamma r^2}$.
                    3.  **Pohni svetlušku $i$ smerom k svetluške $j$** (podľa rovnice pohybu).
                *   **NIE:** Nerob nič (ignoruj ju).
    *   **Prepočet:** Po pohybe všetkých svetlušiek vypočítaj nové Intenzity (Fitness).
    *   **Zoraď:** Nájdi aktuálne najlepšiu (pre info).

3.  **Koniec:** Opakuj, kým neprejdú generácie.

---

Takže: **Nie je to "Všetci na jedného" (All-To-One). Je to skôr "Každý za každým lepším".**

Tu máš finálny Cheat Sheet pre Svetlušky do skrípt:

***

# ✨ Firefly Algorithm (FA) - Ultimate Cheat Sheet

**Čo to je:** Algoritmus inšpirovaný blikaním svetlušiek.
**Kľúčová vlastnosť:** Multimodálna optimalizácia (vie nájsť viacero vrcholov naraz, nielen jeden, vďaka tomu, že svetlo slabne so vzdialenosťou).

---

## 🔑 3 Zlaté pravidlá
1.  **Unisex:** Všetky svetlušky sa priťahujú navzájom bez ohľadu na pohlavie.
2.  **Atraktivita $\propto$ Jas:** Menej jasná svetluška sa vždy hýbe smerom k jasnejšej.
3.  **Absorpcia:** Jas (a teda atraktivita) klesá so zväčšujúcou sa vzdialenosťou.

---

## 🎛️ Parametre (Ovládanie)

*   **$\beta_0$ (Base Attractiveness):** Sila príťažlivosti pri zdroji (vzdialenosť 0). Zvyčajne $1.0$.
*   **$\gamma$ (Gamma - Absorption):** Koeficient pohlcovania svetla.
    *   $\gamma \to 0$: Svetlo neslabne (správa sa ako PSO, vidia sa navždy).
    *   $\gamma \to \infty$: Svetlo zmizne hneď (správa sa ako Random Search, nikto nikoho nevidí).
*   **$\alpha$ (Alpha):** Miera náhodnosti pohybu (Randomization). Zabezpečuje exploráciu.

---

## 🏃 Rovnica Pohybu (The Equation)
Ak je svetluška $j$ jasnejšia ako $i$, svetluška $i$ sa pohne podľa:

$$x_{i}^{new} = \underbrace{x_{i}}_{\text{Stará poloha}} + \underbrace{\beta_0 \cdot e^{-\gamma r_{ij}^2} \cdot (x_j - x_i)}_{\text{Príťažlivosť (Attraction)}} + \underbrace{\alpha \cdot (\text{rand} - 0.5)}_{\text{Náhoda (Random)}}$$

*   **Vysvetlenie:**
    *   Sčítavam svoju polohu + vektor k lepšiemu kolegovi (tlmený vzdialenosťou) + malý náhodný šum.

---

## 🔄 Algoritmus (Dvojitý cyklus)

Dôležité: Každá svetluška sa porovnáva s každou inou. Zložitosť je $O(N^2)$.

1.  **Inicializácia:** Vygeneruj $N$ svetlušiek.
2.  **Cyklus Generácií:**
    *   `For i = 1 to N` (Ja):
        *   `For j = 1 to N` (Ostatní):
            *   **Ak $Intenzita_j > Intenzita_i$:**
                *   Vypočítaj vzdialenosť $r$.
                *   Pohni svetlušku $i$ smerom k $j$.
                *   *(Ak nenájdem nikoho lepšieho, pohnem sa náhodne).*
    *   Prepočítaj Fitness všetkým posunutým svetluškám.
    *   Zníž parameter $\alpha$ (voliteľné, pre ustálenie).

---

## 🎓 Otázky na skúšku

*   **Aký je rozdiel medzi PSO a FA?**
    *   V PSO je "globálny pohľad" (všetci vidia gBest). Svetlušky majú "lokálny pohľad" (vidia len tých, čo sú blízko, lebo svetlo z diaľky k nim nedoletí kvôli $\gamma$).
    *   Preto je FA lepší na hľadanie viacerých lokálnych miním (Multimodal), kým PSO rýchlo konverguje k jednému bodu.
*   **Čo sa stane, ak Gamma = 0?**
    *   Atraktivita je konštantná ($\beta = \beta_0$). Svetlo neslabne. Algoritmus sa zmení na zjednodušenú verziu PSO.

---

## 🏫 5. Ostatné a Moderné heuristiky

### Teaching-Learning Based Optimization (TLBO)
*   **Analógia:** Trieda žiakov a učiteľ.
*   **Princíp:** Nemá parametre ako mutácia/kríženie! Má dve fázy:
    1.  **Teacher Phase:** Učiteľ (najlepší jedinec) sa snaží posunúť priemer triedy (ostatných) smerom k sebe (zvyšuje vedomosti).
    2.  **Learner Phase:** Žiaci sa učia navzájom (interakcia dvoch náhodných žiakov). Ak vie kolega viac, posuniem sa k nemu.
*   **Výhody:** "Parameter-less" algoritmus (netreba ladiť parametre), veľmi efektívny.

---

## ⚖️ 6. Multi-objective optimization (Viacero cieľov)
Čo ak chceš auto, ktoré je **najrýchlejšie** A ZÁROVEŇ **najlacnejšie**? Tieto ciele idú proti sebe.

### NSGA-II (Non-dominated Sorting Genetic Algorithm II)
*   **Cieľ:** Nenájde jedno riešenie, ale **Pareto Front** (množinu kompromisných riešení).
    *   *Dominancia:* Riešenie A dominuje B, ak je A lepšie vo všetkých kritériách (alebo aspoň v jednom lepšie a v ostatných rovnaké).
*   **Kľúčové mechanizmy:**
    1.  **Fast Non-dominated Sorting:** Rozdelí populáciu do "vrstiev" (frontov). 1. front sú riešenia, ktoré nikto nedominuje (najlepšie).
    2.  **Crowding Distance (Vzdialenosť v dave):** Ak máme dve riešenia v rovnakom fronte, uprednostníme to, ktoré je v "prázdnejšej" oblasti (aby sme mali rozmanité riešenia, nie všetky na kope).
*   **Výstup:** Graf (krivka), z ktorého si užívateľ vyberie kompromis.

***

# 🎓 Ako sa to učiť (Stratégia)

1.  **Základ:** Pochop rozdiel medzi *Exploráciou* (hľadám v celom priestore - lietam náhodne) a *Exploitáciou* (našiel som kopec, idem presne na vrchol). Každý algoritmus to rieši inak.
    *   *PSO:* Inertia weight to mení.
    *   *SA:* Teplota to mení.
2.  **Prax:** Skús si pre každý algoritmus predstaviť, ako sa zmení **jeden bod (x,y)** v jednom kroku.
    *   *HC:* Posunie sa k lepšiemu susedovi.
    *   *PSO:* Pripočíta sa vektor rýchlosti.
    *   *DE:* Pripočíta sa rozdielový vektor.
    *   *SOMA:* Skočí smerom k lídrovi.

---

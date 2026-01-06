### 1. Typy premenných (Kvalita vs. Kvantita)

Toto je prvá vec, ktorú musíš určiť, keď vidíš dáta. Podľa toho vyberáš grafy a výpočty.

#### A) Kvalitatívne premenné (Kategoriálne)
*   **Čo to je:** Slová, texty, kategórie. Nemôžeš s nimi robiť matematiku (sčítať ich).
*   **Príklady:** Farba očí (Modrá, Hnedá), Pohlavie (M/Ž), Typ školy.
*   **Čo počítame:**
    *   **Početnosť:** Koľko ľudí má modré oči?
    *   **Relatívna početnosť:** Koľko % to je?
    *   **Modus:** Ktorá kategória je najčastejšia?
*   **Grafy:** Stĺpcový graf (Bar chart), Koláčový graf (Pie chart).

#### B) Kvantitatívne premenné (Numerické)
*   **Čo to je:** Čísla, s ktorými má zmysel počítať (priemer, rozdiel).
*   **Delenie:**
    *   **Diskrétne:** Len celé čísla (Počet detí, počet gólov). "Skáče to".
    *   **Spojité:** Akékoľvek reálne číslo (Výška, Čas, Plat). "Tečie to".
*   **Čo počítame:** Priemer, Medián, Smerodajná odchýlka, Kvartily.
*   **Grafy:** Histogram (rozdelenie početností), Boxplot (krabicový graf - pre kvartily).

---

### 2. Odľahlé hodnoty a Pravidlo 3 sigma

Tu skúšajúci zisťujú, či vieš rozoznať "normálne" dáta od "extrémov".

#### A) Odľahlé pozorovania (Outliers)
*   **Definícia:** Hodnoty, ktoré sú "príliš ďaleko" od zvyšku dát.
*   **Ako ich nájsť (Metóda vnútorných hradieb):** To je ten príklad s Excelom, čo sme robili.
    *   Hranice: $Q1 - 1.5 \times IQR$ a $Q3 + 1.5 \times IQR$.
*   **Prečo sú problém:** Extrémne kazia **Priemer** (ťahajú ho k sebe). **Mediánu(prostredna hodnota)** nevadia (je voči nim odolný/robustný).

#### B) Pravidlo 3 sigma ($3\sigma$)
*   **Kedy platí:** LEN pre **Normálne rozdelenie** (Gaussova krivka).
*   **Čo hovorí:**
    *   $\mu \pm 1\sigma$ = 68 % dát.
    *   $\mu \pm 2\sigma$ = 95 % dát.
    *   $\mu \pm 3\sigma$ = **99,7 % dát**.
*   **Použitie:** Ak je niečo vzdialené viac ako $3\sigma$ od priemeru, považujeme to za **extrém** (takmer nemožné).
*   *Poznámka:* Čebyševova nerovnosť je "slabší odvar" tohto pravidla pre divné rozdelenia, ktoré nie sú normálne.

---

### 3. Teória odhadu (Bodový vs. Intervalový)

Tu sa hráme na detektívov. Máme vzorku (napr. 100 ľudí) a chceme niečo povedať o celej populácii (všetci ľudia).

#### A) Bodový odhad
*   **Definícia:** Jedno konkrétne číslo.
*   **Príklad:** "Priemerný plat v SR je 1350 €." (Vypočítané ako priemer vzorky $\bar{x}$).
*   **Nevýhoda:** Pravdepodobnosť, že sme sa trafili úplne presne na desatinné miesto, je nulová. Je to síce najlepší tip, ale nevieme, ako veľmi sme sa sekli.

#### B) Intervalový odhad (Confidence Interval - CI)
*   **Definícia:** Interval, v ktorom sa "skutočná hodnota" nachádza s určitou spoľahlivosťou (najčastejšie 95 %).
*   **Príklad:** "S 95 % istotou je priemerný plat medzi 1300 € a 1400 €."
*   **Vzťah Šírka vs. Spoľahlivosť (Toto milujú na skúške!):**
    *   Chcem **vyššiu istotu** (99 %)? $\to$ Musím interval **rozšíriť** (1200 – 1500). "Chytám rybu do väčšej siete, aby neušla."
    *   Chcem **vyšší presnosť** (užší interval)? $\to$ Musím znížiť istotu, ALEBO **zväčšiť počet dát ($n$)**.

---

Máš to zhrnuté **výborne**. Tvoja intuícia funguje správne. 👍

Dovolím si len dve malé doplnenia (tzv. "kozmetické úpravy"), aby to bolo na skúške na 100 %:

1.  **Modus vs. Medián:** Pri outlieroch si napísal, že **modus** je odolný. To je pravda, ale v praxi (napr. pri platoch) sa ako "náhrada" za priemer používa **Medián**.
    *   *Prečo?* Lebo medián je presný stred. Modus môže byť niekde úplne na kraji (napr. najčastejší plat je minimálna mzda, ale to nevystihuje strednú vrstvu). Takže na skúške hovor: *"Priemer je citlivý na extrémy, preto radšej používame Medián."*
2.  **Odpoveď pre šéfa (Interval):** Správne si povedal, že ak zúžim interval, klesne istota. Ale čo ak šéf trvá na 95 % istote A ZÁROVEŇ chce úzky interval?
    *   Jediné riešenie: **Zvýšiť počet dát ($n$)**.
    *   Ak sa opýtam 1000 ľudí namiesto 10, môj odhad bude oveľa presnejší (užší interval) pri rovnakej istote.

---

### 1. Hypotézy ($H_0$ a $H_1$)

Každý test začína súbojom dvoch tvrdení:

*   **$H_0$: Nulová hypotéza (Obhajoba / Nuda / Status Quo)**
    *   Hovorí: "Nič sa nedeje. Nie je tam rozdiel. Liek nefunguje. Kocka je férová."
    *   **Znak:** Vždy obsahuje rovná sa ($=$).
    *   *Poznámka:* My $H_0$ nikdy "nedokazujeme". My ju len buď **zamietneme** (ak sú dôkazy silné), alebo **nezamietneme** (pre nedostatok dôkazov).

*   **$H_1$: Alternatívna hypotéza (Obžaloba / Objav / To čo chceme)**
    *   Hovorí: "Niečo sa deje! Je tam rozdiel! Liek funguje! Kocka je cinknutá."
    *   **Znak:** Obsahuje nerovnosť ($\neq, <, >$).

---

### 2. P-hodnota (p-value) – Kľúč k rozhodnutiu 🗝️

Počítač ti vypľuje číslo zvané **p-value**.
Definícia (pre babku): **"Miera prekvapenia, že by to bola len náhoda."**

Porovnávame ju s **Hladinou významnosti $\alpha$** (alfa). Štandardne je $\alpha = 0.05$ (5 %).

*   **Ak $p < 0.05$ (Malé číslo):**
    *   Sme veľmi prekvapení. Toto nemôže byť náhoda!
    *   Dôkazy sú silné $\to$ **ZAMIETAME $H_0$**.
    *   **Prijímame $H_1$** (Platí alternatíva).
    *   *Verdikt:* "Štatisticky významný rozdiel."

*   **Ak $p > 0.05$ (Veľké číslo):**
    *   Nuda. Toto sa mohlo stať aj náhodou.
    *   Dôkazy sú slabé $\to$ **NEZAMIETAME $H_0$**.
    *   *Verdikt:* "Rozdiel sa nepreukázal." (Pozor! Nehovoríme, že neexistuje, len sme ho nenašli).

---

### 3. Chyby rozhodovania (I. a II. druhu) ⚠️

Nikdy si nie sme istí na 100 %. Môžeme sa seknúť:

*   **Chyba I. druhu ($\alpha$):**
    *   Realita: $H_0$ platí (Liek nefunguje / Nevinný).
    *   My povieme: Zamietame $H_0$ (Liek funguje / Odsúdime ho).
    *   *Dôsledok:* Falošný objav. Odsúdenie nevinného. (Horšia chyba vo vede).

*   **Chyba II. druhu ($\beta$):**
    *   Realita: $H_0$ neplatí (Liek funguje / Vinný).
    *   My povieme: Nezamietame $H_0$ (Nič sme nenašli / Pustíme ho).
    *   *Dôsledok:* Prehliadli sme objav. Pustili sme vinníka.

---
Super, ideme na to. Toto je tvoj **"Kufrík s náradím" (Toolbox)**.

Na skúške ti dajú do ruky dáta (alebo popis situácie) a ty musíš siahnuť do kufríka a vytiahnuť správny nástroj (test).

Aby si sa v tom vyznal, rozdelíme si testy na **dve hlavné rodiny**:

1.  **Parametrické testy (Elita):**
    *   Sú presnejšie a silnejšie.
    *   **Podmienka:** Vyžadujú **Normálne rozdelenie** dát (a často aj zhodu rozptylov).
    *   Pracujú s **Priemerom** ($\mu$).

2.  **Neparametrické testy (Robotníci):**
    *   Sú robustné (nezľaknú sa outlierov).
    *   **Podmienka:** Stačí im akékoľvek rozdelenie.
    *   Pracujú s **Mediánom** (alebo poradím).

---

### 1. Kategória: DVE SKUPINY (Najčastejšie otázky)

Tu sa vždy pýtaj: **Sú skupiny Nezávislé (A vs B) alebo Závislé (Pred vs Po)?**

#### A) Nezávislé výbery (Muži vs. Ženy / Bratislava vs. Košice)

| Situácia | Názov testu | Predpoklady (Čo musí platiť?) |
| :--- | :--- | :--- |
| **Dáta sú Normálne** | **Dvojvýberový t-test**<br>*(Independent samples t-test)* | 1. Normalita dát.<br>2. **Homoskedasticita** (Rovnosť rozptylov - vysvetlím nižšie). |
| **Dáta NIE SÚ Normálne** | **Mann-Whitney U test**<br>*(Wilcoxonov dvojvýberový)* | 1. Nezávislosť výberov.<br>2. Podobný tvar rozdelení. |

#### B) Závislé / Párové výbery (Pred vs. Po / Ľavá vs. Pravá ruka)

| Situácia | Názov testu | Predpoklady |
| :--- | :--- | :--- |
| **Dáta sú Normálne** | **Párový t-test**<br>*(Paired t-test)* | 1. Normalita **rozdielov** (nie pôvodných dát, ale stĺpca "rozdiel"). |
| **Dáta NIE SÚ Normálne** | **Wilcoxonov párový test**<br>*(Signed-rank test)* | 1. Symetria rozdielov okolo mediánu. |
| **Dáta sú len +/-** | **Znamienkový test**<br>*(Sign test)* | Žiadne špeciálne (len či sa to zlepšilo/zhoršilo). Je veľmi slabý. |

---

### 2. Kategória: VIAC AKO 2 SKUPINY (3+)

Napríklad porovnávaš 3 lieky (A, B, Placebo) alebo 4 pobočky firmy.
*Chyták:* Tu nemôžeš použiť t-testy (musel by si robiť A vs B, A vs C, B vs C... a to zvyšuje chybu).

| Situácia | Názov testu | Čo to robí? |
| :--- | :--- | :--- |
| **Dáta sú Normálne** | **ANOVA**<br>*(Analysis of Variance)* | Zistí, či sa aspoň jeden priemer líši od ostatných. |
| **Dáta NIE SÚ Normálne** | **Kruskal-Wallis test** | Neparametrická verzia ANOVY (cez mediány). |

**Dôležitý pojem: POST-HOC Analýza**
ANOVA ti povie len: *"Niekde je rozdiel."* (Ale nepovie kde).
Aby si zistil, KTO je ten iný (či A vs B, alebo B vs C), musíš urobiť **Post-hoc test** (napr. Tukeyho test).
*   *Analógia:* ANOVA je alarm, ktorý povie "Niekto sa vlámal do domu!". Post-hoc je policajt, ktorý zistí, že to bol zlodej v kuchyni.

---

### 3. Kategória: KATEGÓRIE (Áno/Nie, Farba očí)

Keď nemáš čísla, ale početnosti.

| Názov testu | Použitie | Príklad |
| :--- | :--- | :--- |
| **Chí-kvadrát test nezávislosti**<br>($\chi^2$ test of independence) | Zisťuje, či súvisia dve kategórie. | Súvisí **Fajčenie** (Áno/Nie) s **Rakovinou** (Áno/Nie)? |
| **Test dobrej zhody**<br>(Goodness of Fit) | Zisťuje, či dáta sedia na nejaký model. | Padajú na kocke čísla 1..6 rovnako často? |

---

### ⚠️ Špeciálny pojem: HOMOSKEDASTICITA

V sylabe máš otázku: *"Testy o rozptyle / overenie homoskedasticity".*
Toto musíš vedieť vysvetliť.

*   **Čo to je:** "Rovnosť rozptylov". Znamená to, že dve skupiny majú podobne "široké" Gaussove krivky. (Nie že jedna je úzka špicatá a druhá široká placka).
*   **Prečo je to dôležité:** Je to **predpoklad** pre Dvojvýberový t-test a ANOVU. Ak rozptyly nie sú rovnaké, t-test môže klamať.
*   **Ako sa to testuje:**
    *   **F-test:** Len pre 2 skupiny (veľmi citlivý na normalitu).
    *   **Leveneho test / Bartlettov test:** Používajú sa častejšie (aj pre viac skupín).
    *   *Hypotézy:* $H_0$: $\sigma_1^2 = \sigma_2^2$ (Rozptyly sú zhodné - Homoskedasticita).

---
**Áno!** S týmto zhrnutím, ktoré si práve poslal, pokrývaš približne **85 – 90 %** toho, čo na skúške reálne zaznie. Máš v tom systém a chápeš súvislosti, čo je dôležitejšie než bifľovanie vzorcov.

Ak vieš vysvetliť tieto bloky, tak skúšku určite **spravíš**.

Aby si však dostal **A-čko** alebo **B-čko** a nenechal sa zaskočiť nejakou "drobnosťou" zo sylabu, vypichnem ti posledné **4 malé témy**, ktoré v tvojom zhrnutí chýbajú (ale v sylabe sú).

Sú to rýchlovky, stačí si ich len prečítať a pochopiť princíp.

---

#### 1. Jednostranný vs. Obojstranný interval (a test)
*V sylabe: "rozdíl mezi oboustrannými, levostrannými a pravostrannými..."*

*   **Obojstranný (Two-sided):**
    *   Pýtaš sa: *"Je tam rozdiel?"* (Nezaujíma ťa smer).
    *   Hypotéza: $\mu \neq 0$.
    *   Interval: Hľadáš stredný pás (napr. 95 %).
*   **Jednostranný (One-sided):**
    *   Pýtaš sa: *"Je to **väčšie**?"* alebo *"Je to **menšie**?"*
    *   Hypotéza: $\mu > 0$ alebo $\mu < 0$.
    *   Interval: Hľadáš len jednu hranicu (napr. Dolnú: "Garantujem, že to je aspoň X").
    *   *Výhoda:* Ak máš smerovú hypotézu, ľahšie zamietneš $H_0$.

#### 2. Vzťah Intervalový odhad $\leftrightarrow$ Testovanie hypotéz
*V sylabe: "Jak lze využít intervalové odhady k testování...?"*

Toto je super trik. Testovať hypotézu môžeš aj bez p-hodnoty, len pomocou intervalu.
*   **Pravidlo:** Pozri sa, či hodnota z $H_0$ (napr. 0 alebo 500) leží v tvojom Intervalovom odhade.
    *   Ak je **VNÚTRI** intervalu $\to$ **Nezamietam $H_0$**. (Je to možná hodnota).
    *   Ak je **MIMO** intervalu $\to$ **Zamietam $H_0$**. (Je to vylúčené).

#### 3. Štatistická vs. Praktická významnosť (Effect size)
*V sylabe: "souvislost rozsah výběru a velikost efektu..."*

Toto je moderná kritika p-hodnôt.
*   **Štatistická významnosť ($p < 0.05$):** Hovorí len, že rozdiel nie je náhoda.
    *   *Problém:* Ak máš obrovskú vzorku ($n=1 000 000$), tak aj rozdiel 0.0001 mm bude "štatisticky významný", hoci v praxi je to blbosť.
*   **Praktická významnosť (Effect size):** Hovorí, **ako veľký** ten rozdiel je. (Napr. Cohenovo d).
    *   *Záver:* Na zamietnutie $H_0$ pri malej vzorke potrebuješ veľký efekt. Pri obrovskej vzorke stačí pidiminiatúrny efekt.

#### 4. Medicínske ukazovatele (Riziká)
*V sylabe: "poměr šancí (Odds Ratio), relativní riziko..."*

Používa sa pri tabuľkách 2x2 (napr. Fajčenie vs. Rakovina).
*   **Relatívne riziko (RR):** $\frac{\text{Pravdepodobnosť choroby u fajčiarov}}{\text{Pravdepodobnosť choroby u nefajčiarov}}$. (Ak vyjde 5, fajčiari majú 5x väčšiu šancu).
*   **Pomer šancí (OR - Odds Ratio):** Podobné, ale počíta sa cez stávkový kurz (Šanca pre / Šanca proti).

---


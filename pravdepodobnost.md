#### Otazka : Uveďte klasickou/statistickou definici pravděpodobnosti a příklad jejího použití.
---

### 1. Klasická definícia (Laplaceova)

Toto je definícia "od stola". Nepotrebuješ robiť žiadny pokus, stačí ti logika.

*   **Definícia:** Pravdepodobnosť javu $A$ je podiel počtu priaznivých výsledkov ($m$) k počtu všetkých možných výsledkov ($n$).
    $$P(A) = \frac{m}{n}$$
*   **Kľúčový predpoklad (NUTNÉ POVEDAŤ):** Všetky možné výsledky musia byť **rovnako pravdepodobné** a ich počet musí byť **konečný**.
*   **Intuícia:** Mám hraciu kocku. Má 6 strán. Je dokonale vyvážená. Aká je šanca, že padne šestka? 1 zo 6. Nemusím tou kockou hádzať, viem to *a priori* (vopred).
*   **Príklad:** Hod kockou, ťahanie kariet z balíčka, lotéria.

---

### 2. Štatistická definícia (Geometrická / Frekventistická)

Toto je definícia "z terénu". Používame ju, keď nevieme, či je kocka vyvážená, alebo keď je možností nekonečno.

*   **Definícia:** Pravdepodobnosť je číslo, ku ktorému sa **ustáľuje relatívna početnosť** javu pri mnohonásobnom opakovaní nezávislého pokusu.
    $$P(A) \approx \frac{m}{n} \quad (\text{pre } n \to \infty)$$
    *(Kde $n$ je počet vykonaných pokusov a $m$ je počet, koľkokrát jav nastal).*
*   **Kľúčový predpoklad:** Pokus musí byť **opakovateľný** za rovnakých podmienok donekonečna. Ide o tzv. *a posteriori* (spätnú) pravdepodobnosť.
*   **Intuícia:** Mám ohnutú mincu. Neviem, či padá viac hlava alebo orol. Nemôžem použiť klasickú definíciu (nie sú rovnako pravdepodobné). Musím ňou hodiť 1000-krát. Ak padne hlava 600-krát, prehlásim, že pravdepodobnosť hlavy je 0.6.
*   **Príklad:** Pravdepodobnosť, že sa narodí chlapec (cca 0.51), pravdepodobnosť, že výrobok bude chybný (zistíme až kontrolou výroby), úspešnosť liečby.

---

### 3. Hlavné rozdiely (Na toto sa pýtajú)

| Vlastnosť | Klasická | Štatistická |
| :--- | :--- | :--- |
| **Kedy ju vieme?** | **Pred** pokusom (A priori) | **Po** pokusoch (A posteriori) |
| **Podmienka** | Rovnaká šanca všetkých možností | Veľký počet opakovaní ($n \to \infty$) |
| **Presnosť** | Je to presné číslo | Je to odhad (limita) |
| **Použitie** | Hazardné hry, ideálne modely | Reálny svet, fyzika, poisťovníctvo |

---
### Otazka : Co je to podmíněná pravděpodobnost? Uveďte vzorec a příklad.
---

# 🎓 Podmienená pravdepodobnosť

### 1. Čo to je? (Definícia a Intuícia)
Podmienená pravdepodobnosť je pravdepodobnosť, že nastane jav **A**, ak už vieme (máme informáciu), že nastal jav **B**.

*   **Kľúčová myšlienka:** Informácia o jave $B$ **mení náš "svet"** (výberový priestor). Už nás nezaujímajú všetky možné výsledky, ale **len tie, ktoré patria do B**.
*   Jav $B$ sa stáva našou "novou istotou" (nových 100 %).

### 2. Vzorec
$$P(A \mid B) = \frac{P(A \cap B)}{P(B)}$$

*   **$P(A \mid B)$**: Pravdepodobnosť javu A za podmienky B (číta sa "A ak B").
*   **$P(A \cap B)$**: Pravdepodobnosť prieniku (že nastanú **oba naraz**).
*   **$P(B)$**: Pravdepodobnosť podmienky (tá musí byť nenulová, $P(B) > 0$).

---

### 3. Příklad (Ideálne na skúšku)
Najlepšie sa to vysvetľuje na **hracej kocke**, lebo si to skúšajúci vie predstaviť bez kalkulačky.

**Zadanie:**
Hádžeme jednou spravodlivou kockou.
*   Jav A: Padne **šestka** ($6$).
*   Jav B: Padne **párne číslo** ($2, 4, 6$).

**Otázka:** Aká je pravdepodobnosť, že padla šestka, ak vieme, že padlo párne číslo? ($P(A|B)$)

**Riešenie (Intuitívne):**
Vieme, že padlo párne číslo. Možnosti sú len tri: $\{2, 4, 6\}$.
Z týchto troch možností nám vyhovuje len jedna (tá šestka).
Výsledok musí byť **$1/3$**.

**Riešenie (Cez vzorec):**
1.  **$P(B)$** (Párne číslo): Sú 3 čísla zo 6. $\rightarrow 3/6 = 0.5$
2.  **$P(A \cap B)$** (Šestka A ZÁROVEŇ párne): To je len číslo 6. Je to 1 číslo zo 6. $\rightarrow 1/6$.
3.  **Dosadenie:**
    $$P(A \mid B) = \frac{1/6}{3/6} = \frac{1}{3}$$

---
### Otazka : Co to znamená, že náhodné jevy jsou disjunktní/nezávislé? Jak tyto vlastnosti ovlivní pravděpodobnost sjednocení/průniku?
---

### 1. Disjunktné (Nezlučiteľné) javy
*(Cudzie slovo: Disjoint / Mutually Exclusive)*

*   **Ľudsky:** "Nemôžu nastať naraz." Sú to nepriatelia. Ak nastane jeden, druhý automaticky zomrel.
*   **Vizuálne (Vennov diagram):** Dve bubliny, ktoré sa **nedotýkajú**.
*   **Príklad:** Hod jednou kockou.
    *   Jav A: Padne 1.
    *   Jav B: Padne 2.
    *   *Môžu padnúť naraz? Nie. Sú disjunktné.*

**Ako to ovplyvní vzorce?**
*   **Prienik (Průnik):** Je nemožný.
    $$P(A \cap B) = 0$$
*   **Zjednotenie (Sjednocení):** Pravdepodobnosti sa jednoducho sčítajú.
    $$P(A \cup B) = P(A) + P(B)$$

---

### 2. Nezávislé javy
*(Cudzie slovo: Independent)*

*   **Ľudsky:** "Jeden o druhom nevie." Informácia, že nastal jeden, nijako nezmení šancu toho druhého.
*   **Vizuálne:** Dve bubliny, ktoré sa prekrývajú "tak akurát".
*   **Príklad:** Hod kockou a hod mincou.
    *   Jav A: Na kocke padne 6.
    *   Jav B: Na minci padne Hlava.
    *   *Ovplyvňuje minca kocku? Nie. Sú nezávislé.*

**Ako to ovplyvní vzorce?**
*   **Prienik (Průnik):** Pravdepodobnosti sa násobia.
    $$P(A \cap B) = P(A) \cdot P(B)$$
*   **Zjednotenie (Sjednocení):** Použiješ všeobecný vzorec a dosadíš tam ten súčin.
    $$P(A \cup B) = P(A) + P(B) - [P(A) \cdot P(B)]$$

---

### 💡 Veľký Ťahák (Rozdiel)

Aby si to nikdy nepomýlil, zapamätaj si toto:

1.  **Disjunktné javy sú EXTRÉMNE ZÁVISLÉ!**
    *   Prečo? Ak viem, že padla 1 (Jav A), tak som si na 100 % istý, že nepadla 2 (Jav B). Jedna informácia totálne ovplyvnila druhú.
2.  **Disjunktné** $\rightarrow$ Týka sa to **JEDNÉHO** pokusu (nemôžu padnúť dve čísla naraz).
3.  **Nezávislé** $\rightarrow$ Týka sa to zvyčajne **DVOCH RÔZNYCH** pokusov (kocka a minca, dvaja rôzni ľudia).

---

### 🧪 Skúška správnosti (Tvoj ťah)

Máme balíček kariet (52 kariet, 4 farby: Srdce, Pika, Kríž, Káro). Ťaháme **jednu** kartu.

Mám tu dve dvojice javov. Povedz mi, ktorá dvojica je **Disjunktná** a ktorá je **Nezávislá**, a prečo:

1.  **Dvojica X:**
    *   Jav A: Karta je Eso.
    *   Jav B: Karta je Kráľ.
2.  **Dvojica Y:**
    *   Jav A: Karta je Eso.
    *   Jav B: Karta je Srdcová (Červená farba).

### 📝 Zhrnutie do ťaháku (Hierarchia vzorcov)

| Operácia | **Všeobecný vzorec (Platí vždy)** | Disjunktné (Len ak sa neprekrývajú) | Nezávislé (Len ak sa neovplyvňujú) |
| :--- | :--- | :--- | :--- |
| **Zjednotenie** ($A \cup B$) | $P(A) + P(B) - P(A \cap B)$ | $P(A) + P(B)$ | $P(A) + P(B) - P(A)P(B)$ |
| **Prienik** ($A \cap B$) | $P(A) \cdot P(B \mid A)$ | $0$ | $P(A) \cdot P(B)$ |

---
### Otazka : Co je to úplná množina vzájemně disjunktních jevů? Uveďte větu o úplné pravděpodobnosti a příklad její aplikace v reálné úloze.
---

### 1. Čo je to "Úplná množina vzájomne disjunktných javov"?
V odbornejšej literatúre sa tomu hovorí aj **Rozklad (partícia) výberového priestoru**.

Predstav si to ako **Tortu rozkrájanú na kúsky**.

Aby bola množina javov $\{H_1, H_2, \dots, H_n\}$ úplná a disjunktná, musí spĺňať dve podmienky:

1.  **Vzájomne disjunktné:** Žiadne dva javy sa neprekrývajú.
    *   *Ľudsky:* Nemôžeš byť naraz v dvoch skupinách. (Napríklad jeden výrobok nemôže byť vyrobený naraz na Stroji A aj na Stroji B).
    *   *Matematicky:* $H_i \cap H_j = \emptyset$ (pre $i \neq j$).
2.  **Úplné (Súčet je celok):** Keď ich všetky spojíme, dostaneme celý svet (celú tortu, 100 %).
    *   *Ľudsky:* Musí nastať aspoň jeden z nich. Neexistuje nič "mimo" týchto možností.
    *   *Matematicky:* $P(H_1 \cup H_2 \cup \dots \cup H_n) = 1$ (alebo súčet ich pravdepodobností je 1).

Týmto javom $H_i$ často hovoríme **Hypotézy** (príčiny).

---

### 2. Veta o úplnej pravdepodobnosti
Táto veta nám slúži na výpočet pravdepodobnosti nejakého javu $A$, ktorý sa môže stať **rôznymi spôsobmi** (cez rôzne hypotézy).

*   **Myšlienka (Divide and Conquer):** Je ťažké vypočítať $P(A)$ priamo. Preto si problém rozdelíme na menšie "podproblémy" podľa hypotéz a potom ich sčítame.
*   Je to vlastne **vážený priemer**.

**Vzorec:**
$$P(A) = \sum_{i=1}^{n} P(A | H_i) \cdot P(H_i)$$

**Rozpísané:**
$$P(A) = [P(A|H_1) \cdot P(H_1)] + [P(A|H_2) \cdot P(H_2)] + \dots$$

*   $P(H_i)$ = Ako veľký je kúsok torty (váha).
*   $P(A|H_i)$ = Aká je šanca javu A v tomto konkrétnom kúsku.

---

### 3. Príklad aplikácie (Továreň na skrutky)

Toto je klasický príklad, ktorý sa dáva na skúškach (okrem lekárskych testov).

**Situácia:**
Máme továreň s troma strojmi, ktoré vyrábajú skrutky.
1.  **Stroj 1** vyrobí 50 % celej produkcie. Kazovosť má 1 %.
2.  **Stroj 2** vyrobí 30 % celej produkcie. Kazovosť má 2 %.
3.  **Stroj 3** vyrobí 20 % celej produkcie. Kazovosť má 5 %.

**Otázka:** Aká je pravdepodobnosť, že náhodne vybraná skrutka zo skladu je chybná ($A$)?

**Aplikácia teórie:**
1.  **Úplná množina (Hypotézy):** Skrutka musela prísť buď zo stroja 1, 2 alebo 3. Nemohla prísť odnikiaľ, ani z dvoch naraz.
    *   $P(H_1) = 0.5$, $P(H_2) = 0.3$, $P(H_3) = 0.2$. (Súčet je 1).
2.  **Podmienené pravdepodobnosti (Kazovosť):**
    *   $P(A|H_1) = 0.01$
    *   $P(A|H_2) = 0.02$
    *   $P(A|H_3) = 0.05$
3.  **Výpočet (Veta o úplnej pravdepodobnosti):**
    $$P(A) = (0.01 \cdot 0.5) + (0.02 \cdot 0.3) + (0.05 \cdot 0.2)$$
    $$P(A) = 0.005 + 0.006 + 0.010 = 0.021$$

**Odpoveď:** Celková kazovosť výroby je 2,1 %.

---

### Spojitosť s tvojím príkladom (Antivírus)
Pamätáš si príklad s Antivírusom?
Tam boli hypotézy len dve: **Malware ($M$)** a **Čistý ($\bar{M}$)**.
Tieto dve tvoria úplnú množinu (lebo $10\% + 90\% = 100\%$).

Vetu o úplnej pravdepodobnosti si použil, keď si počítal menovateľa:
$$P(+) = P(+|M) \cdot P(M) + P(+|\bar{M}) \cdot P(\bar{M})$$

---
### Otazka : Uveďte Bayesovu větu a ilustrujte její použití na konkrétním příkladu.
---

### 1. Čo to je? (Intuitívna definícia)
Bayesova veta je návod, ako **aktualizovať našu pravdepodobnosť**, keď získame **novú informáciu** (dôkaz).

Umožňuje nám "otočiť" podmienenú pravdepodobnosť:
*   Vieme, s akou presnosťou test odhalí chorobu: $P(\text{Test} + \mid \text{Choroba})$.
*   Chceme vedieť, či máme chorobu, keď vyšiel test: $P(\text{Choroba} \mid \text{Test} +)$.

### 2. Vzorec (Musíš vedieť naspamäť)

$$P(A \mid B) = \frac{P(B \mid A) \cdot P(A)}{P(B)}$$

**Rozbor členov (Terminológia pre A-čkarov):**
*   **$P(A \mid B)$ (Aposteriórna):** Výsledná pravdepodobnosť javu A po zohľadnení dôkazu B. (To, čo hľadáme).
*   **$P(A)$ (Apriórna):** Naša pôvodná viera, ako často jav nastáva v populácii (predtým, než sme urobili test).
*   **$P(B \mid A)$ (Vierohodnosť / Likelihood):** Ako pravdepodobný by bol dôkaz B, keby hypotéza A platila. (Presnosť testu).
*   **$P(B)$ (Normalizačná konštanta):** Celková pravdepodobnosť dôkazu. (Tu zvyčajne používame **Vetu o úplnej pravdepodobnosti**, ktorú sme preberali pred chvíľou).

---

### 3. Konkrétny príklad (Lekársky test)
Použi ten istý príklad ako pri antivíruse, je najľahší na vysvetlenie.

**Zadanie:**
V populácii trpí **1 %** ľudí vzácnou chorobou ($A$). Máme test, ktorý má **99 %** senzitivitu (ak si chorý, ukáže $+$) a **5 %** chybovosť (ak si zdravý, ukáže $+$).
Pacientovi vyšiel pozitívny test ($B$). Je chorý?

**Dosadenie do Bayesa:**

1.  **Hľadáme:** $P(A \mid B)$ ... Šanca, že je chorý, ak má plus.
2.  **Poznáme (Z čitateľa):**
    *   $P(A) = 0.01$ (Vzácnosť choroby).
    *   $P(B \mid A) = 0.99$ (Presnosť testu).
3.  **Poznáme (Z menovateľa - Veta o úplnej pravdepodobnosti):**
    *   $P(B) = (0.01 \cdot 0.99) + (0.99 \cdot 0.05)$
    *   *(Chorý a Nájdený)* + *(Zdravý a Falošný poplach)*
    *   $P(B) = 0.0099 + 0.0495 = 0.0594$

**Výpočet:**
$$P(A \mid B) = \frac{0.01 \cdot 0.99}{0.0594} = \frac{0.0099}{0.0594} \approx 0.167$$

**Interpretácia (Pointa):**
"Aj keď má test presnosť 99 %, pozitívny výsledok znamená len **16,7 %** šancu, že je pacient naozaj chorý. Je to preto, lebo choroba je veľmi vzácna (Apriórna pravdepodobnosť je nízka) a falošné poplachy u zdravých ľudí 'prevalcujú' skutočné prípady."

---

### 💡 Ako si to zapamätať (Mnemotechnická pomôcka)

Vzorec vyzerá zložito, ale v skutočnosti je to len:

$$P(\text{Príčina} \mid \text{Dôkaz}) = \frac{\text{Správny dôkaz (Cesta A)}}{\text{Všetky dôkazy (Cesta A + Cesta B)}}$$

Skúšajúci bude nadšený, ak spomenieš, že menovateľ $P(B)$ sa počíta cez Vetu o úplnej pravdepodobnosti. Tým prepojíš dve otázky do jednej.

---

### 1. BLOK: DISKRÉTNA NÁHODNÁ VELIČINA (Schody) 🧱
*Syllabus: "Diskrétní náhodná veličina a její rozdělení"*

**TIER 1 (Musíš vedieť):**

1.  **Čo to je:** Veličina, ktorá nadobúda len **spočítateľné hodnoty** (zvyčajne celé čísla). "Skáče".
    *   *Príklad:* Počet detí v rodine, počet hodov mincou, počet kazov.
2.  **Pravdepodobnostná funkcia $P(x)$ (PMF):**
    *   Hovorí: "Aká je šanca, že padne presne číslo $x$?"
    *   *Vlastnosť:* Súčet všetkých stĺpčekov musí byť **1**. $P(x) \ge 0$.
3.  **Distribučná funkcia $F(x)$ (CDF):**
    *   Hovorí: "Aká je šanca, že padne číslo **menšie alebo rovné** $x$?" (Súčet zľava).
    *   *Vlastnosti:* Je to "schodíkovitá" čiara. Začína v 0, končí v 1. Je neklesajúca.
4.  **Charakteristiky:**
    *   **Stredná hodnota $E(X)$:** Očakávaný priemer (vážený priemer).
    *   **Rozptyl $D(X)$ / $Var(X)$:** Ako veľmi to "lieta" okolo priemeru.

**TIER 1: ZOO Diskrétnych rozdelení (Modelové príklady)**
*Toto chcú počuť najviac. Kedy použiť ktoré?*

*   **Bernoulliho pokus:** Základná tehla. Pokus s dvoma výsledkami (Úspech/Neúspech). Napr. jeden hod mincou.
*   **A) Binomické rozdelenie ($Bi(n, p)$):**
    *   *Princíp:* Opakujem Bernoulliho pokus $n$-krát a počítam **počet úspechov**.
    *   *Príklad:* Hádžem 10x mincou. Koľkokrát padne orol? (Mám pevný počet pokusov).
*   **B) Poissonovo rozdelenie ($Po(\lambda)$):**
    *   *Princíp:* Počítam výskyt **vzácnych javov** v čase alebo priestore. Neviem $n$ (počet pokusov), viem len priemer ($\lambda$).
    *   *Príklad:* Koľko áut prejde križovatkou za hodinu? Koľko hrozienok je vo vianočke?
*   **C) Hypergeometrické rozdelenie:**
    *   *Princíp:* Výber **BEZ vrátenia**. (Závislé pokusy).
    *   *Príklad:* Ťahám 5 kariet z balíčka. Koľko je es? (Keď vytiahnem eso, šanca na ďalšie klesá).

**TIER 2 (Na A-čko):**

*   **D) Negatívne binomické rozdelenie:**
    *   *Princíp:* Čakám na **k-ty úspech**. (Neviem počet pokusov $n$, ten je náhodný).
    *   *Príklad:* Koľkokrát musím vystreliť na bránu, aby som dal **konečne 3 góly**? (Môže to byť 3 strely, ale aj 50).

---

### 2. BLOK: SPOJITÁ NÁHODNÁ VELIČINA (Krivky) 🌊
*Syllabus: "Spojitá náhodná veličina a její rozdělení"*

**TIER 1 (Musíš vedieť):**

1.  **Čo to je:** Veličina, ktorá môže nadobúdať **ľubovoľnú hodnotu** z intervalu. "Tecie".
    *   *Príklad:* Výška, Váha, Čas, Teplota.
    *   *Pozor:* $P(X = \text{konkrétne číslo}) = 0$. (Plocha čiary je nula).
2.  **Hustota pravdepodobnosti $f(x)$ (PDF):**
    *   To je tá **krivka** (napr. Gaussov zvon).
    *   *Vlastnosti:* $f(x) \ge 0$. Celková plocha pod krivkou (integrál) = **1**.
3.  **Vzťah Hustota $\leftrightarrow$ Distribučná:**
    *   $F(x)$ (plocha) je **INTEGRÁL** z $f(x)$ (krivka).
    *   $f(x)$ (krivka) je **DERIVÁCIA** z $F(x)$ (plocha).

**TIER 1: ZOO Spojitých rozdelení**

*   **A) Normálne rozdelenie ($N(\mu, \sigma^2)$):**
    *   Kráľovná rozdelení. Gaussova krivka.
    *   **Vplyv parametrov (Otázka zo sylabu):**
        *   $\mu$ (Stredná hodnota): Posúva kopec **doľava/doprava**.
        *   $\sigma$ (Odchýlka): Mení tvar. Malá $\sigma$ = úzky špicatý kopec. Veľká $\sigma$ = široká nízka placka.
*   **B) Exponenciálne rozdelenie ($Exp(\lambda)$):**
    *   *Princíp:* Čakanie na prvú poruchu/udalosť. ("Doba života").
    *   *Príklad:* Ako dlho vydrží žiarovka, kým praskne? Ako dlho budem čakať na hovor?
*   **C) Rovnomerné rozdelenie ($U(a, b)$):**
    *   *Princíp:* Všetky hodnoty v intervale majú rovnakú šancu.
    *   *Príklad:* Čakanie na autobus, ktorý chodí každých 10 minút (môžem prísť kedykoľvek v čase 0 až 10). Hustota je obdĺžnik.

---

### 3. BLOK: NÁHODNÝ VEKTOR A KORELÁCIA 🔗
*Syllabus: "Náhodný vektor"*

**TIER 1 (Musíš vedieť):**

1.  **Náhodný vektor:** Keď nemeriame jednu vec, ale dve naraz. $(X, Y)$. Napr. (Výška, Váha) jedného človeka.
2.  **Marginálne rozdelenie:**
    *   Máme tabuľku pre $(X, Y)$. Marginálne rozdelenie je, keď nás zaujíma **len X** (a Y ignorujeme/sčítame) alebo **len Y**.
    *   *Analógia:* Súčet riadkov alebo stĺpcov na okraji tabuľky (margin = okraj).
3.  **Korelácia (Pearsonov koeficient $\rho$):**
    *   Meria **lineárnu závislosť** medzi X a Y.
    *   Hodnoty od **-1 po 1**.
        *   $+1$: Priama úmera (Čím vyšší, tým ťažší).
        *   $-1$: Nepriama úmera (Čím staršie auto, tým nižšia cena).
        *   $0$: Žiadna **lineárna** závislosť (neznamená to nezávislosť, môže tam byť oblúk!).

---

### 4. BLOK: LIMITNÉ VETY 🏁
*Syllabus: "Centrální limitní věta"*

**TIER 1 (Musíš vedieť rozdiel):**

1.  **Zákon veľkých čísel (Law of Large Numbers - LLN):**
    *   Hovorí o **presnosti**.
    *   "Čím viac pokusov urobím, tým viac sa nameraný priemer blíži k skutočnej teoretickej hodnote."
    *   *Príklad:* Hodím mincou 10x $\to$ môže padnúť 70% orlov. Hodím 1000x $\to$ bude to cca 50%.
2.  **Centrálna limitná veta (Central Limit Theorem - CLT):**
    *   Hovorí o **tvare rozdelenia**.
    *   "Súčet (alebo priemer) mnohých nezávislých náhodných veličín má vždy **Normálne rozdelenie**, bez ohľadu na to, aké mali rozdelenie tie pôvodné veličiny."
    *   *Príklad:* Hod kockou je rovnomerný (1..6). Ale priemer zo 100 hodov kockou vytvorí Gaussovu krivku.

---


# 📘 BIA: Skriptá na skúšku (Cheat Sheet)

## 🎯 1. Testovacie funkcie a Blind Search
Predtým, než začneš optimalizovať, musíš vedieť, čo optimalizuješ a s čím porovnávaš.

### Testovacie funkcie (Benchmarky)
Slúžia na otestovanie kvality algoritmu. Delíme ich podľa vlastností:
*   **Unimodálne (Jednovrcholové):** Majú len jedno globálne minimum, žiadne lokálne pasce. Ideálne na testovanie rýchlosti konvergencie (napr. *Sphere*).
*   **Multimodálne (Viacvrcholové):** Majú veľa lokálnych miním (pascí). Testujú schopnosť algoritmu "utiecť" z lokálneho optima (napr. *Rastrigin, Ackley, Schwefel, Griewangk*).
*   **Separabilné vs. Neseparabilné:** Či sa dajú premenné optimalizovať nezávisle (napr. *Rosenbrock* je neseparabilný – "banánové údolie", ťažké pre algoritmy).

### Blind Search (Slepé hľadanie)
*   **Princíp:** Algoritmus nemá žiadnu inteligenciu. Generuje náhodné riešenia alebo prehľadáva priestor mriežkou.
*   **Účel:** Slúži ako "baseline" (spodná hranica). Ak tvoj super algoritmus nedosiahne lepšie výsledky ako náhodné hľadanie, je zlý.
*   **Výhody:** Jednoduché.
*   **Nevýhody:** Extrémne pomalé, nepoužiteľné pre veľké dimenzie.

---

## 🏔️ 2. Algoritmy založené na jednom riešení (Trajectory Methods)
Pracujú len s **jedným** agentom/bodom v priestore, ktorý sa v každom kroku posúva.

### Hill Climbing (HC - Horolezecký algoritmus)
*   **Analógia:** Horolezec v hmle, ktorý chce vyliezť na najvyšší kopec. Vidí len pod nohy a vždy urobí krok smerom hore.
*   **Princíp:**
    1.  Vygeneruj náhodné riešenie.
    2.  Pozri sa do okolia (susedov).
    3.  Ak je sused lepší, presuň sa tam.
    4.  Opakuj, kým nenájdeš vrchol.
*   **Problém:** Uviazne v **lokálnom optime** (vylezie na malý kopček a nevidí, že vedľa je Mount Everest).
*   **Kedy použiť:** Jednoduché, unimodálne problémy.

### Simulated Annealing (SA - Simulované žíhanie)
*   **Analógia:** Kováčstvo – ochladzovanie rozžeraveného kovu. Keď je kov horúci, atómy skáču divoko (prijímame aj horšie riešenia). Keď chladne, atómy sa usádzajú (prijímame len lepšie).
*   **Princíp:** Vylepšený Hill Climbing. Aby sme neuviazli v lokálnom optime, **občas prijmeme aj horšie riešenie**.
*   **Kľúč:** Pravdepodobnosť prijatia horšieho riešenia závisí od **Teploty (T)**. Na začiatku je T vysoká (veľa náhodných skokov), postupne klesá (algoritmus sa "upokojí").
*   **Výhody:** Dokáže uniknúť z lokálneho optima.
*   **Nevýhody:** Treba dobre nastaviť schému ochladzovania.

---

## 🧬 3. Evolučné algoritmy (Population based)
Inšpirované Darwinovou teóriou. Pracujú s **populáciou** riešení naraz.

### Genetic Algorithm (GA) - aplikovaný na TSP
*   **Analógia:** Prežitie najsilnejšieho, kríženie chromozómov.
*   **Aplikácia na TSP (Travelling Salesman Problem):**
    *   *Jedinec:* Permutácia miest (napr. [1, 3, 2, 4, 5]).
    *   *Fitness:* 1 / celková dĺžka trasy (chceme najkratšiu).
*   **Operátory:**
    1.  **Selekcia:** Ruleta alebo Turnaj (vyberieme rodičov).
    2.  **Kríženie (Crossover):** Musí zachovať unikátnosť miest (napr. Order Crossover - OX).
    3.  **Mutácia:** Výmena dvoch miest v poradí (Swap) alebo obrátenie úseku (Inversion).
*   **Výhody:** Univerzálny, robustný.
*   **Nevýhody:** Veľa parametrov na nastavenie.

### Differential Evolution (DE)
*   **Analógia:** Matematická operácia s vektormi v populácii.
*   **Princíp:** Nového jedinca netvoríme krížením dvoch rodičov, ale **diferenciou (rozdielom)** iných vektorov.
*   **Rovnica mutácie:** $v = r1 + F \cdot (r2 - r3)$
    *   Vyberieš 3 náhodných jedincov ($r1, r2, r3$). Rozdiel dvoch pripočítaš k tretiemu (násobené váhou $F$).
*   **Improved versions:** Rôzne stratégie výberu (napr. *DE/best/1/bin* - berie sa najlepší jedinec namiesto náhodného r1).
*   **Výhody:** Skvelé na spojité funkcie (čísla), rýchla konvergencia, málo parametrov.
*   **Nevýhody:** Niekedy predčasná konvergencia.

---

## 🐝 4. Rojová inteligencia (Swarm Intelligence)
Inšpirované správaním zvierat (kolektívna inteligencia).

### Particle Swarm Optimization (PSO) - s Inertia Weight
*   **Analógia:** Kŕdeľ vtákov hľadajúcich potravu. Vtáky nemajú lídra, ale vedia o polohe najlepšieho v skupine.
*   **Princíp:** Každá častica má **Polohu** a **Rýchlosť**.
*   **Pohyb:** Rýchlosť sa mení na základe 3 zložiek:
    1.  **Inertia (Zotrvačnosť):** "Letím tam, kam som letel doteraz" (parameter $w$).
    2.  **Cognitive (Osobná skúsenosť):** "Vraciam sa tam, kde som ja našiel najlepšie jedlo" ($pBest$).
    3.  **Social (Sociálna skúsenosť):** "Letím tam, kde celý kŕdeľ našiel najlepšie jedlo" ($gBest$).
*   **Výhody:** Veľmi jednoduchý kód, rýchle.
*   **Inertia Weight ($w$):** Na začiatku veľké (Explorácia - lietam všade), na konci malé (Exploitácia - ladím detaily).

### Self-Organizing Migration Algorithm (SOMA) - AllToOne
*   **Analógia:** Svorka šeliem pri love. Všetci bežia smerom k vodcovi.
*   **Princíp:**
    *   *Leader:* Jedinec s najlepšou fitness.
    *   *Migrácia:* Všetci ostatní jedinci skáču smerom k Lídrovi.
    *   *AllToOne:* Všetci (All) idú k Jednému (One - Leader).
*   **Kľúč:** Jedinec nejde priamo na pozíciu lídra, ale "vzorkuje" cestu k nemu (robí kroky a meria fitness). Ak nájde cestou niečo lepšie, ostane tam.
*   **Parameter PRT (Perturbation):** Určuje, či sa zmenia všetky súradnice alebo len niektoré (zavádza chaos/náhodu).

### Ant Colony Optimization (ACO) - aplikované na TSP
*   **Analógia:** Mravce hľadajúce cestu k jedlu. Zanechávajú feromónovú stopu.
*   **Princíp:**
    *   Mravec si vyberá ďalšie mesto pravdepodobnostne.
    *   Čím viac **feromónu** na ceste ($\tau$) a čím je mesto **bližšie** ($\eta = 1/vzdialenosť$), tým vyššia šanca, že tam pôjde.
    *   *Evaporácia (Vyparovanie):* Feromón sa časom stráca. To je kľúčové, aby sme nezostali zaseknutí na starej zlej ceste.
*   **Výhody:** Najlepšie na grafové problémy (TSP, logistika).
*   **Nevýhody:** Pomalé pre veľké problémy.

### Firefly Algorithm (FA)
*   **Analógia:** Svetlušky. Svetlušky svietia, aby prilákali partnerov.
*   **Princíp:**
    1.  Všetky svetlušky sú unisex (každá priťahuje každú).
    2.  Atraktivita je úmerná **jasu** (fitness funkcia).
    3.  Menej jasná svetluška sa hýbe k jasnejšej.
    4.  **Absorpcia svetla:** S rastúcou vzdialenosťou svetlo slabne (exponenciálne).
*   **Kľúč:** Funguje dobre na multimodálne funkcie (rozdelí sa do podskupín okolo lokálnych maxím).

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

# Prehľad optimalizačných algoritmov a ich použitia

---

## 1) Hill Climbing
**Reálne použitie:**
- lokálna optimalizácia parametrov
- ladenie hyperparametrov (ML)
- plánovanie a optimalizácia trás s malou zložitosťou
- scheduling (krátke úlohy)
- optimalizácia jednoduchých funkcií

**Nevhodné pre:**
- problémy s mnohými lokálnymi minimami

---

## 2) Simulated Annealing (SA)
**Použitie:**
- TSP a kombinatorické problémy
- optimalizácia výrobných liniek
- layout čipov (mikroelektronika)
- optimalizácia portfólií
- routing v sieťach
- optimalizácia designu (architektúra, inžinierstvo)

**Dôvod:**
- vie unikať z lokálnych miním → vhodné na rugged landscape

---

## 3) Blind Search (ochutnávková heuristika)
**Použitie:**
- baseline na porovnanie algoritmov
- malé nenáročné funkcionality
- experimentálne merania
- random search v ML (hyperparametre)

---

## 4) Tabu Search
**Použitie:**
- kombinatorická optimalizácia
- scheduling, timetabling (rozvrhy)
- vehicle routing (VRP)
- TSP
- priemyselné plánovanie (výroba, preprava)
- telekomunikačné siete

**Dôvod:**
- pamäť + zakázané pohyby → uniká lepšie z lokálnych miním než HC

---

## 5) Genetic Algorithm (GA)
**Použitie:**
- evolučný design (antény, drony)
- optimalizácia parametrov pre ML
- automatizované obchodovanie
- engineering design (mechanika, aerodynamika)
- bioinformatika
- scheduling (letiská, logistika)
- hry a AI (evolúcia strategií)

---

## 6) Differential Evolution (DE)
**Použitie:**
- globálna optimalizácia black-box funkcií
- kalibrácia modelov (chemické, fyzikálne, biologické)
- tuning neurónových sietí
- inverzné problémy (geofyzika)
- systémová identifikácia
- elektronické obvody

**Poznámka:**
- silné tam, kde derivácia neexistuje alebo je špinavá

---

## 7) Particle Swarm Optimization (PSO)
**Použitie:**
- kontinuálne optimalizačné úlohy
- control engineering (PID tuning)
- neural network training
- fuzzy systems tuning
- robot path planning
- radar / sonar optimalizácia
- ekonomické modely

**Poznámka:**
- obľúbené v robotike a automatizácii

---

## 8) SOMA (Self Organizing Migrating Algorithm)
**Použitie:**
- optimalizácia technických parametrov
- engineering design
- robotika (trajektórie)
- optimalizácia modelov a simulácií
- systémové ladenie (control)

**Silné pri:**
- multimodálnych problémoch

---

## 9) Ant Colony Optimization (ACO)
**Použitie (hlavné):**
- TSP
- routing v sieťach (dáta, telekomunikácie)
- logistika / plánovanie trás
- robot path planning
- flow scheduling

**Charakteristika:**
- hľadanie ciest v grafoch

---

## 10) Teaching–Learning Based Optimization (TLBO)
**Použitie:**
- optimalizácia kontinuálnych funkcií
- kalibrácia parametrov
- structural design
- optimalizácia výrobných procesov
- optimalizácia energetických systémov

**Výhoda:**
- bezparametrový → jednoduché použitie

---

## 11) Firefly Algorithm
**Použitie:**
- multimodálna optimalizácia
- image processing
- thresholding v computer vision
- energetické systémy
- engineering design
- bioinformatika

**Dôvod:**
- dobre preskakuje lokálne minimá

---

## 12) NSGA-II (multi-objective GA)
**Použitie:**
- multi-objective engineering
- aerodynamika (drag vs lift)
- investičné portfóliá (zisk vs riziko)
- distribučné siete (náklady vs bezpečnosť)
- energetika (výkon vs spotreba)
- evolučný design
- architektúra + plánovanie
- biomedicína

**Výstup:**
- Pareto fronta (nie jedno optimálne riešenie)

---

# 1. Proces forenzného vyšetrovania a digitálne dôkazy

## i. Fázy forenzného vyšetrovania (6 fáz)

1.  **Identifikácia (Identification)**
    *   Určenie rozsahu: Kde sú dôkazy? (PC, mobily, cloud, logy).
    *   Právna a technická príprava pred zásahom.
2.  **Zber (Collection)**
    *   Fyzické alebo logické zaistenie dát.
    *   **Live acquisition** (zo zapnutého PC – RAM) vs. **Dead acquisition** (vypnuté PC).
    *   Zabezpečenie miesta činu a dokumentácia zapojenia.
3.  **Uchovávanie (Preservation)** – *Kritická fáza*
    *   Cieľ: Zachovať pôvodný stav dát (integritu).
    *   **Write-blocker:** Hardvérové zariadenie blokujúce zápis, aby sa nezmenil originál.
    *   **Bitová kópia (Forensic Image):** Klon 1:1 (vrátane zmazaných dát a prázdneho miesta). Pracuje sa vždy na kópii, nie na origináli!
4.  **Skúmanie (Examination)**
    *   Automatizované spracovanie dát nástrojmi (EnCase, FTK, Autopsy).
    *   Extrakcia súborov, obnova zmazaných dát, dešifrovanie.
5.  **Analýza (Analysis)**
    *   Interpretácia dát – hľadanie súvislostí.
    *   Odpovede na otázky: *Kto, čo, kedy, kde, prečo?*
    *   Spájanie dôkazov do časovej osi.
6.  **Prezentácia (Presentation)**
    *   Výsledný report pre laikov (súd, manažment).
    *   Musí byť objektívny, zrozumiteľný a podložený faktami.

---

## ii. Reťazec péče o dôkaz (Chain of Custody - CoC)

*   **Definícia:** Dokumentácia (protokol), ktorá chronologicky mapuje **celú históriu pohybu dôkazu** od jeho zaistenia až po súd/zničenie.
*   **Obsah:**
    *   **Kto** dôkaz držal/prevzal.
    *   **Kedy** (dátum a čas).
    *   **Kde** bol uložený (napr. Trezor A).
    *   **Prečo** (napr. prevzatie na analýzu).
*   **Dôležitosť:**
    *   Zaručuje dôveryhodnosť a integritu dôkazu.
    *   Bez neporušeného CoC je dôkaz na súde **nepoužiteľný** (obhajoba ho napadne pre možnú manipuláciu).

---

## iii. Hash a integrita dát

*   **Hash:** Matematický algoritmus (napr. MD5, SHA-1, SHA-256), ktorý zo vstupu vytvorí unikátny reťazec znakov ("digitálny odtlačok").
*   **Vlastnosti:**
    *   Jednosmernosť (nedá sa z neho získať pôvodný súbor).
    *   **Lavínový efekt:** Zmena 1 bitu v súbore = úplne iný výsledný hash.
*   **Využitie vo forenzike:**
    *   Slúži na **overenie integrity** (nemennosti) dôkazu.
    *   *Postup:* Vypočíta sa hash originálu -> urobí sa kópia -> vypočíta sa hash kópie. Ak sa zhodujú = kópia je verná a s dátami nikto nemanipuloval.

---
# 2. Digitálne dôkazy a ich analýza

## i. Digitálny dôkaz: Definícia a vlastnosti

**Definícia:**
Digitálny dôkaz je akákoľvek informácia uložená alebo prenášaná v **binárnej forme** (0 a 1), ktorá môže byť použitá na súde. Zahŕňa súbory, logy, históriu, metadáta, dáta v RAM aj sieťovú komunikáciu.

**Kľúčové vlastnosti:**
1.  **Latentný (Skrytý):**
    *   Dôkaz nie je viditeľný voľným okom (na rozdiel od fyzických dôkazov).
    *   Na jeho zobrazenie a interpretáciu sú potrebné špeciálne hardvérové a softvérové nástroje.
2.  **Volatilný a krehký (Fragile):**
    *   Veľmi ľahko sa dá zmeniť, poškodiť alebo zničiť (často aj neúmyselne, napr. zapnutím PC).
    *   Niektoré dôkazy zmiznú po odpojení napájania (RAM).
3.  **Ľahko kopírovateľný:**
    *   Je možné vytvoriť **identickú bitovú kópiu** originálu.
    *   Digitálny originál a kópia sú nerozoznateľné (na rozdiel od fyzických kópií).
4.  **Objemný:**
    *   Dnešné úložiská majú obrovské kapacity (TB), čo sťažuje hľadanie relevantných informácií ("ihla v kope sena").

---

## ii. 7 kľúčových otázok pri analýze (Kriminalistická taktická analýza)

Cieľom je zrekonštruovať príbeh a vytvoriť logický celok.

1.  **Kto? (Identita)**
    *   Kto je páchateľom a kto obeťou?
    *   *Pozor:* Digitálny dôkaz identifikuje **používateľský účet**, nie priamo fyzickú osobu. Nutné prepojiť s inými dôkazmi (kamery, svedkovia).
2.  **Čo? (Skutok)**
    *   Čo sa stalo? (Únik dát, neoprávnený prístup, zmazanie databázy, inštalácia malvéru).
3.  **Kedy? (Čas / Timeline)**
    *   Vytvorenie časovej osi udalostí.
    *   *Kritické:* Správne určenie časových pásiem (UTC vs. lokálny čas) a overenie presnosti systémového času.
4.  **Kde? (Miesto)**
    *   **Fyzické:** GPS súradnice, poloha pripojenia k Wi-Fi, lokalita BTS stanice mobilu.
    *   **Logické:** IP adresa, konkrétny priečinok na disku, cloudové úložisko, URL adresa.
5.  **Ako? (Metóda)**
    *   Aký bol postup útoku? (Phishing, zneužitie zraniteľnosti, uhádnutie hesla, SQL injection).
6.  **Čím? (Nástroj)**
    *   Aké prostriedky boli použité?
    *   **Hardvér:** USB kľúč, keylogger, klonovacie zariadenie.
    *   **Softvér:** Tor prehliadač, hackerské nástroje, šifrovací softvér.
7.  **Prečo? (Motív)**
    *   Hľadanie dôvodu konania v dátach.
    *   Vyhľadávanie na webe, chatová komunikácia, finančné záznamy, e-maily preukazujúce úmysel.

---
# 3. Vytvorenie laboratórneho prostredia a nástroje

## i. Pravidlá pre používanie forenzných nástrojov
Aby bola analýza uznaná súdom, musí spĺňať prísne štandardy:

1.  **Legálnosť softvéru:**
    *   Vždy používať **licencovaný a legálny softvér**.
    *   Použitie "cracknutých" verzií znižuje dôveryhodnosť experta a prináša riziko malvéru, ktorý môže poškodiť dôkazy.
2.  **Validácia a testovanie:**
    *   Nástroj musí byť overený (otestovaný na známych dátach), aby sme mali istotu, že funguje správne.
3.  **Evidencia verzií:**
    *   Nutné presne zaznamenať **názov a verziu** použitého softvéru (vrátane build number).
    *   Dôvod: Rôzne verzie môžu mať rôzne funkcie alebo chyby (bugy).
4.  **Opakovateľnosť (Reproducibility):**
    *   Základná vedecká podmienka.
    *   Ak iný expert použije rovnaké nástroje a postupy na rovnakých dátach, musí dospieť k **identickému výsledku**.

## ii. Nástroje forenznej analýzy a ich funkcie

Nástroje delíme na hardvérové a softvérové.

1.  **Write Blocker (Blokátor zápisu):**
    *   *Typ:* Primárne hardvér (existuje aj softvérový, ale menej spoľahlivý).
    *   *Funkcia:* Fyzicky **blokuje akýkoľvek zápis** na skúmané médium. Zabezpečuje, že sa pri pripojení disku nezmení ani 1 bit (napr. metadáta "Last Access"). Zaručuje integritu.
2.  **Analýza pamäte (Memory Forensics):**
    *   *Nástroje:* Volatility, FTK Imager.
    *   *Funkcia:* Skúmanie obsahu RAM (operačnej pamäte).
    *   *Cieľ:* Získanie bežiacich procesov, otvorených sieťových pripojení, dešifrovacích kľúčov a neuložených dát. Nutné vykonať pred vypnutím PC.
3.  **Obnova súborov (Data Carving):**
    *   *Nástroje:* Photorec, Autopsy, EnCase.
    *   *Funkcia:* Hľadanie a obnovovanie zmazaných súborov v "nealokovanom priestore" disku. Identifikuje súbory podľa ich hlavičiek (file signatures/headers), aj keď súborový systém informáciu o nich zmazal.
4.  **Analýza logov (Log Analysis):**
    *   *Nástroje:* Event Viewer (Windows), Splunk, textové editory.
    *   *Funkcia:* Skúmanie systémových a aplikačných denníkov.
    *   *Cieľ:* Rekonštrukcia histórie udalostí (kedy sa kto prihlásil, pripojenie USB zariadení, chyby systému, inštalácie).
5.  **Monitorovanie procesov:**
    *   *Nástroje:* Sysinternals Suite (Process Explorer, ProcMon), Task Manager.
    *   *Funkcia:* Sledovanie aktuálne bežiacich programov a služieb v reálnom čase.
    *   *Využitie:* Odhalenie skrytého malvéru, podozrivej sieťovej komunikácie alebo neautorizovaných aplikácií pri "Live" analýze.

---
# 4. Využitie OSINT (Spravodajstvo z otvorených zdrojov)

## i. Verejne dohľadateľné dáta a ich využitie vo forenzike

OSINT využíva legálne dostupné zdroje (nejde o hacking).

*   **Typy dát:**
    1.  **Sociálne siete (Social Media):** Fotky, statusy, zoznamy priateľov, check-iny (poloha).
    2.  **Technické registrácie:** WHOIS záznamy (kto vlastní doménu), DNS záznamy, SSL certifikáty.
    3.  **Úniky dát (Data Leaks):** Databázy hesiel a emailov (napr. HaveIBeenPwned) – zisťujeme, či páchateľ používa rovnaké heslo všade.
    4.  **Verejné registre:** Obchodný register, kataster, dlžníci, súdne rozhodnutia.
    5.  **Multimédiá:** EXIF metadáta vo fotkách, videá na YouTube.
*   **Využitie vo forenznej analýze:**
    *   **Profilovanie:** Prepojenie virtuálnej identity (prezývka, email) s reálnou osobou.
    *   **Overenie alibi:** Ak podozrivý tvrdí, že bol doma, ale postol fotku z iného mesta (GEO dáta).
    *   **Sociálna väzba:** Dokázanie, že dve osoby sa poznajú (napr. pri organizovanom zločine).

## ii. Nástroje na automatizovaný zber dát

Manuálne hľadanie je pomalé, preto sa používajú automatizované nástroje.

*   **Nástroje:**
    1.  **Maltego:**
        *   *Funkcia:* Vizualizácia vzťahov. Vytvára grafy prepojení (Entity Link Graph) medzi emailmi, osobami, doménami a IP adresami.
    2.  **TheHarvester:**
        *   *Funkcia:* Zber e-mailových adries, subdomén, hostiteľov a otvorených portov z verejných vyhľadávačov (Google, Bing, LinkedIn).
    3.  **Shodan:**
        *   *Funkcia:* Vyhľadávač pripojených zariadení (IoT, servery, kamery). Nehľadá obsah webu, ale technické parametre (otvorené porty, verzie OS).
    4.  **Wayback Machine (Internet Archive):**
        *   *Funkcia:* Umožňuje zobraziť staré verzie webových stránok, ktoré už boli zmazané alebo zmenené.
*   **Možné problémy:**
    *   **Anti-scraping mechanizmy:** Weby blokujú automatizované nástroje (CAPTCHA, banovanie IP).
    *   **Informačný šum (False Positives):** Nástroje nájdu príliš veľa nerelevantných dát (napr. menovec Ján Novák).
    *   **Etika a legalita:** Automatické sťahovanie dát môže porušovať podmienky používania služieb (ToS).

## iii. Typy OSINT (Kategórie)

1.  **SOCMINT (Social Media Intelligence):**
    *   *Popis:* Zber a analýza dát zo sociálnych sietí (Facebook, Instagram, X/Twitter, LinkedIn, TikTok).
    *   *Cieľ:* Analýza správania, životného štýlu, politických názorov a siete kontaktov. Často zahŕňa aj analýzu sentimentu.
2.  **GEOINT (Geospatial Intelligence):**
    *   *Popis:* Analýza informácií viazaných na geografickú polohu. Využíva satelitné snímky (Google Earth), mapy, Street View a geolokačné metadáta z fotiek.
    *   *Cieľ:* Určenie presného miesta, kde bola fotografia vyhotovená (podľa horizontu, budov, tieňov), sledovanie pohybu osôb.
3.  **Technical / Cyber OSINT:**
    *   *Popis:* Zameriava sa na technickú infraštruktúru internetu. Zahŕňa analýzu IP adries, domén, DNS záznamov, hashov súborov (VirusTotal) a malvéru.
    *   *Cieľ:* Identifikácia serverov útočníka, phishingových kampaní a technického zázemia zločinu.

---
# 5. Forenzná analýza v OS Windows

## i. Windows Registre (Registry)
Registre sú hierarchická databáza konfigurácií OS. Sú kľúčové pre analýzu aktivity používateľa a prítomnosti malvéru.

*   **Čo možno získať:**
    *   História pripojených USB zariadení (USBSTOR).
    *   Zoznam naposledy otvorených dokumentov a spustených programov (UserAssist, ShimCache).
    *   Informácie o sieti a nainštalovanom softvéri.
*   **Kľúče automatického spustenia (Persistence):**
    *   Útočníci ich využívajú na to, aby malvér prežil reštart počítača.
    *   **Run (`HKCU\...\Run`):** Programy uvedené v tomto kľúči sa spúšťajú automaticky **pri každom** prihlásení používateľa.
    *   **RunOnce:** Program sa spustí automaticky **iba raz** (pri najbližšom prihlásení) a následne sa kľúč zmaže. Často využívané na dokončenie inštalácie malvéru alebo zametenie stôp.

## ii. Windows Logy (Event Logs)
Hlavný zdroj auditných informácií (formát .evtx). Analyzujú sa najmä logy *Security* a *System*.

*   **Kľúčové udalosti (Event IDs):**
    1.  **Account Logged In (Event ID 4624):**
        *   Zaznamenáva úspešné prihlásenie.
        *   *Dôležité:* **Logon Type**. Typ 2 = lokálne prihlásenie (fyzicky), Typ 10 = RDP (vzdialený prístup - častý útok), Typ 3 = sieťové prihlásenie.
    2.  **New Process Executed (Event ID 4688):**
        *   Vznik nového procesu.
        *   *Obsahuje:* Názov procesu, cestu k súboru a **Parent Process ID** (kto proces spustil). Umožňuje sledovať reťazec útoku (napr. Word spustil PowerShell).
    3.  **New Service Installed (Event ID 7045 / 4697):**
        *   V systéme bola nainštalovaná nová služba.
        *   Indikátor perzistencie malvéru (snaha získať systémové oprávnenia a bežať na pozadí).

## iii. Analýza bežiacich procesov a služieb
Vykonáva sa pri živej analýze (Live Forensics) alebo analýze RAM. Hľadajú sa anomálie oproti bežnému stavu.

*   **Čo analyzujeme:**
    1.  **Vzťah Rodič-Dieťa (Parent-Child):**
        *   Má proces logického rodiča?
        *   *Podozrivé:* `svchost.exe` by mal byť spustený procesom `services.exe`. Ak ho spustil `explorer.exe` alebo `winword.exe`, ide o malvér.
    2.  **Cesta k súboru (Path):**
        *   Beží systémový proces zo správneho priečinka?
        *   *Podozrivé:* `svchost.exe` bežiaci z `C:\Temp` alebo `C:\Users\Downloads` (má byť v `C:\Windows\System32`).
    3.  **Digitálny podpis:**
        *   Je binárny súbor podpísaný dôveryhodnou autoritou (Microsoft, Adobe)?
    4.  **Sieťová aktivita:**
        *   Komunikuje proces (napr. Kalkulačka alebo Poznámkový blok) s internetom?
    5.  **Používateľ (User context):**
        *   Beží proces pod správnym účtom? (Systémové služby bežia pod SYSTEM/NETWORK SERVICE).

---
# 6. Steganografia a jej odhaľovanie

## i. Čo je steganografia?

**Definícia:**
Technika ukrývania tajnej informácie do inej, verejnej informácie (tzv. nosič alebo "cover medium") takým spôsobom, aby **existencia tajnej správy ostala utajená**.

*   **Rozdiel oproti kryptografii:**
    *   Kryptografia chráni *obsah* správy (je nečitateľná).
    *   Steganografia chráni *existenciu* správy (je neviditeľná).

**Aplikácie na rôznych typoch médií:**
1.  **Obrázky (Najčastejšie):**
    *   **LSB (Least Significant Bit):** Zmení sa posledný (najmenej významný) bit hodnoty farby pixelu.
    *   *Príklad:* Zmena hodnoty farby z `11111110` na `11111111`. Ľudské oko rozdiel vo farbe nerozozná, ale z týchto posledných bitov sa poskladá tajný súbor.
2.  **Audio:**
    *   Ukrývanie dát do frekvencií, ktoré sú pre ľudské ucho nepočuteľné (podobne ako pri MP3 kompresii, ale opačne), alebo využitie LSB v audio vzorkách.
3.  **Video:**
    *   Ukrývanie dát do jednotlivých snímok (frames) alebo do audio stopy videa.
4.  **Text / Sieťové protokoly:**
    *   Využitie "bielych znakov" (medzery vs. tabulátory na konci riadkov) alebo manipulácia s hlavičkami TCP/IP paketov.

## ii. Nástroje a postupy na odhalenie (Steganalýza)

Odhaľovanie sa nazýva **steganalýza**. Neexistuje jedno univerzálne tlačidlo "nájdi steganografiu", používajú sa rôzne prístupy.

**Nástroje a ich funkcia:**

1.  **Stegsolve (Vizuálna analýza):**
    *   *Funkcia:* Umožňuje prechádzať jednotlivé bitové roviny (Bit Planes) obrázka.
    *   *Princíp:* Zobrazí napr. len "najnižší bit modrého kanála". Ak sa v ňom objaví štruktúra, text alebo vzor (namiesto náhodného šumu), ide o steganografiu.
2.  **Binwalk (Štrukturálna analýza):**
    *   *Funkcia:* Analyzuje binárnu štruktúru súboru a hľadá vnorené súbory.
    *   *Princíp:* Hľadá známe hlavičky súborov (Magic Numbers). Odhalí, ak niekto "prilepil" ZIP archív na koniec JPG obrázka (tzv. append steganography).
3.  **StegExpose (Štatistická analýza):**
    *   *Funkcia:* Automatizovaný nástroj na detekciu LSB steganografie v hromadnom množstve obrázkov.
    *   *Princíp:* Analyzuje histogram a štatistické odchýlky (napr. Chi-Square test). Prirodzený šum fotky má určité vlastnosti – vložená správa tieto vlastnosti naruší.
4.  **OpenStego / Steghide:**
    *   Nástroje, ktoré slúžia na vytváranie steganografie, ale často sa používajú aj na pokus o extrakciu, ak poznáme heslo (Dictionary attack na heslo k steganografii).

**Postupy detekcie:**
5.  **Vizualizácia:** Hľadanie vizuálnych anomálií v jednotlivých farebných kanáloch.
6.  **Analýza histogramu:** Hľadanie neprirodzených "skokov" v rozložení farieb (napr. párovanie hodnôt).
7.  **Kontrola veľkosti súboru:** Ak má jednoduchý obrázok podozrivo veľkú veľkosť, môže obsahovať skryté dáta.

---
# 7. Zaisťovanie logov a analýza sieťovej prevádzky

## i. Informácie z logov o aktivite v sieti

Logy poskytujú metadáta o komunikácii (nie jej obsah). Sú kľúčové pre rekonštrukciu útoku.

*   **Zdroje logov:** Firewall, Router, Proxy server, DNS server, VPN koncentrátor.
*   **Aké informácie získavame:**
    1.  **5-tuple (Pätica):** Zdrojová IP, Cieľová IP, Zdrojový port, Cieľový port, Protokol (TCP/UDP).
    2.  **Časová pečiatka (Timestamp):** Kedy presne spojenie nastalo (kritické pre koreláciu s inými logmi).
    3.  **Akcia (Action):** `ALLOW` (povolene) vs. `DENY/DROP` (zablokované firewallom).
    4.  **DNS dopyty:** Aké domény zariadenie hľadalo (odhaľuje komunikáciu s C&C servermi útočníka).
    5.  **URL adresy (z Proxy):** Konkrétne navštívené stránky a stiahnuté súbory.

## ii. Honeypoty a identifikácia útočníkov

**Definícia:**
Honeypot je **návnada** – systém alebo server zámerne nastavený tak, aby vyzeral zraniteľne a prilákal útočníkov. Neobsahuje žiadne produkčné dáta.

**Využitie pri identifikácii:**
*   **Princíp "Zero False Positives":** Keďže o honeypote bežní užívatelia nevedia a nemá žiadnu produkčnú funkciu, **akákoľvek interakcia s ním je považovaná za škodlivú/neautorizovanú**.
*   **Zber informácií (Threat Intelligence):**
    *   Odhalenie IP adries útočníka.
    *   Analýza použitých nástrojov a techník (TTPs - Tactics, Techniques, and Procedures).
    *   Získanie vzoriek malvéru, ktorý sa útočník pokúsi nahrať.
*   **Odvrátenie pozornosti:** Zdržuje útočníka, zatiaľ čo správcovia zabezpečujú reálnu sieť.

## iii. Analýza zachytenej sieťovej prevádzky (Network Traffic Analysis)

Ide o hĺbkovú analýzu paketov (Packet Capture - PCAP).

*   **Nástroje:**
    1.  **Wireshark:** Grafický nástroj na detailnú analýzu paketov. Umožňuje filtrovanie a rekonštrukciu streamov (Follow TCP Stream).
    2.  **Tcpdump:** Príkazový riadok (CLI) na rýchly zber paketov na serveroch.
    3.  **NetworkMiner:** Nástroj zameraný na extrakciu súborov a osôb z prevádzky.
    4.  **Zeek (Bro):** Nástroj na analýzu sieťových metadát.

*   **Typy získaných dát:**
    *   **Obsah komunikácie (Payload):**
        *   Ak nie je šifrovaná (HTTP, FTP, Telnet, SMTP): Možno čítať e-maily, vidieť prezerané obrázky, **zachytiť prihlasovacie údaje (mená a heslá)** v otvorenom texte.
        *   Extrakcia prenášaných súborov (napr. útočník sťahuje kradnuté PDF).
    *   **Hlavičky (Headers):** MAC adresy (fyzická identifikácia zariadenia), IP adresy, nastavenia TCP flagov (SYN, ACK, FIN) na analýzu skenovania portov.
    *   **Šifrovaná prevádzka (SSL/TLS):** Analyzujeme aspoň metadáta (SNI – názov servera, platnosť certifikátu, veľkosť toku dát).

---
# 8. Blockchain a analýza sociálnych väzieb

## i. Technológia Blockchain

**Definícia:**
Decentralizovaná, distribuovaná databáza (účtovná kniha - ledger), ktorá uchováva stále sa rozširujúci zoznam záznamov (blokov).

**Kľúčové vlastnosti:**
1.  **Reťazenie (Chaining):** Každý blok obsahuje kryptografický hash predchádzajúceho bloku. Tým sa vytvára reťaz.
2.  **Imutabilita (Nezmeniteľnosť):** Akonáhle je blok zapísaný a potvrdený sieťou, nemožno ho zmeniť bez zmeny všetkých nasledujúcich blokov (čo je pri dostatočnom výkone siete nemožné).
3.  **Decentralizácia:** Neexistuje centrálna autorita (banka). Kópiu databázy majú tisíce uzlov (počítačov) po celom svete.
4.  **Využitie:** Kryptomeny (Bitcoin), Smart kontrakty (Ethereum), dodávateľské reťazce (sledovanie tovaru), nezmeniteľné logy.

## ii. Sledovanie transakcií v sieti Bitcoin

Bitcoin nie je anonymný, ale **pseudonymný**. Identita je skrytá za alfanumerický reťazec (adresu peňaženky), ale história transakcií je verejná.

**Postup analýzy:**
1.  **Sledovanie toku (Follow the money):** Analytik sleduje presun prostriedkov z adresy na adresu vo verejnom blockchaine.
2.  **Identifikácia (De-anonymizácia):** Cieľom je nájsť bod, kde digitálna stopa prechádza do fyzického sveta. Najčastejšie sú to **centralizované burzy (Exchanges)**, ktoré musia dodržiavať pravidlá **KYC (Know Your Customer)** a **AML (Anti-Money Laundering)**.
3.  **Clustering (Zhlukovanie):** Algoritmy odhadujú, ktoré adresy patria tej istej osobe (napr. ak v jednej transakcii použijem vstupy z troch rôznych adries, pravdepodobne všetky tri patria mne).

**Nástroje:**
*   **Blockchain Explorers:** Webové stránky na ručné prezeranie transakcií (napr. Blockchain.com, Etherscan).
*   **Profesionálne nástroje:** Chainalysis, Elliptic – automatizovane vizualizujú toky a identifikujú rizikové peňaženky (Darknet, Ransomware).

## iii. Analýza a vizualizácia sociálnych väzieb (SNA - Social Network Analysis)

Metóda skúmania sociálnych štruktúr pomocou teórie grafov.

**Základné prvky:**
*   **Uzly (Nodes):** Reprezentujú entity (ľudia, telefónne čísla, bankové účty, Bitcoin adresy).
*   **Hrany (Edges):** Reprezentujú vzťahy (hovor, email, transakcia, priateľstvo na Facebooku).

**Čo analyzujeme (Metriky):**
1.  **Centralita (Centrality):** Kto je najdôležitejšia osoba v sieti? (Napr. boss gangu má najviac spojení).
2.  **Mosty (Betweenness):** Kto prepája dve inak izolované skupiny? (Spojka).
3.  **Komunity (Clusters):** Ktoré skupiny uzlov spolu komunikujú častejšie než s ostatnými?

**Nástroje na vizualizáciu:**
*   **Maltego:** Vizualizácia vzťahov z OSINT dát.
*   **Gephi:** Open-source nástroj na analýzu a vizualizáciu veľkých grafov a sietí.
*   **i2 Analyst's Notebook:** Štandard pre policajné zložky (drahý komerčný softvér).
---
# 9. Analýza podvodných URL adries

## i. Domain Hijacking (Únos domény)

**Definícia:**
Neoprávnené prevzatie kontroly nad doménovým menom. Útočník nezíska prístup len k webovému serveru, ale zmení registráciu domény, čím presmeruje všetku prevádzku na svoje servery.

**Ako k tomu dochádza:**
*   Phishing namierený na registrátora domény.
*   Krádež prístupových údajov k administratívnemu účtu domény.
*   Sociálne inžinierstvo.

**Detekcia (Odhalenie):**
1.  **WHOIS História:** Sledovanie zmien v registračných údajoch (zmena mena vlastníka, kontaktného e-mailu).
2.  **Zmena DNS záznamov:** Doména zrazu smeruje na IP adresu v inej krajine alebo na neznámy hosting.
3.  **Neplatné SSL certifikáty:** Po presmerovaní môže mať útočník problém okamžite získať validný certifikát (prehliadač hlási chybu).

## ii. IDN a Punycode (Homograph Attacks)

**IDN (Internationalized Domain Names):**
Umožňuje používať v doménach znaky národných abecied (diakritika, cyrilika, čínske znaky) namiesto štandardného ASCII.

**Punycode:**
*   Systém kódovania, ktorý prevádza Unicode znaky (napr. `ü`, `č`) na ASCII reťazec začínajúci predponou `xn--`.
*   *Príklad:* `münchen.de` sa v DNS systéme preloží na `xn--mnchen-3ya.de`.

**Riziko pre phishing (Homoglyfy):**
*   Útočníci využívajú vizuálnu podobnosť znakov z rôznych abecied (Homoglyphs).
*   *Príklad:* Latinské `a` (U+0061) vs. Cyrilické `а` (U+0430). Vyzerajú identicky.
*   Útočník zaregistruje doménu, ktorá vizuálne vyzerá ako `apple.com`, ale technicky je to iná doména.

## iii. Techniky maskovania URL adries

Cieľom je oklamať používateľa, aby si myslel, že je na legitímnej stránke.

1.  **Zneužitie subdomén (Subdomain Abuse):**
    *   Vytvorenie dlhej subdomény, ktorá obsahuje názov legitímnej služby.
    *   *Príklad:* `facebook.com.secure-login.update-user.com`.
    *   *Vysvetlenie:* Reálna doména je `update-user.com`, ale používateľ vidí na začiatku "facebook.com".
2.  **Typosquatting:**
    *   Registrácia domén s preklepmi (`gogle.com`, `faceboook.com`).
3.  **Punycode / Homograph útoky:**
    *   Využitie vyššie spomínaných IDN znakov na vizuálnu zhodu.
4.  **Skracovače URL:**
    *   Použitie služieb ako bit.ly alebo tinyurl na skrytie cieľovej destinácie.
5.  **IP adresa namiesto domény:**
    *   Niekedy (menej časté) útočník pošle priamo `http://192.168.x.x`, čo bežný používateľ nevie overiť.

## iv. Single script vs. Mixed script spoofing

Rozdiel v spôsobe využitia IDN znakov pri útoku:

1.  **Mixed Script Spoofing (Miešané písma):**
    *   Útočník kombinuje znaky z rôznych abecied v jednom slove (napr. latinka + gréčtina + cyrilika).
    *   *Detekcia:* Moderné prehliadače majú ochranné mechanizmy. Ak detegujú miešanie abecied (čo je v bežnej reči nezmysel), **automaticky zobrazia surový Punycode** (`xn--...`) namiesto falošného názvu, čím útok prezradia.
2.  **Single Script Spoofing (Jedno písmo):**
    *   Celá doména (alebo label) je vytvorená znakmi z **jednej cudzej abecedy**, ktoré vyzerajú ako latinka.
    *   *Príklad:* Celé slovo "paypal" napísané len znakmi z cyriliky, ktoré vyzerajú identicky.
    *   *Riziko:* Toto je **ťažšie odhaliteľné** pre prehliadače, pretože doména v jednom jazyku je technicky validná (napr. ruská doména). Prehliadač ju často zobrazí v "čitateľnej" forme, čím používateľa oklame.

---
# 10. Sieť Tor a onion služby

## i. Princíp fungovania Tor a Cibuľové smerovanie

**Tor (The Onion Router):**
Sieť zameraná na anonymizáciu používateľa tým, že prevádzku preposiela cez sériu dobrovoľníckych serverov (uzlov).

**Cibuľové smerovanie (Onion Routing):**
*   Dáta sú zabalené do viacerých vrstiev šifrovania (ako vrstvy cibule).
*   Štandardná cesta (Circuit) sa skladá z 3 skokov (Hops):
    1.  **Vstupný uzol (Entry/Guard Node):** Pozná IP klienta, ale nevidí obsah ani cieľ. Odstráni prvú vrstvu šifrovania.
    2.  **Stredný uzol (Middle Node):** Pozná len predchádzajúci a nasledujúci uzol. Nevie nič o zdroji ani cieli. Odstráni druhú vrstvu.
    3.  **Výstupný uzol (Exit Node):** Odstráni poslednú vrstvu a pošle dáta na cieľový server (internet). Vidí obsah (ak nie je HTTPS), ale nevie, kto ho poslal.
*   **Anonymita:** Je zaručená tým, že žiadny jednotlivý uzol nepozná celú cestu (zdroj aj cieľ súčasne).

## ii. Kľúčové pojmy: Relay, Bridge, Pluggable Transport

1.  **Relay (Uzol):**
    *   Verejne uvedený server v sieti Tor, ktorý preposiela prevádzku.
    *   Zoznam všetkých Relay uzlov je verejný (Consensus), čo umožňuje firewallom ich blokovať.
2.  **Bridge (Most):**
    *   **Neverejný (tajný) uzol**.
    *   Slúži pre používateľov v krajinách alebo sieťach s cenzúrou, kde sú verejné Relay uzly zablokované. Keďže nie sú v zozname, cenzor ich ťažšie nájde.
3.  **Pluggable Transport (PT):**
    *   Softvér na **obfuskáciu (maskovanie)** prevádzky.
    *   Transformuje tok dát Toru tak, aby pre systémy hĺbkovej inšpekcie paketov (DPI) vyzeral ako niečo iné (napr. ako náhodný šum alebo bežný HTTPS).
    *   *Príklad:* `obfs4`, `meek`.

## iii. Onion služby (Hidden Services)

Špeciálne webové služby prístupné iba cez sieť Tor, identifikované doménou `.onion`.

**Ako fungujú:**
*   Služba neuvádza svoju IP adresu (DNS sa nepoužíva).
*   Namiesto priameho spojenia využívajú komplexný systém "zoznamovacích bodov".
    1.  **Introduction Points:** Služba si vyberie niekoľko uzlov v sieti a povie im "tu som".
    2.  **Rendezvous Point (Stretávací bod):** Klient si vyberie náhodný uzol v sieti a povie službe (cez Introduction point), aby sa tam stretli.
*   Spojenie prebehne v tomto strede.

**Zabezpečenie anonymity:**
*   **Obojstranná anonymita:** Klient nepozná IP adresu servera a Server nepozná IP adresu klienta.
*   **End-to-End šifrovanie:** Komunikácia je šifrovaná automaticky (nie je potrebný certifikát od autority), pretože samotná `.onion` adresa je odvodená z kryptografického kľúča služby.
*   **Uzavretosť:** Prevádzka nikdy neopustí sieť Tor (neprechádza cez Exit uzol), čím sa eliminuje riziko odpočúvania na výstupe.

---
# 11. Lámanie hesiel (Password Cracking)

Ide o proces získavania pôvodného textu hesla (plaintext) z jeho zahashovanej podoby alebo prekonávanie autentifikácie.

## i. Princípy útokov

1.  **Brute Force (Útok hrubou silou):**
    *   *Princíp:* Systematické skúšanie všetkých možných kombinácií znakov (a-z, 0-9, symboly) danej dĺžky.
    *   *Vlastnosti:* Zaručene nájde heslo, ale je časovo extrémne náročný (exponenciálny nárast času s dĺžkou hesla). Vhodný len pre krátke heslá (do 7-8 znakov).
2.  **Dictionary Attack (Slovníkový útok):**
    *   *Princíp:* Používa zoznam pravdepodobných hesiel (slovník) – napr. bežné slová, mená, dátumy.
    *   *Hybridný útok:* Kombinuje slovník s pravidlami (napr. vezme slovo "Admin" a skúša variácie "Admin123", "admin!", "4dmin").
    *   *Vlastnosti:* Veľmi rýchly a efektívny proti bežným používateľom, neúčinný proti náhodným reťazcom (`Xy9#m_P`).
3.  **Rainbow Tables (Dúhové tabuľky):**
    *   *Princíp:* Metóda **Time-Memory Tradeoff**. Využíva obrovské predvypočítané databázy hashov.
    *   Keď útočník získa hash, nepočíta ho znova, ale len ho vyhľadá v tabuľke a zistí pôvodné heslo.
    *   *Obmedzenie:* Sú neúčinné, ak systém používa **Solenie (Salting)** – pridanie náhodného reťazca k heslu pred hashovaním.

## ii. Nástroje na lámanie hesiel

Rozdeľujeme ich na **Offline** (máme súbor s hashom) a **Online** (skúšame sa prihlásiť na web/server).

1.  **Hashcat:**
    *   *Funkcia:* Najrýchlejší a najpokročilejší nástroj na **Offline** útoky. Využíva výkon grafickej karty (**GPU akcelerácia**).
    *   *Použitie:* Podporuje stovky typov hashov (MD5, SHA, BitLocker, WPA2).
    *   *Obmedzenie:* Vyžaduje výkonný hardvér a znalosť príkazového riadku.
2.  **John the Ripper (JtR):**
    *   *Funkcia:* Univerzálny nástroj (CPU based). Výborný na automatickú detekciu typu hashu.
    *   *Použitie:* Často sa používa na Linuxové heslá (/etc/shadow) alebo ZIP archívy.
3.  **Ophcrack:**
    *   *Funkcia:* Nástroj špecializovaný na heslá Windows (LM a NTLM hashe).
    *   *Použitie:* Využíva **Rainbow Tables**. Dokáže prelomiť heslá Windows XP/7 v priebehu sekúnd (ak nie sú príliš dlhé).
4.  **Hydra:**
    *   *Funkcia:* Nástroj na **Online** útoky.
    *   *Použitie:* Skúša heslá priamo proti bežiacej službe (SSH, FTP, Web form).
    *   *Obmedzenie:* Pomalé (závisí od siete) a hrozí zablokovanie účtu po X neúspešných pokusoch.

---
# 12. Analýza mobilných zariadení

## i. Digitálne stopy na mobilných zariadeniach

Mobilné zariadenia sú najosobnejším zdrojom dôkazov.

*   **Komunikácia:**
    *   Zoznamy hovorov (Call Logs), SMS/MMS.
    *   **Chatovacie aplikácie (IM):** WhatsApp, Messenger, Signal, Telegram. Dáta sú často uložené v **SQLite databázach**, odkiaľ je možné obnoviť aj zmazané správy (WAL súbory, nealokovaný priestor).
*   **Lokalizačné údaje (Geo-lokácia):**
    *   História GPS (Google Maps, Waze).
    *   **Wi-Fi siete:** Zoznam sietí, ku ktorým sa zariadenie pripojilo, dokazuje fyzickú prítomnosť na danom mieste.
    *   **BTS (Cell towers):** Informácie o pripojení k mobilným vežiam.
    *   **Multimédiá:** Fotografie a videá obsahujúce EXIF metadáta (GPS súradnice miesta vyhotovenia).
*   **Aplikačné dáta:**
    *   Internetové prehliadače (história, cookies, heslá).
    *   **Health (Zdravie):** Počet krokov, srdcový tep (Apple Health/Google Fit) – môžu potvrdiť aktivitu používateľa v čase trestného činu.
    *   Bankové aplikácie, Uber/Bolt história.

## ii. Výzvy pri analýze mobilných zariadení (Mobile Forensics Challenges)

Mobilná forenzika je zložitejšia než počítačová kvôli rýchlemu vývoju a uzavretosti systémov.

1.  **Šifrovanie a bezpečnosť (Encryption):**
    *   Moderné systémy (iOS, Android) používajú **Full Disk Encryption (FDE)** alebo **File Based Encryption (FBE)**.
    *   Dáta sú čitateľné iba po zadaní PIN kódu/hesla/biometrie. Bez neho je extrakcia často nemožná (existujú výnimky pomocou nástrojov ako Cellebrite, GrayKey, ktoré využívajú zraniteľnosti na obídenie zámku).
2.  **Rôznorodosť operačných systémov (Fragmentácia):**
    *   **Android:** Tisíce rôznych modelov a verzií OS. Každý výrobca (Samsung, Xiaomi, Huawei) má vlastné úpravy, čo sťažuje vývoj univerzálnych extrakčných nástrojov.
    *   **iOS:** Uzavretý "ekosystém" (Walled Garden) s vysokou bezpečnosťou, ktorý sťažuje prístup k súborovému systému.
3.  **Vzdialené zmazanie (Remote Wipe):**
    *   Zariadenia sú neustále pripojené k sieti. Páchateľ môže na diaľku vydať príkaz na zmazanie (Find My iPhone / Find My Device).
    *   *Riešenie:* Okamžité umiestnenie zariadenia do **Faradayovho vrecka** (blokuje signál) alebo prepnutie do letového režimu.
4.  **Aktualizácie aplikácií:**
    *   Aplikácie sa aktualizujú veľmi často. Zmena štruktúry databázy aplikácie môže spôsobiť, že forenzný nástroj nedokáže správne interpretovať dáta, kým nevydá aktualizáciu.
5.  **Hardvérové pripojenie:**
    *   Poškodené konektory alebo proprietárne porty môžu znemožniť extrakciu dát štandardnou cestou.

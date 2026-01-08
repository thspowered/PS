
**Jaké protokoly a technologie využívá WebRTC?**
Websockety, HTML5, DTLS
***
**Na jaké vrstvě ISO/OSI modelu pracuje RTP:**
4.vrstva
***
**U protokolu ZRTP se pro výměnu klíčů využívá metoda:**
Diffie Helmann
***
**Nástroj Sipp využívá pro řízení SIP dialogu schémata definovaná v jazyce:**
XML
***
**Jak se nazývá možná grafická nádstavba pro IDS/IPS nástroj Suricata:**
Kibana
***
**SIP Proxy Kamailio podporuje zabezpečení SIP pomocí:**
TLS
***
**Distribuce master klíče pro šifrování transportního protokolu RTP se v praxi realizuje pomocí metod(y):**
SDES-SRTP, DTLS-SRTP, ZRTP
***
**Co znamená pojem RRD u výkonnostního testování IP telefonní infrastruktury:**
Časový interval od odeslání SIP zprávy REGISTER, do přijetí kladné odpovědi 200 OK..
***
**Na jaké vrstvě ISO/OSI modelu pracuje IPsec:**
3. vrstva
***
**Která s uvedených aplikací slouží pro skenování a monitoring v prostředí IP telefonie:**
SIPVicious
***
**Pro aktivaci podpory SRTP v Asterisk slouží příkaz:**
encryption=yes
***
**K prolomení hesel pomocí nástroje SIPVicious slouží skript:**
svcrack
***
**Pro podepsaný certifikát se mohou použít přípona(y) souboru:**
.pem , 
.crt
***
**SPIT je:**
Obdoba spam útoku v IP telefonii.
Typ sociálního útoku
***
**U protolu SIP se dá využít následujících autentizačních schémat:**
HTTP Digest
***
**Ktera z uvedenych aplikaci slouzi pro vytvoreni Dos utoku v prostredi IP telefonie**
INVITEflood
***
**Jak se v adresnim radku prohlizece znaci prenos pres WebSockety**
wss
ws
***
**IDS/IPS Suricata ukládá zachycená data do logu výhradně pomocí technologie:**
JSON
***
**Pro privátní klíč se mohou použít přípona(y) souboru:**
.key
.pem
***

***
***
**Co je to steganografie**
Zposob tajneho ukritia informacie do jine, nenapadne nosne zpravy - najcastejsie obrazok, zvuk, video
Cielom je zpravu zkryt nie zasaifrovat
***
**Co je to Honeypot, uveďte příklady Honeypotů pro IP telefonii?**
Je to návnada pro útočníka v naší síti. Tváří se jako nějaký síťový prvek s otevřenými porty a když na něj útočník zaútočí, sbírá o útoku detailní data a poté je využívá ke své obraně a lepšímu zabezpečení. Honeypoty mohou simulovat různé prvky - SIP klienty, SIP proxy, různé síťové servery.
***
**Do jakých kategorií můžeme rozdělit IDS/IPS systémy (podle jejich umístění v síti) ?**
NIDS (Network intrusion detection system) - nasazen na okraji síťě, monitoruje provoz celé sítě 
HIDS (Host intrusion detection system) - nasazen u klienta, monitoruje provoz u klienta
***
**Jakým způsobem rozšiřuje ZRTP původní SRTP ?**
Klasické SRTP používá k šifrování RTP klíče ze signalizace, tudíž například když nezašifrujeme SIP signalizaci pomocí TLS, tak může útočník ten klíč zjistit. ZRTP je nadstavba SRTP a pro sdílení klíčů používá Diffie-Hellmanův algoritmus, tudíž je bezpečnější pokud se například nešifruje signalizace.
***
**Co je to MitM, definujte:**
Typ útoku (Man-in-the-middle), kdy se útočník připojí do sítě pomocí např. ARP spoofingu (princip vysvětlen v KB zkoušce). Odchytává provoz mezi zařízeními bez toho, aniž by o tom tato zařízení věděla.
***
**Uveďte stručně a výstižně, jaký je účel IPS a IDS systémů, rozdíl mezi nimi a příklady implementace.**
IDS (Intrusion detection system) - jedná se o systém, který detekuje a loguje informace o vniknutí do systému - např. Snort IPS (Intrusion prevention system) - systém, který dokáže detekovat, ukládat logy i aktivně zasahovat při vniknutí do systému - např. Surikata
***
**Uveďte dva druhy VoIP Honeypotů, jež se v praxi využívají, principy funkce, příklady zapojení, příklady aplikací.**
Artemisa - může simulovat různé SIP prvky a tváří se jako nezabezpečený VoIP prvek. Brekeke - je VoIP SIP proxy server, který může být v módu Honeypot Dionae - command based honeypot, jenž může simulovat i jiné než VoIP prvky (různé HTTP servery, FTP servery apod.). Možno umístit do DMZ, jenž je oddělena od naší vnitřní sítě a poskytuje další úroveň zabezpečení.
***
**Popište stručně jednotlivé bezpečnostní mechanismy používané u protokolu SIP a jejich rozdělení podle OSI/ISO vrstev.**
SIP sám o sobě žádnou bezpečnost v sobě nemá, je potřeba využít například TLS, které přidává šifrování a autentizaci. Přidružené protokoly, které se používají při protokolu SIP jsou nejčastěji RTP, což probíhá na L4, bezpečnostní mechanismy SRTP nebo ZRTP. V L3 se v souvislosti se SIP používá IPsec. L2, zde je potřeba hlavně mít zabezpečenou proti ARP poisoningu. Na L1 - fyzické vrstvě je potřeba dbát o fyzickou přístupnost k zařízením pouze autorizovaným osobám.
***
**Popište rozdíl mezi NIDS a HIDS?**
NIDS - network intrusion detection system - IDS systémy monitorují a detekují podezřelý provoz a hlásí jej například správci sítě, ale nezasahují aktivně (oproti IPS intrusion protection system), NIDS toto dělá v celé síti. HIDS - host intrusion detection system HIDS je IDS systém, který monitoruje podezřelý provoz u hosta. Opět je vlastně pasivní, podezřelé pakety nedokáže zaříznout nebo je umístit do karantény, ale spíše hlásí.
***
**Co je to Wangiri?**
Wangiri je podvodná technika, kdy útočník prozvoní (one ring) oběti s cílem ať oběť zavolá zpět na nějaké prémiové číslo. Část výtěžku z poplatku zavolání na prémiové číslo putuje právě útočníkovi.
***
**Vysvětlete, jak probíhá zabezpečení SIP signalizace pomocí TLS v mezidoménové komunikaci.**
SIP se stará o signalizaci a výměnu různých řídících informaci pro spojení. V této signalizaci se nachází zranitelné informace, které útočník může zachytit a použít k útoku. Proto se SIP signalizace zabezpečuje protokolem TLS, jenž může zabezpečit provoz čtvrté vrstvy RM OSI a vyšší (transportní,relační, prezentační, aplikační). Například při použití protokolu SRTP pro přenos hlasových dat, je důležité šifrovat pomocí TLS signalizaci, jelikož si z ní útočník může vyčíst klíč použitý pro šifrování SRTP. TLS tudíž může poskytovat ochranu proti MITM útoku, kdy i když zachytíme provoz nemůžeme z něj nic vyčíst. TLS dále může zajištovat autentizaci SIP prvků v komunikaci. K zabezpečení SIP signalizace se používají TLS 1.2 a 1.3. TLS může používat algoritmy pro hashovaní (zajištění integrity a autentizace) třeba SHA-2, pro šifrování například symetrickou šifru AES. Nebo pro TLS1.3 Chacha20.
***
**Popište možnosti využití a princip funkce nástroje Sipp?**
SIPp slouží k testování a simulaci SIP komunikace, včetně bezpečnostních scénářů. Umožňuje různé druhy testů, například zátěžové testování, a vše je realizováno pomocí scénářů.**
***
**K čemu slouží penetrační testování v IP telefonii, uveďte příklady nástrojů zaměřených na VoIP**
Penetrační testování v IP telefonii slouží k ověření bezpečnosti VoIP systémů simulací útoků. Používá se k odhalení zranitelností, slabých hesel a možnosti zneužití služeb. Mezi nástroje patří například SIPp, SIPVicious, VoIP Hopper nebo Wireshark.
***
**Popište v jednotlivých krocích, jak funguje krádež TFTP konfiguračních souborů v prostředí VoIP.**
Krádež TFTP konfiguračních souborů ve VoIP spočívá v tom, že útočník získá přístup do hlasové sítě, zjistí TFTP server a stáhne konfigurační soubory IP telefonů, které jsou často pojmenované podle MAC adresy. Tyto soubory nejsou chráněny autentizací ani šifrováním a obsahují SIP přihlašovací údaje. Získaná data mohou být zneužita k přihlášení k SIP účtům nebo k toll fraud.
***
**Popište v jednotlivých krocích, jak funguje ARP Poisoning.**
ARP poisoning funguje tak, že útočník v lokální síti posílá falešné ARP odpovědi, ve kterých přiřadí svou MAC adresu k IP adrese jiného zařízení (např. brány). Tím otráví ARP cache obětí. Provoz mezi obětí a cílovým zařízením je pak směrován přes útočníka, který jej může odposlouchávat, měnit nebo blokovat.
***

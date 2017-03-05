# **SAN - Storage Area Network** 
##### **Dariusz Gawron, Mariusz Okularczyk, Krzysztof Czech**

##1. Podstawowe informacje o SAN. 
###  * SAN jest typem sieci komputerowej, której celem jest udostępnianie zasobów takich jak macierze dyskowe (storage) dla serwerów w ramach organizacji.
###  * Jest to dedykowany typ sieci, do której zazwyczaj nie ma dostępu z sieci LAN organizacji. SAN ma własne dedykowane urządzenia sieciowe.
###  * Zazwyczaj jest to storage typu blokowego.
###  * Według [Storage Network Industry Association](http://www.snia.org/about) głównym celem SAN jest tranfer danych pomiędzy systemami komputerowymi, a urządzeniami storage.

##2. Podstawowe topologie SAN

![Topologie SAN](/SAN-DG/Grafiki/San-Top.PNG)

###  1. Point-to-Point (Punkt-Punkt).
###    Najprostsza topologia sieci SAN, wykorzystywana do podłączania ze sobą dwóch węzłów (urządzeń). Zakładamy, że nie będziemy skalować infrastruktury poziomo (vertical scaling) - czyli nie będą podłączane nowe urządzenia (węzły).
###    Przepustowość łącza nie jest współdzielona pomiędzy urządzeniami, więc wykorzystywana jest ona w pełni na potrzeby komunikacji pomiędzy połączonymi węzłami.
###    Łącze działa trybie pełnego dupleksu - komunikacja może odbywać się jednocześnie w dwóch kierunkach.
###  2. Arbitrated loop (pętla z arbitrażem).
###    Zwana inaczej siecią FC-AL (Fibre Channel - Arbitrated Loop). Topologia tego typu nie wymaga dodatkowych urządzeń sieciowych takich jak przełączniki SAN. Wszystkie urządzenia połączone są ze sobą w pętlę. Komunikacja odbywa się pomiędzy kolejnymi urządzeniami w pętli, to oznacza że wszystkie urządzenia muszą działać przy tej samej przepływności (channel capacity). Inaczej mówiąc, sieć działa z najwyższą przepływnością najwolniejszego elementu pętli.

![FC-AL](/SAN-DG/Grafiki/FC-AL.PNG)

###    Z uwagi na ograniczenia adresowe w pętli nie może być w niej więcej niż 126 urządzeń - zarządzane są one jako jedna współdzielona szyna transmisji. Ruch odbywa się w jednym kierunku przekazując ramki przez kolejne elementy pętli. Protokół arbitrażu pozwala na ustanowienie jednego połączenia między nadawcą i odbiorcą, kiedy komunikacja zostaje zrealizowana pomiędzy dwoma portami następuje zwolnienie pętli i może być ustanowione nowe połączenie pomiędzy dwoma portami w pętli. Pętle można skonfigurować z Hubami w celu ułatwienia zarządzania połączeniami. Dystans do 10 km jest wspierany przez standard Fibre Channel, jednak długość pętli wpływa na opóżnienia w komunikacji.  
###  3. Switched Fabric (pełna sieć - tzw. Fabric)
### Najbardziej przydatna topologia, wykorzystująca przełączniki i inne urządzenia sieciowe. Zwana inaczej Fibre Channel Switched Fabric (FC-SW). Fabric ma przynajmniej jeden przełącznik SAN w ramach swojej konfiguracji. Przełączany Fabric zapewnia pełną szerokość pasma w medium transmisyjnym (bandwidth) na każdy port w porównaniu ze współdzieloną szerokością pasma w przypadku implementacji pętli z arbitrażem.

![FC-SW](/SAN-DG/Grafiki/FC-SW.PNG)

### Najważniejszą różnicą pomiędzy FC-AL, a FC-SW jest to że dodanie nowego urządzenia w FC-AL powoduje dalszy podział współdzielonej szerokości pasma. W przypadku FC-SW przepustowość pasma w medium transmisyjnym zostaje zwiększona. Powoduje to stopniowe odchodzenie od topologii FC-AL.

### Tradycyjne topologie FC-SW:
### Pojedynczy przełącznik (single switch) - urządzenie podpięte są do jednego przełącznika FC.

![Single Switch](/SAN-DG/Grafiki/FC-SW-Single.PNG)

### Pierścień (ring) - przełączniki są podłączone ze sobą, przełączniki na początku i na końcu kolejki mają dodatkowe połączenie zamykające pierścień.

![Ring topology](/SAN-DG/Grafiki/FC-SW-Ring.PNG)

### Kaskadowa (Cascade) - przełączniki są podłączone ze sobą (w kolejce).

![Cascade topology](/SAN-DG/Grafiki/FC-SW-Cascade.PNG)

### Topologia Siatki (Mech topology) - każdy przełącznik jest podłączony fizycznie do pozostałych przełączników w sieci (zapewnia redundancje połączeń).

![Mesh topology](/SAN-DG/Grafiki/FC-SW-Mesh.PNG)

### Topologie warstwowe.
### Edge-Core - urządzenia pamięci masowej podłączone są do urządzenia głównego (centralnego, w jądrze sieci).
![Core-Edge](/SAN-DG/Grafiki/FC-Core-Edge.PNG)

### Edge-Core-Edge - urządzenia pamięci masowej moga być podłączone do urządzeń wyższej warstwy sieci. W tym przypadku są to przełączniki brzegowe.

![Edge-Core-Edge](/SAN-DG/Grafiki/FC-Edge-Core-Edge.PNG)

### Edge Switch (przełącznik brzegowy) - przełącznik znajdujący się na brzegu sieci, umożliwiający komunikację pomiędzy innymi sieciami, może być to komunikacja z hostami lub innymi Fabricami.
### Obydwie wspomniane wyżej architektury mogą opisywać więcej "podsieci FC" - **subfabrics**. W przypadku architektury Core-Edge może istnieć podział na Core Fabric oraz na Edge Fabrics. W **Edge-Core-Edge** oraz **Core-Edge** można izolować zasoby od hostów (serwerów). Zasoby dyskowe są podłączone do innego Fabrica niż serwery - może to służyć łatwiejszej i bezpieczniejszej administracji infrastrukturą SAN. 

## 3. Fibre Channel (dodatkowe informacje o [FC](/FC - Fibre Channel.md)):
### Warstwy Fibre Channel:
Warstwa | Opis
--------|---------
FC0 | Warstwa fizyczna - stardard zastosowanego okablowania, jego cechy. W przypadku FC stosujemy okablowanie światłowodowe oraz miedziane.
FC1 | Warsta łącza danych (Data-Link). Odpowiedzialna za obsługę odpowiedniego schematu kodowania (encoding scheme) dla danego łącza. 
FC2 | Warstwy odpowiedzialna za zarządzanie parametrami transferu danych - podział danych na ramki (*Framing Protocol*), wielkość pojedyńczej ramki danych (flow control), port/adres docelowy dla tej ramki. Wartswa ta zawiera definicje klas usługi - wybieranych zależności od wymagań które musi spełnić system. Warstwa ta zajmuje się definiowaniem funkcji dla transmisji z wykorzystaniem pojedynczego portu.
FC3 | Warstwa ta definiuje zaawansowne funkcje takie jak stripping (tranfer danych przy pomocy wielu łączy), multicast (wielu odbiorców), hunt group (przypisanie wielu portów do jednego węzła). Warstwa ta definiuje funkcje transmisji wykorzystujące wiele portów.  
FC4 | Umożliwia współpracę FC z innymi protokołami takimi jak np. IP, SCSI, FCP, FICON. 
![Warstwy Fibre Channel](/SAN-DG/Grafiki/FC-Layers.PNG)
### **Warstwy FC0, FC1 oraz FC2 nazywane są czasem warstwą fizyczną i sygnałową protokołu FC - opisywaną skrótem FC-PH**
### Fibre Channel jest to protokół łączący cechy zwykłej szyny danych (np. SCSI) - przestrzeń dyskowa udostępniona w ten sposób jest widoczna jako zwykły DAS, z funkcjonalnościami dostępnymi w tradycyjnych sieciach.
![Warstwy FC, z opisem i protokołami](/SAN-DG/Grafiki/FC-Layers2.PNG)

Klasy usługi FC | Opis | Wymaga potwierdzenia (istotna jest kolejność przesyłanych ramek)
----------------|------|------------------------------------------------------------------
Class 1 | Dedykowane połączenie z pełną przepustowością. | Tak
Class 2 | Połączenie nie wymaga rozpoczęcia komunikacji (connectionless). Komunikacja Przełącznik-Przełącznik do przesyłania ramek FC (ramki FC są podstawową jednostka danych przesyłaną poprzez protokół) | Tak
Class 3 | Podobnie jak klasa 2. Z wyjątkiem braku potwierdzeń. | Nie
Class 4 | Dedykowane połączenie wykorzystujące tylko część przepustowości w trakcie komunikacji port-port, wykorzystuje tzw. Virtual Circuits (VCs). Każdy port typu N może zarządać VC wraz z gwarantowaną jakością usług (przepustowością łącza). Zestawiony obwód wirtualny składa się z dwóch jednokierunkowych połączeń, prędkość połączeń nie musi być równa. Klasa usługi osiągalna tylko w sieciach z przełącznika (FC-SW) | Tak.
Class 5 | Klasa jeszcze niezdefiniowana, nazywana izochroniczą usługą (isochronous service). Z założenia będzie miała zastosowania przy aplikacjach wymagających prawie natychmiastowego odbioru danych (usługi wideokonferencji dla przykładu). Klasa nie jest opisana w dokumentacji FC-PH. | Brak danych
Class 6 | Klasa wspierająca połączenia multicast, wymagająca ustonowienia połączenie (connection-oriented). | Tak
Class F | Klasa wykorzystywana do połączeń ISLs (Inter-switch links). Połączenie nie musi być wcześniej ustanowione (connectionless) ale przesyłane są potwierdzenia braku dostarczenia ramki. Klasa wykorzystywana do kontroli, koordynacji i konfiguracji Fabrics. | Tak

### **ISL - inter-switch link - protokół połączenia ustanawianego pomiędzy przełącznika lub logicznymi przełącznika.**
### Ramka FC
![Schemat ramki Fibre channel](/SAN-DG/Grafiki/FC-frame.PNG)

###Elementy ramki FC:
### SOF (Start of Frame), Nagłówek FC, Blok danych SCSI, Cyclic Redundancy Check, End of Frame delimeter;      
## 4. Fabric
### Fabric - sieć urządzeń (np. przełączników FC) zapewniająca dostęp do danych. Dane znajdują się na urządzeniach pamięci masowej podłączonych w ramach Fabrica.
## 5. Porty
### **Port jest podstawowym elmentem sieci opartej na Fibre Channel.**
Port | Opis
-----|------
F_port | Wykorzystywana do połączenia się z portem typu N_port (node port), połączenie punkt-punkt z przełącznikiem.
FL_port | Port pętli, wykorzystywana do podłączenia się do portu NL_port (node loop port). Porty pętli wykorzystywane są w rozwiązaniach typu pętla z arbitrażem.
TL_port | Port w urządzeniach firmy CISCO wykorzystywany do podłączenia urządzeń nierozpoznających Fabrica (non-fabric aware) w prywatnych pętlach urządzeń. Translative loop port.
G_port | port typu rodzajowego (generic), może pracować jako expansion port (E_port) lub jako F_port. Port jest definiowany jako G_port jeżeli nastapiło połączenie ale nie otrzymano potwierdzenia inicjalizacji pętli (look initialization) lub nie ukończono inicjalizacji pętli z najbliższym urządzeniem Fibre Channel.
L_port | Port typu loop-capable, może dotyczyć węzła lub przełącznika. 
U_port | Port uniwersalny, bardziej uniwersalny niż G_port. Może pracować jako E_port, F_port lub FL_port. Port jest definiowany jako U_port jeżeli nie został jeszcze wykorzystany do podłączenia lub nie ma z góry przypisanej roli w Fabricu.
N_port | Port węzła, niezdolny do utworzenia pętli (not loop-capable). Port końcowy dla hosta (serwera) wykorzystywany do podłączenia się do przełącznika FC.
NL_port | Port węzła, zdolny do utworzenia pętli (loop-capable). Wykorzystywany do podłączania urządzeń poprzez porty L_port i FL_port.

![Podstawowe porty w Fabricu](/SAN-DG/Grafiki/FCPorts.PNG)

### **Powyższa konfiguracja nie posiada bezpośredniego połączenia pomiędzy przełącznika.**
### Porty rozszerzające (Expansion port types)
Port | Opis
-----|-------
E_port | Port wykorzystywany w ISL do powiększania Fabrica.
EX_port | Port nie pozwala na łączenie Fabrics ale wspiera FC-NAT (Fibre Channel Network Address Translation). Wykorzystujemy ten port w celu podłączenia wieloprotokołowych routerów do Edge Fabrics.
VE_port | Wirtualny E_port, emulujący E_port i wykorzystujący protokół FCIP (Fibre Channel over Internet Protocol). Funckja VE_port jest dostępna w przypadku połączeń punkt-punkt.
VEX_port | Jest to zroutowany VE_port, ma taką samą funkcjonalność jak VE_port.
TE_port | Zapewnia funkcje standardowego E_port, dodatkowo pozwala na routing wielu wirtualnych sieci SAN (VSANs). Port zwany inaczej **Trunking E_port**.

![Fabric z portami typu rozszerzającego](/SAN-DG/Grafiki/FCExpPorts.PNG)

### **Inni producenci sprzętu stosują swoje rozwiązania dotyczące typów portów. Poniższa grafika przedstawia porty FC w urządzeniach firmy CISCO.**

![Porty FC w urządzeniach CISCO](/SAN-DG/Grafiki/FC-Cisco.PNG)

## 6. Protokoły
### FCIP - Fibre Channel over Internet Protocol - protokół pozwalający na wysyłanie pakietów Fibre Channel poprzez zwykłą sieć z wykorzystaniem protokołu IP. FCIP wykonuje enkapsulację ramki FC, i wysyła ją w pakiecie IP.

![Enkapsulacja w protokole FCIP](/SAN-DG/Grafiki/FCIP-Encapsulation.PNG)

###Podstawowym argumentem za wykorzystywaniem FCIP jest możliwość wysyłania danych do lokalizacji odległych, w sytuacji gdy odległość fizyczna wykracza poza możliwości Fibre Channel. Kolejnym argumentem "za" jest możliwość wykorzystania istniejącej infrastruktury sieciowej, bez konieczności rozbudowywania lokalnej infrastruktury SAN.
###Z uwagi na to, że FCIP tworzy tunel komunikacyjny pomiędzy dwiema lokalizacjami (podobnie jak Inter-switch links), Fabrics w dwóch odrębnych lokalizacjach zostają połączone ze sobą w jeden Fabric. Może to powodować problemy biznesowe, szczególnie gdy chcemy utrzymać podział Fabrics. Ponadto łącze może nie zawsze zapewniać stabilność parametrów połączenia, co może powodować problemy z utrzymaniem jakości usług.
### iFCP - Internet Fibre Channel Protocol - protokół dostarczający usługi Fabrica Fibre Channel dla urządzeń FC poprzez sieć TCP/IP. iFCP wykorzystuje TCP do zapobieganiu przeciążeniu sieci (congestion control), wykrywaniu błędów w transmisji danych (error detection) oraz odzyskiwaniu (recovery).
### Podstawowym celem iFCP jest wykorzystanie istniejącej infrastruktury sieciowej do rozszerzenia sieci SAN bez konieczności rozbudowywania sieci SAN. W iFCP, stos TCP/IP i jego infrastruktura zastępują infrastrukturę Fibre Channel. Jest to protokół brama-brama (router-router).
### Enkapsulacja w pakietach IP odbywa się podobnie jak w przypadku FCIP, za wyjątkiem nagłówka, który jest mapowany (odwzorowywany) w nagłówku IP, i danych sesji TCP.

![Enkpsulacja w iFCP](/SAN-DG/Grafiki/iFCP-encapsulation.PNG)

### SCSI - [SCSI](/scsi/scsi.md)
### iSCSI - [iSCSI](/iSCSI.md)
### FICON - Fiber Connectivity - protokół/interfejs, będący własnością intelektualną firmy IBM, wykorzystywany do połączeń komputerów typu Mainframe z urządzeniami storage. Następca **ESCON**, poprzedniego standardu do połączeń storage.
### FCoE - [FCoE](/FCoE.md)
### iSNS - Internet Storage Name Service - protokół służący do obsługi interakcji pomiedzy serwerami iSNS oraz klientami iSNS. Klienci iSNS to komputery (nazywane inicjatorami), które podejmują próby odnajdowania urządzeń magazynujących (nazywanych obiektami docelowymi) w sieci Ethernet. Protokół iSNS umożliwia zautomatyzowane odnajdowanie i konfigurowanie urzędzeń iSCSI oraz Fibre Channel (przy użyciu bram iFCP), a także zarządzanie nimi w sieci TCP/IP.     
## 7. Schemat adresowania
### WWN - World-wide Name - każde urządzenie FC posiada unikatowy identyfikator WWN. Podobnie jak karty Ethernet posiadają unikatowy adres MAC (Media Access Control address). Każdy N_port ma przypisany adres WWN, więc istnieje możliwość posiadania wielu WWN (posiadanie wielu interfejsów FC - m. in. kart HBA z portem, portów w urządzeniu sieciowym). WWN to adres o długości 64 bitów, i gdy dwa adresy WWN są umieszczone w nagłówku ramki FC - 16 bitów jest zarezerwowane dla identyfikacji adresu docelowego oraz adresu źródłowego.

![World Wide Name](/SAN-DG/Grafiki/WWN-Scheme.PNG)
##### IEEE definiuje dwa standardy WWN.

### WWNN - world-wide node name - adres o długości 64 bitów, globalnie unikatowy (przynajmniej w ramach sieci), przypisany do węzła lub urządzenia sieciowego (serwera, przełącznika). W przypadku serwera z dwoma kartami HBA, każda karta ma unikatowy adres WWNN. W przypadku przełącznika SAN, WWNN jest przypisany do urządzenia (obudowy - chassis). Dla urządzeń storage, WWNN może być przypisany do każdego kontrolera (w urządzeniu), a w przypadku urządzeń klasy high-end enterprise - do macierzy dysków.  
### WWPN - world-wide port name - jest unikatowym identyfikatorem dla każdego portu FC. Dla serwera, karta HBA może [posiadać więcej portów, kazdy z nich ma przypisany adres WWPN]. W przełączniku, każdy port FC urządzenia ma odrębny WWPN. W przypadku urządzeń magazynujących dane, każdy port hosta ma swój WWPN.

![WWPN-Serwer](/SAN-DG/Grafiki/WWPN-Serwer.PNG)

![WWPN-Switch](/SAN-DG/Grafiki/WWPN-Switch.PNG)

![WWPN-Storage](/SAN-DG/Grafiki/WWPN-Storage.PNG)

### **Jeżeli wykorzystywane są wirtualizatory Storage, WWNN może odnosić się do indywidualnej wirtualnej instancji zasobów Storage.**

![WWPN-Tapes](/SAN-DG/Grafiki/WWPN-Tapes.PNG)

##### WWNN oraz WWPN dla taśm

### Adres portu
### Routing wykorzystujący 64-bitowe adresy może być niewydajny i problematyczny, w sieciach Fibre Channel wykorzystuje się jeszcze inny schemat adresowania. Wykorzystywany do praktycznej komunikacji w FC-SW (Fibre Channel Switched Fabric).
### Każdy port w sieci FC ma swój unikatowy 24-bitowy adres, uzyskany m. in. poprze wykorzystywanie krótszego nagłówka. Taka konfiguracja przyspiesza routing w sieci. W schemacie adresowania, z adresami długości 24 bitów, jest możliwość wykorzystania 16 milionów adresów. W przeciwieństwie do sieci Internetowej, gdzie taka pula adresów została już wielokrotnie wyczerpana, pojedyncze sieci SAN nie posiadają tyle fizycznych i/lub wirtualnych portów.
### Z uwagi na wspomniany wcześniej schemat WWN, istnieje zależność pomiędzy tymi dwoma schematami adresacji. WWN jest przypisany do urządzenia/portu przez producenta. Adresacja 24-bitowa jest nadawana urządzeniom podłączanym do sieci, adresacja jest utrzymywana poprzez przełączniki. Przełącznik zachowuje korelację adres WWN z adresem 24-bitowym portu.
### **Name server** - komponent systemu operacyjnego fabrica, działający w przełączniku, jest to baza danych obiektów w których urządzenia podpinane do fabrica zapisują wartości. Koncepcyjnie jest to odpowiednik tablicy routingu.

![Schemat adresu portu - 24-bitowego](/SAN-DG/Grafiki/Adres-24.PNG)

### Istnieją dwie możliwości przypisywania adresów w sieci SAN, podobnie jak w sieciach LAN, **dynamicznie** i **statycznie**.

### 24 bitowy adres składa się z 3 części:
### 1. Domain (bity 23 - 16)
### Domena jest adresem przełącznika, może być statyczny lub dynamiczny. Adres statyczny jest wymagany dla połączeń FICON. Każdy producent ma zakres liczb i maksymalną liczbę identyfikatorów domenowych (domain IDs), które można wykorzystać w fabricu.
### Każdy bajt pozwala na 256 możliwych adresów, jednak należy pamiętać że część z nich jest już zarezerwowana np. adres rozgłoszeniowy (broadcast). Ostatecznie tylko 239 adresów jest możliwych do wykorzystania. Identyfikator domeny pozwala na identyfikację przełącznika.
### 2. Area (bity 15 - 08)
### Pole Area pozwala na stworzenie 256 adresów. Pole to pozwala na indentyfikację indywidualnego portu.
### 3. Port lub adres fizyczny w pętli z arbitrażem: AL_PA (bity 07 - 00)
### Pozwala na identyfikację podłączonych **N port's** lub **NL port's**.

### Liczba prawie 16 milionów adresów, bierze się z:
### **Domain x area x ports = 239 x 256 x 256 = 15 663 104 adresów**
### W sieciach SAN opartych na topologii Switched Fabric, wyróżnić można adresy powiązane z usługami w sieci Fibre Channel (tzw. well-known addresses):

Adres | Nazwa | Zastosowanie
------|-------|----------------------------------
0xFFFFF0 - 0xFFFFF4 | Zarezerwowane | Adresy zarezerwowane dla późniejszych zastosowań
0xFFFFF5 | Multicast server | Serwer multicast wykorzystywany usługach klasy 6. Fibre Channel
0xFFFFF6 | Clock Synchronization Server | Serwer wykorzystywany w usługach multicastowych klasy 6 Fibre Channel
0xFFFFF7 | Security Key Distribution Server | Serwer wykorzystywany przy dystrybucji kluczy szyfrowania
0xFFFFF8 | Alias Server | Serwer odpowiadający za przypisywanie adresów portów N do identyfikatorów grup Multicast i Hunt
0xFFFFF9 | Quality of Service Facilitator | Serwer odpowiadający za parametry jakości usług w klasie 4. FC
0xFFFFFA | Management Server | Serwer zbierający informacje o topologii sieci, stanach urządzeń i łączy, wspomaga administrację sieci
0xFFFFFB | Time Server | Serwer synchronizacji czasu dla urządzeń sieciowych
0xFFFFFC | Directory Server | Serwer odwzorowujący adresy 24-bitowe na adresy WWN i odwrotnie
0xFFFFFD | Fabric Controller | Serwer odpowiadajacy za routing ramek oraz powiadamianie o zmianach stanu urządzeń
0xFFFFFE | Fabric F_Port | Adres przypisywany wszystkim portom F, wykorzystywany do komunikacji z przełącznikiem
0xFFFFFF | Broadcast Address | Adres używany jako docelowy dla ramek adresowanych do wszystkich portów

### Na potrzeny topologii pętli z arbitrażem zarezerwowano parę adresów AL_PA:
Adres | Zastosowanie
------|-------------------------------
0x00 | Adres przyznawany portowi FL na etapie inicjalizacji pętli
0xF0 | Adres wykorzystywany w algorytmie sprawiedliwości (fairness algorithm) oraz na etapie inicjalizacji pętli (przy wyborze zarządcy pętli)
0xF1 - 0xF6 | Adresy zarezerwowane dla późniejszych zastosowań
0xF7 | Wartość wykorzystywana w sekwencji LIP w celu wskazania, że wysyłający ją port nie został zainicjowany (nie posiada adresu AL_PA)
0xF8 | Wartość wykorzystywana w sekwencji LIP w celu wskazania uszkodzenia pętli
0xF9 - 0xFE | Adresy zarezerwowane dla późniejszych zastosowań
0xFF | Adres broadcast (ramki wysłane na ten adres trafią do wszystkich portów pętli,
oprócz portu, który ramkę wysłał)

### **Loop Initialization Primitive - LIP**

### **Format adresu może się różnić w zależności od zastosowanej topologii.**
### **Adres FICON - adres FICON różni się co nieco od standardowego schematu.**
## 8. Inicjalizacja portów w FC
### 8.1. Fabric Login (FLOGI)
### Gdy podłączane jest urządzenie ***fabric-capable*** do przełącznika SAN, następuje Fabric Login.
### Inicjuje ono sesję połączenia pomiędzy dwoma urządzeniami. Sesja jest tworzona pomiędzy portami N_port (lub NL port), a przełącznikiem. N port wysyła ramkę FLOGI zawierającą nazwę swojego węzła (node name), nazwę swojego portu N port i parametry usługi na adres 0xFFFFFE (adres przypisywany wszystkim portom F, wykorzystywanu do komunikacji z przełącznikiem - **Fabric F port**).
### 8.2. Port Login (PLOGI)
### PLOGI jest wykorzystywany do nawiązania/zainicjowania sesji pomiędzy dwoma portami N (N_port, urządzeniami). Proces ten jest konieczny przed wykonanywaniem każdej operacji wyższego poziomu. W trakcie PLOGI dwa porty N wymieniają ze sobą informacje dotyczące parametrów usługi. 
### 8.3. Process Login (PRLI)
### PRLI jest wykorzystywany do stworzenia środowiska pomiędzy powiązanymi ze sobą procesami na porcie żródłowym N oraz decelowym portem N (odpowiadającym na komunikację z portu źródłowego).
###Procesy powiązane (related processes, grupa takich procesów nazywana jest wyrażeniem **image pair**.), to mogą być procesy systemowe, obrazy systemowe (np. Logical Partitions na Mainframe), procesy warstwy 4. FC (FC-4). Wykorzystywanie PRLI jest opcjonalne z punktu widzenia warstwy 2. FC (FC-2), jednak może być wymagane przez konkretną technologię operującą w wyższej warstwie np. mapowanie SCSI-FCP.
## 9. Fabric Services
### Zestaw usług dostępnych dla każdego urządzenia podłączonego do fabrica Fiber Channel.
### 9.1. Management Services - usługa odpowiedzialna za zbieranie informacji o topologii, adresach, wykorzystaniu i jakości łączy oraz błędach transmisji. Umożliwia dostęp, poprzez oprogramowanie zarządzające, do Simple Name Server (SNS), rozwiązując potencjalne problemy związane z **zoning**. Oprogramowanie zarządzające może mieć informacje o całej sieci SAN, wykorzystując tą usługę. Ułatwia to oczywiście monitoring oraz administrację. Dobrze znany port tej usługi to 0xFFFFFA.
### 9.2. Time Services - znane też jako **time server**, dostarcza informacje o aktualnym czasie urządzeniom w sieci, co pozwala zarządzać funkcjami które mają ograniczenie czasowe.
### Modelowo usługę można podzielić na dwa obiekty:
### Time Service Application - obiekt ten reprezentuje użytkownika łączacego się do serwera czasu
### Time Server - poprzez usługę time service dostarcza informację o aktualnej dacie i godzinie.
### 9.3. Simple Name Server - usługa, stale aktualizowana przez wszystkie przełączniki w fabricu - co powoduje, że "znają" one wszystkie urządzenia zapisane w SNS. Węzęł, po udanym zalogowaniu się do fabrica, wykonuje operację logowania portu (PLOGI, port login) na adres docelowy 0xFFFFFC. Proces ten pozwala węzłowi na zarejestrowanie się, i przekazanie krytycznych informacji (takich jak np. klasa usługi, jej parametry itp.). 
### 9.4. Login Services, Fabric Login Services - serwer odpowiedzialny za proces logowania do fabrica (FLOGI), dostępny pod adresem portu 0xFFFFFE.
### 9.5. Registered State Change Notification (RSCN) - usługa krytyczna dla prawidłowego funkcjonowania fabrica, propaguje ona informację na temat zmiany stanu węzłów w sieci SAN wszystkim pozostałym węzłom. Dzięki temu urządzenia nie próbują się stale komunikować z niedziałającymi węzłami.
### Węzły rejestrują się do kontrolera fabrica (fabric kontroler) specjalną ramką SCR (state change registration). Kontroler fabrica, utrzymujący stan sieci rozsyła komunikaty RSCN do wszystkich zarejestrowanych urządzeń, w przypadku każdej zmiany: np. usunięcia/dodania urządzenia, zmiany Zone, adres przełącznika się zmienił, nazwa się zmieniła. Adres kontrolera fabrica to port 0xFFFFFD.
### Wymienione wyżej usługi są zaimplementowane w przełącznikach i innych podobnych urządzeniach w sieci SAN. Wszystkie wymienione usługi są dostępne poprzez ramki warstwy 2. FC (FC-2), pod zarezerwowanymi adresami portów (well-known addresses).
## 10. Routing w sieciach SAN
### Rozbudowana sieć SAN, może zawierać w sobie wiele przełączników i innych urządzeń. Może nawet wykraczać poza sieć SAN i wykorzystywać połączenia do sieci LAN oraz WAN. Potrzebne są mechanizamy zapewniające QoS (Quality of Service) w nawet bardzo rozbudowanej sieci. 
### 10.1. Spanning Tree - szukanie najbardziej wydajnej ścieżki, wykorzystując liczbę przeskoków pomiędzy urządzeniami. Wykorzystywana jest tylko jedna ścieżka, pozostałe są zablokowane i wykorzystywane tylko gdy pierwotnie najkrótsza ścieżka staje się niemożliwa do wykorzystania. Najczęściej wykorzystywanym protokołem jest Fabric Shortest Path First (FSPF).     
### 10.2. Fabric Shortest Path First - wybór ścieżki następuje po zainicjowaniu urządzeń, nie jest on zmieniany poza przypadkami awarii urządzeń bądź podłączaniu nowych przełączników (nowe połączenia ISL).
### Protokół FSPF sprawdza koszt każdego łącza na przełącznikach w sieci. Koszt jest zawsze liczony w liczbie wymaganych skoków (hops, ilości urządzeń przez które musi przejść pakiet by dotrzeć do celu).
###Wybierany jest zawsze wariant najmniejszej liczby skoków. Przełącznik przechowuje ścieżki do innych przełączników w sieci w bazie topologii. Zwana jest ona inaczej Link State Database. Baza topologii jest utrzymywana na każdym przełączniku, ponadto jest synchronizawana pomiędzy przełącznikami gdy następują w niej zmiany. W przypadku obecności alternatywnych ścieżek, wybierana jest najmniej kosztowna (najmniejsza liczba skoków). 
### Jeżeli opóźnienie przy skokach jest takie samo, łącza pomiędzy przełącznikami mają taką samą prędkość oraz nie są przeciążone przez ruch sieciowy - FSPF wybierze najkrótszą ścieżkę.
### 10.3. Zoning - pozwala na dalszy podział sieci SAN (fabrica), przypisanie do zony pozwala udostępniać dany zasób tylko hostom przypisanych do tej zony.
### Przykład: Chcemy oddzielić środowisko Microsoft Server od środowiska UNIX. Windows Server stara się zainicjować wszystkie dostępne zasoby storage. Nie każde urządzenie magazynujące jest w stanie ochronić swoje zasoby przed próbą dostępu do danego zasobu.

![Zoning](/SAN-DG/Grafiki/Zoning.PNG) 

###Zoning może służyć do separacji zasobów dla środowisk wykonujących różne zadania, np. podział na środowiska testowe oraz produkcyjne. Może także służyć jako element systemu bezpieczeństwa, ograniczając dostęp do krytycznych zasobów.

### 10.4. Hardware Zoning - zoning opierający się na fizycznym numerze portu fabrica. Członkami danej zone, są porty fizyczne na przełączniku SAN. HZ można podzielić na konfigurację: jeden-do-jeden, jeden-do-wielu oraz wiele-do-wielu. 
### 10.5. Software Zoning - zoning utworzony za pomocą oprogramowania, dokładnie przez system operacyjny fabrica. Gdy port wysyła zapytanie do Serwera Nazw (Name Server), otrzymuje tylko informacje o portach w jego zdefiniowanej soft-zone (software-zone). Oczywiści jest zrobione na poziome oprogramowania, więc jeżeli nastąpi wysłanie ramki na niepoprawny port - ramka do niego dotrze. Definiując członków soft-zone możemy się posługiwać ich WWN (WWNN oraz WWNP).  
### 10.6. Logical Unit Number Masking - LUN Masking - Więcej niż jeden host może widzieć, a nawet zarządać dostępu (lub po prostu uzyskać dostęp) do konkretnego urządzenia magazynującego (LUNa). Logical Unit Masking służy do kontrolowania dostępu do LUNów dostepnych przez dane urządzenie magazynujące. Host może wysłać żądanie uzyskania dostępu do danego LUNa, i uzyskać dostęp jeżeli jest na liście dostępowej dla danego LUNa (podobnie jak Access Control Lists).
### **LUN - Logical Unit Number** 
### Termin pierwotnie kategoryzował obiekt SCSI, wykonujący operacje I/O (Input/Output) - np. dysk. Współcześnie macierz storage, może mieć wirtualne dyski udostępnione jako zasoby dla hostów (serwerów). W tym przypadku każdy wirtualny dysk może mieć swój LUN. 
## 11. Podstawowe urządzenia SAN
### 11.1. HBA - Host Bus Adapter - odpowiednik karty NIC w sieciach TCP/IP.
![Karta HBA](/SAN-DG/Grafiki/hba.jpg)
### 11.2. Fibre Channel Bridge - pozwala na integrację tradycyjnego urządzenia SCSI z siecią Fibre Channel. Mostki są uznawane za urządzenia historyczne, z uwagi na to że nie zapewniały nic poza przesyłaniem informacji między różnymi protokołami komunikacyjnymi.
### 11.3. Huby
###Niezarządzalne huby służą jako koncetratory okablowania, wspierają topologię pętli z arbitrażem. Zarządzalne Huby mają dodatkowo opcję konfiguracji oraz wspierają wykorzystanie SNMP (Simple Networking Management Protocol) do zarządzania zdalnego.
### W topologii pętli z arbitrażem (FC-AL) huby mogą wspierać konfiguracje, które bazują wykrywaniu czy dany port jest aktualnie zagospodarowany (czy wtyczka jest do niego wpięta) - jeżeli nie, jest on wyłączany.
### Przełącznik Hub (switched hub) - wykorzystywane jako urządzenia z których można zbudować wewnętrzną pętle z arbitrażem dla podpiętych do niego urządzeń. Jednocześnie mogą one korzystać z pełnej przepustowości Fibre Channel (w przeciwieństwie do współdzielonej przez wszystkie urządzenia przepustowości).       
### 11.3. FC-Switch - Fibre Channel Switch - przełącznik FC.
![SAN Switch](/SAN-DG/Grafiki/san-switch.jpg)
### 11.4. FC-Director - zestaw urządzeń (przełączników i innych urządzeń) zamknięty w jednej obudowie. Może służyć jako np. Core-Switch. Director-switch to w dużym uproszczeniu serwer z zestawem przełączników SAN, być może awaryjnym zasilaniem i wirtualizatorami Storage. Urządzenie ma zapewnioną redundancję sprzętową: chłodzenie, procesory, awaryjne zasilanie. Zapewnia modułowość i wymianę komponentów bez wyłączania urządzenia (w locie, podobnie jak komputery klasy Mainframe).
![SAN Director](/SAN-DG/Grafiki/san-director.png)
### 11.5. Wieloprotokołowe routery - pozwalają na komunikację urządzeń w odrębnych sieciach SAN na komunikację bez konieczności łączenia fabrics. Wspierają one takie protokoły jak: FCP, FCIP, iFCP, iSCSI, IP.
### 11.6. Moduły rozszerzające - do niektórych urządzeń (np. Director-class switch) można dokupywać moduły rozszerzające ich funkcjonalność.
### 11.7. Multipleksery (multiplexers) - pozwalają na wysyłanie wielu sygnałów przy pomocy jednego fizycznego łącza.
## 12. Źródła
####	12.1. [FICON](http://searchstorage.techtarget.com/definition/FICON)
####	12.2. [FICON, wikipedia](https://en.wikipedia.org/wiki/FICON)
####	12.3. [iSNS, wikipedia](https://en.wikipedia.org/wiki/Internet_Storage_Name_Service)
####	12.4. [iSNS, w wersji Microsoft](https://technet.microsoft.com/pl-pl/library/cc772568(v=ws.11).aspx)
####	12.5. [Introduction to Storage Area Networks, RedBook](http://www.redbooks.ibm.com/redbooks/pdfs/sg245470.pdf)
####    12.6. [Differentiating Fibre Channel logins](http://www.redbooks.ibm.com/abstracts/tips0035.html?Open)
####    12.7. [Praca dyplomowa Krzysztofa Bożyka](http://zskl.p.lodz.pl/~morawski/Dyplomy/Praca%20dyplomowa%20p.%20Bozyka.pdf)
####    12.8. [Director-class switch](http://searchstorage.techtarget.com/definition/Fibre-Channel-director-FC-director)






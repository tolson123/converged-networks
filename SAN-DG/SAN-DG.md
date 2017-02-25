# SAN - Storage Area Network

##1. Podstawowe informacje o SAN. 
####  * SAN jest typem sieci komputerowej, której celem jest udostępnianie zasobów takich jak macierze dyskowe (storage) dla serwerów w ramach organizacji.
####  * Jest to dedykowany typ sieci, do której zazwyczaj nie ma dostępu z sieci LAN organizacji. SAN ma własne dedykowane urządzenia sieciowe.
####  * Zazwyczaj jest to storage typu blokowego.
####  * Według [Storage Network Industry Association](http://www.snia.org/about) głównym celem SAN jest tranfer danych pomiędzy systemami komputerowymi, a urządzeniami storage.
##2. Podstawowe topologie SAN
![Topologie SAN](/SAN-DG/Grafiki/San-Top.PNG)
####  1. Point-to-Point (Punkt-Punkt).
#####    Najprostsza topologia sieci SAN, wykorzystywana do podłączania ze sobą dwóch węzłów (urządzeń). Zakładamy, że nie będziemy skalować infrastruktury poziomo (vertical scaling) - czyli nie będą podłączane nowe urządzenia (węzły).
#####    Przepustowość łącza nie jest współdzielona pomiędzy urządzeniami, więc wykorzystywana jest ona w pełni na potrzeby komunikacji pomiędzy połączonymi węzłami.
#####    Łącze działa trybie pełnego dupleksu - komunikacja może odbywać się jednocześnie w dwóch kierunkach.
####  2. Arbitrated loop (pętla z arbitrażem).
#####    Zwana inaczej siecią FC-AL (Fiber Channel - Arbitrated Loop). Topologia tego typu nie wymaga dodatkowych urządzeń sieciowych takich jak przełączniki SAN. Wszystkie urządzenia połączone są ze sobą w pętlę. Komunikacja odbywa się pomiędzy kolejnymi urządzeniami w pętli, to oznacza że wszystkie urządzenia muszą działać przy tej samej przepływności (channel capacity). Inaczej mówiąc, sieć działa z najwyższą przepływnością najwolniejszego elementu pętli.
![FC-AL](/SAN-DG/Grafiki/FC-AL.PNG)
#####    Z uwagi na ograniczenia adresowe w pętli nie może być w niej więcej niż 126 urządzeń - zarządzane są one jako jedna współdzielona szyna transmisji. Ruch odbywa się w jednym kierunku przekazując ramki przez kolejne elementy pętli. Protokół arbitrażu pozwala na ustanowienie jednego połączenia między nadawcą i odbiorcą, kiedy komunikacja zostaje zrealizowana pomiędzy dwoma portami następuje zwolnienie pętli i może być ustanowione nowe połączenie pomiędzy dwoma portami w pętli. Pętle można skonfigurować z Hubami w celu ułatwienia zarządzania połączeniami. Dystans do 10 km jest wspierany przez standard Fibre Channel, jednak długość pętli wpływa na opóżnienia w komunikacji.  
####  3. Switched Fabric (pełna sieć - tzw. Fabric)
##### Najbardziej przydatna topologia, wykorzystująca przełączniki i inne urządzenia sieciowe. Zwana inaczej Fibre Channel Switched Fabric (FC-SW). Fabric ma przynajmniej jeden przełącznik SAN w ramach swojej konfiguracji. Przełączany Fabric zapewnia pełną szerokość pasma w medium transmisyjnym (bandwidth) na każdy port w porównaniu ze współdzieloną szerokością pasma w przypadku implementacji pętli z arbitrażem.
![FC-SW](/SAN-DG/Grafiki/FC-SW.PNG)
##### Najważniejszą różnicą pomiędzy FC-AL, a FC-SW jest to że dodanie nowego urządzenia w FC-AL powoduje dalszy podział współdzielonej szerokości pasma. W przypadku FC-SW przepustowość pasma w medium transmisyjnym zostaje zwiększona. Powoduje to stopniowe odchodzenie od topologii FC-AL.
#### Tradycyjne topologie FC-SW
#####Pojedynczy przełącznik (single switch) - urządzenie podpięte są do jednego przełącznika FC.
![Single Switch](/SAN-DG/Grafiki/FC-SW-Single.PNG)
#####Pierścień (ring) - przełączniki są podłączone ze sobą, przełączniki na początku i na końcu kolejki mają dodatkowe połączenie zamykające pierścień.
![Ring topology](/SAN-DG/Grafiki/FC-SW-Ring.PNG)
#####Kaskadowa (Cascade) - przełączniki są podłączone ze sobą (w kolejce).
![Cascade topology](/SAN-DG/Grafiki/FC-SW-Cascade.PNG)
#####Topologia Siatki (Mech topology) - każdy przełącznik jest podłączony fizycznie do pozostałych przełączników w sieci (zapewnia redundancje połączeń).
![Mesh topology](/SAN-DG/Grafiki/FC-SW-Mesh.PNG)
#### Topologie warstwowe.
#####Edge-Core - urządzenia pamięci masowej podłączone są do urządzenia głównego (centralnego, w jądrze sieci).
![Core-Edge](/SAN-DG/Grafiki/FC-Core-Edge.PNG)
##### Edge-Core-Edge - urządzenia pamięci masowej moga być podłączone do urządzeń wyższej warstwy sieci. W tym przypadku są to przełączniki brzegowe.
![Edge-Core-Edge](/SAN-DG/Grafiki/FC-Edge-Core-Edge.PNG)
##### Edge Switch (przełącznik brzegowy) - przełącznik znajdujący się na brzegu sieci, umożliwiający komunikację pomiędzy innymi sieciami, może być to komunikacja z hostami lub innymi Fabricami.
##### Obydwie wspomniane wyżej architektury mogą opisywać więcej "podsieci FC" - **subfabrics**. W przypadku architektury Core-Edge może istnieć podział na Core Fabric oraz na Edge Fabrics. W **Edge-Core-Edge** oraz **Core-Edge** można izolować zasoby od hostów (serwerów). Zasoby dyskowe są podłączone do innego Fabrica niż serwery - może to służyć łatwiejszej i bezpieczniejszej administracji infrastrukturą SAN. 

## 3. Fibre Channel
### Warstwy Fibre Channel:
Warstwa | Opis
--------|---------
FC0 | Warstwa fizyczna - stardard zastosowanego okablowania, jego cechy. W przypadku FC stosujemy okablowanie światłowodowe oraz miedziane.
FC1 | Warsta łącza danych (Data-Link). Odpowiedzialna za obsługę odpowiedniego schematu kodowania (encoding scheme) dla danego łącza. 
FC2 | Warstwy odpowiedzialna za zarządzanie parametrami transferu danych - podział danych na ramki (*Framing Protocol*), wielkość pojedyńczej ramki danych (flow control), port/adres docelowy dla tej ramki. Wartswa ta zawiera definicje klas usługi - wybieranych zależności od wymagań które musi spełnić system. Warstwa ta zajmuje się definiowaniem funkcji dla transmisji z wykorzystaniem pojedynczego portu.
FC3 | Warstwa ta definiuje zaawansowne funkcje takie jak stripping (tranfer danych przy pomocy wielu łączy), multicast (wielu odbiorców), hunt group (przypisanie wielu portów do jednego węzła). Warstwa ta definiuje funkcje transmisji wykorzystujące wiele portów.  
FC4 | Umożliwia współpracę FC z innymi protokołami takimi jak np. IP, SCSI, FCP, FICON. 
![Warstwy Fiber Channel](/SAN-DG/Grafiki/FC-Layers.PNG)
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
![Schemat ramki Fiber channel](/SAN-DG/Grafiki/FC-frame.PNG)

####Elementy ramki FC:
#### SOF (Start of Frame), Nagłówek FC, Blok danych SCSI, Cyclic Redundancy Check, End of Frame delimeter;      
## 4. Fabric
#### Fabric - sieć urządzeń (np. przełączników FC) zapewniająca dostęp do danych. Dane znajdują się na urządzeniach pamięci masowej podłączonych w ramach Fabrica.
## 5. Porty
### **Port jest podstawowym elmentem sieci opartej na Fiber Channel.**
Port | Opis
-----|------
F_port | Wykorzystywana do połączenia się z portem typu N_port (node port), połączenie punkt-punkt z przełącznikiem.
FL_port | Port pętli, wykorzystywana do podłączenia się do portu NL_port (node loop port). Porty pętli wykorzystywane są w rozwiązaniach typu pętla z arbitrażem.
TL_port | Port w urządzeniach firmy CISCO wykorzystywany do podłączenia urządzeń nierozpoznających Fabrica (non-fabric aware) w prywatnych pętlach urządzeń. Translative loop port.
G_port | port typu rodzajowego (generic), może pracować jako expansion port (E_port) lub jako F_port. Port jest definiowany jako G_port jeżeli nastapiło połączenie ale nie otrzymano potwierdzenia inicjalizacji pętli (look initialization) lub nie ukończono inicjalizacji pętli z najbliższym urządzeniem Fiber Channel.
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
EX_port | Port nie pozwala na łączenie Fabrics ale wspiera FC-NAT (Fiber Channel Network Address Translation). Wykorzystujemy ten port w celu podłączenia wieloprotokołowych routerów do Edge Fabrics.
VE_port | Wirtualny E_port, emulujący E_port i wykorzystujący protokół FCIP (Fiber Channel over Internet Protocol). Funckja VE_port jest dostępna w przypadku połączeń punkt-punkt.
VEX_port | Jest to zroutowany VE_port, ma taką samą funkcjonalność jak VE_port.
TE_port | Zapewnia funkcje standardowego E_port, dodatkowo pozwala na routing wielu wirtualnych sieci SAN (VSANs). Port zwany inaczej **Trunking E_port**.
![Fabric z portami typu rozszerzającego](/SAN-DG/Grafiki/FCExpPorts.PNG)

Inni producenci sprzętu stosują swoje rozwiązania dotyczące typów portów. Poniższa grafika przedstawia porty FC w urządzeniach firmy CISCO.

![Porty FC w urządzeniach CISCO](/SAN-DG/Grafiki/FC_Cisco_ports.PNG)

## 6. Protokoły
### FCIP - Fiber Channel over Internet Protocol - protokół pozwalający na wysyłanie pakietów Fiber channel poprzez zwykłą sieć z wykorzystaniem protokołu IP. FCIP wykonuje enkapsulację ramki FC, i wysyła ją w pakiecie IP.
![Enkapsulacja w protokole FCIP](/SAN-DG/Grafiki/FC-Encapsulation.PNG)
####Podstawowym argumentem za wykorzystywaniem FCIP jest możliwość wysyłania danych do lokalizacji odległych, w sytuacji gdy odległość fizyczna wykracza poza możliwości Fiber Channel. Kolejnym argumentem "za" jest możliwość wykorzystania istniejącej infrastruktury sieciowej, bez konieczności rozbudowywania lokalnej infrastruktury SAN.
####Z uwagi na to, że FCIP tworzy tunel komunikacodrębnychyjny pomiędzy dwiema lokalizacjami (podobnie jak Inter-switch links), Fabrics w dwóch odrębnych lokalizacjach zostają połączone ze sobą w jeden Fabric. Może to powodować problemy biznesowe, szczególnie gdy chcemy utrzymać podział Fabrics. Ponadto łącze może nie zawsze zapewniać stabilność parametrów połączenia, co może powodować problemy z utrzymaniem jakości usług.
### iFCP - Internet Fiber Channel Protocol - protokół dostarczający usługi Fabrica Fiber Channel dla urządzeń FC poprzez sieć TCP/IP. iFCP wykorzystuje ...    
# 7. Schemat adresowania
### WWNN
### WWPN
### Adres portu

## 8. Inicjalizacja portów w FC
## 9. Fabric Services
## 10. Routing w sieciach SAN




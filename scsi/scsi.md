# SCSI #
**SCSI** (**Small Computer System Interface**) - SCSI jest równoległą magistralą danych której przeznaczeniem jest 
przesył danych między urządzeniami.

System SCSI jeszcze nie tak dawno wykorzystywany był przeważnie w wysokiej klasy serwerach i stacjach roboczych.
Obecnie nie jest on już tak często używany i jest wypierany przez nowe interfejsy **SAS**
nowsze komputery wykorzystują obecnie standard Serial ATA III

## Właściwości SCSI ##
Wszystkie urządzenia podłączone za pomocą magistrali SCSI są równorzędne dzieki czemu każde z nich może pełnić
zarówno rozpoczynać operację(Inicjator) jak i wykonywać operację zleconą przez innego inicjatora
jednak nie wszystkie urządzenia potrafią działać w tym trybie u mogą wykonywać jednocześnie tylko jedną z tych ról

![Terminator SCSI](/scsi/terminator SCSI.png)


Każde urządzenie podłączone do magistrali SCSI otrzymuje swój unikatowy identyfikator (**SCSI ID**).
Pierwotnie adresowanie urządzeń było wykonywane przez tylko 3 bity magistrali co umożliwiało połączenie ze sobą maksymalnie 3
urządzeń. Obecnie gdy magistrala danych rozrosła się do szerokości **16 bitów** powiękrzeniu uległa również część magistrali 
odpowiadająca za adresowanie, została ona zwiększona do 4 bitów.

**SCSI ID** pełni również rolę priorytety przy rozstrzyganiu próby jednoczesnego dostępu przez wiele urządzeń do magistrali.
W obrębie jednego identyfikatora **SCSI ID** wykorzystywany jest również tzw. **Logical Unit Number** (**LUN**)
identyfikujący ilość urządzeń logicznych na jakie może być podzielone fizyczne urządzenie SCSI, Jednym z przykładów takiego
urządzenia jest zmieniarka płyt CD, drukarki, czy nagrywarki.

Magistrala SCSI umożliwia podłączenie jednego dysku do wielu komputerów w tzw **układzie V**.
możliwy dzięki magistrali SCSI jest również przesył danych między urządzeniami bez ingerencji komputera poprzez wykonanie
macierzy dyskowej na taśmie magnetycznej.

## Parametry ##
**Magistrale SCSI**  można podzielić ze względu na sposób transmisji, jej prędkość, szerokości magistrali 
oraz parametry elektryczne. Poniżej przedstawiam szczegółowy podział:

1. **Sposób transmisji.**

    * synchroniczny
    * asynchroniczny

2. **Prędkość transmisji.**

    * 5 MB/s
    * 10 MB/s
    * 20 MB/s
    * 40 MB/s
    * 80 MB/s
    * 160 MB/s
    * 320 MB/s
    * 640 MB/s

3. **Szerokość magistrali.**

    * 8 bitów 
    * 16 bitów

4. **Parametry elektryczne**

    * sterowanie napięciowe SE (Single Ended)
    * sterowanie różnicowe wysokonapięciowe HVD (High Voltage Differential ) - 5V, długość kabla do 25m
    * sterowanie róznicowe niskonapięciowe LVD (Low Voltage Differential) - 3.3V, długość kabla do 12m

## Odmiany SCSI ##

* __SCSI-1__ :Pierwsza wersja standardu, posiada złącze Centronics 50 stykowe, wersja ta pozwalała na transfer z prędkością 5MB/s 
              na maksymalną odległość 6 metrów

* __SCSI-2__ :Wprowadzony został w 1994 roku. Kolejna wersja standardu, posiadała ona dwa warianty. Fast SCSI na złączu centronics 50 stykowym 
              pozwalającym na transfer rzędu 10 MB/s 
              oraz Fast Wide SCSI na złączu 50 lub 68 stykowym o maksymalnej prędkości transferu 20 MB/s. 
              maksymalna odległość obu wariantów to 3 metry.

* __SCSI-3/Ultra SCSI__ :swą premierę miał w roku 1996 Zwany również Ultra SCSI lub Fast20- również posiadał 2 warianty, 
20 MB/s na 50 stykowym złączu oraz 40MB/s na złaczu 68 stykowym. odległość maksymalnie 1,5 metra 

* __Ultra 2 SCSI__ :jest wersją przełomową w technologii SCSI,zwany też SCSI 40- zaprezentowany w roku 1997 tak 
jak poprzednik dostępny był w 2 wariantach Ultra2 SCSI na klasycznym
              złączu 50 stykowym z transferem 40MB/s oraz Ultra2 Wide SCSI o transferze 80 MB/s ze złączem 68 stykowym.
               w tej wersji zastosowane zostało nowe sterowanie przesyłem danych, sterowanie niskonapięciowe LVD 
              dzięki czemu zwiękrzono długość kabla do 12 metrów.
* __Ultra 3 SCSI__ :(Ultra- 160 SCSI) maksymalny transfer 160 MB/s, dodano funkcje wspomagające wykrywanie i usuwanie przekłamań. 68- lub 80-stykowe złącze.
* __Ultra 4 SCSI__ :(Ultra- 320 SCSI) maksymalny transfer 320 MB/s. 68- lub 80-stykowe złącze.
* __Ultra 5 SCSI__ :(Ultra- 640 SCSI) maksymalny transfer 640 MB/s.

poniżej przedstawiam tabele rozpisującą rodzaje SCSI 

![tabela rodzajów SCSI](/scsi/tabelaSCSI.png)

większość rodzajów SCSI jest ze sobą wzajemnie kompatybilna i można je ze sobą łączyć za pomocą odpowiednich przejściówek, 
ważne podczas łączenia wielu urządzeń jest sprawdzenie w jakim trybie one pracuje.
jeżeli choć jedno urządzenie będzie działało tylko w trybie SE całe połączenie przełączy się na tryb SE jeżeli magistrala to potrafi,
 w przeciwnym wypadku połączenie nie będzie działać.
oznaczenie w jakim trybie pracuje dane urządzenie zwykle widnieje na logo SCSI.
poniższa grafika przedstawia oznaczenia.

![tryby SCSI](/scsi/tryby.png)

urządzenie z oznaczeniem trzecim: LVD/SE potrafi samodzielnie zmienić tryb pracy z LVD na SE, jeżeli połączymy urządzenia SE z 
urządzeniem o oznacziu tylko LVD połączenie to nie zadziała.



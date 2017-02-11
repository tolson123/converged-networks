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


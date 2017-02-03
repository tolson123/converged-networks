# Systemy RAID

RAID (ang. Redundand Array of Independent Disks) to sposób połączenia dwóch lub większej ilości dysków twardych w jedną macierz, która zapewnia dodatkową funkcjonalność w porównaniu z oddzielnie podłączonymi pojedynczymi dyskami twardymi. 

Macierze RAID są powszechnie stosowane w rozwiązaniach serwerowych, dzięki nim uzyskujemy:
- zwiększenie prędkości transmisji w porównaniu z pojedynczym dyskiem
- odporność na awarie
- zależnie od rodzaju pamięć widoczna jako jedno urządzenie

#### Rodzaje macierzy RAID:
##### RAID 0

Ta macierz charakteryzuje sie przyśpieszeniem pracy systemu. W RAID 0 łączymy ze sobą dwa (lub więcej) dyski fizyczne w jeden logiczny napęd. Przykładowo łącząc ze sobą dwa dyski po 500 GB, otrzymamy jeden dysk wielkości 1000 GB, a dane będą zapisywane jednocześnie na obu dyskach, co znacznie przyśpieszy prędkość i odczyt danych. Wadą RAID 0 jest to, że dane nie są zabezpieczone w żadnen sposób. Jeśli jeden dysk ulegnie uszkodzeniu, traci się wszystkie dane.

Zalety:

- zwiększona prędkość zapisu/odczytu (prawie podwójnie)
- wykorzystanie całej pojemności dysku doi zapisu

Wady:

- brak odporności na awarie dysku
- łatwość utraty danych

Zastosowania:

- zwiększenie szybkości operacji dyskowych na stacjach roboczych
- obróbka dużych plików multimedialnych
- dysk do przechowywania instalacji gier komputerowych

![Raid0](http://www.kylos.pl/wp-content/uploads/2014/06/RAID_0.png)

#####  RAID 1

Macierz RAID 1 składa się również z dwóch dysków twardych połączonych ze sobą. Ale w przeciwieństwie do RAID 0, dane na dyskach są zapisywane równolegle na każdym dysku. Czyli towrzy się tak jakby lustro (mirror) danych. Jest to podstawowe zabezpieczenie przed utratą danych - jeśli jeden z dysków ulegnie awarii, wtedy system nadal może działać, gdyż takie same dane są na drugim działającym dysku. Utworzona macierz ma pojemność równą wielkości najmniejszego dysku.

Zalety:

- odporność na awarię pojedynczego dysku

Wady:

- macierz ma pojemnośc najmniejszego dysku
- prędkość operacji zapisu/odczytu jest na poziomie najwolniejszego dysku

Zastosowania:

- miejsce pod instalację systemu operacyjnego serwera
- kopie zapasowe
- ważne dane


![Raid1](http://www.kylos.pl/wp-content/uploads/2014/06/RAID_1.png)

##### RAID 2

Do utworzenia tego typu macierzy potrzebne są minimum 3 dyski twarde. Dane na dyskach są dzielone na poziomie bitów i zapisywane jednoczenie na dwóch dyskach. Trzeci dysk przechowuje informacje o dotyczące korekcji błędów generowane za pomocą kodu Hamminga. Macierz jest odporna na awarię jednego z dysków. Ten rodzaj macierzy jest przestarzały i obecnie nieużywany. Został wyparty przez rozwiązania typu RAID 5 i 6. 

Zastosowania:

- obecnie brak
- wyparte przez lepsze rozwiązania w postaci RAID 5 i 6

![RAID2](https://upload.wikimedia.org/wikipedia/commons/b/b5/RAID2_arch.svg)

##### RAID 3
W RAID 3 dane na dyskach przechowywane są na n-1 dyskach. Natomiast jeden z dysków przechowuje tzw. sumy kontrolne obliczane przed dedykowany procesor. Dlatego do spięcia dysków w ten sposób wykorzystywana jest odrębna karta sprzętowa RAID, aby cała operacja nie obciążała procesora głownego komputera. Zasada działania tej konfiguracji przypomina RAID 0 z tą różnicą, że awarii może ulec jeden z dysków, którego dane zostaną odczytane z sum kontrolnych, kosztem szybkości.

Zastosowania:

- obecnie brak
- wyparte przez lepsze rozwiązania w postaci RAID 5 i 6

![RAID3](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f9/RAID_3.svg/675px-RAID_3.svg.png)
##### RAID 4

RAID 4 działa na podobnej zasadzie co RAID 3. Z tą różnicą, że dane są zapisywane na segmenty liczące 16, 32, 64, lub 128 kB. Ta metoda przydatna jest przy przechowywaniu plików o dużych rozmiarach.

Zastosowania:

- obecnie brak
- wyparte przez lepsze rozwiązania w postaci RAID 5 i 6

![Raid4](http://www.kylos.pl/wp-content/uploads/2014/06/RAID_4.png)


##### RAID 5

Bardzo popularna metoda łączenia dysków w macirze stosowana w środowiskach serwerowych. Do RAID 5 potrzebne są co najmniej 3 dyski twarde, na których zapisywane są dane wraz sumami kontrolnymi. Np. łącząc 3 dyski po 500GB otrzymamy pojemność 1000GB. Gdy uszkodzi się jeden z dysków, system nadal będzie działał.

Zalety:

- odporność na awarię jednego z dysków
- wyższa prędkość zapisu/dczytu w porównianiu z RAID 1
- tracona jest pojemność jednego dysku w macierzy

Wady:

- niższa wydajność od RAID 0 spowodowana koniecznością wyliczania parzystości dla każdego bloku danych

Zastosowania:

- storage dla baz danych
- archiwizacja
- magazyn danych dla aplikacji

![Raid5](http://www.kylos.pl/wp-content/uploads/2014/06/RAID_5.png)





##### RAID 6


RAID 6 to rozbudowana wersja RAID 5, gdyż pojemność tej macierzy wynosi n-2 razy pojemność najmniejszego z dysków. Na dysku zapisywane są dwie sumy kontrolne, więc awarii mogą ulec aż dwa HDD bez uszczerbku w działaniu systemu.

Zalety:

- odporność na awarię dwóch dysków
- wyższa prędkość zapisu/dczytu w porównianiu z RAID 1
- tracona jest pojemność dwóch dysków w macierzy

Wady:

- niższa wydajność od RAID 0 spowodowana koniecznością wyliczania parzystości dla każdego bloku danych

Zastosowania:

- storage dla baz danych
- archiwizacja
- magazyn danych dla aplikacji
- rozwiązania wysokiej dostępności

![Raid6](http://www.kylos.pl/wp-content/uploads/2014/06/RAID_6.png)


##### RAID 0+1

Jest to kobinacja dwóch pierszych rodzajów macierzy. Dwie macierze RAID 0 połączone są ze sobą przez RAID 1, dzięki czemu łączymy zalety obydwu sposobów. Macierz ta jest dwukrotnie szybsza i bezpieczna. Uszkodzenie jednego z dysków nie powoduje utraty danych, a cała macierz automatycznie przekształca się w RAID 0.

Zalety:

- szybkość RAID 0
- prostsza w działaniu i implementacji od rozwiązań z parzystością (RAID 5, 6)

Wady:

- większy koszt przechowywania danych w porównaniu do poprzednich rodzajów macierzy
- lepszym wyoborem jest RAID 1+0

Zastosowania:

- szybkie magazyny danych
- serwery aplikacji

![Raid0+1](http://www.kylos.pl/wp-content/uploads/2014/06/RAID_01.png)


##### RAID 1+0

Na pierwszy rzut oka ta macierz jest podobna do RAID 0+1 i rzeczywiśćie jest w tym sporo prawdy. Charakteryzuje sie również bezpieczeństwem danych i zwiększoną szybkością, ale trochę inną filozofią działania. Nawet gdy dwa dyski z różnych mirrorów (RAID 1) ulegną awarii, macierz nadal będzie działać.

Zalety:

- szybkość RAID 0
- prostsza w działaniu i implementacji od rozwiązań z parzystością (RAID 5, 6)

Wady:

- większy koszt przechowywania danych w porównaniu do poprzednich rodzajów macierzy

Zastosowania:

- szybkie magazyny danych
- serwery aplikacji
- magazyny danych maszyn wirtualnych

![Raid1+0](http://www.kylos.pl/wp-content/uploads/2014/06/RAID_10.png)


##### RAID sprzętowy

Sprzętowe kontrolery RAID posiadają procesor dla obliczeń wszystkich operacji RAID, przez co nie jest generowane dodatkowe obciążenie dla procesora przez obliczenia RAID.

![RYS](http://www.powerserver.pl/images/LSI_SAS9280-8e_03_1.jpg)

##### RAID programowy

Programowy RAID nie wymaga kontrolera RAID, mogą zostać wykorzystane normalne kontrolery pamięci masowej SATA lub SAS bez funkcjonalności RAID (np. kontroler SATA, który jest zintegrowany w chipsecie płyty głównej). Funkcjonalność RAID jest kompletnie realizowana przez system operacyjny (np. Windows lub Software RAID w Linuksie). Obliczenia wszystkich operacji RAID są realizowane przez procesor komputera (nie przez dedykowany procesor kontrolera sprzetowego)



## Źródła:
[Pierwsze](http://www.powerserver.pl/d6387_sprzetowy_kontroler_raid__a_wydajnosc_serwera..html)
[Drugie](https://en.wikipedia.org/wiki/RAID#Software-based_RAID)
[Trzecie](https://www.thomas-krenn.com/pl/wiki/Podstawowe_informacje_o_kontrolerach_RAID#cite_note-3)
[Czwarte](https://en.wikipedia.org/wiki/Standard_RAID_levels)
[Piąte](https://www.kylos.pl/blog/co-to-jest-raid-roznice-miedzy-raidem-sprzetowym-i-programowym)




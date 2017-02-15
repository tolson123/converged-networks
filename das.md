
#DAS (Direct Attached Storage)

### Czym  jest DAS?

Bezpośrednio podłączana przestrzeń dyskowa – Czyli DAS, była pierwszym rodzajem platformy sieciowej służącej do przechowywania danych. Mimo konkurencji ze strony NAS i SUN nadal występuje w powszechnym użyciu.


Jest to rozwiązanie w którym każdy serwer posiada dedykowaną pamięć masową podłączoną bezpośrednio poprzez jeden z interfejsów SCFI(Small Computer Systems Interface) lub FC(Fibre Channel.) 

![enter image description here](http://winfwiki.wi-fom.de/images/thumb/e/eb/DAS.gif/350px-DAS.gif)

Dzięki kontrolerowi HBA (Host Bus Adapter) DAS może obejmować jeden lub więcej dysków połączonych z serwerem które mogą pracować w układzie RAID. Operacje odczytu/zapisu związane m.in. z kopiami bezpieczeństwa, odtwarzaniem czy archiwizacją przeprowadzane są bezpośrednio na podłączony zasób. Zasób ten nie jest współdzielony a dostęp do niego posiada tylko serwer do którego jest on podpięty.



###Zastosowanie
Rozwiązanie DAS może być stosowane w przypadku, gdy chcemy zbudować infrastrukturę złożoną z kilku serwerów o ściśle zdefiniowanej, wymaganej pojemności pamięci masowej i nie planujemy jej dalszej rozbudowy w przyszłości.

![enter image description here](http://www.storagesearch.com/auspexfig_01.gif)

Serwery oprócz swojej podstawowej funkcji udostępniania, często używane są również do zarządzania różnymi aplikacjami takimi jak email, pakiety rachunkowe, aplikacje bazodanowe. Każda z nich wymaga dostępu na poziomie blokowym (możliwość dostępu do bloków danych wewnątrz pliku, takich jak konkretne rekordy lub pola), zamiast dostępu z poziomu plików (możliwość dostępu do wszystkich plików danych, takich jak arkusz kalkulacyjny lub edytor tekstu). 



### Zalety...
- Niski koszt początkowy-. Pierwsza inwestycja w serwer i dodatkową pamięć masową jest w stanie zaspokoić potrzeby małych organizacji przez pewien czas. Dochodzi do tego łatwość implementacji.
- Wysoka wydajność – Dzięki dedykowanym zasobom na każdy serwer .

 ###...Wady
- Słaba skalowalność – Jest temu winien  kontroler HBA który może kontrolować ograniczoną liczbą dysków. Do tego dochodzi trudność w konfiguracji przy zwiększaniu ilości serwerów.
- Wyłączony serwer = brak dostępu do danych- W momencie gdy serwer musi zostać wyłączony np. w celu konserwacji, przeglądu, zainstalowania nowego oprzyrządowania, aktualizacji systemu operacyjnego lub w przypadku zainfekowania wirusem, użytkownicy nie będą mieli dostępu do danych .


## Źródła


* <http://www.elibron.pl/magazynowanie-i-ochrona-danych-bw/90-das-nas-san-storage-nie-jedno-ma-imie>

* <https://www.backupacademy.pl/das-vs-nas/>
* <https://www.siemon.com/us/white_papers/14-07-29-data-center-storage-evolution.asp>





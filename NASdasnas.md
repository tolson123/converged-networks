#NAS (Network Attached Storage)



### Skad wzięło się NAS?

NAS to skrót od Network-attached Storage. Jest to protokół software/hardware obejmujący **dedykowane serwery plikowe**, opracowany przez znanego producenta podzespołów sieciowych - 3Com, obecnie przejętego przez HP. Ideą NAS było podłączenie zasobów masowych pamięci dyskowych bezpośrednio do sieci. Pod tym względem, można powiedzieć, 3Com wygrało wyścig zbrojeń z takimi firmami jak IBM czy też Novell & SUN. NASy zdobywaja popularność od połowy lat dziewięćdziesiątych. 



### Czym dokładnie jest NAS?

Mówiąc NAS w kontekście produktu mówimy o urządzeniu do przechowywania danych które podłączamy bezpośrednio do sieci. Najczęściej przyjmuje ono formę computer appliance, to jest, urządzenia dedykowanego, z hardwarem, firmwarem i konfiguracja przeznaczonymi dla przechowywania danych dla użytkowników sieci. Takie NASy NAS w porównaniu z SAN dostarcza nie tylko pamięci dla danych ale również system plików dla ich obsługi, kiedy SAN pozostawia ta kwestię stronie klienta. Dedykowany NAS zawiera sloty na kilka dysków twardych, które są łączone w systemie RAID w celu zapewnienia redundancji danych.Dostęp do danych zapisanych w NAS jest w pełni kontrolowany, przykładowo klienci mogą uzyskać czasowy dostęp do określonych danych a pełny dostęp jest możliwy tylko z scentralizowanej lokacji w sieci przez upoważnionych użytkowników. NAS podobnie jak router posiada interfejs sieciowy do jego konfiguracji. Jego oprogramowanie oferuje różne przydatne aplikacje, np. służące do streamowania mediów lub klient Torrent dla pobierania danych do urządzenia.

![enter image description here](http://www.elibron.pl/images/das02.jpg)



###Formy NAS:

1. Dedykowane urzadzenie NAS

2. Innym, bardziej budżetowym rozwiązaniem kwestii NAS jest zastosowanie routerów z wbudowanymi dyskami twardymi i oprogramowaniem serwera NAS. Najpopularniejszymi tego typu produktami sa AirpPort Time Capsule firmy Apple. Alternatywa dla wbudowanego dysku twardego jet tutaj router z złączem USB 3.0 do którego można podłączyć dysk zewnętrzny.

3. Na użytek domowy lub małego biura, kolejna opcja stworzenia NAS jest zagospodarowanie nieużywanego, podłączonego do sieci PC za pomocą systemu FreeNAS. 



* Systemy FreeNAS i NAS4Free są również wykorzystywane w urządzeniach dedykowanych. FreeNAS oferuje interfejs webowy, protokoły udostępniania plików: SMB/CIFS (dla Windowsa), NFS (dla rodziny UNIX), AFP (dla oprogramowania Apple) oraz FTP. Inne możliwości to w pełni konfigurowalne snapshoty i ich replikacja.



Wspólnym mianownikiem tych wszystkich rozwiązań jest:

Tworzenie własnej, prywatnej chmury dla przechowywania danych

Skalowalność, dodając kolejne urządzenia zwiększamy dostępna w sieci pamięć masowa

Ograniczenie oczekiwania na odpowiedź na zapytania o dane w obrębie sieci

Łatwe tworzenie kopii zapasowych



### Dlaczego NAS i ile kosztuje?

NAS znajdują zastosowanie zarówno wśród sieci domowych jak i przedsiębiorstw o różnym rozmiarze, ceny NASów dla użytkowników domowych i małych biur zaczynają się od 169$ a dochodzą do 1770$. Ceny Apple Time Capsule oscylują wokół 300$. 



Tym co odróżnia NASy od serwerów “ogólnego zastosowania” jest łatwiejsza i bardziej przejrzysta konfiguracja i inne czynności administracyjne oraz  szybszy dostęp do plików.



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

* <http://cctvinstitute.co.uk/network-attached-storage/> -

* <http://www.seagate.com/pl/pl/tech-insights/what-is-nas-master-ti/> 

* <http://www.howtogeek.com/208030/how-to-set-up-a-nas-network-attached-storage-drive/>
* <http://www.elibron.pl/magazynowanie-i-ochrona-danych-bw/90-das-nas-san-storage-nie-jedno-ma-imie>

* <https://www.backupacademy.pl/das-vs-nas/>
* <https://www.siemon.com/us/white_papers/14-07-29-data-center-storage-evolution.asp>





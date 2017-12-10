# **System Lustre**
**Lustre** - to rodzaj rozproszonego systemu plików używanego w superkomputerach. Nazwa jest połączeniem słów Linux i klaster. Dzięki zgodnemu z POSIX interfejsowi systemu plików i swojej skalowalności Lustre może być częścią wielu klastrów komputerowych z dziesiątkami tysięcy klientów, z dostępem do  dziesiątek peta bajtów danych na setkach serwerów przy przepustowości więcej niż 1TB/s. Oprogramowanie tego systemu plików jest dostępne na licencji GNU. Wszystko to sprawia, że jest to najpopularniejszy system plików używany w komputerach klasy HPC. To doskonały wybór dla firm z dużymi centrami danych w takich branżach jak symulacje meteorologiczne, ropa i gaz, life science, rich media, czy finanse.
Lustre działa na różnych jądrach Linuksa z dystrybucji Linuksa, w tym RHEL, CentOS i SLES. Używając tylko Lustd ldiskfs OSD, konieczne będzie poprawienie jądra przed zbudowaniem Lustera. Luster ZFS OSD i kod klienta Lustre nie wymagają poprawek do jądra.


Pracę nad systemem Lustre rozpoczął Peter J. Braam w 1999 roku na Uniwersytecie Carnegie Mellon, aby je kontynuować we własnej firmie. W 2007 roku aktywa firmy przejęło Sun. W 2010 roku Sun stało się częścią firmy Oracle i tym samym kontynuatorem badań nad rozwojem tego systemu. W grudniu tego samego roku Oracle ogłosiło zaprzestanie tworzenia Lustre 2.x i zajęło się wyłącznie wsparciem dotyczącym wersji 1.8. W lutym 2013 własność intelektualną i wszystko co związane z Lustre nabyła firma Xyratex. Ostatecznie 8 kwietnia 2014 Xyratex przekazał domenę Lustre org na ręce społeczności użytkowników.

## **Cechy Systemu Lustre:**

- **Skalowalność** - najbardziej skalowalny system plików POSIX. Klienci Lustre mogą odczytywać i zapisywać bezpośrednio z serwerów pamięci masowej, usuwając pliki z wielu obiektów docelowych. Pozwala to zwiększyć zarówno wydajność, jak i objętość w miarę dodawania serwerów pamięci, a ponieważ Luster zapewnia niezwykle wydajne wykorzystanie sprzętu, systemy pamięci masowej mogą skalować się nawet do tysięcy węzłów magazynowania. Katalogi zdalnego systemu plików można teraz rozłożyć na wiele serwerów metadanych w celu zapewnienia większej wydajności, ponieważ zwiększa się liczba ich serwerów .

- **Wydajność** - ldfsx to wydajny rozszerzony system plików ext4 z księgowaniem, ulepszony w celu zwiększenia wydajności i zapewnienia funkcjonalności wymaganej przez Lustre

- **Wysokowydajna, heterogeniczna sieć** - oprogramowanie Lustre wspiera: Remote Direct Memory Access (RDMA) dla InfiniBand, OpenFabrics Enterprise Distribution (OFED), Intel OmniPath® i inne zaawansowane technologie sieciowe. Wiele sieci RDMA można połączyć za pomocą routingu Lustre celem otrzymania maksymalnej wydajności. Oprogramowanie Lustre obejmuje również zintegrowaną diagnostykę sieci. 

- **Wysoka dostępność** - system plików Lustre może współpracować z różnymi menedżerami wysokiej dostępności (HA) aby umożliwić automatyczne przełączanie awaryjne i nie ma pojedynczego punktu awarii (NSPF). Pozwala to na przejrzyste odzyskiwanie aplikacji. Multiple Mount Protection (MMP) zapewnia zintegrowaną ochronę przed błędami w wysoce dostępnych systemach, które mogłyby spowodować uszkodzenie systemu plików.


- **Bezpieczeństwo** - Lustre zapewnia ulepszone uwierzytelnianie i szyfrowanie dzięki wykorzystaniu protokołu Kerberos w celu zapewnienia klientom bezpiecznego uwierzytelniania i szyfrowania informacji przesyłanych przez sieć. Obsługuje SELinux, umożliwiając przeniesienie kontroli dostępu do plików z przestrzeni użytkownika do przestrzeni jądra, zapewniając wymuszanie dostępu klienta do dozwolonych plików.

- **Lista kontroli dostępu (ACL)** - model bezpieczeństwa Lustre jest zgodny z modelem UNIX system, rozszerzonym o listy ACL POSIX. Na uwagę zasługują dodatkowe funkcje takie jak root squash.

- **Interoperacyjność** - system plików Lustre działa na różnych architekturach procesorów i mieszanych endianach klastrów i współdziała z kolejnymi wersjami oprogramowania.

- **Architektura oparta na obiektach** - klienci są odizolowani od struktury pliku na dysku, co umozliwia uaktualnienie architektury pamięci masowej bez wpływu na klienta.

- **Precyzyjne blokowanie metadanych** - wielu klientów może jednocześnie czytać i modyfikować ten sam plik lub katalog. Menedżer blokowania rozproszonego Lustre (LDLM) zapewnia spójność plików między wszystkimi klientami i serwerami w systemie plików. LDL MDTM zarządza blokadami uprawnień i-węzłów i ścieżek. Każdy OST ma swój własny LDLM dla blokad przechowywanych na nim pasków plików, które skalują wydajność blokowania w miarę wzrostu systemu plików.

- **Przydziały** - dostępne są limity użytkowników i grup.

- **Wzrost wydajności** - rozmiar systemu plików i zagregowaną przepustowość klastra można zwiększyć bez przerywania działania systemu, dodając do klastra nowe OST i MDT.

- **Kontrolowany układ plików** - układ plików między OST można skonfigurować dla każdego pliku, dla każdego katalogu lub dla każdego systemu plików. Umożliwia to dostrojenie I/O pliku do określonych wymagań aplikacji w ramach jednego systemu plików. System plików Lustre wykorzystuje striping RAID-0 i równoważy wykorzystanie przestrzeni przez OST.

- **Ochrona integralności danych sieciowych** -  suma kontrolna wszystkich danych przesyłanych od klienta do OSS chroni przed uszkodzeniem podczas przesyłania danych.

- **MPI I/O** - architektura Lustre ma dedykowaną warstwę MPIO ADIO, która optymalizuje równoległe operacje wejścia / wyjścia, aby dopasować się do architektury systemu plików.

- **Eksport NFS i CIFS** - pliki Lustre mogą być eksportowane ponownie za pomocą NFS (przez Linux knfsd) lub CIFS (przez Sambę), co umożliwia ich współdzielenie z klientami innymi niż Linux, takimi jak Microsoft Windows i Apple Mac OSX.

- **Narzędzie do odzyskiwania po awarii** - system plików Lustre zapewnia kontrolę online systemu plików rozproszonych (LFSCK), która może przywrócić zgodność między komponentami pamięci masowej w przypadku poważnego błędu systemu plików. System plików Lustre może działać nawet w obecności niespójności systemu plików, a LFSCK może działać, gdy system plików jest w użyciu, więc LFSCK nie musi być ukończony przed zwróceniem systemu plików do produkcji.

- **Monitorowanie wydajności** - system plików Lustre oferuje wiele mechanizmów do sprawdzania wydajności i tuningu.

- **Open source** - oprogramowanie Lustre jest licencjonowane na licencji GPL 2.0 do użytku z systemem operacyjnym Linux.


## **Komponenty Systemu Lustre:**
![image](http://doc.lustre.org/figures/Basic_Cluster.png)


### **1 Management Server (MGS)** ###

MGS przechowuje informacje konfiguracyjne dla wszystkich systemów plików Lustre w klastrze i dostarcza te informacje do innych komponentów Lustre. Każdy Lustre target kontaktuje się z MGS w celu dostarczenia informacji, a klienci Lustre kontaktują się z MGS w celu uzyskania informacji. Zaleca się, aby MGS posiadał własną przestrzeń do przechowywania, aby można było nią zarządzać niezależnie. Jednak MGS może być umieszczony razem i współużytkować przestrzeń dyskową z MDS, jak pokazano na rysunku powyżej.

### **2 Składniki Lustre File System** ###

Każdy system plików Lustre składa się z następujących komponentów:

- **Serwery metadanych (MDS)** - metadane przechowywane są w co najmniej jednym MDT dostępnym dla klientów Lustre. Każdy MDS zarządza nazwami i katalogami w systemie plików i zapewnia obsługę żądań sieciowych dla jednego lub więcej lokalnych MDT.

- **Metadata Targets** (MDT) - w przypadku oprogramowania Luster w wersji 2.3 i wcześniejszych każdy system plików ma jeden MDT. MDT przechowuje metadane (takie jak nazwy plików, katalogi, uprawnienia i układ pliku) w pamięci masowej dołączonej do MDS. Każdy system plików ma jeden MDT. MDT we współużytkowanym celu pamięci masowej może być dostępny dla wielu MDS, ale tylko jeden może uzyskać do niego dostęp w danej chwili. Jeśli aktywny MDS ulegnie awarii, rezerwowy MDS może obsługiwać MDT i udostępniać go klientom. Jest to określane jako przełączanie awaryjne MDS.

- **Object Storage Servers (OSS)** - OSS zapewnia obsługę plików I/O oraz obsługę żądań sieciowych dla jednego lub kilku lokalnych OST. Zazwyczaj OSS obsługuje od dwóch do ośmiu OST-ów, do 16 TB każdy. Typowa konfiguracja to MDT na dedykowanym węźle, dwa lub więcej OST w każdym węźle OSS i klient na każdej z dużej liczby węzłów obliczeniowych.

- **Object Storage Target (OST)** - dane pliku użytkownika są przechowywane w jednym lub kilku obiektach, każdy obiekt w oddzielnym OST w systemie plików Lustre. Liczba obiektów na plik jest konfigurowalna przez użytkownika i można ją dostroić w celu optymalizacji wydajności dla danego obciążenia.

- **Klienci Lustre** - klienci Lustre to komputery obliczeniowe, wizualizacyjne lub desktopowe, które korzystają z oprogramowania klienckiego Lustre, pozwalając im na zamontowanie systemu plików.

Oprogramowanie klienckie Lustre zapewnia interfejs między wirtualnym systemem plików Linux a serwerami Lustre. Obejmuje klienta zarządzającego (MGC), klienta metadanych (MDC) i wielu klientów przechowywania obiektów (OSC), z których jeden odpowiada każdemu OST w systemie plików. 
Obiekt logiczny voluminu (LOV) agreguje elementy OSC, aby zapewnić przejrzysty dostęp do wszystkich OST. W ten sposób klient z zamontowanym systemem plików Lustre widzi pojedynczą, spójną, zsynchronizowaną przestrzeń nazw. Kilku klientów może jednocześnie pisać do różnych części tego samego pliku, podczas gdy inni klienci mogą czytać z pliku.
Logiczny wolumin metadanych (LMV) agreguje MDC, aby zapewnić przejrzysty dostęp do wszystkich MDT w podobny sposób jak LOV dla dostępu do plików. Dzięki temu klient może zobaczyć drzewo katalogów na wielu MDT jako pojedynczą spójną przestrzeń nazw, a pofragmentowane katalogi są scalane na klientach w celu utworzenia pojedynczego widocznego katalogu dla użytkowników i aplikacji.

### **3 Lustre Networking (LNet)** ###

Lustre Networking (LNet) to niestandardowy interfejs sieciowy udostępniający infrastrukturę komunikacyjną, która obsługuje metadane i dane wejścia/wyjścia pliku dla serwerów i klientów systemu plików Lustre.
W klastrze wykorzystującym jeden lub więcej systemów plików Lustre infrastruktura komunikacji sieciowej wymagana przez system plików Luster jest implementowana za pomocą funkcji Sieci Lustre (LNet).
LNet obsługuje wiele powszechnie używanych typów sieci, takich jak InfiniBand czy IP, i umożliwia równoczesną dostępność w wielu typach sieci z routingiem między nimi. Możliwy jest zdalny dostęp do pamięci bezpośredniej (RDMA), ale musi być obsługiwany przez sieci bazowe. Odbywa się to przy użyciu odpowiedniego sterownika sieciowego - LND. Jest on wtyczkowym sterownikiem zapewniającym obsługę określonego typu sieci. Na przykład ksocklnd to sterownik implementujący protokół TCP Socket LND obsługujący sieci TCP. LND są ładowane do stosu sterowników, z jednym LND dla każdego używanego typu sieci.
Funkcje wysokiej dostępności i odzyskiwania umożliwiają przezroczyste odzyskiwanie w połączeniu z serwerami przełączania awaryjnego
LNet pozwala na uzyskanie kompleksowej przepustowości odczytu / zapisu na poziomie lub blisko szczytowej przepustowości na różnych połączeniach sieciowych.

Sieć Lustre składa się z klientów i serwerów z oprogramowaniem Lustre. Nie musi być ograniczona do jednej podsieci LNet i może obejmować kilka sieci z ustwionym routingiem. W podobny sposób pojedyncza sieć może mieć wiele podsieci LNet.

Stos sieciowy Lustre składa się z dwóch warstw: modułu LNet i LND. Warstwa LNet działa nad warstwą LND w sposób podobny do działania warstwy sieci nad warstwą łącza danych. Warstwa LNet jest bezpołączeniowa, asynchroniczna i nie sprawdza, czy dane zostały przesłane, podczas gdy warstwa LND jest zorientowana na połączenie i zwykle sprawdza transmisję danych.

LNets są jednoznacznie identyfikowane za pomocą etykiety składającej się z ciągu odpowiadającego LND i liczby, takiej jak tcp0, o2ib0 lub o2ib1, która jednoznacznie identyfikuje każdą LNet. Każdy węzeł na LNet ma co najmniej jeden identyfikator sieci (NID). NID jest kombinacją adresu interfejsu sieciowego i etykiety LNet w postaci: adres @ LNet_label.

Przykłady:

>_192.168.1.2@tcp0_ 

>_10.13.24.90@o2ib1_

W pewnych okolicznościach wymaga się, aby ruch systemu plików Lustre przechodził między wieloma LNetami. Jest to możliwe dzięki routingowi LNet. Ważne jest, aby zdać sobie sprawę, że routing LNet to nie to samo co routing w sieci. 

LNet obsługuje wiele typów sieci, w tym:

- InfiniBand: OpenFabrics OFED (o2ib)

- TCP (każda sieć przenosząca ruch TCP, w tym GigE, 10GigE i IPoIB)

- RapidArray: ra

- Quadrics: Elan



### **4 Klaster Lustre** ###

Klaster systemu plików Lustre może zawierać setki systemów OSS i tysiące klientów. W klastrze Lustre można stosować więcej niż jeden typ sieci. Współużytkowane magazynowanie między OSS umożliwia przełączanie awaryjne. 

 ![image](http://opensfs.org/wp-content/uploads/2013/10/LustreComponents21.gif)

## **Failover** ##
W systemie o wysokiej dostępności (HA) nieplanowane przestoje są minimalizowane dzięki wykorzystaniu nadmiarowych komponentów sprzętowych i programowych oraz komponentów oprogramowania, które automatyzują odzyskiwanie po wystąpieniu awarii. Jeśli wystąpi incydent, taki jak utrata serwera, urządzenia pamięci masowej, usterka sieci lub oprogramowania, usługi systemu będą kontynuowane z minimalną przerwą. Zasadniczo dostępność określa się jako procent czasu, przez jaki system musi być dostępny.

Dostępność jest osiągnięta poprzez replikację sprzętu i / lub oprogramowania. Gdy serwer podstawowy ulegnie awarii lub jest niedostępny, serwer zapasowy może zostać przełączony na jego miejsce w celu uruchamiania aplikacji i powiązanych zasobów. Proces ten, zwany przełączeniem awaryjnym, jest automatyczny w systemie HA iw większości przypadków jest całkowicie przezroczysty.

Konfiguracja sprzętowa przełączania awaryjnego wymaga pary serwerów z zasobem udostępnionym (zwykle jest to fizyczne urządzenie pamięci masowej, które może być oparte na technologii SAN, NAS, sprzętowej macierzy RAID, SCSI lub Fibre Channel (FC)). Sposób udostępniania pamięci powinien być zasadniczo przezroczysty na poziomie urządzenia; ten sam numer jednostki logicznej (LUN) powinien być widoczny z obu serwerów. Aby zapewnić wysoką dostępność na poziomie fizycznego przechowywania, zachęca się do korzystania z macierzy RAID w celu ochrony przed awariami na poziomie dysku.

Oprogramowanie Lustre nie zapewnia redundancji danych - zależy to wyłącznie od redundancji urządzeń pamięci masowej. Kopią zapasową OST powinna być pamięć RAID 5 lub, najlepiej, pamięć RAID 6. Pamięć MDT powinna być RAID 1 lub RAID 10.

**Możliwości przełączania awaryjnego**

Aby stworzyć wysoce dostępny system plików Lustre, oprogramowanie do zarządzania zasilaniem lub sprzęt i oprogramowanie wysokiej dostępności (HA) jest używane w celu zapewnienia następujących funkcji przełączania awaryjnego:

- Ogrodzenia zasobów - chroni fizyczną pamięć masową przed równoczesnym dostępem przez dwa węzły.

- Zarządzania zasobami - uruchamia i zatrzymuje zasoby Lustre w ramach przełączania awaryjnego, utrzymuje stan klastra i wykonuje inne zadania związane z zarządzaniem zasobami.

- Monitorowania kondycji - Weryfikuje dostępność sprzętu i zasobów sieciowych i reaguje na wskazania kondycji komponentów dostarczone przez oprogramowanie Lustre.

**Rodzaje konfiguracji pracy awaryjnej**

Węzły w klastrze można skonfigurować do przełączania awaryjnego na kilka sposobów. Często są one konfigurowane parami (na przykład dwa OST dołączone do współużytkowanego urządzenia pamięci masowej), ale możliwe są również inne konfiguracje przełączania awaryjnego. Konfiguracje przełączania awaryjnego obejmują:

- Para active/pasive - w tej konfiguracji aktywny węzeł zapewnia zasoby i obsługuje dane, podczas gdy pasywny węzeł zwykle stoi bezczynnie. Jeśli aktywny węzeł ulegnie awarii, węzeł pasywny przejmuje i staje się aktywny.

- Para active/active - w tej konfiguracji aktywne są oba węzły, z których każdy zapewnia podzbiór zasobów. W przypadku awarii drugi węzeł przejmuje zasoby z uszkodzonego węzła.

W wersjach oprogramowania Lustre poprzedzających wydanie oprogramowania 2.4 Splash MDS można skonfigurować jako parę active/pasive, natomiast OSS można wdrożyć w konfiguracji active/active, która zapewnia nadmiarowość bez dodatkowego narzutu. Często rezerwowy MDS jest aktywnym MDS dla innego systemu plików Lustre lub MGS, więc żadne węzły nie są bezczynne w klastrze.

**Funkcja failover w systemie plików Lustre**

Funkcję przełączania awaryjnego zapewnianą przez oprogramowanie Lustre można wykorzystać w następującym scenariuszu przełączania awaryjnego. Gdy klient próbuje wykonać operacje wejścia/wyjścia do uszkodzonego Lustre Source, kontynuuje próbę do momentu otrzymania odpowiedzi od któregokolwiek ze skonfigurowanych węzłów przełączania awaryjnego dla Lustre Source. Aplikacja przestrzeni użytkownika nie wykrywa niczego niezwykłego, z tym wyjątkiem, że operacje we/wy mogą trwać dłużej.

Przełączanie awaryjne w systemie plików Lustre wymaga skonfigurowania dwóch węzłów jako pary przełączania awaryjnego, które muszą współdzielić jedno lub więcej urządzeń magazynujących. System plików Lustre można skonfigurować tak, aby zapewniał przełączanie awaryjne MDT lub OST.

- W przypadku przełączania awaryjnego MDT można skonfigurować dwa MDS do obsługi tego samego zestawu MDT. Tylko jeden węzeł MDS może jednocześnie obsługiwać MDT. Wprowadzono w Lustre 2.4 Wersja oprogramowania 2.4 pozwala na wiele MDT. Umieszczając dwie lub więcej partycji MDT w magazynie współużytkowanym przez dwa MDS. W przypadku gdy jeden MDS ulegnie awarii, drugi może rozpocząć obsługę niezarejestrowanego MDT. Określa się to mianem pary active/active przełączania awaryjnego.

- W przypadku przełączania awaryjnego OST można skonfigurować wiele węzłów OSS, aby móc obsługiwać ten sam OST. Jednak tylko jeden węzeł OSS może obsługiwać OST na raz. OST można przenosić między węzłami OSS, które mają dostęp do tego samego urządzenia pamięci masowej za pomocą poleceń umount / mount.

#### **Para active/pasive:** ####
![image](http://doc.lustre.org/figures/MDT_Failover.png)


#### **Para active/active:** ####
![image](http://doc.lustre.org/figures/MDTs_Failover.png)



# **Źródła**
 - Wikipedia
 - http://lustre.org
 - https://www.intel.com/content/www/us/en/lustre/new-generation-lustre-software.html


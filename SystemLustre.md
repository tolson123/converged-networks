# **System Lustre**

System plików Lustre jest otwartym, równoległym systemem plików, który obsługuje wiele wymagań wiodących środowisk symulacji HPC. Opracowany na podstawie projektu badawczego na Uniwersytecie Carnegie Mellon system plików Luster przekształcił się w system plików obsługujący niektóre z najpotężniejszych superkomputerów na Ziemi. System plików Lustre zapewnia zgodny z POSIX interfejs systemu plików, może skalować do tysięcy klientów, petabajtów pamięci i setek gigabajtów na sekundę przepustowości we / wy. Kluczowymi komponentami systemu plików Lustre są serwery metadanych (MDS), cele metadanych (MDT), obiekty pamięci masowej obiektów (OSS), obiekty docelowe serwera obiektowego (OST) i klienci Luster.

Luster działa na większości urządzeń z dowolnym typem blokowego urządzenia pamięci masowej, w tym pojedynczych dysków, oprogramowania i sprzętu RAID i menedżera woluminu logicznego. 64-bitowe architektury są zalecane dla serwerów. Luster obsługuje sieci Ethernet i InfiniBand.

Luster pozwala na wiele MDS dla wysokiej dostępności. Rozmiar systemu plików nośnika MDT powinien być wybrany na podstawie łącznej liczby plików planowanych do przechowywania w systemie plików Lustre, a zagregowana przestrzeń OST powinna zostać wybrana na podstawie całkowitej ilości danych planowanych do zapisania w pliku system. Wstępne oszacowanie wymagań dotyczących miejsca może narzucać wymagania sprzętowe.
Luster działa na różnych jądrach Linuksa z dystrybucji Linuksa, w tym RHEL, CentOS i SLES. Używając tylko Lustd ldiskfs OSD, konieczne będzie poprawienie jądra przed zbudowaniem Lustera. Luster ZFS OSD i kod klienta Lustre nie wymagają poprawek do jądra.
![image](http://opensfs.org/wp-content/uploads/2013/10/LustreComponents21.gif)

# **Skalowalność**

Najbardziej skalowalny system plików POSIX. Klienci Lustre mogą odczytywać i zapisywać bezpośrednio z serwerów pamięci masowej, usuwając pliki z wielu obiektów docelowych. Pozwala to zwiększyć zarówno wydajność, jak i objętość w miarę dodawania serwerów pamięci, a ponieważ Luster zapewnia niezwykle wydajne wykorzystanie sprzętu, systemy pamięci masowej mogą skalować się nawet do tysięcy węzłów magazynowania. 

Skalowalna wydajność metadanych 

Katalogi zdalnego systemu plików można teraz rozłożyć na wiele serwerów metadanych w celu zapewnienia większej wydajności metadanych, ponieważ zwiększa się liczba serwerów metadanych.

# **Bezpieczeństwo**

Oprogramowanie Luster zapewnia ulepszone uwierzytelnianie i szyfrowanie dzięki wykorzystaniu protokołu Kerberos w celu zapewnienia klientom bezpiecznego uwierzytelniania i szyfrowania informacji przesyłanych przez sieć.
Luster obsługuje teraz użycie SELinux, umożliwiając przeniesienie kontroli dostępu do plików z przestrzeni użytkownika do przestrzeni jądra i zapewniając wymuszanie dostępu klienta do dozwolonych plików.

# **Zarządzanie danymi**
Warstwowe przechowywanie

Oprogramowanie Lustre zapewnia modułowe interfejsy do warstwowego przechowywania danych i inteligentnie zarządza systemem plików poprzez ruch danych oparty na zasadach. Dzięki temu administratorzy pamięci masowej mogą dynamicznie migrować "gorące" i "zimne" dane pomiędzy Luster i dynamicznie optymalizowaną pamięcią masową, aby uzyskać idealną równowagę między wydajnością i kosztami.

Migawki systemu plików

Zintegrowana obsługa migawek umożliwia administratorom pamięci masowej korzystanie z tej funkcji ochrony danych w systemach plików punktów kontrolnych. Migawki mogą być montowane jako nowe przestrzenie nazw umożliwiające dostęp do wcześniej zmodyfikowanych lub usuniętych plików w systemie pamięci masowej.

Kompresja

Luster i OpenZFS zapewniają kompresję danych w locie, maksymalizując dostępną pamięć i zwiększając ogólną wydajność, zmniejszając liczbę żądań we / wy danych.

Podmontaż podkatalogów

Klienci mogą zamontować pojedynczy katalog, ograniczając przypadkowe modyfikowanie lub usuwanie plików poza podkatalogiem.

# **Źródła**

- http://lustre.org
- https://www.intel.com/content/www/us/en/lustre/new-generation-lustre-software.html

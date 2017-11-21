# **System Lustre**

System plików Lustre jest otwartym, równoległym systemem plików, który obsługuje wiele wymagań wiodących środowisk symulacji HPC. Opracowany na podstawie projektu badawczego na Uniwersytecie Carnegie Mellon system plików Luster przekształcił się w system plików obsługujący niektóre z najpotężniejszych superkomputerów na Ziemi. System plików Lustre zapewnia zgodny z POSIX interfejs systemu plików, może skalować do tysięcy klientów, petabajtów pamięci i setek gigabajtów na sekundę przepustowości we / wy. Kluczowymi komponentami systemu plików Lustre są serwery metadanych (MDS), cele metadanych (MDT), obiekty pamięci masowej obiektów (OSS), obiekty docelowe serwera obiektowego (OST) i klienci Luster.

Luster działa na większości urządzeń z dowolnym typem blokowego urządzenia pamięci masowej, w tym pojedynczych dysków, oprogramowania i sprzętu RAID i menedżera woluminu logicznego. 64-bitowe architektury są zalecane dla serwerów. Luster obsługuje sieci Ethernet i InfiniBand.

Luster pozwala na wiele MDS dla wysokiej dostępności. Rozmiar systemu plików nośnika MDT powinien być wybrany na podstawie łącznej liczby plików planowanych do przechowywania w systemie plików Lustre, a zagregowana przestrzeń OST powinna zostać wybrana na podstawie całkowitej ilości danych planowanych do zapisania w pliku system. Wstępne oszacowanie wymagań dotyczących miejsca może narzucać wymagania sprzętowe.
Luster działa na różnych jądrach Linuksa z dystrybucji Linuksa, w tym RHEL, CentOS i SLES. Używając tylko Lustd ldiskfs OSD, konieczne będzie poprawienie jądra przed zbudowaniem Lustera. Luster ZFS OSD i kod klienta Lustre nie wymagają poprawek do jądra.
![image](http://opensfs.org/wp-content/uploads/2013/10/LustreComponents21.gif)

# **Źródła**

- http://lustre.org
- https://www.intel.com/content/www/us/en/lustre/new-generation-lustre-software.html

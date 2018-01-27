# Co to jest NAS?

### NAS  (Network Attached Storage)
To sieciowy serwer plików, który umożliwia przechowywanie i uzyskiwanie dostępu do danych, które się na nim znajdują ze scentralizowanej lokalizacji przez upoważnionych użytkowników sieciowych oraz zróżnicowanych klientów. Zatem jest to urządzenie pamięci masowej podłączone do sieci.
Systemy NAS zawierają jeden lub więcej napędów pamięci masowej, często ułożone w logiczne, redundantne kontenery. Zaczęły one zdobywać popularność jako wygodna metoda udostępniania plików na wielu komputerach. Potencjalne korzyści korzystania z serwera plików to szybszy dostęp do danych, łatwiejsza administrację i prosta konfiguracja.

### Co oferuje NAS:

1.	Wszystkie pliki w jednym miejscu:
Wszystkie pliki znajdują się w jednym miejscu, a dostęp do nich można uzyskać z poziomu komputera, telefonu czy tabletu.
2.	Synchronizacja plików i dokumentów:
W ciągu kilku sekund następuje synchronizacja plików między urządzeniami, a także synchronizacji folderów współdzielonych dzięki protokołowi rsync o którym można przeczytać na stronie:
[Rsync](https://pl.wikipedia.org/wiki/Rsync  )
3.	Tworzenie kopii zapasowych:
NAS pozwala na zaplanowanie zadań, a dzięki odpowiedniemu harmonogramowi będzie wykonywał kopie danych w czasie rzeczywistym.
Przykładem może być artykuł dotyczący takiej konfiguracji:
[Rsync Przykłady](http://linux.mazowsze.pl/rsync-przyklady-uzycia-kopia-zapasowa-synchronizacja)
4.	Udostępnianie plików na różne platformy:
Dzięki zastosowaniu protokołów SMB/CIFS, NFS i AFP serwer NAS daje możliwość dostępu do plików przy użyciu urządzeń z systemami Windows®, Mac®, Linux®/UNIX®, Android™ i iOS®. Dodatkowo posiadając odpowiednie aplikacje możemy uzyskać zdalny dostęp do plików.
Informacje odnośnie protokołów znajdziemy na stronach:
[SMB,](https://pl.wikipedia.org/wiki/Server_Message_Block)
[NFS,](https://pl.wikipedia.org/wiki/Network_File_System_(protok%C3%B3%C5%82))
[AFP](https://en.wikipedia.org/wiki/Apple_Filing_Protocol)
5.	Ochrona danych:
Serwery mogą wykorzystywać mechanizmy zabezpieczeń, takie jak weryfikacja dwuetapowa, szyfrowanie woluminów i folderów udostępnionych, a także natychmiastowe powiadomienia, które są wysyłane do urządzeń mobilnych. Jeśli chodzi o dane, to przed ich utratą bezpieczeństwo zapewnia odpowiednio skonfigurowana macierz RAID.
Więcej informacji na temat RAID można znaleźć na stronie:
[RAID](https://github.com/MRostanski/converged-networks/blob/master/RAID.md)
Odnośnie weryfikacji dwuetapowej można przeczytać na
[stronie](https://www.qnap.com/pl-pl/how-to/tutorial/article/w-jaki-spos%C3%B3b-poprawi%C4%87-bezpiecze%C5%84stwo-konta-korzystaj%C4%85c-z-2-krokowej-weryfikacji)
6.	Domowe centrum multimedialne:
Wykorzystując standard [DLNA](https://www.lifewire.com/what-is-dlna-1847363) NAS pozwala na strumieniowanie treści audio oraz wideo do odpowiednich urządzeń takich jak Smart TV. Przykładowe wykorzystanie serwer NAS zostało przedstawione w artykule na [stronie](http://www.benchmark.pl/testy_i_recenzje/DLNA-4124.html)
7.	Wirtualizacja:
- tworzenia maszyn wirtualnych z różnymi systemami operacyjnym
- dostęp do danych i otwierania plików bezpośrednio przez aplikacje zainstalowane na maszynach wirtualnych 
- wszystkie operacje są wykonywane na serwerze NAS, co minimalizuje ryzyko wycieku danych i oszczędza przepustowość sieci.
8.	Plug-iny:
Od antywirusów, przez Drupala, Joomla, Magento, Perl, phpBB, Plex Media Server aż po Ruby i Pythona. NAS może być platformą dla sklepu internetowego, forum strony internetowej, serwerem FTP, poczty i druku. 

## Rodzaje serwerów plikowych:

-	Dedykowane urządzenie NAS wraz z odpowiednio przygotowanym panelem pozwalającym na zarządzenie serwerem plikowym
-	Routery pozwalające na podpięciu urządzeń pod porty USB pełniące funkcje NAS
-	Komputer (stary PC ) lub specjalnie do tego celu złożony sprzęt wyposażony w oprogramowanie [FreeNAS](http://www.freenas.org/) lub NAS4Free [nas4free](https://www.nas4free.org) umożlwiający konfigurację sprzętu według własnych upodobań oraz jego możliwości
-	Clustered NAS - Serwer NAS klastrowany używa rozproszonego systemu plików działającego jednocześnie na wielu serwerach. Kluczową różnicą między klastrami i tradycyjnymi serwerami NAS jest możliwość dystrybucji danych i metadanych, które są potrzebne w węzłach klastra lub urządzeniach pamięci masowej

![](http://www.qnap.com/images/products/NAS/vsseries/TSX69L_us11.png)

## Jaki NAS wybrać?

Wszystko zależy od celu do jakiego zamierzamy wykorzystać ten sprzęt. Jeśli zależy nam na możliwościach,  ale także na prostocie w konfigurowaniu sprzętu to powinniśmy skorzystać z dedykowanych do tego urządzeń (QNAP czy Synology ).
Zaawansowanymi użytkownicy mogą sami zbudować od podstaw taki sprzęt, począwszy od konfiguracji sprzętowej po instalację oprogramowania specjalnie do tego przeznaczonego.

## Kiedy stosować serwer NAS?

Serwer plikowy najlepiej stosować, gdy:
-	mamy rozbudowaną sieć domową, a w niej komputery, notebooki, tablety czy smartfony (więcej niż 2 urządzenia),
-	wymieniamy duże ilości danych w sieci lokalnej,
-	gromadzimy duże ilości danych,
-	chcemy zadbać o bezpieczeństwo danych,
-	chcemy magazynować dane w scentralizowanym miejscu (łatwość obsługi i zarządzania),
-	chcemy tworzyć kopie zapasowe komputerów domowych,
-	chcemy mieć szybki dostęp do danych w sieci lokalnej,
-	szukamy cichego i energooszczędnego magazynu na dane,
-	chcemy wykorzystać zasoby serwera łącząc się spoza sieci LAN,


## Jakie cechy powinien mieć serwer NAS?

- co najmniej 2 zatoki na dyski (elastyczne dostosowanie powierzchni i możliwość zwiększenia zabezpieczenia przed awarią)
-	praca w trybie RAID
-	dodatkowe porty USB do podłączenia dysków zewnętrznych lub drukarek
-	obsługa wielu protokołów sieciowych
-	mechanizmy kopii zapasowych dla rożnych systemów operacyjnych
-	dodatkowe aplikacje rozszerzające możliwości
-	administracja i dostęp do zasobów serwera z poziomu aplikacji mobilnych
-	obsługa w języku polskim



## Źródła


[Link1](http://www.seagate.com/pl/pl/tech-insights/what-is-nas-master-ti)
[Link2](https://gadzetomania.pl/3878,dyski-sieciowe-nas-i-kopie-zapasowe-czyli-na-czym-i-jak-zrobic-backup-poradnik,all)
[link3](https://www.qnap.com/solution/7-reasons-why-nas/pl-pl/index.php)
[Link4](https://www.spidersweb.pl/2015/02/raspberry-pi-nas.html)








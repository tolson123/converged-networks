# Fibre Channel over Ethernet
### Definicja
Fibre Channel over Ethernet (FCoE) to protokół, który pozwala na zwiększenie elastyczności rozwiązań SAN (Storage Area Network).
FCoE łączy protokół Fibre Channel (FC) oraz 10-gigabitowy Ethernet, dzięki czemu rozszerza możliwości sieci SAN.

![Przykład SAN](https://upload.wikimedia.org/wikipedia/commons/5/58/Storage_FCoE.png)

### Opis
Jak sama nazwa wskazuje jest to protokół, który pozwala przesyłać dane FC poprzez Ethernet.
FCOE nie wykorzystuje jednak "standardowego" Ethernetu, ale jego rozbudowaną wersję czyli tzw: CEE ( Converged Enhanced Ethernet) zwany także DCE (Data Center Ethernet) - przy czym ta druga nazwa jest zastrzeżona przez Cisco. Główne zmiany pomiędzy tym "wzbogaconym", a "normalnym" Ethernetem są związane z wyeliminowaniem tzw: "frame drops" i utraty pakietów podczas transmisji.

![Converged Enhanced Ethernet](http://www.emc-macierze.pl/uploads/pics/fcoe.jpg)

FCoE transportuje Fibre Channel przez Ethernet bezpośrednio, niezależnie od systemu przesyłania Ethernet. Specyfikacja protokołu FCoE zastępuje Ethernetem warstwy FC0 i FC1 z stosu Fibre Channel.

Głównym zastosowaniem FCoE jest w Data Centers i ich sieciach pamięci masowej (SAN). FCoE ma szczególne zastosowanie w Data Centers ze względu na możliwość redukcji okablowania potrzebnego, a także w aplikacjach do wirtualizacji serwerów, które często wymagają wielu połączeń fizycznych I / O na serwerze.

Za pomocą FCoE, przesył danych sieci (IP) i pamięci masowej (SAN) mogą być konsolidowane za pomocą jednej sieci. Taka konsolidacja może:
- zmniejszyć liczbę kart sieciowych wymaganych do podłączenia do różnego przechowywania i sieci IP
- zmniejszenie liczby kabli i przełączników
- obniżenie kosztów zasilania i chłodzenia

# FCoE Frame diagram

![Przykład SAN](https://upload.wikimedia.org/wikipedia/commons/8/8d/Frame_FCoE.png)

# Zastosowania w Centrach Danych

Protokół Fibre Channel jest też odpowiedzią na potrzebę konsolidacji środowisk centrów danych, gdzie konsolidowane są nie tylko serwery i pamięci masowe, ale także ruch sieciowy. Przy konsolidacji ruchu sieciowego najważniejsze jest, aby nie dopuścić do sytuacji, gdzie jedna klasa ruchu uniemożliwia transport danych z innej klasy. Między innymi z tego powodu grupa standaryzacyjna IEEE 802 wyodrębniła grupę roboczą DCB (Data Center Bridging), aby rozszerzyć funkcjonalność standardu Ethernet o elementy spełniające wymogi nowoczesnych centrów danych i umożliwić sprawne przesyłanie danych różnego rodzaju.

Czym zatem FCoE różni się od iSCSI? Przy protokole iSCSI dane są przesyłane poprzez warstwy TCP/IP. Protokół FCoE zastępuje te warstwy i korzysta z usprawnień stworzonych przez grupę DCB. Jednak brak warstwy IP powoduje, że protokół ten nie może być routowalny poprzez tradycyjne rozwiązania (routing protokołu FCoE może być wykonany przy pomocy protokołu FCIP). Wadą protokołu FCoE jest też to, że nie może on być wdrożony w sieci podatnej na utraty pakietów, podczas gdy dla iSCSI nie stanowi to problemu.

![FCoE i iSCSI](http://blogs.cisco.com/wp-content/uploads/2012.08.07-iSCSI-Latency-and-Design-550x348.png)

# Sources

[Czy FCoE wyprze ISCSI?](http://itfocus.pl/dzial-it/storage/czy-fcoe-wyprze-iscsi/)

[Overview FCoE](http://www.cisco.com/c/en/us/solutions/data-center-virtualization/fibre-channel-over-ethernet-fcoe/index.html)

**Grupa: Michał Repeć, Oleksandr Oliinykov, Olena Bondarenko**

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

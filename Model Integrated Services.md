## Model Integrated Services


Grupa robocza IETF Integrated Services (grupa usług zintegrowanych) opracowała model usług zintegrowanych (Intserv). Model ten wymaga zasobów, takich jak szerokość pasma i wielkość buforów, które muszą być zarezerwowane a priori dla danego strumienia ruchu, by upewnić się, czy jakość usług (QoS) żądana przez strumień ruchu jest satysfakcjonująca. Model Intserv zawiera dodatkowe komponenty poza tymi, które są używane w modelu best-effort (brak QoS, brak reguł, czyli sieć przesyła najlepiej jak potrafi). 
Tymi dodatkowymi komponentami są: klasyfikatory pakietów, programy szeregujące pakiety oraz wstępne kontrolowanie.


Klasyfikatory pakietów są wykorzystywane do zidentyfikowania strumieni, które otrzymają odpowiedni poziom usługi. Programy szeregujące pakiety obsługują przydzielanie usługi do różnych strumieni pakietów, aby upewnić się, że zawarte zobowiązanie QoS jest spełnione. Wstępne kontrolowanie jest wykorzystywane w celu określenia czy router ma niezbędne zasoby, by zaakceptować i obsłużyć nowy strumień.
W modelu usług zintegrowanych (Intserv) zdefiniowano dwie usługi: guaranteed service i controlled-load service.

Usługa gwarantowana (ang. > guaranteed service) może być stosowana do obsługi aplikacji wymagających ograniczonego czasu dostarczenia. Dla tego typu aplikacji, dane dostarczane do aplikacji po przekroczeniu predefiniowanej jednostki czasu są bezwartościowe. Dlatego też usługa gwarantowana przeznaczona jest do utrzymania określonej wartości opóźnienia w dostarczaniu pakietów end-to-end (od końca do końca) dla strumienia. Jest to osiągane dzięki sterowaniu opóźnieniami kolejkowania w elementach sieciowych wzdłuż ścieżki strumienia danych. Usługa gwarantowana nie wprowadza jednak ograniczeń w jitterze (czyli czasie pomiędzy kolejnymi przychodzącymi pakietami).

Usługa sterowanego obciążenia (ang. > controlled-load service) może być stosowana dla aplikacji adaptacyjnych, które mogą tolerować pewne opóźnienia, ale są wrażliwe na stany przeciążenia ruchem. Tego typu aplikacje działają efektywnie wtedy, gdy sieć jest lekko obciążona, natomiast wydajność maleje drastycznie w stanie mocnego obciążenia sieci. Dlatego też, controlled-load service został zaprojektowany do wprowadzenia w przybliżeniu takiej samej usługi jak usługa best-effort w lekko obciążonej sieci bez względu na aktualny stan sieci. Usługa ta jest opisywana jakościowo jako ta, gdzie brak jest określonych wartości opóźnienia i strat.
Zagadnieniem spornym modelu Integrated Services (Intserv) jest jego skalowalność, szczególnie ma to znaczenie w wielkich sieciach publicznych IP, które mogą potencjalnie mieć miliony aktywnych mikro-strumieni w ruchu tranzytowym równocześnie.
Warto w tym miejscu zauważyć, że model Intserv wymaga jednej bardzo ważnej cechy, a mianowicie jawnej sygnalizacji wymagań QoS od systemu końcowego do wszystkich routerów w sieci, obsługujących dany strumień. Te funkcje sygnalizacyjne spełnia Resource ReserVation Protocol (RSVP). Protokół ten jest krytycznym komponentem modelu usług zintegrowanych (Intserv).


## Architektura IntServ:
- W architekturze IntServ [RFC1633] zakłada się, że zasoby w sieci są rezerwowane dla poszczególnych lub zagregowanych strumieni danych
- RSVP (ReSerVation Protocol) [RFC2205, RFC2210] — specjalny protokół sygnalizacyjny umożliwiający danej aplikacji rezerwację zasobów w sieci
- Implementacja protokołu RSVP jest konieczna w każdym węźle (ruterze IP) 
- Ruter jest odpowiedzialny za przyjmowanie i realizowanie żądań rezerwacji – konieczne jest przechowywanie informacji o każdej rezerwacji wraz z informacją o skojarzonym strumieniu danych
Cechy architektury IntServ:
- Rozszerzenie istniejącego modelu „Best Effort” — przeznaczona dla aplikacji wymagających gwarancji odnośnie parametrów jakości przekazu danych związanych z opóźnieniami, 
- Przydzielanie QoS do przepływów. Przez przepływ należy rozumieć rozróżnialny strumień powiązanych ze sobą datagramów, który został wytworzony przez aktywność pojedynczego użytkownika, i który wymaga jednakowego QoS
- Sterowanie przyjmowaniem zgłoszeń – wymaga się, aby każdy router potrafił podjąć decyzję o przyjęciu do obsługi nowego
- Rezerwacja zasobów – wymaga się, aby każdy router potrafił zarezerwować zasoby w celu zapewnienia QoS obsługiwanym przepływom
- Opis ruchu przy pomocy modelu płynnego – wiadro tokenowe (r – intensywność (szybkość) napływania tokenów, b - głębokość wiadra, p – szybkość szczytowa, m – najmniejsza rozróżnialna wielkość pakietu, M – maksymalny rozmiar pakietu)
Usługi w architekturze IntServ:
- Guaranteed Service [RFC2212] — przeznaczona dla aplikacji wymagających gwarancji odnośnie parametrów jakości przekazu danych związanych z opóźnieniami
- Controlled-load Service [RFC2211] — przeznaczoną dla aplikacji wymagających bezstratnego przekazu danych i charakteryzującą się jakością przekazu określaną jako lepszą niż Best Effort.

### Źródła
[Źródło pierwsze](http://www.tech-portal.pl/content/view/61/45/)
[Źródło drugie](http://www.cisco.com/c/en/us/products/ios-nx-os-software/integrated-services/index.html)
[Źródło trzecie](https://pl.wikipedia.org/wiki/Integrated_Services)

> Adrian Krawczyński, Daniel Cegielski, Damian Kaczyński

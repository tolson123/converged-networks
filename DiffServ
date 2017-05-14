# Wstęp
Ewolucja sieci IP w kierunku sieci wielo-usługowej (Multi-Service Network), czyli sieci umożliwiającej przekaz ruchu generowanego przez różne typy aplikacji (np. mowa, wideo) potrzebuje odpowiednich gwarancji dotyczących przekazu pakietów. Te gwarancje określają parametry jakościowe (Quality of Service - QoS). Dotyczą one charakterystyk opóźnień przekazu pakietów, dopuszczalnego poziomu strat pakietów czy też m.in. średniej szybkości przekazu pakietów. 
Sieci klasy IP QoS dzielimy na: 
określone gwarancje jakości przekazu pakietów-> strict-QoS
dążą do potencjalnie lepszej jakości przekazu dla wybranych strumieni pakietów-> relative-QoS

Dzięki zastosowaniu funkcji przyjmowania nowych wywołań (Admisssion Control - AC) ograniczone jest obciążenie ruchowe sieci.  Metody jakości przekazu pakietów są związane z architekturą sieci oraz usługami sieciowymi (Network Services). Dla IP QoS poza architekturą sieci IP, stworzono dwie architektury takie jak architekturę dla integracji usług sieciowych (Integrated Services - IntServ) oraz architekturę dla zróżnicowania jakości przekazu pakietów w ramach dostępnych usług sieciowych (Differentiated Services - DiffServ) Dla każdej  z nich zdefiniowano mechanizmy pozwalające na różnicowanie przekazu pakietów w węzłach sieci.
Architektura IntServ charakteryzuje się słabą skalowalnością, tzn.wymaga zastosowania sygnalizacji dla zestawienia i utrzymania każdego połączenia w sieci, dlatego też nie jest dalej rozwijana.

# Differentiated Services 
DiffServ  dzieli przepływające datagramy na klasy i zapewniania odpowiednią obsługę w zależności od niej. Domena DiffServ (DS) to obszar sieci, w której zaimplementowany został model DiffServ i składa się z routerów brzegowych (odpowiedzialnych za klasyfikowanie strumieni danych) oraz routerów szkieletowych przesyłających pakiety zgodnie z własnymi politykami. Routery szkieletowe przesyłają strumienie danych zgodnie z zasadami określonymi przez PHB (model określający sposób traktowania danej klasy ruchu rozpoznawanej na podstawie odpowiedniego pola w nagłówku IP). Dzięki temu w porównaniu do modelu IntServ zyskujemy dużą skalowalność i elastyczność.
W architekturze IntServ oprócz standardowej, niesklasyfikowanej usługi typu Best Effort (BS) są jeszcze dwie usługi takie jak: Guaranteed Service GS (RFC 2212), która przeznaczona jest dla aplikacji wymagających gwarancji odnośnie parametrów jakości przekazu danych związanych z opóźnieniami oraz  Controlled Load Service CL (RFC 2211), która przeznaczona jest dla aplikacji wymagających bezstratnego przekazu danych i charakteryzuje się jakością przekazu określaną jako lepszą niż Best Effort.

Zapewnianie jakości usług w DiffServ odbywa się na poziomie pewnej klasy (grupy) połączeń.
Nazwa Diffserv wzięła się m.in. od zdefiniowania w nagłówku IP pola Differentiated Services (pole DS). Składa się ono z 6 bitów które są jedną z części nagłówka IP znanego jako oktet TOS (Type Of Service). Bity ToS są wykorzystywane do przenoszenia informacji odnośnie aplikacji. Priorytety byłyby bezsensowne, gdyby aplikacje nadały sobie najwyższy priorytet, dlatego istnieje możliwość zmiany bitów TOS w czasie wędrówki pakietu od węzła do węzła, co zapobiega takiej sytuacji.
Dzięki usługom Diffserv, w polu DS wskazywana jest tylko skończona liczba klas usług, natomiast w modelu DiffServ jest ograniczenie maksymalnej liczby klas usług różniących się parametrami QoS  do 64. Najbardziej znana zaleta podejścia Diffserv to skalowalność. Na podstawie klas przydziela się zasoby, przy czym z liczbą klas wzrasta liczba stanów (instancji), za to wolniej z ilością strumieni aplikacyjnych. Na odcinku do następnego skoku, zastosowanie modelu Diffserv rozwiązuje problem zarządzania ruchu. Zbiór mechanizmów sterowania mikroinżynieriami ruchu (mikro-TE) obejmuje model sterowania Diffserv. Potrzebne są także inne możliwości inżynierii ruchu- zarządzanie przepustowością (wliczając w to sterowanie trasowaniem) aby dostarczyć akceptowaną jakość usług w sieci Diffserv.

Dla zapewnienia QoS, używa się mechanizmów takich jak:
• kształtowanie i ograniczane przepustowości
• zapewnienie sprawiedliwego dostępu do zasobów
 • nadawanie odpowiednich priorytetów poszczególnym pakietom wędrującym przez sieć
• zarządzanie opóźnieniami w przesyłaniu danych
• zarządzanie buforowaniem nadmiarowych pakietów: DRR, WFQ, WRR
• określenie charakterystyki gubienia pakietów
 • unikanie przeciążeń: Connection Admission Control (CAC), Usage Parameter Control (UPC).



# Diffserv i PHB
Istnieją rodzaje usług PHB:
• Przekazywanie przyśpieszone EF (ang. Expedited Forwarding) 
• Przekazywanie gwarantowane AF (ang. Assured Forwarding) 
• Przekazywanie niesklasyfikowane (bez opcji klasyfikowania). Klasa EF zapewnia małe opóźnienia pakietów oraz małą zmienność opóźnienia- w dodatku pakiety należące do tej usługi mają też zagwarantowane pewne pasmo. Zwykle używana do łączy punkt-punkt o określonych parametrach. Natomiast w przypadku klas usług z grupy AF nie ma gwarancji dotyczącej wielkości opóźnienia pakietów. Istnieją cztery klasy usług AF. Do każdej określono trzy poziomy prawdopodobieństwa odrzucenia pakietu (drop precedence). Jakość usług w ramach danej klasy AF jest zależna od wielkości przydzielonych dla niej zasobów sieciowych.

W ramach architektury DiffServ zdefiniowano dwie główne grupy PHB, takie jak Expedited Forwarding (EF) [RFC3246] oraz Assured Forwarding (AF) [RFC2597].  Grupa EF PHB dotyczy przekazu pakietów, które wymagają obsługi w czasie rzeczywistym, za to grupa AF PHB dotyczy przekazu pakietów w ramach wielu klas ruchu elastycznego.  W celu gwarancji QoS przy przekazie pakietów, w każdym węźle sieci (routerze), powinny być utworzone tzw. bloki dla regulowania ruchu (Traffic Conditioning Blocks - TCB) [RFC3290] stanowiące zestaw wybranych mechanizmów QoS dla regulowania ruchu w ramach danej usługi sieciowej. W zależności od typu routera stosuje się odpowiedni zestaw mechanizmów QoS w ramach bloków TCB. Dla routerów brzegowych, bloki TCB będą zawierały mechanizmy QoS dla obsługi pojedynczych strumieni ruchu, natomiast bloki routerów szkieletowych mechanizmy QoS dla obsługi strumieni zbiorczych.  Na przykład, mechanizmy monitorowania ruchu, które są dedykowane do obsługi pojedynczych strumieni ruchu są stosowane w routerach brzegowych sieci. Dodatkowo, funkcje związane z sygnalizacją QoS oraz metodami AC, a nawet konfiguracja parametrów urządzeń monitorujących ruch, powinny być realizowane tylko na wejściu i wyjściu z sieci szkieletowej.

Inne usługi
W ramach architektury DiffServ można nie tylko używać usługi oferujące ścisłe gwarancje QoS ale zaprojektować także usługi oferujące względne gwarancje QoS. Usługi te nie wymagają zastosowania mechanizmów AC. W ramach IETF, opierając się o EF PHB, zaproponowana została realizacja usługi Premium [RFC2638], dla aplikacji, które generują ruch o stałej szybkości bitowej. Usługa Premium realizuję emulację łącza o stałej szybkości na poziomie pakietów. 
Wymagania QoS dla usługi Premium to: 
Usługa powinna gwarantować bardzo małe opóźnienia przekazu pakietów, małą zmienność tych opóźnień oraz małe straty pakietów. Zakłada się, iż pakiety w ramach usługi Premium będą obsługiwane z najwyższym priorytetem z zastosowaniem odpowiedniej metody AC. W tym przypadku proponuje się zastosowanie metody AC typu REM z alokacją pasma na podstawie szczytowej szybkości bitowej (peak rate allocation scheme). Konieczne jest uprzednie uzgodnienie tzw. „kontraktu ruchowego” między użytkownikiem a siecią. Kontrakt taki jest określany jako Service Level Agreement (SLA) i jest zawierany na podstawie parametrów mechanizmu token bucket, tj. szczytowej szybkości bitowej oraz maksymalnego rozmiaru paczki pakietów. Dodatkowo, w ruterach brzegowych sieci DiffServ ruch, w ramach pojedynczych strumieni, podlega procesowi kształtowania, aby był zgodny z zawartym kontraktem ruchowych na wejściu do sieci szkieletowej i na jej wyjściu. Usługa Premium jest jedną z propozycji realizacji usługi w ramach architektury DiffServ. Przewiduje się, iż jednocześnie sieć może oferować także inne usługi QoS.


# Współpraca modeli IntServ i DiffServ
Model usług zintegrowanych IntServ oraz model usług zróżnicowanych DiffServ poniekąd się uzupełniają- jest możliwość zastosowania ich w różnych obszarach sieci. 
Protokół sygnalizacyjny RSVP, który został opracowany dla modelu IntServ, pozwala zapewniać żądaną jakość obsługi pojedynczym strumieniom danych w relacji od końca do końca. Ze względu na problemy skalowalności, używany jest tylko w małych sieciach- w obszarze sieci dostępowej, obsługującej stosunkowo niewielką liczbę użytkowników, czyli niską liczbę pojedynczych strumieni danych wymagających rezerwacji zasobów sieciowych.
Model DiffServ omija problemy ze skalowalnością poprzez ograniczenie liczby klas usług oraz rezygnacji z protokołu sygnalizacyjnego i dlatego stosuje się go w dużych sieciach. Dzięki obsłudze ruchu zagregowanego, używany jest w sieciach szkieletowych jako element pośredniczący w zapewnieniu jakości usług w relacji od końca do końca.



# Źródła:
https://pl.wikipedia.org/wiki/DiffServ
http://robert.wojcik.staff.iiar.pwr.wroc.pl/dydaktyka/dzienne/zssk/ZSK_5.pdf
http://aai.tele.pw.edu.pl/data/SWUS/swus_diffserv_n.pdf
https://www.ibm.com/support/knowledgecenter/pl/ssw_ibm_i_61/rzak8/rzak8diffserv.htm

(DiffServ Configurations +Implementation Troubleshooting Logs)
http://www.cisco.com/c/en/us/td/docs/ios/12_2/qos/configuration/guide/fqos_c/qcfdfsrv.html



# DCB
Anna Radecka,
Pawel Mizera

#”Technologie konwergentnego data-center: DCB”

DCB to skrót od Data Center Bridging inaczej Mostkowanie Centrum Danych. Jest to zestaw standardów IEEE (Institute of Electrical and Electronics Engineers) umożliwiających działanie konwergentnych sieci szkieletowych w centrach danych, w których magazyn, sieć danych, komunikacja IPC klastrów i ruch związany z zarządzaniem działają w tej samej infrastrukturze sieci Ethernet. DCB zawiera również sprzętowe możliwości przydziału przepustowości dla określonego typu ruchu i zwiększa niezawodność transportu w sieci Ethernet dzięki sterowaniu przepływem na podstawie priorytetu. Przydzielanie przepustowości niezbednie jest oparte na sprzęcie, w momencie gdy ruch omija system operacyjny i jest odciążany do karty sieci konwergentnej, która może  obsługiwać interfejs iSCSI (Internet Small Computer System Interface), zdalny bezpośredni dostęp do pamięci (RDMA) przez konwergentną sieć Ethernet lub protokół FCoE (Fiber Channel over Ethernet). Niezbędne jest również oparcie sterowania przepływem na priorytetach kiedy protokół warstwy wyższej, np. Fiber Channel, zakłada bezstratny transport w warstwie niższej. 

<img src="https://image.slidesharecdn.com/sdnenableddatacenterbridging-130829131938-phpapp01/95/sdnenabled-data-center-bridging-9-638.jpg?cb=1377782467">

Najważniejszymi funkcjami jakie zapewnia DCB jest:

* Zapewnienie współpracy między kartami sieciowymi i przełącznikami z obsługą funkcji DCB.
* Zapewnienie bezstratną transmisję za pośrednictwem sieci Ethernet między komputerem z systemem Windows Serwer 2012 i sąsiadującym przełącznikiem przez włączenie w karcie sieciowej sterowania przepływem na podstawie priorytetów.
*	Zapewnienie bezstratnej transmisji za pośrednictwem sieci Ethernet między komputerem z systemem Windows Server 2012 i sąsiadującym przełącznikiem przez włączenie w karcie sieciowej sterowania przepływem na podstawie priorytetów.
*	Umożliwienie przydzielenia wartości procentowej przepustowości do kontroli ruchu, gdzie kontrola ruchu może składać się z co najmniej jednej klasy ruchu rozróżnianej na podstawie wartości 802.1p.
*	Umożliwienie administratorom serwera lub administratorom sieci przypisanie aplikacji do określonej klasy ruchu lub priorytetu na podstawie dobrze znanych protokołów, dobrze znanego portu TCP/UDP lub portu NetworkDirect używanego przez tę aplikację.
*	Zapewnienie możliwości zarządzania funkcją DCB przy użyciu infrastruktury Instrumentacji zarządzania Windows (WMI) i programu Windows PowerShell w systemie Windows Server 2012.
*	Zapewnienie możliwości zarządzania funkcją DCB przy użyciu zasad grupy w systemie Windows Server 2012.
*	Obsługiwanie współistnienia rozwiązań jakości usług (QoS) w systemie Windows Server 2012.


Aby osiągnąć swoje cele DCB stworzyło i obecnie tworzy nowe standardy. Maja one za zadanie albo rozszerzać obecne protokoły Ethernetu albo emulować połączenia oferowane poprzez Ethernet. Są one tworzone w oparciu o dwa główne standardy:

* The Institute of Electrical and Electronics Engineers (IEEE)
*	Internet Engineering Task Force (IETF). 

Przy nieregularnych topologiach sieci oraz bez specjalnych ruterów DCB może spowodować deadlocks, długie buforowanie i blokowanie. 

Architektura DCB, która jest oparta na kolekcji otwartych standardów rozszerzeń Ethernetu stworzonych w oparciu o IEEE 802.1, skupia się ona na polepszeniu i rozszerzeniu łączności sieciowej Ethernetu i jej zarządzaniu kompatybilnością w Data Center. 
IEEE DCB buduje w oparciu o klasyczne zalety Ethernetu dodając wiele potrzebnych rozszerzeń by pozwolić na lepsza strukturę w sieciach data center i tworzy jednolita infrastrukturę. 

Zaadoptowanymi standardami IEEE są:

*	Priority-based Flow Control (PFC): IEEE 802.1Qbb daje on mechanizm poziomu przepływu połączenia, który może być kontrolowany oddzielnie dla każdego priorytetu. Jego celem jest upewnienie się o zerowej utracie w wypadku zatoru.
*	Dancehall Transmission Selection (ETS): IEEE 802.1Qaz tworzy on jednolite zarządzanie ramą dla przepustowości dla priorytetu.
*	Congestion Notification: IEEE 802.1Qau daje on zarządzanie końcowymi zatorami dla protokołów, które potrafią ograniczać współczynnik transmisji by ominąć ubytki. Używany zwłaszcza przy TCP.
*	Data Center Bridging Capabilities Exchange Protocol (DCBX): protokół wymiany wydajności i odkryć, który jest używany do przekazywania wydajności i konfiguracji wymienionych cech pomiędzy sąsiadami by upewnić się o jednolitej konfiguracji w sieci. Ten protokół wpływa na funkcje IEEE 802.1AB (LLDP). 

Innymi istniejącymi standardami są:

*	The IETF TRILL (Transparent Interconnection of Lots of Links) standard oferujący najmniejszy koszt względem ilości przepływu daty w multi-hop sieciach bez potrzeby konfiguracji w dowolnej topologii. Bezpieczny przepływ nawet w czasie chwilowych pętli. Obsługuje wielowątkowość zarówno w unicast jak i multicast.
*	IEEE 802.1aq Shortest Path Bridging (IEEE 802.1aq) 802.1aq wyszczególnia najkrótsze drogi mostkowania w unicast i multicast ramach Ethernetu aby wyliczyć ilość aktywnych topologii(virtual LANs), które mogą dzielić się poznanymi informacjami o lokacji. 
*	Dwoma operującymi modelami są oparty o przekaz źródłowy Bridge 802.1ad (QinQ) znany jako SPBV oraz 802.1ah (MACinMAC) znany również jako SPBM. SPBV wspomaga VLAN używając VLAN Identyfikator(VID) dla węzła by odnaleźć shortest path tree (SPT) powiązane z węzłem. SPBM wspomaga VLAN używając jednego lub więcej adresów Backbone MAC by znaleźć powiązany z SPT węzeł, może on tez wspomagać wiele topologii aby ładować współdzielone SPT używając jednego B-VID dla wysyłającej topologii. Zarówno SPBV jak i SPBM używają link state routing technologi. SPBM ze względu na swoje MACinMAC kapsułkowanie bardziej nadaje się do większych centrum danych niż SPBV. 
*	Fibre Channel over Ethernet: T11 FCoE Ten protokół używa istniejące protokoły Fibre Channel by uruchamiać serwery w Ethernecie dla dania dostępu serwera do pamięci Fibre Channel poprzez Ethernet. Jednym  z głównych zadań sterowników dla ulepszenia Ethernetu jest wspomaganie przepływu danych. Kiedy iSCSI  był dostępny zależał on od TCP/IP i potrzebował możliwości wspomagania pamięci przesyłu w drugiej warstwie. To spowodowało powstanie prac nad protokołem FCoE, który potrzebował pewnego wspomagania Ethernetu. Ten standard wszedł w życie w czerwcu 2009 zaakceptowała go komisja ANSI T11. 
*	IEEE 802.1p/Q daje on 8 class przepływu dla priorytetów w przesyłaniu.
*	IEEE 802.3bd daje on mechanizm dla link-level w priority pause flow control. 

Te nowe protokoły wymagają nowych urządzeń oraz oprogramowania zarówno dotyczących sieci oraz interfejsu sieciowego. Produkty te są tworzone przez kompanie takie jak: Avaya, Brocade, Cisco, Dell, EMC, Emulex, HP, Huawei, IBM, and Qlogic.

Aby Mostkowanie Centrum Danych dzialo  jest wymagana karta sieciowa Ethernet obsługująca funkcję DCB zainstalowanych w komputerach, na których uruchomiona jest funkcja DCB w systemie Windows Server 2012 oraz wymagane jest wdrożenia przełączników sprzętowych z obsługą funkcji DCB w sieci.

* Źródła: https://www1.cisco.com/ https://technet.microsoft.com/en-us/library/hh849179(v=ws.11).aspx
* Więcej informacji można znaleźć w : http://searchconvergedinfrastructure.techtarget.com/definition/data-center-bridging-DCB http://www.cisco.com/c/en/us/solutions/data-center-virtualization/ieee-802-1-data-center-bridging/index.html https://docs.oracle.com/cd/E26502_01/html/E28993/gmfbf.html http://www.ieee802.org/1/pages/dcbridges.html

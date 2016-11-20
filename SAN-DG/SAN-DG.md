# SAN - Storage Area Network

##1. Podstawowe informacje o SAN. 
####  * SAN jest typem sieci komputerowej, której celem jest udostępnianie zasobów takich jak macierze dyskowe (storage) dla serwerów w ramach organizacji.
####  * Jest to dedykowany typ sieci, do której zazwyczaj nie ma dostępu z sieci LAN organizacji. SAN ma własne dedykowane urządzenia sieciowe.
####  * Zazwyczaj jest to storage typu blokowego.
####  * Według [Storage Network Industry Association](http://www.snia.org/about) głównym celem SAN jest tranfer danych pomiędzy systemami komputerowymi, a urządzeniami storage.
##2. Podstawowe topologie SAN
####  1. Point-to-Point (Punkt-Punkt).
#####    Najprostsza topologia sieci SAN, wykorzystywana do podłączania ze sobą dwóch węzłów (urządzeń). Zakładamy, że nie będziemy skalować infrastruktury poziomo (vertical scaling) - czyli nie będą podłączane nowe urządzenia (węzły).
#####    Przepustowość łącza nie jest współdzielona pomiędzy urządzeniami, więc wykorzystywana jest ona w pełni na potrzeby komunikacji pomiędzy połączonymi węzłami.
#####    Łącze działa trybie pełnego dupleksu - komunikacja może odbywać się jednocześnie w dwóch kierunkach.
####  2. Arbitrated loop (pętla z arbitrażem).
#####    Zwana inaczej siecią FC-AL (Fiber Channel - Arbitrated Loop). Topologia tego typu nie wymaga dodatkowych urządzeń sieciowych takich jak przełączniki SAN. Wszystkie urządzenia połączone są ze sobą w pętlę. Komunikacja odbywa się pomiędzy kolejnymi urządzeniami w pętli, to oznacza że    #####    wszystkie urządzenia muszą działać przy tej samej przepływności (channel capacity). Inaczej mówiąc, sieć działa z najwyższą przepływnością najwolniejszego elementu pętli.
#####    Z uwagi na ograniczenia adresowe w pętli nie może być w niej więcej niż 126 urządzeń - zarządzane są one jako jedna współdzielona szyna transmisji. Ruch odbywa się w jednym kierunku przekazując ramki przez kolejne elementy pętli. Protokół arbitrażu pozwala na ustanowienie jednego        #####    połączenia między nadawcą i odbiorcą, kiedy komunikacja zostaje zrealizowana pomiędzy dwoma portami następuje zwolnienie pętli i może być ustanowione nowe połączenie pomiędzy dwoma portami w pętli. Pętle można skonfigurować z Hubami w celu ułatwienia zarządzania połączeniami.           #####    Dystans do 10 km jest wspierany przez standard Fibre Channel, jednak długość pętli wpływa na opóżnienia w komunikacji.  
####  3. Switched Fabric (pełna sieć - tzw. Fabric)
#####    Najbardziej przydatna topologia, wykorzystująca przełączniki i inne urządzenia sieciowe. Zwana inaczej Fibre Channel Switched Fabric (FC-SW). Fabric ma przynajmniej jeden przełącznik SAN w ramach swojej konfiguracji. Przełączany Fabric zapewnia pełną szerokość pasma w medium transmisyjnym #####    (bandwidth) na każdy port w porównaniu ze współdzieloną szerokością pasma w przypadku implementacji pętli z arbitrażem. Najważniejszą różnicą pomiędzy FC-AL, a FC-SW jest to że dodanie nowego urządzenia w FC-AL powoduje dalszy podział współdzielonej szerokości pasma. W przypadku FC-SW #####    przepustowość pasma w medium transmisyjnym zostaje zwiększona. Powoduje to stopniowe odchodzenie od topologii FC-AL.                                                                                                                                                                               

##3. Warstwy Fibre Channel:
#### FC0
#### FC1 
#### FC2
#### FC3
#### FC4

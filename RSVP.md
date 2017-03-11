## RSVP


RSVP (_Resource ReSerVation Protocol_) jest protokołem, który zaprojektowano w celu dostarczania aplikacjom internetowym, a dokładniej generowanemu przez nie ruchowi, różnych poziomów jakości obsługi QoS (pierwotnie planowano jego użycie łącznie z IntServ). 

Dotyczy to przede wszystkim rezerwacji zasobów (pierwotnie przepływność, później np. etykiety). Wiadomości protokołu RSVP nie korzystają z żadnego protokołu transportowego (są wprost przenoszone w datagramach IP). 
Protokół ten jest wykorzystywany przez rutery w celu zapewnienia odpowiedniej jakości usług żądanych we wszystkich węzłach komunikacyjnych wzdłuż określonej ścieżki transmisji strumieni danych, głosu, obrazu itp. 
RSVP został opracowany w celu współpracy z istniejącymi protokołami rutingu. Protokół ten dobrze współdziała również z techniką MPLS. 

Protokół RSVP-TE (_Resource ReSerVation Protocol with Traffic Engineering extensions_) jest rozszerzeniem protokołu RSVP, które powstało w celu zestawiania ścieżek LSP w sieciach MPLS. Nowymi funkcjami protokołu jest dystrybucja etykiet, jak również przenoszenie informacji o tunelu MPLS. Tunel pozwala na implementację różnych polityk obsługi ruchu w celu optymalizacji działania sieci. Protokół ten pomaga w zestawieniu ścieżki LSP rozsyłając do wszystkich urządzeń, które mają uczestniczyć w transmisji wiadomości:  
- Path w kierunku wysyłania danych,
- Resv w kierunku przeciwnym do transmitowanych danych.
Wiadomość RSVP Path używa pola LABEL REQUEST do zażądania powiązania etykiety wejściowej z wyjściową w każdym węźle. Pole SESSION ATTRIBUTE zawarte w RSVP Path określa atrybuty ścieżki LSP (np. priorytet, wymagany poziom protekcji). 
Pole ROUTE zawiera ścieżkę, którą podąża wiadomość RSVP Path. Wiadomość RSVP Resv używa z kolei bloku LABEL do dystrybucji etykiet. 
Pole RECORD ROUTE obecne zarówno w RSVP Path, jak i RSVP Resv gromadzi informacje o węzłach/etykietach, które zostały odwiedzone/przyznane po drodze. W ten sposób wiadomości RSVP Resv przenoszą numery etykiety nadanej danemu węzłowi w kontekście określonego tunelu, dzięki czemu nowa ścieżka zostaje zestawiona. 
Rezultatem żądania RSVP będzie rezerwacja zasobów w każdym węźle należącym do ścieżki, ale tylko w jednym kierunku (tunele są jednokierunkowe). Proces RSVP korzystając w węźle wejściowym z lokalnej tablicy rutingu stara się dobrać przebieg ścieżki LSP do określonego rutera końcowego (na tym polega właśnie ruting źródłowy).

RSVP nie jest więc odpowiedzialny za wybór trasy. W praktyce rezerwacja etykiet za pomocą RSVP wygląda następująco: ruter wejściowy dla tunelu (ścieżki) generuje wiadomość RSVP Path, która jest przesyłana do kolejnych urządzeń na trasie aż do rutera kończącego tunel (ścieżkę). W odpowiedzi ruter kończący ścieżkę generuje wiadomość RSVP Resv, która jest przesyłana do każdego węzła na ścieżce. W trakcie trwania tej operacji każdy ruter na ścieżce dokonuje rezerwacji zasobów (o ile nimi dysponuje). Oprócz omówionych wcześniej wiadomości Path i Resv, RSVP używa kilku innych. Służą one głównie do poinformowania o wystąpieniu jakiegoś problemu. PathTear jest wysyłana przez ruter w celu powiadomienie o usunięciu aktywnej ścieżki. ResvTear jest odpowiedzią na PathTear. PathErr jest to wiadomość przesyłana w kierunku urządzenia wejściowego. Najbardziej prawdopodobną przyczyną jej wygenerowania jest uszkodzenie łącza, a co za tym idzie przerwanie ścieżki lub niepowodzenie w ustanowieniu ścieżki.

### Źródła
[Źródło pierwsze](http://www.tech-portal.pl/content/view/81/37/)
[Źródło drugie](https://pl.wikipedia.org/wiki/Resource_Reservation_Protocol)
[Źródło trzecie](http://www.tech-portal.pl/content/view/62/45/)


> Adrian Krawczyński, Daniel Cegielski, Damian Kaczyński

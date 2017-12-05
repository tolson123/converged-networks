# Best Effort
Best Effort jest mechanizmem, który traktuje wszystkie pakiety jednakowo i wysyła je z najwyższą możliwą przepustowością. Nie gwarantuje poziomu usług QoS. Jest najczęściej spotykanym sposobem postępowania z kolejkami pakietów w Internecie. 
Best Effort używany jest w przypadku usług i sieci, w których czas dostarczenia jest ważniejszy niż dokładność. Nadawca nie ma pewności czy pakiety zostały dostarczone, a w przypadku uszkodzenia lub zagubienia nie następuje retransmisja. W przypadku transferu w czasie rzeczywistym audio lub wideo, utrata niewielkiego procentu nie ma zauważalnego wpływu na odbierany obraz lub dźwięk. Odzyskiwanie utraconych lub uszkodzonych pakietów powoduje obciążenie sieci i zmniejszenie wydajności.

### Protokół IP
Obsługuje komunikację w Internecie, nie zapewnia żadnego mechanizmu określającego, czy pakiet dociera do miejsca docelowego, czy nie. IP tylko martwi się o weryfikację integralności przesyłanych danych, stosując sumy kontrolne do nagłówków pakietów. Z tego powodu mówi się, że IP zapewnia niewiarygodną usługę datagramu, ponieważ nie gwarantuje odbioru wszystkich pakietów. Ten brak gwarancji w dostawie może spowodować, że uszkodzone, zduplikowane pakiety dotrą do odbiorcy, a nawet, że niektóre pakiety zostaną utracone po drodze. Zgodnie z modelem odniesienia OSI, kontrola niezawodności transmisji jest obowiązkiem protokołów warstwy transportowej, takich jak TCP.

### UDP
Warstwa transportowa segmentuje dane oraz składa je w tzw. strumień. Warstwa ta zapewnia całościowe połączenie między stacjami: źródłową oraz docelową, które obejmuje całą drogę transmisji. Następuje tutaj podział danych na części, które są kolejno indeksowane i wysyłane do docelowej stacji. Na poziomie tej warstwy do transmisji danych wykorzystuje się dwa protokoły TCP (ang. Transmission Control Protocol) oraz UDP (ang. User Datagram Protocol). Oba protokoły warstwy transportowej stosują kontrolę integralności pakietów, a pakiety zawierające błędy są odrzucane.

![obraz](tcpudp.jpg)

**UDP** jest protokołem bezpołączeniowym nie podlegającym automatycznemu ograniczaniu prędkości oraz nie posiadającym mechanizmów kontroli przepływu i retransmisji danych. Protokół ten nie kontroluje poprawności danych. Używany jest w strumieniowaniu multimediów, telefoni VOIP, routingu, DNS, sieci P2P, SMTP, TFTP.

![obraz1](udp.gif)

**UDP-Lite** (Lightweight User Datagram Protocol) jest protokołem bezpołączeniowym, który umożliwia dostarczenie potencjalnie uszkodzonego ładunku danych do aplikacji, a nie odrzucenie go przez stację odbiorczą. Jest to użyteczne, ponieważ pozwala podejmować decyzje dotyczące integralności danych w warstwie aplikacji, gdzie zrozumiane jest znaczenie bitów.

Bazuje na UDP, ale UDP-lite pozwala na częściowe sumy kontrolne, które obejmują tylko część datagramu, a zatem dostarczy pakiety, które zostały częściowo uszkodzone. Zaprojektowany dla multimedialnych protokołów takich jak VOIP, transfer video i audio w czasie rzeczywistym, w przypadku których lepiej dostać uszkodzone pakiety niż nie dostać ich wcale.

### Ograniczenia modelu Best Effort
Wady modelu Best Effort doprowadziły do pojawienia się bardziej niezawodnych alternatyw zaprojektowanych, w celu zapewnienia wysokiej jakości usług (QoS) i niezawodności w komunikacji. 
Tak jest w przypadku tak zwanych usług zróżnicowanych (DiffServ) i usług zintegrowanych (IntServ), oba zapewniają usługę sieciową, która gwarantuje ostateczne dostarczenie danych.

### Źródła:
* http://www.linfo.org/best_effort.html
* https://es.wikipedia.org/wiki/Entrega_de_mejor_esfuerzo
* http://www.inetdaemon.com/tutorials/internet/tcp/tcp_header.shtml

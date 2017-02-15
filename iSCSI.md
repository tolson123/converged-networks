# iSCSI

**iSCSI** (ang. Internet SCSI) – technika umozliwiajaca wykonywanie operacji wejscia-wyjscia na dysku twardym odleglej maszyny za pomoca protokolu TCP/IP. Protokol iSCSI umozliwia budowe systemow pamieci masowych SAN (ang. Storage Area Network) przy zastosowaniu macierzy dyskowych SCSI i sieci Ethernet (protokol TCP/IP). Najwieksza zaleta iSCSI jest mozliwosc tworzenia rozleglych systemow SAN przy wykorzystaniu typowych elementow sieciowych, co ulatwia budowe systemu i zmniejsza jego koszt w porownaniu z klasycznymi rozwiazaniami typu Fibre Channel. Specyfikacja iSCSI okresla sposob transformacji rownoleglych polecen SCSI na format TCP/IP i na odwrot. Transformacja polecen moze byc realizowana zarowno sprzetowo, jak i programowo.

# Jak to dziala

iSCSI to protokol opierajacy sie o enkapsulacje polecen SCSI wewnatrz protokolu TCP/IP. Jest to wiec swego rodzaju wirtualizacja dostepu do urzadzenia blokowego. Z podobnych technologii mozna wspomniec HyperSCSIczy ATAoE – protokoly przekazujace odpowiednio polecenia SCSI i ATA bezposrednio w ramkach Ethernet. W odroznieniu od nich iSCSI moze byc rutowane (ale ma w zwiazku z tym wiekszy narzut w postaci dodatkowych naglowkow TCP/IP). Ponadto iSCSI pozwala na obustronne uwierzytelnienie za pomoca protokolu CHAP.

Zasada dzialanie jest bardzo prosta. Po stronie serwera (w terminologii iSCIS – target) dziala demon _ietd_ (iSCSI Enterprise Target), ktory eksportuje wskazane urzadzenia blokowe. Po stronie klienta dziala demon _open-iscsi_ (inicjator), ktorego zadaniem jest nawiazanie polaczenia i komunikacja z targetem oraz utworzenie urzadzen blokowych (np. sdb, sdc, itd.) w katalogu _/dev_. Utworzone przez inicjator urzadzenia widoczne sa w systemie klienckim jak zwyczajne dyski SCSI czy SATA.

# Komunikacja iSCSI

Jak opisano wyzej w komunikacji iSCSI dochodzi do wymiany komunikatow pomiedzy inicjatorem i celem iSCSI. Komunikacja zawsze rozpoczyna sie od wyslania zapytania przez inicjator iSCSI. W komunikacji wykorzystane moze byc jedno lub wiele  **polaczen iSCSI**  (iSCSI connection). Jedno polaczenie iSCSI odpowiada jednemu polaczeniu TCP. Komunikacja pomiedzy inicjatorem i celem iSCSI okreslana jest mianem  **sesji iSCSI**.

Ponizsza grafika obrazuje schematyczna budowe zestawu iSCSI:


![image](https://cloud.githubusercontent.com/assets/25791214/22972245/1bc211ca-f379-11e6-8b4a-4839b75f7ec7.png)


**Typy sesji iSCSI**

Wystepuja dwa typy sesji iSCSI:

- --Normal operational session: nielimitowana sesja iSCSI.
- --Discovery session: Ta sesja sluzy tylko do wykrywania celow iSCSI. Cel iSCSI przyjmuje tylko zapytania SendTargets.

Typ sesji iSCSI definiowany jest podczas logowania iSCSI.

# Podsumowanie

Technologia  iSCSI jest ciekawa alternatywa dla tych, ktorych nie stac na Fibre Channel. Za jej pomoca mozemy zbudowac funkcjonalna i niedroga „macierz&quot; , a korzystajac z pakietow DRBD oraz Heartbeat – mozna zbudowac wysokowydajna macierz replikowana w czasie rzeczywistym. Nalezy jednak pamietac, ze serwer iSCSI nie kontroluje rownoczesnego dostepu do urzadzen wiec rownoczesne wykorzystanie wolumenow na kilku maszynach wymaga zastosowania dodatkowych mechanizmow zabezpieczajacych jak np. klastrowy system plikow.

Zrodla informacji:

- -- [https://pl.wikipedia.org/wiki/ISCSI](https://pl.wikipedia.org/wiki/ISCSI)
- -- [http://www.gumularz.net/linux-tips/2009/10/iscsi-czyli-fibre-channel-dla-ubogich/](http://www.gumularz.net/linux-tips/2009/10/iscsi-czyli-fibre-channel-dla-ubogich/)

Dmytro Zozulia

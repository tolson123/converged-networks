Przykłady DSCP
=============
Spis treści
---------------
* [DSCP oparte o QoS z HTB](#dscp-oparte-o-qos-z-htb)
* [Znakowanie DSCP](#znakowanie-dscp)
* [Konfiguracja drzewa klas](#konfiguracja-drzewa-klas)
* [Dalsze udoskonalenia (według BrotherDust)](#dalsze-udoskonalenia-według-brotherdust)
* [Komentarz do różnic pomiędzy modyfikacja a pierwszym przykładem](#komentarz-do-różnic-pomiędzy-modyfikacja-a-pierwszym-przykładem)
* [Architektura Diffserv – RFC2475](#architektura-diffserv--rfc2475)
* [Klasyfikacja i oznaczanie](#klasyfikacja-i-oznaczanie)
* [Narzędzia klasyfikacji IP Precedence i DiffServ Code Points](#narzędzia-klasyfikacji-ip-precedence-i-diffserv-code-points)
* [Źródła](#Źródła)

---------------------

DSCP oparte o QoS z HTB
------------------------------------
Na tej tablice opisany jest sposób priorytetyzowania ruchu przy użyciu znaczników (tags) DSCP. DiffServ Code Point jest polem w nagłówku IP, który pozwala na klasyfikacje ruchu. Założeniem DSCP jest zarządzanie sposobem per-hob-based, pozwalającym każdemu routerowi w trasie określić, jaki każda klasa ruchu powinna otrzymać priorytet. Rozwiązanie opisane w tym dokumencie jest oparte o algorytm kolejkowania Hierarchical Token Bucket, rozdzielający 64 możliwe kombinacje wartości pola DSCP na 8 dostępnych kolejek. Ponadto, to rozwiązanie wykorzystuje drzewo klas (drzewo kolejek): kontrolę pasma pełni klasa-rodzic mający klasy potomne dla każdej możliwej wartości DSCP.

Kolejkowanie realizowane jest jak na tej tablicy:

Nazwa klasy | Uprzywielojowanie | Zakres DSCP |Prioritetowanie HTB
:------------------|:------------------|:--------------------------|:-------------------
Routing (domyślne)| 000 (0)           |000000(0) – 000111 (7)      |8
Priorytet         | 001 (1)           |001000 (8) – 001111 (15)    |7
Pilny             | 010 (2)           |010000 (16) – 010111 (23)   |6
Błyskawiczny      | 011 (3)           |011000 (24) – 011111 (31)   |5
Błyskawiczny Uprzywilejowany| 100 (4) |100000 (32) – 100111 (39)   |4
Krytyczny         | 101 (5)           |101000 (40) – 101111 (47)   |3
Sterowanie międzysieciowe| 110 (6)    |111000 (48) – 110111 (55)   |2
Sterowanie sieci  | 111 (7)           |111000 (56) – 111111 (63)   |1

To rozwiązanie zostało przetestowane na RB450, RB600 i RB1000 przy użyciu dowolnego interfejsu 3.x.

----------

Znakowanie DSCP
-------------------------
Aby dobrać wartości DSCP dla klas, należy oznakować pakiety używając firewall'a ze znakowaniem Najlepiej jest to zrobić tym poleceniem:
```
:for x from 0 to 63 do={/ip firewall mangle add action=mark-packet chain=postrouting \
comment=("dscp_" . $x . "_eth") disabled=no dscp=$x new-packet-mark=("dscp_" . $x . "_eth") passthrough=no}
```


To polecenie tworzy 64 linie w */ip firewall mangle*, które znakując każdy pakiet z ustawioną wartością DSCP do dalszego przetwarzania.

----------

Konfiguracja drzewa klas
-------------------

W poniższym przykładzie założono, że ether1 jest interfejsem WAN, a dostępne pasmo jest równe 5Mbit/s.
```
/queue tree
add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=5000000 name=ether1 \
parent=ether1 queue=default

#prio8
:for z from 0 to 7 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("routine_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=8 queue=ethernet-default}

#prio7
:for z from 8 to 15 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("priority_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=7 queue=ethernet-default}

#prio 6

:for z from 16 to 23 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("immediate_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=6 queue=ethernet-default}

#prio 5
:for z from 24 to 31 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("flash_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=5 queue=ethernet-default}
#prio 4
:for z from 32 to 39 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("flash_override_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=4 queue=ethernet-default}
 
#prio 3`
:for z from 40 to 47 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("critical_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=3 queue=ethernet-default}

#prio 2
:for z from 48 to 55 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("intercon_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=2 queue=ethernet-default}
 
#prio 1
:for z from 56 to 63 do={/queue tree add burst-limit=0 burst-threshold=0 burst-time=0s disabled=no limit-at=0 max-limit=0 \
name=("netcon_" . $z . "_ether1") packet-mark=("dscp_" . $z . "_eth") parent=ether1 priority=1 queue=ethernet-default}
```

**Komentarz** 

>Głównym założeniem jest to, że największe oznakowanie DSCP jest obsługiwane jako pierwsze. Kształtowanie ruchu na interfejsie może zostać przeniesione do prostej kolejki w celu różnej polityki dla ruchu w górę i w dół, ale ja preferuje kształtowanie ruchu dla obu stron. Jeśli masz różne prędkości w obie strony, powinieneś kształtować względem prędkości w górę.

--------

Dalsze udoskonalenia (według BrotherDust)
------------------------------

Używając powyższego skryptu jako punktu początkowego, można opracować poniższy skrypt:
```
#Set interface here
:global outboundInterface "ether1"
#Set bandwidth of the interface (remember, this is for OUTGOING)
:global interfaceBandwidth 0
#Set where in the chain the packets should be mangled
:global mangleChain postrouting

#Don't mess with these. They set the parameters for what is to follow
:global queueName ("qos_" . $outboundInterface)
:global qosClasses [:toarray "netcon,intercon,critical,flash_override,flash,immedate,priority,routine"]
:global qosIndex 64

#Set up mangle rules for all 64 DSCP marks
#This is different in that the highest priority packets are mangled first.
:for indexA from 63 to 0 do={
	/ip firewall mangle add \
	action=mark-packet \
	chain=$mangleChain \
	comment=("dscp_" . $indexA) \
	disabled=no \
	dscp=$indexA \
	new-packet-mark=("dscp_" . $indexA) \
	passthrough=no
}

#Add a base queue to the queue tree for the outbound interface
/queue tree add \
	max-limit=$interfaceBandwidth \
	name=$queueName \
	parent=$outboundInterface \
	priority=1

#Set up queues in queue tree for all 64 classes, subdivided by 8.`
:for indexA from=0 to=7 do={
	:local subClass ([:pick $qosClasses $indexA] . "_" . $outboundInterface)
	/queue tree add \ 
		name=$subClass \
		parent=$queueName \
		priority=($indexA+1) \
		queue=ethernet-default
	:for indexB from=0 to=7 do={
		:set qosIndex ($qosIndex-1)
		/queue tree add \
		name=($subClass . "_" . $indexB) \
		parent=$subClass \
		priority=($indexB+1) \
		packet-mark=("dscp_" . $qosIndex) \
		queue=ethernet-default
     }
}
```

Ten skrypt tworzy więcej struktur priorytetów przez tworzenie 64 różnych klas zgrupowanych w 8 klasach nadrzędnych. Więc tak będzie to wyglądało w kolejkach interfejsu gdy wpiszesz skrypt do konsoli:

![] (http://mikrotik.net.pl/w/images/2/25/QoS_Structure.png)

Kilka praktycznych uwag:
1. Warto pamiętać! Sposób w jaki skonfigurowany jest skrypt domyślnie, działa tylko na ruch wychodzący. Najlepiej skonfigurować wszystko tak, aby nie było potrzeby kształtowania ruchu przychodzącego.
2. Jeśli skrypt będzie użyty dla więcej niż jeden interfejsów, usuń odpowiednie polecenia w skrypcie, ponieważ nie ma potrzeby ponownego tworzenia reguł znakowania.
3. Należy ustawić parametr wielkości pasma, jeśli masz interfejs z określoną szerokością pasma, lub gdy chcesz ograniczyć ruch na tym interfejsie. Określony jest w bitach na sekundę.

--------------

Komentarz do różnic pomiędzy modyfikacja a pierwszym przykładem
-------------

Strategia znakowania DSCP w tym przypadku jest całkowicie inna niż w pierwszym skrypcie. Zwróć uwagę, czy pasuje ona do Twojej konfiguracji QoS zanim uruchomisz skrypt. Np. RouterOS automatycznie oznacza dynamiczny routing wartości DSCP 48 i w tym przykładzie aktualizacje routingu otrzymają priorytet 8, który jest najniższym priorytetem. W praktyce sugeruję, aby obsługiwane były tylko te kody DSCP, które są używane w Twojej sieci. Przykładem aktualną konfiguracją znakowania wygląda tak:

```
/ip firewall mangle add action=mark-packet chain=postrouting comment=dscp.0 disabled=no \
dscp=0 new-packet-mark=dscp.0 passthrough=no
/ip firewall mangle add action=mark-packet chain=postrouting comment=dscp.46 disabled=no \
dscp=46 new-packet-mark=dscp.46 passthrough=no
/ip firewall mangle add action=mark-packet chain=postrouting comment=dscp.48 disabled=no \
dscp=48 new-packet-mark=dscp.48 passthrough=no
:for x from 1 to 45 do={/ip firewall mangle add action=mark-packet chain=postrouting \
comment=dscp.1-45 disabled=no dscp=$x new-packet-mark=dscp.other passthrough=no}
/ip firewall mangle add action=mark-packet chain=postrouting comment=dscp.47 disabled=no \
dscp=47 new-packet-mark=dscp.other passthrough=no
:for x from 49 to 63 do={/ip firewall mangle add action=mark-packet chain=postrouting \
comment=dscp.49-63 disabled=no dscp=$x new-packet-mark=dscp.other passthrough=no}
```

To daje cztery oznaczenia: 

- dscp.0 dla pakietów nie mających ustawionego DSCP
-  dscp.46 dla pakietów EF (mój ruch VoIP)
- dscp.48 dla aktualizacji routingu
- dscp.other dla wszystkich pozostałych wartości DSCP

Po takiej konfiguracji układamy drzewo klas, w którym pakiety nieoznakowane mają najniższy priorytet. Następne w kolejności są: dscp.other, dscp.46 i dscp.48. Pakiety aktualizacji routingu powinny mieć największy priorytet - bez nich nic nie działa. Następnie VoIP i inne. Najniższy priorytet mają pozostałe nieoznakowane pakiety

----------

Architektura Diffserv – RFC2475
--------------------

- Mały poziom złożoności – brak utrzymania stanów czy sygnalizacji
- Usługi tworzone są przez kombinację złożonej klasyfikacji, oznaczania, ewentualnie przycinania ruchu na brzegu sieci i konfiguracji szkieletu (PBH)

![]
(http://s8.hostingkartinok.com/uploads/images/2017/02/e4365eb18829dcecb074a9f34949953b.jpg)

------------

Klasyfikacja i oznaczanie
-----------------------------------
Klasyfikacja i oznaczenie z lokalną polityką powinna być realizowana jak tylko blisko się zródła ruchu. Najlepiej gdy w całej sieci daje się stosować zunifikowany schemat oparty o IP DSCP.

![] (http://s8.hostingkartinok.com/uploads/images/2017/02/b3e2b5b5e9532a6afa2892ccff166537.jpg)

-------------------

Narzędzia klasyfikacji IP Precedence i DiffServ Code Points
-----------------------------
![] (http://s8.hostingkartinok.com/uploads/images/2017/02/a615a08599672ed11b7f38c377454d0c.jpg)

----------------

Źródła
---------------
- [DiffServ](https://pl.wikipedia.org/wiki/DiffServ)
- [DSCP oparte o QoS z HTB](http://mikrotik.net.pl/wiki/DSCP_oparte_o_QoS_z_HTB)
- [Mechanizmy QoS Jak projektować, wdrażać i monitorować Łukasz Bromirski](http://docplayer.pl/1009536-Mechanizmy-qos-jak-projektowac-wdrazac-i-monitorowac-lukasz-bromirski-lbromirski-cisco-com.html)

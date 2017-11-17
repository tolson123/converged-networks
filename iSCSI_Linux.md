# Instalacja i konfiguracja serwera/klienta iSCSI na systemie Debian9/Fedora24







## Serwer Debian/Fedora


#### Instalacja potrzebnego oprogramowania:

###### Debian
```
# apt-get install targetcli-fb
```

###### Fedora
```
# apt-get install targetcli
```

#### Utworzenie katalogu dla wirtualnych dysków iSCSI
```
mkdir /home/user/iscsi_hdd
```
W miejsce user należy podać nazwę użytkownika


#### Konfiguracja/utworzenie napędów iSCSI

###### Konsola do zarządzania
```
targetcli
```

###### Utworzenie wirtualnego dysku
```
cd backstores/fileio
create disk01 /home/user/iscsi_hdd/disk01.img 100G
```
disk01 - nazwa
/home/user/iscsi_hdd/hdd1.img - ścieżka oraz nazwa pliku z wirtualnym dyskiem
100G - rozmiar wirtualnego dysku w Gigabajtach.
UWAGA! Dysk nie jest dynamiczny. Oznacza to, że zajmie on od razu taką powierzchnię na dysku jaka zostanie mu przypisana.

###### Utworzenie 'udziału' sieciowego
```
cd /iscsi
create iqn.2017-11.convergent.srv:storage.target01
```

###### Ustawienie LUN
```
cd iqn.2017-11.convergent.srv:storage.target01/tpg1/luns
create /backstores/fileio/disk01
```

###### Ustawienie ACL
```
cd ../acls
create iqn.2017-11.convergent.srv:www.srv.convergent
```

###### Ustawienie autoryzacji
```
set auth userid=user
set auth password=haslo
```

###### Opuszczenie konsoli do zarządzania
```
exit
```

#### Weryfikacja uruchomionej usługi
```
ss -napt | grep 3260
```

#### FEDORA - Włączenie 'udziału'
```
systemctl enable target
```  

#### FEDORA - Dodanie wyjątku do zapory
```
# firewall-cmd --add-service=iscsi-target --permanent
# firewall-cmd --reload
```



## Klient Debian9/Fedora24


#### Instalacja potrzebnego oprogramowania
###### Debian
```
# apt-get install open-iscsi
```

###### Fedora
```
# iscsi-initiator-utils
```

#### Konfiguracja nazwy udostępnionego zasobu
###### Należy podać taką samą nazwę jaka została ustawiona podczas tworzenia udziału w sekcji serwer
```
# nano /etc/iscsi/initiatorname.iscsi

InitiatorName=iqn.2017-11.convergent.srv:www.srv.convergent
```

#### Konfiguracja autoryzacji
```
# nano /etc/iscsi/iscsid.conf

Odkomentować linię 56
node.session.auth.authmethod = CHAP

Ustawić login/hasło w liniach 60,61 (takie jak podane w sekcji serwer)
node.session.auth.username = login
node.session.auth.password = haslo
```

#### DEBIAN - Restart usługi
```
# systemctl restart iscsid open-iscsi
```

#### Ustawienie adresu serwera
```
# iscsiadm -m discovery -t sendtargets -p 192.168.1.100
```
W ostatniej pozycji należy podać adres IP komputera, na którym uruchomiony jest serwer iSCSI

#### Weryfikacja ustawień udziału
```
# iscsiadm -m node -o show
```

#### Logowanie do udziału
```
# iscsiadm -m node --login
```

#### Weryfikacja podłączonego udziału
```
iscsiadm -m session -o show
```

#### Sprawdzenie czy udział pojawia się jako fizyczny dysk
```
# fdisk -l
```


###### Żródło

[https://wiki.debian.org/SAN/iSCSI/open-iscsi](https://wiki.debian.org/SAN/iSCSI/open-iscsi)

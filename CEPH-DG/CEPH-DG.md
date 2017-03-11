# Ceph Filesystem

	Dariusz Gawron, Mariusz Okularczyk, Krzysztof Czech

##1. Podstawowe informacje o Ceph.

### 1.1. Ceph jest systemem plików zgodnym z POSIX, wykorzystującym [**Ceph Storage Cluster**](http://docs.ceph.com/docs/jewel/rados/).  
### 1.2. Ceph jest z założenia rozproszonym systemem zarządzającym i udostępniajacym dane (Distrubuted Data Storage Platform).

### 1.3. System składa się z przynajmniej trzech serwerów (wirtualnych lub fizycznych) zwanych węzłami (nodes).

### 1.4. Ceph jest stosowany m. in. w Openstack'u. Jest stosowany w OpenStack Swift. Poza tym warto wspomnieć, że CEPH object storage jest dostępny poprzez Amazon Simple Storage Service (S3).

##2. Rodzaje storage, które wspiera Ceph:

### 2.1. Obiektowy (Object Storage)

#### Ten typ storage oparty jest na obiektach. Dane przechowywane są jako obiekty i odczytywane, zmieniane poprzez interfejsy RESTowe lub SOAPowe (RESTful HTTP APIs). Należy pamiętać o tym, że ten typ storage nie jest obiektowym NAS lub SAN. Obiekty są przechowywane w "szerokiej" przestrzeni nazw (namespace), jest to struktura płaska - dlatego nie jest zachowywana ich dokładna hierarchia, w przeciwieństwie do bardziej tradyjnych technologii storage.

#### Przechowywane obiekty nie są przyjazne dla użytkownika, dlatego konieczne jest stosowanie RESTowego API w celu interakcji z przechowywanymi obiektami.

#### Dostęp do OSDs (Object storage devices) nie odbywa się z wykorzystaniem jakiegokolwiek protokołu plikowego, takiego jak: BFS, SMB, CIFS.

#### Storage obiektowy może nie spełniać wymagań dotyczących przechowywania danych o określonej strukturze, z naciskiem na wysoką wydajność, które podlegają ciągłej zmianie. Mowa jest głównie o bazach danych.

### 2.2. Blokowy (Block device)

#### Storage blokowy w CEPH jest realizowany poprzez Ceph Block Device. Jest to wirtualny dysk twardy, który "podpinamy" do fizycznych instalacji opartych na systemach Linux lub do takich maszyn wirtualnych. CEPH wykorzystuje RADOS (Reliable Autonomic Distributed Object Storage) w celu realizacji funkcji blokowego storage, takich jak: Migawki (snapshots) i replikacja (replication). Urządzenie blokowe RADOS jest zintegrowane tak by działać jako back-end dla OpenStack Block Storage.  
### 2.3. System plików (plikowy) - CEPH Filesystem, CephFS.

#### Storage typu plikowego jest realizowany poprzez zastosowanie systemu zgodnego z POSIX (Portable Operating System Interface) - systemu plików Ceph File System (CephFS). CephFS przechowuje dane w Ceph Storage Cluster. Ceph wykorzystuje ten sam system klastrowy jak Ceph Block Storage i Ceph Object Storage.

##3. Elementy klastra storage'owego CEPH:


![Elementy Ceph](/CEPH-DG/Grafiki/Ceph_components.svg)


### OSD - fizyczne lub logiczne (np. LUN) urządzenie storage.
### 3.1. OSDs, Object Storage Devices Daemon - oprogramowanie, które działa z OSD, jeden z elementów obowiązkowych stosu CEPH. Jest odpowiedzialne za przechowywanie danych, zarządzanie replikacją danych, odzyskiwaniem, zarządzaniem obciążeniem. Ponadto wysyła informacje na temat działania systemu do Ceph monitor, poprzez sprawdzanie pozostałych OSDs Daemons w systemie.
### Klaster Ceph Storage wymaga przynajmniej dwóch Ceph OSDs Daemons by uzyskać stan **active + clean**, kiedy klaster robi dwie kopie danych (Ceph domyślnie robi 3 kopie ale jest to ustawienie w konfiguracji klastra). 
### 3.2. Monitor - oprogramowanie monitorujące, instalacja CEPH musi posiadać określoną liczbę serwerów monitorujących. Podtrzymuje aktualizowane mapy stanów klastra (monitor map, OSD map, Placement Group - PG map, CRUSH map). Ceph zapisuje historię (tzw. **epoch**) każdej zmiany stanu klastra  i jego elementów (OSDs Daemons, Ceph Monitors, PGs).
### 3.3. Metadata Server (MDS) - przechowuje metadane, dla systemu Ceph filesystem (Ceph Block storage, Object storage nie wykorzystują tego serwera). MDS umożliwia wykonywanie przez użytkowników podstawowych poleceń takich jak: ls, find itd., bez zbędnego obciążania reszty klastra Ceph.
### **Ceph przechowuje dane jako obiekty w pulach zasobów storage (storage pools).
##4. Element wyróżniający CEPH - algorytm CRUSH.
### **Controlled Replication Under Scalable Hashing** - tzw. CRUSH. Algorytm wykorzystywany w Ceph do "obliczania" lokalizacji danego obiektu w odpowiedniej Placement Group (PG), póżniej oblicza który OSD Daemon powinien przechowywać PG. Algorytm CRUSH pozwala na dynamiczne skalowanie, load-balancing oraz odzyskiwanie.
##5. Oprogramowanie oraz bilbioteki.

![Architektura Ceph](/CEPH-DG/Grafiki/storage_ceph-architecture.jpg)

##### Ogólna architektura klastra Ceph

![Stos ceph](/CEPH-DG/Grafiki/Ceph_stack.png)

### **Ceph Storage Gateway** - interfejs zbudowany na librados zapewniający aplikacjom RESTowego API umożliwiające dostęp do klastra storage opartego na Ceph.
### Ceph object storage wspiera dwa interfejsy (APIs):
#### 5.1. S3-compatible - kompatybilność z REStowym API Amazon Web Services (AWS).
#### 5.2. Swift-compatible - kompatybilność z OpenStack'owym Swift API.

![Ceph APIs](/CEPH-DG/Grafiki/1.PNG)

##5. Podstawowe informacje o instalacji.
### 5.1. CEPH można uruchomić na jednym hoście w celach testowych.
### 5.2. Klaster CEPH wymaga co najmniej jednego CEPH Monitor, co najmniej dwa OSDs Daemons.
### 5.3. CEPH Metadata Server (MDS) jest niezbędny do działania CephFS (Ceph Filesystem).
### 5.4. Ceph z założenia może działać na różnych klasach sprzętu (bez konieczności stosowania specjalistycznego sprzętu komputerowego lub storage'owego).

##6. Źródła:

#### 6.1. [Dokumnetacja projektu Ceph](http://docs.ceph.com/docs/jewel/)

#### 6.2. [Dokumentacja projektu OpenStack](https://docs.openstack.org/)

#### 6.3. [POSIX](http://searchenterpriselinux.techtarget.com/definition/POSIX)

#### 6.4. [RADOS](http://searchstorage.techtarget.com/definition/RADOS-Reliable-Autonomic-Distributed-Object-Store)

#### 6.5. [Ceph](http://searchstorage.techtarget.com/definition/Ceph)


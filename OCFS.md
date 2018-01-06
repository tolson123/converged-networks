## OCFS2
**to uniwersalny system plików klastra dysku współużytkowanego dla systemu Linux, który zapewnia zarówno wysoką wydajność, jak i wysoką dostępność. Ponieważ zapewnia semantykę lokalnego systemu plików, może być używany z prawie wszystkimi aplikacjami. Aplikacje wykorzystujące klastry mogą wykorzystywać równoległe operacje wejścia / wyjścia w pamięci podręcznej z wielu węzłów w celu łatwego skalowania aplikacji. Inne aplikacje mogą wykorzystywać możliwości systemu plików do uruchamiania aplikacji w przypadku awarii węzła.**

System plików jest obecnie używany w wirtualizacji (Oracle VM) zarówno w domenie zarządzania, do hostowania obrazów maszyn wirtualnych, jak iw domenie gościa, aby umożliwić gościom systemu Linux współdzielenie systemu plików. Jest również używany w klastrach baz danych (Oracle RAC), klastrach oprogramowania pośredniego (Oracle E-Business Suite), urządzeniach (SAP Business Intelligence Accelerator) itp.

**System plików jest obecnie używany w domenie wirtualnej (maszyna wirtualna systemu Linux). Jest również używany w klastrach baz danych (Oracle RAC), klastrach oprogramowania pośredniego (Oracle E-Business Suite), urządzeniach (SAP Business Intelligence Accelerator) itp.**
 
**Jako system plików klastrów, OCFS2 przenosi raczej więcej bagażu niż jedno-węzłowy system plików, taki jak ext3. 
Ma on, w swojej istocie, implementację systemu plików na dysku, który jest silnie zainspirowany przez ext3. 
Są jednak pewne różnice: jest to system plików oparty na zasięgu, co oznacza, że pliki są reprezentowane na dysku w dużych, ciągłych porcjach. Numery inode to 64 bity. OCFS2 używa jednak warstwy JBD Linux do kronikowania, więc nie musi wnosić ze sobą dużej części własnego kodu księgowania.**

**Aby faktycznie działać w trybie klastrowym, OCFS2 musi mieć informacje o klastrze, w którym działa. W tym celu zawiera on prostą warstwę informacji o węźle, która zawiera opis systemów tworzących klaster. Ta struktura danych jest zarządzana z przestrzeni użytkownika poprzez configfs; narzędzia przestrzeni użytkownika z kolei pobierają odpowiednie informacje z pojedynczego pliku konfiguracyjnego (/etc/ocfs2/cluster.conf). Nie wystarczy jednak wiedzieć, które węzły powinny być częścią klastra: te węzły mogą przychodzić i odchodzić, a system plików musi być w stanie reagować na te zdarzenia. Tak więc OCFS2 zawiera również prostą implementację pulsu do monitorowania, które węzły rzeczywiście są aktywne. Ten kod działa poprzez odłożenie specjalnego pliku; każdy węzeł musi co jakiś czas zapisywać blok do tego pliku (ze zaktualizowanym znacznikiem czasu). Jeśli określony blok przestaje się zmieniać, oznacza to, że powiązany z nim węzeł opuścił klaster.**

**Kolejnym ważnym elementem jest rozproszony menedżer blokad. OCFS2 zawiera menedżera blokad, który podobnie jak implementacja objęta w zeszłym tygodniu nazywa się "dlm" i implementuje interfejs podobny do VMS. Wdrożenie Oracle jest jednak prostsze (jego podstawowa funkcja blokowania ma tylko osiem parametrów ...) i brakuje w nim wielu zaawansowanych typów blokad i funkcji implementacji Red Hat. Istnieje również interfejs wirtualnego systemu plików ("dlmfs"), który udostępnia funkcje blokowania przestrzeni użytkownika.**

**Istnieje prosty, oparty na protokole TCP system przesyłania komunikatów, który jest używany przez OCFS2 do rozmowy między węzłami w klastrze.**

**Pozostały kod to sama implementacja systemu plików. Ma wszystkie komplikacje, których można oczekiwać od implementacji systemu plików o wysokiej wydajności. OCFS2 ma jednak działać z dyskiem, który sam jest współużytkowany w klastrze (być może za pośrednictwem jakiejś sieci obszaru pamięci lub schematu wielościeżkowego). Zatem każdy węzeł na klastrze manipuluje bezpośrednio systemem plików, ale musi to robić w sposób, który pozwala uniknąć chaosu. Kod menedżera blokady obsługuje wiele z tego - węzły muszą wyłapać blokady na strukturach danych na dysku przed rozpoczęciem pracy z nimi.**

**Jest jednak coś więcej. Istnieje na przykład oddzielny "obszar alokacji" zarezerwowany dla każdego węzła w klastrze; kiedy węzeł musi dodać zakres do pliku, może pobrać go z własnego obszaru alokacji i uniknąć rywalizacji z innymi węzłami dla globalnej blokady. Istnieją również pewne operacje (na przykład usuwanie i zmienianie nazw plików), których nie może wykonać sam węzeł. Nie wystarczy, aby jeden węzeł usunął plik i zawrócił jego bloki, jeśli plik pozostanie otwarty w innym węźle. Istnieje zatem mechanizm głosowania dla operacji tego typu; węzeł, który chce usunąć plik, najpierw prosi o głosowanie. Jeśli inny węzeł zawetuje operację, plik pozostanie na razie. Tak czy inaczej, wszystkie węzły w klastrze mogą zauważyć, że plik jest usuwany i odpowiednio dostosowywać lokalne struktury danych.**

rys.1 Postfix, replikacja w czasie rzeczywistym na serwerze pocztowym za pomocą podwójnego podstawowego DRBD z OCFS2
![alt text](https://www.kutukupret.com/wp-content/uploads/2011/06/Postfix-drbd-ocfs2.png)

# linki:

https://oss.oracle.com/projects/ocfs/dist/documentation/RHAS_best_practices.html

https://lwn.net/Articles/137278/

https://pl.wikipedia.org/wiki/OCFS2

https://oss.oracle.com/projects/ocfs/

# wykonanie: Kamil Błaś, Jakub Dobisiak

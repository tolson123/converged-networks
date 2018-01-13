## OCFS2
**To uniwersalny system plików klastra dysku współużytkowanego dla systemu Linux, który zapewnia zarówno wysoką wydajność, jak i wysoką dostępność. Ponieważ zapewnia semantykę lokalnego systemu plików, może być używany z prawie wszystkimi aplikacjami. Aplikacje wykorzystujące klastry mogą wykorzystywać równoległe operacje wejścia / wyjścia w pamięci podręcznej z wielu węzłów w celu łatwego skalowania aplikacji. Inne aplikacje mogą wykorzystywać możliwości systemu plików do uruchamiania aplikacji w przypadku awarii węzła.**

**System plików jest obecnie używany w wirtualizacji (Oracle VM) zarówno w domenie zarządzania, do hostowania obrazów maszyn wirtualnych, jak iw domenie gościa, aby umożliwić gościom systemu Linux współdzielenie systemu plików. Jest również używany w klastrach baz danych (Oracle RAC), klastrach oprogramowania pośredniego (Oracle E-Business Suite), urządzeniach (SAP Business Intelligence Accelerator) itp.**

**Jako system plików klastrów, OCFS2 przenosi więcej danych niż jedno-węzłowy system plików, taki jak ext3. 
Ma on, w swojej istocie, implementację systemu plików na dysku, który jest silnie zainspirowany przez ext3. 
Są jednak pewne różnice: jest to system plików oparty na zasięgu, co oznacza, że pliki są reprezentowane na dysku w dużych, ciągłych porcjach. Numery inode to 64 bity. OCFS2 używa jednak warstwy JBD Linux do kronikowania, więc nie musi wnosić ze sobą dużej części własnego kodu księgowania.**

**Aby faktycznie działać w trybie klastrowym, OCFS2 musi mieć informacje o klastrze, w którym działa. W tym celu zawiera on prostą warstwę informacji o węźle, która zawiera opis systemów tworzących klaster. Ta struktura danych jest zarządzana z przestrzeni użytkownika poprzez configfs; narzędzia przestrzeni użytkownika z kolei pobierają odpowiednie informacje z pojedynczego pliku konfiguracyjnego (/etc/ocfs2/cluster.conf). Nie wystarczy jednak wiedzieć, które węzły powinny być częścią klastra: te węzły mogą przychodzić i odchodzić, a system plików musi być w stanie reagować na te zdarzenia. Tak więc OCFS2 zawiera również prostą implementację pulsu do monitorowania, które węzły rzeczywiście są aktywne. Ten kod działa poprzez odłożenie specjalnego pliku; każdy węzeł musi co jakiś czas zapisywać blok do tego pliku (ze zaktualizowanym znacznikiem czasu). Jeśli określony blok przestaje się zmieniać, oznacza to, że powiązany z nim węzeł opuścił klaster.**

**Kolejnym ważnym elementem jest rozproszony menedżer blokad. OCFS2 zawiera menedżera blokad, który podobnie jak implementacja objęta w zeszłym tygodniu nazywa się "dlm" i implementuje interfejs podobny do VMS. Wdrożenie Oracle jest jednak prostsze (jego podstawowa funkcja blokowania ma tylko osiem parametrów ...) i brakuje w nim wielu zaawansowanych typów blokad i funkcji implementacji Red Hat. Istnieje również interfejs wirtualnego systemu plików ("dlmfs"), który udostępnia funkcje blokowania przestrzeni użytkownika.**

**Istnieje prosty, oparty na protokole TCP system przesyłania komunikatów, który jest używany przez OCFS2 do rozmowy między węzłami w klastrze.**

rys.1 Porównywanie przepustowości transakcji dla systemów zarządzania plikami klastrowymi OCFS2 i ASM
![alt text](https://www.ibm.com/support/knowledgecenter/linuxonibm/liaag/oracle_rac/l0wozl00_fig03.jpg)

# Wniosek

**Znacznie wyższy wskaźnik transakcji z ASM z 60 użytkownikami w mniej kontrowersyjnym scenariuszu pokazuje przewagę ASM w porównaniu z OCFS2. Przy 100 użytkownikach rywalizacja w klastrze jest czynnikiem dominującym, który ma większy wpływ niż różnice w podstawowym narzędziu używanym do zarządzania współużytkowaną pamięcią masową.**

rys.2 Porównanie obciążenia procesora dla systemów zarządzania plikami klastrowymi OCFS2 i ASM
![alt text](https://www.ibm.com/support/knowledgecenter/linuxonibm/liaag/oracle_rac/l0wozl00_fig04.jpg)

# Wniosek

**Porównując 60 użytkowników z 100 użytkownikami, obciążenie procesora było prawie stałe. OCFS2 wymaga większego wykorzystania procesora w wartościach bezwzględnych, około trzech procesorów w porównaniu do wartości mniejszej niż dwa procesory dla ASM (cztery procesory są dostępne).**


# linki:

https://oss.oracle.com/projects/ocfs/dist/documentation/RHAS_best_practices.html

https://lwn.net/Articles/137278/

https://pl.wikipedia.org/wiki/OCFS2

https://oss.oracle.com/projects/ocfs/

# wykonanie: Kamil Błaś, Jakub Dobisiak

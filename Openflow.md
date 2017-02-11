![alt text](http://archive.openflow.org/img/newlogo7.png "Logo Title Text 1") 
###1. Co to jest OpenFlow:
Def "Standardowy protokół komunikacyjny używany pomiędzy „control” i „data panels"
OpenFlow  jest protokołem komunikacyjnym umożliwiając zdalny dostęp do poszczegulnych płaszczyzn danych urządzenia sieciowego.
Głównym zamierzenim twórców protokołu było wsparcie budowy programowalnych sieci komputerowych dzięki standaryzacji oraz dopasowaniu 
do możliwości produkowanych urządzeń.

###2. Zarys działania
Wykorzystując technologię OpenFlow, otrzymujemy bogaty zestaw narzędzi pozwalający na zaawansowaną inżynierię ruchu. 
Możemy optymalizować transmisję pod kątem zapewnienia odpowiedniego pasma, unikania opóźnień czy liczby węzłów, 
przez które przechodzi pakiet. Dzięki temu jesteśmy w stanie oferować usługi spełniające wymagania QoS. 
W oparciu o OpenFlow jesteśmy w stanie tworzyć wirtualne sieci prywatne, a nawet coś więcej, bo sieci wielodzierżawne . 
Protokół ten wprowadza pojęcie przepływów ruchu, co pozwala na całkowitą wirtualizację sieci i separację ruchu. 
Daje to administratorom nowe możliwości rozbudowy, modyfikacji i testowania sieci komputerowych. 
Mogą oni badać nowe rozwiązania wykorzystując do tego środowisko produkcyjne, a jednocześnie nie zakłócają w ten sposób 
normalnego działania sieci.

###3. Mechanizm działania:
OpenFlow jest protokołem działającym w drugiej warstwie modelu ISO OSI. Do stworzenia sieci opartej na technologii OpenFlow 
niezbędne są trzy elementy: przełączniki współpracujące z tym protokołem, kontroler oraz kanał komunikacyjny, 
wykorzystujący protokół OpenFlow, za pomocą którego kontroler i przełącznik mogą się komunikować.
![alt text](https://gigadom.files.wordpress.com/2011/07/openflow1.jpg?w=300&h=225)

###4.Przełączniki w OpenFlow:
Przełącznik OpenFlow Jest to element infrastruktury sieciowej działający w warstwie drugiej modelu ISO OSI, 
który przechowuje w swojej pamięci tabelę przepływów oraz posiada kanał komunikacyjny, 
który może być używany do komunikacji za pomocą protokołu OpenFlow z kontrolerem. Możemy wyróżnić specjalistyczne, 
fizyczne urządzenia, czyli dedykowane przełączniki obsługujące tę technologię, jak i przełączniki programowe, 
czyli zazwyczaj zwykłe komputery, tyle że działające pod kontrolą odpowiednio przygotowanego systemu operacyjnego.

###5.Kontroler w OpenFlow:
Kontroler Za jego pomocą do tabel przepływów w przełącznikach dodawane są odpowiednie reguły. 
Funkcję kontrolera może pełnić jakiś bardzo wyrafinowany program, sterujący ruchem wedle określonych kryteriów bądź 
bardzo prosty mechanizm, który będzie dodawał statyczne wpisy do pamięci przełącznika. 

###6.Kanał komunikacyjny w OpenFlow:
Kanał komunikacyjny Jest to bardzo ważny element w sieciach opartych na technologii OpenFlow. 
Służy on do komunikacji przełączników z kontrolerami, co jest kluczowe, ponieważ tak naprawdę decyzje o zarządzaniu ruchem w 
sieci są podejmowane przez kontroler i muszą być rozpropagowane wśród przełączników. Postać danych przesyłanych takim kanałem 
musi być zgodna ze specyfikacją OpenFlow i zazwyczaj jest zaszyfrowana przy użyciu SSL. 

##Więcej informacji o Protokole można znaleść :

[OpenFlow Specification](http://archive.openflow.org/documents/openflow-spec-v1.1.0.pdf)

[OpenFlow version 1.2](https://www.opennetworking.org/images/stories/downloads/sdn-resources/onf-specifications/openflow/openflow-spec-v1.2.pdf)

[OpenFlow version 1.4](https://www.opennetworking.org/images/stories/downloads/sdn-resources/onf-specifications/openflow/openflow-spec-v1.4.0.pdf)

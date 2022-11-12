# **_SYMULATOR SELEKCJI NATURALNEJ_**

Projekt ten został napisany w języku C# na silniku Unity Engine. Jest utrzymany w konwencji gry - symulacji, z której można na koniec wyeksportować dane. Użytkownik na wejściu może ustawić dane, które realnie wpływają na przebieg symulacji. 

W repozytorium znajduje się plik Simulation.exe, który uruchomi aplikację bez potrzeby instalacji dodatkowych bibliotek.

Do stworzenia projektu zainspirował mnie [ten film o doborze naturalnym.](https://www.youtube.com/watch?v=0ZGbIKd0XrM)

## ŚWIAT

Program symuluje cykl życia populacji zwierząt w środowisku o zadanych parametrach. Zwierzęta są reprezentowane przez kolorowe kapsułki – ich kolor zależny jest od genów danego osobnika. W środowisku panuje cykl dzień – noc, w ciągu dnia zwierzęta szukają pożywienia (zielone sześciany), aby przetrwać noc muszą się schować do domu, czyli do jednej z różowych sfer.

W trakcie działania symulacji wyświetlane są aktualne dane: data, czas, ilość żywych zwierząt, średnie z ich genów i wieku. Przyciskami na dole ekranu można przyspieszać, pauzować i zwalniać symulację.

W programie pojawia się element Environment – jest to „świat”, który kontroluje wszystko co dzieje się na mapie. Jest odpowiedzialny za stworzenie pierwszej generacji zwierząt, postawienie im domów, odliczanie czasu i dokładanie oraz usuwanie pożywienia. Przekazuje też dane do obiektu Data Manager, który odpowiada za eksport danych i wyświetlanie ich na ekranie.

## ZWIERZĘTA ŻYJĄCE W SYMULACJI

**Genotyp**
Każde zwierzę posiada swój genotyp, na który składa się gen Vision Radius – zasięg wzroku, gen określa jak daleko zwierzę może wyczuć pożywienie. Od tego genu zależy między innymi sposób poruszania się zwierzęcia. Zwierzęta o słabym wzroku poruszają się krótkimi ruchami i często zmieniają kierunek ruchu. Drugim genem, który wchodzi w skład genotypu jest Speed, czyli gen odpowiedzialny za prędkość poruszania się zwierzęcia. Prędkość ta ma bezpośredni wpływ na to jak szybko zwierzę staje się głodne i ile zużywa energii. Im bardziej u danego zwierzęcia przeważa gen Speed tym bardziej jest żółte, a im bardziej przeważa gen Vision Radius tym bardziej jest niebieskie. Jeśli oba geny mają wysokie wartości to kolor zwierzęcia zbliża się do białego. Podstawowym kolorem zwierząt jest zielony.

**Parametry**
Oprócz genotypu każde zwierzę posiada parametry życiowe, czyli Staminę oraz Hunger (głód). Na te parametry ma wpływ sposób poruszania się zwierzęcia. Jeśli zwierzę zauważy w trakcie dnia, że jest zmęczone może wrócić na chwilę do domu i odpocząć – przybywa mu wtedy staminy.

**Rozmnażanie**
Zwierzęta rozmnażają się jeśli uda im się zdobyć odpowiednią ilość pożywienia. Im lepszy wzrok ma dane zwierzę tym więcej pożywienia potrzebuje do rozrodu. Rozmnażanie zachodzi tylko kiedy znajdują się w domu, tworzą wtedy swoją lekko zmutowaną kopię – przekazują swoje geny z losowymi, małymi zmianami. Istnieje 5% szansy na powstanie odmieńca, czyli zwierzęcia, które byłoby znacząco odmienne od swojego rodzica.

**Zachowanie**
Zwierzęta korzystają z wzorca projektowego maszyna stanów – dzięki temu mogą „decydować” co chcą robić. Każde zwierzę posiada stany:

 - **Hunt** – w tym stanie zwierzę porusza się po mapie i poszukuje
   pożywienia. Jeśli znajdzie jedzenie i do niego dotrze to przełącza się w stan Eat
 - **Eat** – w tym stanie zwierzę je, czyli aktualizuje swój głód i niszczy obiekt pożywienie. Po zjedzeniu wraca do stanu Hunt
 - **GoHome** – jeżeli jest późno lub zwierzę jest zmęczone to szuka schronienia
 - **Sleep** – jeżeli jest późno i zwierzę jest w domu to przełącza się w stan Sleep, dodaje mu się stamina
 - **Replicate** – jeżeli poprzedniego dnia zwierzę zdobyło wystarczającą ilość pożywienia to przed wyruszeniem na Hunt zwierzę przełącza się w stan Replicate i się rozmnaża. Następnie zawsze wraca do stanu Hunt
 
 ## PARAMETRY POCZĄTKOWE
 Po uruchomieniu aplikacji otwiera się menu do ustawienia parametrów symulacji:
 - **Animals population** – jak duża ma być populacja wejściowa
 - **Food per day** – jak dużo pożywienia ma dostać populacja każdego dnia, tę wartość można zmieniać również w trakcie działania symulacji
 - **Base vision gene** – bazowy gen wzroku, czyli wartość wokół której będą oscylowały geny pierwszej generacji i odmieńców
 - **Vision mutation range** – zakres w jakim będą oscylowały wartości genu wzroku pierwszej generacji oraz odmieńców
 - **Base speed gene** – bazowy gen prędkości, analogicznie jak w przypadku wzroku
 - **Speed mutation range** – zakres genów prędkości dla pierwszej generacji
 

## EKSPORT DANYCH
Po zakończeniu symulacji otwiera się menu końcowe.

Użytkownik może wyeksportować dane z symulacji – po przyciśnięciu przycisku EXPORT DATA zostanie utworzony plik simulationData.csv. Dane zapisywane są w wygodnym do obsługi formacie .csv dzięki czemu można od razu otworzyć plik i zobaczyć wyniki w Excelu.

## PODSUMOWANIE

Projekt spełnia swoje zadanie – po wykonaniu symulacji z różnymi parametrami widać, że zwierzęta ewoluują i dostosowują się do środowiska. Ponadto w trakcie symulacji można wytrenować populację. Jest to bardzo ciekawe zjawisko: jeśli ustalimy geny zwierzętom i damy zbyt mało jedzenia to populacja umrze. Natomiast jeśli zadamy te same geny i zaczniemy od wystarczającej ilości pożywienia, a następnie będziemy stopniowo zmniejszać ilość – to okaże się że udało się wytrenować populację i zwierzęta ewoluowały do korzystania z małej ilości pokarmu. Program jest stosunkowo łatwo rozwijać, istnieje możliwość dodania innych gatunków zwierząt np. drapieżników, które będą zjadały zwierzęta.

## WYGLĄD SYMULACJI

![1](https://user-images.githubusercontent.com/101990687/201497274-bd4dfeab-98cf-4d2a-99ac-cf6e6a06032f.png)
![2](https://user-images.githubusercontent.com/101990687/201497279-9d2afd6d-a2ea-4426-b6e0-0451f0898656.png)
![3](https://user-images.githubusercontent.com/101990687/201497277-79bcf06b-7a41-4979-87d7-c6504ed43d06.png)

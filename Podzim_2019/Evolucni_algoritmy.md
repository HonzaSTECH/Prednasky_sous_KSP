# Evoluční algoritmy
### *Jiří Setnička*
### *16.09.2019*

EVA = **EV**oluční **A**lgorytmy

Inspirováno přírodní evolucí

**Fitness** = hodnota udávající kvalitu jedince

Vytvoříme si původní populaci P1 tvořenou náhodně vygenerovanými jedinci

Další populaci vytvoříme tak, že proženeme P1 nějakým algoritmem, ve kterém bude mít každý jedinec nějakou šanci, že bude **zmutován**. Poté proběhne selekce rodičů a **křížení**. Výsledkem je pool pro populaci P2

Velikost nové populace potřebujme udržet přibližně stejnou jako velikost předchozí populace, aby nám nedošla paměť. Toho docílíme **selekcí** v poolu pro novou populaci. Odebereme nějakým způsobem potřebný počet jedinců s nejnižším fitness

**SGA** - něco jako genom jedince. Skládá se třeba z jedniček a nul
  - mutace SGA - překlopení jedné nebo více jedniček nebo nul
  - křížení SGA - Rozdělíme si sekvenci na dvě nebo více segmentů a v každém segmentu použijeme tu samou část SGA, ale z jednoho vybraného rodiče

**Selekce**
  - ruletová selekce - každý jedinec má takovou šanci, že bude vybrán pro další populaci, jaká je hodnota jeho fitness (např. v populaci pěti jedinců s fitness 2, 3, 6 a 9 mají jedinci v prvním točením šanci 10%, 15%, 30% a 45%)
  
  ![Ruletová selekce](images/Rullete_selection.svg)
  - stochastická ruleta
  - turnaj - vybere se X náhodných jedinců a pro další populaci jsou vybráni vítězové "zápasu" (porovnávání fitness hodnot)

Nastavení běžná pro evoluční programy
  - velikost populace
  - počet generací které se budou počítat
  - pravděpodobnost křížení rodičů (v opačném případě se pouze překopíruje SGA)
  - pravděpodobnost mutace
  - pravděpodobnost zmutování každého prvku SGA (pokud bude mutace probíhat)

#### Problém loupežníků

Jak rozdělit věci různých cen na X hromádek tak, aby byly hromádky stejně cenné

Exaktní řešení by běželo v exponenciálním čase *X^n*
  - Jedinec - pole číslic
  - Délka jedince = počet věcí k rozdělení
  - Věc = prvek v poli obsahuje
    - svou cenu
    - svou identifikaci (určena pozicí v poli)
  - Obsah jedince
    - 0 = dáme věc loupežníkovy s indexem 0
    - 1 = dáme věc loupežníkovy s indexem 1
    - n = dáme věc loupežníkovy s indexem n
  - Mutace
    - změníme u věci číslo loupežníka, kterému patří
    - prohodíme dvě věci v jednom jedinci
    
#### Problém obchodního cestujícího

Jak projet X měst tak, aby nás to stálo co nejméně peněz

Exaktní řešení by běželo v exponenciálním čase

  - Jedinec - náhodné pořadí měst
  - Délka jedince - počet měst
  - Mutace
    - swap - prohodíme dvě města v pořadníku jejich návštěv
    - vybereme segment cesty a otočíme jej
    - shift - posuneme segment cesty na jiné místo
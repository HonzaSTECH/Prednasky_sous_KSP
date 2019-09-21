# Počítačové sítě II
### *Jiří Setnička*
### *19.09.2019*

**TCP** = **T**ranslation **C**ontrol **P**rotocol

TCP stack = až po aplikační vrstvu

V hlavičce paketu posílaného přes TPC je obsaženo pořadové a potvrzovací číslo

Jako první klient posílá **SYN** paket, který se pokusí navázat spojení se serverem. Ten obsahuje náhodně vybrané počáteční sekvenční číslo (X)

Server si poté vymyslí své počáteční sekvenční číslo (Y) a pošle jej klientovy pomocí **SYN ACK** paketu - sekvenční číslo paketu = X + 1

Další pakety (**ACK**) posílá server se sekvenčním číslem X + n a klient se sekvenčním číslem Y + n

Server si musí pamatovat, jaká sekvenční čísla paketů již obdržel a která ještě ne

**DDos Attack** - pokus zahltit systém způsobem, který jej znemožní používat (SYN flood)

Útočník vytvoří spoustu SYN paketů se spoustou různých sekvenčních čísel a server se s nimi pokusí navázat spojení, důsledkem čehož mu dojde paměť, protože si potřebuje pamatovat ona sekvenční čísla

Jedna z možných obran je ukládání sekvenčních čísel až v okamžiku, kdy klient pošle první ACK paket

Další možnost je zahazovat náhodné existující spojení místo nově příchozího

**HTTP** = **H**yper**T**ext **T**ransfer **P**rotocol

Odesílá se při stahování webových stránek - HTTP požadavek a HTTP odpověď

Je bezstavový (neuchovává žádná data mezi dvěma HTTP požadavky)

Požadavek klienta obsahuje:
  - Hlavičku
    - Typ (GET / HEAD / POST / PUT / DELETE)
    - Verze HTTP (nejčastěji 1.1)
    - Host
    - Další informace o prohlížeči
    - Očekávaný typ odpovědi a její jazyky
    - Akceptované kódování
    - Cookies
    - Pár dalších věcí
  - Prázdný řádek (někdy)
  - Tělo (někdy)

Odpověď serveru obsahuje:
  - Hlavičku
    - Odpovědní kód (např 200 - OK nebo 404 - Not Found)
    - Typ odeslaného obsahu a jeho délka
    - Maximální doba, po kterou je možné použít přijatá data, pokud je uložíme do cache (v zájmu snížení datového přenosu)
    - Pokud máme data již uloženou v cache, jak stará mohou být, abychom je mohli použít
    - Poslední modifikace obdržovaných dat (určuje, zda je potřeba získat novou verzi)
    - Pár dalších věcí
  - Prázdný řádek (někdy)
  - Tělo (někdy)
    - Například webová stránka, obrázek, PDF soubor, zvukový soubor, ...
    
Typy HTTP požadavků:
  - GET = získávání dat
  - HEAD = získávání dat, ale pouze hlavičky
  - POST = požadavek na zpracování odeslaných dat
  - PUT = odeslání dat
  - DELETE = odstranění dat ze serveru

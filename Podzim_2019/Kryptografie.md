Kryptografie
============

### *Standa Lukeš*

### *18.09.2019*

Když chceme poslat zabezpečenou zprávu, zašifrujeme jí před odesláním
šifrovacím algoritmem za pomocí nějakého klíče / hesla. Příjemce musí
dostat ten samý klíč a pomocí dešifrovacího algoritmu jej dešifrovat.

Pokud někdo bude odposlouchávat komunikaci, bude moci přečíst pouze
zašifrované zprávy, které mu budou k ničemu.

Pokud známe původní zprávu a šifru, která z ní vznikne, můžeme z ní
vymlátit klíč - to se nesmí stát

Klíč musí být vždy náhodně vygenerován - nesmí výt vazby mezi
jednotlivými znaky

Klíč musí být pokaždé jiný - útočník může po čase odhalit klíč od první
zprávy z jiných zdrojů (bude znát cipher text a odněkud zjistí co jsme
posílali).

CS-PRNG = **C**rypthograpthy-**S**ave **P**seudo-**R**andom **N**umber
**G**enerator - Na vstupu dostane 256b klíč a vyhodí náhodná data

Vstup: klíč, plain text část 0 - n, náhodná funkce (veřejná)

Cipher text část i = náhodná funkce(klíč, i);

Dešifrování pomocí klíče a náhodné funkce

Aby byl klíč vždy náhodný, dává se před celý cipher text náhodně
vygenerovaná 196b "nonce" a v náhodné funkci je i nahrazeno hodnotou
nonce+i (i musí být nižší)

Pokud se dvakrát vygeneruje ta stejná nonce, máme problém

#### Obrana proti modifikaci cipher textu

MAC = **M**essage **A**uthentication **C**ode

MAC verifikace dostane klíč, zprávu a MAC a rozhodne, zda je neoprávněně
modifikovaná nebo ne.

K přelstění MACové verifikace by byl potřeba klíč.

MAC se generuje ze zprávy a klíče pomocí podpisu:
`hash(klíč, zpráva) --> MAC`

HMAC - ještě bezpečnější verze a také mnohem běžnější:
`hash(klíč_část1, hash(klíč_část2, zpráva) --> HMAC`

Hash (= podpis / heš) 
  - vzniká ze zprávy
  - má omezenou délku a to vždy stejnou
  - lehce odlišná zpráva má naprosto odlišný hash
  - nelze z něj zpět vytvořit zprávu
  - `nahodna_funkce(blok1,nahodna_funkce(blok2,nahodna_funkce(blok3,nahodna_funkce(blok4,...))));`
  - nakonec se přidává délka zprávy a zahešuje se společně se zbytkem, aby
se minimalizovala šance kolize (stejný heš pro různé zprávy) - Pokud
budeme hešovat celou zprávu (včetně nonce), není prakticky žádná šance,
že nám stejná zpráva vytvoří stejný heš

Hesla se před ukládáním do databáze hešují, aby nebyly hned vidět.

Uživatelé si často dávají jednoduchá hesla, nebo hesla která používají
ve více službách. Řešení - k heslům se přilepí náhodně vygenerovaný
**salt**, který výrazně sníží pravděpodobnost stejných nebo častých
hesel.

KDF - **K**ey **D**erivation **F**unction - funkce která z jednoho klíče
a ID vyrobí jiný klíč. Používá se pro komunikaci mezi různými částmi
jedné služby s jednou zprávou

#### Asymetrická Kryptografie

Nedokážeme si nasdílet klíč

Uživatel má dva klíče:
  - tajný - nikdy se nesdílí
  - veřejný - posílá se tam, odkud očekáváme zabezpečené informace - lze s ním zprávu
zašifrovat, ale ne odšifrovat

Certifikační autority - existuje jich kolem stovky a jejich veřejné
klíče máme v počítači

Vlastník serveru zajde za certifikační autoritou a nechá si podepsat
svůj veřejný klíč

Uživatel poté může ověřit obdržený veřejný klíč u certifikační autority

*Cryptography I* od *Dan*a *Boneh*a - dobrý kurz na internetu
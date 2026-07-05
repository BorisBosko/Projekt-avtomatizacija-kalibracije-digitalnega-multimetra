# Avtomatizirano umerjanje digitalnega multimetra

Avtor: Boris Jovanović
Ustanova: Fakulteta za elektrotehniko, Univerza v Ljubljani
Kontakt: bj3670@student.uni-lj.si

## Opis projekta
Ta projekt predstavlja programsko rešitev za avtomatizirano umerjanje digitalnega multimetra, razvito v grafičnem programskem okolju LabVIEW. Sistem je zasnovan z namenom zmanjšanja ročnih napak pri prepisovanju, skrajšanja časa izvajanja meritev ter zagotavljanja ponovljivega in preglednega laboratorijskega postopka. 

Glavna odlika posodobljene različice programa je uvedba ustrezne časovne zakasnitve za stabilizacijo signala pred zajemom meritev, kar bistveno izboljša zanesljivost rezultatov v primerjavi s starejšimi različicami.

## Podprte merilne funkcije
Program omogoča umerjanje naslednjih električnih veličin:
* Enosmerna napetost (DCV)
* Izmenična napetost (ACV)
* Enosmerni tok (DCI)
* Izmenični tok (ACI)
* Upornost (RES)
* Frekvenca (FREQ)

## Uporabljena oprema in komunikacija
Sistem za delovanje potrebuje naslednjo strojno in programsko opremo:
* **Merjeni instrument:** Digitalni multimeter HP 34401A
* **Referenčni vir:** Kalibrator Fluke 5560A
* **Komunikacijski vmesnik:** Računalnik z GPIB (IEEE-488) vmesnikom
* **Programsko okolje:** LabVIEW z nameščenimi gonilniki VISA

Komunikacija med računalnikom in instrumenti poteka preko standardnih ukazov VISA preko vodila GPIB.

## Programska zasnova
Program je strukturiran kot **stanjski avtomat**, ki temelji na glavni `while` zanki in `case` strukturi. Podpira naslednja ključna stanja delovanja:
1. `INICIALIZACIJA` – Vzpostavitev komunikacije z instrumenti.
2. `PRIPRAVI TOČKE` & `NASTAVITEV TOČKE` – Izbira in priprava merilnih točk.
3. `NASTAVI KALIBRATOR` – Pošiljanje ukazov referenčnemu viru.
4. `ČAKAJ NA UMIRITEV` – Uvedba ključne časovne zakasnitve za stacionarnost signala.
5. `MERITEV` – Zajem več zaporednih meritev iz multimetra.
6. `IZRAČUN` – Statistična obdelava podatkov (povprečje, standardna deviacija, odstopanje).
7. `ZAPIS V DATOTEKO` – Samodejno shranjevanje rezultatov.
8. `NAPAKA` – Centralizirana varnostna obravnava napak preko VISA linije.
9. `SHRANI GRAFE` – Izvoz vizualnih grafov na disk.

## Zapis in organizacija rezultatov
Rezultati se samodejno shranjujejo v tekstovno datoteko (`.txt`) v strukturirani obliki, ki vsebuje:
`Datum | Čas | Funkcija | Frekvenca | Referenca | Povprečje | Razlika | StdDev`

Uporabniški vmesnik prav tako omogoča sproten grafični prikaz izmerjenih povprečij, razlik (odstopanj) in standardne deviacije (raztrosa) za takojšnjo oceno stabilnosti merilnega postopka.

## Možne nadgradnje v prihodnosti
* Avtomatsko preverjanje skladnosti s tehničnimi specifikacijami instrumenta.
* Podrobnejša analiza in izračun celotne merilne negotovosti.
* Izboljšano avtomatsko generiranje končnih merilnih poročil.

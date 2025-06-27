# Implementacija aplikacije za komunikaciju putem openPOWERLINK protokola na Raspberry Pi platformi

## Opis projekta

Cilj ovog projekta je realizacija jednostavnog sistema zasnovanog na **openPOWERLINK** protokolu, korišćenjem tri **Raspberry Pi** uređaja, povezanih putem **Ethernet HUB-a**. Projekat implementira osnovnu komunikaciju između čvorova koristeći jednobitni digitalni ulaz i izlaz.

## Struktura sistema

- **MN (Managing Node)** – jedan Raspberry Pi uređaj u ulozi mastera.
- **CN1 (Controlled Node 1)** – jedan Raspberry Pi uređaj sa digitalnim ulazom (dugme).
- **CN2 (Controlled Node 2)** – jedan Raspberry Pi uređaj sa digitalnim izlazom (LED dioda).

Uređaji su međusobno povezani preko **Ethernet HUB-a** kako je i navedeno.

## Funkcionalnost sistema

Kada korisnik pritisne dugme povezano na CN1, LED dioda na CN2 se uključuje. LED ostaje uključena sve dok je dugme fizički pritisnuto, čime se realizuje direktan prenos stanja jednog bita kroz POWERLINK mrežu.

## Softverska implementacija

- Korišćen je openPOWERLINK kod na osnovu primjera `demo_mn_console` i `demo_cn_console`, a koji su preuzeti sa [https://github.com/OpenAutomationTechnologies/openPOWERLINK_V2.git](https://github.com/OpenAutomationTechnologies/openPOWERLINK_V2.git)
- Komunikacija se obavlja putem PDO (Process Data Object) strukture, sa po jednim ulaznim/izlaznim bitom.
- CN uređaji komuniciraju sa GPIO pinovima:
  - CN1: čita stanje dugmeta i prenosi ga kao ulazni bit.
  - CN2: prima izlazni bit i upravlja LED diodom.
- Sav kod i konfiguracija su rađeni u **konzolnom režimu**, bez grafičkog interfejsa.

## Kompajliranje

- openPOWERLINK je **kros-kompajliran** za ARM arhitekturu (Raspberry Pi).
- Konfiguracija XML fajlova omogućava MN-u da upravlja CN čvorovima i mapira ulazno/izlazne PDO podatke.

## Testiranje sistema

Testiranje se vrši tako što se CN1 poveže sa fizičkim tasterom, a CN2 sa LED diodom. Nakon pokretanja svih čvorova i uspostavljanja komunikacije preko MN, potrebno je detektovati prenos stanja:

- Pritiskom na dugme LED treba da se uključuje.
- Oslobađanjem dugmeta LED treba da se isključuje.

Mjerenjem vremena odziva može se provjeriti da li komunikacija između čvorova zadovoljava parametre real-time prenosa.

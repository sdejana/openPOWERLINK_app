# openCONFIGURATOR

openCONFIGURATOR je open-source alat za konfiguraciju POWERLINK mreža, koji omogućava jednostavno kreiranje i upravljanje mrežnom konfiguracijom za industrijske komunikacione sisteme zasnovane na openPOWERLINK protokolu. 
Ovaj alat se može instalirati kao standalone aplikacija i kao plugin za Eclipse IDE okruženje. 

#### Koristi se za:

- Definisanje i konfiguraciju Managing Node (MN) i Controlled Node (CN) uređaja u mreži,
- Postavljanje Object Dictionary (OD) parametara za svaki čvor,
- Mapiranje procesa podataka (Process Data Mapping) – tj. dodjeljivanje ulazno/izlaznih signala za real-time komunikaciju,
- Generisanje konfiguracionih fajlova (npr. .xdc, .xap, .xml i drugih) koji se kasnije koriste u MN/CN aplikacijama.

openCONFIGURATOR podržava standardizovani POWERLINK XML format, koji omogućava interoperabilnost između različitih proizvođača i uređaja.

#### Ključne karakteristike:

- Grafički korisnički interfejs (GUI) za jednostavnu upotrebu, dostupan kroz Eclipse IDE kao dodatak (plugin),

- Automatizovano generisanje svih neophodnih konfiguracionih fajlova za rad openPOWERLINK mreže,

- Podrška za validaciju konfiguracije prema POWERLINK specifikaciji (EPSG – Ethernet POWERLINK Standardization Group),

- Podrška za više verzija POWERLINK standarda (v1.1, v2.0, itd).

#### Uloga u POWERLINK sistemu:

U jednoj tipičnoj POWERLINK mreži, openCONFIGURATOR se koristi pre pokretanja aplikacija. Nakon što se pomoću alata definiše topologija mreže i svi parametri, generisani fajlovi se prenose:

- Na Managing Node (MN) – koji koristi konfiguraciju da upravlja mrežom,

- Na svaki Controlled Node (CN) – koji koristi sopstveni deo konfiguracije da zna koje podatke razmenjuje.

Ovi fajlovi omogućavaju pravilno funkcionisanje mreže, uključujući pravilno vrijeme ciklične komunikacije, kao i razmjenu ulazno/izlaznih podataka.

#### Instalacija:

Kao što je navedeno, openCONFIGURATOR se može instalirati kao standalone i Eclipse IDE dodatak. 
U ovom projektu smo koristili dodatak za Eclipse IDE, za Windows i Linux operativni sistem

- Instalacija na Windows OS
- Instalacija na Linux OS

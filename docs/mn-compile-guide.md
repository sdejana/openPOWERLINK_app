# Uputstvo za kompajliranje MN aplikacije

> [!NOTE] 
> Pretpostavićemo da je kloniran repozitorijum sa izvornim kodom i konfiguracijama, te da su instalirane i/ili kompajlirane potrebne zavisnosti.
> Za detaljno uputstvo posjetite [repozitorijum](https://github.com/knezicm/ikm-labs/tree/master/lab9#ethernet-powerlink-protokol).

MN aplikacija može da se kompajlira za Linux x86_64 sistem, kao i za ARM arhitekturu.

#### Kompajliranje aplikacije sa funkcionalnostima Managing čvora za x86_64 arhitekturu

Aplikacija Managing Node može da se kompajlira tako da je koristimo sa host računara. Proces se svodi na nekoliko komandi:

> [!Note]
> Prvo je potrebno u direktorijumu stack u originalnom repozitorijumu da se izgradi openPOWERLINK stack za x86_64, te instalira biblioteka (`liboplkmn.a`) u stack/lib/linux/x86_64/
```bash
cd openPOWERLINK_V2/stack/build
mkdir -p linux/x86_64
cd linux/x86_64
cmake ../.. -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=../../../lib/linux/x86_64
make
make install
```
Nakon ovoga, potrebno je prvo instalirati dodatno biblioteku `systemd`, ukoliko ne postoji `sudo apt install libsystemd-dev`, te pokrenuti kompajliranje tako da se dobije izvršni fajl `demo_mn_console` koji se može pokrenuti na x86_64 Linux platformi.
```bash
cd openPOWERLINK_app/code/MN240/build/linux/x86_64
cmake ../.. -DCMAKE_BUILD_TYPE=Debug
make
```
Nakon ovog koraka, dobija se izvršni fajl koji se pokreće komandom `sudo ./demo_mn_console`, koja se može koristiti za testiranje.
> [!Note]
> Bez dodatnog podešavanja .xdd fajlova, ovaj pristup nije dobar, jer host računar ne radi u realnom vremenu i ne može da ispuni zahtjeve mreže koji se odnose na pravovremeno dostavljanje paketa, te zato mreža ne može da fukncioniše ispravno.

#### Kros-kompajliranje aplikacije sa funkcionalnostima Managing čvora za ARM arhitekturu

U folderu `code` nalazi se `CMakeLists.txt`, datoteka potrebne za kros-kompajliranje aplikacija. Takođe, potrebno je preuzeti ili napisati toolchain za ciljnu platformu. 

> [!NOTE]
> Potrebno je da se i u ovom slučaju da se izgradi openPOWERLINK stack, ali za ARM arhitekturu, kros-kompajliran
```bash
cd openPOWERLINK_V2/stack/build/linux
cmake ../.. -DCMAKE_TOOLCHAIN_FILE=../../../cmake/toolchain-rpi.cmake -DCMAKE_BUILD_TYPE=Release
make
make install
```
Nakon steka, potrebno je kompajlirati aplikaciju

```bash
cd 
cd openPOWERLINK_app/code/MN240/build/linux/
cmake ../.. -DCMAKE_TOOLCHAIN_FILE=../../cmake/toolchain-rpi.cmake
make
```
Nakon dobijanja izvršnog fajla, isti je potrebno prebaciti/prekopirati na ciljnu platformu. 
Za Raspberry Pi to je moguće učini npr. pomoću `scp` komande:
```bash
scp hostname@ip-adresa:/specifikovati/putanju
```
Sada je moguće pokrenuti izvršavanje aplikacije na sljedeći način
```bash
sudo ./demo_mn_console
```
Kada se aplikacija pokrene, pitaće korisnika na koji ethernet interfejs želi da spoji svoju openPOWERLINK mrežu. Koristik mora da interaktivno odabere interfejs na svom računaru pomoću rednog broja interfejsa u listi koja se ispiše na konzoli.

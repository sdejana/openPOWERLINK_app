> [!NOTE] 
> Pretpostavićemo da je kloniran repozitorijum sa izvornim kodom i konfiguracijama, te da su instalirane i/ili kompajlirane potrebne zavisnosti.
> Za detaljno uputstvo posjetite [repozitorijum](https://github.com/knezicm/ikm-labs/tree/master/lab9#ethernet-powerlink-protokol).

#### Kros-kompajliranje aplikacije sa funkcionalnostima Controlled čvora za ARM arhitekturu

Prije nego se sama aplikacija kros-kompajlira, potrebno je instalirati `wiringPi` biblioteku, pomoću koje se, u ovom slučaju, manipuliše dugmetom (GPIO ulazom) i  LED (GPIO izlazom).

To je moguće učiniti na sljedeći način:

1. Prvo je potrebno klonirati repozitorijum gdje se biblioteka nalazi.
```bash
git clone https://github.com/WiringPi/WiringPi.git
```
2. Potom je potrebno prebaciti se na granu `tags/2.61-1`.
```bash
git checkout tags/2.61-1
```
Ovo je verzija koja je korištena u ovom projektnom zadatku, ali i u srodnim, embedded projektima.
3. Sada možemo kompajlirati biblioteku za ciljnu arhitekturu
```bash
cd WiringPi/wiringPi
make CC=arm-linux-gnueabihf-gcc # Ovim govorimo o kojoj arhitekturi je riječ zapravo
```
i prebaciti/kopirati novonastalu dijeljenu biblioteku (`*.so`) u bibliotečki folder projekta ili ciljne platforme (najčešće `/usr/lib`).

Nakon kros-kompajliranja `wiringPi` biblioteke moguće je kros-kompajlirati i CN aplikacije. 

U folderu `code` nalazi se `CMakeLists.txt`, datoteka potrebne za kros-kompajliranje aplikacija. Takođe, potrebno je preuzeti ili napisati toolchain za ciljnu platformu. 
> [!Note]:
> Putanje koje se koriste pri kros-kompajliranju zavise od kloniranja repozitorijuma i strukture direktorijuma.

```bash
cmake /putanja/do/CMakeLists.txt -DCMAKE_TOOLCHAIN_FILE=/putanja/do/toolchain/datoteke/toolchain-rpi.cmake
```
```bash
make
```
```bash
make install
```
Nakon dobijanja izvršnog fajla, isti je potrebno prebaciti/prekopirati na ciljnu platformu. 
Za Raspberry Pi to je moguće učini npr. pomoću `scp` komande:
```bash
scp hostname@ip-adresa:/specifikovati/putanju
```
Sada je moguće pokrenuti izvršavanje aplikacije na sljedeći način
```bash
sudo ./demo_cn_console -n 1 -d eth0
```
gdje je `n` broj čvora.

Postupak kros-kompajliranja je analogan za oba CN, ali je potrebno uskladiti broj čvorova tako da čvor 1 odgovara čvoru koji čita stanje dugmeta, a čvor 110 odgovara čvoru koji upravlja stanjem LE diode.
# openCONFIGURATOR Plugin za LinuxOS

## Izgradnja (build) openCONFIGURATOR plugina

### Preduslovi

- JDK verzije **1.8.0_452**
- Apache Maven verzije **3.8.7**

---

### Instalacija Mavena i Java-JDK pomoću terminala

Prvi korak u instaliranju dodatka je ispunjavanje preduslova, to jeste instalacija Mavena i JDK pomoću terminala:

```bash
sudo apt update
sudo apt-get install maven
sudo apt install openjdk-8-jdk
   ```
---

### Instalacija Eclipse IDE i potrebnih biblioteka

Nakon uspješno instaliranih paketa, potrebno je instalirati Eclipse okruženje.
U ovom projektu korišten je Eclipse Neon 3, a postupak instalacije je sljedeći:

```bash
wget https://archive.eclipse.org/eclipse/downloads/drops4/R-4.6.3-201703010400/eclipse-SDK-4.6.3-linux-gtk-x86_64.tar.gz
tar -xvzf eclipse-SDK-4.6.3-linux-gtk-x86_64.tar.gz
```
Na ovaj način se dobija direktorijum koji sadrži izvršni fajl Eclipse aplikacije.

---

Uz prethodne korake, potrebno je instalirati i Boost biblioteku, koja je neophodna za rad openCONFIGURATOR-a. 
Za ispravan rad je potrebno instalirati verziju 1.58, jer je to stabilna verzija biblioteke sa kojom konfigurator radi. 
Pošto ta verzija biblioteke ne može da se instalira pomoću sudo apt install, potrebno je instalirati biblioteku preko arhive na sljedeći način:

```bash
wget https://sourceforge.net/projects/boost/files/boost/1.58.0/boost_1_58_0.tar.bz2/download -O boost_1_58_0.tar.bz2
tar -xvjf boost_1_58_0.tar.bz2
cd boost_1_58_0
./bootstrap.sh --prefix=/opt/boost_1_58_0
./b2 install
```
Uspješnost instalacije i generisanja dijeljenih biblioteka potvrđuje se pomoću komande:
```bash
ls /opt/boost_1_58_0/lib/libboost_*.so
```

Kada verifikujemo da je sve uspješno instalirano, potrebno je dodati putanju do djeljene biblioteke. Najlakši način za to je da se na kraj .bashrc fajla doda sljedeći niz komandi
```bash 
export LD_LIBRARY_PATH=/opt/boost_1_58_0/lib:$LD_LIBRARY_PATH
export BOOST_ROOT=/opt/boost_1_58_0
```
---

## Koraci za buildovanje plugina

Nakon uspješno odrađenih prethodnih koraka, može se pristupiti instalaciji openCONFIGURATOR plugin-a.
Prvo je potrebno skinuti arhivu sa interneta, te je raspakovati
```bash
wget https://sourceforge.net/projects/openconf/files/openCONFIGURATOR%20eclipse%20plugin/2.2.0/org.epsg.openconfigurator.updatesite-2.2.0.zip -O openconfigurator-2.2.0.zip
mkdir ~/openconfigurator
unzip openconfigurator-2.2.0.zip -d ~/openconfigurator-update
```
Sljedeći korak je instalacija dodatka u Eclipse okruženju. 
Potrebno je otvoriti Eclipse aplikaciju, te u opcijama pratiti sljedeću sekvencu naredbi Help → Install New Software... → Add...
U ovom prozoru potrebno je unijeti sljedeće podatke:




> Name: openCONFIGURATOR<br>
> Location: odabrati opciju Local..., te je potrebno odabrati ~/openconfigurator <br>

Kada se pojavi lista, označiti openCONFIGURATOR Eclipse Plugin, te Next → Finish.

Nakon ovog je dodatak uspješno instaliran i potrebno je ponovo pokrenuti Eclipse.

> [!IMPORTANT]
> Zbog velikog broja GUI elemenata pri pokretanju openCONFIGURATOR-a, moguće je da SWT (grafički alat Eclipse-a) ostane bez raspoloživih X11/GTK resursa, tj. nema više hendlera za kreiranje novih. <br>
> Da bi radio pravilno u Eclipse okruženju, potrebno je pokrenuti LinuxOS kao `"Ubuntu on Xorg"` ili `"GNOME on Xorg"`, te Eclipse pokretati pomoću komande `GDK_BACKEND=x11 ./eclipse`
---

Nakon svih koraka, pri pravljenju novog projekta u Eclipse, moguće je izabrati opciju Industrial Automation → New POWERLINK Network ili otvoriti postojeći POWERLINK projekat.

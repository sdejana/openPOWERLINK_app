#### Podešavanje i pokretanje openConfiguratora kroz Eclipse C&C++ 2020 okruženje za Windows OS

Potrebno je preuzeti Eclipse C&C++ 2020 verziju zbog kompatibilnosti sa openConfigurator plug-in - om, a što se može učiniti klikom na [link](https://www.eclipse.org/downloads/packages/release/2020-03/r). Takođe, potrebno je voditi računa o korištenom operativnom sistemu i u skladu sa tim izabrati verziju za preuzimanje (Windows verzija). 

Nakon preuzimanja, potrebno je raspakovati .zip datoteku u željeni direktorijum. Pošto Eclipse C&C++ 2020 koristi Java 8 verziju, nije potrebno ručno podešavati verziju Java JDK koji će se koristiti. 

Eclipse se pokreće dvoklikom na `eclipse.exe` datoteku koja se nalazi u raspakovanom direktorijumu. Nakon pokretanja aplikacije, otvara se prozor koji od korisnika zahtijeva da izabere radni direktorijum gdje će se čuvati projekti, postavke projekata i lokalne konfiguracije. 

Nakon odabira radnog direktorijuma, otvara se početna strana samog programa. Sada je potrebno dodati plug-in za openPOWERLINK tipove projekta. 

Plug-in za openPOWERLINK u Eclipse okruženju se može preuzeti na [linku](https://sourceforge.net/projects/openconf/), klikom na `Download` dugme. Preuzimanjem se dobija .zip datoteka, koju je takođe potrebno raspakovati u željeni direktorijum.

Plug-in se dodaje sljedećim koracima:
- `Help` >> `Install New Software` >> `Add` >> `Local`, te potom navigirati do lokacije direktorijuma u kojem je plug-in prethodno raspakovan i kliknuti dugme `Add`. Ukoliko je ispoštovana procedura, u sljedećem koraku prikazaće se naziv samog plug-in-a, odnosno `Industrial Automation`, koji je potrebno čekirati, te će klikom na `Finish` dugme plug-in biti uspješno dodan.
Nakon dodavanja plug-in - a, trebalo bi biti moguće kreirati novu POWERLINK mrežu ili analizirati postojeću. 

Moguće je odabrati postojeću POWERLINK mrežu, te je uvesti kao projekat, a potom analizirati čvorove u mreži i konfiguraciju. To se radi na način da se u kartici `File` izabere opcija `Import Projects from File System or Archive`, a potom navigira do direktorijuma gdje je projekat, tj. struktura mreže smještena. 

![eclipse-project-view](/imgs/eclipse-project-view.png)
_Izgled programskog prozora za projekat Demo_3CN_

U dostupnoj implementaciji jedne mreže sa tri čvora - dva CN i jednog MN koristi se osmobitni prenos podataka. Neke od osnovnih osobina su: 
- **Veličina procesne slike:**
  - Ulaz: `1 byte` po CN čvoru
  - Izlaz: `1 byte` po CN čvoru
- **PDO mapiranje (Object Dictionary)**

| Objekat (indeks)        | Podobjekat (podindeks) | Opis                      | Tip    |
|----------------|-----------|---------------------------|--------|
| `0x6000`       | `0x01`    | Digitalni ulaz   | `UINT8` |
| `0x6200`       | `0x01`    | Digitalni izlaz | `UINT8` |

Informacije o mreži dostupne su u karticama `Properties`, kao i u `PDO Mapping`, `SDO Mapping`. Tu je moguće vidjeti osobine mreže koje su gore navedene, ali i mnoge druge. Moguće je mijenjati vrijeme ciklusa, mapirati objekte i vidjeti .xdd fajlove za svaki od čvorova.

Da bi eventualne izmjene bile zapisane, potrebno je uraditi `Build` projekta, ručno ili automatski. Ručno bildanje projekta se obavlja klikom na ikonicu ,,čekića" u lijevom gornjem uglu, a automatsko bildanje se može uključiti zako što se klikne na karticu `Project`, a potom uključi opcija `Build Automatically`. 

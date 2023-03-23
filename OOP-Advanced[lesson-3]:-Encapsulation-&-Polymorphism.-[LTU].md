## Įkapsuliavimas

Įkapsuliavimas yra esminis į objektus orientuoto programavimo aspektas. Paaiškinkime inkapsuliavimą paprastais žodžiais: **informacijos slėpimas**. Tai reiškia vidinės sąsajos atribojimą ir atribojimą nuo išorinio pasaulio.
Pythone tai galima pasiekti naudojant prieigos modifikatorius, kuriais kontroliuojamas klasės atributų ir metodų matomumas.

Pavyzdžiui, panagrinėkime paprastą klasę, kuri vaizduoja asmenį, turintį vardą ir amžių:

```python
class Person:
    def __init__(self, name: str, age: int) -> None:
        self._name = name
        self._age = age
    
    def get_name(self) -> str:
        return self._name
    
    def set_name(self, name: str) -> None:
        self._name = name
    
    def get_age(self) -> int:
        return self._age
    
    def set_age(self, age: int) -> None:
        self._age = age

```
Šiame pavyzdyje `Person` klasė turi du privačius atributus `_name` ir `_age` ir keturis viešus metodus `get_name()`, `set_name()`, `get_age()` ir `set_age()`. Prieš atributų pavadinimus esantis pabraukimas rodo, kad jie yra **privatūs**, t. y. jie neturėtų būti tiesiogiai pasiekiami iš klasės išorės. Vietoj to pateikiame viešuosius metodus, skirtus šių atributų reikšmėms pasiekti ir keisti.

Štai pavyzdys, kaip galime naudoti šią klasę:

```python
person = Person("Alice", 25)
print(person.get_name())  # Output: Alice
person.set_name("Bob")
print(person.get_name())  # Output: Bob
print(person.get_age())   # Output: 25
person.set_age(30)
print(person.get_age())   # Output: 30

```

Naudodamiesi viešaisiais metodais, kuriuos pateikia `Person` klasė, galime **kontroliuojamai ir nuspėjamai sąveikauti su objektu, nežinodami klasės įgyvendinimo detalių**. Dėl to mūsų kodas tampa labiau modulinis ir lengviau prižiūrimas.

Informacijos paslėpimo privalumai - sistemos sudėtingumo mažinimas ir patikimumo didinimas. Kodėl? Nes inkapsuliavimas apriboja skirtingų programinės įrangos komponentų tarpusavio priklausomybę.

## Polimorfizmas
`Polimorfizmas` - tai principas, pagal kurį viena daikto rūšis gali būti įvairių formų. Programavimo kontekste tai reiškia, kad viena programavimo kalbos esybė, priklausomai nuo konteksto, gali elgtis įvairiais būdais. Tai panašu į tai, kad toks žodis kaip `išreikšti` viename sakinyje gali būti veiksmažodis, kitame - daiktavardis, o trečiame - būdvardis. Raidžių seka puslapyje nesikeičia, tačiau prasmė, kurią jos suteikia sakiniui, kiekvienu atveju iš esmės skiriasi. Panašiai ir polimorfinėse programavimo kalbose viena esybė skirtinguose kontekstuose gali veikti skirtingai.


### Operatoriaus polimorfizmas
Operatorių polimorfizmas, arba operatorių perkrovimas, reiškia, kad vienas simbolis gali būti naudojamas kelioms operacijoms atlikti. Vienas iš paprasčiausių pavyzdžių yra sudėties operatorius `+`. Pythono sudėties operatorius skirtingai veikia skirtingų `duomenų tipų` atžvilgiu. Pavyzdžiui, jei `+` veikia su dviem sveikaisiais skaičiais, rezultatas yra adityvus, grąžinama dviejų sveikųjų skaičių suma: 

```python
int_one = 10
int_two = 15
print(int_one + int_two)
# returns 25
```
Pirmiau pateiktame pavyzdyje operatorius `+` sudeda `10` ir `15`, todėl išvesties rezultatas yra `25`.

Tačiau jei pridėjimo operatorius naudojamas dviem eilutėms, **jis sujungia** eilutes. Štai pavyzdys, kaip + operatorius veikia eilutės duomenų tipus: 

```python
str_one = "10"
str_two = "15"
print(str_one + str_two)
# returns '1015'
```
Šiuo atveju išvesties rezultatas yra `1015`, nes operatorius `+` sujungia eilutes `10` ir `15`. Tai vienas iš pavyzdžių, kaip vienas operatorius gali atlikti skirtingas operacijas **skirtinguose kontekstuose**.

### Funkcijų polimorfizmas

Kai kurios Python funkcijos taip pat yra polimorfinės, t. y. jos gali veikti kelis duomenų tipus ir struktūras, kad gautų skirtingą informaciją.

Pavyzdžiui, "Python" integruota funkcija `len()` gali būti naudojama objekto ilgiui grąžinti. Tačiau priklausomai nuo objekto duomenų tipo ir struktūros ji skirtingai išmatuos objekto ilgį. Pavyzdžiui, jei objektas yra eilutė, funkcija `len()` grąžins eilutės simbolių skaičių. Jei objektas yra sąrašas, ji grąžins sąrašo įrašų skaičių.

Štai pavyzdys, kaip `len()` funkcija veikia eilutes ir sąrašus:

```python
str_one = "animal"
print(len(str_one))
# returns 6
list_one = ["giraffe","lion","bear","dog"]
print(len(list_one))
# returns 4
```
Rezultatai yra atitinkamai `6` ir `4`, nes funkcija `len()` skaičiuoja simbolių skaičių eilutėje ir įrašų skaičių sąraše. Funkcija veikia skirtingai, priklausomai nuo duomenų, su kuriais ji veikia, pobūdžio.

### Klasių ir metodų polimorfizmas, metodų perėmimas.

Python polimorfiškumas palengvina klasių ir metodų pertvarkymą. Atminkite, kad klasė yra tarsi projektas, o objektas yra konkretus šio projekto įkūnijimas. Taigi, metodas, kuris yra klasės dalis, pasikartos objektuose, kurie instancuoja tą klasę. Panašiai, jei sukursite naują klasę iš jau egzistuojančios klasės, naujoji klasė paveldės jau egzistuojančios klasės metodus. Šiuo atveju nauja klasė vadinama "dukterine klase", o jau egzistuojanti klasė - "tėvine klase".

Pythone galima, kad "antrinė klasė" **pakeistų** savo viršklasės atributus ir metodus. Tai reiškia, kad poklasis gali apibrėžti savo atributo ar metodo, kuris jau egzistuoja viršklasėje, įgyvendinimą.

Pateikiame pavyzdį, kaip naudoti metodų perėmimą:

```python

class Vehicle:
    def __init__(self, make: str, model: str) -> None:
        self.make = make
        self.model = model

    def start(self) -> None:
        print(f"Starting {self.make} {self.model}")

class Car(Vehicle):
    def __init__(self, make: str, model: str, year: int) -> None:
        super().__init__(make, model)
        self.year = year

    def start(self) -> None:
        print(f"Inserting key in {self.year} {self.make} {self.model}")
        super().start()

car = Car("Honda", "Accord", 2020)
car.start()  # prints "Inserting key in 2020 Honda Accord", "Starting Honda Accord"

```
Šiame pavyzdyje `Car` klasė paveldi iš "Vehicle` klasės ir **perima** `start` metodą. Kai sukuriame `Car` egzempliorių ir iškviečiame `start` metodą, jis naudoja `start` metodo, apibrėžto `Car` klasėje, realizaciją, kuri spausdina pranešimą apie raktelio įkišimą į automobilį. Tada jis iškviečia `Vehicle` klasės `start` metodą, naudodamas `super().start()` sintaksę, kuri spausdina pranešimą apie automobilio užvedimą.

## Pratimai: 
🧠 : Pakartokite [OOP 2 dalis](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* Užduotis Nr.1:  

   Nasa turi apskaičiuoti naujos misijos išlaidas: naudodamiesi OOP principais įgyvendinkite bazės ir kosminio laivo klases.
   Sukurkite paprastą skaičiuoklę su: 
   - Bazinė klasė turėtų suteikti galimybę sužinoti informaciją apie erdvėlaivius (amžių, kainą, pagaminimo metus, svorį ir t. t. ).
   - Naudodami pagrindinę klasę turėtumėte galėti apskaičiuoti misijos sąnaudas, kurias sudaro: degalų sąnaudos (FUEL_COST x BURN_RATE (kg/mylia) * 
     BURN_RATE_VARIABLE (2500 / orbitos aukštis (myliomis))) , vidutinės personalo išlaidos ( ppl x bazinis_darbo užmokestis ).
   - Paruoškite galutinę ataskaitą failo dokumente ir ekrane naudodami metodą `get_full_report` su visais surinktais ir apskaičiuotais duomenimis. 

* Kavinės projektas:
  Sukurkite `gyvą` meniu ir mokėjimo sistemą (taip pat vadinamą konsoline programa):
  - Pirmiausia programa turėtų paklausti, ar staliukas rezervuotas/ne (nurodant savo vardą ir pavardę). Ir tada, jei ne, paskirtų jums staliuką (yra tam tikras 
    skaičius vienviečių, dviviečių ar šeimyninių staliukų). Po to, kai stalas bus jums priskirtas, sistema turėtų parodyti, kiek yra laisvų stalų ir kiek jų yra. 
    rezervuota ir (arba) užimta. Sistema turi galėti parodyti rezervuoto staliuko savininko vardą ir pavardę (CLI parinktis: įveskite rezervuoto staliuko numerį; 
    REZULTATAI: Vardas ir pavardė / laikas rezervuotas). 
  - Priskyrus staliuką, sistema turi rodyti įvairius pusryčių, pietų , vakarienės , gėrimų (alkoholio. be alkoholio) meniu variantus, iš kurių būtų galima rinktis. 
    Į specialųjį meniu turi būti įtrauktas ir vegetarams bei veganams skirtas meniu. Prie visų meniu punktų turi būti nurodytas svoris, paruošimo laikas minutėmis, 
    kalorijos ir kaina.
  - Turiu turėti galimybę keisti užsakymą prieš mokėjimo skiltį. Taigi galiu ištrinti, pridėti daugiau, atnaujinti to paties užsakymo sumą.
  - Turėčiau galėti pasirinkti, ką noriu, iš visų meniu vienu užsakymu. Baigęs turiu matyti, ką pasirinkau, visą mokėtiną sumą ir 
    apytikslį laiką, kol bus patiektas maistas.
  - Į galutinę sąskaitą įtraukti galimybę pridėti arbatpinigių (% nuo visos kainos).
  - Atlikus mokėjimą , sistema turėtų sugeneruoti kvitą (registruoti).


## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Visas OOP kursas - "Youtube"] (https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (keli vaizdo įrašai)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
***

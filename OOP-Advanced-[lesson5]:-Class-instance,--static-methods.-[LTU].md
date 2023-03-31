## Instancijos metodai
Kaip jau žinome, `Instanciniai metodai` Pythone yra **funkcijos**, susietos su klasės egzemplioriumi. Jie gali pasiekti ir keisti **egzemplioriaus būseną**, taip pat gali pasiekti pačią klasę. Pateikiame pavyzdį apie instancinį metodą Pythone:

```python
class Car:
    def __init__(self, make: str, model: str, year: int) -> None:
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    
    def update_odometer(self, mileage: int) -> None:
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            raise ValueError("You can't roll back an odometer!")
    
    def drive(self, miles: int) -> None:
        self.update_odometer(self.odometer_reading + miles)

```

Šiame pavyzdyje apibrėžiame `Car` klasę su **atvejų metodais** `update_odometer()` ir `drive()`.  Metodas `update_odometer()` priima argumentą rida ir atnaujina automobilio atributo `odometer_reading` reikšmę. Metodas `drive()` priima argumentą `miles` ir `kviečia `update_odometer()` metodą, kad padidintų atributo `odometer_reading` reikšmę nurodytu mylių skaičiumi.

Be to, į objektus orientuotame programavime (OOP) klasė yra objektų, kuriuose yra duomenų ir metodų, kūrimo planas. Kurdami klasės egzempliorių, jūs sukuriate objektą, kuris turi savo būseną ir elgseną. Instancijos metodas yra funkcija, kuri yra susieta su klasės instancija ir gali pasiekti ir keisti jos būseną.

Instancijos metodai Pythone apibrėžiami klasėje, o pirmuoju argumentu nurodomas "self". "Self" reiškia klasės egzempliorių, kuriam metodas yra kviečiamas. Tai leidžia egzempliorių metodams pasiekti ir keisti egzemplioriaus atributus.

Norėdami iškviesti objekto egzemplioriaus metodą, pirmiausia turite sukurti klasės egzempliorių ir tada iškviesti metodą tame egzemplioriuje:

```python
my_car = Car("Honda", "Civic", 2021)
my_car.drive(100)
print(f"My car's odometer reading is now {my_car.odometer_reading} miles.")

```

This will output: `My car's odometer reading is now 100 miles`.

## Static Methods 
**Static methods** in Python are methods that _are bound to a class rather than an instanc_e of the class. They don't require access to the instance or the class itself and don't modify the state of the class or instance. **They are typically used for utility functions** that don't depend on the state of the object.

Here's an example of a static method in Python:

```python
class MathUtils:
    @staticmethod
    def add(a: int, b: int) -> int:
        return a + b

```
Šiame pavyzdyje apibrėšime `MathUtils` klasę su **statiniu metodu add**, kuris priima du sveikųjų skaičių argumentus `a` ir `b` ir grąžina jų sumą. Naudojame dekoratorių `@staticmethod`, kad parodytume, jog tai yra statinis metodas.

Norėdami iškviesti statinį metodą klasėje, galite naudoti klasės pavadinimą:

```python
result = MathUtils.add(2, 3)
print(result)  # Output: 5
```
Šiame pavyzdyje iškviečiame `MathUtils` klasės `MathUtils` pridėjimo `statinį metodą`, kaip argumentus perduodami `2` ir `3`. Metodas grąžina jų sumą, kuri saugoma kintamajame rezultate.

**Statiniai metodai gali būti kviečiami ir klasei, ir jos egzemplioriams**. Tačiau, kadangi jiems nereikia prieigos prie egzemplioriaus, _daug dažniau jie kviečiami pačioje klasėje_.

Štai dar vienas statinio metodo, kuriuo apskaičiuojamas apskritimo plotas, pavyzdys:

```python
class Circle:
    PI = 3.14159
    
    def __init__(self, radius: float) -> None:
        self.radius = radius
    
    def area(self) -> float:
        return Circle.calculate_area(self.radius)
    
    @staticmethod
    def calculate_area(radius: float) -> float:
        return Circle.PI * radius ** 2

```
Šiame pavyzdyje apibrėžiame `Circle` klasę su statiniu metodu `calculate_area`, kuris priima spindulio argumentą ir grąžina to spindulio apskritimo plotą. Taip pat apibrėžiame `__init__` metodą, kuris priima spindulio argumentą ir inicializuoja egzemplioriaus spindulio atributą, ir ploto metodą, kuris grąžina apskritimo plotą, apskaičiuotą iškvietus `calculate_area` statinį metodą.

Norėdami sukurti `Circle` klasės **atvejį** ir iškviesti jo ploto metodą, galime atlikti šiuos veiksmus:

```python
circle = Circle(5)
print(circle.area())  # Output: 78.53975
```
Šiame pavyzdyje sukursime `Circle` klasės egzempliorių, kurio spindulys yra 5. Tuomet iškviečiame **apskritimo** atvejo `area` metodą, kuris grąžina apskritimo plotą, apskaičiuotą iškvietus statinį metodą calculate_area.

Apibendrinant, statiniam metodui: 
 - Turi būti @staticmethod inicijuotas funkcijos dekoratorius.
 - Naudojant statinius metodus nei self (objekto egzempliorius), nei myClass (klasė) nėra netiesiogiai perduodami kaip pirmasis argumentas. Jie elgiasi kaip paprasti
   funkcijos, išskyrus tai, kad jas galima iškviesti iš egzemplioriaus arba klasės. Jos neturi jokio konkretaus argumento.
 - Statinis metodas taip pat yra metodas, kuris yra susietas su klase, o ne su klasės objektu.
 - Statinis metodas negali pasiekti ar keisti klasės būsenos.
 - Statiniai metodai nieko nežino apie klasės būseną. Jie yra naudingumo tipo metodai, kurie priima tam tikrus parametrus ir dirba su tais parametrais. Dėl 
   kita vertus, klasės metodai turi turėti klasę kaip parametrą.


## Pratimai: 

* Užduotis Nr.1:  

  Sukurkite klasę, kuri priima temperatūros matavimus `Kelvino` vienetais, ir pridėkite statinius metodus, skirtus temperatūros matavimams transformuoti 
  į `Celcijaus` ir `Fahrenheito` vienetus. Naudokite OOP abstrakcija. 


* Užduotis Nr.2:
 
  Sukurkite klasę, kuri priimtų bent penkis `imperinės sistemos` matavimus ir statiniais metodais transformuotų į `metrinę` sistemos vienetus.

* Užduotis Nr.3:

  Sukurti klasę `TimeUtils`, kuri turėtų statinį metodą `time_to_seconds`, priimantį laiko eilutę formatu `hh:mm:ss` ir grąžinantį laiko eilutę. 
  bendrą sekundžių skaičių, išreikštą tuo laiku. Naudokite **funkcinio programavimo paradigmą**.

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3-2) 

* Užduotis Nr.4: 

  Sukurkite klasę `Employee` su statiniu metodu `calculate_payroll`, kuris priima `Employee` egzempliorių sąrašą ir grąžina bendrą sumą. 
  kuri turi būti išmokėta visiems darbuotojams. Kiekvienas `Employee` egzempliorius turi du atributus: `Vardas` ir `Apmokestis`.

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4-1) 


## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Visas OOP kursas - "Youtube"](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (keli vaizdo įrašai)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [RealPhyton](https://realpython.com/instance-class-and-static-methods-demystified/)
***


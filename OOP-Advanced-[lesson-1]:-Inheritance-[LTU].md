## Daugkartinis paveldėjimas ir MRO (metodų pertvarkymo tvarka)

Pythono kalboje,  klasė **gali paveldėti iš kelių superklasių**, ši sąvoka vadinama `daugialypiu paveldėjimu`. Tai leidžia klasei paveldėti atributus ir metodus iš kelių viršklasių.

Pateikiame pavyzdį, kaip naudoti kartotinį paveldėjimą "Python":
```python

class Animal:
    def __init__(self, name: str) -> None:
        self.name = name
    
    def make_sound(self) -> None:
        print("Some generic animal sound")

class Dog(Animal):
    def __init__(self, name: str, breed: str) -> None:
        super().__init__(name)
        self.breed = breed
    
    def make_sound(self) -> None:
        print("Bark")

class Cat(Animal):
    def __init__(self, name: str, fur_color: str) -> None:
        super().__init__(name)
        self.fur_color = fur_color
    
    def make_sound(self) -> None:
        print("Meow")

# Štai klasės, kuri paveldi ir iš šuns, ir iš katės, pavyzdys
class DogCat(Dog, Cat):
    def __init__(self, name: str, breed: str, fur_color: str) -> None:
        super().__init__(name, breed)
        Cat.__init__(self, name, fur_color)

dogcat = DogCat("Fluffy", "Poodle", "White")
print(dogcat.name)  # prints "Fluffy"
print(dogcat.breed)  # prints "Poodle"
print(dogcat.fur_color)  # prints "White"
dogcat.make_sound()  # prints "Bark"

```

Pirmiau pateiktame pavyzdyje `DogCat` klasė paveldi iš `Dog` ir `Cat` klasių. Ji turi prieigą prie visų šių klasių atributų ir metodų. Kai sukuriame DogCat` egzempliorių, jis pirmiausia iškviečia `Dog` klasės `__init__` metodą, nurodydamas argumentus vardas ir veislė, o tada iškviečia `Cat` klasės `__init__` metodą, nurodydamas argumentus `pavadinimas` ir `kailinė_palva`.

Kai iškviečiame `DogCat` egzemplioriaus `make_sound` metodą, jis naudoja metodo, apibrėžto `Dog` klasėje, realizaciją, nes `Dog` klasė paveldimumo sąraše yra pirmiau už `Cat` klasę.

Daugkartinis paveldėjimas gali būti galingas įrankis, tačiau dėl jo kodas gali tapti sudėtingesnis ir sunkiau suprantamas, todėl jį reikėtų naudoti atsargiai.

### MRO

Python programoje, kai klasė paveldi iš kelių superklasių, gali būti neaišku, kurią atributo ar metodo versiją naudoti. Šiam dviprasmiškumui išspręsti "Python" naudoja mechanizmą, vadinamą **metodų skirstymo tvarka (MRO)**.

MRO - tai tvarka, kuria klasės atributai ir metodai paveldimi iš jos `viršinių klasių`. Ji nustato, kuri atributo ar metodo realizacija bus naudojama, kai klasės egzempliorius jį iškvies.

Štai pavyzdys, kaip MRO veikia Pythone:

```python

class A:
    def foo(self) -> None:
        print("A.foo")

class B(A):
    def foo(self) -> None:
        print("B.foo")

class C(A):
    def foo(self) -> None:
        print("C.foo")

class D(B, C):
    pass

d = D()
d.foo()  # prints "B.foo"

```

Pateiktame pavyzdyje `D` klasė paveldi iš `B` ir `C` klasių. Metodas `foo` yra apibrėžtas ir `B`, ir `C` klasėse, todėl neaišku, kurią iš jų naudoti.

Norėdamas nustatyti `D` klasės `MRO`, Python atlieka šiuos veiksmus:

1. Pradedama nuo `D` klasės ir ji įtraukiama į MRO sąrašą.
2. Peržiūrima pirmoji `D` viršklasė, kuri yra `B`. Jis įtraukia `B` į MRO sąrašą, o tada pakartoja šį procesą su `B` viršklase `A`.
3. Peržiūrima antroji `D` antrinė klasė, t. y. `C`. Jis įtraukia `C` į MRO sąrašą, o tada pakartoja šį procesą su `C` viršklase `A`.
4. Iš MRO sąrašo pašalinamos visos besidubliuojančios klasės. Šiuo atveju pašalinamas antrasis `A` egzempliorius, nes jis jau buvo įtrauktas į sąrašą.

Gautas `D` klasės MRO yra `[D, B, C, A]`. Tai reiškia, kad kai iškviesime `D` egzemplioriaus metodą foo, jis naudos metodo foo realizaciją, apibrėžtą `B` klasėje.

Norėdami pamatyti klasės MRO, galite naudoti `__mro__` atributą:

```python
print(D.__mro__)  
# prints (<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)

```

## Daugiapakopis paveldėjimas

Pythone klasė gali paveldėti iš klasės, kuri pati paveldi iš kitos klasės - ši sąvoka vadinama `daugiapakopiu paveldėjimu`. Tai leidžia klasei _paveldėti atributus ir metodus iš kelių paveldėjimo hierarchijos lygių_.

Štai pavyzdys, kaip naudoti kelių lygių paveldėjimą "Python":

```python

class A:
    def foo(self) -> None:
        print("A.foo")

class B(A):
    def bar(self) -> None:
        print("B.bar")

class C(B):
    def baz(self) -> None:
        print("C.baz")

c = C()
c.foo()  # prints "A.foo"
c.bar()  # prints "B.bar"
c.baz()  # prints "C.baz"
```

Pirmiau pateiktame pavyzdyje `C` klasė paveldi iš `B` klasės, kuri savo ruožtu paveldi iš `A` klasės. Taip sukuriama `daugiapakopio paveldėjimo` hierarchija, kurioje `C klasė` turi prieigą prie visų B ir A klasės atributų ir metodų**.

Kai sukuriame `C` egzempliorių ir iškviečiame `foo` metodą, jis naudoja `foo` metodo, apibrėžto `A` klasėje, realizaciją. Panašiai, kai iškviečiame `bar` metodą, jis naudoja `bar` metodo, apibrėžto `B` klasėje, realizaciją. O kai iškviečiame `baz` metodą, naudojama `baz` metodo, apibrėžto `C` klasėje, realizacija.

## Metodo perėmimas

Pythone `paviršutinė klasė` gali **pakeisti** savo viršklasės atributus ir metodus. Tai reiškia, kad poklasis gali apibrėžti savo atributo ar metodo, kuris jau egzistuoja superklasėje, įgyvendinimą.

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
Šiame pavyzdyje `Automobilių` klasė paveldi iš `Transporto priemonių` klasės ir **perima** `Start` metodą. Kai sukuriame `Car` egzempliorių ir iškviečiame `start` metodą, jis naudoja `start` metodo, apibrėžto `Car` klasėje, realizaciją, kuri spausdina pranešimą apie raktelio įkišimą į automobilį. Tada jis iškviečia `Vehicle` klasės `start` metodą, naudodamas `super().start()` sintaksę, kuri spausdina pranešimą apie automobilio užvedimą.


## Pratimai: 
🧠 : Pakartokite [OOP 2 dalis](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* Užduotis Nr.1:  

  Apibrėžkite Shape klasę su šiais atributais ir metodais:

  * Atributas name, kuris yra eilutė, reiškianti formos pavadinimą.
  * Atributas sides, kuris yra sveikasis skaičius, reiškiantis figūros kraštinių skaičių.
  * metodas area, kuris grąžina figūros plotą.

  Tada apibrėžkite stačiakampio klasę, kuri paveldi iš formos klasės ir turi šiuos atributus bei metodus:

  * atributas width, kuris yra kintamasis, reiškiantis stačiakampio plotį.
  * Aukščio atributas, kuris yra kintamasis, žymintis stačiakampio aukštį.
  * Metodas __init__, kuris inicializuoja pavadinimą, kraštines, plotį ir aukštį.
  * metodas area, kuris pakeičia klasės Shape metodą area ir grąžina stačiakampio plotą.

  Galiausiai apibrėžkite Square klasę, kuri paveldi iš Rectangle klasės ir turi šiuos atributus bei metodus:

  * Atributas side_length, kuris yra kintamasis, reiškiantis kvadrato kraštinių ilgį.
  * Metodas __init__, kuris inicializuoja atributą side_length ir iškviečia klasės Rectangle metodą __init__, kad būtų inicializuotas vardas, kraštinės, 
  pločio ir aukščio atributus.

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers#oop-advanced--inheritance) 


* Užduotis Nr.2:
 
  - Sukurti iš transporto priemonės klasės paveldimas klases: Autobusas, Taksi, Traukinys.
  - Viršklasėje įgyvendinkite bent penkis metodus, kurie apibūdintų šias transporto priemones.
  - Numatytasis bet kurios transporto priemonės bilieto mokestis yra sėdimų vietų skaičius * 100 . Jei Transporto priemonė yra Autobusas 
  - egzempliorius, turime pridėti papildomus 10 % prie visos kainos kaip techninės priežiūros mokestį.

* Užduotis Nr.3:

  - Apibrėžkite gyvūnų, žinduolių ir primatų klases.
  - Gyvūnas turi turėti atributą name ir metodą make_noise().
  - Mammal turėtų turėti atributą warm_blooded ir metodą give_birth().
  - Primate turėtų turėti atributą opposable_thumbs ir metodą swing().
  - Patikrinkite klases sukurdami šimpanzę ir priversdami ją atlikti įvairius veiksmus :) 🐒 

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers#task-nr3) 

* Užduotis Nr.4: 

  Tarkime, turime klases: A, B ir C:
    - Pakeiskite programą taip, kad į A klasę būtų pridėtas metodas say_hello, kuris spausdina "Sveiki iš A klasės".
    - Modifikuokite programą taip, kad į B klasę būtų pridėtas metodas say_hello, kuris spausdina "Hello from class B".
    - Modifikuokite programą, kad į C klasę būtų įtrauktas metodas say_hello, kuris spausdina "Sveiki iš C klasės".
    - Sukurkite C klasės objektą ir iškvieskite jam metodą say_hello. Koks bus išvesties rezultatas?
    - Pakeiskite programą taip, kad B klasės metodas say_hello iškviestų A klasės metodą say_hello naudodamas super() funkciją.
    - Sukurkite C klasės objektą ir vėl iššaukite jo metodą say_hello. Koks dabar bus išvesties rezultatas?

## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Visas OOP kursas - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (keli vaizdo įrašai)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [PyNative](https://pynative.com/python-inheritance/)
***


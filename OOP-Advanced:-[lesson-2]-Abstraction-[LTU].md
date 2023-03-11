## Abstrakčios klasės ir metodai

Objektiniame programavime **abstrakcija** yra principas, padedantis atskirti klasės įgyvendinimo detales nuo jos **sąsajos** (žr. toliau ⏬ ), arba būdo, kuriuo kitos klasės sąveikauja su ja. Tai leidžia užtikrinti didesnį lankstumą ir pakartotinį kodo panaudojimą, nes klasės įgyvendinimą galima keisti nedarant poveikio kitoms sistemos dalims.

**Pythone abstrakcija pasiekiama naudojant abstrakčias klases ir abstrakčius metodus**. `Abstrakti klasė` - tai klasė, kuri yra apibrėžta, bet **nėra skirta instantizuoti**. Vietoj to ji tarnauja kaip **šablonas** kitoms klasėms, iš kurių galima **paveldėti**. _Abstrakčios klasės gali apibrėžti abstrakčius metodus, t. y. metodus, kurie apibrėžiami abstrakčioje klasėje, bet neturi įgyvendinimo. Abstrakčios klasės poklasiai privalo **pateikti** šių metodų realizaciją.

Pateikiame abstrakčios klasės pavyzdį Pythone:

```python
from abc import ABC, abstractmethod
from typing import Union

class Shape(ABC):
    @abstractmethod
    def area(self) -> int:
        pass

class Rectangle(Shape):
    def __init__(self, width: int, height: int):
        self.width = width
        self.height = height

    def area(self) -> int:
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius: float):
        self.radius = radius

    def area(self) -> float:
        return 3.14 * self.radius ** 2

```
Pirmiau pateiktame pavyzdyje `Shape` yra `abstrakti klasė`, apibrėžianti abstraktų metodą `area()`. `Rectangle` ir `Circle` klasės yra `Shape` poklasiai ir pateikia `area()` metodo realizacijas.

Svarbu pastebėti, kad `ABC` ir `abstractmethod` yra python integruotos bibliotekos `abc` dalis, Ši biblioteka suteikė python `abstrakčią bazinę klasę (ABC)` ir dekoratorių (žr. kitą pamoką, TBA) `abstractmethod`, kurį reikia importuoti ir naudoti, įgyvendinant `abstrakčias` klases.

Taip pat svarbu paminėti, kad neleidžiama kurti abstrakčios klasės egzempliorių**, Jei bandysite sukurti abstrakčios klasės egzempliorių, "Python" iškels `TypeError` išimtį.

Be pirmiau pateikto pavyzdžio, pateikiame dar vieną pavyzdį:

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def no_of_wheels(self) -> None:
        pass

class Car(Vehicle):
    def no_of_wheels(self) -> int:
        return 4

class Bike(Vehicle):
    def no_of_wheels(self) -> int:
        return 2
```
Šiame pavyzdyje `Transporto priemonė` yra abstrakti klasė, apibrėžianti abstraktų metodą `ne_riedžių()`, o `Automobilis`, `Dviratis` yra konkretūs poklasiai, kurie pateikia metodo `ne_riedžių` realizaciją.

Dar vienas pavyzdys apie mokėjimo sistemas (sudėtingesnis: abstrakcija, paveldėjimas):

```python
from abc import ABC, abstractmethod
from typing import List

class Payment(ABC):
    @abstractmethod
    def get_transactions(self) -> List[str]:
        pass

    @abstractmethod
    def process_payment(self, amount: float) -> str:
        pass

class CreditCardPayment(Payment):
    def __init__(self, card_number: str):
        self.card_number = card_number
        self.transactions = []

    def get_transactions(self) -> List[str]:
        return self.transactions

    def process_payment(self, amount: float) -> str:
        transaction_id = "CC" + str(hash(str(amount) + self.card_number))
        self.transactions.append(transaction_id)
        return f"Payment of {amount} processed with card number {self.card_number}. Transaction ID: {transaction_id}"

class PayPalPayment(Payment):
    def __init__(self, email: str):
        self.email = email
        self.transactions = []

    def get_transactions(self) -> List[str]:
        return self.transactions

    def process_payment(self, amount: float) -> str:
        transaction_id = "PP" + str(hash(str(amount) + self.email))
        self.transactions.append(transaction_id)
        return f"Payment of {amount} processed with PayPal account {self.email}. Transaction ID: {transaction_id}"

```

Šiame pavyzdyje yra abstrakti klasė `Payment`, kuri apibrėžia du abstrakčius metodus `get_transactions()` ir `process_payment()`.

`CreditCardPayment` ir `PayPalPayment` yra `Payment` poklasiai, kuriuose pateikiamos konkrečios dviejų abstrakčių metodų, apibrėžtų pagrindinėje klasėje, realizacijos.

Kiekvienas poklasis turi savo mokėjimo apdorojimo ir sandorio ID generavimo būdą.

Kiekviena klasė taip pat turi egzemplioriaus kintamąjį transactions, kuriame pateikiamas sandorių, atliktų naudojant šį mokėjimo būdą, sąrašas. Kiekvienos klasės metodas `get_transactions()` grąžina per šį mokėjimo metodą atliktų operacijų sąrašą.

Šiame pavyzdyje parodyta, kaip _naudojama abstrakcija, siekiant atskirti skirtingų mokėjimo metodų įgyvendinimo detales nuo jų bendros sąsajos, apibrėžtos `Payment` klasėje. _Mokėjimo klasė pateikia šabloną, kuriuo turi sekti poklasiai, o poklasiai pateikia konkrečias abstrakčių metodų realizacijas _.

**Geriausia praktika yra visus abstrakčius metodus laikyti atskiroje abstrakčioje klasėje**, taip galite užtikrinti, kad panašioms klasėms būdingos bendros savybės ir metodai bus užrašyti ir valdomi vienoje vietoje.

Trumpai tariant - _pytono abstrakcijos principas leidžia atskirti įgyvendinimo detales nuo sąsajos, o abstrakčiosios klasės ir metodai suteikia galimybę apibrėžti šį atskyrimą pateikiant šabloną, kuriuo turi sekti poklasiai, taip poklasiai priversti įgyvendinti tam tikrus metodus, apibrėžtus abstrakčiojoje klasėje_.

## Abstrakti klasė vs sąsaja
Kaip jau žinome, abstrakčioji klasė yra klasė, kurioje yra vienas ar daugiau abstrakčiųjų metodų, t. y. metodų**, kurie turi apibrėžimą, bet neturi įgyvendinimo**. Konkretus abstrakčios klasės poklasis, prieš jį instancuojant, turi pateikti visų savo abstrakčių metodų realizaciją. Abstrakti klasė taip pat gali apibrėžti konkrečius metodus, kurie turi ir apibrėžtį, ir realizaciją.

Kita vertus, **sąsaja** yra abstrakčių metodų, kuriuos klasė gali įgyvendinti, rinkinys**. Pythone nėra integruotos sąsajos sąvokos, tačiau ją galima įgyvendinti naudojant abstrakčią _bazinę klasę (ABC)_. Abstrakti bazinė klasė - tai klasė, kurioje yra tik abstraktūs metodai, ir ji nėra skirta instantizuoti. Vietoj to tikimasi, kad kitos klasės paveldės iš jos ir pateiks jos abstrakčių metodų realizacijas.

Štai abstrakčios klasės pavyzdys:

```python3
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass
    
    def perimeter(self) -> float:
        pass

class Rectangle(Shape):
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height
    
    def area(self) -> float:
        return self.width * self.height
    
    def perimeter(self) -> float:
        return 2 * (self.width + self.height)

rect = Rectangle(3, 4)
print(rect.area()) # 12
print(rect.perimeter()) # 14
 
```

ir sąsajos:

```python3
from abc import ABC, abstractmethod

class IAnimal(ABC):

    @abstractmethod
    def move(self) -> str:
        pass

    @abstractmethod
    def eat(self) -> str:
        pass

class Dog(IAnimals):
    def move(self) -> str:
        return 'Dog can walk and run'

    def eat(self) -> str:
        return 'Dog eat meat'

class Fish(IAnimals):
    def move(self) -> str:
        return 'Fish swim'

    def eat(self) -> str:
        return 'Fish eat small insects or plants'

dog = Dog()
print(dog.move())
print(dog.eat())

fish = Fish()
print(fish.move())
print(fish.eat())

```

## Pratimai: 
🧠 : Pakartokite [OOP 2 dalis](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* **Užduotis Nr.1**:
  
  Sukurkite abstrakčią klasę Animal, kurios įvestis - gyvūno vardas, ir ją inicializuokite. 
  Sukurti `speak` abstraktų metodą, kurį galėtų perrašyti poklasiai.
  Ir `get_name` metodą, kuris grąžina gyvūno vardą.

  Dabar sukurkite du gyvūnų poklasius: `Dog` ir `Cat`, kurie perrašo `speak` metodą ir pateikia realizaciją, grąžinančią eilutę "Dog 
  sako Woof!" ir "Cat says Meow!".
  

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-1) 

* **Užduotis Nr.2**:

  Sukurkite abstrakčią klasę `Money`, kuri įvesties duomenimis priima `currency` ir `value` bei ją inicializuoja. Klasė turi turėti šiuos metodus:
   - `get_value` metodą, kuris grąžina pinigų vertę.
   - `get_currency` metodą, kuris grąžina pinigų valiutą.
   - `convert_to_currency` abstraktus metodas, kuris įvesties metu priima tikslinę valiutą ir konvertavimo kursą ir konvertuoja pinigų vertę į tikslinę valiutą. 
      valiutą.

   Dabar sukurkite du `Money` poklasius: `Cash` ir `Card`. Klasė `Cash` konstruktoriaus įraše turėtų priimti grynųjų pinigų nominalą, o 
   turėtų įgyvendinti `konvertuoti_į_valiutą` metodą. Kortelės `Card` klasė konstruktoriaus įvestyje turėtų priimti kortelės kredito limitą ir turėtų 
   įgyvendinti `convert_to_currency` metodą, naudodama konvertavimo kursą, kad konvertuotų kortelės vertę į tikslinę valiutą.

   [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2) 

* **Užduotis Nr.3**:

  Kaip ir ankstesniuose pavyzdžiuose, sukurkite savo pavyzdį. Abstrakčioje klasėje turėtų būti penki (3 abstraktūs ir 2 įprasti ) metodai. Sukurkite 2 
  poklasius, kurie paveldėtų abstrakčią klasę. 

* **Užduotis Nr.4**: 

  Sukurkite skaičiuotuvo programą: joje turėtų būti abstrakti klasė su metodais (abstrakčiais ir neabstrakčiais), bazinė klasė, `geometrijos`, `aritmetinis` skaičiuotuvas 
  klases. 
  Kiekviena poklasė turėtų turėti bent 5 metodus, kad būtų galima atlikti keletą prasmingų skaičiavimo operacijų. 
  
## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Visas OOP kursas - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (keli vaizdo įrašai)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [Oficiali dokumentacija - Abstrakčios bazinės klasės](https://docs.python.org/3/library/abc.html)
* [PythonTutorial](https://www.pythontutorial.net/python-oop/python-abstract-class/)
***


## Klasės metodai

Python `classmethod()` funkcija yra galingas įrankis, leidžiantis kūrėjams švariai ir efektyviai **manipuliuoti klasės lygmens duomenimis**. Funkcija `classmethod()`, galinti kurti _factory metodus, alternatyvius konstruktorius, valdyti klasės lygio būseną ir įgyvendinti klasės lygio operacijas, suteikia galimybę lanksčiai ir elegantiškai spręsti daugelį programavimo uždavinių. Panagrinėsime, kaip naudoti `classmethod()` Pythone, kad pagerintumėte kodo organizavimą ir skaitomumą. Naudodami `classmethod()` patobulinsite savo "Python" įgūdžius, o jūsų kodas taps efektyvesnis ir lengviau prižiūrimas.

#### Kas yra `classmethod()` "Python"?

`classmethod()` yra "Python" programoje integruota funkcija, naudojama **metodui, kuris veikia klasę, o ne klasės egzempliorių**, apibrėžti. Ji naudojama sukurti metodui, kuris **gali būti iškviestas tiesiogiai klasėje**, o ne klasės egzemplioriuje. Tai reiškia, kad metodas gali būti naudojamas klasės lygio duomenims tvarkyti arba operacijoms, kurios nėra būdingos kuriam nors vienam klasės egzemplioriui, atlikti.
`klasėsmetodo()` sintaksė yra tokia:

```python
class MyClass:
    @classmethod
    def my_class_method(cls, arg1: Any, arg2: Any, ...) -> cls
        # code here
```
Funkcija `classmethod()` taikoma kaip dekoratorius klasės metodui. Pirmasis klasės metodo argumentas **visada yra pati klasė**, išreikšta parametru `cls`. Tai leidžia metodui pasiekti ir keisti klasės lygio duomenis.

Štai klasės metodo, kuriuo apskaičiuojamas stačiakampio plotas, pavyzdys:

```python3
class Rectangle:
    def __init__(self, width: float, height: float) -> None:
        self.width = width
        self.height = height
    
    def area(self) -> float:
        return self.width * self.height
    
    @classmethod
    def from_square(cls, side_length: float) -> 'Rectangle':
        return cls(side_length, side_length * 2)

rectangle1: Rectangle = Rectangle(3.0, 4.0)
rectangle2: Rectangle = Rectangle.from_square(2.0)

print(rectangle1.area())  # 12.0
print(rectangle2.area())  # 4.0

```
### Kodėl reikia naudoti `classmethod()`?

Pagrindinis `classmethod()` naudojimo privalumas yra tas, kad jis leidžia apibrėžti metodus, kurie veikia pačią klasę, o ne klasės egzempliorių. Tai gali būti naudinga įvairiose situacijose, pvz:
- **Gamybinių metodų kūrimas** - `classmethods` galima naudoti kuriant gamyklinius metodus, kurie sukuria ir grąžina naujus klasės egzempliorius su tam tikra konfigūracija:

```python
import datetime

class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name: str, birth_year: int) -> 'Person':
        age = cls.get_age(birth_year)
        return cls(name, age)

    @staticmethod
    def get_age(birth_year: int) -> int:
        return datetime.date.today().year - birth_year

person: Person = Person.from_birth_year('John', 1990)
print(person.name)  # John
print(person.age)  # 33

```
Šiame pavyzdyje `from_birth_year()` klasės metodas veikia kaip **pagrindinis metodas**, kuris sukuria naują `Person` egzempliorių iš gimimo metų. Jis apskaičiuoja asmens amžių naudodamas statinį metodą `get_age()` ir grąžina naują klasės `Person` egzempliorių.

- Alternatyvių konstruktorių kūrimas** - `classmethods` gali būti naudojamas alternatyviems klasės konstruktoriams** sukurti. Tai naudinga, kai norite sukurti klasės egzempliorius su skirtingais argumentų rinkiniais: 

```python
class Point:
    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y

    @classmethod
    def from_tuple(cls, point_tuple: tuple[float, float]) -> 'Point':
        x, y = point_tuple
        return cls(x, y)

point: Point = Point.from_tuple((3, 4))
print(point.x)  # 3
print(point.y)  # 4

```

Šiame pavyzdyje klasės metodas `from_tuple()` veikia kaip **alternatyvus konstruktorius**, kuris sukuria naują `Point` egzempliorių iš `(x, y)` reikšmių tuple. Jis grąžina naują Point klasės egzempliorių.

- Klasės lygmens būsenos valdymas** - klasės lygmens būsenai valdyti galima naudoti `klasės metodus`. Tai reiškia, kad galite apibrėžti metodą, kuris keičia arba kreipiasi į kintamąjį, kuris yra bendras visiems klasės egzemplioriams:

```python
class Car:
    total_cars_sold: int = 0

    def __init__(self, make: str, model: str):
        self.make = make
        self.model = model
        Car.total_cars_sold += 1

    @classmethod
    def get_total_cars_sold(cls) -> int:
        return cls.total_cars_sold

car1: Car = Car('Toyota', 'Camry')
car2: Car = Car('Honda', 'Civic')

print(Car.get_total_cars_sold())  # 2

```

Šiame pavyzdyje klasės lygio kintamasis `total_cars_sold` didinamas kiekvieną kartą, kai sukuriamas naujas klasės `Car` egzempliorius. Klasės metodas `get_total_cars_sold()` grąžina dabartinę kintamojo `total_cars_sold` vertę.

- Klasės lygmens operacijų įgyvendinimas** - `klasės metodais` galima įgyvendinti klasės lygmens operacijas, pavyzdžiui, rūšiuoti arba filtruoti klasės egzempliorių sąrašą:

```python
class Student:
    all_students: list['Student'] = []

    def __init__(self, name: str, grade: float):
        self.name = name
        self.grade = grade
        Student.all_students.append(self)

    @classmethod
    def get_highest_grade(cls) -> 'Student':
        return max(cls.all_students, key=lambda student: student.grade)

    @classmethod
    def get_lowest_grade(cls) -> 'Student':
        return min(cls.all_students, key=lambda student: student.grade)

student1: Student = Student('John', 90)
student2: Student = Student('Jane', 95)
student3: Student = Student('Alice', 80)

print(Student.get_highest_grade().name)  # Jane
print(Student.get_lowest_grade().name)  # Alice

```
Atributas `all_students` deklaruojamas kaip klasės lygmens sąrašas, kuriame yra objektai `Student`. `Student` egzempliorių atributas name deklaruojamas kaip eilutė, o atributas grade - kaip kintamasis. Klasės metodai `get_highest_grade` ir `get_lowest_grade` grąžina "Student`" objektą, turintį atitinkamai aukščiausią ir žemiausią įvertinimą. `Student1`, `Student2` ir `Student3` egzemplioriai yra aiškiai anotuoti su `Student` klase.

## Pratimai: 

1) Sukurkite klasės metodą, grąžinantį duoto skaičiaus **faktorių**.

   [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-3) 


2) Sukurkite klasės metodą, grąžinantį duotos eilutės **atvirkštinę eilutę**.

   [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2-2) 

3) Sukurkite klasės metodą, kuris grąžintų** pirminių skaičių sąrašą** iki duoto skaičiaus.

   [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3-3) 

4) Sukurkite paprastą banko sąskaitos klasę `BankAccount` su šiomis specifikacijomis:
    - `BankAccount` klasė turi turėti atributą `balance`, kuris prasideda nuo `0`.
    - Ji turėtų turėti instance metodą `deposit`, kuris leistų pridėti sumą prie balanso.
    - Ji turėtų turėti instance metodą `withdraw`, leidžiantį paimti sumą iš likučio. Jei likutis yra mažesnis už išėmimo sumą, 
      išspausdinkite pranešimą "Insufficient funds" (lėšų nepakanka).
    - Pridėkite klasės metodą `from_balance`, kuris kaip argumentą priima pradinį likutį ir grąžina naują `BankAccount` instance su šiuo pradiniu 
      likučiu.
    - Pridėkite statinį metodą `transfer`, kuris kaip argumentus priima du `BankAccount` instance ir sumą. Jis turėtų paimti sumą iš pirmosios 
      sąskaitos ir pervesti ją į antrąją sąskaitą.

    [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4-2)

5) Sukurkite `SpaceStation` klasę su šiomis specifikacijomis:
   - `SpaceStation` klasė turi turėti atributą `astronauts`, kuris yra žodynų sąrašas. Kiekvienas žodynas reiškia astronautą ir turi 
     raktus, kuriuos sudaro šie elementai: `name`, `nationality` ir `mission_duration`.
   - Ji turėtų turėti instance metodą `add_astronaut`, kuris priima `name`, `nationality` ir `mission_duration` ir sukuria naują astronautų žodyną, 
     ir įtraukia jį į astronautų sąrašą.
   - Jis turėtų turėti instance metodą `find_astronaut`, kuris priima `name` ir grąžina astronautų žodyną su šiuo `name` arba 
     `None`, jei toks astronautas nerastas.
   - Pridėkite klasės metodą `from_astronaut_list`, kuris priima astronautų sąrašą (kiekvienas iš jų pateikiamas kaip žodynas) ir grąžina naują 
     `SpaceStation` egzempliorių su tais astronautais.
   - Pridėti statinį metodą `is_long_term_mission`, kuris priima astronauto žodyną ir grąžina `True`, jei astronauto misijos trukmė yra ilgesnė nei 
     `6` mėnesių, o kitu atveju - `False`.
   - Pridėkite instance metodą `remove_astronaut`, kuris priima `name` ir pašalina astronautą su šiuo vardu iš astronautų sąrašo.

    [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-5) 

6) Sukurkite klasę, vaizduojančią bibliotekos sistemą. Bibliotekos sistema turi turėti knygų, kurias vartotojai gali pasiskolinti, kolekciją. Vartotojai 
   gali užsiregistruoti bibliotekos sistemoje, skolintis knygas ir jas grąžinti. Bibliotekos sistema turėtų sekti vartotojų pasiskolintų knygų ir turimų 
   knygų skaičių kiekvienos knygos egzempliorių.

   [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-6) 


## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Visas OOP kursas - "Youtube"](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python klasės ir statiniai metodai](https://www.youtube.com/watch?v=rq8cL2XMM5M&t)
* [RealPhyton](https://realpython.com/instance-class-and-static-methods-demystified/)
***





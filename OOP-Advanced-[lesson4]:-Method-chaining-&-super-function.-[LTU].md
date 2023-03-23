## Metodų grandinė 

Metodų grandininis sujungimas - tai metodas, kai _daugelio metodų iškvietimai sujungiami į vieną komandą**, naudojant vieno metodo išvestį kaip kito metodo įvestį. Dėl to kodas gali būti glaustesnis ir aiškesnis, taip pat lengva grandininiu būdu sujungti operacijas, kurias reikia atlikti su objektu.

Pateikiame metodų grandininio jungimo Pythone pavyzdį:

```python
class MyString:
    def __init__(self, value: str):
        self.value = value

    def add_exclamation(self) -> 'MyString':
        self.value += "!"
        return self

    def make_upper(self) -> 'MyString':
        self.value = self.value.upper()
        return self

my_string = MyString("hello")
my_string.add_exclamation().make_upper()

print(my_string.value) # output: "HELLO!"

```
Šiame pavyzdyje turime `MyString` klasę su dviem metodais: `add_exclamation` ir `make_upper`. Abu šie metodai grąžina `self`, todėl galime grandininiu būdu sujungti jų iškvietimus. Metodas `add_exclamation` keičia objekto `MyString` vertę, pridėdamas prie jos šauktuką, o metodas `make_upper` keičia vertę, konvertuodamas ją į didžiąją raidę.

Sukuriame `MyString` egzempliorių su verte `hello`, o tada vienu sakiniu jam iškviečiame `add_exclamation` ir `make_upper`. Dėl to objekto `MyString` reikšmė pakeičiama į `HELLO!`.
Kitas pavyzdys:


```python
class Person:
    def __init__(self, name: str, age: int) -> None:
        self.name = name
        self.age = age
        self.address = None
    
    def set_name(self, name: str) -> 'Person':
        self.name = name
        return self

    def set_age(self, age: int) -> 'Person':
        self.age = age
        return self
    
    def set_address(self, address: str) -> 'Person':
        self.address = address
        return self
    
    def __str__(self) -> str:
        return f'{self.name}, {self.age}, {self.address}'

p = Person("John", 25)
p.set_address("123 Main St").set_age(26)

print(p) # output: "John, 26, 123 Main St"

```

Šiame pavyzdyje turime `Person` klasę, kuri turi tris metodus: `set_name`, `set_age` ir `set_address`. Kiekvienas iš šių metodų nustato skirtingą `Person` objekto atributą ir grąžina patį **objekto egzempliorių**. Paskutinėse kodo eilutėse matome, kaip grandiniškai sujungti metodų iškvietimus naudojant `return` teiginį.

Sukuriame `Person` egzempliorių su vardu `John` ir amžiumi `25`, tada vienu sakiniu grandininiu būdu iškviečiame du metodus `set_address` ir `set_age`, kurie atitinkamai nustato adreso atributą `123 Main St` ir amžiaus atributą `26`.

Atkreipkite dėmesį į `__str__` (būsima paskaita - magiški metodai) metodą, kuris leidžia mums atspausdinti asmens objektą skaitomu formatu, jis neprivalomas, bet leidžia lengvai pamatyti klasės būseną.

Šiame pavyzdyje parodyta, kaip galime naudoti_metodų grandinėlę_, kad vienu glaustu teiginiu nustatytume kelis objekto atributus, todėl kodas tampa skaitomesnis ir lengviau suprantamas.

## super() funkcija

Pythone `super()` funkcija naudojama **kviesti metodą iš pagrindinės klasės**. Tai ypač naudinga tais atvejais, kai kuriamas poklasis ir norima perrašyti tėvinės klasės metodą, bet vis tiek norima kokiu nors būdu naudoti pradinio metodo funkcionalumą.

Pateikiame pavyzdį, kaip naudoti super() funkciją norint iškviesti metodą iš patronuojančios klasės:

```python
class Parent:
    def greet(self) -> None:
        print("Hello from Parent class")

class Child(Parent):
    def greet(self) -> None:
        super().greet()
        print("Hello from Child class")

c = Child()
c.greet()
# output: 
# "Hello from Parent class"
# "Hello from Child class"
```
Šiame pavyzdyje turime `Parent` klasę su `greet` metodu, kuris paprasčiausiai spausdina "Hello from Parent class". Klasė `Child` paveldi iš klasės `Parent` ir taip pat turi savo metodo `greet` realizaciją.

`Child` klasės sveikinimo metodas naudoja `super()` funkciją, kad iškviestų savo tėvinės klasės `Parent` metodą `greet`. Po to ji spausdina "Hello from Child class" (Sveiki iš Child klasės).

Taigi, `super()` funkcija čia naudojama iškviesti tėvinės klasės `greet` metodą, kad antrinė klasė galėtų paveldėti tėvinės klasės metodo funkcionalumą ir pridėti savo funkcionalumą.

Štai dar vienas pavyzdys:

```python
class A:
    def __init__(self, value: int) -> None:
        self.value = value
        
    def increment(self) -> None:
        self.value += 1

class B(A):
    def __init__(self, value: int, step: int) -> None:
        super().__init__(value)
        self.step = step
        
    def increment(self) -> None:
        super().increment()
        self.value += self.step

b = B(5, 3)
b.increment()
print(b.value) # output: 8

```
Šiame pavyzdyje turime dvi klases: `A` ir `B`. `A` turi `__init__` metodą, kuris priima parametrą value ir priskiria jį atributui value. Ji taip pat turi metodą increment, kuris padidina atributą value vienetu.

`B` yra `A` poklasis, jis paveldi `A` funkcionalumą ir taip pat turi savo funkcionalumą. `B` turi papildomą žingsnio atributą, kurį priima kaip parametrą savo `init` metode, taip pat turi savo inkrement metodo realizaciją, kuri iškviečia viršklasės inkrement metodą, naudodama `super().increment()`, ir padidina vertės atributą žingsniu.

Sukūrus `B` egzempliorių ir iškvietus inkrementavimo metodą, pirmiausia iškviečiamas tėvinio egzemplioriaus inkrementavimo metodas, kuris padidina reikšmės atributą vienetu, o paskui jį padidina žingsniu.

Svarbu atkreipti dėmesį, kad iškvietus `super()` metodą, jis grąžina laikiną viršklasės objektą, kuris leidžia iškviesti jos metodus.

Funkcija `super()` ypač naudinga dirbant su_ daugialypiu paveldėjimu ir padeda išvengti pavadinimų konfliktų tarp skirtingų tėvinių klasių metodų.

## Pratimai: 
🧠 : Pakartokite [OOP 2 dalis](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* **Užduotis Nr.1**:
  
  Sukurkite klasę `Person`, kuri turi du metodus: `set_name` ir `set_age`, kuriais nustatomi atitinkamai klasės vardo ir amžiaus atributai.
  Pakeiskite šiuos metodus taip, kad jie grąžintų `self`, kad jų iškvietimus būtų galima grandininiu būdu sujungti.
  

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1) 

* **Užduotis Nr.2**:

  Sukurkite klasę Currency, turinčią šias savybes:

    - kodą: USD", "EUR", "GBP").
    - amount (suma)
    - exchange_rate

  Sukurkite šiuos metodus:

    - set_code: Metodas, kuris priima 3 raidžių valiutos kodą ir nustato objekto atributą code
    - set_amount: Metodas, priimantis skaičių float ir nustatantis objekto atributą amount
    - set_exchange_rate: Metodas, priimantis kintamąjį skaičių ir nustatantis objekto atributą exchange_rate
    - convert: Metodas, priimantis 3 raidžių valiutos kodą ir kintamąjį skaičių, reiškiantį naująjį valiutos kursą, ir apskaičiuojantis naująją sumą. 
      valiutą pagal valiutos kursą.
    - __str__: Metodas, kuris grąžina valiutos objekto eilutę tokiu formatu "kodas: suma".

     Kiekvienas metodas turėtų grąžinti klasės egzempliorių, kad būtų galima taikyti metodų grandinę.

* **Uždavinys Nr.3**:

  - Sukurkite Animal klasę su metodu speak, kuris spausdina "Animal can't speak" (Gyvūnas negali kalbėti).

  - Sukurkite klasę Dogs, kuri paveldi iš Animals ir pakeičia metodą speak, kad spausdintų "Woof woof".

  - Sukurkite klasę Katės, kuri paveldi iš Gyvūnų ir pakeičia metodą kalbėti. Tačiau šiame naujame metode iškvieskite klasės Gyvūnai metodą kalbėti 
    naudodami super() funkciją, po to spausdinkite "Miau miau miau".

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3) 

* **Užduotis Nr. 4**: 

  Sukurkite klasę Person, kuri turi šias savybes:

   - vardas: eilutė, reiškianti asmens vardą.
   - amžius: Visas skaičius, reiškiantis asmens amžių.

  Sukurkite šiuos metodus:

   - get_name: Metodas, grąžinantis asmens vardą
   - get_age: Metodas, grąžinantis asmens amžių
   - __str__: Metodas, kuris grąžina eilutę, atvaizduojančią Person objektą tokiu formatu: "vardas yra amžius metai."

  Sukurkite klasę Student, kuri paveldi iš Person ir prideda šias savybes:

   - Student_id: Įrašykite: Studentidid: sveikasis skaičius, reiškiantis studento ID
   - major: Studentas: eilutė, reiškianti studento specialybę

  Sukurkite šiuos metodus:

   - get_student_id: Metodas, grąžinantis studento ID
   - get_major: Metodas, grąžinantis studento specialybę
   - __str__: Metodas, kuris grąžina Student objekto eilutę tokiu formatu: "vardas yra amžiaus metų amžiaus studentas, kurio specialybė 
     major. Studento ID: student_id"

  Sukurkite klasę GraduateStudent, kuri paveldi iš Student ir prideda šias savybes:

   - programa: Įrašoma: eilutė, reiškianti studento programą.
   - patarėjas: A string, reiškianti studento patarėją.

  Sukurkite šiuos metodus:

   - get_program: Metodas, kuris grąžina studento programą
   - get_advisor: Metodas, kuris grąžina magistranto patarėją
   - __str__: Metodas, kuris grąžina GraduateStudent objekto eilutę tokiu formatu: "vardas yra amžiaus metų absolventas 
     studentas, kurio pagrindinė specialybė yra major major. Studento ID: student_id. Programa: programa ir patarėjas: patarėjas."
   - __init__: Šis metodas turėtų priimti tuos pačius parametrus kaip ir Person init, tačiau taip pat priimti papildomus parametrus student_id, major, program, 
     advisor ir iškviesti super klasės init metodą su Person parametrais bei nustatyti papildomus parametrus.

   Parodykite pavyzdžių su veikiančiu kodu. 
   
 [Patarimas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4) 

## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Visas OOP kursas - "Youtube"](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (keli vaizdo įrašai)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [QuanticDev - method chaining](https://quanticdev.com/articles/method-chaining/)
* [RealPhyton - super() funkcija](https://quanticdev.com/articles/method-chaining/)
***


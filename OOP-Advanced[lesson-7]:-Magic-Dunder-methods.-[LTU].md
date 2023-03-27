## Magiški metodai

Pythono kalboje _"magiškais metodais"_ arba _"dunder metodais"_ vadinami specialūs metodai, kurių pavadinimų pradžioje ir pabaigoje yra **dvigubas pabraukimas** (pvz., `__init__`, `__add__`). Šie metodai naudojami tam tikrų operacijų su klasės objektais elgsenai apibrėžti. Pavyzdžiui, `__add__` metodas iškviečiamas, kai klasės objektams naudojamas `+` operatorius, o `__init__` metodas iškviečiamas, kai sukuriamas naujas klasės objektas. Apibrėždami šiuos metodus klasėje, galite pritaikyti tos klasės egzempliorių integruotų operacijų elgseną. Apžvelgsime tik kai kuriuos iš jų, visą sąrašą rasite [čia](https://docs.python.org/3/reference/datamodel.html).

### `__init__` :
Kaip jau žinote, `__init__` metodas yra specialus Python klasių metodas, kuris iškviečiamas, kai sukuriamas naujas klasės egzempliorius. Jis naudojamas objekto pradinei būsenai nustatyti. Pirmasis `__init__` metodo argumentas yra self, kuris nurodo kuriamo objekto egzempliorių. Argumentą self "Python" automatiškai perduoda, kai kuriamas naujas egzempliorius, todėl jums nereikia jo įtraukti į metodo iškvietimą.

Pateikiame klasės `Person`, turinčios `__init__` metodą, pavyzdį:

```python
class Person:
    def __init__(self, name:str, age:int):
        self.name = name
        self.age = age
```
### `__str__` : 

`__str__` dunder metodas naudojamas objekto _string reprezentacijai apibrėžti. Jis iškviečiamas, kai objektui naudojamos integruotos `str()` arba `print()` funkcijos, ir grąžina eilutę, apibūdinančią objektą. Pateikiame pavyzdį, kaip naudoti `__str__` metodą, kad apibrėžtumėte nuosavo objekto, vadinamo `Person`, eilutės atvaizdavimą:

```python3
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Person(name={self.name}, age={self.age})"

p = Person("John", 30)
print(p) # Person(name=John, age=30)

```

### `__repr__` : 
`__repr__` naudojamas objekto _"oficialiam"_ arba nedviprasmiškam _string reprezentacijai_ apibrėžti. Ją iškviečia integruota `repr()` funkcija, taip pat ją naudoja interaktyvusis vertėjas objektui atvaizduoti, kai **jis nėra priskirtas kintamajam**. Ji turėtų grąžinti eilutę, kurią perdavus `eval()` funkcijai, būtų sukurtas objektas, lygus originalui.

Pateikiame pavyzdį, kaip naudoti `__repr__` metodą, kad apibrėžtumėte nuosavo objekto, pavadinto `Person`, atvaizdavimą eilutėje:

```python3
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

p = Person("John", 30)
print(p) # Person('John', 30)
print(repr(p)) # Person('John', 30)

```
Gera praktika klasėse įgyvendinti ir `__str__` metodą, kuris naudojamas patogiai objekto eilutės reprezentacijai grąžinti, pavyzdžiui, kai iškviečiama `spausdinti()` funkcija.

### `__eq__` : 

`__eq__` naudojamas lygybės operatoriaus `==` elgsenai apibrėžti pasirinktiniam objektui. Jis iškviečiamas, kai operatorius `==` naudojamas dviem tos pačios klasės objektams **lyginti**, ir turėtų grąžinti `True`, jei objektai lygūs, arba `False`, jei jie nelygūs.

Štai pavyzdys, kaip naudoti `__eq__` metodą su ta pačia `Person` klase:


```python3
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def __eq__(self, other: 'Person') -> bool:
        if isinstance(other, Person):
            return self.name == other.name and self.age == other.age
        return False

p1 = Person("John", 30)
p2 = Person("John", 30)
p3 = Person("Jane", 25)

print(p1 == p2) # True
print(p1 == p3) # False

```
Svarbu pažymėti, kad lyginant pasirinktinius objektus taip pat patartina įgyvendinti `__ne__` metodą, kuris **grąžina priešingą** `__eq__` metodo rezultatą. Jis iškviečiamas, kai naudojamas `!=` operatorius, tai padeda išlaikyti nuoseklią palyginimo operatorių elgseną.

### `__add__` :

Funkcija `__add__` naudojama norint apibrėžti papildymo operatoriaus `+` elgesį su pasirinktiniu objektu. Jis iškviečiamas, kai `+` operatorius naudojamas **sudėti du tos pačios klasės objektus**, ir turėtų grąžinti naują objektą, **atspindintį pridėjimo rezultatą**.

Pateikiame pavyzdį, kaip naudoti `__add__`` metodą, kad apibrėžtumėte pasirinktinio objekto, vadinamo `Vector`, papildymą:

```python
class Vector:
    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y

    def __add__(self, other: 'Vector') -> 'Vector':
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        raise TypeError("unsupported operand type(s) for +: 'Vector' and '{}'".format(type(other).__name__))

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2
print(v3.x, v3.y) # 4 6

```
Svarbu pažymėti, kad pridedant pasirinktinius objektus taip pat patartina įgyvendinti `__radd__` metodą, kuris leidžia užtikrinti sudėties operacijos komutatyvumą. Šis metodas kviečiamas, kai kai kairysis operandas yra **kitos klasės** objektas, o dešinysis operandas yra klasės, įgyvendinančios `__add__` metodą, egzempliorius:

```python3
class Vector:
    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y

    def __add__(self, other: 'Vector') -> 'Vector':
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        raise TypeError("unsupported operand type(s) for +: 'Vector' and '{}'".format(type(other).__name__))
    
    def __radd__(self, other: 'Vector') -> 'Vector':
        return self.__add__(other)

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2
print(v3.x, v3.y) # 4 6
v4 = 2 + v1
print(v4.x, v4.y) # 3 4

```
#### `__len__` :

Funkcija `__len__` naudojama norint apibrėžti integruotos funkcijos `len()` elgesį su pasirinktiniu objektu. Ji **turėtų grąžinti sveikąjį skaičių**, reiškiantį objekto elementų skaičių.

Pateikiame pavyzdį, kaip naudoti `__len__` metodą, kad apibrėžtumėte pasirinktinio objekto, pavadinto `MyList`, ilgį:

```python
class MyList:
    def __init__(self, items: list):
        self.items = items

    def __len__(self) -> int:
        return len(self.items)

ml = MyList([1, 2, 3, 4, 5])
print(len(ml)) # 5

```

Verta paminėti, kad `__len__` metodas **visada turi grąžinti neneigiamą sveiką skaičių**, jei jis grąžina neigiamą arba neintegralinę reikšmę, bus iškelta `TypeError` klaida.

### `__bool__` :

Funkcija `__bool__` naudojama apibrėžti integruotos funkcijos `bool()` elgesį ir pasirinktinio objekto _boolean reikšmę. **Ji turėtų grąžinti True, jei objektas laikomas "teisingu", ir False, jei jis yra "klaidingas "**.

Pateikiame pavyzdį, kaip naudoti `__bool__` metodą pasirinktinio objekto, vadinamo `MyNumber`, `buolea`n vertei apibrėžti:

```python
class MyNumber:
    def __init__(self, num: int):
        self.num = num

    def __bool__(self):
        return bool(self.num)

mn = MyNumber(5)
print(bool(mn)) # True
mn2 = MyNumber(0)
print(bool(mn2)) # False

```
Verta paminėti, kad jei `__bool__` metodas neapibrėžtas, "Python" objekto `buolean reikšmei` nustatyti naudos `__len__` metodą. Jei `__len__` **grąžina 0**, objektas laikomas `False`, priešingu atveju - `True`.

```python
class MyNumber:
    def __init__(self, num: int):
        self.num = num

    def __bool__(self):
        return bool(self.num)
    
    def __len__(self) -> int:
        return 1

mn = MyNumber(5)
print(bool(mn)) # True
mn2 = MyNumber(0)
print(bool(mn2)) # False
print(len(mn)) # 1

```

### `__getitem__` :

Funkcija `__getitem__` naudojama apibrėžti, kaip elgtis su pasirinktinio objekto kvadratinių skliaustų užrašu `[]`. Jis iškviečiamas, kai `kvadratiniai skliaustai []` naudojami **prieigai prie objekto elemento ir turėtų grąžinti elementą nurodytu indeksu arba raktu**.

Toliau pateikiamas pavyzdys, kaip naudoti `__getitem__` metodą, kad apibrėžtumėte pasirinktinio objekto, pavadinto `MyDict`, prieigą prie elemento:

```python
class MyDict:
    def __init__(self, data: dict):
        self.data = data

    def __getitem__(self, key: str):
        return self.data[key]

md = MyDict({'a':1, 'b':2})
print(md['a']) # 1

```

Verta paminėti, kad jei `__getitem__` metodas sukelia `KeyError` klaidą, kai **raktas objekte neegzistuoja**, verta įgyvendinti `__missing__` metodą klasėje, kuri paveldi iš integruotos `dict` klasės. Šį metodą `dict` klasė iškviečia, **kai žodyne nerandamas raktas, ir turėtų grąžinti numatytąją rakto reikšmę**.

```python3
class MyDict(dict):
    def __missing__(self, key: str):
        return 'default'
    
md = MyDict({'a':1, 'b':2})
print(md['a']) # 1
print(md['c']) # default

```

## Pratimai: 
🧠 : Pakartokite [OOP 2 dalis](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* **Užduotis Nr.1**:
  
  Sukurkite klasę `Product`, kuri kaip parametrus priima `pavadinimą` ir `kainą` bei turi apibrėžtus `__str__` ir `__repr__` metodus.

  - Metodas `__str__` turėtų grąžinti eilutę formatu "Product: name, Price: price".
  - Metodas `__repr__` turėtų grąžinti eilutę formatu "Product('name', price)".
  

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-2) 

* **Užduotis Nr.2**:

  Sukurkite klasę pavadinimu `MyQueue`, kurioje apibrėžti `__bool__`, `__repr__` ir `__len__` metodai.

  - Metodas `__bool__` turėtų grąžinti `True`, jei eilėje yra elementų, ir `False`, jei ji yra tuščia.
  - Metodas `__repr__` turėtų grąžinti eilutę formatu `MyQueue(items)`, kur items yra eilės elementų sąrašas.
  - Metodas `__len__` turėtų grąžinti eilėje esančių elementų skaičių.

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2-1)

* **Užduotis Nr.3**:

  Sukurti klasę `Knyga`, kuri kaip parametrus priima `pavadinimą`, `autorių` ir `ISBN`. Klasė turėtų turėti `__bool__`, `__repr__`, `__len__`, 
  `__str__`, `__eq__`, `__add__` ir `__getitem__` metodus.

  - Metodas `__bool__` turėtų grąžinti True, jei knyga turi pavadinimą, priešingu atveju - False.
  - Metodas `__repr__` turėtų grąžinti eilutę formatu "Book(title, author, ISBN)", kur title, author ir ISBN yra atitinkami atributai 
    klasės atributai
  - Metodas `__len__` turėtų grąžinti knygos puslapių skaičių
  - Metodas `__str__` turėtų grąžinti eilutę formatu "title by author (ISBN)".
  - Metodas `__eq__` turėtų palyginti dvi knygas ir grąžinti True, jei abiejų ISBN sutampa, ir False priešingu atveju.
  - Metodas `__add__` turėtų pridėti dvi knygas ir grąžinti naują knygos objektą, kuriame būtų sujungtas abiejų knygų turinys ir naujos knygos pavadinimas. 
    knygos pavadinimas turėtų būti pirmosios knygos pavadinimas
  - Metodas `__getitem__` turėtų grąžinti knygos pavadinimą, jei perduotas indeksas yra 0, ir knygos autorių, jei perduotas indeksas yra 1.

  [Atsakymas](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3) 

* **Užduotis Nr.4**: 

  Sukurkite tris skirtingas užduotis su realaus pasaulio scenarijumi, kurios apimtų visus šiandien nagrinėtus magiškus metodus ir dar 3 kitus iš pateikto [sąrašo](https://docs.python.org/3/reference/datamodel.html). 

## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Pilnas OOP kursas - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (keli vaizdo įrašai)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [Corey Schafer: Magiški metodai](https://www.youtube.com/watch?v=3ohzBxoFHAY)
* [DataCamp](https://www.datacamp.com/tutorial/introducing-python-magic-methods)

***




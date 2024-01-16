## `Įvadas`
Python kalboje `generatorius` yra specialus `iterable` tipas, **kuriantis reikšmių seką po vieną**. Priešingai nei `list`, **kuris atmintyje saugo visas reikšmes iš karto**, generatoriai taupiau naudoja atmintį**, nes jie grąžina tik tas `vertes`, kurių iš tikrųjų reikia**. Tai gali būti naudinga didelėms arba begalinėms duomenų sekoms.

`Generatoriai` sukuriami naudojant `yield` teiginį. Teiginys `yield` yra panašus į teiginį `return`, tačiau vietoj to **sustabdo funkcijos vykdymą ir grąžina reikšmę**. Kitą kartą iškvietus funkciją, jos vykdymas tęsiamas **nuo tos vietos**, kur ji buvo nutraukta.

### `Apžvalga`
Generatoriai yra `iterable` tipas, kaip ir `listai` ar `tuples`. Jie **nelaiko savo turinio atmintyje**, o kiekvieną reikšmę generuoja "iteravbimo metu".

Paprasta generatoriaus išraiška: 

```python
from typing import Generator

def simple_generator(n: int) -> Generator[int, None, None]:
    for i in range(n):
        yield i

# Usage
for value in simple_generator(5):
    print(value)
```
Begalinių skaičių generatorius:

```python
from typing import Generator

def infinite_range(start: int = 0) -> Generator[int, None, None]:
    current = start
    while True:
        yield current
        current += 1

# Usage
counter = 0
for value in infinite_range(10):
    print(value)
    counter += 1
    if counter == 5:
        break
```
Kitas pavyzdys:

```python
def count_up_to(x: int) -> Generator[int, None, None]:
    count = 1
    while count <= x:
        yield count
        count += 1

for number in count_up_to(5):
    print(number)
# 1
# 2
# 3
# 4
# 5
```

Pirmiau pateiktame pavyzdyje `count_up_to` yra `generatorius`, kuris sukuria skaičius iki tam tikro duoto dėmens. Raktažodis `yield` naudojamas norint sukurti `vertę` ir sustabdyti generatoriaus vykdymą.

Python `typing` modulyje `Generator` tipas naudojamas `Generator` funkcijoms anotuoti. Štai `Generator` apibrėžimas `typing` modulyje:

```python
typing.Generator[ValueType, SendType, ReturnType]
```

 - `ValueType`: Tipas: generatoriaus generuojamų verčių tipas (`yield` išraiškos).
 - `SendType`: Tipas reikšmių, kurias galima siųsti į generatorių naudojant `generator.send(value)` metodą. Tai neprivaloma ir numatytoji reikšmė yra 
   `None`.
 - `ReturnType`: Generatoriaus grąžinamos reikšmės tipas, kai generatorius baigia veikti (`iššaukia "StopIteration"`). Neprivalomas ir numatytasis 
    reikšmuo yra `None`.

### `yield`

Pythone `yield` naudojamas `generatoriui` apibrėžti. Jis veikia kaip standartinis raktažodis `return`. Tačiau jis **grąžina generatorių**.

```python
def generator():
    yield 1
    yield 2
    yield 3

for value in generator():
    print(value)
# 1
# 2
# 3
```
Pirmiau pateiktame pavyzdyje generatoriaus funkcija `generator()` grąžina `generatoriaus objektą`. Galite `iteruoti` per `generatoriaus objektą` naudodami `for` ciklą.

### `Generatoriaus išraiškos`
Kaip galite sukurti `list comprehension`, taip galite sukurti ir `gereneratorines išraiškas`. Jos yra efektyvesnės už `list comprehension` ir gali taupyti atmintį, jei gaunamas `list` bus **didelis**, nes jos generuoja kiekvieną reikšmę, o ne saugo jas sąraše.

```python
numbers = (x for x in range(10))

for number in numbers:
    print(number)
# 0
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
```
Pirmiau pateiktame pavyzdyje numbers yra `generatorius`, kuris generuoja skaičius nuo `0` iki `9`. Tai yra efektyvesnis atminties naudojimas nei šių skaičių `list` kūrimas.

## Pratimai: 🧠
1) Parašykite Python programą, kuri sukurtų generatorių, generuojantį skaičių `kvadratus` iki duoto skaičiaus.
2) Parašykite Python programą, kad sukurtumėte generatorių, kuris gautų "n" atsitiktinių skaičių, esančių tarp `mažo` ir `didelio` skaičiaus, kurie yra `programos įvestys`.
3) Parašykite Python programą, kad sukurtumėte generatorių, kuris iteruoja `string`.
4) Parašykite Python programą, kuri sukurtų `Fibonačio` eilučių generatorių.
5) Parašykite Python programą, kuri sukurtų generatorių iš `list`, kuris duoda elementą iš `list`, jei jis yra `int`.
6) Sukurkite `sąrašą`, sudarytą iš `tuples`, kurių kiekvienas atspindi informaciją apie asmenį. Kiekviename `tuple` yra tokia informacija: (name: str, 
   age: int, city: str, wage: float). Jūsų užduotis - sukurti Python generatorius, kurie atliktų šias užduotis:

   - Filtravimo generatorius: Sukurkite generatoriaus funkciją, kuri filtruoja žmones, kurių amžius nesiekia tam tikros ribos.
   - Atvaizdavimo generatorius: Sukurkite generatoriaus funkciją, kuri atvaizduoja žmonių vardus į didžiąsias raides.
   - Agregavimo generatorius: Sukurkite generatoriaus funkciją, kuri apskaičiuoja pasirinktos grupės vidutinį atlyginimą.


## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Real Phyton](https://realpython.com/introduction-to-python-generators/)
* [Youtube](https://www.youtube.com/watch?v=bD05uGo_sVI&ab_channel=CoreySchafer)
***

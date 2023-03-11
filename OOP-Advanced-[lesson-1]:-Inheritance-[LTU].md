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
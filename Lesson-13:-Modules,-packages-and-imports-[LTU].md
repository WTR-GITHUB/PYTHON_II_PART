## Įvadas
Kol mokotės programuoti Python kalba, gali būti prasminga visą kodą rašyti Python integruotoje kūrimo ir mokymosi aplinkoje (IDLE). Po kurio laiko tai tampa nepraktiška. Natūraliausia iš ten pradėti kurti savo "Python" šaltinio failus, kurie naudojami kodui išsaugoti - "Python" šaltinio failai saugomi su plėtiniu .py.

Šiuose šaltinio failuose galite apibrėžti įvairias funkcijas, klases ir kitus objektus, taip pat tiksliai nurodyti, ką norite, kad programa darytų paleidus kodą. Kadangi failas yra išsaugotas, jums nereikia iš naujo rašyti kodo kiekvieną kartą, kai norite pateikti kokius nors nurodymus "Python" interpretuotojui: tiesiog paleidžiate anksčiau parašytą scenarijų.

Tačiau saugoti visą kodą viename šaltinio faile yra nepraktiška, kai pradedate kurti sudėtingesnes programas. Stebėti visas funkcijas ir klases bei tai, kaip kodai dera tarpusavyje, darosi vis sudėtingiau, nes programos sudėtingumas didėja. Net ir turintieji geriausią atmintį gali prisiminti tik tiek daug, todėl turime kurti programas taip, kad mums būtų lengviau gyventi.
Štai čia į pagalbą ateina **_modulinis programavimas_**.

#### Modulinio programavimo pristatymas
Python programuotojai naudoja modulinį programavimą įvairioms programoms kurti. Modulinis programavimas - tai tiesiog programų struktūrizavimo būdas, kai didėja jų sudėtingumas. Jame daugiausia dėmesio skiriama didelių užduočių skaidymui į mažus subuždavinius, kuriuos lengviau valdyti.

Mažesnių užduočių sujungimas sudaro programą; "Python" programoje kiekvieną atskirą užduotį vadiname moduliu, kuris iš tikrųjų yra bendras terminas, reiškiantis pakartotinai naudojamą kodą. Moduliai saugomi su plėtiniu .py ir importuojami į įvairias kitas programas.

Kai turime kelis modulius, jų rinkinys vadinamas paketu. Paketą galima įsivaizduoti kaip aplanką, kuriame yra moduliai ir galbūt kiti aplankai, kuriuose yra moduliai [ir t. t.]. Taigi paketas yra tiesiog pavadinimas, naudojamas visiems jame esantiems moduliams susieti, kad ateityje galėtume į jį atsiremti, kai norėsime tą kodą naudoti kitoje programoje.

Kai kurie modulinio programavimo privalumai:
* Kai savo programas suskirstome į modulius, galime sutelkti dėmesį į mažesnes didesnės problemos dalis. Tai reiškia, kad galime daugiau dėmesio skirti tam, kad įsitikintume, jog mūsų parašytas kodas veikia, prieš integruodami jį į didesnę programą. Kitaip tariant, rašydami modulinį kodą galime rašyti išsamesnius ir griežtesnius testus, kad patikrintume funkcionalumą, kuris atlieka mažiau funkcijų.
Be to, kodą kur kas lengviau sekti ir skaityti, kai jis suskirstytas į dalis, susijusias su konkrečiomis funkcionalumo dalimis. Jei vietoj to naudotume monolitinį kodą, rasti konkrečias dalis taptų vis sudėtingiau, nes didėjant rašomų eilučių skaičiui - mažiau kalbėti apie failo dydį.

* **Prižiūrimumas** - Dideles programas paprastai kuria keli programuotojai, kurie sutelkia savo įgūdžius; kai kiekvienas modulis yra vienintelis jo funkcionalumo tiesos šaltinis, sumažėja klaidų, galinčių atsirasti programoje, skaičius. Taip yra todėl, kad, kai savo kode aptiksime klaidą arba kai reikės atnaujinti tam tikrą funkcionalumo dalį, pakeitimus reikės atlikti tik modulio lygmeniu, o ne visoje programoje - atsižvelgiant į tai, kad patikrinome tarpusavio patikimumo kriterijus.
Taip ne tik lengviau pastebėti ir greitai ištaisyti šias klaidas, bet ir skatinamas komandų bendradarbiavimas. Pavyzdžiui, atsakomybė už konkrečius modulius gali būti paskirta įvairiems komandos nariams, ir nors vis tiek būtume sunerimę, yra daugiau pasitikėjimo, kad mūsų atliekami pakeitimai ar atnaujinimai nesugadins visos sistemos.

* **Pakartotinis panaudojamumas** - pagrindinė esmė ta, kad kurdami programinę įrangą dažnai pakartotinai naudojame kodą. Užuot kopijavus ir klijavus šį kodą, geresnis sprendimas yra reikiamą kodą pritraukti iš vieno šaltinio, o tai mums leidžia daryti moduliavimas.

## Moduliai

### Sukurti

Modulio kūrimas python kalba yra panašus į paprasto python scenarijaus rašymą naudojant `.py` plėtinį. Toliau pateiktame pavyzdyje pabandykime sukurti modulį įvairioms operacijoms atlikti:

```python
def add(x: int,y: int) -> int:
     return x + y
 
def sub(x: int,y: int) -> int:
     return x - y
 
def prod(x: int,y: int) -> int:
    return x * y
 
def div(x: int,y: int) -> int:
    return x // y
```
Išsaugokite pirmiau pateiktą kodą faile `calc.py` (galite jį pavadinti kaip norite). _Taip mes sukuriame modulį pythone_. Šiame modulyje sukūrėme įvairias funkcijas. Šiuos modulius galime naudoti savo pagrindiniame faile.

### Paprastai
Naudosime raktinį žodį **import**, kad modulį įtrauktume į savo programą, iš raktinis žodis naudojamas norint iš modulio gauti tik kelis arba tam tikrus metodus ar funkcijas. Pažiūrėkime, kokie yra skirtingi modulio naudojimo jūsų programoje būdai. Tarkime, kad turime savo failą, kurio pavadinimas main.py :
```python
import calc as calculator
a = 10
b = 20
 
addition = calculator.add(a,b)
print(addition)

# Output: 30
```

Pirmiau pateiktame kode sukūrėme slapyvardį naudodami raktinį žodį **as**. Pirmiau pateikto kodo išvestis bus dviejų skaičių a ir b sudėtis, naudojant **calc.py** modulio add funkcijoje nurodytą logiką.

Pažvelkime į kitą metodą. Toliau pateiktame kode **importavome visas funkcijas** naudodami žvaigždutę, o norėdami gauti rezultatus, galime tiesiog paminėti funkcijos pavadinimą.

```python
from calc import *
a = 20
b = 30
 
print(add(a,b))

# Output: 50
```

#### Python modulio kelias
Kai importuojame modulį, interpreteris ieško modulio sys.path esančiuose modulių kataloguose ir, jei neranda, ieško modulio tokia tvarka:


```python
import sys 
print(sys.path)
```
Paleidę pirmiau pateiktą kodą, gausite katalogų sąrašą. Sąraše galite atlikti pakeitimus ir sukurti savo kelią.

Įdiegti moduliai parašyti C kalba ir integruoti su Python interpreteriu. Kiekviename integruotajame modulyje yra išteklių, skirtų tam tikroms specifinėms funkcijoms, pavyzdžiui, operacinės sistemos valdymui, disko įvesties ir (arba) išvesties funkcijoms ir t. t.

Standartinėje bibliotekoje taip pat yra daugybė python skriptų, kuriuose yra naudingų pagalbinių programų. Mūsų žinioje yra keletas integruotų python modulių, kuriais galime naudotis, kai tik norime.

Norėdami gauti visų python modulių sąrašą, python konsolėje galite parašyti šią komandą:


```python
help('modules')
```

## `# `if __name__ == "__main__"` magic
Daugeliu praktinių atvejų galite manyti, kad sąlyginis blokas, kurį atidarote su `if __name__ == "__main__"`, yra būdas saugoti kodą, kuris turėtų būti vykdomas tik tada, kai jūsų failas vykdomas kaip skriptas.

Pavyzdys:

```python
# echo.py

def echo(text: str, repetitions: int = 3) -> str:
    """Imitate a real-world echo."""
    echoed_text = ""
    for i in range(repetitions, 0, -1):
        echoed_text += f"{text[-i:]}\n"
    return f"{echoed_text.lower()}."


if __name__ == "__main__":

    text = input("Yell something at a mountain: ")
    print(echo(text))
```
Šiame pavyzdyje apibrėžiama funkcija echo(), kuri imituoja realų aidą, palaipsniui spausdindama vis mažiau paskutinių įvesties teksto raidžių.
Kai paleidžiate failą kaip skriptą, perduodami failo objektą "Python" interpretatoriui, išraiška `__name__ == "__main__"` grąžina `True`. Tuomet paleidžiamas kodo blokas po if, todėl "Python" surenka naudotojo įvestį ir iškviečia `echo()`.

**Pamirškite:**
Kodo įterpimas po `if __name__ == "__main__"` leidžia patenkinti skirtingus naudojimo atvejus:
 * Skriptas: Vykdomas kaip scenarijus, jūsų kodas paprašo naudotojo įvesti duomenis, iškviečia echo() ir išspausdina rezultatą.
 * Modulis: Kai importuojate "echo" kaip modulį, tada apibrėžiama funkcija echo(), bet kodas nevykdomas. Pagrindiniam kodo seansui suteikiate echo() be 
   jokių šalutinių poveikio.

## Pratimai: 

* Sukurkite paprastą skaičiavimo programą kaip skriptą ir kaip modulį.
* Sukurkite programą su 3 skirtingais moduliais: 
  - Pirma, atlikti pagrindines užduotis su eilutėmis
  - antra, pagrindinius uždavinius su sąrašais.
  - trečias, pagrindiniai uždaviniai su skaičiais

  Importuokite juos kaip modulius į `main.py` modulį ir parodykite skaičiavimus.

* Sukurkite modulį ir importuokite bet kurį pasirinktą PIP paketą. Tada sukurkite funkciją, kuri jį naudotų.
  Importuokite tą funkciją į `main.py` modulį ir ją naudokite.

## 🌐 Papildomas skaitymas (arba žiūrėjimas 📺 ):

* [Python Official](https://docs.python.org/3/tutorial/modules.html)
* [Medium](https://medium.com/python-features/understanding-if-name-main-in-python-a37a3d4ab0c3)

***
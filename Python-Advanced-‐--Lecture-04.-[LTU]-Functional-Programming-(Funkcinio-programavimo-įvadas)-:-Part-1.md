## `Įvadas`

Kompiuterių moksle funkcinis programavimas - tai **programavimo paradigma, kai programos kuriamos taikant ir sudarant funkcijas**. Tai deklaratyvioji programavimo paradigma, kurioje funkcijų apibrėžtys yra išraiškų medžiai, atvaizduojantys reikšmes į kitas reikšmes, o ne imperatyvinių teiginių seka, atnaujinanti programos veikimo būseną.

Šiame skyriuje daugiau dėmesio skirsime kai kurioms python programavimo kalbos jau pateiktoms funkcijoms, kurios šiek tiek palengvina mūsų gyvenimą. Dalykai, kuriuos čia aptarsime, taip pat naudingi ir **OOP paradigmoms**. 

Python kalboje apskritai viskas yra **`objektas`**, taigi funkcijos taip pat to išvengia. Funkcijoms galima priskirti kitus vardus ir pan.

### `Apžvalga`

`Funkcinis programavimas` apskritai nesaugo jokios programos būsenos. Daugiausia funkcijos negali žinoti ir keisti jokių `globalų`. 
`Funkcinis programavimas` atliekamas pagal tam tikras taisykles:
- Naudojame grynąsias (idempotentines) funkcijas.
- Neprieiname prie globalių būsenos kintamųjų ir jų nekeičiame
- Jokiomis aplinkybėmis negali keistis funkcijos rezultatai, jei pateikiami tie patys įėjimai

**PASTABA** ❗Funkcinio programavimo funkcijos neturi jokio šalutinio poveikio. Tai reiškia, kad jas taikydami nieko neįrašome į atmintį, tiesiog atvaizduojame įvestį į išvestį.

### `sorted funkcija`

Šią funkciją jau matėme kurso pradžioje.

````python
gyvūnai = ["šeškas", "pelėda", "šuo", "gekonas"]
sorted(animals)
# ["šuo", "šeškas", "gekonas", "pelėda"]
```

Tai jau matėme, tačiau `sorted` funkcijos [dokumentacijoje](https://docs.python.org/3/library/functions.html#sorted) rašoma, kad į funkciją gali būti perduodamas dar vienas parametras - `key`. _`key` nurodo vieno argumento funkciją, kuri naudojama iš kiekvieno `iterable` elemento išgauti palyginimo raktą (pavyzdžiui, `key=str.lower`). Numatytoji reikšmė yra `None` (lyginkite elementus tiesiogiai).

Taigi, šis rakto parametras priima palyginamąjį sąrašą ir tada bando surūšiuoti mūsų duomenis pagal jį:

```python
gyvūnai = ["šeškas", "pelėda", "šuo", "gekonas"]
sorted(animals, key=len)
# ['dog', 'vole', 'gecko', 'šeškas']
```

#### `Lambda funkcijos`


Jau turėjome įvadą į `lambdas` [čia](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-11:-Functions-(-Part-2-))
Funkcinio programavimo esmė - funkcijų iškvietimas ir jų perdavimas, todėl natūralu, kad reikia apibrėžti daug funkcijų. Visada galite apibrėžti funkciją įprastu būdu, naudodami raktinį žodį [def](https://realpython.com/defining-your-own-python-function/#function-calls-and-definition), kaip matėte ankstesnėse šio ciklo pamokose.

Tačiau kartais patogu, kai anoniminę funkciją galima apibrėžti tiesiog eigoje, nesuteikiant jai vardo. Pythone tai galite padaryti naudodami lambda išraišką:
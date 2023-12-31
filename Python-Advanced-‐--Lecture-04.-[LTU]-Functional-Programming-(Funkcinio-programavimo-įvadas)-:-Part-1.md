## `Įvadas`

Kompiuterių moksle funkcinis programavimas - tai **programavimo paradigma, kai programos kuriamos taikant ir sudarant funkcijas**. Tai deklaratyvioji programavimo paradigma, kurioje funkcijų apibrėžtys yra išraiškų medžiai, atvaizduojantys reikšmes į kitas reikšmes, o ne imperatyvinių teiginių seka, atnaujinanti programos veikimo būseną.

Šiame skyriuje daugiau dėmesio skirsime kai kurioms python programavimo kalbos jau pateiktoms funkcijoms, kurios šiek tiek palengvina mūsų gyvenimą. Dalykai, kuriuos čia aptarsime, taip pat naudingi ir **OOP paradigmoms**. 

Python kalboje apskritai viskas yra **`objektas`**, taigi funkcijos taip pat to išvengia. Funkcijoms galima priskirti kitus vardus ir pan.

## `# `Apžvalga`

`Funkcinis programavimas` apskritai nesaugo jokios programos būsenos. Daugiausia funkcijos negali žinoti ir keisti jokių `globalų`. 
`Funkcinis programavimas` atliekamas pagal tam tikras taisykles:
- Naudojame grynąsias (idempotentines) funkcijas.
- Neprieiname prie globalių būsenos kintamųjų ir jų nekeičiame
- Jokiomis aplinkybėmis negali keistis funkcijos rezultatai, jei pateikiami tie patys įėjimai

**PASTABA** ❗funkcinio programavimo funkcijos neturi jokio šalutinio poveikio. Tai reiškia, kad jas taikydami nieko neįrašome į atmintį, tiesiog atvaizduojame įvestį į išvestį.
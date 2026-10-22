# Budi pasaulių nuotykiai

Mažas naršyklinis žaidimas pagal „Budi“ novelės pasaulį. Veikėjai nupiešti ranka braižyto eskizo stiliumi (languotas sąsiuvinio popierius, kiaušinio formos kūnai su spiraline akimi), o kiekvienoje scenoje reikia surasti ir paspausti paslėptus paveiksliukus, kad surinktum žvaigždučių.

Tekstas ir pasaulis: [Novelė](https://marcobonety.blogspot.com/p/novele.html).

## Kaip paleisti

Projektas yra vienas failas, jokio diegimo ar surinkimo nereikia.

1. Atsisiųsk `budi-zaidimas.html`.
2. Atidaryk jį naršyklėje (dukart spustelėk failą).

Jei nori patalpinti internete, pervadink failą į `index.html` ir įkelk į bet kurią statinių puslapių talpyklą (pavyzdžiui, GitHub Pages).

> Šriftas „Architects Daughter“ kraunamas iš Google Fonts. Be interneto žaidimas veiks, bet rašysena bus pakeista atsarginiu šriftu.

## Kaip žaisti

- Viršuje pasirink vieną iš penkių pasaulių: **Askezis**, **Bokštas**, **Krautuvėlė**, **Marsas**, **Viešbutis**.
- Spausk ant scenos objektų ir veikėjų. Kiekvienas naujas paspaudimas duoda 5 žvaigždutes.
- Kai surandi visus scenos objektus, atsiranda ✅ prie jos pavadinimo ir atsidaro mygtukas **Toliau**.
- Baigus paskutinę sceną rodomas sveikinimo langas su galutiniu rezultatu.
- **Iš naujo** nuresetina visą pažangą.

| Scena | Surandamų objektų |
|---|---|
| Askezis | 4 |
| Bokštas | 3 |
| Krautuvėlė | 4 |
| Marsas | 4 |
| Viešbutis | 3 |

Iš viso 18 objektų ir 90 žvaigždučių.

## Ekranai

Išdėstymas pritaikytas taip, kad viskas tilptų į langą be slinkimo:

- **Stačias telefonas:** pavadinimas ir taškai viršuje, skirtukai, scena per visą likusį plotą, apačioje aprašymas ir mygtukai.
- **Kompiuteris ir gulsčias telefonas:** scena kairėje, valdymo skydelis dešinėje.

Scena yra SVG su `viewBox="0 0 800 450"`, todėl automatiškai prisitaiko prie laisvos vietos išlaikydama proporcijas.

## Projekto sandara

Viskas yra viename HTML faile ir susideda iš trijų dalių:

| Dalis | Paskirtis |
|---|---|
| `<style>` | Išdėstymas, spalvų kintamieji (šviesi ir tamsi tema), animacijos |
| Veikėjų generatorius | Funkcija `ch(...)` nupiešia veikėją pagal parametrus iš `K` |
| Scenos ir žaidimo logika | Masyvas `S` (scenos), `T` (aprašymai), `HINTS` (kiek objektų reikia surasti) |

### Veikėjai

Veikėjai apibrėžti objekte `K`:

```js
const K = {
  V:  { w: 92,  h: 150, f: 'hood' },    // Vauris
  B:  { w: 122, h: 118, f: 'apron' },   // Bauderis
  G:  { w: 80,  h: 165, f: 'hat' },     // Garletas P.
  I:  { w: 84,  h: 160, f: 'hair' },    // Ilis / Wau Ku
  Pi: { w: 76,  h: 112, f: 'ant' },     // Pijus
  A:  { w: 78,  h: 135, f: 'glasses' }, // Aja
  Bp: { w: 132, h: 130, f: 'ears' },    // Bioprimatas
  X:  { w: 70,  h: 105, f: 'ant' }      // Praeivis
};
```

`w` ir `h` yra kūno plotis ir aukštis, `f` yra skiriamasis ženklas iš objekto `F` (gobtuvas, prijuostė, skrybėlė ir t. t.).

Veikėjo įdėjimas į sceną:

```js
ch(K.V, x, y, mastelis, { walk: 1, mv: [pastūmimas, trukmė] })
```

### Nauja scena

1. Į masyvą `S` pridėk funkciją, kuri grąžina SVG eilutę.
2. Paspaudžiamus objektus apgaubk funkcija `clk('unikalus-id', turinys, [x, y, plotis, aukštis])`.
3. Į `N` įrašyk skirtuko pavadinimą, į `T` aprašymą, į `HINTS` paspaudžiamų objektų sąrašą.
4. Pakeisk `currentScene<4` sąlygas pagal naują scenų skaičių (ten, kur tikrinama, ar tai paskutinė scena).

### Spalvos ir tema

Spalvos laikomos CSS kintamuosiuose (`--paper`, `--ink`, `--blue`, `--red`, `--green`, `--gold`). Tamsi tema įsijungia pagal sistemos nustatymą, o `data-theme="light"` ar `data-theme="dark"` ant `:root` ją užfiksuoja rankiniu būdu.

## Prieinamumas

- Skirtukai yra tikri mygtukai, pasiekiami klaviatūra su matomu fokusu.
- Gerbiamas `prefers-reduced-motion`: animacijos išjungiamos.
- Palaikomi telefonų saugūs plotai (`safe-area-inset`).

## Žinomi apribojimai

- Scenų objektai paspaudžiami pelės ar prisilietimo, bet ne klaviatūra.
- Veikėjai rodomi tik iš priekio ir į šoną nesisuka.
- Mygtukas **Iš naujo** naudoja naršyklės `confirm()` langą.
- Pažanga neišsaugoma, perkrovus puslapį žaidimas prasideda iš naujo.

## Idėjos tolesniam darbui

- Profilio projekcijos veikėjams, kad jie sektų judėjimo kryptį.
- Garsai ir muzika kiekvienam pasauliui.
- Pažangos išsaugojimas naršyklėje.
- Papildomi veikėjai: Garletas P. ir Ilis / Wau Ku Marso administracijos scenoje.

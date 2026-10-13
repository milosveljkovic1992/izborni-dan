# Izborni dan

Krovna stranica za seriju edukativnih igara o izborima u Srbiji. Prikazuje četiri igre kao kartice. Klik na karticu otvara igru na njenoj adresi.

| Igra | Uloga | Adresa | Folder u repozitorijumu |
|---|---|---|---|
| Kontrolor | član biračkog odbora | https://kontrolor.netlify.app/ | `bir/` |
| Posmatrač | posmatrač | https://posmatrac.netlify.app/ | `pos/` |
| Mobilni tim | mobilni tim posmatrača | https://mobilni-tim.netlify.app/ | `mob/` |
| Glasač | glasač | https://glasac.netlify.app/ | `birac/` |

Krovna stranica je na https://izborni-dan.netlify.app/. Svaka igra ima link „← Sve igre“ koji vodi nazad na nju.

## Struktura projekta

```
index.html     krovna stranica (HTML i CSS u jednom fajlu, bez JavaScript-a)
og-image.png   slika za deljenje na društvenim mrežama (1200 × 630)
igre/          slike kartica, kopije `og-image.png` iz svake igre
netlify.toml   podešavanja za Netlify (objava i bezbednosna zaglavlja)
CHANGELOG.md   spisak izmena po verzijama
README.md      ovaj fajl
```

Nema zavisnosti ni build koraka. Jedini spoljni resursi su fontovi sa Google Fonts (Bitter, Source Serif 4, IBM Plex Mono).

## Slike kartica

Kartice koriste iste slike koje igre koriste za deljenje. Slike su kopirane u folder `igre/`, jer bezbednosna pravila u `netlify.toml` dozvoljavaju samo slike sa iste adrese. Kad se promeni `og-image.png` neke igre, kopiraj ga i ovde:

```sh
cp ../bir/og-image.png   igre/kontrolor.png
cp ../pos/og-image.png   igre/posmatrac.png
cp ../mob/og-image.png   igre/mobilni-tim.png
cp ../birac/og-image.png igre/glasac.png
```

## Lokalno pokretanje

```sh
python3 -m http.server 8000
```

pa otvori http://localhost:8000. Linkovi na kartice vode na objavljene igre.

## Objava na Netlify

Svih pet sajtova (krovna stranica i četiri igre) mogu da se objavljuju iz istog Git repozitorijuma. Za svaki sajt na Netlify u **Site configuration → Build & deploy** postavi **Base directory** na njegov folder (`izborni-dan`, `bir`, `pos`, `mob`, `birac`). Build command ostaje prazan, a publish directory je `.`, kao u `netlify.toml`.

Bez Git-a: prevuci folder `izborni-dan` na https://app.netlify.com/drop.

## Dodavanje nove igre

1. Dodaj novi `<li class="game …">` u listu `.games` u `index.html`, po uzoru na postojeće.
2. Za boju igre dodaj token u `:root` (svetla tema) i u oba tamna bloka, kao i klasu koja postavlja `--accent`.
3. Kopiraj `og-image.png` igre u `igre/`.
4. U samu igru dodaj link „← Sve igre“ ka https://izborni-dan.netlify.app/.

## Verzionisanje

Verzija je upisana u `<meta name="version">` u `index.html` i prati ista pravila kao igre (`GLAVNI.SPOREDNI.ISPRAVKA`). Izmene se beleže u `CHANGELOG.md`.

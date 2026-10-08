# Resultats de la competició Gaia Climb

Landing estàtica en valencià que mostra el rànquing i les estadístiques de les participacions guardades en Google Sheets pel formulari de Gaia Climb.

## Funcionament

- La web consulta la lectura pública de Google Apps Script; el full de càlcul continua sent privat.
- La resposta conté l’identificador, el nom, el gènere, 17 blocs, el total i la data. No conté correus.
- Cada bloc val `0`, `Zona` (10 punts) o `Top` (25 punts), amb un màxim de 425.
- El rànquing general inclou totes les participacions. Les categories Femení i Masculí utilitzen el valor exacte de `genero`.
- Els empats compartixen posició amb numeració densa: `1, 2, 2, 3`.
- Les persones amb zero punts apareixen al rànquing i compten en el total i en la mitjana.
- El gràfic mostra les zones sense top i els tops en cinc pàgines de blocs: `4 + 4 + 4 + 4 + 1`.

No hi ha dependències ni procés de compilació.

## Configuració

Desplega primer `google-apps-script.gs` seguint el README del projecte `FormulariCompeGaia`. Després copia la mateixa URL pública acabada en `/exec` al principi de `script.js`:

```js
const GOOGLE_APPS_SCRIPT_URL = 'https://script.google.com/macros/s/IDENTIFICADOR/exec';
```

Pots comprovar la resposta pública en el navegador:

```text
URL_DE_APPS_SCRIPT?action=resultats
```

El JSON ha de tindre `ok: true` i una propietat `resultats`. No ha d’incloure mai `correo`.

## Prova local

Des de la carpeta del projecte:

```sh
python3 -m http.server 8000
```

Obri `http://localhost:8000` i comprova:

- Càrrega correcta, estat sense resultats, error de xarxa i botó «Torna-ho a provar».
- Rànquing general, Femení i Masculí; empats, noms llargs, zeros i més de cinc participants.
- Mitjana i total de participants.
- Recompte de zones i tops en les cinc pàgines del gràfic.
- Navegació amb teclat i amplada mínima de 320 px.

## Publicació

Publica `index.html`, `styles.css`, `script.js` i `Gaia.svg` en GitHub Pages mitjançant **Settings → Pages → Deploy from a branch**. Després de cada canvi, espera que acabe el desplegament i recarrega sense memòria cau.

# Padawan VUE-CLI helper
- BOOTSTRAP: come installo bootstrap?
- AXIOS: come installo axios?
- ICONE: come installo fontawesome?
- FONTS: come installo fontsource?


Dopo aver creato un nuovo progetto vue. Entra nella cartella del progetto e da terminale digita i vari comandi.

## BOOTSTRAP 

Digita nel terminale 
```
npm i bootstrap
```

Aggiungi al file main.js 

```js
/* Bootstrap */
const bootstrap = require('bootstrap')
Vue.use(bootstrap)
```

Crea un file assets/scss/style.scss e importa il sass di bootstrap

```scss
@import '~/node_modules/bootstrap/scss/bootstrap.scss';
```

🥳 Ora puoi usare bootstrap, i suoi componenti e le sue classi utility etc.



## AXIOS

Da terminale, nella cartella del progetto digita
```
npm i axios
```

Per usare axios e fare le chiamate ajax in un file `.vue` dove vuoi fare il v-for per mostrare i risultati, importa axios dentro al tag script (prima di export default)

```html
<script>
import axios from "axios";

export default {
}
</script>
```

## ICONE

Installa fontawesome

```
npm i --save @fortawesome/fontawesome-svg-core
npm i --save @fortawesome/free-solid-svg-icons
npm i --save @fortawesome/free-regular-svg-icons
npm i --save @fortawesome/vue-fontawesome@latest
```

nel file main.js importa i vari moduli dalla riga 3 in poi.

```js
import Vue from 'vue'
import App from './App.vue'

/* Font Awesome icons*/
/* import the fontawesome core */
import { library } from '@fortawesome/fontawesome-svg-core'

/* import specific icons 👇 QUI AGGIUNGI LE ICONE che vuoi usare in camelCase */
import { faUserSecret, faMagnifyingGlass } from '@fortawesome/free-solid-svg-icons'

/* import font awesome icon component */
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

/* add icons to the library 👇 QUI AGGIUNGI IL NOME DELL'ICONA in camelCase*/
library.add(faUserSecret, faMagnifyingGlass) 

/* add font awesome icon component */
Vue.component('font-awesome-icon', FontAwesomeIcon)
```

Ora puoi usare le icone (solo quelle che hai importato sopra) nel tuo markup
```html
<font-awesome-icon icon="fa-solid fa-magnifying-glass" />
```


## FONTS

Scegli sul sito il font che vuoi usare e installalo con npm. 
Ad esempio, open-sans

```bash
npm install @fontsource/poppins
```

Nel file main.js importa il font e i vari pesi che vuoi usare

```js
import "@fontsource/poppins"
import "@fontsource/poppins/100.css"
import "@fontsource/poppins/500.css"
import "@fontsource/poppins/900.css"
```

Ricordati di settare il font-family 

```css
font-family: 'Poppins', sans-serif;
```

🥳 Fatto, ora Lavora!
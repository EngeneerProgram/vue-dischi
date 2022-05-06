# 705 Vue CLI - $emit, Computed propertis, Vue Observable

- $EMIT: Child components events with $emit
- COMPUTED: Computed properties
- OBSERVABLE: Vue.Observable a simple global state management


## $emit: crea eventi personalizzati
Il metodo speciale `$emit()` permette la creazione di un evento personalizzato che possiamo emettere 
da un componente. Nel componente genitore in cui poi importeremo ed useremo questo componente potremo ascoltare per l'emissione di questo evento personalizzato.

In questo modo possiamo anche passare dei dati al genitore durante l'emissione dell'evento personalizzato. 

Questo é ok se i componenti sono padre e figlio.

Immagina un componente, un form con un input text e un bottone.
Al click del bottone, il form emette un evento che viene intercettato dal genitore e usato per eseguire una funzione di ricerca.

```html
<!-- SearchBox.vue -->
<form class="d-flex" @submit.prevent="$emit('formSubmit')">
    <input
      class="form-control me-2"
      type="search"
      placeholder="Search"
      aria-label="Search"
      :value="searchText"
      @input="$emit('input', $event.target.value)"
      @keyup="$emit('formSubmit', searchText)"

    />
    <button
      class="btn btn-outline-success d-flex align-items-center"
      type="submit"
      :disabled="searchText < 1"
    >
      <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
      Search
    </button>
  </form>
```
Nel codice qui sopra, il form quando viene inviato non esegue una funzione direttamente, ma emette un evento personalizzato che abbiamo chiamato `formSubmit` ma poteva chiamarsi anche `babyYoda`. Quando questo evento viene emesso, insieme all'evento possiamo passare anche un valore come secondo parametro della funzione $emit come vedremo nei due $emit successivi.

C'é un'altra cosa da puntualizzare nel codice qui sopra. Il searchBox ha un input al suo interno. Per poter usare il v-model direttamente sul componente SearchBox quando poi verrá usato, bisogna registrare una props che in questo esempio ho chiamato `searchText` e usare la rirettiva `v-bind` sull'attributo html `value`, poi si emette un evento usando la direttiva `v-on` sull'evento della dom `input` con `@input="$emit('input', $event.target.value)"` Qui, tramite la proprietá speciale `$event` é possibile recuperare il valore digitato nell'input tramite `$event.target.value` e passarlo all'emit come secondo parametro.

Il componente finale sará il seguente:

```vue
<template>
  <form class="d-flex" @submit.prevent="$emit('formSubmit')">
    <input
      class="form-control me-2"
      type="search"
      placeholder="Search"
      aria-label="Search"
      :value="searchText"
      @input="$emit('input', $event.target.value)"
      @keyup="$emit('formSubmit', searchText)"

    />
    <button
      class="btn btn-outline-success d-flex align-items-center"
      type="submit"
      :disabled="searchText < 1"
    >
      <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
      Search
    </button>
  </form>
</template>

<script>
export default {
    name:"SearchBox",
    props: {
        searchText: String,
    }
};
</script>

<style>
</style>

```

Ora usiamo questo componente nel markup di SiteHeader.
```html
<header>
<SearchBox v-model="searchText" @formSubmit="search" />
</header>
```
Nel codice qui sopra abbiamo usato la direttiva v-on con un evento personalizzato emesso dal componente SearchBox e la direttiva v-model="" bindata alla proprietá searchText poi definita nella funzione data del SiteHeader component.

```js
data() {
    return {
      searchText: "",
    };
  },
```

il metodo search invocato dal `formSubmit`
```js
methods: {
    search() {
      console.log('Searching ...');
    },
  },
```
## Observable
Se i componenti che devono passarsi dati non sono padre e figlio, il problema é un pó piú complesso. In applicazioni sofisticate si utilizzano librerie di state management come ad esempio Vuex. Nel nostro caso, trattandosi di un applicazione semplicissima é possibile utilizzare il metodo `.observable` come descritto nella 
documentazione Vue. Questo metodo, parte della global api, é quello che dietro le quinte permette a vue di monitorare il cambiamento dei dati dentro `data` e di notificare eventuali componenti che i dati sono appunto stati mutati.

Nell'applicazione Ricky and Morty, abbiamo inserito il searchBox dentro al componente SiteHeader, mentre i dati dei personaggi sono nel componente `CharactersListComponent`. Questo ci rende difficile e poco pratico l'utilizzo di emit, visto che i due componenti non sono padre e figlio. É quindi un ottimo use case per l'observable.

### Creiamo un file per la gestione dello state a livello globale
In src, creiamo un file che chiameremo state.js
Per poter usare observable bisogna importare la classe Vue all'inizio del file, poi possiamo creare una nuova costante  che chiameremo `state` e la esporteremo usando un default export. 

```js
/* src/state.js */
// Importa Vue
import Vue from 'vue'
// crea un oggetto usando .observable
const state = Vue.observable({
    searchText: ''
})
// esporta lo state
export default state
```
Nello state abbiamo subito inserito una proprietá che vogliamo usare e monitorare da dentro il componente `SiteHeader.vue` e che muteremo assegnandole il valore che l'utente inserisce nell'input del componente `SearchBox.vue`.

Il nostro state ora é un modulo che bisognerá importare quando vogliamo leggere/scrivere i suoi valori.

Nel componente SiteHeader.vue ora importiamo lo state

```js
/* src/components/SiteHeader.vue */
import state from "@/state.js";

```
e aggiorniamo il metodo `search()` in modo che possa editare lo state

```js
/* src/components/SiteHeader.vue */
search() {
      //console.log('Searching ...');
      state.searchText = this.searchText;
      //console.log(state.searchText);
    },
```
Abilitando il console log, possiamo vedere che lo state viene aggiornato nonappena l'utente digita nell'input qualcosa. 

Ecco la sezione script dell SiteHeader.vue component completa.
```js
import state from "@/state.js";
import SearchBox from "@/components/SearchBox";
export default {
  name: "SiteHeader",
  components: {
    SearchBox,
  },
  data() {
    return {
      searchText: "",
    };
  },
  methods: {
    search() {
      //console.log('Searching ...');
      state.searchText = this.searchText;
      //console.log(state.searchText);
    },
  },
};

```
Adesso grazie allo state condiviso a livello globale possiamo filtrare i risultati mostrati usando le computed properties.

## Computed
Le computed properties sono dei metodi che restituiscono dei dati modificandone la presentazione. Questi metodi vengono cashati (salvati in memoria) e rieseguiti solo se i dati che manipolano vengono aggiornati. Tramite una proprietá computata non si alterano i dati, ma si modifica la loro presentazione. Se l'obbiettivo del metodo é modificare i dati, allora si deve utilizzare un metodo e non una compoted property.

Immagina di avere un'array di oggetti da filtrare. Nella computed property, non modificheremo l'array originale, ma ne creeremo una copia, la filtreremo in base a delle condizioni e poi, la restituiremo. 

Questa operazione, verrá eseguita una volta e poi cashata in memoria e rieseguita solo se l'array originale cambia per qualsiasi motivo.

Creiamo una computed property dentro `CharactersListComponent.vue`. 

```js

computed: {
    filtered(){
    }
  }


```
`computed` é una proprietá che definiamo nell'istanza del componente e alla quale assegniamo un oggetto. In questo oggetto scriviamo le nostre funzione che devono sempre restituire un valore.
Nel codice qui sopra abbiamo create `filtered(){}` questo metodo dovrá filtrare i dati presenti nel componente sotto la proprietá `characters` e restituircene una copia filtrata in base alla proprietá `searchText` del nostro state globale.

Prima di tutto importiamo il modulo state nel tag script del componente `CharactersListComponent.vue`
```js
/* CharactersListComponent.vue */
import state from "@/state.js";
```
ora che abbiamo accesso all'oggetto reattivo state possiamo usarlo per filtrare l'array `characters` nella computed property creata poco fá `filtered`

```js
filtered(){
    // Verifichiamo se state.searchText non é vuoto e se si filtriamo l'array facendone una copia con filter e restituendola
      if(state.searchText) {
        // applicando filter all'array stiamo generando una nuova array
        return this.characters.filter(character => {
            // ora usiamo state.searchText per filtrare i dati
          return character.name.toLowerCase().includes(state.searchText.toLowerCase())
        })
        
      } 
      /* Se lo state.searchText é vuoto restituiamo l'array originale */
      else {
        return this.characters
      }
    }
```
Nel codice qui sopra, abbiamo usato `array.filter()` per filtrare l'array `this.characters`, poiché filter restituisce una nuova array, usando il return la restituiamo dalla computed propery e non manipoliamo direttamente l'array originale. Dentro alla callback di filter prendiamo il singolo elemento dell'array `character` e selezioniamo la proprietá `name` con la dot notation, verifichiamo se questa include il testo presente nella proprietá `searchText` dello state globale (state.js) e se si la resituiamo cosí filter aggiungerá l'elemento alla nuova array. 
Nell'else gestiamo il caso in cui nel searchText non ci sia nulla e quindi restituiamo l'array originale.

Ora possiamo usare questa computed property al posto di `characters` nel template sostituendo il valore nel ciclo for `v-for="character in filtered"`

```html

 <!-- usa la direttiva v-if per verificare se la ricerca ha prodotto almeno 1 risultato -->
<div class="row g-3" v-if="filtered.length > 0">
    <Character
    :character="character"
    v-for="character in filtered"
    :key="character.id"
    />
</div>
<!-- Se la ricerca non ha prodotto risultati mostra messaggio e pulsante per refreshare la pagina  -->
<div class="text-center" v-else>
    <p>Nothing to show</p>
    <a href="" class="btn btn-outline-primary">Reset Search</a>
</div>

```

Qui sotto alcuni link di riferimento per approfondire.

## Link di riferimento
- Emit [here](https://v2.vuejs.org/v2/guide/components.html#Listening-to-Child-Components-Events)
- Usare v-model su un componente [here](https://v2.vuejs.org/v2/guide/components.html#Using-v-model-on-Components)
- Computed Properties [here](https://v2.vuejs.org/v2/guide/computed.html)
- Observable [here](https://v2.vuejs.org/v2/api/#Vue-observable)
- Articolo su Observable [here](https://betterprogramming.pub/how-to-manage-vues-state-with-vue-observable-25988a88938b)

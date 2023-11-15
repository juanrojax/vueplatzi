# vueplatzi
Repositorio de Vue.js con Platzi

Fundado por Evan You

### FUNDAMENTOS COMPONENTES
Desarrollo basado en componentes: la intención es abstraer las partes del software, pueden ser encapsulados o aislados que interactúan entre sí a través de una interfaz. 
COMPONENTES UI: módulos o pedazos de un todo (html, css js) en una misma interfaz.
Partes de un componente: La vista; Estado(el estado interno del componentes ej: un botón habilitado o deshabilitado); Interfaz (es la forma en que el resto del sistema interactúa con el componente ej: eventos onlick).
Patrón MVVM: Ayudar a separar cómo definimos la interfaz y cómo programamos la lógica de negocio. 
![image](https://github.com/juanrojax/vueplatzi/assets/43138305/6cafffa2-91e8-4ed2-a086-fb7883005616)

Two-way data binding: permite sincronizar la vista con el modelo de una forma muy transparente.

### **Iniciar con vue:**
```html
<div id="app">{{ text }}</div>
<script>
    const vm = Vue.createApp({
        data(){
            return {
                text: "Hola men"
            };
        }
    }).mount("#app");
</script>
```
### INTERPOLACIÓN DE DATOS
La interpolación de datos hace referencia a la forma como se trabaja con variables dentro de los componentes Vue. Estas variables utilizan la sintaxis de doble llave {{ text }}
Las directivas son tags de HTML que permiten que los valores de las etiquetas en el DOM cambien. dinámicamente. ejemplos son:

v-text=‘text’ : añade texto al elemento html o componente, este escucha cambios en la variable text. Ejemplo:
```javascript
template: `<div v-text='text'>{{ text }}</div>`
```
v-once : permite que no se modifique el valor de un elemento, guarda el valor con el que se renderiza la primera vez.Ejemplo:
```javascript
template: `<div v-once v-text='text'>{{ text }}</div>`
```
v-html: permite no solo introducir texto en una cadena válida sino HTML.Ejemplo:
```javascript
const vm = Vue.createApp({
            data(){
                return {
                    text: "<p>Hola men</p>"
                };
            },
            template: `<div v-html='text'></div>`
        }).mount("#app");
```
Directivas en Vue: https://vuejs.org/api/built-in-directives.html

### ATRIBUTOS REACTIVOS
La directiva v-bind permite modificar los atributos.de forma dinamica ejemplo:
```javascript
const vm = Vue.createApp({
            data(){
                return {
                   img: "https://logos.flamingtext.com/Word-Logos/cualquier-cosa-design-china-name.png"
                };
            },
            template: `<img  v-bind:src="img" v-bind:alt="img">`
        }).mount("#app");
```
Los atributos después de Vue.js 3 se pueden cambiar a variables, por ejemplo un atributo como lo es src se puede cambiar para usarlo con una variable, ejemplo:
```javascript
data(){
                return {
                    attr: "src",
                    img: "https://logos.flamingtext.com/Word-Logos/cualquier-cosa-design-china-name.png"
                };
            },

template: `<img  v-bind:[attr]="img" v-bind:alt="img">`
```

### EVENTOS DE USUARIO
Existe una directiva para detectar eventos del usuario como lo es v-on, v-on escucha los eventos de DOM y ejecuta JavaScript cuando se activa
Por ejemplo:
```javascript
const vm = Vue.createApp({
            data(){
                return {
                    counter: 0
                };
            },
            methods:{
                increment(){
                    console.log("CLick")
                }
            },
            template: `<button v-on:click="increment">{{counter}}</button>`
        }).mount("#app");
```

v-on tiene una serie de eventos que se puede utilizar como clic, aqui una lista de eventos: https://es.vuejs.org/v2/guide/events
Dentro de v-on también existen los modificadores de eventos como por ejemplo la necesidad de utilizar un preventDefault para que el formulario no se recargue se puede utilizar esto:
```html
<!-- El evento de enviar ya no volverá a cargar la página. -->
    <form v-on:submit.prevent="onSubmit"></form>
```
Aqui hay un listado de los modificadores de eventos: https://es.vuejs.org/v2/guide/events#Modificadores-de-eventos

### INPUTS REACTIVOS
Es una forma de ver cómo vue.js se encarga de sincronizar la vista con el modelo de una forma sencilla.
Ejemplo:
```javascript
const vm = Vue.createApp({
    data(){
        return {
            text: "HOLA MEN"
        };
    },
    methods:{
        input(e){
            this.text = e.target.value;
        }
    },
    template: `<p>{{text}}</p>
        <input type="text" v-on:change="input" v-bind:value="text">
    `
}).mount("#app");
```

v-on y v-bind permiten usarse con alias, ejemplo:
```html
<input type="text" @:change="input":value="text">
```
Atributos -> :
Eventos -> @
Otra forma de escribir menos código es combinar dos directivas en una como lo es v-model
Ejemplo:
```html
<input type="text" v-model="text">
```

### PROPRIEDADES COMPUTADAS
Son características de vue que permiten transformar o realizar cálculos sobre nuestros datos y luego reutilizar fácilmente el resultado como una variable en nuestro template o data. La ventaja que tienen las propiedades computadas es que son reactivas.
Ejemplo:
```javascript
const vm = Vue.createApp({
    data() {
        return {
            firstName: "Juan",
            lastName: "Rojas",
            now: new Date()
        };
    },
    computed: {
        fullName() {
            return this.firstName + " " + this.lastName;
        },
        today() {
            return this.now.toLocaleDateString();
        }
    },
    template: `
    <div>{{ fullName }}</div>
    <div>{{ today }}</div>
    `
}).mount("#app");
```
### WATCHERS
En ocasiones solo quieres escuchar cambios y empezar actuar sobre el, para que un watcher funcione la función definida enel watch debe tener el mismo nombre que la variable:
Ejemplo:
```javascript
const vm = Vue.createApp({
    data(){
        return {
            text: "Hola men"
        };
    },
    watch: {
        text(value,old){
            console.log("wath",value,old);
        }
    },
    template: `{{ text }}`
}).mount("#app");
```
```javascript
const vm = Vue.createApp({
    data(){
        return {
            text: "Puerta cerrada",
            open: false
        };
    },
    computed:{
        label(){
            return this.open ? "Cerra":"Abrir"
        }
    },
    watch: {
        open(value){
            if (value) {
                this.text = "Puerta abierta"
            }else{
                this.text = "Puerta cerrada"
            }
        }
    },
    template: `<div>{{ text }}</div>
        <button @click="open=!open">{{ label }}</button>`
}).mount("#app");
```
### ESTILOS REACTIVOS
Existen dos directivas para lograr estilos reactivos con vue.js que son style y class.
Ejemplo usando :style
```html
<style>
    .closed {
        background-color: #eca1a6;
    }
    .open {
        background-color: #b5e7a0;
    }
</style>
```
```javascript
const vm = Vue.createApp({
    data(){
        return {
            text: "Puerta cerrada",
            open: false,
            styles: {
                backgroundColor: "#eca1a6"
            }
        };
    },
    computed:{
        label(){
            return this.open ? "Cerra":"Abrir"
        }
    },
    watch: {
        open(value){
            if (value) {
                this.text = "Puerta abierta";
                this.styles.backgroundColor= "#b5e7a0"
            }else{
                this.text = "Puerta cerrada"
                this.styles.backgroundColor= "#eca1a6"
            }
        }
    },
    template: `<div class="container" :style="styles">
            <h2>{{ text }}</h2>
            <button @click="open=!open">{{ label }}</button>
        </div>
        `
}).mount("#app");
```
Ejemplo usando :class
```javascript
const vm = Vue.createApp({
    data(){
        return {
            text: "Puerta cerrada",
            open: false
        };
    },
    computed:{
        label(){
            return this.open ? "Cerra":"Abrir"
        },
        styles(){
            return this.open ? ['open']:['closed']
        }
    },
    watch: {
        open(value){
            if (value) {
                this.text = "Puerta abierta";
            }else{
                this.text = "Puerta cerrada"
            }
        }
    },
    template: `<div class="container" :class="styles">
            <h2>{{ text }}</h2>
            <button @click="open=!open">{{ label }}</button>
        </div>
        `
}).mount("#app");
```

### CONDICIONALES
También se pueden utilizar condicionales dentro de los template, dentro de los componentes, para eso vue.js nos da v-if y v-else
Ejemplo:
```javascript
const vm = Vue.createApp({
    data(){
        return {
            text: "Sesión cerrada",
            open: false,
            username:""
        };
    },
    computed:{
        label(){
            return this.open ? "Cerra":"Abrir"
        },
        styles(){
            return this.open ? ['open']:['closed']
        }
    },
    watch: {
        open(value){
            if (value) {
                this.text = "Cierra sesión";
            }else{
                this.text = "Abre sesión";
                this.username = ""
            }
        }
    },
    template: `<div class="container" :class="styles">
            <h2>{{ text }}</h2>
            <div v-if="open">
                <p>Hola, {{ username }}</p>    
            </div>
            <div v-else>
                <label>Username</label>
                <input type="text" v-model="username"/>
            </div>
            <button @click="open=!open">
                <div v-if="!open">Acceder</div>
                <div v-else>Salir</div>
            </button>
        </div>
        `
}).mount("#app");
```

### LISTAS
Otra de las funcionalidades esenciales de Vue.js es la posibilidad de mapear o imprimir arrays de elementos con la directiva v-for y mostrarlo en forma de listas.
La directiva v-for requiere de una sintaxis específica para recorrer un array item in items, lo que viene a ser cada elemento del conjunto de elementos
EJEMPLO:
```javascript
const vm = Vue.createApp({
    data(){
        return {
            text: "Sesión cerrada",
            open: false,
            username:"",
            posts: [
                {
                title: "Titulo 1",
                description: "Descripción UNO"
                },
                {
                title: "Titulo 2",
                description: "Descripción DOS"
                },
                {
                title: "Titulo 3",
                description: "Descripción TRES"
                }
            ]
        };
    },
    computed:{
        label(){
            return this.open ? "Cerra":"Abrir"
        },
        styles(){
            return this.open ? ['open']:['closed']
        }
    },
    watch: {
        open(value){
            if (value) {
                this.text = "Cierra sesión";
            }else{
                this.text = "Abre sesión";
                this.username = ""
            }
        }
    },
    template: `<div class="container" :class="styles">
            <h2>{{ text }}</h2>
            <div v-if="open">
                <p>Hola, {{ username }}</p>
                <div class="list">
                    <div v-for="item in posts" class="item">
                        <div  class="tittle">{{item.title}}</div>
                        <p>{{item.description}}</p>
                    </div>
                </div>
            </div>
            <div v-else>
                <div>Username</div>
                <input type="text" v-model="username"/>
            </div>
            <button @click="open=!open">
                <div v-if="!open">Acceder</div>
                <div v-else>Salir</div>
            </button>
        </div>
        `
}).mount("#app");
```

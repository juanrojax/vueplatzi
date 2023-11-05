# vueplatzi
Repositorio de Vue.js con Platzi

Fundado por Evan You

FUNDAMENTOS COMPONENTES
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
INTERPOLACIÓN DE DATOS
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

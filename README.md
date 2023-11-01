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
```
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

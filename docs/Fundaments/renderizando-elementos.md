# Renderizando elementos

Un elemento describe lo que se quiere ver en pantalla.

A diferencia de los elementos del DOM de los navegadores, los elemntos de React son objetos planos, y su creación es de bajo costo.

En alguna parte del HTML

~~~html
<div id="root"></div>
~~~

Lo anterior es un nodo raiz porque todo lo que esté dentro de el será manejado por React.

Las app creadas por React usualmente tienen un unico nodo raiz en el DOM.

Para renderizar un elementos se usa:

~~~js
const element = <h1>Hello, world</h1>;
const root = ReactDom.createRoot(
  document.getElementById('root')
);
root.render(element);
~~~

## Actualizando el elemento renderizado

Los elementos de React son inmutable, una vez creas un elemento, no puedes cambiar sus hijos o atributos.

En estos momentos la unica forma de actualizar la intrfaz de usuario es creando un nuevo elemento y pasarlo al root.render().

~~~js
const root = ReactDOM.createRoot(
  document.getElementById('root')
);

function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
~~~

El codigo anterio va actualizando el DOM cada segundo.

[Regresar al index](../README.md)

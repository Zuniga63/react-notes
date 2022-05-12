# Presentando JSX

~~~js
const element = <h1>Hello, word </h1>;
~~~

React acepta el hecho de que la logica de renderizado está intrinsecamente unida a la lógica de la interfaz de usuario.

En lugar se separar artificialmente tecnologías poniendo el maquetado y la lógica en archivos diferentes, React separa intereses con unidades ligeramente acopladas llamadas “componentes” que contienen ambas.

## Insertando expresiones en JSX

~~~js
const name = 'Josh Perez';
const element = <h1>Hello, {name} </h1>;
~~~

Se pueden poner cualquier expresión de javaScript dentro de llaves en JSX.

~~~js
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez',
}

const element = (
  <h1>
    Hello, { formatName(user) }
  </h1>
);
~~~

## JSX tambien es una expresión

~~~js
function getGreeting(user) {
  if(user){
    return <h1>Hello, {formatName(user)}</h1>
  }
  return <h1>Hello, Stranger.</h1>
}
~~~

JSX se puede usar dentro de delcaraciones **if**, **for**, asignarlo a variables, aceptarlo como argumento, y retornarlo desde dentro funciones.

## Especificando atributos con JSX

Se puede utilizar comillas para especificar strings literales o llaves para insertar una expsión javaScript en un atributo.

~~~js
const link = <a href="https://www.reactjs.org">Link</a>

-o-

const avatar = <img src={user.avatarUrl} />;
~~~

**Nota:** No se debe poner comillas dobles rodeando una expresión javaScript en un atributo. No deben ir ambas en el mismo atributo.

**Advertencia**: React Dom usa la convención de nomenclatura *camelCase* en vez de nombres de atributos HTML. Por ejemplo *class* se vuelve `className` y *tabindex* se vuelve `tabIndex`.

## Especificando hijos

~~~js
const element = <img src={user.avatarUrl} />;

const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
~~~

## JSX previne ataques de inyección

Por defecto, ReactDom escapa cualquier valor insertado en JSX antes de renderizarlo.

## JSX representa objetos

Los iguientes ejemplos son identicos

~~~js
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
~~~

~~~js
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
~~~

y son representados de la siguiente forma

~~~js
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
~~~

[Regresar al index](../README.md)

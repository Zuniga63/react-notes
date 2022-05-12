# Componente y propiedades

Los componentes permiten separar la interfaz de usuario en piezas mas independientes, reutilizables y pensar en cada pieza de forma aislada.

Conceptualmente los componetes son como las funciones en JavaScript. Aceptan entradas arbitrarias y retornan elementos de React que describen lo que debe aparecer en la pantalla.

## Componentes duncionales y de clase

- Funcionales

~~~js
function Wellcome(props){
  return <h1>Hello, {props.name}</h1>
}
~~~

- De clase

~~~js
class Wellcome extends React.Component{
  render(){
    return <h1>Hello, {this.props.name}</h1>
  }
}
~~~

Los dos componentes anteriores son equivalentes para React.

## Renderizando un componente

Los componentes pueden renderizar un elemento del DOM

~~~js
const element = <div />
~~~

sin embargo tambien se puede representar componentes definidos por el usuario.

~~~js
const element = <Wellcome name="Sara"/>
~~~

Ejemplo:

~~~js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(element);
~~~

1. Llamamos a root.render() con el elemento `<Welcome name="Sara" />`.
2. React llama al componente Welcome con `{name: 'Sara'}` como “props”.
3. Nuestro componente Welcome devuelve un elemento `<h1>Hello, Sara</h1>` como resultado.
4. React DOM actualiza eficientemente el DOM para que coincida con `<h1>Hello, Sara</h1>`.

## Composición

~~~js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}
~~~

## Extracción de componentes

Se considera el siguiente ejemplo

~~~js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
~~~

El componente anterior acepta *author* (objecto), *text* (string) y *date* (una fecha) como props.

- Se puede extraer el avatar en un componente individual

~~~js
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
~~~

El avatar no necesita saber que está siendo renderizado dentro de un comment. Es por eso que se cambia author por user.

Ahora el componente **comment** se puede simplicar un poco

~~~js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
~~~

- El componente anterior aun se puede refactorizar mas, creando un componente userInfo

~~~js
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}

//Lo que nos permite simplicar el comment

function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
~~~

***Nota***: Una buena regla en general, es que si una parte de la interfaz de usuario se usa varias veces, o es lo suficientemente compleja por si misma, es buen candidato para extraerse en un componente independiente.

## Los props son de solo lectura

Ya sea que declares un componente como función o como una clase, este nunca debe modificar sus props. Es pocas palabras ***Todos los componentes de React deben actuar como funciones puras respecto a sus props.***

[Regresar al Index](../../README.md)

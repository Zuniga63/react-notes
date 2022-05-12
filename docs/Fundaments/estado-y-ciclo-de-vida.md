# Estado y ciclo de vida

El estado de un componente es similar a las props, pero es privado y está completamente controlado por el componente.

## Convertir una función en una clase

Se puede comvertir un componente de función en una clase en cinco pasos:

1. Crear una clase ES6 con el mimo nombre que herede de `React.component`.
2. Agrega un unico metodo vacío llamado `render()`.
3. Mover el cuerpo de la función al metodo `render()`.
4. Reemplazar `props` con `this.props` en el cuerpo del render.
5. Borrar el resto de la función ya vacía.

El metodo render se invocará cada vez que ocurra una actualización; pero siempre y cuando renderizemos `<Clock />` en el mismo nodo del DOM, se usará solo una unica instancia de la clase Clock.

~~~js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
~~~

## Agregar estado local a una clase

1. Se añade un constructor de clase que signe el `this.estate` inicial.
2. Pasar las `props` al constructor base. Los componentes de clase siempre deben invocar al constructor base con props.

~~~js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Clock />);
~~~

## Agregar metodos de ciclo de vida a una clase

En aplicaciones con muchos componentes, es muy importante liberar recursos tomados por los mismos cuando se destruye.

Por ejemplo, un componente que quiera configurar un temporizador cada que se renderize por primera vez, esto se llama "montaje" en React.  
Tambien se quiere borrar ese temporizador cada vez el DOM producido por Clock se elimine.

~~~js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
  }

  componentWillUnmount() {
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
~~~

Estos metodos son llamados metodos de ciclo de vida.

Por ejemplo al montar el temporizador

~~~js
componentDidMount() {
  this.timerID = setInterval(() => this.tick(), 1000);
}
~~~

Si bien this.props es configurado por el mismo react y this.state tiene un significado especial, como desarrolladores somos libres de añadir campos adicionales a la clase manualmente si necesitas alamacenar algo que no participa en el flujo de dato.

## Usar el estado correctamente

Existen tres cosas que se deben saber sobre setState

### No modifiques el estado directamente

~~~js
// Incorrecto
this.state.comment = 'Hello';
~~~

En su lugar utilizar

~~~js
// Correcto
this.setState({comment: 'Hello'});
~~~

El unico lugar donde se puede asignar this.state es en el constructor.

### Las actualizaciones de estado puedens er asincronas

Debido a que `this.props` y `this.state` pueden actualizarse de forma asincrona, no debes confiar en sus valores para actualizar el siguiente estado.

El siguiente codigo puede fallar en actualizar elcontador

~~~js
// Incorrecto
this.setState({
  counter: this.state.counter + this.props.increment,
});
~~~

Para arreglarlo se utiliza una segunda forma de setState que recibe una función en lugar de un objeto. Dicha función recibe el estado previo como primer argumento y las props en el segundo argumento.

~~~js
// Correcto
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
~~~

Lo anterior se puede hacer de igual manera con funciones comunes.

### Las actualizaciones de estado se fusionan

Cuando se invoca `setState()`, React combina el objeto proporcionado con el estado actual.

~~~js
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }

  //Luego se puede actualizar de forma independiente

  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
~~~

[Regresar al Index](../../README.md)

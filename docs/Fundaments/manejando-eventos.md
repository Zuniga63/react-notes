# Manejando Eventos

- Los eventos de React se nombra usando camelCase, en lugar de minusculas.
- Con JSX pasas una función como el manejador de evento, en lugar de un string.

Ejemplo HTML

~~~html
<button onclick="activateLasers()">
  Activate Lasers
</button>
~~~

Ejemplo JSX

~~~js
<button onClick={activateLasers}>
  Activate Lasers
</button>
~~~

En React no puedes retornar false para prevenir un comportamiento por defecto.

- HTML

~~~html
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
~~~

- JSX

~~~js
function Form() {
  function handleSubmit(e) {
    e.preventDefault();
    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>
  );
}
~~~

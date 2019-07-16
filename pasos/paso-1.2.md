## Paso 1.2
Es este paso vamos a encargarnos de renderizar los dias 

Vamos definir el siguiente formato de dia
```js 
{day,month,year}
```

Bueno para hacer este check vamos a modificar el contexto ya existente del test, para enviarle los dias, pero primero hagamos una funcion auxiliar que nos crea dias, para mantener la consistencia entre todos los dias, y si por algun motivo cambia la estructura de los dias, no tenemos que tocar en todos lados.
```js
const createDate = (day,month,year) => ({day,month,year})
```

Vamos a identificar nuestros dias via id, entonces dentro de nuestra funcion setup vamos a definir un `getDate` que nos devuelva el elemento donde esta contenido un dia:
```js
getDate: (date) => wrapper.find(`#date-${date.day}-${date.month}-${date.year}`)
```

Ahora modifiquemos el contexto de nuestro anterior test para que tenga dias:

```js
const firstDate = createDate(20, 2, 2021)
const secondDate = createDate(26, 2, 2021)
const weeksValue = [
        [firstDate],
        [secondDate]
      ]
const { weeks, getDate } = setup({ weeks: weeksValue })
```

Nota: En general conviene tener el contexto en un `beforeEach` para asegurarnos de que los tests sean independientes entre sí, pero en este caso podemos dejarlo así porque sabemos que nuestro código no va a tener efecto de lado.

y agregamos un test para verificar que los dias se renderizen correctamente. 
En general tener 2 asserts en un mismo test es considerado una mala práctica, pero en este caso lo hacemos porque esos dos assertions comprenden lo que esperamos que pase cuando decimos que se 'renderizan los días'.
```js
it('render the dates', () => {
        expect(getDate(firstDate).text()).toEqual(firstDate.day.toString())
        expect(getDate(secondDate).text()).toEqual(secondDate.day.toString())
})
```      

Corremos los tests, vemos que falla.

Y ahora vamos a hacer el codigo para que este test pase!

```jsx
{weeks.map((week) => <tr className="date-picker__week">
          {week.map(({ day, month, year }) => <td id={`date-${day}-${month}-${year}`}>{day}</td>)}
</tr>)}
```

[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/ba9816ab0cace844eed4fea59325050960e442ad) podemos ver el codigo terminado de este paso

Excelente ya renderizamos los dias, ahora [hagamos que se puedan clickear](./paso-1.3.md)

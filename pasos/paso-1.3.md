## Paso 1.3
En este paso vamos a encargarnos de poder clickear un dia especifico

Para esto, el componente va a recibir por prop una funcion que llamaremos `onDateClicked`

En nuestros test vamos a usar un espia para saber si se llamo a esta prop, con la funcionalidad de jest `jest.fn()`

Entonce nuevamente deberiamos agregar este espia al contexto del test :

```js
const onDateClickedSpy = jest.fn()
const { weeks, getDate } = setup({ weeks: weeksValue, onDateCliked: onDateClickedSpy })
```

y agregamos el test correspodiente, donde en el hook beforeAll, hacemos que se clicke el dia que queremos :
```js
describe('when click a date', () => {
        beforeAll(() => {
          const dateToClick = getDate(firstDate)
          dateToClick.simulate('click')
        })
        it('call onDateClikedProp with the date', () => {
          expect(onDateClickedSpy).toBeCalledWith(firstDate)
        })
      })
```

Corremos los tests, vemos que falla, y escribinmos el codigo para hacerlo pasar:

```jsx
{week.map(
        (date) => {
        const { day, month, year } = date
        return <td id={`date-${day}-${month}-${year}`} onClick={() => onDateClicked(date)}>{day}</td>
        })
}
```


[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/69663d1b1178631be9d950bbfe0eadbe6814171d) podemos ver el codigo terminado de este paso


Excelente ya hicimos que se puedan clickear los dias, ahora [pongamos un boton de aplicar](./paso-1.4.md)


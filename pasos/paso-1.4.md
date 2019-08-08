## Paso 1.4
En este paso vamos a marcar un dia como seleccionado

Decidimos que nuestro componente va a entende por props que dia esta seleccionado mediante `selectedDate`

En la funcion setup agregaremos el selector del dia seleccionado :

```js
    selectedDateElement: wrapper.find('.date--selected')
```

y luego escribiremos nuestro test

```js
describe('when pass a selectedDate', () => {
    describe('and this day existing in the calendar', () => {
      const selectedDate = createDate(20, 4, 2021)
      const { selectedDateElement } = setup({
        weeks: [[selectedDate]],
        selectedDate
      })

      it('mark as selected', () => {
        expect(selectedDateElement.text()).toEqual(selectedDate.day.toString())
      })
    })
  });
```

El minimo codigo para hacer pasar este test, deberia ser agregar en algun lado de nuestro componente lo siguiente :

```jsx
<div className="date--selected">
          20
</div>
```

Perfecto, escribimos el codigo minimo para que nuestros test pasen !

Entonces escribamos el otro escenario, cuando el dia seleccionado no se encuentra en el calendario.

```js
describe('and this day doesnt existing in the calendar', () => {
      const { selectedDateElement } = setup({
        weeks: [[createDate(19, 3, 2090)]],
        selectedDate
      })

      it('doenst mark as selected', () => {
        expect(selectedDateElement).toHaveLength(0)
      })
})
```

Y escribiremos el codigo para que el test pase !

```jsx
const DatePicker = (props) => {
  const { weeks, onDateClicked, selectedDate } = props;
  return (
    <table>
      <tbody>
        {weeks.map((week) => <tr className="date-picker__week">
          {week.map(
            (date) => {
              const { day, month, year } = date
              let classNameDate = ""
              if (selectedDate && selectedDate.day === day
                && selectedDate.month === month
                && selectedDate.year === year
              ) {
                classNameDate = "date--selected"
              }
              return (
                <td id={`date-${day}-${month}-${year}`}
                  onClick={() => onDateClicked(date)}
                  className={classNameDate}
                >{day}</td>)
            })
          }
        </tr>)}
      </tbody>
    </table>
  );
}
```

Perfecto ahora nuestro componente entiende de dias seleccionados ! vayamos a [siguiente paso](./paso-1.5.md) donde agregaremos el boton de aplicar
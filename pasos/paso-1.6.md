## Paso 1.6
En este paso comenzaremos con nuestro componente `Calendar`

Deberiamos encontrar la manera de generar las fechas, yo recomiendo usar la lib `date-fns`

Pero por el momento hardcodemoslas, y hagamos la funcionalidad de seleccionar un dia.

```js
describe('Calendar', () => {
    describe('when select a date', () => {
        const { wrapper, datePicker } = setup();
        const selectedDate = createDate(20, 8, 2019)
        beforeAll(() => {
            datePicker.props().onDateClicked(selectedDate);
        })
        it('pass this selected date to the datePicker', () => {
            const datePickerWithSelectedDate = wrapper.find('DatePicker')
            expect(datePickerWithSelectedDate.props().selectedDate).toEqual(selectedDate)
        })
    })
})
```

Vemos que los tests falla e implementamos el codigo necesario :

```jsx
const Calendar = () => {
  const [selectedDate, setSelectedDate] = useState(null)
  const onDateClicked = (dateSelected) => {
    setSelectedDate(dateSelected)
  }
  return (
    <div>
      <DatePicker
        onDateClicked={onDateClicked}
        selectedDate={selectedDate}
      />
    </div>
  );
}
```

Genial nuestros tests dan verde !
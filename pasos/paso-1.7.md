## Paso 1.7
En este paso vamos a aplicar la seleccion

Vamos a escribir un test, en el cual chequeemos que al aplicar, se renderize el dia seleccionado en la pantalla

Para reutilizar contextos, usemos la fecha seleccionada de antes
```js
describe('when select a date', () => {
        const { wrapper, datePicker } = setup();
        const selectedDate = createDate(20, 8, 2019)
        let datePickerWithSelectedDate
        beforeAll(() => {
            datePicker.props().onDateClicked(selectedDate);
            datePickerWithSelectedDate = wrapper.find('DatePicker')
        })

        it('pass this selected date to the datePicker', () => {
            expect(datePickerWithSelectedDate.props().selectedDate).toEqual(selectedDate)
        })

        describe('and click on apply button', () => {

            beforeAll(() => {
                datePickerWithSelectedDate.props().onApply();
            })

            it('show the selected date', () => {
                const selectedDateElement = wrapper.find('.applied-date')
                expect(selectedDateElement.text()).toEqual("20/8/2019")
            })
        })
    })
```

Buenismo nuestros test fallan por varias razones !

Arreglemoslas !

```js
const Calendar = () => {
  const [selectedDate, setSelectedDate] = useState(null)
  const [appliedDate, setAppliedDate] = useState("")
  const onDateClicked = (dateSelected) => {
    setSelectedDate(dateSelected)
  }
  const onApply = () => {
    setAppliedDate(`${selectedDate.day}/${selectedDate.month}/${selectedDate.year}`)
  }
  return (
    <div>
      <DatePicker
        weeks={[[{ day: 20, month: 2, year: 2018 }], [
          { day: 28, month: 2, year: 2018 }
        ]]}
        onDateClicked={onDateClicked}
        selectedDate={selectedDate}
        onApply={onApply}
      />
      <div >
        El dia seleccionado es :
        <span className="applied-date">
          {appliedDate}
        </span>
      </div>
    </div>
  );
}
```

Perfecto ahora mostramos en pantalla el dia aplicado !
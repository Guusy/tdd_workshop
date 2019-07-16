## Paso 1.1
Renderizar las semanas que nos pasen via `props`
1) Comando para correr los tests
```
npm run test
```

### Partes del test
 
Para facilitar la lectura de los test, vamos a crear una funcion `setup`, que nos va a permitir instanciar el componente y devolvernos los selectores del mismo.
Ejemplo:

```js
const setup = (props) => {
   const wrapper = shallow(<DatePicker {...props}>)

   return {
     wrapper,
     weeks: wrapper.find('.date-picker__week'),
   }
}
```

De esta manera podemos hacer esto en nuestros tests:
```js
const { weeks } = setup({weeks:[VALOR DE LAS SEMANAS]})
```

Entonces... ahora deberiamos pensar cual es el formato en que queremos recibir las semanas. Para no quemarnos la cabeza propongo el siguiente:

```js
{
    weeks:[ // seria el mes la composicion de 4 semanas
        [ // esto es una semana (de length 7)
          1,2,3,4,5,6,7
        ],
        [
          8,9,10,11,12,13,14
        ],
        ...
    ]
}
    
```
Aca ya tomamos varias decisiones de diseño (vamos diseñando a medida que implementamos los tests).

2) Entonces vamos al file `DatePicker.spec.js` y escribimos el primer test

```js
describe('basic render', () => {
    describe('when pass weeks', () => {
      const weeksValue = [
        [],
        []
      ]
      const { weeks } = setup({ weeks: weeksValue })
      it('renders it', () => {
        expect(weeks).toHaveLength(2)
      });
    })
  })
```

Vemos que el test falla y vamos a escribir un poco de codigo como para que este test pase
Por temas de tiempo decidimos que el componente datePicker va renderizar en una tabla los dias y si bien deberiamos hacer test del renderizado de la tabla, por el momento vamos a saltearlo.

```jsx
 {
          props.weeks.map(() => <tr className="date-picker__week"></tr>)
 }
 ```

Una vez terminado esto, vamos a ver que los test siguen fallando ya que nuestro smoke test no tiene la propiedad `weeks`, para esto podemos agregar en las props default que tenemos arriba de la funcion setup la propiedad `weeks`.

[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/472ccc1c308b4890597ce7ae306a522b1c18d9de) podemos ver el codigo terminado de este paso

Excelente ya hicimos nuestro primer test, ahora [renderizemos los dias !](./paso-1.2.md)



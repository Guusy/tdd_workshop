## Paso 1.1
Es este paso vamos a encargarnos de crear renderizar las semanas que nos pasen via `props`
1) Run command test to watch it
```
npm run test
```

### Partes del test
 
Para facilitar la lectura de los test, creamos una funcion `setup` que se provee de devolvernos el componente (o diferentes partes del mismo) con las props que le pasemos + unas props default que le querramos declarar, asi tenenemos contextos mas descriptivos

Ahora para ver que ver que renderizen correctamente las semanas que le pasamos vamos a agregar un propiedad llamada `weeks` en el retorno de la funcion `setup` que nos va a retornar todas las semanas que estan renderizadas en nuestro componente:
```
weeks: wrapper.find('.date-picker__week')
```

De esta manera dentro del contexto podemos hacer esto
```
const { weeks } = setup({weeks:[VALOR DE LAS SEMANAS]})
```

Entonces... ahora deberiamos pensar cual es el formato en que queremos recibir las semanas que contienen dias, para no quemarnos la cabeza propongo el siguiente formato:

```js
{
    weeks:[ // seria el mes la composicion de 4 semanas
        [ // esto es una semana (de length 7)
        ],  
    ]
}
    
```
Aca ya tomamos varias decisione de disenio

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



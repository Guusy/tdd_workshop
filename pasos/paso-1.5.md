## Paso 1.5
En este paso vamos dibujar nuestro boton de aplicar


Lo primero que debemos hacer es, en nuestro describe de `basic render` deberiamos agregar un test que chequee que el boton sea renderizado

para esto vamos a agregar un atributo a la funcion `setup`, que se busque nuestro boton

```js
    applyButton: wrapper.find('.apply-button')
```

Agregamos el test correspondiente, dentro de nuestro describe `basic render`

```js
it('render apply button', () => {
        expect(applyButton).toHaveLength(1)
  })
```

lo vemos fallar y agregamos el tag html en nuestro componente:

```html
      <button className="apply-button"></button>
```

Buensimo ! pero vemos que ese boton le falta informacion, podriamos agregarle un label ! 

Hay varias formas de hacerlo :  podriamos agregar 1 expect mas en mismo it, podriamos hacer otro it, podriamos refactorizar y hacer un describe con el boton de aplicar. Pero para este caso agregaremos otro it

```js
it('render apply with "Aplicar" label', () => {
        expect(applyButton.text()).toEqual('Aplicar')
  })
```

Entonces solo nos queda agregar la palabra `Aplicar` a nuestro boton

```html
      <button className="apply-button">Aplicar</button>
```

Genial ! Ahora me gustaria saber que pasa cuando clickeamos en aplicar no ?

Para eso lo que haremos que es nuestro componente reciba una funcion que queremos que se ejecute cuando clickean el boton de aplicar

```js
describe('when click on apply button', () => {
    const onApplySpy = jest.fn();
    const { applyButton } = setup({ onApply: onApplySpy })

    beforeAll(() => {
      applyButton.simulate('click')
    })

    it('call onApply prop', () => {
      expect(onApplySpy).toBeCalled();
    })
  })

```

Perfecto, como siempre nuestros tests fallan ! jajaja

Ahora vayamos a implementar el codigo !

Deberiamos agarrar esta `prop` nueva:

```js
const { weeks, onDateClicked, selectedDate, onApply } = props;
```

y ponerla en el evento `onClick` de nuestro boton

```jsx
      <button onClick={onApply} className="apply-button">Aplicar</button>
```

Perfecto, nuestros tests ya dan verde ! 


En el [proximo paso](./paso-1.6.md) empezaremos a construir el componente `Calendar` que va tener la logica de negocio !
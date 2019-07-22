# Paso 2

Objetivo: Hacer una transacción de credito (agrega plata a nuestra cuenta)

Entonces vamos a escribir un test para este caso
```js
describe('cuando hacemos una transacción de credito', () => {
        const wallet = new Wallet(20)
        beforeAll(() => {
            wallet.add(20)
        })
        it('aumenta el monto de la cuenta', () => {
            expect(wallet.getBalance()).toEqual(40)
        })
    })
```

Vemos que nuestro test falla ya que el dinero de nuestra cuenta quedo en 20, cuando deberia estar en 40.

Ahora implementemos el minimo codigo para que esto funcione, dentro de la clase agregamos un metodo llamado `add`:
```js
 add(amount) {
        this.balance = this.balance + amount
 }
```

Perfecto ahora nuestro test da verde !

[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/bdf3b0f1dde45c584aa76ada070737e4ab84d1a0) podemos ver el codigo terminado de este paso

Excelente ya cumplimos nuestro objetivo, ahora [hagamos una transacción de debito](./paso-3.md)







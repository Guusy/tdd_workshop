# Paso 2

Objetivo: Hacer una transacción de credito (agrega plata a nuestra cuenta)

Para este punto decidimos tener un estructura especifica para nuestras transacciónes :
```json
    {
        "type":"CREDIT",
        "amount":20
    }
```

Entonces vamos a escribir un test para este caso
```js
describe('cuando hacemos una transacción de credito', () => {
        const wallet = new Wallet(20)
        beforeAll(() => {
            const creditTransaction = { type: 'CREDIT', amount: 20 }
            wallet.add(creditTransaction)
        })
        it('esta debe sumar el monto de nuestra cuenta', () => {
            expect(wallet.getBalance()).toEqual(40)
        })
    })
```

Vemos que nuestro test falla ya que el dinero de nuestra cuenta quedo en 20, cuando deberia estar en 40.

Ahora implementemos el minimo codigo para que esto funcione, dentro de la clase agregamos un metodo llamado `add`:
```js
 add(transaction) {
        this.balance = this.balance + transaction.amount
    }
```

Perfecto ahora nuestro test da verde !

[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/4b8ae79c605932a04021c1d7e75126b7d75ec7c5) podemos ver el codigo terminado de este paso

Excelente ya cumplimos nuestro objetivo, ahora [hagamos una transacción de debito](./paso-3.md)







# Paso 3

Objetivo: Hacer una transacción de debito (saca plata a nuestra cuenta)


Entonces vamos a escribir un test para este caso
```js
describe('cuando hacemos una transacion de debito', () => {
        const wallet = new Wallet(200)
        beforeAll(() => {
            const creditTransaction = { type: 'DEBIT', amount: 100 }
            wallet.add(creditTransaction)
        })
        it('esta debe restar el monto de nuestra cuenta', () => {
            expect(wallet.getBalance()).toEqual(100)
        })
    })
```

Vemos que falla ya que espera que el nuevo monto sea 100 y tenemos 300.

Vamos a arreglar esto, modificando el metodo `add` de la siguiente manera:
```js
add(transaction) {
        if (transaction.type === "CREDIT") {
            this.balance = this.balance + transaction.amount
        } else {
            this.balance = this.balance - transaction.amount
        }
    }
```

El codigo no es el mejor, pero ahora podriamos refactorizarlo como quisieramos.

Viendo el test que escribimos, nuestra gran duda es que pasa si la transaccion hace que el monto sea negativo ?

Genial hacer los tests nos ayudo a ver que nos falta un caso de uso, para el mismo decidimos lanzar un error con un mensaje, ahora tambien deberiamos reescribir nuestros test anteriores para dar un mejor contexto, por que difurca en 2, cuando tenemos saldo suficiente o y cuando no.

```js
describe('cuando hacemos una transacion de debito', () => {
        describe('y nuestro saldo es suficiente', () => {
            const wallet = new Wallet(200)
            beforeAll(() => {
                const creditTransaction = { type: 'DEBIT', amount: 100 }
                wallet.add(creditTransaction)
            })
            it('se resta el monto de nuestra cuenta', () => {
                expect(wallet.getBalance()).toEqual(100)
            })
        })
        describe('y nuestro saldo no es suficiente', () => {
            const wallet = new Wallet(200)
            const creditTransaction = { type: 'DEBIT', amount: 999 }
            it('lanza una excepcion "saldo insuficiente"', () => {
                const addTransaction = () => wallet.add(creditTransaction);
                expect(addTransaction).toThrow('saldo insuficiente');
                expect(wallet.getBalance()).toEqual(200)
            })
        })
    })
```

Vemos que falla, ya que no lanza ninguna excepcion.

Modifiquemos el metodo `add` para que este test pase !

```js
add(transaction) {
        if (transaction.type === "CREDIT") {
            this.balance = this.balance + transaction.amount
        } else {
            const newBalance = this.balance - transaction.amount
            if (newBalance < 0) {
                throw new Error('saldo insuficiente')
            }
            this.balance = newBalance
        }
    }
```

[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/1db300afbdd08bdf9f5b8e06ad7f573a7fe811f5) podemos ver el codigo terminado de este paso








# Paso 3

Objetivo: Hacer una transacción de debito (saca plata a nuestra cuenta)

Pero ahora nos damos cuenta que el argumento que recibimos por el metodo add no nos permite diferenciar si es de debito o credito, entonces deberiamos definir uno :
```json
    {
        "type":"CREDIT",
        "amount":20
    }
```

Ahora vamos nuestro test
```js
describe('cuando hacemos una transacion de debito', () => {
        describe('y nuestro saldo es suficiente', () => {
            const wallet = new Wallet(200)
            beforeAll(() => {
                const debitTransaction = { type: 'DEBIT', amount: 100 }
                wallet.add(debitTransaction)
            })
            it('se resta el monto de nuestra cuenta', () => {
                expect(wallet.getBalance()).toEqual(100)
            })
        })
    })
```

Observamos que falla, ya trata de hacer `numero + objeto` 

Vamos a arreglar esto, modificando el metodo `add` de la siguiente manera:
```js
add(transaction) {
    this.balance = this.balance - transaction.amount
}
```

:eyes: Arreglamos este test, pero los test anteriores rompieron ya que no usan el mismo formato.

```js
describe('cuando hacemos una transacción de credito', () => {
        const wallet = new Wallet(20)
        beforeAll(() => {
            const creditTransaction = { type: 'CREDIT', amount: 20 }
            wallet.add(creditTransaction)
        })
        it('aumenta el monto de la cuenta', () => {
            expect(wallet.getBalance()).toEqual(40)
        })
    })
```

Modificamos el formato, pero aun asi sigue rompiendo los test :(, dice que espera 40 pero que recibio 0, los que nos falta aca es diferenciar por tipo :

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

Genial hacer los tests nos ayudo a ver que nos falta un caso de uso, cuando un el monto se hace negativo no se realiza la transaccion

```js
describe('cuando hacemos una transacion de debito', () => {
        describe('y nuestro saldo es suficiente', () => {
            const wallet = new Wallet(200)
            beforeAll(() => {
                const debitTransaction = { type: 'DEBIT', amount: 100 }
                wallet.add(debitTransaction)
            })
            it('se resta el monto de nuestra cuenta', () => {
                expect(wallet.getBalance()).toEqual(100)
            })
        })
        describe('y nuestro saldo no es suficiente', () => {
            const wallet = new Wallet(200)
            beforeAll(() => {
                const debitTransaction = { type: 'DEBIT', amount: 999 }
                wallet.add(debitTransaction)
            })
            it('no se resta el saldo de nuestra cuenta', () => {
                expect(wallet.getBalance()).toEqual(200)
            })
        })
    })
```

Vemos que falla, ya que resta el saldo de nuestra cuenta.

Modifiquemos el metodo `add` para que este test pase !

```js
add(transaction) {
        if (transaction.type === "CREDIT") {
            this.balance = this.balance + transaction.amount
        } else {
            const newBalance = this.balance - transaction.amount
            if (newBalance >= 0) {
                this.balance = newBalance
            }
        }
    }
```

Aca siendo nosotros los primeros usuarios de este componente, nos damos cuenta que falta feedback de que es lo que paso.

Estaria bueno en este caso lanzar una excepcion y que una capa superior, o aquel que nos este usando, sepa como interpretarla

```js
describe('y nuestro saldo no es suficiente', () => {
            const wallet = new Wallet(200)
            const debitTransaction = { type: 'DEBIT', amount: 999 }
            let addTransaction
            beforeAll(() => {
                addTransaction = () => wallet.add(debitTransaction);
            })
            it('no se resta el saldo de nuestra cuenta', () => {
                try {
                    addTransaction();
                } catch{
                    expect(wallet.getBalance()).toEqual(200)
                }
            })
            it('lanza una excepcion "insufficient balance"', () => {
                expect(addTransaction).toThrow('insufficient balance');
            })
        })
```        

Ahora agreguemos la excepcion a nuestro codigo

```js
add(transaction) {
        if (transaction.type === "CREDIT") {
            this.balance = this.balance + transaction.amount
        } else {
            const newBalance = this.balance - transaction.amount
            if (newBalance < 0) {
                throw new Error('insufficient balance')
            }
            this.balance = newBalance
        }
    }
```    


[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/ddca218949769333b48c1ed80b3f55d852d62b88) podemos ver el codigo terminado de este paso

Damos por finalizado el ejercicio ! 







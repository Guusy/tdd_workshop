# Paso 1

Objetivo: Mostrar el saldo disponible

Comando para correr los tests
```
npm run test
```

Desde el comienzo ya tenemos que pensar 2 decisiones de diseño, si nuestra billetera virtual va ser una clase estatica o vamos la instanciar.

Seria un buen tema a discutir pero para este caso usaremos una clase no estatica

Para comenzar podriamos escribir nuestro primer test:

```js
import Wallet from './Wallet'

describe('Wallet', () => {
    describe('cuando preguntamos por el saldo de la cuenta', () => {
        const wallet = new Wallet(20)
        it('deberia retornar el saldo actual', () => {
            expect(wallet.getBalance()).toEqual(20)
        });
    })
})

```

Entonces vemos el test fallar de la siguiente manera `TypeError: wallet.getBalance is not a function`

Ahora, vamos a hacer pasar este test con el siguiente codigo

```js
export default class Wallet {
    constructor(balance) {
        this.balance = balance;
    }

    getBalance() {
        return this.balance
    }

}
```

Perfecto ahora nuestro test da verde !

[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/4c6053706da4d6c62bdb08a2723a5572666ae737) podemos ver el codigo terminado de este paso

Excelente ya hicimos nuestro primer test, ahora [hagamos una transacción de credito](./paso-2.md)





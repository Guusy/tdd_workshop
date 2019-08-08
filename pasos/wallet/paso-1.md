# Paso 1

Objetivo: Mostrar el saldo disponible

Comando para correr los tests
```
npm run test -- -t="Wallet"
```

Desde el comienzo ya tenemos que pensar 2 decisiones de diseño, si nuestra billetera virtual va ser una clase estatica o vamos la instanciar.

Seria un buen tema a discutir pero para este caso usaremos una clase no estatica

Para comenzar podriamos escribir nuestro primer test:

```js
import Wallet from './Wallet'

describe('Wallet', () => {
    describe('cuando preguntamos por el saldo de la cuenta', () => {
        describe('y no tenemos dinero', () => {
            const wallet = new Wallet();
            it('retorna 0', () => {
                expect(wallet.getBalance()).toEqual(0)
            })
        })
    })
})

```

Entonces vemos el test fallar de la siguiente manera `TypeError: wallet.getBalance is not a function`

Ahora, vamos a hacer el minimo codigo indispensable para pasar este test con el siguiente codigo

```js
export default class Wallet {
    getBalance() {
        return 0
    }
}
```

Pero ahora la duda que nos surgue es que pasa cuando tenemos dinero ? Agregemos un nuevo test que hable sobre esto :
```js
 describe('cuando preguntamos por el saldo de la cuenta', () => {
        describe('y no tenemos dinero', () => {
            const wallet = new Wallet();
            it('retorna 0', () => {
                expect(wallet.getBalance()).toEqual(0)
            })
        })
        describe('y tenemos dinero', () => {
            const wallet = new Wallet(20);
            it('retorna el saldo actual', () => {
                expect(wallet.getBalance()).toEqual(20)
            })
        })
    })
```

Vemos que falla ya que el metodo devuelve 0 siempre, vamos a escribir el codigo para que esto se comporte como realmente queremos:

```js
export default class Wallet {
    constructor(balance) {
        this.balance = balance || 0;
    }

    getBalance() {
        return this.balance
    }
}    
```


Perfecto ahora nuestro test da verde !

[Aca](https://github.com/Guusy/tdd-workshop-quickstart/commit/90ddab000cec2f092fed71ac0917b98b12c27038) podemos ver el codigo terminado de este paso

Excelente ya hicimos nuestro primer test, ahora [hagamos una transacción de credito](./paso-2.md)





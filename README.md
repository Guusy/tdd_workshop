# Workshop TDD

## Que vamos a hacer ?

Vamos a hacer un componente de calendario:

![](./src_readme/demo_component.gif)

Para esto vamos a concentrarnos en 2 partes criticas y separaremos en 2 componentes (uno dumb y otro smart)

1) `<DatePicker/>` : Render de dias (dumb)
2) `<Calendar/>` : Logica de manejo de dias (smart)

## Render
1) Un dia puede estar seleccionado o no
2) Un dia puede estar habilitado o no
3) Un dia puede tener un tipo de selector que indique que se encuentra entremedio de una seleccion
4) El dia de hoy tiene que ver con un estilo diferente
5) Renderizar un header con [DOM,LUN,MAR,MIE,JUE,VIE,SAB]
6) Renderizar flechas para moverse entre los meses (disparan un callback) Y el mes-año donde se encuentra posicionado
7) Al clickear un dia debemos disparar un callback que avise

## Logica
1) Tener una funcion que te seleccione un dia y que tenga una logica diferente si es de tipo unico o rango
2) Si es de tipo rango, tener un maximo o un minimo de dias a seleccionar 
3) Transferirnos hacia otro mes
4) Recibir por parametro dias preselecionados (si es un rango vamos a tener que marcar como dias intermedios los demas) (objetos Date js)
5) Recibir una fecha por la cual arrancar (el mes que vamos a renderizar) o si no renderizar el mes actual
6) Un boton de aplicar (opcional)
7) Recibir un callback de cuando se seleccionar una fecha o cuando se selecciona un rango (habilitado y deshabilitado del mismo)
8) Recibir un  un habilitado desde y hasta para la seleccion de dias
9) Recibir dias especificos a desahabilitar
10) Al cambiar las fechas mantener la seleccion

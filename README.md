# Workshop TDD

## Que vamos a hacer ?

Vamos a hacer un componente de calendario:

![](./src_readme/demo_component.gif)

Para esto vamos a concentrarnos en 2 componentes (uno dumb y otro smart)

1) `<DatePicker/>` : Render de dias (dumb)

- Un dia puede estar seleccionado o no
- Un dia puede estar habilitado o no
- El dia de hoy se tiene que ver con un estilo diferente
- Renderizar un header con `[DOM, LUN, MAR, MIE, JUE, VIE, SAB]`
- Al clickear un dia debemos disparar un callback

2) `<Calendar/>` : Logica de manejo de dias (smart)

- Soportar dos tipos de selección: multiples días y de 1 día
- Si es de tipo rango, tener un maximo de dias a seleccionar
- Recibir por parametro dias preselecionados
- Renderizar el mes actual
- Un boton de aplicar (que esté deshabilitado si no se completó la selección)
- Recibir un callback para cuando se seleccione una fecha o un rango 
- Recibir dias especificos a desahabilitar

Comenzemos con el [paso 1](./pasos/paso-1.1.md)

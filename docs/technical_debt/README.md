# Deuda Técnica

## ¿Qué es la deuda técnica?

Se refiere a la falta de calidad en el código, esto genera una deuda que repercutirá en costos futuros (económicos).

- Tiempo en realizar mantenimientos
- Tiempo en refactorizar código
- Tiempo en comprender el código
- Tiempo adicional en la transferencia del código

## Esquema de deuda técnica de Martin Fowler

Cuatro cuadrantes:

- **Imprudente y deliverada**: El desarrollador actua de forma consciente e imprudente, lo que genera un proyecto de poca calidad y es intolerante al cambio.

- **Imprudente e inadvertida**: Es probablemente la más peligrosa, ya que se genera por el desconocimiento o falta de experiencia, generalmente se desarrolla por algun Junior Dev o falso Sr Dev

- **Prudente y deliverada**: Es la deuda en la cual sabemos y estamos conscientes que dicha deuda existe. El peligro radica en que si no se paga a tiempo, más intereses pagaremos en el futuro cercano. Un ejemplo claro es el uso de `TODOs` indicando cambios futuros.

- **Prudente e inadvertida**: "Ahora sabemos como lo deberíamos haber hecho", esta deuda aparece cuando el proyecto ha crecido y madurado, los devs son conscientes de posibles mejoras o cambios.

<br/>

> Caer en la deuda técnica es normal y a menudo inevitable

<br/>

`Lo que hace un buen programador, es estar consciente de esa deuda y preocuparse por pagarla`

Para pagar la deuda técnica debemos pensar en: `Refactorización`

## ¿Qué es la refactorización?

Es el proceso que tiene como objetivo mejorar el código sin alterar su comportamiento para que sea más entendible y tolerante a cambios. Usualmente para que una refactorización tenga el objetivo esperado, es imprescindible contar con `testing`.

Sin pruebas automáticas o `testing` no podemos estar seguros al 100% de que la refactorización funcionó (**"Si funciona no lo toques"**).

## Ten en cuenta

La mala calidad del código siempre la acaba pagando o asumiendo alguien (cliente, proveedor o desarrollador).

## Clean Code

> "Es aquel que se ha escrito con la intención de que otra persona (o tú mismo en el futuro) lo entienda. **Carlos Blé**"

<br/>

> "Nuestro código tiene que ser simple y directo, debería leerse con la misma facilidad que un texto bien escrito. **Grady Booch**"

<br/>

> "Programar es el arte de decirtle a otro humano lo que quieres que la computadora haga. **Donald Knuth**"
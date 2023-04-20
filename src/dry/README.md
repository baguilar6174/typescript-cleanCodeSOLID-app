# Principio DRY (Don't repeat yourself)

> "Si quieres ser un desarrollador productivo esfuérzate en escribir un código legible" **Robert C. Martin**

## ¿Qué es el principio DRY?

- Se resume a evitar tener duplicidad en el código
- Simplifica las pruebas
- Ayuda a centralizar los procesos
- Aplicarlo, usualmente implica refactorizar el código

```typescript
type Size = '' | 'S' | 'M';

class Product {
  constructor(
    public name: string = "",
    public price: number = 0,
    public size: Size = "",
  ){}

  isProductReady(): boolean {
    for ( const key in this ) {
      switch ( typeof this[key] ) {
        case 'string':
          if ( this[key].toString().length <= 0 ) throw Error(`${key} is empty`);
          break;
        case 'number':
          if ( Number(this[key]) <= 0 ) throw Error(`${key} is zero`);
          break;
        default:
          throw Error(`${typeof this[key]} is not supported`);
      }
    }
    return true;
  }

  toString() {
    // 🟥 no DRY
    if( this.name.length <= 0 ) throw Error("Name is empty");
    if( this.price <= 0 ) throw Error("Price is empty");
    if( this.size <= 0 ) throw Error("Size is empty");
    // 🟩 with DRY
    if ( !this.isProductReady ) return;
    return `${this.name} (${this.price}), ${this.size}`;
  }
}

const bluePants = new Product("Blue large pants");
console.log(bluePants.toString()); // Blue large pants
```
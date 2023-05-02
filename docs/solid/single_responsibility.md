# Single responsibility (Responsabilidad única)

> "Nunca debería haber más de un motivo por el cual cambiar una clase o un módulo" -**Robert C. Martin**

Una clase debe tener una única responsabilidad, tener más de una responsabilidad en nuestras clases o módulos hace que el código sea dificil de leer testear y mantener. Es decir, hace que el código sea menos flexible, más rígido y en definitiva menos tolerante al cambio.

**"tener una única responsabilidad" !== "hacer una única cosa"**

Queremos que nuestras clases o módulos se enfoquen en realizar una serie de procesos estrechamente relacionados entre sí.

```typescript
🟥 bad
interface Product { 
  id:   number;
  name: string;
}

// Usualmente, esto es una clase para controlar la vista que es desplegada al usuario
// Recuerden que podemos tener muchas vistas que realicen este mismo trabajo.
class ProductBloc {

  loadProduct( id: number ) {
    // Realiza un proceso para obtener el producto y retornarlo
    console.log('Producto: ',{ id, name: 'OLED Tv' });
  }

  saveProduct( product: Product ) {
    // Realiza una petición para salvar en base de datos 
    console.log('Guardando en base de datos', product );
  }

  notifyClients() {
    console.log('Enviando correo a los clientes');
  }

  onAddToCart( productId: number ) {
    // Agregar al carrito de compras
    console.log('Agregando al carrito ', productId );
  }
}

const productBloc = new ProductBloc();

productBloc.loadProduct(10);
productBloc.saveProduct({ id: 10, name: 'OLED TV' });
productBloc.notifyClients();
productBloc.onAddToCart(10);
```

```typescript
🟩 best
interface Product { 
  id:   number;
  name: string;
}

class ProductService {
  getProduct(id: number){
    // Realiza un proceso para obtener el producto y retornarlo
    console.log('Producto: ',{ id, name: 'OLED Tv' });
  }

  postProduct(product: Product){
    // Realiza una petición para salvar en base de datos 
    console.log('Guardando en base de datos', product );
  }
}

class Mailer {
  sendEmail(emails: string[]) {
    console.log('Enviando correo a los clientes');
  }
}

// Usualmente, esto es una clase para controlar la vista que es desplegada al usuario
// Recuerden que podemos tener muchas vistas que realicen este mismo trabajo.
class ProductBloc {

  private productService: ProductService;
  private mailer: Mailer;

  constructor(productService: ProductService, mailer: Mailer){
    this.productService = productService;
    this.mailer = mailer;
  }

  loadProduct( id: number ) {
    this.productService.getProduct(id);
  }

  saveProduct( product: Product ) {
    this.productService.postProduct(product);
  }

  notifyClients(emails: string[]) {
    this.mailer.sendEmail(emails)
  }
}

class CartBloc {
  addToCart( productId: number ) {
    // Agregar al carrito de compras
    console.log('Agregando al carrito ', productId );
  }
}

const productService = new ProductService();
const mailer = new Mailer();

const productBloc = new ProductBloc(productService, mailer);

productBloc.loadProduct(10);
productBloc.saveProduct({ id: 10, name: 'OLED TV' });
productBloc.notifyClients();

const cartBloc = new CartBloc();
cartBloc.addToCart(10);
```

## Detectar violaciones de SRP

- Nombres de clases y módulos demasiado genéricos
- Cambios en el código suelen afectar la clase o módulo
- La clase involucra múltiples capas
- Número elevado de importaciones
- Cantidad elevada de métodos o funciones públicas
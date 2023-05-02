# Liskov substitution (Principio de sustitución de Liskov)

> "Las funciones que utilicen punteros o referencias a clases deben ser capaces de usar objetos de clases derivadas sin saberlo" **-Robert C. Martin**

Siendo `U` un subtipo de `T`, cualquier instancia de `T` debería poder ser sustituida por cualquier instancia de `U` sin alterar las propiedades del sistema.

```typescript

// 🟥 bad

export class Tesla {
  constructor( private numberOfSeats: number ) {}
  getNumberOfTeslaSeats() {
    return this.numberOfSeats;
  }
}

export class Audi {
  constructor( private numberOfSeats: number ) {}
  getNumberOfAudiSeats() {
    return this.numberOfSeats;
  }
}

export class Toyota {
  constructor( private numberOfSeats: number ) {}
  getNumberOfToyotaSeats() {
    return this.numberOfSeats;
  }
}

export class Honda {
  constructor( private numberOfSeats: number ) {}
  getNumberOfHondaSeats() {
    return this.numberOfSeats;
  }
}

const printCarSeats = ( cars: (Tesla | Audi | Toyota | Honda)[] ) => { 
  for (const car of cars) {      
    if( car instanceof Tesla ) {
        console.log( 'Tesla', car.getNumberOfTeslaSeats() )
        continue;
    }
    if( car instanceof Audi ) {
        console.log( 'Audi', car.getNumberOfAudiSeats() )
        continue;
    }
    if( car instanceof Toyota ) {
        console.log( 'Toyota', car.getNumberOfToyotaSeats() )
        continue;
    }
    if( car instanceof Honda ) {
        console.log( 'Honda', car.getNumberOfHondaSeats() )
        continue;
    }         
  }
}

const cars = [ new Tesla(7), new Audi(2), new Toyota(5), new Honda(5)];
printCarSeats( cars );
```

```typescript

// 🟩 best

export abstract class Vehicle {
  abstract getNumberOfSeats(): number;
}

export class Tesla extends Vehicle {
  constructor( private numberOfSeats: number ) {
    super();
  }
  getNumberOfSeats() {
    return this.numberOfSeats;
  }
}

export class Audi extends Vehicle {
  constructor( private numberOfSeats: number ) {
    super();
  }
  getNumberOfSeats() {
    return this.numberOfSeats;
  }
}

export class Toyota extends Vehicle {
  constructor( private numberOfSeats: number ) {
    super();
  }
  getNumberOfSeats() {
    return this.numberOfSeats;
  }
}

export class Honda extends Vehicle {
  constructor( private numberOfSeats: number ) {
    super();
  }
  getNumberOfSeats() {
    return this.numberOfSeats;
  }
}

const printCarSeats = ( cars: Vehicle[] ) => { 
  cars.forEach((car) => {
    console.log(car.constructor.name, car.getNumberOfSeats());
  })
}

const cars = [ new Tesla(7), new Audi(2), new Toyota(5), new Honda(5)];
printCarSeats( cars );
```
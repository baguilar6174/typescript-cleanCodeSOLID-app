# Interfaz Segregation (Segregación de interfaz)

> "Los clientes no deberían estar obligados a depender de interfaces que no utilicen" **-Robert C. Martin**

Este principio establece que los clientes no deberían verse forzados a depender de interfaces que no usan.

```typescript
interface Bird {
  fly(): void;
  eat(): void;
  run(): void;
}

class Tucan implements Bird {
  public fly() {}
  public eat() {}
  public run() {}
}

class Humminbird implements Bird {
  public fly() {}
  public eat() {}
  public run() {}
}

class Ostrich implements Bird {
  public fly() {} // No debería implementar este método
  public eat() {}
  public run() {}
}
```

```typescript
interface Bird {
  eat(): void;
}

interface FlyingBird {
  fly(): void;
}

interface RunningBird {
  run(): void;
}

class Tucan implements Bird, FlyingBird {
  public fly() {}
  public eat() {}
}

class Humminbird implements Bird, FlyingBird {
  public fly() {}
  public eat() {}
}

class Ostrich implements Bird, RunningBird {
  public eat() {}
  public run() {}
}
```

## Detectar violaciones

- Este principio está estrechamente relacionado con el principio de responsabilidad única y el principio de sustitución de Liskov. Si las interfaces que estamos diseñando nos obligan a violentar dichos principios, posiblemente se este violando este principio.

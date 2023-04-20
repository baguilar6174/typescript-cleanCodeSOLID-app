# Clases y comentarios

Las clases deben tener una responsabilidad específica y bien definida, es importante evitar nombres genéricos, ya que esto implica que las clases realicen demasiado trabajo o más trabajo que el que deberían hacer. Las clases deben tener nombres formados por un sustantivo o frases de sustantivo, 

**Se procura usar UpperCamelCase**

Para determinar si un nombre de clase es bueno se debe responder tres preguntas:

1. ¿Qué exactamente hace la clase?
2. ¿Cómo exactamente esta clase realiza cierta tarea?
3. ¿Hay algo específico sobre su ubicación?

```typescript
// 🟥 bad
class Manager {}
class Data {}
class Info {}
class Individual {}
class Processor {}
class SpecialMonsterView {}
```

## Ejercicio

```typescript
type Gender = "M" | "F";

class Person {
  public name: string;
  public gender: Gender;
  public birthdate: Date;

  // create constructor first option
  constructor(
    name: string,
    gender: Gender,
    birthdate: Date,
  ){
    this.name = name;
    this.gender = gender;
    this.birthdate = birthdate;
  }

  // create constructor second option
  constructor(
    public name: string,
    public gender: Gender,
    public birthdate: Date,
  ){}
}

const newPerson = new Person("Bryan", "M", new Date("1996-05-06"));
```
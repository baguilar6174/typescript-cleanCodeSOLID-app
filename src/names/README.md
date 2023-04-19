# Convenciones para nombres

## Nombres pronunciables y expresivos

Los nombres de variables, funciones, clases, etc, deben estar escritos en inglés y deben ser pronunciables, además deben expresar de manera clara a que se hace referencia con el nombre (**no necesitas ahorrar letras en los nombres de tus variables**).

```typescript
// uso incorrecto
const n = 53;
const tx = .15;
const cat = "Shirts";
const ddmmyyyy = new Date();
```

```typescript
// uso correcto
const numberOfunits = 53;
const tax = .15;
const category = "Shirts";
const birthDate = new Date();
```

## Ausencia de información técnica

Debemos evitar que los nombres no contengas información técnica (evitar la relación con la tecnología que se este usando)

```typescript
// uso incorrecto
class AbstractUser {} // la palabra `abstract` es parte de la teconología
class UserMixin {}
class UserImplementation {}
interface UserInterface {} // ya sabemos que se trata de una interfaz por la misma declaración
```

```typescript
// uso correcto
class User {}
interface User {}
```

El uso de comentario en el código es un indicador de que posiblemente los nombres otorgados no son los adecuados.

```typescript
// ❌ Archivos a evaluar
const fs = [
    { id: 1, f: false },
    { id: 2, f: false },
    { id: 3, f: true },
    { id: 4, f: false },
    { id: 5, f: false },
    { id: 7, f: true },
];

// ✅
const filesToEvaluate = [
    { id: 1, flagged: false },
    { id: 2, flagged: false },
    { id: 3, flagged: true },
    { id: 4, flagged: false },
    { id: 5, flagged: false },
    { id: 7, flagged: true },
];

// ✅ Archivos marcados para borrar
const filesToDelete = filesToEvaluate.map( file => file.flagged );

// ❌ día de hoy
const ddmmyyyy = new Date();
// ✅
const today = new Date();

// ❌ días transcurridos
const d: number = 23;
// ✅
const elapsedTimeInDays: number = 23;

// ❌ número de archivos en un directorio
const dir = 33;
// ✅
const numberOfFilesInDirectory = 33;

// ❌ primer nombre
const nombre = 'Bryan';
// ✅
const firstName = 'Bryan';

// ❌ cantidad máxima de clases por estudiante
const max = 6;
// ✅
const maxClassesPerStudent = 6;
```

## Nombres según tipo de dato

### Arreglos

Sabes que es una lista iterable de elementos, por lo general, todos los elementos tienen una característica en común por lo que pluralizar su nombre es recomendado.

```typescript
// 🟥 bad
const fruit: string[] = ["apple", "banana", "orange"];

// 🟧 regular
const fruitList: string[] = ["apple", "banana", "orange"];

// 🟨 good
const fruits: string[] = ["apple", "banana", "orange"];

// 🟩 best
const fruitName: string[] = ["apple", "banana", "orange"];
```

### Booleans

Usualmente tienen dos valores (excepto que tengan `undefined` | `null`, etc). El uso de prefijos como: `is`, `has`, `can`, puede ser de mucha ayuda a que el nombre tenga mucho más sentido semántico.

**Se procura que su significado siempre sea positivo y evitar las negaciones en el nombre**

```typescript
// 🟥 bad
const open = true;
const write = true;
const fruit = true;
const active = false;
const noValues = true;
const notEmpty = true;

// 🟩 best
const isOpen = true;
const canWrite = true;
const hasFruit = true;
const isActive = false;
const hasValues = false;
const isEmpty = false;
```

### Números

Se pueden usar muchos términos para nombrar variables numéricas, se puede hacer uso de palabras como: `min`, `max`, `total`, `of` para dar un mejor signiticado.

```typescript
// 🟥 bad
const fruits = 3;
const cars = 10;

// 🟩 best
const maxFruits = 5;
const minFruits = 2;
const totalFruits = 4;
const totalOfCars = 10;
```

### Funciones

Los nombres de las funciones deben representar acciones, por lo general deben construirse usando el verbo que representa la acción seguido de un sustantivo. El nombre de la función debe expresar lo que hace, pero también debe abstenerse de toda la implementación de la función.

**Los nombres de las funciones tienen que hacer exactamente lo que dice su nombre**

```typescript
// 🟥 bad
function sendEmail(): boolean {
  // verify if user exists
  ...
  // create user in DB
  ...
  // if OK, send email
  ...
  return true;
}
```

```typescript
// 🟥 bad
createUserIfNotExits();
updateUserIfNotEmpty();
sendEmailIfFieldsValid();

// 🟩 best
createUser();
updateUser();
sendEmail();
```

#### Argumentos y Parámetros

Se recomienda limitar a tres parámetros ya que si existen más de tres se tiende a complicar la lectura y posición que se deben enviar en los argumentos. Además, se recomienda ordenar las propiedades alfabéticamente.

**Si se nececita enviar más de tres argumentos se recomienda el uso de objectos, o si se usa un lenguaje tipado como TS, usar interfaces o tipos**

### Ejemplos

```typescript
// ❌arreglo de temperaturas celsius
const arrayOfNums = [33.6, 12.34];
// ✅
const temperaturesCelsius = [33.6, 12.34];

// ❌ Dirección ip del servidor
const ip = '123.123.123.123';
// ✅
const serverIp = '123.123.123.123';


// ❌ Listado de usuarios
const people = [{id: 1, email: 'bryan@google.com'},{ id: 2, email: 'alexander@google.com' }];
// ✅
const users = [...]


// ❌ Listado de emails de los usuarios
const emails = people.map( u => u.email );
// ✅
const userEmails = people.map( user => user.email );

// ❌ Variables booleanas de un video juego
const jump = false;
const run = true;
const noTieneItems = true;
const loading = false;
// ✅
const canJump = false;
const canRun = true;
const hasItems = false;
const isLoading = false;

// ❌ Obtiene los libros
function book() {}
// ✅
function getBooks() {}

// ❌ obtiene libros desde un URL
function BooksUrl( u: string) {}
// ✅
function getBooksByUrl( url: string) {}


// ❌ obtiene el área de un cuadrado basado en sus lados
function areaCuadrado( s: number ) {}
// ✅
function getSquareArea( side: number ) {}


// ❌ imprime el trabajo
function printJobIfJobIsActive() {}
// ✅
function printJob() {}

```

### Clases

Las clases deben tener nombres formados por un sustantivo o frases de sustantivo, es importante evitar nombres genéricos, ya que esto implica que las clases realicen demasiado trabajo o más trabajo que el que deberían hacer.

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
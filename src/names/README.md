# Convenciones para nombres

## Nombres pronunciables y expresivos

Los nombres de variables, funciones, clases, etc, deben estar escritos en inglés y deben ser pronunciables, además deben expresar de manera clara a que se hace referencia con el nombre (**no necesitas ahorrar letras en los nombres de tus variables**).

```js
// uso incorrecto
const n = 53;
const tx = .15;
const cat = "Shirts";
const ddmmyyyy = new Date();
```

```js
// uso correcto
const numberOfunits = 53;
const tax = .15;
const category = "Shirts";
const birthDate = new Date();
```

## Ausencia de información técnica

Debemos evitar que los nombres no contengas información técnica (evitar la relación con la tecnología que se este usando)

```js
// uso incorrecto
class AbstractUser {} // la palabra `abstract` es parte de la teconología
class UserMixin {}
class UserImplementation {}
interface UserInterface {} // ya sabemos que se trata de una interfaz por la misma declaración
```

```js
// uso correcto
class User {}
interface User {}
```

El uso de comentario en el código es un indicador de que posiblemente los nombres otorgados no son los adecuados.

```js
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



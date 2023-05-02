# Dependency inversion (Inversión de dependencias)

> "Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones. Las abstracciones no deben depender de concreciones. Los detalles deben depender de abstracciones" **-Robert C. Martin**

* Los módulos de alto nivel no deben depender de módulos de bajo nivel
* Ambos deberían depender de abstracciones
* Las abstracciones no deben depender de detalles
* Los detalles deberían depender de abstracciones

## Depender de abstracciones

Nos referimos al uso de clases abstractas o interfaces

Uno de lo smotivos más importantes por el cual las reglas de negocio o capa de dominio deben de estas y no de concreciones es que aumenta la tolerancia al cambio.

**¿Por qué obtenemos este beneficio?**

Cada cambio en un componente abstracto implica un cambio en su implementación.

Por el contrario, los cambios en implementaciones concretas, la mayoría de las veces, no requieren cambios en las interfaces que implementa.

## Inyección de dependencias

Dependencia en programación, significa que un módulo o componente requiere de otro para poder realizar su trabajo.

En algún momento nuestra aplicación llegará a estar formada por muchos módulos, en este momento es cuando debemos usar inyección de dependencias.

```typescript
// 🟥 bad
interface Post {
  body:   string;
  id:     number;
  title:  string;
  userId: number;
}


export class PostService {
  private posts: Post[] = [];

  constructor() {}

  async getPosts() {
    const jsonDB = new LocalDataBaseService();
    this.posts = await jsonDB.getFakePosts();

    return this.posts;
  }
}

export class LocalDataBaseService {
  constructor() {}

  async getFakePosts() {
    return [
      {
        'userId': 1,
        'id': 1,
        'title': 'sunt aut facere repellat provident occaecati excepturi optio reprehenderit',
        'body': 'quia et suscipit suscipit recusandae consequuntur expedita et cum reprehenderit molestiae ut ut quas totam nostrum rerum est autem sunt rem eveniet architecto'
      },
      {
        'userId': 1,
        'id': 2,
        'title': 'qui est esse',
        'body': 'est rerum tempore vitae sequi sint nihil reprehenderit dolor beatae ea dolores neque fugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis qui aperiam non debitis possimus qui neque nisi nulla'
      }
    ]
  }
}

const postService = new PostService();
const posts = await postService.getPosts();
console.log({ posts })
```

```typescript
// 🟩 best
interface Post {
  body:   string;
  id:     number;
  title:  string;
  userId: number;
}


export class PostService {
  private posts: Post[] = [];

  constructor(private postsProvider: PostsProvider) {}

  async getPosts() {
    this.posts = await this.postsProvider.getPosts();

    return this.posts;
  }
}

export abstract class PostsProvider {
  abstract getPosts(): Promise<Post[]>;
}

export class LocalDataBaseService implements PostsProvider {
  constructor() {}
  async getPosts() {
    return [
      {
        'userId': 1,
        'id': 1,
        'title': 'sunt aut facere repellat provident occaecati excepturi optio reprehenderit',
        'body': 'quia et suscipit suscipit recusandae consequuntur expedita et cum reprehenderit molestiae ut ut quas totam nostrum rerum est autem sunt rem eveniet architecto'
      },
      {
        'userId': 1,
        'id': 2,
        'title': 'qui est esse',
        'body': 'est rerum tempore vitae sequi sint nihil reprehenderit dolor beatae ea dolores neque fugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis qui aperiam non debitis possimus qui neque nisi nulla'
      }
    ]
  }
}

export class JsonDataBaseService implements PostsProvider {
  async getPosts() {
    return localPosts; // por ejemplo de un fichero JSON
  }
}

const provider = new PostsProvider();
const postService = new PostService(provider);
const posts = await postService.getPosts();
console.log({ posts })
```
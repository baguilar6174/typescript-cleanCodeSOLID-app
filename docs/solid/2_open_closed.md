# Open closed (Principio de abierto / cerrado)

Es un principio que depende mucho del contexto, establece que las entidades de software (clases, módulos, métodos, etc) deben estar abiertas para la extensión, pero cerradas para la modificación.

Este principio se puede lograr mediante el uso de la herencia o mediante patrones de diseño de composición como el patrón strategy.

```typescript
import axios from 'axios';

// Dependencia de AXIOS en los métodos
export class TodoService { 
  async getTodoItems() {
    const { data } = await axios.get('https://jsonplaceholder.typicode.com/todos/');
    return data;
  }
}

export class PostService {
  async getPosts() {
    const { data } = await axios.get('https://jsonplaceholder.typicode.com/posts');
    return data;
  }
}

export class PhotosService {
  async getPhotos() {
    const { data } = await axios.get('https://jsonplaceholder.typicode.com/photos');
    return data;
  }
}

const todoService = new TodoService();
const postService = new PostService();
const photosService = new PhotosService();

const todos = await todoService.getTodoItems();
const posts = await postService.getPosts();
const photos = await photosService.getPhotos();

console.log({ todos, posts, photos });
```

```typescript
// eliminar dependencia de AXIOS

import axios from 'axios';

export class HttpClient {
  // con dependencia de axios
  async get( url: string ){
    const { data, status } = await axios.get(url);
    return { data, status };
  }

  // con dependencia de fetch
  async get( url: string ){
    const response = await fetch(url);
    const data = await response.json();
    return { data, status: response.status };
  }
}
```

```typescript
export class TodoService { 

  constructor(private httpClient: HttpClient){}

  async getTodoItems() {
    const { data } = await this.httpClient.get('https://jsonplaceholder.typicode.com/todos/');
    return data;
  }
}

export class PostService {

  constructor(private httpClient: HttpClient){}

  async getPosts() {
    const { data } = await this.httpClient.get('https://jsonplaceholder.typicode.com/posts');
    return data;
  }
}

export class PhotosService {

  constructor(private httpClient: HttpClient){}

  async getPhotos() {
    const { data } = await this.httpClient.get('https://jsonplaceholder.typicode.com/photos');
    return data;
  }
}

const httpClient = new HttpClient();

const todoService = new TodoService(httpClient);
const postService = new PostService(httpClient);
const photosService = new PhotosService(httpClient);

const todos = await todoService.getTodoItems();
const posts = await postService.getPosts();
const photos = await photosService.getPhotos();

console.log({ todos, posts, photos });
```

## Detectar violaciones

- Cambios normalmente nuestra clase o módulo
- Cuando una clase o módulo afecta muchas capas (presentación, almacenamiento, etc)

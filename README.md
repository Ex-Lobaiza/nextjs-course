# Curso Introductorio a Next.js con App Directory

¡Bienvenido/a al curso introductorio a Next.js con App Directory! Durante este curso, exploraremos los fundamentos de Next.js utilizando App Directory para construir una aplicación web: Restaurancy, un catálogo de restaurantes.

El diseño de este curso se plantea de manera incremental, donde cada lección se basa en la anterior. Te recomendamos seguir el orden de las lecciones para obtener el máximo beneficio.

Es natural que algunos conceptos puedan resultar complicados al principio o que no siempre sea evidente el motivo detrás de ciertas decisiones. No te preocupes, a medida que avances en el curso y te enfrentes a más ejercicios, así como a la creación de aplicaciones, estos conceptos irán cobrando mayor claridad y sentido. Ten en cuenta que hay diversas formas de lograr los mismos resultados, así que si tienes ideas diferentes, ¡adelante!

Si en algún momento sientes que el contenido del curso no es suficiente para abordar los ejercicios o comprender un tema en particular, no dudes en recurrir a la documentación oficial, ya sea de [Next.js](https://docs.nextjs.org/) o de [React](https://react.dev/reference/react).

## Requisitos

Asegúrate de cumplir con los siguientes requisitos antes de comenzar el curso:

- Conocimientos básicos de HTML, CSS y JavaScript.
  - Si no estás familiarizado con HTML, CSS y JavaScript, te recomendamos realizar la certificación de [Responsive Web Design](https://www.freecodecamp.org/learn/responsive-web-design) de freeCodeCamp.
- Conocimientos básicos de React.
  - En caso de no tener experiencia en React, te sugerimos completar [el curso oficial de React](https://react.dev/learn) o el de [React Foundations de Next.js](https://nextjs.org/learn/react-foundations).
- Tener Node.js instalado en tu computadora.
- Contar con un editor de código de tu preferencia.
  - También puedes optar por un entorno en línea, como [CodeSandbox](https://codesandbox.io), si no deseas o no puedes instalar nada en tu computadora.

## Terminología

A lo largo del curso, utilizaremos algunos conceptos clave que es importante que conozcas, aunque no necesariamente debes memorizar. Estos son:

- **Routing (Enrutamiento):** Decide, basado en la URL, qué contenido mostrar al usuario.
- **Caching (Caché):** Espacio de almacenamiento temporal para guardar datos que se utilizarán en el futuro.
- **Rendering (Renderizado):** Proceso de convertir un componente en una representación visual.
- **Layout (Diseño):** Envoltorio de una página que define la estructura o diseño exterior.
- **Nested layout/pages/etc (Diseño/páginas/etc. anidados):** Por ejemplo, un diseño anidado está dentro de otro diseño.
- **Tree (Árbol):** Convención para visualizar una estructura jerárquica.
- **Subtree (Subárbol):** Un árbol dentro de otro árbol.
- **Leaf/Leaves (Hoja/Hojas):** Nodo sin hijos, como un componente sin componentes internos.
- **URL segment (Segmento de URL):** Por ejemplo, en la URL `restaurancy.com/restaurante/goncy`, `restaurante` y `goncy` son segmentos de URL.
- **URL path (Ruta de URL):** Lo que sigue al dominio, como `/restaurante/goncy` en `restaurancy.com/restaurante/goncy`.
- **Build (Compilación):** Proceso de convertir el código en un paquete listo para ser desplegado.
- **Bundle (Paquete):** Archivo que contiene parte o todo el código de la aplicación.
- **Boilerplate (Código base):** Porción de código repetitivo con poca variación.

# Índice

1. [¿Qué es Next.js?](#que-es-nextjs)
2. [Creación de una Aplicación con Next.js](#creando-una-aplicación-con-nextjs)
   - 2.1 [Tecnologías en el Proyecto](#tecnologías-en-el-proyecto)
   - 2.2 [Estructura del Proyecto](#estructura-del-proyecto)
3. [Ambientes de Renderizado (Servidor y Cliente)](#ambientes-de-renderizado-servidor-y-cliente)
   - 3.1 [Server Components](#server-components)
   - 3.2 [Client Components](#client-components)
   - 3.3 [Cuándo Usar Server Components y Client Components](#cuando-usar-server-components-y-client-components)
4. [Mostrando los Restaurantes](#mostrando-los-restaurantes)
5. [Mostrando un Restaurante](#mostrando-un-restaurante)
   - 5.1 [Router](#router)
   - 5.2 [Rutas Dinámicas](#rutas-dinámicas)
   - 5.3 [Colocación](#colocación)
6. [Navegación](#navegación)
7. [Estados de Carga](#estados-de-carga)
8. [Manejo de Errores](#manejo-de-errores)
9. [Uso de una Base de Datos](#usando-una-base-de-datos)
10. [Construyendo Nuestra Aplicación](#buildeando-nuestra-aplicación)
11. [Estrategias de Renderizado](#estrategias-de-renderizado)
    - 11.1 [Renderizado Estático](#renderizado-estático-por-defecto)
    - 11.2 [Renderizado Dinámico](#renderizado-dinámico)
12. [Caching](#caching)
    - 12.1 [Configuraciones de Revalidación de Caché](#configuraciones-de-revalidación-de-cache)
        - 12.1.1 [cache: no-store](#cache-no-store)
        - 12.1.2 [revalidate: `<number>`](#revalidate-number)
        - 12.1.3 [Configuración de Segmento de Ruta](#configuración-de-segmento-de-ruta)
        - 12.1.4 [Funciones Dinámicas](#funciones-dinámicas)
13. [Revalidación Manual](#revalidación-manual)
    - 13.1 [revalidatePath](#revalidatepath)
    - 13.2 [revalidateTag](#revalidatetag)
14. [Parámetros de URL](#parámetros-de-url)
15. [Agrupación de Rutas](#agrupado-de-rutas)
16. [Server Actions](#server-actions)
17. [Guardado en Favoritos (localStorage)](#guardar-en-favoritos-localstorage)
    - 17.1 [Pre-renderizado](#pre-renderizado)
    - 17.2 [Lazy Loading](#lazy-loading)


## ¿Qué es Next.js?

[Next.js](https://nextjs.org/) es un framework híbrido que opera tanto en el servidor como en el cliente, construido sobre React. Proporciona herramientas y funcionalidades que simplifican el desarrollo de aplicaciones web. Next.js se encarga de toda la configuración necesaria de React y sus herramientas para que nosotros podamos enfocarnos en desarrollar nuestra aplicación.

## Creando una Aplicación con Next.js

La forma más sencilla de iniciar una aplicación Next.js en nuestra máquina es mediante el paquete `create-next-app` de npm. Este paquete facilita la creación de una aplicación Next.js con todas las configuraciones esenciales para comenzar a desarrollar.

```bash
npx create-next-app@latest --example "https://github.com/goncy/nextjs-course" --example-path "code/starter" restaurancy
```
> Puedes omitir los parámetros `--example` y `--example-path` si deseas crear un proyecto personalizado.

Una vez completada la ejecución del comando, se generará una carpeta llamada `restaurancy` con todos los archivos necesarios para ejecutar la aplicación.

A continuación, ejecutemos los siguientes comandos:

```bash
cd restaurancy
npm run dev
```

Después de unos segundos, deberías ver un mensaje como este:

```bash
  ▲ Next.js <versión de Next.js>
  - Local:        http://localhost:3000
```

Si abres el navegador en la dirección `http://localhost:3000`, deberías visualizar una página de bienvenida similar a la siguiente:

![Página de bienvenida de Next.js](./images/starter.jpg)

### Tecnologías en el Proyecto

Además de Next.js y React, este proyecto utiliza [TypeScript](https://www.typescriptlang.org/) para añadir tipado y [Tailwind CSS](https://tailwindcss.com/) para gestionar estilos. No te preocupes si no estás familiarizado con TypeScript o Tailwind CSS; puedes optar por no escribir tipos en TypeScript y evitar el uso de las clases de Tailwind CSS, sustituyéndolas por el método que prefieras para manejar estilos.

### Estructura del Proyecto

En la raíz del proyecto, encontrarás varios archivos de configuración y otros elementos que podemos ignorar por el momento. Por ahora, nos centraremos en la carpeta `src` y su contenido.

```bash
├── src/
│   └── app/
│       ├── globals.css
│       ├── favicon.ico
│       ├── layout.tsx
│       └── page.tsx
└── api.ts
```

- `globals.css`: Este archivo contiene estilos globales para la aplicación, incluyendo los estilos de Tailwind CSS.
- `favicon.ico`: Icono predeterminado de la aplicación, visible en la pestaña del navegador.
- `layout.tsx`: Este archivo, específico de Next.js, nos permite definir un envoltorio para nuestra aplicación o página. En este caso, se encarga de establecer la estructura básica de la página (html y body), importar estilos globales, y agregar un encabezado, un pie de página y un contenedor para el contenido de la página. Recibe una prop `children`, que representa el contenido de la página que verá el usuario.
- `page.tsx`: Otra característica especial de Next.js que nos permite definir una página. Dado que está en la raíz de nuestro directorio `app`, será la página que se mostrará al usuario al acceder al inicio (ruta `/`).
- `api.ts`: Este archivo define algunos métodos que utilizaremos a lo largo del curso para obtener información sobre restaurantes. Por ahora, solo devuelve datos de prueba, pero más adelante lo emplearemos para obtener datos reales.

Tómate un tiempo para modificar el contenido de estos archivos y observa cómo afecta a la aplicación. Mientras el servidor de desarrollo esté en ejecución, bastará con guardar un archivo para ver los cambios reflejados en la pantalla.

## Ambientes de renderizado (Servidor y Cliente)
Hay [dos ambientes](https://nextjs.org/docs/app/building-your-application/rendering#rendering-environments) donde las aplicaciones web se pueden renderizar: el cliente y el servidor.

![](https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fclient-and-server-environments.png&w=3840&q=75&dpl=dpl_DzaGxTbCZzXMDg4XPPbArRct6JPH)

El `cliente` se refiere al navegador en el dispositivo del usuario, que envía una petición al `servidor` para recibir el código de tu aplicación y la convierte en una interfaz visual para el usuario.

El `servidor` se refiere a una computadora en un data center que almacena el código de tu aplicación y recibe peticiones de los clientes, devolviendo una respuesta.

Podemos pensar al `servidor` como el lugar donde comienzan las cosas, está oculto del usuario y tenemos acceso a nuestros secretos y credenciales. El `cliente` es donde terminan las cosas y tenemos acceso a información del usuario, como su navegador, datos y más.

Ayuda el pensar esta transición como un flujo unidireccional del servidor al cliente. Una vez que una petición se termina de ejecutar en el servidor y pasa al cliente, no puede volver al servidor (si necesitás volver al servidor, haces una nueva petición, por ejemplo accediendo a una nueva ruta), a esta línea imaginaria que separa el servidor del cliente se la conoce como `network boundary`.

Este concepto podría no resultar del todo claro en este momento, pero cobrará mayor sentido a medida que adquiramos más práctica.

### Server Components
Por defecto, todos los componentes creados en la carpeta `app` son [React Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components). Los Server Components son componentes que se ejecutan solamente en el servidor y tienen como objetivo describir como debería verse una porción de nuestra interfaz. Los Server Components solo se ejecutan cuando el usuario accede a una ruta o segmento y no se vuelven a ejecutar nuevamente en el cliente, el cliente solo los muestra (recordemos que una vez que se termina de ejecutar la petición en el servidor, no puede volver). Esto quiere decir que no pueden manejar eventos del usuario, estados locales, ni hooks, pero pueden acceder directamente a datos de servidor, base de datos, variables de entorno privadas, y todo lo que se pueda hacer en el servidor.

Sin embargo, una aplicación tradicional se compone también de componentes dinámicos e interactivos que requieren interacciones del usuario, eventos y más. Para eso podemos usar `Client Components`. Los Server Components pueden importar y usar Client Components pero los Client Components no pueden importar Server Components. No te preocupes si esto todavía no hace sentido, vamos a verlo en acción más adelante.

Podemos usar Server Components dentro de Server Components de manera indefinida, pero, en el momento en el que usamos un Client Component, delimitamos nuestro `network boundary`.

Si intentamos usar un hook o suscribirnos a un evento en un Server Component vamos a obtener un error.

```jsx
import { useState } from 'react' // 🚨 ReactServerComponentsError 🚨: You're importing a component that needs useState. It only works in a Client Component but none of its parents are marked with "use client", so they're Server Components by default.

export default function Page() {
  return (...)
}
```

Ahora la pregunta del millón, ¿por qué renderizariamos algo en el servidor? Bueno, acá un listado de beneficios sobre ejecutar cosas en el servidor:
- Obtención de datos: Podemos obtener nuestros datos desde un servidor más cercano a nuestro orígen de datos, haciendo la obtención más rápida y eficiente.
- Seguridad: Al ejecutar desde el servidor podemos mantener toda la data sensible como tokens, credenciales y más, ocultas del usuario.
- Caching: Cuando cacheamos datos en el cliente ese caché es único para cada usuario, en cambio, cuando cacheamos datos en el servidor, ese caché es compartido entre todos los usuarios, lo que nos permite ahorrar recursos y mejorar la performance de nuestra aplicación.
- Bundle size: Mucho del trabajo que antes debíamos hacer en el cliente ahora lo podemos hacer en el servidor, minimizando la cantidad de código que debemos enviar al cliente.
- Pintado inicial y FCP (First Contentful Paint): En el servidor podemos generar HTML y CSS que se envía al cliente de manera inmediata sin necesidad de esperar que el JavaScript se descargue y ejecute en el cliente.
- SEO: El HTML renderizado por el servidor puede ser usado por los motores de búsqueda para indexar nuestra aplicación.
- Streaming: Podemos enviar contenido al cliente a medida que se va generando, en vez de esperar a que se genere todo el contenido para enviarlo al cliente. Esto permite al usuario ver el contenido más rápido.

### Client Components
Los `Client Components` nos permiten escribir interfaces interactivas y dinámicas que se ejecutan en el cliente. Los Client Components pueden usar hooks, estados locales, eventos, APIs del navegador y más. Podemos pensar a los Client Components como "los componentes de siempre", los componentes de React que solemos usar en nuestras aplicaciones con Vite o Create React App (pero con algunas diferencias, como que se renderizan una vez en el servidor antes de renderizarse en el cliente, podés leer más [acá](https://nextjs.org/docs/app/building-your-application/rendering/client-components#how-are-client-components-rendered)).

Para marcar un componente como Client Component, debemos agregar la directive `"use client"` al inicio del archivo. 

```jsx
'use client'

import { useState } from 'react'

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  )
}
```

### Cuando usar Server Components y Client Components
Si bien hay excepciones para cada uno, esta lista resumen cuando deberías usar cada uno la mayoría de las veces.

| ¿Qué debes hacer?                                                                                     | Componente del Servidor  | Componente del Cliente |
| ----------------------------------------------------------------------------------------------------- | ------------------------ | ---------------------- |
| Obtener datos                                                                                         | ✅                       | ⛔                     |
| Acceder a recursos del backend (directamente)                                                         | ✅                       | ⛔                     |
| Mantener información sensible en el servidor (tokens de acceso, claves API, etc.)                     | ✅                       | ⛔                     |
| Mantener dependencias grandes en el servidor / Reducir JavaScript del lado del cliente                | ✅                       | ⛔                     |
| Agregar interactividad y escuchadores de eventos (`onClick()`, `onChange()`, etc.)                    | ⛔                       | ✅                     |
| Utilizar Estado y Efectos del Ciclo de Vida (`useState()`, `useReducer()`, `useEffect()`, etc.)       | ⛔                       | ✅                     |
| Utilizar APIs exclusivas del navegador                                                                | ⛔                       | ✅                     |
| Utilizar hooks personalizados que dependen del estado, efectos o APIs exclusivas del navegador        | ⛔                       | ✅                     |
| Utilizar [Componentes de Clase de React](https://react.dev/reference/react/Component)                 | ⛔                       | ✅                     |

## Mostrando los restaurantes
Ahora que ya tenemos un poco de teoría, vamos a ver realmente como usar Server Components en nuestra aplicación. ¿Recordás el archivo `api.ts` que dijimos que ibamos a usar para obtener datos? Bueno, ahora vamos a usarlo. Si abrimos el archivo vamos a ver que define una interfaz para `Restaurant` con algunos campos.

```ts
interface Restaurant {
  id: number;
  name: string;
  image: string;
  description: string;
  address: string;
  score: number;
  ratings: number;
}
```

También hay un objeto `api` con un método `list` que nos devuelve una `Promise` con un array de `Restaurant`. Vamos a ver como podemos usar ese método en nuestro Server Component `page.tsx`.

```jsx
import api from "@/api";

export default async function Home() {
  const restaurants = await api.list();

  console.log(restaurants);

  return (...);
}
```

Si ahora miramos la consola (no la del navegador, sino la terminal, donde corrimos `npm run dev`) vamos a ver un listado de `Restaurant`. Pero, ¡¿cómo es posible este suceso?! 🤯

Como dijimos antes, los Server Components no se vuelven a renderizar. Por ende podemos convertir nuestro componente en una función asíncrona y esperar a que la `Promise` se resuelva con los datos de los restaurantes y en la línea de abajo podemos usar esos datos para renderizarlos en nuestra página. Vamos a iterar sobre `restaurants` y devolver una grilla de restaurantes mostrando su imágen, título, descripción y rating.

```jsx
import api from "@/api";

export default async function Home() {
  const restaurants = await api.list();

  return (
    <section className="grid grid-cols-1 gap-12 md:grid-cols-2 lg:grid-cols-3">
      {restaurants.map((restaurant) => {
        return (
          <article key={restaurant.id}>
            <img
              alt={restaurant.name}
              className="mb-3 h-[300px] w-full object-cover"
              src={restaurant.image}
            />
            <h2 className="inline-flex gap-2 text-lg font-bold">
              <span>{restaurant.name}</span>
              <small className="inline-flex gap-1">
                <span>⭐</span>
                <span>{restaurant.score}</span>
                <span className="font-normal opacity-75">({restaurant.ratings})</span>
              </small>
            </h2>
            <p className="opacity-90">{restaurant.description}</p>
          </article>
        );
      })}
    </section>
  );
}
```

Y el resultado es el siguiente:
![Listado de restaurantes](./images/restaurants-grid.jpg)

Entonces, aprendimos que además de ejecutarse en el servidor y todos los beneficios que contamos antes, los Server Components pueden usar `async await` y nos ayudan a reducir el boilerplate y complejidad de nuestra aplicación al obtener datos.

> Bonus: Dale tu propio toque mágico de estilos a la grilla de restaurantes.

## Mostrando un restaurante
Ahora vamos a crear una ruta para poder visualizar cada restaurant de manera individual. Para eso primero tenemos que entender un poco más como funciona el router de Next.js, y conocer algunas de sus convenciones de archivos.

### Router
Next.js con App Directory posee un router construido sobre React Server Components, el cual soporta layouts compartidos, enrutamiento anidado, estados de carga, manejo de errores, y mucho más. El enrutamiento de App Router está basado en archivos, lo que significa que podemos crear rutas y segmentos simplemente creando archivos y carpetas. Ahora lo importante, qué archivos y carpetas tenemos que crear? Bueno, ya sabemos de la existencia de `layout.tsx` y `page.tsx`, pero cómo podemos usarlos para crear otras rutas? Qué otras convenciones existen? Veamos algunas de las que vamos a usar en este curso:

- `layout.tsx`: Envuelve a un `page.tsx`, nos permite compartir un layout entre varias páginas.
- `page.tsx`: Define una página, recibe por props parámetros, y parámetros de búsqueda.
- `loading.tsx`: Página de carga, se muestra mientras se está cargando una página, cuando la página termina de cargar, se reemplaza por el contenido de `page.tsx`.
- `error.tsx`: Página de error, se muestra al haber una excepción o error en la ejecución de una página o layout.
- `route.tsx`: Define una ruta de API, se ejecuta en el servidor y devuelve datos usando un objeto `Response`.

Eso debería ser suficiente por ahora en tanto a archivos (si querés ver todos, podés hacerlo [acá](https://nextjs.org/docs/app/building-your-application/routing#file-conventions))

### Rutas dinámicas
Si bien vimos varios archivos, más arriba hablamos también de carpetas y de anidarlas. Como hacemos para crear una ruta para mostrar un restaurant basado en su `id`? De la siguiente manera:

```bash
├── src/
│   └── app/
│       ├── globals.css
│       ├── layout.tsx
│       ├── page.tsx
│       └── [id]/
│           └── page.tsx
└── api.ts
```

Creemos la carpeta y archivo `src/app/[id]/page.tsx` y agreguemos el siguiente contenido:

```jsx
import api from "@/api";

export default async function RestaurantPage({params: {id}}: {params: {id: string}}) {
  const restaurant = await api.fetch(id);

  return (
    <article key={restaurant.id}>
      <img
        alt={restaurant.name}
        className="mb-3 h-[300px] w-full object-cover"
        src={restaurant.image}
      />
      <h2 className="inline-flex gap-2 text-lg font-bold">
        <span>{restaurant.name}</span>
        <small className="inline-flex gap-1">
          <span>⭐</span>
          <span>{restaurant.score}</span>
          <span className="font-normal opacity-75">({restaurant.ratings})</span>
        </small>
      </h2>
      <p className="opacity-90">{restaurant.description}</p>
    </article>
  );
}
```

Si ahora entramos a la ruta `/1` deberíamos ver algo así:
![Página de un restaurante](./images/restaurant-details.jpg)

Veamos como fue que pasó esto. Ya sabemos que los componentes por defecto son Server Components, así que hicimos que sea `async` y usamos nuestro método `api.fetch` para obtener los datos del restaurante. Además, aprendimos algo nuevo, el archivo `page.tsx` recibe como props una propiedad `params` que contiene los parámetros de la ruta. En este caso, como nuestra ruta es `/[id]`, el parámetro se llama `id`. Por lo tanto, podemos desestructurar `params` y obtener el `id`. Luego usamos ese `id` para obtener los datos del restaurante y renderizarlos en la página.

Ahora tenemos un pequeño problema: acabamos de repetir todo el código de la tarjeta del restaurant, podríamos crear un componente y reutilizarlo (te voy a dejar esa tarea a vos). Pero... ¿Dónde irían los componentes que no son páginas / layouts o archivos especiales?

### Colocación
Si bien el router de Next.js es basado en archivos, solamente los archivos con nombres especiales se convierten en rutas de nuestra aplicación, por ende podríamos crear una carpeta `components` dentro de `app` (o anidada donde la necesitemos) y no debería traernos ningún problema. Sin embargo, queda en vos como lo quieras hacer, si querés crear una carpeta `components` (o lo que quieras) fuera de `app` (pero dentro de `src`) podés hacerlo.

![](https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fproject-organization-colocation.png&w=3840&q=75&dpl=dpl_DzaGxTbCZzXMDg4XPPbArRct6JPH)

Ahora si, andá a crear ese componente y reutilizalo en `page.tsx` y `[id]/page.tsx`.

## Navegación
En Next.js tenemos el componente `Link`, que extiende la etiqueta `<a>` para agregarle funcionalidades de pre-carga y pre-renderizado. El componente `Link` nos permite navegar entre páginas de nuestra aplicación sin tener que recargar la página. Se usa de manera muy similar a la etiqueta `<a>` y lo podemos importar desde `next/link`. Agreguemos a nuestra grilla de restaurantes un link para poder navegar a la página de cada restaurante.

```jsx
import Link from "next/link";

import api from "@/api";

export default async function Home() {
  const restaurants = await api.list();

  return (
    <section className="grid grid-cols-1 gap-12 md:grid-cols-2 lg:grid-cols-3">
      {restaurants.map((restaurant) => {
        return (
            ...
              <Link href={`/${restaurant.id}`}>
                {restaurant.name}
              </Link>
            ...
        );
      })}
    </section>
  );
}
```

Bien, ahora te toca a vos. Agregá a la página de detalle del restaurante, un link para volver a la página de inicio y un link al header en el layout para que al clickearlo nos lleve al inicio.

## Estados de carga
Nuestras páginas cargan bastante rápido (estamos simulando un retardo de 750ms), vayamos a `api.ts` y cambiemos ese `750` por `7500`. Si recargamos, vemos efectivamente que la página tarda 7.5 segundos en cargar. El problema es que mientras la página carga, el usuario no ve nada y no sabe si la página no anda, si su internet anda mal o que está pasando. En Next.js podemos definir un archivo `loading.tsx`, el cual está construido sobre [React Suspense](https://react.dev/reference/react/Suspense). Mientras nuestra página esté suspendida (mientras haya operaciones bloqueantes como un `await` de un Server Component asíncrono) se va a mostrar el contenido de `loading.tsx`. Una vez que esas operaciones terminen, se va a reemplazar el contenido de `loading.tsx` por el contenido de `page.tsx`. Esto nos permite no solamente mostrarle al usuario que "algo está cargando" sino que también nos permite enviar todas las partes de nuestra aplicación que no dependan de esas operaciones bloqueantes, como los componentes que ya terminaron sus operaciones, los layouts y más.

Vamos a crear el archivo `src/app/loading.tsx` y agreguemos el siguiente contenido:

```jsx
export default function Loading() {
  return (
    <div>Loading...</div>
  );
}
```

Ahora si recargamos la página, vamos a ver que mientras se está cargando, se muestra el texto "Loading..." y una vez que termina de cargar, se reemplaza por el contenido de `page.tsx`. Pero, también vemos que si vamos a la ruta `/1`, también se muestra el texto "Loading...", por qué si el `loading.tsx` está definido en la raíz de nuestro proyecto? Esto sucede por que `loading.tsx` es una abstracción sobre React Suspense, cuando una parte de nuestra aplicación se suspenda, va a buscar hacia arriba el Suspense Boundary más cercano y va a usarlo. Si quisieramos, podríamos definir un `loading.tsx` dentro de `[id]` y se usaría en vez del de la raíz, pero por ahora estamos bien con este.

## Manejo de errores
De momento nuestra aplicación usa datos de prueba por lo que es poco probable que ocurran errores, pero puede ser que alguien intente acceder a una página que no existe o que simplemente queramos estar preparados para el día de mañana. Vamos a crear el archivo `src/app/error.tsx` y agreguemos el siguiente contenido:

```jsx
'use client'

export default function ErrorPage({error}: {error: Error}) {
  console.error(error);

  return (
    <div>Something went wrong, try again!</div>
  )
}
```

Si intentamos de entrar a una ruta inexistente, como `/123` vamos a ver una ventana de error (en desarrollo) y el contenido de nuestra página de error correctamente. Un detalles es que el archivo `error.tsx` siempre debe ser un Client Component, ya que recibe por props, opcionalmente, una función `reset` a la que podemos llamar para intentar re-renderizar nuestra página con el mismo input que tenía.

El archivo `error.tsx` funciona con un React Error Boundary cuyo comportamiento es similar al Suspense Boundary, buscando hacia arriba el Error Boundary más cercano. Por ende si algo falla en `/1` o en `/` se va a usar el mismo `error.tsx`.

## Usando una base de datos
Vamos a mover nuestros datos de prueba a una base de datos para poder modificarlos cuando queramos, en este caso vamos a usar Google Sheets, ya que es fácil, gratis y sin configuración, vos podés usar la base de datos que quieras! Para eso vamos a [https://sheets.new](https://sheets.new) y creamos una nueva hoja con los mismos datos que nuestra data de prueba.

Podes usar ChatGPT para convertir la data de prueba, igual soy bueno y te lo dejo acá abajo (copialo, pegalo en la primer celda de google sheets y seleccioná "dividir texto en columnas")

```csv
id,name,description,address,score,ratings,image
1,The Golden Spoon,"A fine dining experience with a menu that changes daily based on the freshest ingredients available.",123 Main St. Anytown USA,4.5,100,https://source.unsplash.com/480x300/?restaurant&random=1
2,La Piazza,"Authentic Italian cuisine in a cozy atmosphere with outdoor seating available.",456 Oak Ave. Anytown USA,4.2,80,https://source.unsplash.com/480x300/?restaurant&random=2
3,The Sizzling Skillet,"A family-friendly restaurant with a wide variety of dishes. including vegetarian and gluten-free options.",789 Elm St. Anytown USA,4.8,120,https://source.unsplash.com/480x300/?restaurant&random=3
4,The Hungry Bear,"A rustic cabin-style restaurant serving hearty portions of comfort food.",101 Forest Rd. Anytown USA,4.0,60,https://source.unsplash.com/480x300/?restaurant&random=4
5,The Spice Route,"A fusion restaurant that combines the flavors of India. Thailand. and China.",246 Main St. Anytown USA,4.6,90,https://source.unsplash.com/480x300/?restaurant&random=5
6,The Catch of the Day,"A seafood restaurant with a focus on locally-sourced. sustainable ingredients.",369 Beach Blvd. Anytown USA,4.3,70,https://source.unsplash.com/480x300/?restaurant&random=6
7,The Garden Cafe,"A vegetarian restaurant with a beautiful outdoor garden seating area.",753 Maple St. Anytown USA,4.9,150,https://source.unsplash.com/480x300/?restaurant&random=7
8,The Burger Joint,"A classic American diner with a wide variety of burgers. fries. and milkshakes.",852 Oak Ave. Anytown USA,3.9,50,https://source.unsplash.com/480x300/?restaurant&random=8
9,The Cozy Corner,"A small cafe with a warm and inviting atmosphere. serving breakfast and lunch dishes.",963 Main St. Anytown USA,4.7,110,https://source.unsplash.com/480x300/?restaurant&random=9
10,The Steakhouse,"A high-end restaurant specializing in premium cuts of beef and fine wines.",1479 Elm St. Anytown USA,4.1,75,https://source.unsplash.com/480x300/?restaurant&random=10
11,The Taco Truck,"A casual Mexican restaurant serving authentic street tacos.",753 Main St. Anytown USA,4.4,65,https://source.unsplash.com/480x300/?restaurant&random=11
12,The Ice Cream Parlor,"A family-friendly restaurant with a wide variety of ice cream flavors.",852 Oak Ave. Anytown USA,4.9,150,https://source.unsplash.com/480x300/?restaurant&random=12
```

Luego, para poder acceder a esta data desde nuestra app, debemos ir a `Archivo > Compartir > Publicar en la web`, publicar y copiar el link que nos da para acceder a la data en formato `.csv`.

![](./images/share-web-0.jpg)
![](./images/share-web-1.jpg)

Una vez que tengamos el link, vamos a nuestro `api.ts` y vamos a cambiar nuestro método `list` para que use la data de Google Sheets.

```ts
const api = {
  list: async (): Promise<Restaurant[]> => {
    // Obtenemos la información de Google Sheets en formato texto y la dividimos por líneas, nos saltamos la primer línea porque es el encabezado
    const [, ...data] = await fetch('...').then(res => res.text()).then(text => text.split('\n'))

    // Convertimos cada línea en un objeto Restaurant, asegurate de que los campos no posean `,`
    const restaurants: Restaurant[] = data.map((row) => {
      const [id, name, description, address, score, ratings, image] = row.split(',')
      return {
        id,
        name,
        description,
        address,
        score: Number(score),
        ratings: Number(ratings),
        image
      }
    })

    // Lo retornamos
    return restaurants;
  },
  ...
}
```

¡Listo! Ahora si recargamos la página deberíamos ver los datos de Google Sheets. Ten en cuenta que Next.js maneja su propio caché, así que si no ves los cambios probá con <kbd>ctrl</kbd> + <kbd>f5</kbd> (<kbd>cmd</kbd> + <kbd>f5</kbd> si usas Mac). Ahora te dejo a vos modificar el método `fetch` para traer los datos de un restaurante en particular.

## Buildeando nuestra aplicación
Ahora que tenemos una aplicación más o menos completa, vamos a compilarla y correrla en local para ver más acertadamente que tan bien funcionaría en un entorno productivo. Para eso vamos terminar el comando de nuestro servidor de desarrollo y ejecutamos los siguientes comandos:

```bash
npm run build
npm start
```

Luego de unos segundos vamos a ver algo como esto:

![](./images/build-output.jpg)

Si vamos a `http://localhost:3000` deberíamos ver nuestra aplicación funcionando. ¡Y funciona! Pero... Si vamos a la ruta `/` no se muestra el componente de carga, todo funciona, como por arte de mágia, pero ¿por qué? Antes intentemos algo, vayamos a nuestra hoja de Google Sheets, actualicemos un título, volvamos a nuestra app y recarguemos, con <kbd>ctrl</kbd> + <kbd>f5</kbd>.

Mmm... No funciona.

Vayamos a la ruta del elemento que modificamos. Mmm... acá si funciona, hasta se muestra el componente de carga. Si volvemos al index la data no concuerda. ¿Qué está pasando?

Veamos devuelta la imágen de más arriba:

![](./images/build-output.jpg)

Podemos ver que la ruta de `/` tiene un ícono de `○` (abajo nos dice que significa estático)
Mientras que nuestra ruta de `/[id]` tiene un ícono de `λ` (abajo nos dice que significa server)

## Estrategias de renderizado
En Next.js tenemos dos principales estrategias de renderizado, estática y dinámica.

### Renderizado estático (por defecto)
Con renderizado estático nuestras rutas se renderizan en tiempo de compilación, esto permite que los datos estén disponibles desde la primer visita de un usuario. Estos datos se persisten a lo largo del tiempo y las siguientes visitas de un usuario no impactaran en nuestro origen de datos. Esto nos permite tener una aplicación con un tiempo de carga muy rápido y un bajo consumo de recursos.

El renderizado estático es muy útil para páginas que no cambian frecuentemente o no incluyen información personalizada sobre el usuario. También podemos combinar el renderizado estático con obtener data desde el cliente para crear aplicaciones dinámicas y rápidas.


Nuestra ruta `/` tuvo un renderizado estático por defecto, pero ¿por qué nuestra ruta de `/[id]` no? Bueno, porque Next.js no sabe cuales son los `id` de nuestros restaurantes, por ende no puede renderizarlos en tiempo de compilación. Pero, si en nuestrá página `/[id]/page.tsx` definimos una función [`generateStaticParams`](https://nextjs.org/docs/app/api-reference/functions/generate-static-params) que devuelva los ids, los va a generar en tiempo de compilación de manera estática:

```jsx
export async function generateStaticParams() {
  const restaurants = await api.list()
 
  return restaurants.map((restaurant) => ({
    id: restaurant.id,
  }))
}
```

> También podemos exportar una variable `dynamicParams` como `false` en nuestra página, si queremos que devuelva un 404 para cualquier ruta no definida en `generateStaticParams`

### Renderizado dinámico
Con renderizado dinámico nuestras rutas se renderizan cada vez que un usuario ingresa a ellas. El renderizado dinámico es útil cuando una ruta contiene información personalizada de un usuario, cuando la información de la página no puede calcularse antes de tiempo, o cuando la información cambia de manera muy frecuente.

Para optar una ruta a renderizado dinámico podemos estipular configuraciones de caching a nivel `fetch`, ruta / segmento, o al usar funciones dinámicas, hablaremos de esto en la proxima sección.

## Caching
Cuando trabajamos con aplicaciones React en Vite o Create React App, solemos lidiar con un solo cache, el cache del navegador. En Next.js tenemos muchos tipos de cache diferente:

Aquí tienes la traducción al español de la tabla MDX:

| Mecanismo                    | Qué                             | Dónde    | Propósito                                                  | Duración                                    |
| ---------------------------- | ------------------------------- | -------- | ---------------------------------------------------------- | ------------------------------------------- |
| Memorización de Solicitudes  | Valores de retorno de funciones | Servidor | Reutilizar datos en un árbol de componentes React          | Duración de la solicitud                    |
| Caché de Datos               | Datos                           | Servidor | Almacenar datos entre solicitudes de usuario y despliegues | Persistente (puede ser validado nuevamente) |
| Caché de Ruta Completa       | HTML y carga RSC                | Servidor | Reducir el costo de renderización y mejorar el rendimiento | Persistente (puede ser validado nuevamente) |
| Caché de Enrutamiento        | Carga RSC                       | Cliente  | Reducir las solicitudes al servidor durante la navegación  | Sesión de usuario o basado en el tiempo     |

Next.js por defecto intentará de cachear tanto como sea posible para mejorar el rendimiento y reducir los costos. Cuando tenemos un segmento dinámico pero una petición de datos todavía tiene cache relevante, en vez de ir al orígen, Next.js intentará de obtenerlo desde el cache de datos, abajo podemos ver un diagrama de como funcionan los diferentes tipos de cache.

![](https://nextjs.org/_next/image?url=%2Fdocs%2Fdark%2Fcaching-overview.png&w=3840&q=75&dpl=dpl_Ejtt9BCyCFNeRJdBoVsM9Es9x8xe)

El comportamiento del cache va a depender de si tu ruta tiene renderizado estático o dinámico, los datos están cacheados o no o si un request es parte de una visita inicial o una navegación subsecuente. Esto puede marear un poco pero con el tiempo y práctica vamos a ver que los beneficios son muchos.

> Saber esto sobre caching ayuda a entender como Next.js funciona, pero no es contenido esencial para ser productivo en Next.js.

### Configuraciones de revalidación de cache
No siempre queremos contenido 100% estático o 100% dinámico, por eso tenemos varias maneras de estipular cómo queremos que se maneje el cache.

#### `cache: no-store`
Definir la propiedad `cache: 'no-store'` en un fetch que se use en una página o segmento. Por ejemplo ir a nuestro `api.ts` y actualizar nuestro fetch de `list` de la siguiente manera:

```ts
const [, ...data] = await fetch('...', { cache: 'no-store' }).then(res => res.text()).then(text => text.split('\n'))
```

Esto le va a indicar a Next.js que cada vez que una ruta deba obtener los datos de `list`, no debe usar la caché de datos. Para probar si funcionó, terminá el servidor(<kbd>ctrl</kbd> + <kbd>c</kbd> / <kbd>cmd</kbd> + <kbd>c</kbd>), y volvé a ejecutar:

```bash
npm run build
npm start
```

![](./images/build-output.jpg)

Ahora no solo debería funcionar, sino que podemos ver en el build output que la ruta `/` está marcada como `server`.

#### `revalidate: number`
Si no queremos que cada petición traiga información nueva cada vez, sino que queremos que "revalide" esa información cada cierto tiempo, podemos definir la propiedad `revalidate` en nuestros `fetch` de la siguiente manera:

```ts
const [, ...data] = await fetch('...', { revalidate: 100 }).then(res => res.text()).then(text => text.split('\n'))
```

Eso va a hacer que cada luego de 100 segundos de haber obtenido los datos, la próxima vez que un usuario ingrese a la ruta, se le van a servir datos de caché y en segundo plano se van a obtener datos nuevos, van a sobre-escribir la caché y la próxima vez que un usuario ingrese a la ruta, se le van a servir los datos nuevos. A esto se lo conoce como `time-based revalidation`.

#### Configuración de segmento de ruta
Las rutas pueden exportar constantes de configuración para definir ciertos comportamientos, incluyendo la revalidación y estrategia de renderizado. Podríamos hacer lo siguiente en nuestro `page.tsx`:

```tsx
export const dynamic = 'force-dynamic' // default: auto
export const revalidate = 100 // default: false
```

Existen muchas otras configuraciones las cuales podés ver [acá](https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config).

Ahora, si definimos `force-dynamic`, `revalidate` en 100 y en el fetch le ponemos `revalidate` en 50. ¿Qué configuración se sobrepone al resto? La respuesta es fácil, la de menor revalidación, en este caso como definimos `force-dynamic` los datos se van a obtener de origen en cada petición. Igualmente no suele ser algo por lo que tengamos que preocuparnos, Next.js siempre va a optimizar lo más posible para que nuestra aplicación sea lo más rápida posible.

#### Funciones dinámicas
También hay funciones a las que se las denomina [funciones dinámicas](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-functions). Las funciones dinámicas dependen de información de la petición, como [`cookies`](https://nextjs.org/docs/app/api-reference/functions/cookies), [`headers`](https://nextjs.org/docs/app/api-reference/functions/headers), [`useSearchParams`](https://nextjs.org/docs/app/api-reference/functions/use-search-params) y [`searchParams`](https://nextjs.org/docs/app/api-reference/file-conventions/page#searchparams-optional). Al usar alguna de estas funciones en nuestros segmentos (o funciones llamadas dentro de nuestros segmentos) la ruta optará por un renderizado dinámico.

### Revalidación manual
La revalidación por tiempo es útil pero no para todos los casos, a veces tenemos datos que no cambian muy seguido pero cuando cambian queremos que se actualicen de inmediato. Por ejemplo, un producto en una tienda virtual que cambió su precio luego de 15 días y queremos que los usuarios vean el nuevo precio inmediatamente. Para eso podemos usar dos métodos que se ejecutan del lado del servidor [`revalidatePath`](https://nextjs.org/docs/app/api-reference/functions/revalidatePath) y [`revalidateTag`](https://nextjs.org/docs/app/api-reference/functions/revalidateTag).

#### `revalidatePath`
Nos permite revalidar el contenido de una ruta en particular, por ejemplo, nuestra ruta `/` si sabemos que agregamos nuevos restaurantes a la base de datos. Como nuestra aplicación no tiene un formulario para agregar nuevos restaurantes o modificar existentes, vamos a crear una ruta de API (Route Handler) utilitaria para que al llamarla, se revalide la ruta `/`.

Para eso vamos a crear un archivo `src/app/api/revalidate/route.ts` con el siguiente contenido:

```ts
import { revalidatePath } from "next/cache";

export async function GET() {
  revalidatePath('/')

  return Response.json({success: true})
}
```

En un Route Handler podemos exportar funciones con los nombres de los métodos HTTP habituales y se van a llamar cuando la ruta reciba una petición de ese mismo método.

Ahora podemos volver eliminar todos los `revalidate`, `dynamic` y cualquier cosa que haga nuestra ruta `/` dinámica y volver a compilar y correr nuestra aplicación. Si vamos a `http://localhost:3000` deberíamos ver nuestros restaurantes. Luego modifiquemos uno en la base de datos, vayamos manualmente a `http://localhost:3000/api/revalidate` y volvamos a `http://localhost:3000`. Deberíamos ver los datos actualizados.

> Tomá en cuenta que Google Sheets aveces tarda un poco en reflejar los datos publicados así que dale unos segundos.

Es una buena práctica proteger nuestras rutas de API con alguna clave secreta para evitar que usuarios malintencionados ejecuten estos métodos. Tu taréa es definir una variable de entorno `REVALIDATE_SECRET` y usarla en nuestra ruta de API para solo ejecutarla cuando nos manden un parametro `secret` con el valor correcto. Podés usar la documentación oficial de Next.js para ver como usar variables de entorno.

#### `revalidateTag`
También puede pasar que modifiquemos un dato que afecte varias rutas al mismo tiempo y cuando las aplicaciones crecen es muy difícil poder saber que rutas se ven afectadas por un cambio. Para eso podemos usar `revalidateTag` que nos permite revalidar todas las rutas que tengan un tag en particular.

Agreguemos un tag `restaurants` a nuestros dos llamados en `api.ts`, asi cuando revalidemos el tag `restaurants` se revalidará el contenido tanto para `/` como para cada `/[id]`.

```ts
const [, ...data] = await fetch('...', {next: {tags: ['restaurants']}}).then(res => res.text()).then(text => text.split('\n'))
```

Ahora actualizamos nuestra ruta de API utilitaria para usar `revalidateTag` y listo:

```ts
import { revalidateTag } from "next/cache";

export async function GET() {
  revalidateTag('restaurants')

  return Response.json({success: true})
}
```

## Parámetros de URL
Manejar estado de nuestra aplicación en la URL es una buena práctica, nos permite compartir links, volver a una página en particular y más. También nos permite delegar en el router el manejo de la navegación y seguir usando Server Components a pesar de tener interactividad en nuestra aplicación (ya que al cambiar la ruta hacemos otra petición).

Vamos a crear un componente `src/app/components/SearchBox.tsx` que contenga un campo, dentro de un formulario. Al hacer submit del formulario vamos a actualizar la URL con el valor del campo y dejar a Next.js hacer el resto. Vamos a agregarle el siguiente contenido:

```tsx
'use client'

import { useRouter, useSearchParams } from "next/navigation";

export default function SearchBox() {
  const {push} = useRouter()
  const searchParams = useSearchParams()

  function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
    // Prevenimos que la página se refresque al enviar el formulario
    event.preventDefault();

    // Obtenemos el valor del input
    const query = event.currentTarget.query.value;

    // Redireccionamos al index con una query
    push(`/?q=${query}`);
  }

  return (
    <form onSubmit={handleSubmit} className="inline-flex gap-2 mb-4">
      {/* Inicializamos el input para que contenga el valor actual de la query */}
      <input defaultValue={searchParams.get('q') || ''} className="px-2" name="query" />
      <button className="p-2 bg-white/20">Search</button>
    </form>
  );
}
```
> Al necesitar interactividad, nuestro componente debe ser un Client Component

Ahora agregamos la caja de búsqueda en nuestro `src/app/page.tsx` y probamos que funcione.

```tsx
...

import SearchBox from "./components/SearchBox";

export default async function Home() {
  const restaurants = await api.list();

  return (
    <section>
      <SearchBox />
      <section className="grid grid-cols-1 gap-12 md:grid-cols-2 lg:grid-cols-3">
        ...
  )
```

![](./images/search-box.jpg)

Bien, al hacer submit del formulario nos redirige correctamente, ahora hay que hacer que funcione la búsqueda. Para eso vamos a modificar nuestro `api.ts` para que tenga un método `search` que reciba un `query` y filtre los restaurantes por nombre o descripción:

```ts
const api = {
  ...,
  search: async (query: string): Promise<Restaurant[]> => {
    const results = await api.list();

    return results.filter((restaurant) => {
      return restaurant.name.toLowerCase().includes(query.toLowerCase());
    })
  }
}
```

> Como estamos obteniendo el contenido en `.csv` de Google Sheets no podemos hacer el filtrado en la API y debemos obtener todos los resultados y filtrarlos en el servidor. No es algo óptimo para una aplicación real pero dado que el `fetch` siempre va a ser igual nos vamos a beneficiar del Data Cache de Next.js en vez de descargarnos un nuevo `.csv` en cada búsqueda.

Y vamos a pasarle el `searchParams.q` (todas las `page` reciben la prop `searchParams`) a `api.search` en vez de `api.list` en nuestra `src/app/page.tsx`:

```tsx
export default async function Home({searchParams}: {searchParams: {q: string}}) {
  const restaurants = await api.search(searchParams.q);

  ...
}
```

> Utilizar `searchParams` en una `page` hace que el segmento sea dinámico ya que necesita ejecutarse en cada petición para obtener los valores correctos.

![](./images/search-box-1.jpg)

Bien! Nuestra búsqueda funciona correctamente. Pero... Si un usuario busca algo que no existe no se muestra nada. Asegurate de mostrar algun mensaje cuando no haya resultados como tarea.

## Agrupado de rutas
Esto es algo personal, pero ahora nos quedó una carpeta `components` dentro del directorio `app`, que tiene un solo archivo que es relavante para una sola página (`/app/page.tsx`), no me gusta que esté a nivel de `app` porque no es algo que se comparta entre todas las páginas. Podríamos sacar la carpeta `components` fuera de `app` pero pasaría lo mismo. Por suerte en App Directory podemos [agrupar rutas](https://nextjs.org/docs/app/building-your-application/routing/route-groups) y archivos de la siguiente manera:

```bash
└── app/
    ├── globals.css
    ├── layout.tsx
    ├── loading.tsx
    ├── error.tsx
    ├── api/
    │   └── route.ts
    ├── [id]/
    │   └── page.tsx
    └── (index)
        ├── components/
        │   └── SearchBox.tsx
        └── page.tsx
```
> (index) es solo un nombre, puede llamarse (loquequieras)

Al crear una carpeta envuelta en (parentesis) podemos no solamente acomodar mejor nuestros archivos sino que podríamos definir diferentes `layout` / `loading` / `error` para grupos de rutas que están a un mismo nivel (o hasta tener layouts anidados). Ahora nuestra carpeta components está colocada lo más cerca de donde es relevante posible. No te olvides de actualizar las importaciones para que nuestra aplicación siga funcionando.

## Server Actions
Mmm... Ahora que me doy cuenta puede ser que no necesitemos un Client Component o un componente de búsqueda. Podríamos usar un Server Action directamente en `src/app/page.tsx`.

Los [Server Actions](https://nextjs.org/docs/app/api-reference/functions/server-actions) nos permiten ejecutar código del lado del servidor cuando el usuario envía un formulario. Nos da acceso a los datos incluidos en ese formulario así que podríamos usarlo para hacer la búsqueda. Vamos a ir a `src/app/page.tsx` y vamos a reemplazar nuestro componente de búsqueda por lo siguiente:

```tsx
import { redirect } from "next/navigation";

export default async function Home({searchParams}: {searchParams: {q?: string}}) {
  const restaurants = await api.search(searchParams.q);

  async function searchAction(formData: FormData) {
    'use server'

    redirect(`/?q=${formData.get('query')}`);
  }

  return (
    <section>
      <form action={searchAction} className="inline-flex gap-2 mb-4">
        <input defaultValue={searchParams.q || ''} className="px-2" name="query" />
        <button className="p-2 bg-white/20">Search</button>
      </form>
      <section className="grid grid-cols-1 gap-12 md:grid-cols-2 lg:grid-cols-3">
        ...
```

Los Server Actions requieren que especifiquemos la directive `'use server'` en la función de nuestra acción (o en la parte superior del archivo si vamos a tener un archivo con muchas acciones). Luego pasamos esta función a la propiedad `action` de nuestro formulario. Al hacer submit del formulario se va a ejecutar la función `searchAction` y se va a redireccionar a la ruta `/` con el valor del campo `q` como query string.

> Ahora podés borrar la carpeta `components` y el grupo `(index)`. O mover el Server Action al componente `SearchBox`, decidí vos.

## Guardar en favoritos (localStorage)
Vamos a implementar la funcionalidad de guardar en favoritos. Para eso vamos a ir a nuestro componente de `RestaurantCard.tsx` (o como sea que lo hayas llamado de ejercicios anteriores, si no lo hiciste, crealo donde te parezca) y vamos a agregarle un botón de corazón que al clickearlo guarde el id del restaurante en localStorage.

```tsx
'use client'

import { Restaurant } from "@/types";
import Link from "next/link";

export default function RestaurantCard({restaurant}: {restaurant: Restaurant}) {
  const isFavourite = window.localStorage.getItem('favorites')?.includes(restaurant.id)

  return (
    <article>
      <img
        alt={restaurant.name}
        className="mb-3 h-[300px] w-full object-cover"
        src={restaurant.image}
      />
      <h2 className="inline-flex gap-2 text-lg font-bold items-center">
        <Link href={`/${restaurant.id}`}>
          <span>{restaurant.name}</span>
        </Link>
        <small className="inline-flex gap-1">
          <span>⭐</span>
          <span>{restaurant.score}</span>
          <span className="font-normal opacity-75">({restaurant.ratings})</span>
        </small>
        <button className={`text-red-500 text-xl ${isFavourite ? 'opacity-100' : 'opacity-20'}`}>♥</button>
      </h2>
      <p className="opacity-90">{restaurant.description}</p>
    </article>
  );
}
```

Nuestro componente va a ser un Client Component ya que necesitamos estar en el cliente para poder acceder a localStorage que es una API del navegador. Pero sin embargo vemos el siguiente error cuando renderizamos el componente:

![](./images/window-undefined.jpg)

### Pre-renderizado
En Next.js todos los componentes son pre-renderizados en el servidor por defecto. Esto significa que un componente (aunque sea un Client Component) va a ser ejecutado en el servidor y luego en el cliente. Esto nos permite generar una previsualización (no interactiva) mientras el JavaScript se descarga del lado del cliente, una vez que esto sucede, nuestra aplicación se hidrata y se vuelve interactiva.

Pero, al ser ejecutado en el servidor, no tenemos acceso a `window`, por eso tenemos que asegurarnos de que nuestro componente se renderice solamente en el cliente.

### Lazy loading
En Next.js podemos usar la función `dynamic` importada desde [`next/dynamic`](https://nextjs.org/docs/app/building-your-application/optimizing/lazy-loading#nextdynamic) para hacer lazy loading de nuestros componentes. Esto nos permite importar un componente de manera dinámica, solo cuando sea necesario. También nos permite definir si un componente debería o no ser renderizado en el servidor mediante la propiedad `ssr`.

Vamos a actualizar el código de nuestro componente `RestaurantCard` para que contenga dos componentes, uno para la información y uno para el botón de favorito. El componente de información va a ser pre-renderizado en el servidor y el componente de favorito va a ser renderizado solo en el cliente mediante `dynamic`.

```tsx
'use client'

import { Restaurant } from "@/types";
import dynamic from "next/dynamic";
import Link from "next/link";

function FavoriteButton({restaurant}: {restaurant: Restaurant}) {
  const isFavourite = window.localStorage.getItem('favorites')?.includes(restaurant.id)

  return (
    <button className={`text-red-500 text-xl ${isFavourite ? 'opacity-100' : 'opacity-20'}`}>♥</button>
  )
}

// Creamos un componente dinámico para que no se renderice en el servidor
const DynamicFavoriteButton = dynamic(async () => FavoriteButton, {ssr: false})

export default function RestaurantCard({restaurant}: {restaurant: Restaurant}) {

  return (
    <article>
      <img
        alt={restaurant.name}
        className="mb-3 h-[300px] w-full object-cover"
        src={restaurant.image}
      />
      <h2 className="inline-flex gap-2 text-lg font-bold items-center">
        <Link href={`/${restaurant.id}`}>
          <span>{restaurant.name}</span>
        </Link>
        <small className="inline-flex gap-1">
          <span>⭐</span>
          <span>{restaurant.score}</span>
          <span className="font-normal opacity-75">({restaurant.ratings})</span>
        </small>
        <DynamicFavoriteButton restaurant={restaurant} />
      </h2>
      <p className="opacity-90">{restaurant.description}</p>
    </article>
  );
}
```

Muy bien, si actualizamos la key `favorites` manualmente en localStorage para incluir el id de alguno de nuestros restaurantes lo vamos a ver correctamente:

![](./images/favorites.jpg)

Te dejo un par de tareas:
- Nuestro componente `RestaurantCard` contiene dos componentes, el componente que contiene la información no necesita ninguna actividad, por ende podría seguir siendo un Server Component. Mové el componente del botón de favorito a otro archivo e importalo.
  - Podrías convertir `RestaurantCard` en una carpeta y agregarle un `index.tsx` y un `FavoriteButton.tsx` dentro. De esa manera los componentes seguirían colocados lo más cerca de donde son relevantes posible. Pero manejalo a tu gusto.
- Implementá la funcionalidad de agregar y quitar favoritos en el botón de favorito. Al cargar la página debería mostrar el estado actual y al clickear el botón debería mostrarse actualizado y persistir ese estado al recargar la página.

---
Si te gusta mi contenido, seguime en [Twitter](https://twitter.gonzalopozzo.com), en [Twitch](https://twitch.gonzalopozzo.com), en [YouTube](https://youtube.gonzalopozzo.com), doname un [Cafecito](https://cafecito.gonzalopozzo.com) o volvete [sponsor en github](https://github.com/sponsors/goncy) ✨


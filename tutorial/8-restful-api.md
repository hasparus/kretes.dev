---
pos: 8
title: RESTful APIs
description: >
  Creating REST APIs using Kretes controllers & handlers
---

# RESTful APIs

It's time to move the application data server-side. This is needed as we want to (1) put it in a central location so that it's possible to share that data between users, and (2) because our server can easily integrate with a database to store and persiste that data over time.

Kretes allows to conveniently create REST (and GraphQL) APIs directly in the same application In Kretes, an API is a *set* of controllers. Each controller is responsible for a particular resource. In this tutorial, we are dealing with one resource so far: `Task`.

Controllers group together actions that respond to specific HTTP requests. Each action is represented by a separate file in the `Controller` directory of that resource. There is a file naming conventions so that you can quickly connect actions with specific HTTP requests without configuration. In our case, we need to create an action called `browse`. Check the X for details.

For starters, let's create an action that will be returing a collection of tasks in response to the `GET` request. We haven't yet configured the database, so temporarily let's keep this collection of tasks in the server memory as a regular constant with a predefined value.

```js
const collection = [
  { name: 'Task 1', done: false },
  { name: 'Task 2', done: false },
]
```

Now we are ready to create the action that will be returning this collection. First, in `features/Task/Controller/browse.ts` create the `browse` handler. As previously stated, naming for both the file name and the handler name is important. This way we can reduce the amount of configuration.

```ts
import { Handler, response } from 'kretes';

const { OK } = response;

const collection = [
  { name: 'Task 1', done: false },
  { name: 'Task 2', done: false },
]

export const browse: Handler = ({ }) => {
  return OK(collection);
}
```

This handler will respond to `GET` requests sent to `/_api/task`. You can test it by opening the `http://localhost:5544/_api/task` in your browser.

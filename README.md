# Health Care API - Prisma + Express + TypeScript Setup Guide

## at first we need to initialize the project

```bash
npm init -y
```

---

## 1st step: prisma setup

As we develop prisma based project so we need to setup prisma first.\
Link: [https://www.prisma.io/docs/getting-started/setup-prisma/start-from-scratch/relational-databases-typescript-prismaPostgres](https://www.prisma.io/docs/getting-started/setup-prisma/start-from-scratch/relational-databases-typescript-prismaPostgres)

Then follow the documentation:

```bash
npm install prisma typescript tsx @types/node --save-dev
```

Next, initialize TypeScript:

```bash
npx tsc --init
```

Then in `tsconfig.json` file I need to find `rootDir` and write:

```json
"rootDir": "./src",
"outDir": "./dist"
```

Initialize prisma:

```bash
npx prisma init
```

After that we get `.env` file and a folder named `prisma`.

Then I open `.env` folder and edit the given url link:

```env
DATABASE_URL="postgresql://postgress_user_name:password6@localhost:5432/database_name?schema=public"
```

---

## 2nd step: express setup

```bash
npm i express
```

---

## 3rd step: ts node dev setup as dev dependency

```bash
npm i ts-node-dev -D
```

---

## 4th step: cors setup

```bash
npm i cors
```

---

## 5th step: then create a folder named `src` in root directory and create a file inside `src` named `server.ts`

Then command:

```bash
npm i --save-dev @types/express
```

### For testing if server is running then we update `server.ts`

```ts
import express from 'express'

const app = express();
const port = 3000

app.listen(port, ()=>{
    console.log('app is listening', port);
})
```

### Then update `package.json` and add a script to run server:

```json
"scripts": {
  "dev": "ts-node-dev --respawn --transpile-only src/server.ts"
}
```

### Then command on terminal:

```bash
ts-node-dev --respawn --transpile-only src/server.ts
```

Now server setup done.

---

## **project setup: now I want to project setup**

I create a file inside `src` folder named `app.ts`

Then install:

```bash
npm i --save-dev @types/cors
```

### Update `app.ts`

```ts
import cors from "cors";
import express, { Application, Request, Response } from "express";

const app: Application = express();
app.use(cors());

app.get("/", (req: Request, res: Response) => {
  res.send({
    Message: "health care server",
  });
});

export default app;
```

### Import `app.ts` from `server.ts` and update `server.ts` like this:

```ts
import { Server } from "http";
import app from "./app";

const port = 3000;

async function main() {
  const Server: Server = app.listen(port, () => {
    console.log("health care app is listening on port", port);
  });
}

main();
```

---

> noted: we declear Server as a variable for the future because if the server crash or not responding then we need to handle this.


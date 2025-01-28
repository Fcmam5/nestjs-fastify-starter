<p align="center">
  <a href="https://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" height="120" alt="Nest Logo" /></a> + <a href="https://fastify.dev/" target="blank"> <img
      src="https://github.com/fastify/graphics/raw/HEAD/fastify-portrait.svg"
      width="120"
      alt="Fatify logo"
    />
    </a>
</p>

## Description

[Nest](https://github.com/nestjs/nest) framework TypeScript [using Fastify platform](https://docs.nestjs.com/techniques/performance) starter repository (forked from [`nestjs/typescript-starter`](https://github.com/nestjs/typescript-starter)).

### What did we change from `nestjs/typescript-starter`?

`src/main.ts` ([ref](https://docs.nestjs.com/techniques/performance)):

```diff
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
+ import {
+   FastifyAdapter,
+   NestFastifyApplication,
+ } from '@nestjs/platform-fastify';

async function bootstrap() {
+  const app = await NestFactory.create<NestFastifyApplication>(
+    AppModule,
+    new FastifyAdapter(),
  );

+  await app.listen(3000, '0.0.0.0');
}

bootstrap();
```

And `test/app.e2e-spec.ts` ([ref](https://stackoverflow.com/a/70041368/5078746)):

```diff
- import { INestApplication } from '@nestjs/common';
import { Test } from '@nestjs/testing';
import * as request from 'supertest';
- import { App } from 'supertest/types';
import {
  FastifyAdapter,
  NestFastifyApplication,
} from '@nestjs/platform-fastify';

describe('AppController (e2e)', () => {
+  let app: NestFastifyApplication;

  beforeAll(async () => {
    const moduleFixture = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

+    app = moduleFixture.createNestApplication<NestFastifyApplication>(
+      new FastifyAdapter(),
+    );

    await app.init();
+    await app.getHttpAdapter().getInstance().ready();
  });

  afterAll(async () => {
    await app.close();
  });

  it('/ (GET)', () => {
    return request(app.getHttpServer())
      .get('/')
      .expect(200)
      .expect('Hello World!');
  });
});

```

## Using this template

You can use this template directly by creating a repository on Github, or by cloning the repository to your machine.

### Creating a Github repository using this template

By clicking "[Use this template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template#creating-a-repository-from-a-template)" button in this repo.

<img src="https://docs.github.com/assets/cb-76823/mw-1440/images/help/repository/use-this-template-button.webp"/>

Or, by using [`gh` cli](https://github.com/cli/cli): 

```bash
gh repo create MY_PROJECT --template Fcmam5/nestjs-fastify-starter --private --clone
```

### Cloning the repository 

You can clone this template to your local machine with the following

```bash
$ git clone https://github.com/Fcmam5/nestjs-fastify-starter.git my-project
$ cd my-project
$ npm install
```

<br/>

> [!TIP]
> If you'd like to clone the repository without the git history, you can use [`degit`](https://github.com/Rich-Harris/degit), for example:
> 
> ```bash
> degi https://github.com/Fcmam5/nestjs-fastify-starter
> # or:
> degit git@github.com:Fcmam5/nestjs-fastify-starter
> ```



## Project setup

```bash
$ npm install
```

## Compile and run the project

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Run tests

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Resources

- [NestJS](https://github.com/nestjs/typescript-starter?tab=readme-ov-file#resources)
- [Fastify](https://github.com/fastify/fastify?tab=readme-ov-file#ecosystem)


## License

This template/fork is [MIT licensed](./LICENSE).

# Typescript

**Question**: should we recommend using typescript over javascript?

**TODO:** advantages of typescript over javascript?

Node.js does not support running typescript natively, so it must first be transpiled to JavaScript. There are 2 widely used transpilers:

1. `tsc` - the compiler shipped with [typescript](https://www.npmjs.com/package/typescript), supports type checking and transpiles to JavaScript

2. [`babel`](https://babeljs.io) - can transpile to javascript using the [`@babel/preset-typescript`](https://babeljs.io/docs/en/babel-preset-typescript) preset, does _not_ support type checking

There are other transpilers such as [esbuild](https://esbuild.github.io) and [swc](https://swc.rs) but these are not yet widely adopted and not currently recommended.

Avoid mixing transpilers on the same project as this can lead to inconsistencies. One common mistake is using `tsc` for code transpilation but `babel` (the [default](https://jestjs.io/docs/getting-started#using-typescript)) for jest tests.

More information on choosing a transpiler can be found in the [typescript documentation](https://www.typescriptlang.org/docs/handbook/babel-with-typescript.html).

## Transpiling in development

TODO: talk about nodemon with babel-node, `tsc -w`, `ts-node`

Many code editors (such as Visual Studio Code) provide support for type checking of typescript. If you're using one of these editors, you can speed up transpilation by using babel without type checking. **TODO**: check if there's a way to turn this on for `tsc` as well.

Code editors typically only run type checking for open files, so it is a good idea to run `tsc --noEmit` periodically to check the entire codebase, e.g. as a git pre-push hook.

## Ship JavaScript not TypeScript for deployment

It's best practice to run the transpilation step as part of your deployment pipeline rather than dynamically in production, for the follow reasons:

1. Type errors will get caught before code is deployed
1. The application will start up more quickly as there is no need to transpile
1. You can ship a smaller container as it doesn't need to include the transpiler

## Recommended configuration

The typescript community have produced a series of [recommended base configurations for various versions of node](https://github.com/tsconfig/bases/). Using an up to date version means typescript will not polyfill capabilities that are natively supported by node, which can improve runtime performance.

In addition to the above, we recommend setting the following in the `tsconfig.json` file:

```json
"isolatedModules": true
````

Babel and other transpilers process a single file at a time which is incompatible with some typescript features. Turning on this flag will produce warnings if those features are used.

```json
"strict": true
```

Strict mode turns on a [number of other flags](https://www.typescriptlang.org/tsconfig#strict) which can help prevent bugs in your code. If you're migrating an existing project to typescript it might be difficult to turn this on, but for new projects it is recommended.

```json
"sourceMap": true
```

Improves debuggability of compiled code by generating source maps.

**TODO**: something about not shipping source maps to prod

## Sharing types with npm modules

**TODO**: summarise [this](https://www.typescriptlang.org/docs/handbook/declaration-files/publishing.html)? 

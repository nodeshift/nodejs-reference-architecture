---
sidebar_position: 6
---
# Typescript

TypeScript is a language that compiles to JavaScript and provides static typing by extending the JavaScript syntax. It is worth considering for larger projects as it can bring the following benefits:

- **Error detection**: certain classes of errors can be caught at compile time rather than causing a runtime error, e.g. reading a property from an object that may be undefined.

- **Contextual help in code editors**: for supported editors, TypeScript enables rich code completion both for project code and imported modules via the [DefinitelyTyped](https://definitelytyped.org/) project.

- **Refactoring support**: changing the signature of a function or structure of an object in an incompatible way will cause compilation errors where it is used. TypeScript also enables automated refactorings such as renaming variables across multiple files and extracting methods.  

TypeScript does _not_ provide any runtime type checking. To validate data at runtime, use a library such as [ajv](https://github.com/ajv-validator/ajv) in combination with TypeScript.

## Transpilers

Node.js does not support running TypeScript natively, so it must first be transpiled to JavaScript. We recommend the `tsc` transpiler that is shipped with [typescript](https://www.npmjs.com/package/typescript). This supports both type checking and transpilation to JavaScript.

For front end development, sometimes [`babel`](https://babeljs.io) is used with the [`@babel/preset-typescript`](https://babeljs.io/docs/en/babel-preset-typescript) preset for transpilation, but this does _not_ support type checking and we do not recommend it for Node.js. More information on choosing a transpiler can be found in the [typescript documentation](https://www.typescriptlang.org/docs/handbook/babel-with-typescript.html).

Avoid mixing transpilers on the same project as this can lead to inconsistencies. Sometimes projects unintentionally use `babel` for their jest tests as it is the [default](https://jestjs.io/docs/getting-started#using-typescript).

## Transpiling in development

The `tsc` compiler provides a useful watch mode, activated by the `-w` or `--watch` flag. This will automatically re-transpile source files when they change. If you want to also restart a Node.js server process when this happens, you can use this in combination with [nodemon](https://nodemon.io) using a module such as [concurrently](https://www.npmjs.com/package/concurrently). An example script for `package.json`:

```json
{
  "scripts": {
    "dev": "concurrently -n tsc,node 'tsc -w' 'nodemon -w dist dist/server.js'"
  }
}

```

If you're using `babel` which does not perform type checking, it is a good idea to run `tsc --noEmit` periodically to check the entire codebase, e.g. as a git pre-push hook.

## Ship JavaScript not TypeScript for deployment

It's best practice to run the transpilation step as part of your deployment pipeline rather than dynamically in production, for the follow reasons:

1. Type errors will get caught before code is deployed
1. The application will start up more quickly as there is no need to transpile
1. You can ship a smaller container as it doesn't need to include the transpiler

## Recommended configuration

The typescript community have produced a series of [recommended base configurations for various versions of node](https://github.com/tsconfig/bases/). Using an up to date version means typescript will not polyfill capabilities that are natively supported by node, which can improve runtime performance.

In addition to the above, we recommend setting the following in the `compilerOptions` section of the `tsconfig.json` file:

```json
"isolatedModules": true
```

This flag enables compatibility with Babel and other transpilers that process a project a single file at a time. Some TypeScript features such as `const enums` are not compatible with isolated modules, see the [TypeScript documentation](https://www.typescriptlang.org/tsconfig#isolatedModules) for more details. Turning on this flag will produce warnings if those features are used.

```json
"strict": true
```

Strict mode turns on a [number of other flags](https://www.typescriptlang.org/tsconfig#strict) which can help prevent bugs in your code. If you're migrating an existing project to typescript it might be difficult to turn this on, but for new projects it is recommended.

```json
"esModuleInterop": true
```

This improves TypeScript's [interoperability with with CommonJS/AMD/UMD modules](https://www.typescriptlang.org/tsconfig#esModuleInterop), particularly with regard to how default imports are handled. It is automatically enabled in the Node.js base configurations (see above).

## Hierarchical TypeScript Configuration

If you want to maintain consistency across several components (e.g. microservices) it is a good idea to create a standard base configuration which specifies appropriate and then have every component inherit from it. This can be done by publishing the base configuration as a versioned npm module and then referencing it in a `tsconfig.json` file as follows:

```json
"extends": "@yourproject/projectbase/tsconfig.json"
```

Multiple levels of inheritance are possible, so the `projectbase` configuration could inherit from one of the recommended base configurations described above.

## Sharing types with npm modules

If you are publishing a library code rather than an application it is good practice to publish types for that module alongside the compiled code. There are 2 steps required to enable this:

 1. Turn on [declaration generation](https://www.typescriptlang.org/tsconfig#declaration) in your `tsconfig.json`:

    ```json
    {
      "compilerOptions": {
        "declaration": true
      }
    }
    ```
 2. Reference the main declaration file in your `package.json`:

    ```json
    {
      "types": "./lib/index.d.ts"
    }
    ```
You should also ensure you include dependencies for the types of modules that you depend on, see the [TypeScript documentation](https://www.typescriptlang.org/docs/handbook/declaration-files/publishing.html) for further details.

## Further Reading

[Introduction to the Node.js reference architecture: Typescript](https://developers.redhat.com/articles/2022/04/11/introduction-nodejs-reference-architecture-part-8-typescript)

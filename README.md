# ts-package
Tutorial to create your own typescripted package.
Original tutorial see https://itnext.io/step-by-step-building-and-publishing-an-npm-typescript-package-44fe7164964c


## Requirements

- nodejs
- npm
- yarn (optional and as default here; if there are differences in the commands between yarn and npm then it will be descibe separatly)

---

## Init your TS package

```
yarn init -y
```

Ignore the `node_modules` directory for git:

```bash
echo "node_modules" >> .gitignore
```

add Typescript as a Dev-Dependency

```
yarn add -D typescript
```

add a TS configuration file tsconfig.json

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "declaration": true,
    "outDir": "./lib",
    "strict": true
  },
  "include": ["src"],
  "exclude": ["node_modules", "**/__tests__/*"]
}
```

create a src folder

```
mkdir src
```

---

## Build process

add a build script into package.json

```json
  "scripts": {
    "build" : "tsc"
  }
```

now run build command. The lib folder contains your compiled code and typescript definitions.

```
yarn build
```

or

```
npm run build
```

you will get a `/lib` directory with the compiled version


add the lib directory into .gitignore file. The slash means the lib directory in the root directory.

```bash
echo "/lib" >> .gitignore
```

whitelist lib directory for a published package

add to package.json so no other files will include into the published package

```json
  "files": [
    "lib/**/*"
  ]
```

adapt the package.json

```json
  "main": "lib/index.js",
  "types": "lib/indes.d.ts",
```

---

## Deployment process

add deploy script to publish package

```
"deploy": "yarn publish --access public"
```

publish your package

```
yarn login
yarn publish
```

or

```
npm adduser
npm version patch
npm run publish
```

---

## Use your TS library inside another project

create and initialize a new project

```
yarn init -y
```

add your ts-package library (change @vanvuongngo/ts-package to yours)

```
yarn add @vanvuongngo/ts-package
```

create an example index.mjs and import the package

```
import { Greeter } from '@vanvuongngo/ts-package';

console.log(Greeter("World"));
```

Run your example script

```
node .
```

---

## Use your localley TS library and to prevent publishing on all development changes

Create a locally link to develop the TS library

Use link to link this package that you’d like to test into your current project.

```
yarn link
```

create a new project directory and initialize it

```
yarn init -y
```

add local ts-package as dependency to develop without need of publishing

```
yarn link ts-package
```

create an example script

```
import { Greeter } from 'ts-package';

console.log(Greeter('World'));
```

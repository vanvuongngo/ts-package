# ts-package
Template to create a typescripted package

## Requirements

- nodejs
- npm
- yarn (optional and as default here; if there are differences in the commands between yarn and npm then it will be descibe separatly)

## Init your package

```
yarn init -y
```

Ignore the `node_modules` directory for git:

```bash
echo "node_modules" >> .gitignore
```

## Add Typescript as a Dev-Dependency

```
yarn add -D typescript
```

## Add a TS configuration file tsconfig.json

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

## Create a src folder

```
mkdir src
```

## Add a build script into package.json

```json
  "scripts": {
    "build" : "tsc"
  }
```

## Now run build command

The lib folder contains your compiled code and typescript definitions.

```
yarn build
```

or

```
npm run build
```

## Git ignore the lib directory

add the lib directory into .gitignore file. The slash means the lib directory in the root directory.

```
/lib
```

## Whitelist lib directory for a published package

add to package.json so no other files will include into the published package

```
"files": ["lib/**/*"]
```

## adapt the package.json

```json
  "main": "lib/index.js",
  "types": "lib/indes.d.ts",
```

## Create a locally link to develop the TS library

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

## Add deploy script to publish package

```
"deploy": "yarn publish --access public"
```

## Publish a package

```
yarn login
yarn publish
```

or

```
npm adduser
npm run publish
```

init proj
================
    npm init

necessary pkg
================
    npm install -D typescript ts-node @types/node jest ts-jest @types/jest tsc-alias

tsc settings
===================
+ create `tsconfig.json`
```
    npx tsc --init
```
with content
```json
{
    "compilerOptions": {
        "target": "es2016",
        "module": "commonjs",
        "moduleDetection": "force",
        "strict": true,
        "forceConsistentCasingInFileNames": true,
        "skipLibCheck": true,
        "esModuleInterop": true,
        "outDir": "./dist",
        "baseUrl": ".",
        "paths": {}
    },
    "include": [
        "src",
        "__test__"
    ]
}
```

+ create `tsconfig-build.json`

with content:
```json
{
    "extends": "./tsconfig.json",
    "include": [
        "src"
    ]
}
```

+ commands

In `package.json`
```json
    {
        "scripts": {
            "build": "tsc --project tsconfig-build.json && tsc-alias -p tsconfig-build.json",
            "start": "node ./dist/index.js",
        },
    }
```

test settings
===============
+ In `package.json`
  ```json
    {
        "scripts": {
            "test": "jest"
        },
    }
  ```

+ create `jest.config.js`
  ```
    npx ts-jest config:init
  ```

+ In `jest.config.js`
  ```js
    const { pathsToModuleNameMapper } = require("ts-jest");
    const { compilerOptions } = require("./tsconfig.json");

    /** @type {import('ts-jest').JestConfigWithTsJest} */
    module.exports = {
        preset: 'ts-jest',
        testEnvironment: 'node',
        roots: ['.'],
        modulePaths: [compilerOptions.baseUrl],
        moduleNameMapper: pathsToModuleNameMapper(compilerOptions.paths)
    };
  ```
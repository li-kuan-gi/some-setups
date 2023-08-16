init proj
================
    npm init

necessary pkg
================
    npm install -D typescript ts-node @types/node jest ts-jest @types/jest

build settings
===================
+ create `tsconfig.json`
```
    npx tsc --init
```
with content
```
{
    "compilerOptions": {
        "target": "es2016",
        "module": "commonjs",
        "moduleDetection": "force",
        "strict": true,
        "forceConsistentCasingInFileNames": true,
        "skipLibCheck": true,
        "esModuleInterop": true,
        "outDir": "./dist"
    },
    "include": [
        "src",
        "__test__"
    ]
}
```

+ create `tsconfig-build.json`

with content:
```
{
    "extends": "./tsconfig.json",
    "include": [
        "src"
    ]
}
```

+ commands

In `package.json`
```
    {
        "scripts": {
            "build": "tsc --build tsconfig-build.json",
            "start": "node ./dist/app.js",
        },
    }
```

test settings
===============
+ In `package.json`
  ```
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

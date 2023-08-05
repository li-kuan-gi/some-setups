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
        "strict": true,
        "esModuleInterop": true,
        "outDir": "./dist"
    },
    include: [
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
    "exclude": [
        "./__test__"
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
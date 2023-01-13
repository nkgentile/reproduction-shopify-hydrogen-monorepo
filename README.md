# Steps to reproduce

> NPM 8.19.3
>
> Node 16.19.0, 18.13.0
>
> For dependency version see [`package.json`](apps/hydrogen/package.json)

### 1. Install dependencies
```sh
npm ci
```

### 2. Run development server
```sh
npm start
```

This will fail with the error:
```sh
Command failed with exit code 1: node -p require('./node_modules/@shopify/hydrogen/package.json').version
node:internal/modules/cjs/loader:1042
  throw err;
  ^
Error: Cannot find module './node_modules/@shopify/hydrogen/package.json'
```

### 3. Run build
```sh
npm run build
```
This will build the app with no issue

### 4. Create a symbolic link to the hoisted dependency (MacOS):
```sh
pushd apps/hydrogen
mkdir -p ./node_modules/@shopify
pushd ./node_modules/@shopify
ln -s ../../../../node_modules/@shopify/hydrogen
popd
popd
```
There should now be a symbolic link at `apps/hydrogen/node_modules/@shopify/hydrogen` that points to `node_modules/@shopify/hydrogen`

### 5. Run development server once more:
```sh
npm start
```
Everything should work as expected.
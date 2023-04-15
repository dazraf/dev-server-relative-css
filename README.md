# Reproducer

## Description

This repository reproduces the problem with loading a CSS file that's provided by a thirdparty library (Shoelace) withing a monorepo structure that uses NPM workspaces.There are three sub projects:

* [package.json](./package.json) - defines the workspace
* [tsconfig.json](./tsconfig.json) - defines the top level project tsconfig, that references the sub projects
* [tsconfig.base.json](./tsconfig.base.json) - defines the base configuration for each sub projects
* [packages/web](./packages/web/) - this is the web project that uses dev server. The [index.html](./packages/web/index.html) file contains a `<link>` tag that attempts to load a Shoelace CSS file from the top-level npm_modules. This fails to resolve because DevServer rewrites the relative path to the `../../node_modules/@shoelace-style/...`, removing the relative path.

## How to run

### Install the dependencies

```bash
npm install
```

### Build

```bash
npm run build
```

### Run the dev server

```bash
npm run web
```

This opens a browser. Open the browser dev tools console. You will see:

```
/localhost:8000/node_modules/@shoelace-style/shoelace/dist/themes/light.css net::ERR_ABORTED 404 (Not Found)
```

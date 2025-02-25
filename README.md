# Easy-Experiments - Native Federation Plugin Skeleton

Welcome to the **Easy-Experiments Native Federation Plugin Skeleton** !

This repository serves as a **template** for creating and publishing a new plugin (remote) that can be loaded dynamically by the host application using [Webpack 5 Module Federation](https://webpack.js.org/concepts/module-federation/) in an **Angular 19** environment.

Below, you’ll find everything you need to know to get started: from setting up your local environment and customizing this template, to testing, building, and deploying your plugin.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Project Structure](#project-structure)
3. [Getting Started](#getting-started)
4. [Configuration Details](#configuration-details)
5. [Running and Testing Locally](#running-and-testing-locally)
6. [Updating the Plugin Registry](#updating-the-plugin-registry)
7. [Common Issues and FAQs](#common-issues-and-faqs)
8. [Contributing](#contributing)
9. [License](#license)

---

## Prerequisites

Before you begin, make sure you have:

- **Node.js** (version 16 or above recommended)
- **npm** (version 8 or above recommended) or **yarn**
- Basic knowledge of Angular (>= 19) and Webpack Module Federation.

---

## Project Structure

A typical layout after you clone or generate this repository:

```
.
├── src
│   ├── app
│   │    ├── app.config.ts
│   │    ├── app.routes.ts
│   │    ├── app.component.html
│   │    ├── app.component.scss
│   │    ├── app.component.spec.ts
│   │    └── app.component.ts
|   ├── bootstrap.ts
|   ├── main.ts
├── federation.config.js
├── angular.json
├── package.json
├── README.md
├── ...
```

Key files/folders to note:
- **`federation.config.js`** : Where the Module Federation configuration lives (exposes, shared dependencies, etc.).
- **`src/app/`**: Main Angular application code. You’ll add your custom logic/components here.

---

## Getting Started

### 1. Use this Template
First, fork this repository to create your own copy.

### 2. Install Dependencies
In the root directory, run:
```bash
npm install
```
(This installs all required dependencies, including Angular 19, Webpack 5, etc.)

---

## Configuration Details

### Module Federation Settings

In **`federation.config.js`**, you'll see a configuration object like:

```js
const { withNativeFederation, shareAll } = require('@angular-architects/native-federation/config');

module.exports = withNativeFederation({

  name: 'ee-plugin',

  exposes: {
    './Component': './src/app/app.component.ts',
  },

  shared: {
    ...shareAll({ singleton: true, strictVersion: true, requiredVersion: 'auto' }),
  },

  skip: [
    'rxjs/ajax',
    'rxjs/fetch',
    'rxjs/testing',
    'rxjs/webSocket',
  ]

});

```

- **`name`**: The internal name for this remote.
- **`exposes`**: Key-value pairs defining which modules/components from your plugin are exposed.
- **`shared`**: Defines which dependencies are shared between host and remote(s).
- **`skip`**: ...

**Important**:
- Ensure the `shared` libraries match (or are compatible with) the versions used by the host application.

---

## Running and Testing Locally

1. **Development build**:
   ```bash
   npm start --configuration development
   ```
   By default, the plugin will be available at [http://localhost:4201/](http://localhost:4201/) and the `remoteEntry.json` at [http://localhost:4201/remoteEntry.json](http://localhost:4201/remoteEntry.json).

2. **Check logs**:
   Open the browser console to verify that everything loaded correctly.
   If you see `remoteEntry.json` served successfully, your plugin is up and running.

3. **Testing**:
   - You can write unit tests in the standard Angular way (e.g., using Jasmine/Karma).
   - Run `npm test` (or `npm run test`) to execute tests.

---

## Updating the Plugin Registry

Once your plugin is **tested** and **ready**, it'll be possible to upload the plugin on the plugin registry (https://easy-experiments.com/registry):

1. **A** 
2. **B** 
3. **C** 

---

## Common Issues and FAQs

**1. I get a version mismatch error at runtime.**
Make sure the `shared` dependencies in both your plugin and the host have compatible versions. Sometimes setting `"singleton": true` is required for Angular libraries (Core, Common, Router, etc.).

**2. My plugin compiles but the host can’t find the exposed module.**
Double-check the **`exposes`** key in `federation.config.js` and ensure you’re importing the right string in the host (e.g. `yourPlugin/PluginModule` if you used `./PluginModule`).

**3. The plugin loads but Angular errors appear in the console.**
Verify you’re using Angular 19 (or a version compatible with the host). If the host is on Angular 19 and your plugin is on a different major version, runtime errors can occur.

**4. How do I debug changes quickly?**
Use the **development mode** (`serve`) and reference the local `remoteEntry.json` in your host. Any changes you make will reflect almost immediately after a recompile.

---

## Contributing

We welcome contributions to improve this plugin skeleton:
- **Bug reports**: Submit an issue on GitHub.
- **Feature requests**: Open a discussion or submit a pull request.
- **Pull requests**: Fork the repo, create a branch, make your changes, and submit a PR.

---

## License

This template is released under the [MIT License](./LICENSE). Feel free to modify and share, but please give credit where it’s due.

---

### Happy Coding !

If you have any questions or suggestions, feel free to open an issue or start a discussion on the repository. We hope this skeleton accelerates your workflow and keeps your plugin ecosystem well organized.

**Thanks for contributing to Easy-Experiments project !**
```

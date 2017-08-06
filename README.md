# `add-component`
### Simple, customizable utility for adding new React components to your project.

Anyone else sick of writing the same component boilerplate, over and over?

This project is a globally-installable CLI for adding new React components. It's dead simple to use, and requires no configuration, although it's easy to customize it to fit your project's coding style.

### Features
- Simple CLI interface for adding Component, PureComponent, or Stateless Functional components.
- Uses [Prettier](https://github.com/prettier/prettier) to stylistically match the existing project.
- Offers global config, which can be overridden on a project-by-project basis.
- Colourful terminal output!


### Quickstart

Install via NPM:

```bash
$ npm i -g add-component
```

`cd` into your project's directory, try creating a new component:

```bash
$ add-component SomeComponentName
```

Your project will now have a new directory at `src/components/SomeComponentName`. This directory has two files:

```js
// `SomeComponentName/index.js`
export { default } from './SomeComponentName';
```

```js
// `SomeComponentName/SomeComponentName.js`
import React, { Component } from 'react';

class SomeComponentName extends Component {
  render() {
    return <div />;
  }
}

export default SomeComponentName;
```

> This structure might appear odd to you, with an `index.js` that points to a named file. I've found this to be an optimal way to set up components; the `index.js` allows you to `import` from the directory (eg. `import SomeComponentName from 'components/SomeComponentName'`), while having `SomeComponentName.js` means that you're never lost in a sea of `index.js` files in your editor.
>
> This structure is not currently configurable, but I'm happy to consider implementing alternatives.



### Configuration

Configuration can be done through 3 different ways:

- Creating a global `.add-component-config.json` in your home directory (`~/.add-component-config.json`).
- Creating a local `.add-component-config.json` in your project's root directory.
- Command-line arguments.

The resulting values are merged, with command-line values overwriting local values, and local values overwriting global ones.


##### Type

Control the type of component created:
- `class` for a traditional Component class (default),
- `pure-class` for a PureComponent class,
- `functional` for a stateless functional component.

Legacy `createClass` components are not supported, although support would be easy to add. Feel free to open an issue (or a PR!).

**Usage:**
Command line: `--type <value>` or `-t <value>`
JSON config: `{ "type": <value> }`


##### Directory

Controls the desired directory for the created component. Defaults to `src/components`

Legacy `createClass` components are not supported, although support would be easy to add. Feel free to open an issue (or a PR!).

**Usage:**
Command line: `--dir <value>` or `-d <value>`
JSON config: `{ "dir": <value> }`

##### File Extension

Controls the file extension for the created components. Can be either `js` (default) or `jsx`.

**Usage:**
Command line: `--extension <value>` or `-x <value>`
JSON config: `{ "extension": <value> }`

##### Prettier Config

Delegate settings to Prettier, so that your new component is formatted as you'd like. Defaults to Prettier defaults.

For a full list of options, see the [Prettier docs](https://github.com/prettier/prettier#options).

**Usage:**
Command line: N/A (Prettier config is only controllable through JSON)
JSON config: `{ "prettierConfig": { "key": "value" } }`

**Example:**

```js
{
  "prettierConfig": {
    "singleQuote": true,
    "semi": false,
  }
}
```


### Platform Support
This has only been tested in MacOS. I believe it'd work fine in linux distros, as well. Windows is a big question mark (would welcome contribution here!).


### TODO

This is a brand new thing! I'd like to add more functionality:

- Built-in support for common style tools (CSS modules, Aphrodite, styled-components, etc).
- Better error messaging, more edge-case support
- Editor integrations

# Unique Names Generator


[![Build Status](https://travis-ci.com/andreasonny83/unique-names-generator.svg?branch=master)](https://travis-ci.com/andreasonny83/unique-names-generator)
[![All Contributors](https://img.shields.io/badge/all_contributors-4-orange.svg?style=flat-square)](#contributors-)
[![](https://img.shields.io/npm/v/unique-names-generator.svg)](https://npmjs.org/package/unique-names-generator)
[![](https://img.shields.io/npm/l/unique-names-generator.svg)](https://github.com/andreasonny83/unique-names-generator/blob/master/LICENSE)
[![Greenkeeper badge](https://badges.greenkeeper.io/andreasonny83/unique-names-generator.svg)](https://greenkeeper.io/)
[![](https://img.shields.io/npm/dt/unique-names-generator.svg)](https://npmjs.org/package/unique-names-generator)
[![devDependencies Status](https://david-dm.org/andreasonny83/unique-names-generator/dev-status.svg)](https://david-dm.org/andreasonny83/unique-names-generator?type=dev)

[![NPM](https://nodei.co/npm/unique-names-generator.png)](https://npmjs.org/package/unique-names-generator)

> More than 50,000,000 name combinations out of the box

## What is Unique name generator?

Unique name generator is a tree-shakeable Node package for generating random and unique names.

It comes with a list of dictionaries out of the box, but you can also provide your custom ones.

## Docs

This documentation is for the `unique-names-generator` v4.

If you are using a version 3.x of the library, please refer to the
[v3 Docs](https://github.com/andreasonny83/unique-names-generator/blob/v3.1.1/README.md)

For the version 1 & 2, please refer to the
[v2 Docs](https://github.com/andreasonny83/unique-names-generator/blob/v2.0.2/README.md)

### Migrating to v4

If you want to migrate, from an older version of the library to v4, please read the [Migration guide](#migration-guide)

## Table of contents

- [Unique Names Generator](#unique-names-generator)
  - [What is Unique name generator?](#what-is-unique-name-generator)
  - [Docs](#docs)
    - [Migrating to v4](#migrating-to-v4)
  - [Table of contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Usage](#usage)
    - [Typescript support](#typescript-support)
  - [API](#api)
    - [uniqueNamesGenerator (options)](#uniquenamesgenerator-options)
    - [options](#options)
      - [dictionaries](#dictionaries)
      - [separator](#separator)
      - [length](#length)
      - [style](#style)
  - [Dictionaries available](#dictionaries-available)
      - [Adjectives](#adjectives)
      - [Animals](#animals)
      - [Colors](#colors)
      - [Countries](#countries)
      - [Names](#names)
      - [Star Wars](#star-wars)
    - [Default dictionaries](#default-dictionaries)
    - [Custom dictionaries](#custom-dictionaries)
    - [Combining custom and provided dictionaries](#combining-custom-and-provided-dictionaries)
  - [Migration guide](#migration-guide)
    - [Migration guide from version 3 to version 4](#migration-guide-from-version-3-to-version-4)
      - [Mandatory `dictionaries` config](#mandatory-dictionaries-config)
    - [Migration guide from version 1 or 2](#migration-guide-from-version-1-or-2)
      - [uniqueNamesGenerator](#uniquenamesgenerator)
      - [Separator](#separator)
      - [Short](#short)
  - [Contributing](#contributing)
  - [License](#license)
  - [Contributors ✨](#contributors-%e2%9c%a8)

## Prerequisites

This project requires NodeJS (at least version 6) and NPM.
[Node](http://nodejs.org/) and [NPM](https://npmjs.org/) are really easy to install.
To make sure you have them available on your machine,
try running the following command.

```sh
$ node --version
v7.10.1

$ npm --version
4.2.0
```

## Installation

**BEFORE YOU INSTALL:** please read the [prerequisites](#prerequisites)

Install the package using npm or Yarn

```sh
$ npm i -S unique-names-generator
```

Or using Yarn

```sh
$ yarn add unique-names-generator
```

## Usage

```js
const { uniqueNamesGenerator, adjectives, colors, animals } = require('unique-names-generator');

const randomName = uniqueNamesGenerator({ dictionaries: [adjectives, colors, animals] }); // big_red_donkey

const shortName = uniqueNamesGenerator({
  dictionaries: [adjectives, animals, colors], // colors can be omitted here as not used
  length: 2
}); // big-donkey
```

### Typescript support

This package export a type definition file so you can use it, out of the box,
inside your Typescript project.

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const customConfig: Config = {
  dictionaries: [adjectives, colors],
  separator: '-',
  length: 2,
};

const randomName: string = uniqueNamesGenerator({
  dictionaries: [adjectives, colors, animals]
}); // big_red_donkey

const shortName: string = uniqueNamesGenerator(customConfig); // big-donkey
```

## API

### uniqueNamesGenerator (options)

Returns a `string` with a random generated name

### options

Type: `Config`

#### dictionaries

Type: `array`

required: `true`

This is an array of dictionaries. Each dictionary is an array of strings containing the words to use for generating the string.

The [provided dictionaries](#dictionaries-available) can be imported from the library as a separate modules and provided in the desired order.

```typescript
import { uniqueNamesGenerator, adjectives, colors, animals } from 'unique-names-generator';

const shortName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals]
}); // red_big_donkey
```

Read more about the dictionaries and how to use them, in the [Dictionaries](#dictionaries-available) section.

#### separator

Type: `string`

required: `false`

Default: `_`

A string separator to be used for separate the words generated.
The default separator is set to `_`.

#### length

Type: `number`

required: `false`

Default: `3`

The default value is set to `3` and it will return a name composed of 3 words.
This values must be equal or minor to the number of [dictionaries](#dictionaries-available) defined (3 by default).
Setting the `length` to a value of `4` will throw an error when only 3 dictionaries are provided.

#### style

Type: `lowerCase | upperCase | capital`

required: `false`

Default: `lowerCase`

The default value is set to `lowerCase` and it will return a lower case name.
By setting the value to `upperCase`, the words, will be returned with all the letters in upper case format.
The `capital` option will capitalize each word of the unique name generated

```typescript
import { uniqueNamesGenerator, adjectives, colors, animals } from 'unique-names-generator';

const capitalizedName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals],
  style: 'capital'
}); // Red_Big_Donkey

const upperCaseName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals],
  style: 'capital'
}); // RED_BIG_DONKEY

const lowerCaseName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals],
  style: 'capital'
}); // red_big_donkey
```

## Dictionaries available

#### Adjectives

A list of more than 1,400 adjectives ready for you to use

```typescript
import { uniqueNamesGenerator, Config, adjectives } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives]
}

const characterName: string = uniqueNamesGenerator(config); // big
```

#### Animals

A list of more than 350 animals ready to use

```typescript
import { uniqueNamesGenerator, Config, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [animals]
}

const characterName: string = uniqueNamesGenerator(config); // donkey
```

#### Colors

A list of more than 50 different colors

```typescript
import { uniqueNamesGenerator, Config, colors } from 'unique-names-generator';

const config: Config = {
  dictionaries: [colors]
}

const characterName: string = uniqueNamesGenerator(config); // red
```

#### Countries

A list of more than 250 different countries

```typescript
import { uniqueNamesGenerator, Config, countries } from 'unique-names-generator';

const config: Config = {
  dictionaries: [countries]
}

const characterName: string = uniqueNamesGenerator(config); // United Arab Emirates
```

#### Names

A list of more than 4,900 unique names

```typescript
import { uniqueNamesGenerator, Config, names } from 'unique-names-generator';

const config: Config = {
  dictionaries: [names]
}

const characterName: string = uniqueNamesGenerator(config); // Winona
```

#### Star Wars

A list of more than 80 unique character names from Star Wars

```typescript
import { uniqueNamesGenerator, Config, starWars } from 'unique-names-generator';

const config: Config = {
  dictionaries: [starWars]
}

const characterName: string = uniqueNamesGenerator(config); // Han Solo
```

### Default dictionaries

By default, the Unique name generator library comes with 3 dictionaries out of the box, so that you can use them
straight away.
Starting from the version 4 of the library, however, you must explicitly provide the dictionaries within the
configuration object.
This is for reducing the bundle size and allowing tree shaking to remove the extra dictionaries from your bundle when
using custom ones.

The new syntax for using the default dictionaries is the following:

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives, colors, animals]
}

const characterName: string = uniqueNamesGenerator(config); // red_big_donkey
```

### Custom dictionaries

You might want to provide your custom dictionaries to use for generating your unique names,
in order to meet your business requirements.

You can easily do that using the [dictionaries](#dictionaries-available) option.

```typescript
import { uniqueNamesGenerator } from 'unique-names-generator';

const starWarsCharacters = [
  'Han Solo',
  'Jabba The Hutt',
  'R2-D2',
  'Luke Skywalker',
  'Princess Leia Organa'
];
const colors = [
  'Green', 'Red', 'Yellow', 'Black'
]

const characterName: string = uniqueNamesGenerator({
  dictionaries: [colors, starWarsCharacters],
  length: 2,
  separator: ' '
}); // Green Luke Skywalker
```

### Combining custom and provided dictionaries

You can reuse the dictionaries provided by the library.
Just import the ones that you need and use them directly in your app.

```typescript
import { uniqueNamesGenerator, adjectives, colors } from 'unique-names-generator';

const improvedAdjectives = [
  ...adjectives,
  'abrasive',
  'brash',
  'callous',
  'daft',
  'eccentric',
];
const xMen = [
'professorX',
'beast',
'colossus',
'cyclops',
'iceman',
'wolverine',
];

const characterName: string = uniqueNamesGenerator({
  dictionaries: [improvedAdjectives, color, xMen],
  length: 2,
  separator: '-'
}); // eccentric-blue-iceman
```

## Migration guide

### Migration guide from version 3 to version 4

Unique names generator v4 implement a new breaking change.

#### Mandatory `dictionaries` config

You must now explicitly provide the library with the dictionaries to use.
This is for improving flexibility and allowing tree-shaking to remove the unused dictionaries from
your bundle size.

Read more about the dictionaries in the [Dictionaries](dictionaries-available) section.

**v3**

```typescript
import { uniqueNamesGenerator } from 'unique-names-generator';

const randomName = uniqueNamesGenerator(); // big_red_donkey
```

**v4**

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives, colors, animals]
}

const randomName = uniqueNamesGenerator(config); // big_red_donkey
```

### Migration guide from version 1 or 2

Unique names generator v3 implements a couple of breaking changes.
If are upgrading your library from a version 1 or 2, you might be interested in knowing the following:

#### uniqueNamesGenerator

This will now work only when a `dictionaries` array is provided according to the
[v4 breaking change](#mandatory-dictionaries-config).

**v2**

```typescript
import { uniqueNamesGenerator } from 'unique-names-generator';

const randomName = uniqueNamesGenerator();
```

**v4**

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives, colors, animals]
}

const randomName = uniqueNamesGenerator(config); // big_red_donkey
```

#### Separator

**v2**

```typescript
import { uniqueNamesGenerator } from 'unique-names-generator';

const shortName = uniqueNamesGenerator('-'); // big-red-donkey
```

**v4**

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives, colors, animals],
  separator: '-'
}

const shortName = uniqueNamesGenerator(config); // big-red-donkey
```

#### Short

The `short` property has been replaced by `length` so you can specify as many word as you want

**v2**

```typescript
import { uniqueNamesGenerator } from 'unique-names-generator';

const shortName = uniqueNamesGenerator(true); // big-donkey
```

**v4**

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives, colors, animals],
  length: 2
}

const shortName = uniqueNamesGenerator(config); // big-donkey
```

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

1.  Fork it!
2.  Create your feature branch: `git checkout -b my-new-feature`
3.  Add your changes: `git add .`
4.  Commit your changes: `git commit -am 'Add some feature'`
5.  Push to the branch: `git push origin my-new-feature`
6.  Submit a pull request :sunglasses:

## License

[MIT License](https://andreasonny.mit-license.org/2018) © Andrea SonnY

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://about.me/andreasonny83"><img src="https://avatars0.githubusercontent.com/u/8806300?v=4" width="100px;" alt="Andrea Z"/><br /><sub><b>Andrea Z</b></sub></a><br /><a href="#question-andreasonny83" title="Answering Questions">💬</a> <a href="https://github.com/andreasonny83/unique-names-generator/commits?author=andreasonny83" title="Code">💻</a> <a href="#projectManagement-andreasonny83" title="Project Management">📆</a></td>
    <td align="center"><a href="https://github.com/digibake"><img src="https://avatars1.githubusercontent.com/u/6882093?v=4" width="100px;" alt="Baker"/><br /><sub><b>Baker</b></sub></a><br /><a href="https://github.com/andreasonny83/unique-names-generator/issues?q=author%3Adigibake" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/ajainuary"><img src="https://avatars1.githubusercontent.com/u/30972152?v=4" width="100px;" alt="Anurag Jain"/><br /><sub><b>Anurag Jain</b></sub></a><br /><a href="#ideas-ajainuary" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/erdahuja"><img src="https://avatars3.githubusercontent.com/u/15168716?v=4" width="100px;" alt="Deepak"/><br /><sub><b>Deepak</b></sub></a><br /><a href="https://github.com/andreasonny83/unique-names-generator/commits?author=erdahuja" title="Documentation">📖</a> <a href="#ideas-erdahuja" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/abhijitmehta"><img src="https://avatars2.githubusercontent.com/u/5481869?v=4" width="100px;" alt="Abhijit Mehta"/><br /><sub><b>Abhijit Mehta</b></sub></a><br /><a href="#ideas-abhijitmehta" title="Ideas, Planning, & Feedback">🤔</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
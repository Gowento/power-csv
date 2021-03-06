# power-csv

[![NPM version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Coveralls Status][coveralls-image]][coveralls-url]
[![Dependency Status][depstat-image]][depstat-url]
[![Downloads][download-badge]][npm-url]

> Handle CSV with power

## Features

- Fast and powerful (based on [PapaParse](https://github.com/mholt/PapaParse))
- Handles nested CSV
- Extends Express response (`res.csv`)
- Sane defaults
- Dynamic typing (automatically cast integers et al)

## Install

```sh
npm i power-csv
```

## Usage

#### Convert CSV to JSON

```js
import { csv2json } from 'power-csv';

const csv = 'field;object.field;object.anotherField;object.numericField;array.0;array.1;array.2\r\nfoo;bar;foo;123;1;2;foo\r\nbar;;;456;3;4;bar';
const json = csv2json(csv);

// [
//   {
//     field: 'foo',
//     object: {
//       field: 'bar',
//       anotherField: 'foo',
//       numericField: 123,
//     },
//     array: [1, 2, 'foo'],
//   },
//   {
//     field: 'bar',
//     object: {
//       field: '',
//       anotherField: '',
//       numericField: 456,
//     },
//     array: [3, 4, 'bar'],
//   },
// ]
```

#### Convert JSON to CSV

```js
import { csv2json } from 'power-csv';

const json = {
  foo: 'bar',
  bar: {
    foo: 'bar',
  },
};
const csv = json2csv(json);

// foo;bar.foo\r\nbar;bar
```

#### Express middleware

```js
import csv from 'power-csv';
import express from 'express';

const app = express();

app.use(csv);

app.get('/convert-to-csv', (req, res) => {
  res.csv({foo: bar}, 'filename.csv');
});
```

## License

MIT © [Gowento](https://github.com/gowento)

[npm-url]: https://npmjs.org/package/power-csv
[npm-image]: https://img.shields.io/npm/v/power-csv.svg?style=flat-square

[travis-url]: https://travis-ci.org/gowento/power-csv
[travis-image]: https://img.shields.io/travis/gowento/power-csv.svg?style=flat-square

[coveralls-url]: https://coveralls.io/r/gowento/power-csv
[coveralls-image]: https://img.shields.io/coveralls/gowento/power-csv.svg?style=flat-square

[depstat-url]: https://david-dm.org/gowento/power-csv
[depstat-image]: https://david-dm.org/gowento/power-csv.svg?style=flat-square

[download-badge]: http://img.shields.io/npm/dm/power-csv.svg?style=flat-square

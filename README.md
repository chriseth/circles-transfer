# Circles Transfer

<p>
  <a href="https://badge.fury.io/js/%40circles%2Ftransfer">
    <img src="https://badge.fury.io/js/%40circles%2Ftransfer.svg" alt="npm Version" height="18">
  </a>
  <a href="https://github.com/CirclesUBI/circles-transfer/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-APGLv3-orange.svg" alt="License" height="18">
  </a>
  <a href="https://travis-ci.com/CirclesUBI/circles-transfer">
    <img src="https://api.travis-ci.com/CirclesUBI/circles-transfer.svg?branch=main" alt="Build Status" height="18">
  </a>
  <a href="https://twitter.com/CirclesUBI">
    <img src="https://img.shields.io/twitter/follow/circlesubi.svg?label=follow+circles" alt="Follow Circles" height="18">
  </a>
</p>

Utility module for [Circles](https://joincircles.net) to find the [Maximum flow](https://en.wikipedia.org/wiki/Maximum_flow_problem) and necessary transitive transfer steps in a trust graph with multiple tokens.

## Requirements

- NodeJS

## Installation

```
npm i @circles/transfer
```

## Usage

```js
import findTransitiveTransfer from '@circles/transfer';

// Define a weighted trust graph between trusted tokens. Each edge describes
// how much ("capacity") of what token ("token") can be sent from which node
// ("from") to which ("to"):
const nodes = [
  'A',
  'B',
  'C',
  'D',
];

const edges = [
  {
    from: 'A',
    to: 'B',
    token: 'A',
    capacity: 10,
  },
  {
    from: 'B',
    to: 'C',
    token: 'B',
    capacity: 7,
  },
  {
    from: 'B',
    to: 'C',
    token: 'C',
    capacity: 5,
  },
  ...
];

// Find required transfer steps to send tokens transitively between two nodes:
const { transferSteps, maxFlowValue } = findTransitiveTransfer({
  nodes,
  edges,
  from: 'A',
  to: 'D',
  value: 5,
});

// ... we get the maximum possible value:
console.log(`Can send max. ${maxFlowValue} between A and D`);

// ... and finally the transfer steps:
transferSteps.forEach(({ step, from, to, value, token }) => {
  console.log(`${step}.: Send ${value} of ${token} from ${from} to ${to}`);
});
```

## Development

`circles-transfer` is a JavaScript module written in JavaScript, tested with [Jest](https://jestjs.io/), transpiled with [Babel](https://babeljs.io/) and bundled with [Rollup](https://rollupjs.org).

```
// Install dependencies
npm install

// Run test suite
npm run test
npm run test:watch

// Check code formatting
npm run lint

// Build it!
npm run build
```

## License

GNU Affero General Public License v3.0 `AGPL-3.0`

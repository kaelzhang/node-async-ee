[![Build Status](https://travis-ci.org/kaelzhang/node-async-ee.svg?branch=master)](https://travis-ci.org/kaelzhang/node-async-ee)
[![Coverage](https://codecov.io/gh/kaelzhang/node-async-ee/branch/master/graph/badge.svg)](https://codecov.io/gh/kaelzhang/node-async-ee)
<!-- optional appveyor tst
[![Windows Build Status](https://ci.appveyor.com/api/projects/status/github/kaelzhang/node-async-ee?branch=master&svg=true)](https://ci.appveyor.com/project/kaelzhang/node-async-ee)
-->
<!-- optional npm version
[![NPM version](https://badge.fury.io/js/async-ee.svg)](http://badge.fury.io/js/async-ee)
-->
<!-- optional npm downloads
[![npm module downloads per month](http://img.shields.io/npm/dm/async-ee.svg)](https://www.npmjs.org/package/async-ee)
-->
<!-- optional dependency status
[![Dependency Status](https://david-dm.org/kaelzhang/node-async-ee.svg)](https://david-dm.org/kaelzhang/node-async-ee)
-->

# async-ee

The async/await event emitters.

The usage of `async-ee` is nearly the same as the vanilla [`EventEmitter`](https://nodejs.org/dist/latest-v9.x/docs/api/events.html), except that `asyncEmitter.emit()` returns a `Promise`, while the builtin `emitter.emit()` returns a boolean value.

## Install

```sh
$ npm install async-ee
```

## Usage

`asyncEmitter.emit()` returns a `Promise`, so that we could use it in async functions.

```js
import EventEmitter from 'async-ee'

class MyClass extends EventEmitter {
  async doSomething () {
    await this.emit('before-event')
    const data = await doThings()
    await this.emit('after-event', data)
    this.emit('sync-event')
    return data
  }
}

const foo = new MyClass()
.on('before-some-event', async () => await validateFromRemoveServer())
.on('after-event', async data => await doTheTracking(data))
.on('sync-event', () => console.log('did something'))

;(async function () {
  const data = await foo.doSomething()
})
```

### emitter.emit(eventName[, ...args])

Run event handlers with `Promise.all`.

### emitter.emitSeries(eventName[, ...args])

Run event handlers in sequence.

## License

MIT

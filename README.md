# Bit.js [![Build Status](https://travis-ci.org/uupaa/Bit.js.svg)](https://travis-ci.org/uupaa/Bit.js)

[![npm](https://nodei.co/npm/uupaa.bit.js.svg?downloads=true&stars=true)](https://nodei.co/npm/uupaa.bit.js/)

Bit.js is a JavaScript library that supports the analysis of binary data. It aggregates the low-level bit manipulation functions.


This module made of [WebModule](https://github.com/uupaa/WebModule).

## Documentation
- [Spec](https://github.com/uupaa/Bit.js/wiki/)
- [API Spec](https://github.com/uupaa/Bit.js/wiki/Bit)

## Browser, NW.js and Electron

```js
<script src="<module-dir>/lib/WebModule.js"></script>
<script src="<module-dir>/lib/Bit.js"></script>
<script src="<module-dir>/lib/BitView.js"></script>
<script>

// make bit mask
Bit.mask(2)     // -> 0x03
Bit.mask(4)     // -> 0x0f

// bit split by bit-pattern
Bit.split4(0xffff1234, [16,4,4,4,4])  // -> [0xffff, 0x1, 0x2, 0x3, 0x4]
                                      //         16    4    4    4    4 bits

Bit.split3(0xff1234, [16,4,4]) // -> [0xff, 0x1, 0x2, 0x3, 0x4]
Bit.split2(0x1234,   [8,8])    // -> [0x12, 0x34]
Bit.split1(0xfe,     [2,2,4])  // -> [0x3, 0x3, 0xe]

// With ES6 Destructuring Assignment
var [a, b, c] = Bit.split4(0x00001234, [16, 8, 8]);
// -> a = 0x12, b = 0x3, c = 0x4

// population count (counting 1 bits)
Bit.popcnt(0x6) // -> 2

// Number of Leading Zero
Bit.nlz(0x6)    // -> 29

// Number of Training Zero
Bit.ntz(0x6)    // -> 1

// binary dump
Bit.dump(0x12345678, [4,4,8,4,4,8]);
// -> "0001, 0010, 00110100, 0101, 0110, 01111000"

// verbose dump
Bit.dump(0x12345678, bitPattern, true);
// -> "00010010001101000101011001111000(0x12345678), 0001(1,0x1), 0010(2,0x2), 00110100(52,0x34), 0101(5,0x5), 0110(6,0x6), 01111000(120,0x78)"

// get IEEE754 expression
var doublePrecision = true;
var u32array = Bit.IEEE754(0.15625, doublePrecision);
Bit.dump(u32array[0], [1,11,20]) + Bit.dump(u32array[1], [32])
// -> "0, 01111111100, 0100000000000000000000000000000000000000000000000000"


// BitView
var view = new BitView(new Uint8Array([0, 1, 2, 3, 0xFF, 0xFE, 0xFD, 0xFC]));

view.rs4([8,8,8,8])         // -> [0x00, 0x01, 0x02, 0x03]
view.rs4([4,4,4,4,4,4,4,4]) // -> [0xF, 0xF, 0xF, 0xE, 0xF, 0xD, 0xF, 0xC]

</script>
```

## WebWorkers

```js
importScripts("<module-dir>lib/WebModule.js");
importScripts("<module-dir>lib/Bit.js");
importScripts("<module-dir>lib/BitView.js");

...
```

## Node.js

```js
require("<module-dir>lib/WebModule.js");
require("<module-dir>lib/Bit.js");
require("<module-dir>lib/BitView.js");

...
```


mem-stat
========

```
  ___ ___ _______ ___ ___ _______ _______ _______ _______
 |   Y   |   _   |   Y   |   _   |       |   _   |       |
 |.      |.  1___|.      |   1___|.|   | |.  1   |.|   | |
 |. \_/  |.  __)_|. \_/  |____   `-|.  |-|.  _   `-|.  |-'
 |:  |   |:  1   |:  |   |:  1   | |:  | |:  |   | |:  |
 |::.|:. |::.. . |::.|:. |::.. . | |::.| |::.|:. | |::.|
 `--- ---`-------`--- ---`-------' `---' `--- ---' `---'
```

**Note:** This repo can be found on npm here: [mem-stat](https://www.npmjs.com/package/mem-stat)

**Note:** This repo can be found on github here: [node-mem-stat](https://github.com/jub3i/node-mem-stat)

**Caveat:** Works by parsing `/proc/meminfo`, so will only work on nix OS.

Install
-------

```
npm install mem-stat
```

Example
-------

Require the module:
```
var memStat = require('mem-stat');
```

By default `free()` returns values in bytes:
```
var free = memStat.free();
console.log(free);
```

Return free memory in GiB, see docs below for allowed values of units:
```
var free = memStat.free('GiB');
console.log(free);
```

`usedPercent()` returns the percentage memory used eg. `13.359272`:
```
var usedPercent = memStat.usedPercent();
console.log(usedPercent);
```

Get all the calculated statistics, requiring only one read and parse of `/proc/meminfo`:
```
var allStats = memStat.allStats();
console.log(allStats);
  {
    free: 1000,
    total: 8000,
    freePercent: 86.245977,
    usedPercent: 13.754023,
  }
```

Get all fields available from `/proc/meminfo` formatted as an object, see docs below for example of all the fields:
```
var raw = memStat.raw();
console.log(raw);
``

``
//or use the callback style
memStat.raw(function(err, raw) {
  if (err) {
    return console.log(err);
  }
  console.log(raw);
});
```

free(units)
-----------

Returns the amount of free memory in `units` available on the system.

Option        | Type         | Default       | Explanation
------------- | -------------| ------------- | ------------
units         | `String`     | `'bytes'`     | The units of the returned value, can be one of `bytes`, `KiB`, `MiB` or `GiB`.

total(units)
------------

Returns the amount of total memory in `units` available on the system. It's basically the same as `os.totalmem()`, but instead using `/proc/meminfo`.

Option        | Type         | Default       | Explanation
------------- | -------------| ------------- | ------------
units         | `String`     | `'bytes'`     | The units of the returned value, can be one of `bytes`, `KiB`, `MiB` or `GiB`.

freePercent()
-------------

Returns the amount of free memory as a percentage eg `83.9430437`.

usedPercent()
-------------

Returns the amount of used memory as a percentage eg `13.9430437`.

allStats(units)
---------------

Returns an object of all the stats, therefore only requiring one reading and parsing of `/proc/meminfo`.

```
  {
    free: 1000,
    total: 8000,
    freePercent: 86.245977,
    usedPercent: 13.754023,
  }
```

Option        | Type         | Default       | Explanation
------------- | -------------| ------------- | ------------
units         | `String`     | `'bytes'`     | The units of the returned value, can be one of `bytes`, `KiB`, `MiB` or `GiB`.

raw([cb])
-----

Returns an object representing the data in `/proc/meminfo`.

Option  | Type         | Default                                          | Explanation
------- | -------------| ------------------------------------------------ | ------------
cb      | `Function`   | If no callback is specified, uses sync file read | Gives the user the option of using a callback style interface.


```
  {
    memTotal: 8114892,
    memFree: 794140,
    memAvailable: 5879036,
    buffers: 385952,
    cached: 4597408,
    swapCached: 10992,
    active: 4288952,
    inactive: 2453264,
    activeAnon: 1197680,
    inactiveAnon: 592184,
    activeFile: 3091272,
    inactiveFile: 1861080,
    unevictable: 32,
    mlocked: 32,
    swapTotal: 1951740,
    swapFree: 1930036,
    dirty: 212,
    writeback: 0,
    anonPages: 1748032,
    mapped: 378400,
    shmem: 31012,
    slab: 418628,
    sReclaimable: 385960,
    sUnreclaim: 32668,
    kernelStack: 6800,
    pageTables: 32020,
    nFSUnstable: 0,
    bounce: 0,
    writebackTmp: 0,
    commitLimit: 6009184,
    committedAS: 6138892,
    vmallocTotal: 34359738367,
    vmallocUsed: 120844,
    vmallocChunk: 34359595004,
    hardwareCorrupted: 0,
    anonHugePages: 370688,
    hugePagesTotal: 0,
    hugePagesFree: 0,
    hugePagesRsvd: 0,
    hugePagesSurp: 0,
    hugepagesize: 2048,
    directMap4k: 237136,
    directMap2M: 5992448,
    directMap1G: 2097152
  }
```

Contributing
------------

Just send a PR, or create an issue if you are not sure.

Areas ripe for contribution:
- testing
- cross compatability for windows and darwin/osx
- performance
- bugs

Other Stat Modules
------------------

- cpu-stat [npm](https://www.npmjs.com/package/cpu-stat) [git](https://github.com/jub3i/node-cpu-stat)
- net-stat [npm](https://www.npmjs.com/package/net-stat) [git](https://github.com/jub3i/node-net-stat)
- disk-stat [npm](https://www.npmjs.com/package/disk-stat) [git](https://github.com/jub3i/node-disk-stat)
- mem-stat [npm](https://www.npmjs.com/package/mem-stat) [git](https://github.com/jub3i/node-mem-stat)

**Note:** `net-stat`, `disk-stat`, `mem-stat` only work on nix platforms.

License
-------

MIT

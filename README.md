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

**Caveat:** Works by parsing `/proc/meminfo` - so will only work on nix OS.

Install
-------

```
npm install mem-stat
```

Example
-------

```
var memStat = require('mem-stat');

//by default returns values in bytes
var free = memStat.free();
console.log(free);

//return value in GiB, see docs below for allowed values of units
var free = memStat.free('GiB');
console.log(free);

//returns percentage used eg. `13.359272`
var usedPercent = memStat.usedPercent('GiB');
console.log(usedPercent);

//get all the calculated statistics, requiring only one read and parse of `/proc/meminfo`
var allStats = memStat.raw();
console.log(allStats);

//get all fields available from `/proc/meminfo` as an object
var raw = memStat.raw();
console.log(raw);
```

free(units)
-----------

Returns the amount of free memory in `units` avaialable on the system.

Option        | Type         | Default       | Explanation
------------- | -------------| ------------- | ------------
units         | `String`     | `'bytes'`     | The units of the returned value, can be one of `bytes`, `KiB`, `MiB` or `GiB`.

total(units)
------------

Returns the amount of total memory in `units` avaialable on the system. It's basically the same as `os.totalmem()`, but instead using `/proc/meminfo`.

Option        | Type         | Default       | Explanation
------------- | -------------| ------------- | ------------
units         | `String`     | `'bytes'`     | The units of the returned value, can be one of `bytes`, `KiB`, `MiB` or `GiB`.

freePercent()
-------------

Returns the amount of free memory as a percentage eg `83.9430437`.

freePercent()
-------------

Returns the amount of used memory as a percentage eg `13.9430437`.

allStats(units)
---------------

Returns an object of all the stats, therfore only requiring one reading and parsing of `/proc/meminfo`.

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

raw()
-----

Returns an object representing the data in `/proc/meminfo`.

Contributing
------------

Just send a PR, or create an issue if you are not sure.

Areas ripe for contribution:
- testing
- cross compatability for windows and darwin/osx
- performance
- bugs

License
-------

MIT


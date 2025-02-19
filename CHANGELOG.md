# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## 1.0.1

### Fixes

- Allow better control over debug printing.
- Lower the size when DEBUG is undefined.
- Changed `printf()` to `debug_printf()`, as some implementations put `printf` on unexpected ports. This is requires `debug_printf()` to be defined elsewhere.

## 1.0.0

### Features

- **RS485Class**: The internal library `ArduinoRS485ClassMod` was renamed to `RS485Class`.

### Fixes

- **RS485Class**: handle non-intialized baudrate
    `_baudrate` was not initialized in the constructor. The `begin` functions sets it,
    but `sendBreak` and `sendBreakMicroseconds` did not detect whether it was set or not.
    Calling them without calling `begin` beforehand would cause the `HardwareSerial` passed
    in to the constructor to have its `begin` function called with a garbage baudrate.
    A variable called `_haveInit` has been added, which is initialized to `false`, and set
    to `true` when `begin` is called. `_baudrate` is now initialized to `0`. `sendBreak`
    and `sendBreakMicroseconds` now do nothing if `_haveInit` is `false`.

- **libmodbus**: add parenthesis to clarify operator precedence
    This:
    `dest[i] = tab_byte[(i - idx) / 8] & (1 << shift) ? 1 : 0;`
    to this:
    `dest[i] = (tab_byte[(i - idx) / 8] & (1 << shift)) ? 1 : 0;`

- **libmodbus**: fix the same expression appearing on both side of an `||` in an `if` in `modbus.c`

## 0.0.0 - 2020-10-16

### Features

- Initial commit of everything to the new repository.
    The code is based on my other library, `DynamicModbusRTUServerClass`, forked from its version 4.0.0.

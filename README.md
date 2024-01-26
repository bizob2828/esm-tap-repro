# esm-tap-repro
Repro case for demonstrating a failure of using an ESM loader in tap 18.

## Setup

```sh
npm i
npm test
```

## Tap 18

```sh
❯ npm test

> tap-repro@1.0.0 test
> node --loader ./esm-loader.mjs test.tap.mjs

(node:38556) ExperimentalWarning: `--experimental-loader` may be removed in the future; instead use `register()`:
--import 'data:text/javascript,import { register } from "node:module"; import { pathToFileURL } from "node:url"; register("./esm-loader.mjs", pathToFileURL("./"));'
(Use `node --trace-warnings ...` to show where the warning was created)

node:internal/process/esm_loader:34
      internalBinding('errors').triggerUncaughtException(
                                ^
[Error: ENOENT: no such file or directory, open '/path/to/esm-tap-repro/node_modules/@tapjs/test/dist/esm/@tapjs/test/test-built'] {
  errno: -2,
  code: 'ENOENT',
  syscall: 'open',
  path: '/path/to/esm-tap-repro/node_modules/@tapjs/test/dist/esm/@tapjs/test/test-built'
}
```

## Tap 16

```sh
npm i tap@16
npm test
```

```sh
❯ npm test

> tap-repro@1.0.0 test
> node --loader ./esm-loader.mjs test.tap.mjs

(node:38687) ExperimentalWarning: `--experimental-loader` may be removed in the future; instead use `register()`:
--import 'data:text/javascript,import { register } from "node:module"; import { pathToFileURL } from "node:url"; register("./esm-loader.mjs", pathToFileURL("./"));'
(Use `node --trace-warnings ...` to show where the warning was created)
TAP version 13
# Subtest: hello world
    ok 1 - should work
    1..1
ok 1 - hello world # time=1.707ms

1..1
# time=3.009ms
```

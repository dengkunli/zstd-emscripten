# Zstd Emscripten build

This repo forks from [kig/zstd-emscripten](https://github.com/kig/zstd-emscripten), keeps upstream zstd dependency up-to-date, tweak the build to better suited for web, and fixes some bugs.

This build is based on [facebook/zstd](https://github.com/facebook/zstd) and provides a thin WebAssembly wrapper around the zstd.h API.

Thanks to Ilmari Heikkinen, Fredrick R. Brennan for their awesome work on the wasm build.

## Build

Skip the first line if you already have Emscripten set up.

```bash
git clone https://github.com/emscripten-core/emsdk.git && cd emsdk && ./emsdk install latest && ./emsdk activate latest && source ./emsdk_env.sh && cd .. &&
git clone https://github.com/dengkunli/zstd-emscripten && cd zstd-emscripten && git submodule update --init &&
mkdir -p build && cd build && emcmake cmake ../cmake/ && emmake make -j4 && cd .. &&
http-server . -p 8000
# open http://localhost:8000
```

The last line starts an http server using [http-server](https://www.npmjs.com/package/http-server), you can use any other utilities as you like.

## Usage

See the [test page](index.html) for examples on using the simple API and the streaming compression and decompression API.

Zstd-emscripten is a 1:1 binding to the ZSTD API in [zstd.h](https://github.com/facebook/zstd/blob/dev/lib/zstd.h), please refer to the [ZSTD docs](http://facebook.github.io/zstd/zstd_manual.html) for further details.

The compress-only and decompress-only versions of the library bind just a few functions, see [exported_functions_compress.txt](exported_functions_compress.txt) and [exported_functions_decompress.txt](exported_functions_decompress.txt) for the exported function lists. The full version function list is in [exported_functions.txt](exported_functions.txt).

## License

(c) 2016–2023 Ilmari Heikkinen, Fredrick R. Brennan, Kunli Deng. As with Zstd itself, this is dual-licensed under [BSD](LICENSE) and [GPLv2](COPYING).


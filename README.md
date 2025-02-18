# esbuild_deno_loader

Deno module resolution for `esbuild`.

## Example

This example bundles an entrypoint into a single ESM output.

```js
import * as esbuild from "https://deno.land/x/esbuild@v0.17.11/mod.js";
// Import the WASM build on platforms where running subprocesses is not
// permitted, such as Deno Deploy, or when running without `--allow-run`.
// import * as esbuild from "https://deno.land/x/esbuild@v0.17.11/wasm.js";

import { denoPlugin } from "https://deno.land/x/esbuild_deno_loader@0.6.0/mod.ts";

const result = await esbuild.build({
  plugins: [denoPlugin()],
  entryPoints: ["https://deno.land/std@0.178.0/bytes/mod.ts"],
  outfile: "./dist/bytes.esm.js",
  bundle: true,
  format: "esm",
});

console.log(result.outputFiles);

esbuild.stop();
```

## Permissions

This plugins requires the following permissions:

- `--allow-read` if you need to resolve local files.
- `--allow-net` if you need to resolve remote files.

If the program is run with `--allow-run`, the plugin will use the `deno` binary
to resolve remote files. This allows the plugin to re-use the Deno module cache.

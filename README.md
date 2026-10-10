# @tummycrypt/tinyland-color-utils

Pure TypeScript color utilities: WCAG contrast validation, color parsing
(hex, rgb/rgba, hsl/hsla, oklch, oklab, named colors), color space
conversions and LRU caches. No runtime dependencies and no DOM access.

## Entry points

| Import | Contents |
|---|---|
| `@tummycrypt/tinyland-color-utils` | parsing, conversion, contrast and WCAG helpers, caches, types |
| `@tummycrypt/tinyland-color-utils/types` | `RGB`, `HSL`, `OKLCH`, `OKLAB`, `ParsedColor`, `ContrastResult`, `WCAGLevel` and the other types |
| `@tummycrypt/tinyland-color-utils/cache` | the LRU cache class and the shared cache instances |

## Consuming (Bazel only)

This package is not published to npm. Consume it from
[xoxd-ai/bazel-registry](https://github.com/xoxd-ai/bazel-registry):

```starlark
bazel_dep(name = "tummycrypt_tinyland_color_utils", version = "1.0.0")
```

```starlark
load("@aspect_rules_js//npm:defs.bzl", "npm_link_package")

npm_link_package(
    name = "node_modules/@tummycrypt/tinyland-color-utils",
    src = "@tummycrypt_tinyland_color_utils//:pkg",
)
```

## Development

```sh
pnpm install
pnpm typecheck
pnpm test
bazel build //:pkg && bazel test //...
```

TypeScript 7.0.2, vitest 5.0.3 and vite 8.3.3 are pinned exactly. See CHANGELOG.md.

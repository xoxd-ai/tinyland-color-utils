# Changelog

## 1.0.0 (2026-10-09)

Major release for the 2026-10-08 estate uplift (RU1, RU10). The runtime API is
unchanged: every export of 0.2.3 (`.`, `./types`, `./cache`) keeps its name and
behaviour. The toolchain, module format and distribution change.

### Changed

- TypeScript 7.0.2, vitest 5.0.3 and vite 8.3.3 are pinned exactly (RU1, RU5,
  RU13); fast-check and @fast-check/vitest move to their vitest 5 lines.
- Relative imports in `src/` carry explicit `.js` specifiers, and the
  tsconfig uses `module`/`moduleResolution` `NodeNext`, so the emitted `dist/`
  resolves under plain Node ESM as well as under bundlers. This ports the
  tinyland.dev `packages/` copy (0.2.2) back into the standalone repo.
- tsconfig `lib` is `ES2022` only (the code uses no DOM API) and lists
  `"types": ["node"]`, which TypeScript 6+ no longer infers. `composite` is
  dropped.
- Bazel: aspect_rules_ts 3.10.1 with the `typescript` extension at 7.0.2
  (`ts_project` keeps `transpiler = "tsc"`); `package.json` is in the
  `vitest_test` data.
- Distribution is Bazel only (RU6, RU8): the package is `private`, and the
  publish workflow, `publishConfig` and `prepublishOnly` are removed.
- Repository, homepage and bugs URLs point at xoxd-ai.

### Migration

1. Stop installing `@tummycrypt/tinyland-color-utils` from npmjs or GitHub
   Packages; 0.2.x there is frozen and will be marked deprecated.
2. Re-pin: `bazel_dep(name = "tummycrypt_tinyland_color_utils", version = "1.0.0")`
   from xoxd-ai/bazel-registry, and link it with
   `npm_link_package(name = "node_modules/@tummycrypt/tinyland-color-utils", src = "@tummycrypt_tinyland_color_utils//:pkg")`.
3. Imports are unchanged. Consumers that deep-imported files under `dist/`
   should use the `.`, `./types` or `./cache` exports instead.

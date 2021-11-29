The problematic file is `packages/one/src/index.ts`.

When I try to import something from the `@pkg/lib` which is defined as the alias to `packages/one/src/lib` in `packages/one/tsconfig.json`, I get the following error: `Unable to resolve path to module '@pkg/lib'.eslintimport/no-unresolved`. So it's an alias used only withing a package of a monorepo.

However, when I try to import something from the other monorepo package then everything works well. In this case, I'm importing function from the `@root/shared` which points to `packages/shared/src/lib`.

In the `.vscode/settings.json` I have such a configuration:

```json
{
  "eslint.workingDirectories": [
    { "changeProcessCWD": true, "directory": "./packages/*" }
  ]
}
```

which in theory should cover both cases, but to make it work in VSCode I have to set the following `eslint.workingDirectories` rule:

```json
{
  "eslint.workingDirectories": [
    { "changeProcessCWD": true, "directory": "./packages/one" },
    { "changeProcessCWD": true, "directory": "./packages/*" }
  ]
}
```

And it's only issue in the ESLint extension for VSCode, as the `yarn lint` script is working fine and doesn't see any problem there.
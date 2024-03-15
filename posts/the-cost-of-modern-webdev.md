# the cost of modern web development

2023-10-17

The other night, I was uninstalling unnecessary packages I had installed with `brew` and realized there were far too many to account for. Instead of going through each package in `brew list` and looking up its respective purpose, I decided to purge the entire formulae:

```bash
brew remove --force $(brew list --formula)
```

Unfortunately, I came to the realization I was using a no longer supported version of macOS and as such, no longer supported by Homebrew. The consequence? Installing `node` via `brew` took rather long given it had to run the `node` `make` file, if I'm correct.

But otherwise, reinstalling the necessary packages, I was not surprised to infer the large memory cost of modern web development, i.e., Node.js-based development:

- `brew install node` requires ~58MB.
- `node`'s dependencies account for another ~242MB.
- Furthermore, take into account, for a given project, the `node_modules` folder and all the `"dependencies"` and `"devDependencies"`, and their dependencies, ad infinitum.
- Regardless of the latter ending up in a `.gitignore`, the memory requirements of modern web development is seemingly complex.

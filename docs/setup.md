# Project Setup

## Initialize Vite Project

```bash
npm create vite@latest .
```

- Framework: Lit
- Variant: Typescript

## Prettier Setup

### Install Prettier

```bash
npm install --save-dev prettier
```

### Add Prettier Config

Create `.prettierrc` in the project root

```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "es5",
  "printWidth": 100
}
```

### Ignore Files

Add a `.prettierignore` to skip node_modules, etc

```txt
node_modules
```

### Add Prettier Script

In `package.json`:

```json
"scripts": {
  "format": "prettier --write ."
}
```

### Format Files

```bash
npm run format
```

## ESLint Setup

### Install ESLint and Plugins

```bash
npm install --save-dev eslint typescript-eslint jiti eslint-plugin-import
```

### Create `eslint.config.ts`

```ts
import eslint from '@eslint/js';
import { defineConfig } from 'eslint/config';
import importPlugin from 'eslint-plugin-import';
import tseslint from 'typescript-eslint';

export default defineConfig(
  eslint.configs.recommended,
  tseslint.configs.recommended,
  {
    plugins: { import: importPlugin },
    rules: {
      'import/order': [
        'error',
        {
          groups: ['builtin', 'external', 'internal', 'parent', 'sibling', 'index'],
          alphabetize: { order: 'asc', caseInsensitive: true },
          'newlines-between': 'always',
        },
      ],
    },
  },
  {
    ignores: ['dist/*'],
  }
);
```

### Add ESLint Scripts

In `package.json:`

```json
"scripts": {
  "lint": "eslint . --ext .ts,.js",
  "lint:fix": "eslint . --ext .ts,.js --fix"
}
```

### Run ESLint

```bash
npm run lint      # check for issues
npm run lint:fix  # auto-fix issues
```

## Husky Setup

### Install Husky

```bash
npm install --save-dev husky
```

### Enable Git Hooks

```bash
npx husky init
```

It creates a `pre-commit` script in `.husky/` and updates the prepare script in `package.json`

### Update Pre-commit Hook

To automatically run ESLint auto-fix and Prettier formatting before each commit:

```bash
npm run lint:fix && npm run format
```

Now, whenever you commit changes:

```bash
git add .
git commit -m "your commit message"
```

Husky will first fix linting issues and format files, preventing unformatted or broken code from entering the repository.

## Storybook Setup

```bash
npm create storybook@latest
```

- Configuration: Minimal (component development only)

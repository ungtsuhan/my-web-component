# Project Setup

## Initialize Vite Project

```bash
npm create vite@latest .
```

- Framework: Lit
- Variant: Typescript

## Setup Prettier

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

## Setup ESLint

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

export default defineConfig(eslint.configs.recommended, tseslint.configs.recommended, {
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
});
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
# Check for linting issues
npm run lint

# Auto-fix issues where possible
npm run lint:fix
```

## Setup Storybook

```bash
npm create storybook@latest
```

- Configuration: Minimal (component development only)

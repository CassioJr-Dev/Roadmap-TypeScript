## Ecosystem TypeScript

Este README fornece uma visão geral do ecossistema TypeScript, abordando conceitos essenciais e fornecendo exemplos práticos sobre formatação, linting, pacotes úteis e ferramentas de construção.

### Índice

1. [Formatação](#formatação)
2. [Linting](#linting)
3. [Pacotes Úteis](#pacotes-úteis)
4. [Ferramentas de Construção](#ferramentas-de-construção)

---

### Formatação

A formatação de código é crucial para manter um código consistente e legível. No ecossistema TypeScript, uma ferramenta popular para formatação é o **Prettier**.

#### Prettier

O Prettier é um formatador de código opinativo que suporta muitos idiomas, incluindo TypeScript. Ele garante que o código tenha um estilo consistente, seguindo regras predefinidas.

**Instalação:**

```bash
npm install --save-dev prettier
```

**Configuração:**

Crie um arquivo `.prettierrc` na raiz do seu projeto:

```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all"
}
```

**Uso:**

Adicione um script no `package.json` para formatar o código:

```json
"scripts": {
  "format": "prettier --write 'src/**/*.{ts,tsx}'"
}
```

Execute o script:

```bash
npm run format
```

### Linting

Linting é o processo de analisar o código em busca de problemas potenciais. O **ESLint** é uma ferramenta popular para isso, e pode ser configurado para funcionar com TypeScript.

#### ESLint

**Instalação:**

```bash
npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

**Configuração:**

Crie um arquivo `.eslintrc.json` na raiz do seu projeto:

```json
{
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "rules": {
    "quotes": ["error", "single"],
    "semi": ["error", "always"]
  }
}
```

**Uso:**

Adicione um script no `package.json` para verificar o código:

```json
"scripts": {
  "lint": "eslint 'src/**/*.{ts,tsx}'"
}
```

Execute o script:

```bash
npm run lint
```

### Pacotes Úteis

Existem vários pacotes que podem ser úteis ao trabalhar com TypeScript. Aqui estão alguns dos mais populares:

#### TypeScript

O compilador TypeScript em si.

**Instalação:**

```bash
npm install --save-dev typescript
```

#### ts-node

Permite executar arquivos TypeScript diretamente.

**Instalação:**

```bash
npm install --save-dev ts-node
```

**Uso:**

```bash
npx ts-node src/index.ts
```

#### @types/node

Definições de tipos para Node.js, necessárias para projetos que usam Node.js.

**Instalação:**

```bash
npm install --save-dev @types/node
```

#### ts-jest

Um predefinido para testar TypeScript com Jest.

**Instalação:**

```bash
npm install --save-dev jest ts-jest @types/jest
```

**Configuração:**

Crie um arquivo `jest.config.js`:

```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
};
```

### Ferramentas de Construção

Ferramentas de construção são essenciais para empacotar e otimizar seu código TypeScript para produção. Aqui estão algumas das mais comuns:

#### Webpack

Um empacotador de módulos que ajuda a agrupar arquivos JavaScript para uso em um navegador.

**Instalação:**

```bash
npm install --save-dev webpack webpack-cli ts-loader
```

**Configuração:**

Crie um arquivo `webpack.config.js`:

```javascript
const path = require('path');

module.exports = {
  entry: './src/index.ts',
  module: {
    rules: [
      {
        test: /\.ts$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      },
    ],
  },
  resolve: {
    extensions: ['.ts', '.js'],
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

**Uso:**

Adicione um script no `package.json` para construir o projeto:

```json
"scripts": {
  "build": "webpack"
}
```

Execute o script:

```bash
npm run build
```

#### Rollup

Uma ferramenta de construção leve para pacotes de biblioteca.

**Instalação:**

```bash
npm install --save-dev rollup rollup-plugin-typescript2
```

**Configuração:**

Crie um arquivo `rollup.config.js`:

```javascript
import typescript from 'rollup-plugin-typescript2';

export default {
  input: 'src/index.ts',
  output: {
    file: 'dist/bundle.js',
    format: 'cjs',
  },
  plugins: [typescript()],
};
```

**Uso:**

Adicione um script no `package.json` para construir o projeto:

```json
"scripts": {
  "build": "rollup -c"
}
```

Execute o script:

```bash
npm run build
```

---

Este README fornece uma visão geral dos conceitos essenciais do ecossistema TypeScript, incluindo formatação, linting, pacotes úteis e ferramentas de construção. Seguindo estas práticas e utilizando estas ferramentas, você pode garantir um código TypeScript consistente, de alta qualidade e pronto para produção.

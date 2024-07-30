# Introdução ao TypeScript

TypeScript é um superset do JavaScript que adiciona tipagem estática e outros recursos avançados ao JavaScript. Ele é desenvolvido pela Microsoft e é amplamente usado para desenvolver grandes aplicações JavaScript que são mais robustas e mais fáceis de manter.

## TypeScript vs JavaScript

### JavaScript
- **Dinamicamente tipado**: As variáveis não têm um tipo fixo, podendo mudar ao longo do tempo.
- **Sem verificação de tipos**: Erros de tipo só são descobertos em tempo de execução.
- **Suporte nativo em navegadores**: Não necessita de transpilação para rodar em navegadores.

### TypeScript
- **Estaticamente tipado**: Permite a definição de tipos para variáveis, funções, etc., proporcionando verificação de tipos em tempo de compilação.
- **Verificação de tipos**: Erros de tipo são descobertos durante a compilação, antes de rodar o código.
- **Superset do JavaScript**: Todo código JavaScript válido é também código TypeScript válido.

```typescript
// JavaScript
let message = "Hello, World!";
message = 42; // Válido em JS, mas pode causar problemas em runtime

// TypeScript
let message: string = "Hello, World!";
message = 42; // Erro: Type 'number' is not assignable to type 'string'
```

## TS and JS Interoperability

TypeScript é totalmente compatível com JavaScript. Você pode usar bibliotecas JavaScript dentro de um projeto TypeScript e vice-versa.

### Usando uma biblioteca JavaScript em TypeScript

Para usar uma biblioteca JavaScript em TypeScript, você pode instalar os tipos da biblioteca (se disponíveis) usando npm.

```sh
npm install @types/lodash
```

```typescript
import _ from 'lodash';

const numbers = [1, 2, 3, 4, 5];
console.log(_.shuffle(numbers)); // Embaralha os números
```

### Usando TypeScript em um projeto JavaScript

Você pode gradualmente converter um projeto JavaScript para TypeScript, renomeando arquivos `.js` para `.ts` e adicionando tipos conforme necessário.

## Installation and Configuration

### Instalando TypeScript

Você pode instalar o TypeScript globalmente usando npm:

```sh
npm install -g typescript
```

### Configurando TypeScript: `tsconfig.json`

O arquivo `tsconfig.json` é usado para configurar o compilador TypeScript. Ele define as opções de compilação e os arquivos do projeto.

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "strict": true,
    "outDir": "./dist"
  },
  "include": ["src/**/*"]
}
```

### Opções do Compilador

Algumas opções comuns do compilador incluem:

- **target**: Especifica a versão do ECMAScript que você deseja que o código compilado seja compatível.
- **module**: Especifica o sistema de módulos (por exemplo, `commonjs` ou `es6`).
- **strict**: Ativa todas as verificações de tipo estritas.
- **outDir**: Especifica o diretório de saída para os arquivos compilados.

## Running TypeScript

### Compilando TypeScript com `tsc`

Para compilar arquivos TypeScript, você pode usar o comando `tsc`.

```sh
tsc
```

Isso compilará os arquivos TypeScript de acordo com as opções definidas em `tsconfig.json`.

### Executando TypeScript com `ts-node`

Você também pode executar arquivos TypeScript diretamente com `ts-node`, sem a necessidade de compilá-los previamente.

```sh
npx ts-node src/index.ts
```

### TS Playground

O TypeScript Playground é uma ferramenta online onde você pode experimentar TypeScript diretamente no navegador.

- [TypeScript Playground](https://www.typescriptlang.org/play)

Você pode escrever código TypeScript e ver a saída JavaScript gerada em tempo real, além de explorar diferentes opções do compilador.

## Conclusão

TypeScript oferece uma série de vantagens sobre o JavaScript, especialmente para projetos maiores e mais complexos. Com tipagem estática, verificação de tipos em tempo de compilação e uma configuração flexível, ele ajuda a construir aplicações mais robustas e fáceis de manter. Experimente o TypeScript e veja como ele pode melhorar seu fluxo de trabalho de desenvolvimento JavaScript!

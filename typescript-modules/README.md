## Módulos TypeScript

### Visão Geral

Os módulos do TypeScript ajudam a organizar o código dividindo-o em componentes menores e reutilizáveis. Os módulos podem ser usados para encapsular códigos relacionados, tornando mais fácil gerenciar dependências e evitar a poluição do namespace global.

### Índice

1. [Namespaces](#namespaces)
2. [Módulos Ambientais](#módulos-ambientais)
3. [Módulos Externos](#módulos-externos)
4. [Augmentação de Namespace](#augmentação-de-namespace)
5. [Augmentação Global](#augmentação-global)

### Namespaces

Namespaces são uma forma de agrupar código relacionado e evitar colisões de nomes encapsulando o código dentro de um escopo nomeado.

#### Exemplo

```typescript
namespace Utilidades {
  export function logMensagem(mensagem: string): void {
    console.log(mensagem);
  }

  export function mensagemErro(mensagem: string): void {
    console.error(mensagem);
  }
}

Utilidades.logMensagem("Esta é uma mensagem de log.");
Utilidades.mensagemErro("Esta é uma mensagem de erro.");
```

### Módulos Ambientais

Módulos ambientais são usados para descrever a forma de módulos que estão disponíveis no escopo global. Eles são úteis para trabalhar com bibliotecas de terceiros que não têm typings do TypeScript.

#### Exemplo

```typescript
// modulo-ambiental.d.ts
declare module "lodash" {
  export function chunk<T>(array: T[], size: number): T[][];
}

// uso.ts
import { chunk } from "lodash";

const resultado = chunk([1, 2, 3, 4, 5], 2);
console.log(resultado);
```

### Módulos Externos

Módulos externos são arquivos que usam a sintaxe `import` e `export` para compartilhar código entre diferentes arquivos. Esta abordagem está alinhada com os módulos ECMAScript (ESM).

#### Exemplo

```typescript
// matematica.ts
export function adicionar(a: number, b: number): number {
  return a + b;
}

export function subtrair(a: number, b: number): number {
  return a - b;
}

// principal.ts
import { adicionar, subtrair } from "./matematica";

console.log(adicionar(5, 3)); // Saída: 8
console.log(subtrair(5, 3)); // Saída: 2
```

### Augmentação de Namespace

Augmentação de namespace permite estender namespaces existentes com membros adicionais. Isso é útil para adicionar novos métodos ou propriedades a módulos existentes.

#### Exemplo

```typescript
// validacao.ts
namespace Validacao {
  export const numeroRegExp = /^[0-9]+$/;
  export function validarNumero(input: string): boolean {
    return numeroRegExp.test(input);
  }
}

// augmentacao.ts
namespace Validacao {
  export const letrasRegExp = /^[A-Za-z]+$/;
  export function validarLetras(input: string): boolean {
    return letrasRegExp.test(input);
  }
}

// principal.ts
/// <reference path="validacao.ts" />
/// <reference path="augmentacao.ts" />

console.log(Validacao.validarNumero("123")); // Saída: true
console.log(Validacao.validarLetras("ABC")); // Saída: true
```

### Augmentação Global

Augmentação global é usada para adicionar declarações ao escopo global, frequentemente utilizada para estender objetos globais ou declarar variáveis globais.

#### Exemplo

```typescript
// globais.d.ts
interface String {
  toTitleCase(): string;
}

// implementacao.ts
String.prototype.toTitleCase = function (): string {
  return this.replace(/\w\S*/g, (txt) => txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase());
};

// uso.ts
let str = "olá mundo";
console.log(str.toTitleCase()); // Saída: Olá Mundo
```

### Conclusão

Os módulos do TypeScript fornecem ferramentas poderosas para gerenciar e organizar seu código. Ao entender namespaces, módulos ambientais, módulos externos, tipos de template literal, augmentação de namespace e augmentação global, você pode escrever código mais modular, mantível e seguro em termos de tipos.

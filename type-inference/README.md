## Inferência de Tipos no TypeScript

### Introdução
O TypeScript, um superconjunto do JavaScript, adiciona tipos estáticos à linguagem. Uma de suas funcionalidades poderosas é a inferência de tipos, que permite ao TypeScript determinar automaticamente o tipo de uma variável, retorno de função ou expressão sem anotações explícitas de tipos. Isso leva a um código mais limpo, beneficiando-se ainda da segurança de tipos.

### Tabela de Conteúdos
1. [Inferência Básica de Tipos](#inferencia-basica-de-tipos)
2. [Melhor Tipo Comum](#melhor-tipo-comum)
3. [Tipagem Contextual](#tipagem-contextual)
4. [Inferência de Tipos em Funções](#inferencia-de-tipos-em-funcoes)
5. [Asserção de Tipos](#assercao-de-tipos)
6. [Inferência de Tipos com Genéricos](#inferencia-de-tipos-com-genericos)
7. [Inferência de Tipos Avançada](#inferencia-de-tipos-avancada)

### Inferência Básica de Tipos
O TypeScript infere o tipo das variáveis quando elas são inicializadas.

```typescript
let mensagem = "Olá, Mundo!"; // TypeScript infere o tipo como string
let contador = 42; // TypeScript infere o tipo como number
let ehValido = true; // TypeScript infere o tipo como boolean
```

### Melhor Tipo Comum
Ao inferir tipos para arrays, o TypeScript tenta inferir o melhor tipo comum.

```typescript
let numeros = [1, 2, 3, 4]; // TypeScript infere o tipo como number[]
let arrayMisto = [1, "dois", 3, "quatro"]; // TypeScript infere o tipo como (number | string)[]
```

### Tipagem Contextual
O TypeScript usa o contexto para inferir tipos, especialmente em expressões de funções e literais de objetos.

```typescript
window.onmousedown = function(event) {
    console.log(event.button); // TypeScript infere o tipo de event como MouseEvent
};

let meuObjeto = {
    nome: "TypeScript",
    idade: 8
}; // TypeScript infere o tipo como { nome: string; idade: number; }
```

### Inferência de Tipos em Funções
A inferência de tipos também funciona com tipos de retorno de funções e tipos de parâmetros.

```typescript
function adicionar(a: number, b: number) {
    return a + b; // TypeScript infere o tipo de retorno como number
}

const resultado = adicionar(5, 10); // TypeScript infere o tipo de resultado como number
```

### Asserção de Tipos
As asserções de tipos podem substituir o tipo inferido pelo TypeScript quando você sabe melhor.

```typescript
let algumValor: any = "Isto é uma string";
let tamanhoString: number = (algumValor as string).length;
```

### Inferência de Tipos com Genéricos
O TypeScript pode inferir tipos em funções e classes genéricas.

```typescript
function identidade<T>(arg: T): T {
    return arg;
}

let resultado = identidade("Olá"); // TypeScript infere T como string

class Caixa<T> {
    conteudo: T;
    constructor(valor: T) {
        this.conteudo = valor;
    }
}

let caixa = new Caixa(42); // TypeScript infere T como number
```

### Inferência de Tipos Avançada
O TypeScript pode inferir tipos em cenários mais complexos, como tipos mapeados e tipos condicionais.

```typescript
type Ponto = { x: number; y: number };
type PontoSomenteLeitura = Readonly<Ponto>; // TypeScript infere o tipo como { readonly x: number; readonly y: number; }

type NaoNulo<T> = T extends null | undefined ? never : T;
type Exemplo = NaoNulo<string | number | undefined>; // TypeScript infere o tipo como string | number
```

### Conclusão
A inferência de tipos no TypeScript é uma funcionalidade poderosa que ajuda a manter seu código conciso e legível, ao mesmo tempo em que mantém a segurança de tipos. Entender como o TypeScript infere tipos pode ajudá-lo a escrever um código melhor e mais fácil de manter.

### Referências
- [Manual do TypeScript](https://www.typescriptlang.org/docs/handbook/type-inference.html)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/type-inference)

---

Este README fornece uma visão geral da inferência de tipos no TypeScript com exemplos. Sinta-se à vontade para contribuir adicionando mais exemplos ou melhorando as explicações.
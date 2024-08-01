# TypeScript Functions

Este repositório contém exemplos e explicações sobre funções em TypeScript. Vamos abordar os seguintes tópicos:
- Tipagem de Funções
- Sobrecarga de Funções

## Tipagem de Funções

Em TypeScript, podemos definir o tipo dos parâmetros e o tipo de retorno de uma função para garantir que os valores passados e retornados correspondam aos tipos esperados. Isso ajuda a evitar erros e a melhorar a legibilidade do código.

### Exemplo

```typescript
// Definindo uma função com tipagem
function add(a: number, b: number): number {
    return a + b;
}

// Chamando a função
const result = add(5, 3);
console.log(result); // Saída: 8
```

### Funções Anônimas e Arrow Functions

Também podemos definir funções anônimas e arrow functions com tipagem.

```typescript
// Função anônima
const multiply = function (a: number, b: number): number {
    return a * b;
};

// Arrow function
const divide = (a: number, b: number): number => {
    return a / b;
};

// Chamando as funções
console.log(multiply(6, 2)); // Saída: 12
console.log(divide(10, 2)); // Saída: 5
```

## Sobrecarga de Funções

A sobrecarga de funções em TypeScript permite que uma função tenha várias assinaturas. Isso é útil quando uma função pode ser chamada com diferentes conjuntos de parâmetros, mas ainda assim deve ser tratada como a mesma função.

### Exemplo

```typescript
// Definindo assinaturas de sobrecarga
function combine(a: string, b: string): string;
function combine(a: number, b: number): number;

// Implementação da função
function combine(a: any, b: any): any {
    if (typeof a === "string" && typeof b === "string") {
        return a + b;
    }
    if (typeof a === "number" && typeof b === "number") {
        return a + b;
    }
    throw new Error("Parâmetros inválidos");
}

// Chamando a função com diferentes tipos de parâmetros
console.log(combine("Hello, ", "world!")); // Saída: Hello, world!
console.log(combine(10, 20)); // Saída: 30
```

### Mais Exemplo de Sobrecarga

```typescript
// Definindo assinaturas de sobrecarga para múltiplos tipos de parâmetros
function format(input: string, length: number): string;
function format(input: number, decimals: number): string;

// Implementação da função
function format(input: any, arg: any): string {
    if (typeof input === "string" && typeof arg === "number") {
        return input.padStart(arg, ' ');
    }
    if (typeof input === "number" && typeof arg === "number") {
        return input.toFixed(arg);
    }
    throw new Error("Parâmetros inválidos");
}

// Chamando a função com diferentes tipos de parâmetros
console.log(format("TypeScript", 15)); // Saída: '    TypeScript'
console.log(format(123.456, 2)); // Saída: '123.46'
```

## Conclusão

Este repositório apresentou uma visão geral das funções em TypeScript, com foco na tipagem de funções e sobrecarga de funções. TypeScript nos permite definir tipos explícitos para parâmetros e retornos de funções, o que melhora a segurança e legibilidade do código. A sobrecarga de funções é uma poderosa funcionalidade que permite que uma função lide com diferentes tipos e números de parâmetros.

Para mais informações, consulte a [documentação oficial do TypeScript](https://www.typescriptlang.org/docs/).

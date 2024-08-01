# TypeScript Interfaces

Este repositório contém exemplos e explicações sobre o uso de Interfaces em TypeScript. Aqui você encontrará informações sobre a diferença entre Types e Interfaces, como estender interfaces, declarar interfaces e usar tipos híbridos.

## Sumário

- [Types vs Interfaces](#types-vs-interfaces)
- [Extending Interfaces](#extending-interfaces)
- [Interface Declaration](#interface-declaration)
- [Hybrid Types](#hybrid-types)

## Types vs Interfaces

Em TypeScript, tanto `type` quanto `interface` são usados para definir formas de objetos. No entanto, há algumas diferenças sutis entre eles.

### Exemplo de `type`

```typescript
type Point = {
  x: number;
  y: number;
};

const point: Point = { x: 10, y: 20 };
```

### Exemplo de `interface`

```typescript
interface Point {
  x: number;
  y: number;
}

const point: Point = { x: 10, y: 20 };
```

### Diferenças Principais

- **Extensão e Implementação**: Interfaces podem ser estendidas ou implementadas por classes, enquanto types não podem ser implementados, mas podem ser combinados usando interseção (`&`).
- **Declarar Múltiplas Vezes**: Interfaces podem ser declaradas várias vezes e serão mescladas automaticamente. Types não permitem isso.

## Extending Interfaces

Interfaces podem ser estendidas para criar novas interfaces que herdam propriedades de uma ou mais interfaces.

### Exemplo

```typescript
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

const myDog: Dog = { name: "Buddy", breed: "Golden Retriever" };
```

## Interface Declaration

A declaração de interfaces em TypeScript é feita usando a palavra-chave `interface`.

### Exemplo

```typescript
interface Person {
  firstName: string;
  lastName: string;
  age: number;
}

const person: Person = { firstName: "John", lastName: "Doe", age: 30 };
```

## Hybrid Types

Tipos híbridos são interfaces que descrevem objetos que podem ser chamados como funções e também possuem propriedades.

### Exemplo

```typescript
interface Counter {
  (start: number): string;
  interval: number;
  reset(): void;
}

const getCounter = (): Counter => {
  const counter = ((start: number) => `Count: ${start}`) as Counter;
  counter.interval = 1000;
  counter.reset = () => console.log("Counter reset!");
  return counter;
};

const counter = getCounter();
console.log(counter(10)); // Count: 10
console.log(counter.interval); // 1000
counter.reset(); // Counter reset!
```

## Contribuição

Sinta-se à vontade para contribuir com este repositório. Se encontrar algum problema ou tiver sugestões de melhorias, abra uma issue ou envie um pull request.
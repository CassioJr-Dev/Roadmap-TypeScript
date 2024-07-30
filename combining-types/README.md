# Combining Types em TypeScript

Este repositório contém exemplos e explicações sobre os conceitos de **Combining Types** em TypeScript. Exploramos quatro tópicos principais:

1. Union Types
2. Intersection Types
3. Type Aliases
4. `keyof` operator

## Índice

1. [Union Types](#union-types)
2. [Intersection Types](#intersection-types)
3. [Type Aliases](#type-aliases)
4. [keyof operator](#keyof-operator)

## Union Types

Union Types permitem que uma variável assuma mais de um tipo. Você pode definir um tipo que pode ser qualquer um dos valores especificados.

### Exemplo

```typescript
let value: string | number;

value = "Hello";
console.log(value);  // Output: Hello

value = 42;
console.log(value);  // Output: 42
```

## Intersection Types

Intersection Types combinam múltiplos tipos em um único tipo. Uma variável deste tipo deve satisfazer todos os tipos combinados.

### Exemplo

```typescript
interface Person {
  name: string;
}

interface Employee {
  employeeId: number;
}

type EmployeePerson = Person & Employee;

let employee: EmployeePerson = {
  name: "Alice",
  employeeId: 123
};

console.log(employee);  // Output: { name: 'Alice', employeeId: 123 }
```

## Type Aliases

Type Aliases permitem criar um nome personalizado para um tipo. Eles podem simplificar tipos complexos ou tornar o código mais legível.

### Exemplo

```typescript
type StringOrNumber = string | number;

let value: StringOrNumber;

value = "Hello";
console.log(value);  // Output: Hello

value = 42;
console.log(value);  // Output: 42
```

## `keyof` operator

O operador `keyof` é usado para criar um tipo que consiste nas chaves de um tipo de objeto.

### Exemplo

```typescript
interface Person {
  name: string;
  age: number;
}

type PersonKeys = keyof Person;  // "name" | "age"

let key: PersonKeys;

key = "name";
console.log(key);  // Output: name

key = "age";
console.log(key);  // Output: age
```

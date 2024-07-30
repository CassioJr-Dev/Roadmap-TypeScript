# Type Compatibility in TypeScript

TypeScript é um superconjunto tipado de JavaScript que adiciona tipos estáticos ao código. Um dos conceitos fundamentais no TypeScript é a "Type Compatibility" (compatibilidade de tipos). Este documento explica esse conceito e fornece exemplos para ilustrar como ele funciona.

## Índice

1. [Introdução](#introdução)
2. [Compatibilidade Estrutural](#compatibilidade-estrutural)
3. [Compatibilidade entre Classes](#compatibilidade-entre-classes)
4. [Compatibilidade entre Funções](#compatibilidade-entre-funções)
5. [Compatibilidade com Tipos Genéricos](#compatibilidade-com-tipos-genéricos)
6. [Exemplos Adicionais](#exemplos-adicionais)

## Introdução

No TypeScript, a compatibilidade de tipos refere-se à capacidade de um tipo ser usado no lugar de outro tipo. TypeScript usa um sistema de compatibilidade estrutural, o que significa que a compatibilidade é determinada pela forma (estrutura) dos tipos.

## Compatibilidade Estrutural

Dois tipos são considerados compatíveis se suas estruturas forem compatíveis. Isto é, se um tipo tiver todas as propriedades requeridas pelo outro tipo.

```typescript
interface Person {
    name: string;
    age: number;
}

interface Employee {
    name: string;
    age: number;
    salary: number;
}

let person: Person = { name: "Alice", age: 25 };
let employee: Employee = { name: "Bob", age: 30, salary: 50000 };

// Compatível porque Employee tem todas as propriedades de Person
person = employee;

console.log(person); // { name: "Bob", age: 30 }
```

## Compatibilidade entre Classes

Classes seguem as mesmas regras de compatibilidade estrutural que interfaces.

```typescript
class Animal {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
}

class Dog extends Animal {
    breed: string;
    constructor(name: string, breed: string) {
        super(name);
        this.breed = breed;
    }
}

let animal: Animal;
let dog: Dog = new Dog("Buddy", "Golden Retriever");

// Compatível porque Dog tem todas as propriedades de Animal
animal = dog;

console.log(animal); // Animal { name: "Buddy" }
```

## Compatibilidade entre Funções

Para funções, a compatibilidade é determinada pela compatibilidade dos parâmetros e do tipo de retorno.

```typescript
let x = (a: number) => 0;
let y = (b: number, c: string) => 0;

// Compatível porque 'x' pode ignorar parâmetros adicionais
y = x;

console.log(y(1, "test")); // 0
```

Para o tipo de retorno, a compatibilidade funciona da mesma maneira que para outros tipos.

```typescript
let z = () => ({ name: "Alice" });
let w = () => ({ name: "Alice", age: 25 });

// Compatível porque o tipo de retorno de 'w' tem todas as propriedades de 'z'
z = w;

console.log(z()); // { name: "Alice", age: 25 }
```

## Compatibilidade com Tipos Genéricos

A compatibilidade também se aplica a tipos genéricos. A estrutura interna do tipo genérico é o que importa.

```typescript
interface Container<T> {
    value: T;
}

let container1: Container<number> = { value: 42 };
let container2: Container<string> = { value: "Hello" };

// Incompatível porque os tipos genéricos são diferentes
// container1 = container2; // Erro

let container3: Container<number> = { value: 100 };

// Compatível porque os tipos genéricos são iguais
container1 = container3;

console.log(container1); // { value: 100 }
```

## Exemplos Adicionais

### Comparação de Enums

Enums são compatíveis com números e vice-versa.

```typescript
enum Status {
    Ready,
    Waiting
}

let num: number = Status.Ready;
console.log(num); // 0

let status: Status = 1;
console.log(status); // 1
```

### Comparação de Tipos Interseção e União

Tipos interseção combinam várias estruturas, enquanto tipos união permitem múltiplos tipos alternativos.

```typescript
interface A {
    a: string;
}

interface B {
    b: string;
}

type C = A & B; // Interseção

let c: C = { a: "Hello", b: "World" };
console.log(c); // { a: "Hello", b: "World" }

type D = A | B; // União

let d1: D = { a: "Hello" };
let d2: D = { b: "World" };

console.log(d1); // { a: "Hello" }
console.log(d2); // { b: "World" }
```

## Conclusão

A compatibilidade de tipos no TypeScript é um conceito poderoso que permite flexibilidade ao trabalhar com diferentes tipos de dados. A compreensão da compatibilidade estrutural, bem como de como ela se aplica a classes, funções e tipos genéricos, é essencial para tirar o máximo proveito do TypeScript.

# TypeScript Types

Este README descreve os conceitos fundamentais dos tipos em TypeScript com exemplos para ajudar na compreensão.

## Índice
1. [Assertions](#assertions)
   - [as const](#as-const)
   - [as type](#as-type)
   - [as any](#as-any)
2. [Primitive Types](#primitive-types)
   - [boolean](#boolean)
   - [number](#number)
   - [string](#string)
   - [void](#void)
   - [undefined](#undefined)
   - [null](#null)
3. [Object Types](#object-types)
   - [Interface](#interface)
   - [Class](#class)
   - [Enum](#enum)
   - [Arrays](#arrays)
   - [Tuples](#tuples)
4. [Other Types](#other-types)
   - [any](#any)
   - [object](#object)
   - [unknown](#unknown)
   - [never](#never)

## Assertions

### as const

`as const` é usado para dizer ao TypeScript que uma expressão deve ser tratada como uma constante literal.

```typescript
let x = 'hello' as const;
// x é do tipo 'hello' e não pode ser alterado
```

### as type

`as type` é usado para fazer uma conversão explícita de um tipo para outro.

```typescript
let y: any = 'hello';
let z = y as string;
// z é do tipo string
```

### as any

`as any` é usado para suprimir verificações de tipo e tratar a variável como `any`.

```typescript
let a: unknown = 'hello';
let b = a as any;
// b é do tipo any
```

## Primitive Types

### boolean

O tipo `boolean` representa um valor verdadeiro ou falso.

```typescript
let isDone: boolean = false;
```

### number

O tipo `number` representa valores numéricos.

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

### string

O tipo `string` representa uma sequência de caracteres.

```typescript
let color: string = 'blue';
color = 'red';
```

### void

O tipo `void` é usado para funções que não retornam um valor.

```typescript
function warnUser(): void {
    console.log("This is my warning message");
}
```

### undefined

O tipo `undefined` indica que uma variável foi declarada mas não tem um valor atribuído.

```typescript
let u: undefined = undefined;
```

### null

O tipo `null` representa um valor nulo.

```typescript
let n: null = null;
```

## Object Types

### Interface

Interfaces são usadas para definir a forma de um objeto.

```typescript
interface Person {
    firstName: string;
    lastName: string;
}

let user: Person = {
    firstName: "John",
    lastName: "Doe"
};
```

### Class

Classes são usadas para criar objetos com propriedades e métodos.

```typescript
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}

let greeter = new Greeter("world");
```

### Enum

Enums são usados para definir um conjunto de constantes com nomes.

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

### Arrays

Arrays são usados para armazenar múltiplos valores do mesmo tipo.

```typescript
let list: number[] = [1, 2, 3];
```

### Tuples

Tuples são usadas para armazenar um conjunto de valores de tipos variados.

```typescript
let x: [string, number];
x = ["hello", 10]; // OK
```

## Other Types

### any

O tipo `any` permite que você atribua qualquer valor a uma variável.

```typescript
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

### object

O tipo `object` representa valores que não são primitivos (números, strings, booleanos, símbolos, null ou undefined).

```typescript
let obj: object = { name: "Alice" };
```

### unknown

O tipo `unknown` é similar ao `any`, mas mais seguro porque não permite operações arbitrárias.

```typescript
let notSure: unknown = 4;
if (typeof notSure === "string") {
    console.log(notSure.length);
}
```

### never

O tipo `never` representa o tipo de valores que nunca ocorrem. Por exemplo, uma função que lança uma exceção ou que nunca retorna.

```typescript
function error(message: string): never {
    throw new Error(message);
}
```

---

Espero que este README ajude a entender os tipos em TypeScript. Sinta-se à vontade para contribuir com exemplos adicionais ou correções!

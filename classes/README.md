# Classes em TypeScript

Este repositório contém exemplos de código que explicam conceitos fundamentais de classes em TypeScript. Os tópicos abordados incluem Constructor Params, Constructor Overloading, Access Modifiers, Abstract Classes, Inheritance vs Polymorphism e Method Overriding.

## Índice

- [Constructor Params](#constructor-params)
- [Constructor Overloading](#constructor-overloading)
- [Access Modifiers](#access-modifiers)
- [Abstract Classes](#abstract-classes)
- [Inheritance vs Polymorphism](#inheritance-vs-polymorphism)
- [Method Overriding](#method-overriding)

## Constructor Params

Em TypeScript, podemos definir parâmetros no construtor da classe, que são usados para inicializar as propriedades da classe.

```typescript
class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

const person = new Person("John", 30);
console.log(person.name); // John
console.log(person.age);  // 30
```

## Constructor Overloading

TypeScript não suporta sobrecarga de construtor diretamente, mas podemos simular esse comportamento usando parâmetros opcionais.

```typescript
class Person {
    name: string;
    age: number;

    constructor(name: string);
    constructor(name: string, age: number);
    constructor(name: string, age?: number) {
        this.name = name;
        this.age = age !== undefined ? age : 0;
    }
}

const person1 = new Person("John");
const person2 = new Person("Jane", 25);

console.log(person1.name, person1.age); // John 0
console.log(person2.name, person2.age); // Jane 25
```

## Access Modifiers

TypeScript suporta modificadores de acesso public, private e protected.

```typescript
class Person {
    public name: string;
    private age: number;
    protected address: string;

    constructor(name: string, age: number, address: string) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    getAge(): number {
        return this.age;
    }
}

const person = new Person("John", 30, "123 Main St");
console.log(person.name);    // John
console.log(person.getAge()); // 30
// console.log(person.age);  // Erro: 'age' é privado
// console.log(person.address); // Erro: 'address' é protegido
```

## Abstract Classes

Classes abstratas não podem ser instanciadas e podem conter métodos abstratos que devem ser implementados por classes derivadas.

```typescript
abstract class Animal {
    abstract makeSound(): void;

    move(): void {
        console.log("Moving...");
    }
}

class Dog extends Animal {
    makeSound(): void {
        console.log("Bark!");
    }
}

const dog = new Dog();
dog.makeSound(); // Bark!
dog.move();      // Moving...
```

## Inheritance vs Polymorphism

Herança permite que uma classe derive de outra, enquanto o polimorfismo permite que uma função ou método opere em objetos de diferentes tipos.

```typescript
class Animal {
    move(): void {
        console.log("Moving...");
    }
}

class Dog extends Animal {
    move(): void {
        console.log("Running...");
    }
}

class Bird extends Animal {
    move(): void {
        console.log("Flying...");
    }
}

const animals: Animal[] = [new Dog(), new Bird()];

animals.forEach(animal => animal.move());
// Running...
// Flying...
```

## Method Overriding

Classes derivadas podem sobrescrever métodos da classe base para fornecer uma implementação específica.

```typescript
class Animal {
    makeSound(): void {
        console.log("Some generic sound");
    }
}

class Dog extends Animal {
    makeSound(): void {
        console.log("Bark!");
    }
}

const genericAnimal = new Animal();
const dog = new Dog();

genericAnimal.makeSound(); // Some generic sound
dog.makeSound();           // Bark!
```
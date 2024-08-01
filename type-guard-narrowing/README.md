# Type Guards / Narrowing em TypeScript

Este repositório contém exemplos e explicações sobre os conceitos de Type Guards e Narrowing em TypeScript. Type Guards são técnicas utilizadas para refinar o tipo de uma variável dentro de um escopo, permitindo ao TypeScript entender melhor quais tipos são possíveis em diferentes partes do código.

## Tópicos

1. [instanceof](#instanceof)
2. [typeof](#typeof)
3. [Equality](#equality)
4. [Truthiness](#truthiness)
5. [Type Predicates](#type-predicates)

## `instanceof`

O operador `instanceof` é usado para verificar se um objeto é uma instância de uma determinada classe ou função construtora.

```typescript
class Dog {
  bark() {
    console.log('Woof!');
  }
}

class Cat {
  meow() {
    console.log('Meow!');
  }
}

function makeNoise(animal: Dog | Cat) {
  if (animal instanceof Dog) {
    animal.bark();
  } else if (animal instanceof Cat) {
    animal.meow();
  }
}

const myDog = new Dog();
const myCat = new Cat();

makeNoise(myDog); // Woof!
makeNoise(myCat); // Meow!
```

## `typeof`

O operador `typeof` é usado para verificar o tipo primitivo de uma variável (string, number, boolean, etc).

```typescript
function logValue(value: string | number) {
  if (typeof value === 'string') {
    console.log(`String: ${value}`);
  } else if (typeof value === 'number') {
    console.log(`Number: ${value}`);
  }
}

logValue("Hello"); // String: Hello
logValue(42); // Number: 42
```

## Equality

A verificação de igualdade pode ser usada para narrow types ao comparar valores conhecidos.

```typescript
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function getPet(pet: Fish | Bird) {
  if ('swim' in pet) {
    return pet.swim();
  } else {
    return pet.fly();
  }
}

const fish: Fish = { swim: () => console.log('Swimming!') };
const bird: Bird = { fly: () => console.log('Flying!') };

getPet(fish); // Swimming!
getPet(bird); // Flying!
```

## Truthiness

Valores truthy e falsy podem ser usados para narrowing, permitindo ao TypeScript inferir o tipo dentro de um escopo específico.

```typescript
function printMessage(message?: string) {
  if (message) {
    console.log(message.toUpperCase());
  } else {
    console.log('No message provided.');
  }
}

printMessage('Hello, world!'); // HELLO, WORLD!
printMessage(); // No message provided.
```

## Type Predicates

Os predicados de tipo (`is`) permitem definir funções que retornam um booleano e ao mesmo tempo narrows the type.

```typescript
type Car = { drive: () => void };
type Bike = { ride: () => void };

function isCar(vehicle: Car | Bike): vehicle is Car {
  return (vehicle as Car).drive !== undefined;
}

function useVehicle(vehicle: Car | Bike) {
  if (isCar(vehicle)) {
    vehicle.drive();
  } else {
    vehicle.ride();
  }
}

const myCar: Car = { drive: () => console.log('Driving!') };
const myBike: Bike = { ride: () => console.log('Riding!') };

useVehicle(myCar); // Driving!
useVehicle(myBike); // Riding!
```

## Contribuições

Sinta-se à vontade para abrir issues ou enviar pull requests se tiver sugestões ou melhorias.
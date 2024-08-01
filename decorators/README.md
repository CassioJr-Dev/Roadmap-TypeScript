## Decorators em TypeScript

Os decorators em TypeScript são uma funcionalidade poderosa que permite adicionar comportamento a classes, métodos, acessores, propriedades ou parâmetros de maneira declarativa. Eles são largamente inspirados por uma proposta da ECMAScript e são uma característica comum em frameworks como Angular.

### Sumário

1. [Introdução](#introdução)
2. [Decorator de Classe](#decorator-de-classe)
3. [Decorator de Método](#decorator-de-método)
4. [Decorator de Acessor](#decorator-de-acessor)
5. [Decorator de Propriedade](#decorator-de-propriedade)
6. [Decorator de Parâmetro](#decorator-de-parâmetro)
7. [Exemplo Completo](#exemplo-completo)

### Introdução

Decorators são funções que são aplicadas a declarações de classes, métodos, acessores, propriedades ou parâmetros. Eles fornecem uma maneira de modificar o comportamento desses elementos de forma declarativa.

Para usar decorators em TypeScript, é necessário habilitar a opção `experimentalDecorators` no `tsconfig.json`.

```json
{
  "compilerOptions": {
    "experimentalDecorators": true
  }
}
```

### Decorator de Classe

Um decorator de classe é uma função que recebe o construtor da classe como argumento e pode ser usado para modificar ou substituir a classe.

```typescript
function logClass(constructor: Function) {
  console.log(`Classe criada: ${constructor.name}`);
}

@logClass
class ExampleClass {
  constructor() {
    console.log('Instância criada');
  }
}

const instance = new ExampleClass(); // Saída: Classe criada: ExampleClass | Instância criada
```

### Decorator de Método

Decorators de método podem ser usados para interceptar e modificar o comportamento dos métodos de uma classe.

```typescript
function logMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function(...args: any[]) {
    console.log(`Método chamado: ${propertyKey} com argumentos: ${args}`);
    return originalMethod.apply(this, args);
  };

  return descriptor;
}

class ExampleClass {
  @logMethod
  sayHello(name: string) {
    console.log(`Hello, ${name}`);
  }
}

const instance = new ExampleClass();
instance.sayHello('World'); // Saída: Método chamado: sayHello com argumentos: World | Hello, World
```

### Decorator de Acessor

Decorators de acessor podem ser usados para interceptar e modificar o comportamento de getters e setters de propriedades de uma classe.

```typescript
function configurable(value: boolean) {
  return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    descriptor.configurable = value;
  };
}

class ExampleClass {
  private _name: string = 'default';

  @configurable(false)
  get name() {
    return this._name;
  }

  set name(value: string) {
    this._name = value;
  }
}

const instance = new ExampleClass();
console.log(Object.getOwnPropertyDescriptor(instance, 'name')); // Saída: { get: [Function: get name], set: [Function: set name], enumerable: false, configurable: false }
```

### Decorator de Propriedade

Decorators de propriedade podem ser usados para modificar as propriedades de uma classe.

```typescript
function logProperty(target: any, propertyKey: string) {
  let value = target[propertyKey];

  const getter = () => {
    console.log(`Getter para ${propertyKey} retornando ${value}`);
    return value;
  };

  const setter = (newVal: any) => {
    console.log(`Setter para ${propertyKey} com valor ${newVal}`);
    value = newVal;
  };

  Object.defineProperty(target, propertyKey, {
    get: getter,
    set: setter,
    enumerable: true,
    configurable: true
  });
}

class ExampleClass {
  @logProperty
  public name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const instance = new ExampleClass('TypeScript'); // Saída: Setter para name com valor TypeScript
console.log(instance.name); // Saída: Getter para name retornando TypeScript | TypeScript
instance.name = 'Decorators'; // Saída: Setter para name com valor Decorators
```

### Decorator de Parâmetro

Decorators de parâmetro podem ser usados para modificar os parâmetros de um método de uma classe.

```typescript
function logParameter(target: any, propertyKey: string, parameterIndex: number) {
  const metadataKey = `log_${propertyKey}_parameters`;

  if (Array.isArray(target[metadataKey])) {
    target[metadataKey].push(parameterIndex);
  } else {
    target[metadataKey] = [parameterIndex];
  }
}

class ExampleClass {
  sayHello(@logParameter name: string) {
    console.log(`Hello, ${name}`);
  }
}

const instance = new ExampleClass();
instance.sayHello('World'); // Saída: Hello, World
console.log((instance as any).log_sayHello_parameters); // Saída: [0]
```

### Exemplo Completo

```typescript
function logClass(constructor: Function) {
  console.log(`Classe criada: ${constructor.name}`);
}

function logMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function(...args: any[]) {
    console.log(`Método chamado: ${propertyKey} com argumentos: ${args}`);
    return originalMethod.apply(this, args);
  };

  return descriptor;
}

function configurable(value: boolean) {
  return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    descriptor.configurable = value;
  };
}

function logProperty(target: any, propertyKey: string) {
  let value = target[propertyKey];

  const getter = () => {
    console.log(`Getter para ${propertyKey} retornando ${value}`);
    return value;
  };

  const setter = (newVal: any) => {
    console.log(`Setter para ${propertyKey} com valor ${newVal}`);
    value = newVal;
  };

  Object.defineProperty(target, propertyKey, {
    get: getter,
    set: setter,
    enumerable: true,
    configurable: true
  });
}

function logParameter(target: any, propertyKey: string, parameterIndex: number) {
  const metadataKey = `log_${propertyKey}_parameters`;

  if (Array.isArray(target[metadataKey])) {
    target[metadataKey].push(parameterIndex);
  } else {
    target[metadataKey] = [parameterIndex];
  }
}

@logClass
class ExampleClass {
  @logProperty
  public name: string;

  constructor(name: string) {
    this.name = name;
  }

  @configurable(false)
  get displayName() {
    return this.name;
  }

  @logMethod
  sayHello(@logParameter name: string) {
    console.log(`Hello, ${name}`);
  }
}

const instance = new ExampleClass('TypeScript'); // Saída: Classe criada: ExampleClass | Setter para name com valor TypeScript
console.log(instance.name); // Saída: Getter para name retornando TypeScript | TypeScript
instance.name = 'Decorators'; // Saída: Setter para name com valor Decorators
console.log(instance.displayName); // Saída: Getter para name retornando Decorators | Decorators
instance.sayHello('World'); // Saída: Método chamado: sayHello com argumentos: World | Hello, World
```

### Conclusão

Decorators em TypeScript são uma ferramenta poderosa para adicionar comportamento e modificar o funcionamento de classes, métodos, acessores, propriedades e parâmetros. Eles oferecem uma forma declarativa de aplicar lógica adicional e são essenciais em frameworks modernos como Angular.

# Generics em TypeScript

Generics em TypeScript fornecem uma maneira de criar componentes reutilizáveis. Esses componentes podem trabalhar com qualquer tipo de dado e são particularmente úteis para criar coleções de dados. Generics garantem que os tipos usados sejam consistentes ao longo do código.

## Tabela de Conteúdos
- [Tipos Genéricos](#tipos-genéricos)
  - [Exemplo Básico de Genérico](#exemplo-básico-de-genérico)
  - [Usando Múltiplas Variáveis de Tipo](#usando-múltiplas-variáveis-de-tipo)
- [Restrições Genéricas](#restrições-genéricas)
  - [Usando Restrições](#usando-restrições)
  - [Estendendo Múltiplos Tipos](#estendendo-múltiplos-tipos)
  - [Usando Parâmetros de Tipo em Restrições Genéricas](#usando-parâmetros-de-tipo-em-restrições-genéricas)

## Tipos Genéricos

### Exemplo Básico de Genérico

Um exemplo básico de genérico pode ser uma função que pode trabalhar com qualquer tipo de dado:

```typescript
function identidade<T>(arg: T): T {
  return arg;
}

let resultado1 = identidade<string>("Olá");
let resultado2 = identidade<number>(42);

console.log(resultado1); // Saída: Olá
console.log(resultado2); // Saída: 42
```

No exemplo acima, `T` é uma variável de tipo que atua como um espaço reservado para o tipo que será fornecido quando a função for chamada.

### Usando Múltiplas Variáveis de Tipo

Genéricos também podem ser usados com múltiplas variáveis de tipo:

```typescript
function par<U, V>(primeiro: U, segundo: V): [U, V] {
  return [primeiro, segundo];
}

let par1 = par<string, number>("idade", 30);
let par2 = par<boolean, string>(true, "sucesso");

console.log(par1); // Saída: ['idade', 30]
console.log(par2); // Saída: [true, 'sucesso']
```

Neste exemplo, `U` e `V` são variáveis de tipo que podem representar qualquer tipo fornecido quando a função for chamada.

## Restrições Genéricas

Restrições genéricas permitem limitar os tipos que podem ser usados em uma função ou classe genérica. Isso é útil quando você precisa garantir que o tipo fornecido tenha certas propriedades ou métodos.

### Usando Restrições

Você pode usar a palavra-chave `extends` para especificar uma restrição:

```typescript
interface ComComprimento {
  length: number;
}

function identidadeComLog<T extends ComComprimento>(arg: T): T {
  console.log(arg.length);
  return arg;
}

identidadeComLog({ length: 10, value: "Olá" }); // Saída: 10
// identidadeComLog(3); // Erro: Argument of type 'number' is not assignable to parameter of type 'ComComprimento'.
```

Neste exemplo, a função `identidadeComLog` só aceita argumentos que tenham uma propriedade `length`.

### Estendendo Múltiplos Tipos

Você pode estender múltiplos tipos usando tipos de interseção:

```typescript
interface Nome {
  name: string;
}

interface Idade {
  age: number;
}

function infoPessoa<T extends Nome & Idade>(pessoa: T): string {
  return `Nome: ${pessoa.name}, Idade: ${pessoa.age}`;
}

const pessoa = { name: "João", age: 25, location: "Nova York" };
console.log(infoPessoa(pessoa)); // Saída: Nome: João, Idade: 25
```

Neste exemplo, `T` deve estender ambas as interfaces `Nome` e `Idade`, garantindo que a função `infoPessoa` só aceite objetos que tenham as propriedades `name` e `age`.

### Usando Parâmetros de Tipo em Restrições Genéricas

Parâmetros de tipo também podem ser usados em restrições:

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

let pessoa = { name: "João", age: 25 };
let nomePessoa = getProperty(pessoa, "name");
let idadePessoa = getProperty(pessoa, "age");

console.log(nomePessoa); // Saída: João
console.log(idadePessoa); // Saída: 25
```

Neste exemplo, `K` é restringido para ser uma chave de `T`, garantindo que `getProperty` só aceite nomes de propriedades válidas do objeto `T`.

---

Este README fornece uma visão geral do uso de Generics em TypeScript, focando em Tipos Genéricos e Restrições Genéricas. Com essas ferramentas, você pode criar componentes flexíveis e seguros que podem trabalhar com uma variedade de tipos de dados.

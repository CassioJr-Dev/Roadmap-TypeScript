## Advanced Types em TypeScript

Este documento aborda os conceitos avançados em TypeScript, com foco em Mapped Types, Conditional Types, Literal Types, Template Literal Types e Recursive Types. Cada seção inclui explicações detalhadas e exemplos práticos para ajudar a entender e aplicar esses conceitos em seus projetos.

## Mapped Types

Mapped Types são tipos que são construídos transformando propriedades de um tipo existente. Eles permitem criar novos tipos com base nas propriedades de outros tipos.

## Exemplo

```typescript
type Person = {
    name: string;
    age: number;
    address: string;
};

// Tornando todas as propriedades opcionais
type PartialPerson = {
    [P in keyof Person]?: Person[P];
};

// Tornando todas as propriedades somente leitura
type ReadonlyPerson = {
    [P in keyof Person]: Readonly<Person[P]>;
};
```

## Conditional Types

Conditional Types permitem criar tipos que dependem de uma condição. Eles funcionam de forma semelhante às instruções if em JavaScript, mas para tipos.

## Exemplo

```typescript
type IsString<T> = T extends string ? 'Yes' : 'No';

type A = IsString<string>; // 'Yes'
type B = IsString<number>; // 'No'

// Usando Conditional Types com genéricos
type Flatten<T> = T extends any[] ? T[number] : T;

type Str = Flatten<string[]>; // string
type Num = Flatten<number[]>; // number
type Bool = Flatten<boolean>; // boolean
```

## Literal Types

Literal Types permitem especificar um conjunto exato de valores que um tipo pode ter. Eles são úteis para criar tipos restritivos.

## Exemplo

```typescript
type Direction = 'up' | 'down' | 'left' | 'right';

function move(direction: Direction) {
    console.log(`Moving ${direction}`);
}

move('up');    // Válido
move('down');  // Válido
move('left');  // Válido
move('right'); // Válido
// move('forward'); // Erro: Argument of type '"forward"' is not assignable to parameter of type 'Direction'.
```

## Template Literal Types

Template Literal Types combinam literais de string com tipos para criar novas strings. Eles são úteis para criar tipos de string dinâmicos.

## Exemplo

```typescript
type Color = 'red' | 'green' | 'blue';
type Shade = 'light' | 'dark';

type ColorShade = `${Shade}-${Color}`;

let color1: ColorShade = 'light-red'; // Válido
let color2: ColorShade = 'dark-blue'; // Válido
// let color3: ColorShade = 'bright-yellow'; // Erro: Type '"bright-yellow"' is not assignable to type 'ColorShade'.
```

## Recursive Types

Recursive Types são tipos que se referenciam dentro de sua definição. Eles são úteis para representar estruturas de dados complexas como árvores e listas encadeadas.

## Exemplo

```typescript
type Category = {
    name: string;
    subcategories?: Category[];
};

const category: Category = {
    name: 'Electronics',
    subcategories: [
        {
            name: 'Computers',
            subcategories: [
                { name: 'Laptops' },
                { name: 'Desktops' }
            ]
        },
        {
            name: 'Phones'
        }
    ]
};
```

## Conclusão

Os tipos avançados em TypeScript, como Mapped Types, Conditional Types, Literal Types, Template Literal Types e Recursive Types, oferecem grande flexibilidade e poder na definição de tipos complexos e dinâmicos. Esses conceitos são fundamentais para tirar o máximo proveito do TypeScript e escrever código robusto e seguro.


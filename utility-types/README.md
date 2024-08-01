
# Utility Types em TypeScript

Este README fornece uma visão geral dos Utility Types em TypeScript, explicando cada um deles com exemplos práticos. Utility Types são tipos genéricos fornecidos por TypeScript que ajudam a transformar tipos já existentes.

## Índice
- [Partial](#partial)
- [Pick](#pick)
- [Omit](#omit)
- [Readonly](#readonly)
- [Record](#record)
- [Exclude](#exclude)
- [Extract](#extract)
- [NonNullable](#nonnullable)
- [Parameters](#parameters)
- [ReturnType](#returntype)
- [InstanceType](#instancetype)
- [Awaited](#awaited)

## Partial

O Utility Type `Partial` transforma todas as propriedades de um tipo em opcionais.

```typescript
interface User {
    name: string;
    age: number;
}

const updateUser = (user: Partial<User>) => {
    // Implementação...
};

updateUser({ name: "Alice" });
```

## Pick

O Utility Type `Pick` cria um novo tipo escolhendo um conjunto de propriedades de um tipo existente.

```typescript
interface User {
    name: string;
    age: number;
    email: string;
}

type UserNameAndEmail = Pick<User, 'name' | 'email'>;

const user: UserNameAndEmail = {
    name: "Alice",
    email: "alice@example.com"
};
```

## Omit

O Utility Type `Omit` cria um novo tipo excluindo um conjunto de propriedades de um tipo existente.

```typescript
interface User {
    name: string;
    age: number;
    email: string;
}

type UserWithoutEmail = Omit<User, 'email'>;

const user: UserWithoutEmail = {
    name: "Alice",
    age: 25
};
```

## Readonly

O Utility Type `Readonly` transforma todas as propriedades de um tipo em somente leitura (readonly).

```typescript
interface User {
    name: string;
    age: number;
}

const user: Readonly<User> = {
    name: "Alice",
    age: 25
};

// user.age = 26; // Erro: não é possível atribuir a 'age' porque é uma propriedade de somente leitura.
```

## Record

O Utility Type `Record` cria um tipo de objeto cujas propriedades são chaves do tipo `K` e os valores são do tipo `T`.

```typescript
type Roles = 'admin' | 'user' | 'guest';

type Permissions = Record<Roles, string[]>;

const rolePermissions: Permissions = {
    admin: ["create", "read", "update", "delete"],
    user: ["read"],
    guest: ["read"]
};
```

## Exclude

O Utility Type `Exclude` cria um tipo excluindo de `T` todos os membros que são atribuíveis a `U`.

```typescript
type T = string | number | boolean;
type U = Exclude<T, boolean>; // string | number
```

## Extract

O Utility Type `Extract` cria um tipo extraindo de `T` todos os membros que são atribuíveis a `U`.

```typescript
type T = string | number | boolean;
type U = Extract<T, string | number>; // string | number
```

## NonNullable

O Utility Type `NonNullable` cria um tipo excluindo `null` e `undefined` de um tipo.

```typescript
type T = string | number | null | undefined;
type U = NonNullable<T>; // string | number
```

## Parameters

O Utility Type `Parameters` cria um tupla do tipo dos parâmetros de uma função.

```typescript
function userInfo(name: string, age: number) {
    // Implementação...
}

type UserInfoParams = Parameters<typeof userInfo>; // [string, number]
```

## ReturnType

O Utility Type `ReturnType` cria um tipo baseado no tipo de retorno de uma função.

```typescript
function userInfo(name: string, age: number) {
    return { name, age };
}

type UserInfo = ReturnType<typeof userInfo>; // { name: string, age: number }
```

## InstanceType

O Utility Type `InstanceType` cria um tipo baseado no tipo de instância de uma classe ou função construtora.

```typescript
class User {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

type UserInstance = InstanceType<typeof User>; // User
```

## Awaited

O Utility Type `Awaited` cria um tipo baseado no tipo de retorno de uma Promise ou de uma função async.

```typescript
async function fetchData() {
    return "data";
}

type Data = Awaited<ReturnType<typeof fetchData>>; // string
```

Este README abrange os principais Utility Types em TypeScript, proporcionando uma compreensão fundamental de como cada um pode ser utilizado para transformar tipos de maneira eficaz e segura.

## Что такое TypeScript и чем он отличается от JavaScript?

TypeScript — это надмножество JavaScript, которое компилируется в обычный JavaScript.

TypeScript — это объектно-ориентированный и статически типизированный язык

В отличие от JavaScript, код TypeScript не понятен браузерам и не может быть выполнен непосредственно в браузере или на любой другой платформе. Файлы .ts необходимо сначала транспилировать с помощью tsc транспилятора TypeScript в обычный JavaScript, который затем запускается целевой платформой.

## Перечислите встроенные типы в TypeScript.

- number - числовой тип переменной;

- string - тип переменной, представляющей строку текста;

- boolean - логический тип переменной, принимающий значения true или false;

- array - тип переменной, представляющей массив значений. Может быть записан как тип[] или Array<тип>;

- tuple - тип переменной, представляющей кортеж (упорядоченный набор элементов разных типов);

- enum - тип-перечисление, позволяющий определять набор именованных значений;

- any - тип переменной, который может принимать значения любого типа;

- void - тип, используемый для объявления функций, которые не возвращают значения;

- null и undefined - типы переменных, которые могут принимать значения null или undefined;

## Что такое интерфейс в TypeScript?

В TypeScript интерфейс представляет собой описание структуры объекта. Он определяет, какие свойства и методы должны присутствовать в объекте, а также их типы.

## Чем различаются ключевые слова interface и type в TypeScript?

Основные различия между interface и type в TypeScript:

1. **Расширение:** Интерфейсы могут быть расширены другими интерфейсами, в то время как типы могут быть объединены с помощью оператора &.

2. **Реализация:** Интерфейсы могут быть реализованы классами, в то время как типы не могут быть непосредственно реализованы.

3. **Объединение типов:** Типы могут быть объединены с помощью оператора |, что позволяет создавать объединение типов.

4. **Возможности:** Интерфейсы обладают некоторыми дополнительны


## Различия void и never

void используется всякий раз, когда функция ничего не возвращает явно(например может возвращать undefined), тогда как never используется всякий раз, когда функция **никогда не** возвращает значение.


## Unknow 

unknown — это особый тип, похожий на any. Например any, распространенный вариант использования этого unknown типа — это когда вы заранее не знаете точный тип. unknown переменные принимают любое значение. Однако при попытке оперировать переменной unknown TypeScript требует проверки типа или утверждения типа.

```typescript
invokeCallback(callback: any): void {
  callback();
}
```

```typescript
invokeCallback(callback: unknown): void {
  if (typeof callback === 'function') {
    callback();
  }
}
```
## Utility Types

1. **Awaited** - это специальный тип, который может быть использован для обозначения типа, который будет возвращен из асинхронной функции.

```typescript
async function getData(): Promise<string> {
    return 'hello';
}

let awaitedData: Awaited<ReturnType<typeof getData>>;
// теперь awaitedData может быть 'hello'
```

2. **Partial** - делает все свойства объекта типа T необязательными.

```typescript
interface Person {
  name?: string;
  age?: number;
}

let requiredPerson: Required<Person>;
// теперь requiredPerson может быть { name: string; age: number; }
```

3. **Readonly** - делает все свойства объекта типа T доступными только для чтения.
4. **Record** - Record<Keys, Type> - создает тип, который является записью с ключами, определенными в первом параметре, и значениями типа, определенного во втором параметре.

```typescript
type Keys = 'a' | 'b' | 'c';
type RecordType = Record<Keys, number>;

let record: RecordType;
// теперь record может быть { a: number, b: number, c: number }
```

5. **Pick** - Pick<T, K extends keyof T> - выбирает свойства объекта типа T с ключами, указанными в K.
```typescript
interface Person {
  name: string;
  age: number;
}

let pickedPerson: Pick<Person, 'name'>;
// теперь pickedPerson может быть { name: string; }
```

6. **Omit** - Omit<T, K extends keyof T> - выбирает свойства объекта типа T, исключая те, которые указаны в K.

```typescript
interface Person {
  name: string;
  age: number;
}

let omittedPerson: Omit<Person, 'age'>;
// теперь omittedPerson может быть { name: string; }
```

7. **Exclude** - Exclude<UnionType, ExcludedMembers> - исключает определенные типы из объединенного типа.

```typescript
type A = 'a' | 'b' | 'c';
type B = Exclude<A, 'a' | 'b'>;
// теперь B это 'c'
```

8. **Extract** - Extract<Type, Union> - извлекает из типа Type только те типы, которые присутствуют в Union.

```typescript
type A = 'a' | 'b' | 'c';
type B = 'a' | 'b';
type C = Extract<A, B>;
// теперь C это 'a' | 'b'
```

9. **NonNullable** - NonNullable<Type> - извлекает тип из Type, исключая null и undefined.

```typescript
let value: string | null | undefined;
let nonNullableValue: NonNullable<typeof value>;
// теперь nonNullableValue это string
```

10. **Parameters** - Parameters<Type> - извлекает типы аргументов функции Type.

```typescript
function foo(a: string, b: number) {}
type FooParameters = Parameters<typeof foo>;
// теперь FooParameters это [string, number]
```

11. **ReturnType** - ReturnType<Type> - извлекает тип возвращаемого значения функции Type.

```typescript
function foo(): string { return 'hello'; }
type FooReturnType = ReturnType<typeof foo>;
// теперь FooReturnType это string
```

## Generics 

Дженерики в TypeScript – это мощный инструмент, позволяющий создавать компоненты, способные работать с различными типами ‍данных. Использование генериков помогает обеспечить типобезопасность во время компиляции, а также повысить переиспользуемость кода. Например, вы можете определить функцию  identity, которая будет возвращать значение любого типа, переданного в неё:
```typescript
function identity(arg: T): T {
    return arg;
}
```

В этом примере – это генерик-параметр, который затем используется для типизации аргумента и‌ возвращаемого значения функции. Таким образом, функция identity может работать с числами, строками и другими типами, сохраняя при этом‌ их конкретный тип.

## Enums

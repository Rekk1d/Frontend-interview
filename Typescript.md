## Что такое TypeScript и чем он отличается от JavaScript?

TypeScript — это надмножество JavaScript, которое компилируется в обычный JavaScript.

JavaScript - это язык со слабой и динамической типизацией

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

- bigInt

- symbol

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

Также можно ограничить дженерик с помощью наследования(extends)

```typescript
interface Lengthwise {
  length: number;
}
 
function loggingIdentity<Type extends Lengthwise>(arg: Type): Type {
  console.log(arg.length); // Now we know it has a .length property, so no more error
  return arg;
}
```

## Enums

Перечисления или перечисляемые типы — это средство определения набора именованных констант. Эти структуры данных имеют постоянную длину и содержат набор постоянных значений. Перечисления в TypeScript обычно используются для представления набора параметров для заданного значения с использованием набора пар ключ/значение.


```typescript
enum UserType {
  Guest = "G",
  Verified = "V",
  Admin = "A",
}

const userType: UserType = UserType.Verified;
```

Под капотом TypeScript после компиляции переводит перечисления в простые объекты JavaScript. Это делает использование перечислений более выгодным по сравнению с использованием нескольких независимых const переменных. Группировка, которую предлагают перечисления, делает ваш код типобезопасным и более читабельным.

## Какие модификаторы доступа поддерживает TypeScript?

**public** : все свойства и методы по умолчанию общедоступны. Публичные члены класса видны и доступны из любого места.

**protected** : защищенные свойства доступны из того же класса и его подкласса. Например, переменная или метод с protected ключевым словом будут доступны из любого места в своем классе и в другом классе, который расширяет класс, содержащий переменную или метод.

**private** : частные свойства доступны только из класса, в котором определено свойство или метод.

## В чем разница между типами объединения(union) и пересечения(intersection)?

Объединения и типы пересечения позволяют составлять и комбинировать существующие типы, а не создавать их с нуля. И объединение, и пересечение имеют свои уникальные характеристики, которые делают их идеальными для различных вариантов использования.

Тип объединения описывается как тип, который может быть одним из нескольких типов. Тип объединения использует | символ (вертикальная черта) для разделения списка типов, которые будут использоваться в новом типе. Давайте рассмотрим пример:

```typescript
interface B {
  name: string,
  email: string
}

interface C {
  name: string,
  age: number
}

type A = B | C;
```

A в приведенном выше фрагменте может быть либо типа, B либо C.

С другой стороны, пересечение описывается как тип, который объединяет несколько типов в один, объединяя все свойства каждого типа для создания нового типа. Пересечение использует & символ для разделения списка типов, которые будут объединены. Давайте посмотрим на пример:

```typescript
interface B {
  name: string,
  email: string
}

interface C {
  name: string,
  age: number
}

type A = B & C;
```

A в приведенном выше фрагменте будут содержать все свойства обоих B и C ( name, email, и age).

##  В чем разница между extends и implements в TypeScript?

Когда класс расширяет другой класс, дочерний класс наследует все свойства и методы класса, который он расширяет. Вы можете переопределить любое из существующих свойств и методов его родителя и добавить новые.

Когда класс реализует другой класс или интерфейс, класс должен реализовать все методы и свойства реализованного класса или интерфейса. Ключевое implements слово действует как контракт, которому должен следовать класс, и TypeScript позаботится о том, чтобы класс имел ту же форму, что и класс или интерфейс, который он реализует.

```typescript
class User {
  name: string;
  age: number;
}

// John will contain name and age from the User class
class John extends User {}

// this will result in an error as Bob doesn't have all the properties that
// the User class has
class Bob implements User {}

// This is valid as Mike satisfies the "contract" specified by the 
// User class
class Mike implements User {
  name = 'Mike';
  age = 25
}
```

## Что такое утверждения типа в TypeScript?

Утверждение типа позволяет вам явно установить тип значения и сообщить компилятору, чтобы он не выводил его. Это полезно, когда вы знаете тип объекта более конкретно, чем его текущий тип или текущий предполагаемый тип. В таких случаях вы можете использовать утверждения типа, чтобы указать TypeScript текущий тип переменной.

TypeScript предоставляет два синтаксиса для утверждений типа — as и <>.

```typescript
// using the `as` keyword
const name: string = person.name as string;

// using `<>`
const name: string = <string>person.name;
```

## typeof

Оператор typeof в TypeScript используется для получения типа переменной или выражения.

Примеры использования:

1. Получение типа переменной

```typescript
const myString = "Hello, TypeScript!";
type MyStringType = typeof myString; // MyStringType будет равен string
```
2. Типизация функций

```typescript
const myFunction = (x: number) => x * 2;

type MyFunctionType = typeof myFunction; // MyFunctionType будет равен (x: number) => number
```

3. Создание типов на основе объектов

```typescript
const user = {
    name: "Alice",
    age: 30,
};

type UserType = typeof user; // UserType будет равен { name: string; age: number; }
```

4. Использование с интерфейсами и классами

```typescript
class Person {
    constructor(public name: string, public age: number) {}
}

type PersonType = typeof Person; // PersonType будет равен typeof Person (конструктор класса)
```

## keyof

keyof — это оператор типа, который принимает тип объекта и возвращает тип, представляющий все имена его ключей. Результатом работы keyof является объединение строк или чисел, которое содержит литералы всех возможных ключей объекта.

```typescript
interface User {
  id: number;
  name: string;
  age: number;
}

type UserKeys = keyof User;
// UserKeys теперь равно 'id' | 'name' | 'age'
```

Оператор keyof может быть очень полезен при написании обобщенных функций, которые работают с объектами. Он гарантирует, что функции работают только с существующими ключами объекта.

```typescript
function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user: User = {
  id: 1,
  name: "Alice",
  age: 30
};

const userName = getValue(user, 'name'); // Возвращает 'Alice'
const userAge = getValue(user, 'age'); // Возвращает 30
// const userUnknown = getValue(user, 'email'); // Ошибка: Аргумент типа '"email"' не может быть присвоен параметру типа '"id" | "name" | "age"'
```

## infer

infer в TypeScript — это ключевое слово, которое используется в условных типах для автоматического вывода типа. Оно позволяет TypeScript "угадывать" тип переменной на основе контекста, в котором она используется. Это особенно полезно, когда вы хотите создать обобщенные типы или функции, которые могут работать с различными типами данных.

infer используется только в conditional types и в расширениях(extends).

Предположим, у нас есть функция, которая принимает массив и возвращает его первый элемент. Мы можем использовать infer, чтобы автоматически вывести тип элемента массива:

```typescript
type FirstElement<T> = T extends (infer U)[] ? U : never;

type NumberArray = FirstElement<number[]>; // NumberArray будет равен number
type StringArray = FirstElement<string[]>; // StringArray будет равен string
```


## Сужение типов(Narrowing)

Это процесс, при котором TypeScript сужает широкий тип (например, string | number) до более конкретного типа (string или number) в зависимости от контекста выполнения программы

Пример без сужения типов:

```typescript
function printLength(value: string | number) {
  console.log(value.length); // Ошибка: Property 'length' does not exist on type 'string | number'
}

printLength("Hello");
printLength(123);
```

Основные методы сужения типов:
1. typeof 

```typescript
function logValue(value: string | number) {
    if (typeof value === "string") {
        console.log(`String: ${value.toUpperCase()}`);
    } else {
        console.log(`Number: ${value.toFixed(2)}`);
    }
}
```

2. instanceof
```typescript
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof!");
  }
}

function makeSound(animal: Animal) {
  if (animal instanceof Dog) {
    animal.bark();
  } else {
    animal.speak();
  }
}
```

3. User-Defined Type Guards (Пользовательские защитники типов):

```typescript
interface Bird {
  fly(): void;
}

interface Fish {
  swim(): void;
}

function isFish(animal: Fish | Bird): animal is Fish {
  return (animal as Fish).swim !== undefined;
}

function move(animal: Fish | Bird) {
  if (isFish(animal)) {
    animal.swim();
  } else {
    animal.fly();
  }
}
```

4. in 

```typescript
function makeSound(animal: Cat | Dog) {
  if ("meow" in animal) {
    // Здесь TypeScript понимает, что `animal` — это `Cat`
    animal.meow();
  } else {
    // Здесь `animal` — это `Dog`
    animal.bark();
  }
}

const myCat: Cat = { meow: () => console.log("Meow"), name: "Whiskers" };
const myDog: Dog = { bark: () => console.log("Woof"), name: "Buddy" };

makeSound(myCat); // "Meow"
makeSound(myDog); // "Woof"
```


## Преобразование типов

satisfies - проверяет соответсвие объекта типу, но не преобразовывает объект к конкретному типу/интерфесу как это делать as(as Person)

```typescript

interface Peson {
    name: string;
    age: number;
}

const person = {
    name: 'Test',
    age: 50
} satisfies Person;
```

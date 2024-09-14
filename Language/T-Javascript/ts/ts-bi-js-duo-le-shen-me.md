# TS比JS多了什么？

TypeScript (TS) 是 JavaScript (JS) 的超集，它在 JavaScript 的基础上增加了许多新的特性和功能，主要是为了提升代码的**可维护性、开发效率以及代码的健壮性**。以下是 TypeScript 比 JavaScript 多出的主要内容：

## 1. **静态类型系统**

TypeScript 的核心特性是它的 **静态类型系统**，可以在编译时检查代码中的类型错误。JavaScript 是动态类型语言，变量的类型只有在运行时才能确定，而 TypeScript 可以在开发过程中捕获类型错误。

*   **类型注解**：在 TypeScript 中，开发者可以为变量、函数参数和返回值显式地声明类型。

    ```typescript
    let age: number = 30;
    let name: string = 'John';
    ```
*   **类型推断**：即使没有显式声明，TypeScript 也可以通过上下文推断出变量的类型。

    ```typescript
    let count = 5; // TS 自动推断为 number 类型
    ```
* **类型检查**：在编译时，如果类型不匹配，TypeScript 会报错，帮助开发者避免潜在的运行时错误。

## 2. **接口 (Interfaces)**

TypeScript 引入了 **接口**（`interface`），用于定义对象的结构，确保对象符合特定的类型形状。这对于大规模项目非常有用，可以定义清晰的数据结构和接口契约。

```typescript
interface Person {
  name: string;
  age: number;
}

let user: Person = { name: "Alice", age: 25 };
```

## 3. **类型别名 (Type Aliases)**

TypeScript 支持使用 **类型别名** 来为复杂类型创建快捷方式，简化代码。

```typescript
type StringOrNumber = string | number;

let value: StringOrNumber;
value = "Hello";
value = 42;
```

## 4. **枚举 (Enums)**

TypeScript 提供了 **枚举** 类型，用于定义一组命名常量，便于表示一组相关值。

```typescript
enum Color {
  Red,
  Green,
  Blue
}

let color: Color = Color.Green;
```

## 5. **泛型 (Generics)**

**泛型** 提供了在编写类、函数或接口时使用不指定具体类型的方式，从而实现类型的复用性和灵活性。

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>("myString");  // T 为 string
```

## 6. **高级类型**

TypeScript 支持许多 **高级类型**，使得开发者可以构建复杂的类型系统。

*   **联合类型**（Union Types）：允许一个变量或参数接受多个类型。

    ```typescript
    let id: number | string;
    id = 10;
    id = "A123";
    ```
*   **交叉类型**（Intersection Types）：将多个类型合并为一个类型。

    ```typescript
    interface A { propA: string; }
    interface B { propB: number; }

    let obj: A & B = { propA: "Hello", propB: 42 };
    ```
*   **类型守卫**（Type Guards）：通过条件判断来缩小类型范围，保证在特定代码块中的类型是安全的。

    ```typescript
    function isString(x: any): x is string {
      return typeof x === "string";
    }
    ```

## 7. **静态分析和编译时错误**

TypeScript 的编译器能够在开发阶段通过静态类型检查发现潜在的错误，而不必等到运行时才会抛出错误。JavaScript 则无法在编译时发现这些错误。

```typescript
let num: number = "Hello";  // 编译时会报错
```

## 8. **模块系统和命名空间**

TypeScript 提供了 **模块系统**，可以使用 `import` 和 `export` 来组织代码，并支持 ES6 的模块系统。而在 JavaScript 中，模块化只能通过外部库（如 CommonJS、AMD）或 Node.js 的模块系统来实现。

```typescript
// math.ts
export function add(x: number, y: number): number {
  return x + y;
}

// main.ts
import { add } from './math';
console.log(add(2, 3));
```

## 9. **类型声明文件 (Declaration Files)**

TypeScript 可以与 JavaScript 库无缝协作，通过类型声明文件 (`*.d.ts`)，为没有原生 TypeScript 支持的 JavaScript 库提供类型定义。

*   例如，使用 `@types` 来为第三方库提供类型信息：

    ```bash
    npm install @types/jquery --save-dev
    ```



## 10. **类和面向对象编程增强**

虽然 JavaScript ES6 开始引入类，但 TypeScript 增强了对 **类** 和 **面向对象编程** 的支持，包括：

*   **访问修饰符**：`public`、`private` 和 `protected` 控制类成员的访问权限。

    ```typescript
    class Person {
      private name: string;

      constructor(name: string) {
        this.name = name;
      }

      public getName(): string {
        return this.name;
      }
    }
    ```
*   **抽象类**：允许定义不完全实现的类，用于继承。

    ```typescript
    abstract class Animal {
      abstract makeSound(): void;
    }

    class Dog extends Animal {
      makeSound() {
        console.log("Woof!");
      }
    }
    ```
* **继承**：TypeScript 允许类进行继承，支持面向对象的特性。

## 11. **严格模式**

TypeScript 提供了更多 **严格类型检查** 的选项，比如 `strictNullChecks`、`noImplicitAny` 等，帮助开发者在编写代码时更加严格地检查潜在问题。

*   **strictNullChecks**：在启用时，`null` 和 `undefined` 需要显式处理。

    ```typescript
    let value: string | null = null;
    value = "Hello";  // 必须明确处理 null 类型
    ```

## 12. **工具支持与开发体验**

TypeScript 的类型系统让 IDE（如 VS Code）能够提供更好的代码补全、错误提示和重构工具，从而提高开发效率。这在 JavaScript 中是有限的，除非使用了动态分析工具。

#### 总结

TypeScript 相对于 JavaScript 增加了**静态类型、接口、泛型、枚举、类型声明文件、模块系统**等一系列功能，使得代码更安全、健壮、可维护，并且极大提升了大型项目的开发效率。TypeScript 是一个构建在 JavaScript 之上的工具，能够与现有 JavaScript 代码和库兼容，同时为开发者提供更多功能和类型检查。





## 小结

基于js在ES6之后提供一些让使用起来更加面向对象化的编写方式。


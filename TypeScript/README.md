#### 实现一个 TypeScript 类型工具 DeepReadonly<T>，将一个嵌套对象类型的所有属性及其子属性设为只读。

```typescript
type User = {
  id: number;
  name: string;
  settings: {
    theme: string;
    notifications: boolean;
  };
};
```

```typescript
type DeepReadonly<T> = {
  readonly [k in keyof T]: T[k] extends object
    ? T[k] extends Function
      ? T[k]
      : DeepReadonly<T[k]>
    : T[k];
};
```

#### 请完成题目的要求

```typescript
题目要求：
console.log(add(1, 2));      // ✅ 不报错
console.log(add('1', '2'));  // ✅ 不报错
console.log(add(1, '2'));    // ❌ 报错（类型不匹配）

interface AddFn<T> {
  (a: T, b: T): void;
}

const add: AddFn<number> & AddFn<string> = (a: any, b: any) => {
};
```

#### 请说一下 any 和 unknown 的区别

any 可以表示任意的数据类型，可以绕过类型检查，不安全；unknown 表示未知的数据类型，使用之前需要做类型断言，比 any 更安全。

#### 请谈一下 ts 中的 type 和 interface 的区别

1、interface 主要用于定义对象的结构（属性、方法），也可以用来定义函数类型；type 可以定义任何类型：对象、联合类型、交叉类型、元组、基本类型别名等，功能更广。
2、interface：用 extends 继承，可以多继承；type：用交叉类型 & 组合。
3、interface 支持声明合并（多次声明会自动合并）。type 不能重复定义同名类型（会报错）。

```typescript
interface User {
  name: string;
}
interface User {
  age: number;
}
// 合并成 { name: string; age: number }

type User2 = { name: string };
// type User2 = { age: number } // ❌ 会报错
```

#### Ts如何在众多类型中排除undefined和null类型？

1、使用 NonNullable 工具类型
```typescript
// 原始类型：包含 string、number、null、undefined
type OriginalType = string | number | null | undefined;

// 排除 null/undefined
type NonNullType = NonNullable<OriginalType>; 
// 结果：string | number

// 实际变量使用
const value: NonNullType = "hello"; // ✅ 合法
// const value2: NonNullType = null; // ❌ 报错：不能将类型“null”分配给类型“string | number”
```

2、使用类型排除（Exclude 工具类型）
```typescript
type OriginalType = string | boolean | null | undefined;

// 1. 同时排除 null 和 undefined
type ExcludeNullUndefined = Exclude<OriginalType, null | undefined>;
// 结果：string | boolean
```

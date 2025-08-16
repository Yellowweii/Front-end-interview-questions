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

#### 实现一个 TypeScript 类型工具 DeepReadonly<T>，将一个嵌套对象类型的所有属性及其子属性设为只读。
Example
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
  readonly [k in keyof T]: T[k] extends object ? T[k] extends Function ? T[k] : DeepReadonly<T[k]> : T[k]
}
```


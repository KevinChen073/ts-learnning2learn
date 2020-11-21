## 常见问题
1. Class中的Props和State如何定义
`React.Component<Props,State>`

2. React实例类型
`React.ReactElement<T>`

3. Class
```typescript
class k {
  _privateParam: string;
  a() {
    return this._privateParam;
  }
}
```

## 常见错误
思考 - 从Class到泛型的思考
1. 使用React的Class类型，对应的联想到了HTMLElement等类型。类似于Component<Props,State> 这种类型是如何实现的。
利用泛型这种‘可自定义’的类型。例如RaxElement最简单的写法就是这样的，定义了泛型P和泛型T作为对象中的props和type的类型
```typescript
  interface RaxElement<
    P = any,
    T extends string | JSXElementConstructor<any> = string | JSXElementConstructor<any>
  > {
    type: T;
    props: P;
    key: Key | null;
  }
```
又例如我们用得最多的Rax.Component的写法，按照React的定义把Props、State和Compoent中的生命周期关联在了一起。
```typescript
interface Component<P = {}, S = {}, SS = any> extends ComponentLifecycle<P, S, SS> {}
interface ComponentLifecycle<P, S, SS = any> {
    componentDidMount?(): void;
    shouldComponentUpdate?(
      nextProps: Readonly<P>,
      nextState: Readonly<S>,
      nextContext: any
    ): boolean;
    componentWillUnmount?(): void;
    componentDidCatch?(error: Error, errorInfo: ErrorInfo): void;
    getSnapshotBeforeUpdate?(prevProps: Readonly<P>, prevState: Readonly<S>): SS | null;
    componentDidUpdate?(prevProps: Readonly<P>, prevState: Readonly<S>, snapshot?: SS): void;
    componentWillMount?(): void;
    componentWillReceiveProps?(nextProps: Readonly<P>, nextContext: any): void;
    componentWillUpdate?(nextProps: Readonly<P>, nextState: Readonly<S>, nextContext: any): void;
  }
 ```
2. 泛型这个机制是为了解决什么问题？
可以理解为一个抽象类型，处理一些无法枚举或者约束的外部传入类型，但是内部成员又需要对其有一致性的消费约束。
设计泛型的关键目的是在成员之间提供有意义的约束，这些成员可以是：
• 类的实例成员
• 类的方法
• 函数参数
• 函数返回值
3. 泛型还可以扩展开来干什么呢
一般应用在：
• 数组、对象等类型处理
• React Compoent
• HTMLElement等

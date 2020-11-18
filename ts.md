TS常用小技巧：https://juejin.im/post/6844904055039344654#heading-58
### 11.17
• 声明对象，不要直接用object，需要用 Record<String, any> ，参考文档:https://www.leevii.com/2018/10/record-in-typescript.html
• typeof 操作符可以用来获取一个变量或对象的类型
import AObj from './a'
const a: typeof AObj; // 这样就可以把对象类型赋给变量拉
• Record类型的用法：https://blog.csdn.net/weixin_38080573/article/details/92838045
• type - 类型声明
• interface-对象声明
• function - 函数声明的的ts定义
// 非匿名函数声明
function sum(x: number, y: number): number {
    return x + y;
}
// 匿名函数声明
let sum: (x: number, y: number) => number
• 如何function需要进行is类型的判断，那么要如何做
function isObject(value: unknown): value is Record<string, any> {
  return isType(value, '[object Object]');
}
const a = 'a' as string | Object;
if (isObject(a)) {
  a // a只能是Record<string, any>了
}
### 11.15
函数声明文件，index.d.ts。理论上对ts而言，我们是需要写TS的。但是对老项目而言，如果是js编写的，那么声明文件可以用*.d.ts来声明
理论上在tsconfig.json中，会对 "include" 中的内容都进行查找。
• declare和interface的差别
### 11.01
• 函数类型的声明  (arg1: string, arg2: string) => void

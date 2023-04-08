## exceptionhandling 异常处理

English translation: [README_en.md](README_en.md)

## 描述

这是一个用于统一为所有的异步函数添加 try-catch 异常捕获，并在 class 中使用体验更佳的工具库。

### 安装

使用 npm 安装：

```bash
npm install exceptionhandling --save
```

### 使用

**asyncTryCatch**

使用 try-catch 包装一个异步函数，可以捕获异常并输出错误日志

```javascript
/**
 * @param func 待包装的异步函数
 * @returns 新的异步函数，具有相同的参数和返回值类型，但会在发生异常时返回 undefined
 */
export function asyncTryCatch<T = any>(
    func: (...args: any[]) => Promise<T>
): (...args: any[]) => Promise<T | undefined>
```

**classAsyncTryCatch**

在类中使用 try-catch 包装所有的异步方法，可以捕获异常并输出错误日志

```javascript
/**
 * @param target 待包装的类
 * @returns 新的类，具有相同的参数和返回值类型，但会在发生异常时返回 undefined
 */
export function classAsyncTryCatch<T extends new(...args: any[]) => object>(target: T): T
```

### 代码示例

```javascript
import { asyncTryCatch, classAsyncTryCatch } from "exceptionhandling";

// 异步函数
async function testAsyncFunction() {
	throw new Error("test error");
}

// 异步函数包装
const wrappedFunction = asyncTryCatch(testAsyncFunction);
await wrappedFunction(); // 发生异常，返回 undefined 并输出错误日志

// 类方法
@classAsyncTryCatch
class TestClass {
	async testMethod() {
		throw new Error("test error");
	}
}
const testClass = new TestClass();
await testClass.testMethod(); // 发生异常，返回 undefined 并输出错误日志
```

### 注意事项

使用"@"装饰器时，需要在 tsconfig.json 的 compilerOptions 中配置"experimentalDecorators": true
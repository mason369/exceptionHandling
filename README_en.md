
## exceptionhandling Exception Handling

### Description

This is a tool library for unifying try-catch exception handling for all asynchronous functions and improving the experience of using it in classes.

### Installation

Use npm to install:

```bash
npm install exceptionhandling --save
```

### Usage

**asyncTryCatch**

Wrap an asynchronous function with try-catch to catch exceptions and output error logs.

```javascript
/**
 * @param func The asynchronous function to be wrapped
 * @returns A new asynchronous function that has the same parameter and return value types, but returns undefined when an exception occurs
 */
export function asyncTryCatch<T = any>(
    func: (...args: any[]) => Promise<T>
): (...args: any[]) => Promise<T | undefined>
```

**classAsyncTryCatch**

Wrap all asynchronous methods with try-catch in a class to catch exceptions and output error logs.

```javascript
/**
 * @param target The class to be wrapped
 * @returns A new class that has the same parameter and return value types, but returns undefined when an exception occurs
 */
export function classAsyncTryCatch<T extends new(...args: any[]) => object>(target: T): T
```

### Code Example

```javascript
import { asyncTryCatch, classAsyncTryCatch } from "exceptionhandling";

// Asynchronous function
async function testAsyncFunction() {
	throw new Error("test error");
}

// Wrap asynchronous function
const wrappedFunction = asyncTryCatch(testAsyncFunction);
await wrappedFunction(); // When an exception occurs, returns undefined and outputs the error log.

// Class method
@classAsyncTryCatch
class TestClass {
	async testMethod() {
		throw new Error("test error");
	}
}
const testClass = new TestClass();
await testClass.testMethod(); // When an exception occurs, returns undefined and outputs the error log.
```

### Note

When using "@" decorator, you need to set "experimentalDecorators": true in tsconfig.json's compilerOptions.

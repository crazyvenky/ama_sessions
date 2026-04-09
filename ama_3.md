# 📘 AMA 3 - Quick JS Q&A

## 1. What is callback?

Function passed into another function to be executed later.

``` javascript
function greet(cb){ cb(); }
greet(() => console.log("Hi"));
```

------------------------------------------------------------------------

## 2. Methods of console

-   console.log()
-   console.error()
-   console.warn()
-   console.table()
-   console.time()

------------------------------------------------------------------------

## 3. setTimeout & setInterval

-   setTimeout → runs once after delay\
-   setInterval → runs repeatedly

``` javascript
setTimeout(() => console.log("Hi"), 1000);
setInterval(() => console.log("Repeat"), 1000);
```

------------------------------------------------------------------------

## 4. Event loop in JS

Handles async execution: call stack + queue + event loop.

------------------------------------------------------------------------

## 5. ES6

Modern JS version (2015) with features like let/const, arrow functions,
classes, promises.

------------------------------------------------------------------------

## 6. Why we use JS to develop?

-   Runs in browser\
-   Handles interactivity\
-   Fast and widely supported

------------------------------------------------------------------------

## 7. Difference between == and ===

-   == → compares value (type coercion)\
-   === → compares value + type

------------------------------------------------------------------------

## 8. flat method

Flattens nested arrays.

``` javascript
[1, [2, [3]]].flat(2); // [1,2,3]
```

------------------------------------------------------------------------

## 9. Spread operator

Expands elements.

``` javascript
const arr = [1,2];
const newArr = [...arr, 3];
```

------------------------------------------------------------------------

## 10. Freeze in JS

`Object.freeze()` makes object immutable.

------------------------------------------------------------------------

## 11. return undefined and null

-   undefined → default absence\
-   null → intentional absence

------------------------------------------------------------------------

## 12. Promise

Handles async operations (pending, fulfilled, rejected).

``` javascript
new Promise((res, rej) => res("done")).then(console.log);
```

------------------------------------------------------------------------

## 13. Question on spread operator

Used to copy/merge arrays & objects without mutation.

------------------------------------------------------------------------

## 14. Error handling

Use try...catch to handle errors.

``` javascript
try {
  throw new Error("Oops");
} catch(e) {
  console.log(e.message);
}
```

------------------------------------------------------------------------

## 15. Types of variables

-   var → function scoped\
-   let → block scoped\
-   const → block scoped (no reassignment)

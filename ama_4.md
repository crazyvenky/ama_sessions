# 📘 AMA 4 - Quick Web Dev Q&A

## 1. What are HTTP status codes?

3-digit codes indicating request result.\
- **2xx** → Success (200 OK)\
- **3xx** → Redirection\
- **4xx** → Client error (404 Not Found)\
- **5xx** → Server error (500 Internal Server Error)

------------------------------------------------------------------------

## 2. How do you create a new element in DOM?

Use `document.createElement()`.

``` javascript
const div = document.createElement("div");
div.textContent = "Hello";
document.body.appendChild(div);
```

------------------------------------------------------------------------

## 3. What does POST method do?

Sends data to server to **create a resource**.\
- Data in body\
- Not cached\
- Not idempotent

------------------------------------------------------------------------

## 4. How does the event loop work?

-   Runs sync code in call stack\
-   Async tasks go to queue\
-   Executes them when stack is empty

------------------------------------------------------------------------

## 5. Different HTTP methods

-   **GET** → fetch\
-   **POST** → create\
-   **PUT** → full update\
-   **PATCH** → partial update\
-   **DELETE** → remove

------------------------------------------------------------------------

## 6. Callback vs Higher Order Function

-   **Callback** → function passed as argument\
-   **Higher-order function** → takes/returns function

``` javascript
function greet(cb) { cb(); }
greet(() => console.log("Hi"));
```

------------------------------------------------------------------------

## 7. What is 429 HTTP status?

**Too Many Requests** → rate limit exceeded.

------------------------------------------------------------------------

## 8. git status vs git log

-   **git status** → current changes\
-   **git log** → commit history

------------------------------------------------------------------------

## 9. How to access HTML elements in DOM?

-   `getElementById()`\
-   `getElementsByClassName()`\
-   `querySelector()`\
-   `querySelectorAll()`

``` javascript
document.querySelector("#id");
```

------------------------------------------------------------------------

## 10. What is AggregateError?

Holds **multiple errors** (used in `Promise.any()`).

``` javascript
Promise.any([p1, p2]).catch(e => console.log(e.errors));
```

------------------------------------------------------------------------

## 11. What are DOM nodes?

Basic DOM units (elements, text, comments).

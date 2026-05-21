# Hoisting и TDZ в JavaScript

---

## Содержание

- [Что такое Hoisting](#что-такое-hoisting)
- [Hoisting переменных](#hoisting-переменных)
- [Hoisting функций](#hoisting-функций)
- [TDZ — Temporal Dead Zone](#tdz--temporal-dead-zone)
- [Итоговое сравнение](#итоговое-сравнение)
- [Частые ошибки](#частые-ошибки)
- [Задания](#задания)

---

## Что такое Hoisting

Hoisting (поднятие) — это когда JavaScript перед запуском кода поднимает объявления переменных и функций наверх своей области видимости.

Это происходит автоматически — ты ничего не делаешь, движок JS делает это сам.

Простой пример:

```js
console.log(name); // undefined — не ошибка!
var name = "Иброхим";
```

Ты думаешь код читается сверху вниз. Но JavaScript перед запуском делает так:

```js
var name;            // поднял объявление наверх
console.log(name);   // undefined
name = "Иброхим";   // присваивание осталось на месте
```

Объявление поднялось — значение нет.

---

## Hoisting переменных

### var — поднимается, но без значения

```js
console.log(a); // undefined
var a = 5;
console.log(a); // 5
```

Что видит JavaScript:

```js
var a;          // поднялось
console.log(a); // undefined
a = 5;          // присваивание на месте
console.log(a); // 5
```

---

### let и const — поднимаются, но недоступны

```js
console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

```js
console.log(c); // ReferenceError: Cannot access 'c' before initialization
const c = 20;
```

`let` и `const` тоже поднимаются — но до строки где они объявлены, они находятся в **TDZ** и обратиться к ним нельзя.

---

### Сравнение var, let, const

```js
// var — ошибки нет, но значение undefined
console.log(x); // undefined
var x = 1;

// let — ошибка
console.log(y); // ReferenceError
let y = 2;

// const — ошибка
console.log(z); // ReferenceError
const z = 3;
```

---

## Hoisting функций

### Function Declaration — поднимается полностью

Function Declaration — это обычная функция написанная через `function`.

```js
sayHello(); // "Привет!" — работает!

function sayHello() {
  console.log("Привет!");
}
```

Почему работает? Потому что вся функция поднимается наверх:

```js
// JavaScript видит так:
function sayHello() {
  console.log("Привет!");
}

sayHello(); // "Привет!"
```

---

### Function Expression — не поднимается

Function Expression — это функция записанная в переменную.

```js
sayHi(); // TypeError: sayHi is not a function

var sayHi = function() {
  console.log("Привет!");
};
```

Что видит JavaScript:

```js
var sayHi;   // поднялось только объявление var
sayHi();     // ошибка — sayHi пока undefined, не функция
sayHi = function() {
  console.log("Привет!");
};
```

---

### Arrow Function — тоже не поднимается

```js
greet(); // TypeError: greet is not a function

var greet = () => {
  console.log("Привет!");
};
```

---

### Итог по функциям

```js
// Function Declaration — работает до объявления
hello(); // "Привет!"
function hello() {
  console.log("Привет!");
}

// Function Expression — не работает до объявления
bye(); // TypeError
var bye = function() {
  console.log("Пока!");
};

// Arrow Function — не работает до объявления
go(); // TypeError
var go = () => {
  console.log("Вперёд!");
};
```

---

## TDZ — Temporal Dead Zone

TDZ (Временная мёртвая зона) — это период от начала блока до строки где объявлена переменная `let` или `const`. В этот период переменная существует но обратиться к ней нельзя.

```js
{
  // TDZ для name начинается здесь
  console.log(name); // ReferenceError — TDZ!
  console.log(name); // ReferenceError — TDZ!
  console.log(name); // ReferenceError — TDZ!

  let name = "Иброхим"; // TDZ заканчивается здесь

  console.log(name); // "Иброхим" — теперь можно
}
```

---

### TDZ в функции

```js
function test() {
  console.log(value); // ReferenceError — TDZ
  let value = 42;
  console.log(value); // 42
}

test();
```

---

### Почему TDZ существует

TDZ защищает от ошибок. С `var` можно случайно использовать переменную до её объявления и получить `undefined` — это сложно найти.

```js
// var — тихая ошибка, получаем undefined
function bad() {
  console.log(name); // undefined — непонятно почему
  var name = "Иброхим";
}

// let — явная ошибка, сразу видно проблему
function good() {
  console.log(name); // ReferenceError — сразу понятно
  let name = "Иброхим";
}
```

С `let` и `const` ошибка сразу видна — легче найти и исправить.

---

### TDZ и typeof

С `var` — `typeof` возвращает `"undefined"` без ошибки:

```js
console.log(typeof x); // "undefined"
var x = 5;
```

С `let` — `typeof` тоже вызывает ошибку в TDZ:

```js
console.log(typeof y); // ReferenceError — TDZ!
let y = 5;
```

---

## Итоговое сравнение

| | `var` | `let` | `const` |
|---|---|---|---|
| Поднимается? | да | да | да |
| Доступна до объявления? | да (undefined) | нет (TDZ) | нет (TDZ) |
| Можно переобъявить? | да | нет | нет |
| Можно изменить значение? | да | да | нет |

| | Function Declaration | Function Expression | Arrow Function |
|---|---|---|---|
| Поднимается полностью? | да | нет | нет |
| Работает до объявления? | да | нет | нет |

---

## Частые ошибки

### Ошибка 1 — использовать var и ждать ошибку

```js
// думаешь будет ошибка — но нет
console.log(name); // undefined — не ошибка!
var name = "Иброхим";
```

Используй `let` и `const` — они сразу покажут ошибку.

---

### Ошибка 2 — вызывать Function Expression до объявления

```js
// не работает
sayHi();

var sayHi = function() {
  console.log("Привет!");
};

// работает
sayHello();

function sayHello() {
  console.log("Привет!");
}
```

---

### Ошибка 3 — var в цикле

```js
// var — одна переменная для всех итераций
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// 3, 3, 3

// let — своя переменная для каждой итерации
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// 0, 1, 2
```

---

### Ошибка 4 — забыть про TDZ в блоке

```js
let name = "Иброхим";

{
  console.log(name); // ReferenceError — TDZ!
  // думаешь возьмёт name снаружи — но нет
  // внутри блока есть своя let name, и она в TDZ
  let name = "Азим";
  console.log(name); // "Азим"
}
```

---

## Задания

**1.** Что выведет этот код? Объясни почему.

```js
console.log(a);
var a = 10;
console.log(a);
```

**2.** Что выведет этот код? Объясни почему.

```js
console.log(b);
let b = 20;
```

**3.** Что выведет этот код?

```js
sayHi();
sayBye();

function sayHi() {
  console.log("Привет!");
}

var sayBye = function() {
  console.log("Пока!");
};
```

**4.** Исправь код чтобы он работал правильно.

```js
console.log(multiply(3, 4));

var multiply = function(a, b) {
  return a * b;
};
```

**5.** Что выведет этот код?

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
```

Как исправить чтобы вывело `0, 1, 2`?

---

## Итог

**Hoisting** — JavaScript поднимает объявления переменных и функций наверх до запуска кода.

- `var` — поднимается с значением `undefined`
- `let` и `const` — поднимаются но попадают в TDZ
- `function declaration` — поднимается полностью, можно вызвать до объявления
- `function expression` и `arrow function` — не поднимаются

**TDZ** — период когда `let` и `const` уже существуют но ещё недоступны. Защищает от случайного использования переменной до её объявления.

Главное правило: всегда объявляй переменные и функции до их использования. Используй `let` и `const` вместо `var`.

# JavaScript — Лекции

## Навигация

- [1. Строки и методы строк](#1-строки-и-методы-строк)
- [2. Рекурсия и Замыкания](#2-рекурсия-и-замыкания)
- [3. Массивы](#3-массивы)
- [4. Hoisting и TDZ](#4-hoisting-и-tdz)

---

---

# 1. Строки и методы строк

## Содержание

- [Что такое строка](#что-такое-строка)
- [Создание строки](#создание-строки)
- [Длина строки](#длина-строки)
- [Доступ к символам](#доступ-к-символам)
- [Методы строк](#методы-строк)
- [Шаблонные строки](#шаблонные-строки)
- [Задания — Строки](#задания--строки)

---

## Что такое строка

Строка — это текст. Любой набор символов: буквы, цифры, пробелы, знаки.

```js
let name   = "Ibrohim";
let city   = "Гисар";
let number = "2008";  // это строка, не число
let empty  = "";      // пустая строка
```

---

## Создание строки

В JavaScript строку можно написать тремя способами:

```js
let a = "двойные кавычки";
let b = 'одинарные кавычки';
let c = `обратные кавычки`;  // шаблонная строка
```

Разницы почти нет. Обратные кавычки удобны когда нужно вставить переменную внутрь — об этом в конце.

---

## Длина строки

`length` — показывает сколько символов в строке.

```js
let name = "Ibrohim";
console.log(name.length); // 7

let city = "Гисар";
console.log(city.length); // 5

let empty = "";
console.log(empty.length); // 0
```

---

## Доступ к символам

Каждый символ в строке имеет номер — индекс. Счёт начинается с нуля.

```js
let name = "Ibrohim";
//          0 1 2 3 4 5 6

console.log(name[0]); // "I"
console.log(name[1]); // "b"
console.log(name[6]); // "m"
```

Последний символ:

```js
console.log(name[name.length - 1]); // "m"
```

---

## Методы строк

### toUpperCase и toLowerCase

Переводит все буквы в верхний или нижний регистр.

```js
let name = "Ibrohim";

console.log(name.toUpperCase()); // "IBROHIM"
console.log(name.toLowerCase()); // "ibrohim"
```

Полезно когда нужно сравнить строки без учёта регистра:

```js
let input = "ГИСАР";
let city  = "Гисар";

console.log(input.toLowerCase() === city.toLowerCase()); // true
```

---

### trim

Убирает пробелы в начале и конце строки.

```js
let input = "   Ibrohim   ";
console.log(input.trim()); // "Ibrohim"
```

---

### includes

Проверяет — есть ли одна строка внутри другой. Возвращает `true` или `false`.

```js
let text = "Добро пожаловать в Гисар";

console.log(text.includes("Гисар"));   // true
console.log(text.includes("Душанбе")); // false
```

---

### startsWith и endsWith

Проверяет с чего строка начинается или заканчивается.

```js
let email = "Ibrohim@gmail.com";

console.log(email.startsWith("Ibrohim")); // true
console.log(email.endsWith(".com"));      // true
console.log(email.endsWith(".ru"));       // false
```

---

### indexOf

Находит на какой позиции находится слово. Если не найдено — возвращает `-1`.

```js
let text = "Привет Ibrohim";

console.log(text.indexOf("Ibrohim")); // 7
console.log(text.indexOf("Бобур"));   // -1
```

---

### slice

Вырезает часть строки.

```js
let text = "Привет Ibrohim";

console.log(text.slice(0, 6)); // "Привет"
console.log(text.slice(7));    // "Ibrohim"
console.log(text.slice(-7));   // "Ibrohim"
```

---

### replace и replaceAll

Заменяет одну часть строки на другую.

```js
let text = "кот и кот и кот";

console.log(text.replace("кот", "пёс"));    // "пёс и кот и кот"
console.log(text.replaceAll("кот", "пёс")); // "пёс и пёс и пёс"
```

---

### split

Разбивает строку на массив по разделителю.

```js
let text = "яблоко,груша,банан";
let arr  = text.split(",");

console.log(arr);    // ["яблоко", "груша", "банан"]
console.log(arr[0]); // "яблоко"
```

---

### repeat

Повторяет строку несколько раз.

```js
let star = "*";
console.log(star.repeat(5)); // "*****"
```

---

### padStart и padEnd

Дополняет строку символами до нужной длины.

```js
let hours   = "9";
let minutes = "5";

console.log(hours.padStart(2, "0") + ":" + minutes.padStart(2, "0")); // "09:05"
```

---

## Шаблонные строки

Вместо склейки через `+` используй обратные кавычки и `${}`.

```js
let name = "Ibrohim";
let age  = 16;

// старый способ
console.log("Меня зовут " + name + " и мне " + age + " лет");

// новый способ
console.log(`Меня зовут ${name} и мне ${age} лет`);
```

Внутри `${}` можно писать любой код:

```js
let price    = 1000;
let discount = 30;

console.log(`Цена после скидки: ${price - price * discount / 100}`); // 700
```

---

## Важно помнить

Строки нельзя изменить. Каждый метод возвращает новую строку.

```js
let name = "ibrohim";
name.toUpperCase(); // ничего не меняет

console.log(name); // "ibrohim" — не изменилась

let upper = name.toUpperCase();
console.log(upper); // "IBROHIM"
```

---

## Задания — Строки

**1.** Напиши функцию `isEmail(str)` — проверяет является ли строка email адресом (содержит `@` и заканчивается на `.com`).

```js
isEmail("Ibrohim@gmail.com"); // true
isEmail("Ibrohim@gmail.ru");  // false
isEmail("Ibrohimgmail.com");  // false
```

**2.** Напиши функцию `capitalize(str)` — делает первую букву заглавной, остальные маленькими.

```js
capitalize("ibrohim"); // "Ibrohim"
capitalize("ГИСАР");   // "Гисар"
```

**3.** Напиши функцию `countWords(str)` — считает сколько слов в строке.

```js
countWords("Привет как дела"); // 3
countWords("JavaScript");      // 1
```

**4.** Напиши функцию `isPalindrome(str)` — проверяет является ли строка палиндромом.

```js
isPalindrome("level"); // true
isPalindrome("hello"); // false
isPalindrome("madam"); // true
```

---

## Итог — Строки

| Метод | Что делает |
|---|---|
| `length` | длина строки |
| `toUpperCase()` | все буквы заглавные |
| `toLowerCase()` | все буквы маленькие |
| `trim()` | убирает пробелы по краям |
| `includes()` | есть ли подстрока |
| `startsWith()` | начинается ли с... |
| `endsWith()` | заканчивается ли на... |
| `indexOf()` | позиция подстроки |
| `slice()` | вырезать часть |
| `replace()` | заменить часть |
| `split()` | разбить на массив |
| `repeat()` | повторить строку |
| `padStart()` | дополнить слева |
| `padEnd()` | дополнить справа |

---

---

# 2. Рекурсия и Замыкания

## Содержание

- [Рекурсия](#рекурсия)
- [Замыкания](#замыкания)
- [Задания — Рекурсия и Замыкания](#задания--рекурсия-и-замыкания)

---

## Рекурсия

Рекурсия — это когда функция вызывает саму себя.

Любая рекурсивная функция состоит из двух частей:

- **Base case** — условие остановки. Без него функция будет вызывать себя бесконечно и программа упадёт с ошибкой `Maximum call stack size exceeded`.
- **Recursive case** — вызов самой себя с меньшим значением.

```js
function example(n) {
  if (n <= 0) return 0;    // base case
  return example(n - 1);   // recursive case
}
```

---

### Пример 1 — Обратный отсчёт

```js
function countdown(n) {
  if (n === 0) return;
  console.log(n);
  countdown(n - 1);
}

countdown(5);
// 5
// 4
// 3
// 2
// 1
```

---

### Пример 2 — Факториал

```js
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
// 5 * 4 * 3 * 2 * 1 = 120
```

---

### Пример 3 — Сумма чисел

```js
function sum(n) {
  if (n === 1) return 1;
  return n + sum(n - 1);
}

console.log(sum(4)); // 10
// 4 + 3 + 2 + 1 = 10
```

---

## Замыкания

Замыкание — это когда функция запоминает переменные из внешней области видимости, даже после того как внешняя функция уже завершила работу.

```js
function outer() {
  let cnt = 0;

  return function() {
    cnt++;
    console.log(cnt);
  };
}

let counter = outer();
counter(); // 1
counter(); // 2
counter(); // 3
```

`outer()` уже завершилась, но `cnt` не удалилась — потому что внутренняя функция держит на неё ссылку. Это и есть замыкание.

---

### Пример 1 — Приветствие

```js
function greet(name) {
  return (message) => {
    console.log(name + ": " + message);
  };
}

let ibrohim = greet("Иброхим");
ibrohim("привет");   // Иброхим: привет
ibrohim("как дела"); // Иброхим: как дела
```

---

### Пример 2 — Скидка

```js
function discount(percent) {
  return (price) => {
    console.log(price - price * percent / 100);
  };
}

let vip = discount(30);
vip(1000); // 700
vip(500);  // 350
```

---

### Пример 3 — Счётчик

```js
function counter(start) {
  return () => {
    start++;
    console.log(start);
  };
}

let cnt = counter(0);
cnt(); // 1
cnt(); // 2
cnt(); // 3
```

---

### Пример 4 — Умножение

```js
function multiply(factor) {
  return (number) => {
    console.log(number * factor);
  };
}

let double = multiply(2);
double(5);  // 10
double(8);  // 16
double(12); // 24
```

---

### Пример 5 — Пароль

```js
function checkPass(correct) {
  return (input) => {
    console.log(input === correct ? "верно" : "неверно");
  };
}

let check = checkPass("secret123");
check("1234");      // неверно
check("secret123"); // верно
```

---

## Задания — Рекурсия и Замыкания

**1.** Напиши функцию `power(base, exp)` — возведение в степень без `Math.pow`.

```js
power(2, 3); // 8
power(3, 4); // 81
```

**2.** Напиши функцию `reverse(str)` — переворачивает строку рекурсией.

```js
reverse("hello"); // "olleh"
```

**3.** Напиши функцию `makeAdder(x)` — возвращает функцию которая прибавляет `x`.

```js
let add5 = makeAdder(5);
add5(3);  // 8
add5(10); // 15
```

---

## Итог — Рекурсия и Замыкания

**Рекурсия** — функция вызывает себя. Нужен base case чтобы остановиться. Удобна для вложенных структур.

**Замыкание** — функция запоминает переменные из внешней области. Используется для счётчиков, приватных данных, генераторов функций.

---

---

# 3. Массивы

## Содержание

- [Что такое массив](#что-такое-массив)
- [Создание массива](#создание-массива)
- [Доступ к элементам](#доступ-к-элементам)
- [Основные методы](#основные-методы)
- [Методы перебора](#методы-перебора)
- [Поиск в массиве](#поиск-в-массиве)
- [Сортировка](#сортировка)
- [Spread и Rest](#spread-и-rest)
- [Деструктуризация](#деструктуризация)
- [Задания — Массивы](#задания--массивы)

---

## Что такое массив

Массив — это список значений в одной переменной.

Без массива:

```js
let student1 = "Иброхим";
let student2 = "Азим";
let student3 = "Камол";
```

С массивом:

```js
let students = ["Иброхим", "Азим", "Камол"];
```

Массив может хранить любые типы данных:

```js
let arr = [1, "привет", true, null, [1, 2]];
```

---

## Создание массива

```js
let arr     = [];                        // пустой
let fruits  = ["яблоко", "груша", "банан"]; // строки
let numbers = [1, 2, 3, 4, 5];          // числа
```

---

## Доступ к элементам

Каждый элемент имеет индекс. Счёт начинается с нуля.

```js
let fruits = ["яблоко", "груша", "банан"];
//                0         1       2

console.log(fruits[0]); // "яблоко"
console.log(fruits[1]); // "груша"
console.log(fruits[2]); // "банан"
```

Последний элемент:

```js
console.log(fruits[fruits.length - 1]); // "банан"
console.log(fruits.at(-1));             // "банан"
```

---

## Основные методы

### push и pop

`push` — добавляет в конец. `pop` — удаляет с конца.

```js
let arr = ["а", "б", "в"];

arr.push("г");
console.log(arr); // ["а", "б", "в", "г"]

arr.pop();
console.log(arr); // ["а", "б", "в"]
```

---

### unshift и shift

`unshift` — добавляет в начало. `shift` — удаляет с начала.

```js
let arr = ["а", "б", "в"];

arr.unshift("я");
console.log(arr); // ["я", "а", "б", "в"]

arr.shift();
console.log(arr); // ["а", "б", "в"]
```

---

### splice

Удаляет, заменяет или добавляет элементы в любом месте.

```js
let arr = ["а", "б", "в", "г", "д"];

arr.splice(1, 2);
console.log(arr); // ["а", "г", "д"]

let arr2 = ["а", "б", "в"];
arr2.splice(1, 1, "я");
console.log(arr2); // ["а", "я", "в"]
```

---

### slice

Вырезает часть массива. Оригинал не меняется.

```js
let arr = ["а", "б", "в", "г", "д"];

console.log(arr.slice(1, 3)); // ["б", "в"]
console.log(arr.slice(-2));   // ["г", "д"]
console.log(arr);             // ["а", "б", "в", "г", "д"]
```

---

### concat

Объединяет два массива.

```js
let a = [1, 2, 3];
let b = [4, 5, 6];

let c = a.concat(b);
console.log(c); // [1, 2, 3, 4, 5, 6]
```

---

### join

Соединяет все элементы массива в строку.

```js
let fruits = ["яблоко", "груша", "банан"];

console.log(fruits.join(", "));  // "яблоко, груша, банан"
console.log(fruits.join(" — ")); // "яблоко — груша — банан"
```

---

### reverse

Переворачивает массив. Меняет оригинал.

```js
let arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr); // [5, 4, 3, 2, 1]
```

---

### flat

Разворачивает вложенные массивы.

```js
let arr = [1, [2, 3], [4, [5, 6]]];

console.log(arr.flat());         // [1, 2, 3, 4, [5, 6]]
console.log(arr.flat(2));        // [1, 2, 3, 4, 5, 6]
console.log(arr.flat(Infinity)); // [1, 2, 3, 4, 5, 6]
```

---

## Методы перебора

### forEach

Проходит по каждому элементу. Ничего не возвращает.

```js
let fruits = ["яблоко", "груша", "банан"];

fruits.forEach((fruit, index) => {
  console.log(index + ": " + fruit);
});
// 0: яблоко
// 1: груша
// 2: банан
```

---

### map

Проходит по каждому элементу и возвращает новый массив.

```js
let numbers = [1, 2, 3, 4, 5];

let doubled = numbers.map((n) => n * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
```

---

### filter

Возвращает новый массив только с теми элементами которые прошли условие.

```js
let numbers = [1, 2, 3, 4, 5, 6, 7, 8];

let even = numbers.filter((n) => n % 2 === 0);
console.log(even); // [2, 4, 6, 8]
```

---

### reduce

Сворачивает массив в одно значение.

```js
let numbers = [1, 2, 3, 4, 5];

let sum = numbers.reduce((total, n) => total + n, 0);
console.log(sum); // 15
```

---

## Поиск в массиве

### includes

Проверяет есть ли элемент в массиве.

```js
let fruits = ["яблоко", "груша", "банан"];

console.log(fruits.includes("груша"));    // true
console.log(fruits.includes("апельсин")); // false
```

---

### find

Возвращает первый элемент который прошёл условие.

```js
let numbers = [1, 3, 5, 8, 10];

let firstEven = numbers.find((n) => n % 2 === 0);
console.log(firstEven); // 8
```

---

### findIndex

Возвращает индекс первого элемента который прошёл условие.

```js
let numbers = [1, 3, 5, 8, 10];

console.log(numbers.findIndex((n) => n % 2 === 0)); // 3
console.log(numbers.findIndex((n) => n > 100));     // -1
```

---

### some и every

`some` — хотя бы один элемент прошёл условие.
`every` — все элементы прошли условие.

```js
let numbers = [1, 2, 3, 4, 5];

console.log(numbers.some((n) => n > 4));  // true
console.log(numbers.every((n) => n > 0)); // true
console.log(numbers.every((n) => n > 2)); // false
```

---

## Сортировка

```js
// строки
let fruits = ["банан", "яблоко", "груша"];
fruits.sort();
console.log(fruits); // ["банан", "груша", "яблоко"]

// числа — правильно:
let nums = [10, 1, 5, 2, 8];
nums.sort((a, b) => a - b);
console.log(nums); // [1, 2, 5, 8, 10]

// по убыванию:
nums.sort((a, b) => b - a);
console.log(nums); // [10, 8, 5, 2, 1]
```

---

## Spread и Rest

### Spread — разворачивает массив

```js
let a = [1, 2, 3];
let b = [4, 5, 6];

let c = [...a, ...b];
console.log(c); // [1, 2, 3, 4, 5, 6]

let copy = [...a];
copy.push(99);
console.log(a);    // [1, 2, 3]
console.log(copy); // [1, 2, 3, 99]
```

---

### Rest — собирает аргументы в массив

```js
function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}

console.log(sum(1, 2, 3));       // 6
console.log(sum(1, 2, 3, 4, 5)); // 15
```

---

## Деструктуризация

```js
let fruits = ["яблоко", "груша", "банан"];

let [first, second, third] = fruits;
console.log(first);  // "яблоко"
console.log(second); // "груша"
console.log(third);  // "банан"

// остаток:
let [head, ...tail] = fruits;
console.log(head); // "яблоко"
console.log(tail); // ["груша", "банан"]
```

Поменять переменные местами:

```js
let x = 1;
let y = 2;

[x, y] = [y, x];
console.log(x); // 2
console.log(y); // 1
```

---

## Задания — Массивы

**1.** Есть массив чисел. Напиши код который выводит только чётные числа.

```js
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
// результат: [2, 4, 6, 8, 10]
```

**2.** Напиши функцию `getNames(users)` которая принимает массив объектов и возвращает массив только имён.

```js
let users = [
  { name: "Иброхим", age: 16 },
  { name: "Азим",    age: 18 },
  { name: "Камол",   age: 20 }
];

getNames(users); // ["Иброхим", "Азим", "Камол"]
```

**3.** Напиши функцию `sumArray(arr)` которая возвращает сумму всех чисел.

```js
sumArray([1, 2, 3, 4, 5]); // 15
```

**4.** Напиши функцию `removeDuplicates(arr)` которая убирает повторяющиеся элементы.

```js
removeDuplicates([1, 2, 2, 3, 3, 3, 4]); // [1, 2, 3, 4]
```

---

## Итог — Массивы

| Метод | Что делает |
|---|---|
| `push` / `pop` | добавить / удалить с конца |
| `unshift` / `shift` | добавить / удалить с начала |
| `splice` | удалить, добавить, заменить в любом месте |
| `slice` | вырезать часть массива |
| `concat` | объединить массивы |
| `join` | массив в строку |
| `reverse` | перевернуть массив |
| `flat` | развернуть вложенные массивы |
| `forEach` | пройтись по каждому элементу |
| `map` | создать новый массив с изменёнными элементами |
| `filter` | оставить только элементы которые прошли условие |
| `reduce` | свернуть массив в одно значение |
| `includes` | есть ли элемент |
| `find` | найти первый элемент по условию |
| `findIndex` | найти индекс по условию |
| `some` | хотя бы один прошёл условие |
| `every` | все прошли условие |
| `sort` | сортировка |

---

---

# 4. Hoisting и TDZ

## Содержание

- [Что такое Hoisting](#что-такое-hoisting)
- [Hoisting переменных](#hoisting-переменных)
- [Hoisting функций](#hoisting-функций)
- [TDZ — Temporal Dead Zone](#tdz--temporal-dead-zone)
- [Итоговое сравнение](#итоговое-сравнение)
- [Частые ошибки — Hoisting](#частые-ошибки--hoisting)

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

## Частые ошибки — Hoisting

### Ошибка 1 — использовать var и ждать ошибку

```js
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
  let name = "Азим";
  console.log(name); // "Азим"
}
```

---

## Итог — Hoisting и TDZ

**Hoisting** — JavaScript поднимает объявления переменных и функций наверх до запуска кода.

- `var` — поднимается с значением `undefined`
- `let` и `const` — поднимаются но попадают в TDZ
- `function declaration` — поднимается полностью, можно вызвать до объявления
- `function expression` и `arrow function` — не поднимаются

**TDZ** — период когда `let` и `const` уже существуют но ещё недоступны. Защищает от случайного использования переменной до её объявления.

Главное правило: всегда объявляй переменные и функции до их использования. Используй `let` и `const` вместо `var`.


# Строки и методы строк в JavaScript

---

## Содержание

- [Что такое строка](#что-такое-строка)
- [Создание строки](#создание-строки)
- [Длина строки](#длина-строки)
- [Доступ к символам](#доступ-к-символам)
- [Методы строк](#методы-строк)
- [Шаблонные строки](#шаблонные-строки)
- [Задания](#задания)

---

## Что такое строка

Строка — это текст. Любой набор символов: буквы, цифры, пробелы, знаки.

```js
let name    = "Ibrohim";
let city    = "Гисар";
let number  = "2008";   // это строка, не число
let empty   = "";        // пустая строка
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
//          0 1 2 3 4 5 6 7

console.log(name[0]); // "I"
console.log(name[1]); // "b"
console.log(name[3]); // "o"
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
console.log(name.toLowerCase()); // "Ibrohim"
```

Полезно когда нужно сравнить строки без учёта регистра:

```js
let input = "ГИСАР";
let city  = "Гисар";

console.log(input.toLowerCase() === city.toLowerCase()); // true
```

---

### trim

Убирает пробелы в начале и конце строки. Часто нужно когда пользователь вводит текст.

```js
let input = "   Ibrohim   ";

console.log(input.trim()); // "Ibrohim"
```

```js
let trimStart = "   привет".trimStart(); // "привет"
let trimEnd   = "привет   ".trimEnd();   // "привет"
```

---

### includes

Проверяет — есть ли одна строка внутри другой. Возвращает `true` или `false`.

```js
let text = "Добро пожаловать в  Гисар";

console.log(text.includes("Гисар")); // true
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

Находит на какой позиции находится символ или слово. Если не найдено — возвращает `-1`.

```js
let text = "Привет Ibrohim";

console.log(text.indexOf("Ibrohim")); // 7
console.log(text.indexOf("IbrohimT"));  // -1
```

Часто используют так:

```js
if (text.indexOf("Ibrohim") !== -1) {
  console.log("найдено");
}

// или короче:
if (text.includes("Ibrohim")) {
  console.log("найдено");
}
```

---

### slice

Вырезает часть строки. Принимает два числа: начало и конец.

```js
let text = "Привет Ibrohim";
//          0123456789...

console.log(text.slice(0, 5));  // "Привет"
console.log(text.slice(7));     // "Ibrohim"  — до конца
console.log(text.slice(-7));    // "Ibrohim"  — с конца
```

---

### replace

Заменяет одну часть строки на другую.

```js
let text = "Привет Ibrohim";

console.log(text.replace("Ibrohim", "IbrohimT")); // "Привет IbrohimT"
```

Заменяет только первое совпадение. Чтобы заменить все — используй `replaceAll`:

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
let arr = text.split(",");

console.log(arr); // ["яблоко", "груша", "банан"]
console.log(arr[0]); // "яблоко"
```

Разбить по пробелам:

```js
let sentence = "Привет как дела";
let words = sentence.split(" ");

console.log(words); // ["Привет", "как", "дела"]
console.log(words.length); // 3
```

Разбить на отдельные символы:

```js
let name = "Али";
console.log(name.split("")); // ["А", "л", "и"]
```

---

### repeat

Повторяет строку несколько раз.

```js
let star = "*";
console.log(star.repeat(5)); // "*****"

let line = "=-";
console.log(line.repeat(3)); // "=-=-="
```

---

### padStart и padEnd

Дополняет строку символами до нужной длины. Удобно для форматирования.

```js
let num = "5";
console.log(num.padStart(3, "0")); // "005"
console.log(num.padEnd(3, "0"));   // "500"

// Часы и минуты:
let hours   = "9";
let minutes = "5";
console.log(hours.padStart(2, "0") + ":" + minutes.padStart(2, "0")); // "09:05"
```

---

## Шаблонные строки

Вместо склейки строк через `+` можно использовать обратные кавычки и `${}`.

```js
let name = "Ibrohim";
let age  = 20;

// старый способ
console.log("Меня зовут " + name + " и мне " + age + " лет");

// новый способ — шаблонная строка
console.log(`Меня зовут ${name} и мне ${age} лет`);
```

Внутри `${}` можно писать любой код:

```js
let price = 1000;
let main = 30;

console.log(`Цена после скидки: ${price - price * main / 100}`); // 700
```

Многострочный текст:

```js
let message = `
  Привет, ${name}!
  Добро пожаловать.
`;
console.log(message);
```

---

## Важно помнить

Строки нельзя изменить — они неизменяемые. Каждый метод возвращает новую строку.

```js
let name = "Ibrohim";
name.toUpperCase(); // это ничего не меняет

console.log(name); // "Ibrohim" — всё ещё маленькими

// правильно:
let upperName = name.toUpperCase();
console.log(upperName); // "IBROHIM"
```

---

## Задания

**1.** Напиши функцию `main(str)` — проверяет является ли строка email адресом (содержит `@` и заканчивается на `.com`).

```js
main("Ibrohim@gmail.com"); // true
main("Ibrohim@gmail.ru");  // false
main("Ibrohimgmail.com");  // false
```

**2.** Напиши функцию `capitalize(str)` — делает первую букву заглавной, остальные маленькими.

```js
capitalize("Ibrohim");  // "Ibrohim"
capitalize("IBROHIM T");   // "IBROHIM T"
```

**3.** Напиши функцию `countWords(str)` — считает сколько слов в строке.

```js
countWords("Привет как дела");  // 3
countWords("JavaScript");       // 1
```

**4.** Напиши функцию `isPalindrome(str)` — проверяет является ли строка палиндромом (читается одинаково с обеих сторон).

```js
isPalindrome("level");  // true
isPalindrome("hello");  // false
isPalindrome("madam");  // true
```

---

## Итог

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

# Рекурсия и Замыкания в JavaScript

---

## Содержание

- [Рекурсия](#рекурсия)
- [Замыкания](#замыкания)

---

## Рекурсия

Рекурсия — это когда функция вызывает саму себя.

Любая рекурсивная функция состоит из двух частей:

- **Base case** — условие остановки. Без него функция будет вызывать себя бесконечно и программа упадёт с ошибкой `Maximum call stack size exceeded`.
- **Recursive case** — вызов самой себя с меньшим значением.

```js
function main(n) {
  if (n <= 0) return 0;   // base case
  return main(n - 1);     // recursive case
}
```

---

### Пример 1 — Обратный отсчёт

```js
function main(n) {
  if (n === 0) return;
  console.log(n);
  main(n - 1);
}

console.log(main(5));
// 5
// 4
// 3
// 2
// 1
```

---

### Пример 2 — Факториал

```js
function main(n) {
  if (n <= 1) return 1;
  return n * main(n - 1);
}

console.log(main(5)); // 120
// 5 * 4 * 3 * 2 * 1 = 120
```

---

### Пример 3 — Сумма чисел

```js
function main(n) {
  if (n === 1) return 1;
  return n + main(n - 1);
}

console.log(main(4)); // 10
// 4 + 3 + 2 + 1 = 10
```

---

## Замыкания

Замыкание — это когда функция запоминает переменные из внешней области видимости, даже после того как внешняя функция уже завершила работу.

```js
function main() {
  let cnt = 0;

  function main1() {
    cnt++;
    console.log(cnt);
  }

  return main1;
}

let ccnt = main();
console.log(ccnt()); // 1
console.log(ccnt()); // 2
console.log(ccnt()); // 3
```

`main()` уже завершилась, но `cnt` не удалилась — потому что `main1` держит на неё ссылку. Это и есть замыкание.

---

### Пример 1 — Салом гуфтан

```js
function main(name) {
    return (message) => {
        console.log(name + ": " + message);
    };
}

let Ibrohim = main("Иброхим");
console.log(Ibrohim("привет"));   // Иброхим: привет
console.log(Ibrohim("как дела")); // Иброхим: как дела
```

---

### Пример 2 — Скидка

```js
function main(percent) {
    return (price) => {
        console.log(price - price * percent / 100);
    };
}

let Ibrohim = main(30);
console.log(Ibrohim(1000)); // 700
console.log(Ibrohim(500));  // 350
```

---

### Пример 3 — Счётчик

```js
function main(start) {
    return () => {
        start++;
        console.log(start);
    };
}

let cnt = main(0);
console.log(cnt()); // 1
console.log(cnt()); // 2
console.log(cnt()); // 3
```

---

### Пример 4 — Умножение

```js
function main(factor) {
    return (number) => {
        console.log(number * factor);
    };
}

let Ibrohim = main(2);
console.log(Ibrohim(5));  // 10
console.log(Ibrohim(8);  // 16
console.log(Ibrohim(12)) ; // 24
```

---

## Итог

**Рекурсия** — функция вызывает себя. Нужен base case чтобы остановиться. Удобна для вложенных структур.

**Замыкание** — функция запоминает переменные из внешней области. Используется для счётчиков, приватных данных, кэша.
---

# Массивы (Array) в JavaScript

---

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
- [Итог](#итог)

---

## Что такое массив

Массив — это список значений в одной переменной.

Без массива:

```js
let student1 = "Ибпохим";
let student2 = "Азим";
let student3 = "Иброхим";
```

С массивом:

```js
let students = ["Иброхим", "Азим", "Иброхим"];
```

Массив может хранить любые типы данных:

```js
let arr = [1, "привет", true, null, [1, 2]];
```

---

## Создание массива

```js
// пустой массив
let arr = [];

// массив с элементами
let arr = ["яблоко", "груша", "банан"];

// массив чисел
let arr = [1, 2, 3, 4, 5];
```

---

## Доступ к элементам

Каждый элемент имеет индекс. Счёт начинается с нуля.

```js
let arr = ["яблоко", "груша", "банан"];
//            0         1       2

console.log(main[0]); // "яблоко"
console.log(main[1]); // "груша"
console.log(main[2]); // "банан"
```

Последний элемент:

```js
console.log(main[main.length - 1]); // "банан"

// или новый способ:
console.log(main.at(-1)); // "банан"
console.log(main.at(-2)); // "груша"
```

Изменить элемент:

```js
arr[0] = "апельсин";
console.log(arr); // ["апельсин", "груша", "банан"]
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

// удалить 2 элемента начиная с индекса 1
arr.splice(1, 2);
console.log(arr); // ["а", "г", "д"]

// заменить элемент
let arr2 = ["а", "б", "в"];
arr2.splice(1, 1, "я");
console.log(arr2); // ["а", "я", "в"]

// добавить без удаления
let arr3 = ["а", "б", "в"];
arr3.splice(1, 0, "новый");
console.log(arr3); // ["а", "новый", "б", "в"]
```

---

### slice

Вырезает часть массива и возвращает новый массив. Оригинал не меняется.

```js
let arr = ["а", "б", "в", "г", "д"];

console.log(arr.slice(1, 3)); // ["б", "в"]
console.log(arr.slice(2));    // ["в", "г", "д"]
console.log(arr.slice(-2));   // ["г", "д"]
console.log(arr);             // ["а", "б", "в", "г", "д"] — не изменился
```

---

### concat

Объединяет два или больше массивов.

```js
let a = [1, 2, 3];
let b = [4, 5, 6];

let c = a.concat(b);
console.log(c); // [1, 2, 3, 4, 5, 6]

// три массива:
let d = a.concat(b, [7, 8]);
console.log(d); // [1, 2, 3, 4, 5, 6, 7, 8]
```

---

### join

Соединяет все элементы массива в строку.

```js
let arr = ["яблоко", "груша", "банан"];

console.log(arr.join(", "));  // "яблоко, груша, банан"
console.log(arr.join(" — ")); // "яблоко — груша — банан"
console.log(arr.join(""));    // "яблокогрушабанан"
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

console.log(arr.flat());    // [1, 2, 3, 4, [5, 6]]
console.log(arr.flat(2));   // [1, 2, 3, 4, 5, 6]
console.log(arr.flat(Infinity)); // [1, 2, 3, 4, 5, 6] — любая глубина
```

---

## Методы перебора

### forEach

Проходит по каждому элементу. Ничего не возвращает.

```js
let arr = ["яблоко", "груша", "банан"];

arr.forEach((fr) => {
    console.log(fr);
});
// яблоко
// груша
// банан

// с индексом:
arr.forEach((fr, i) => {
    console.log(i + ": " + fr);
});
// 0: яблоко
// 1: груша
// 2: банан
```

---

### map

Проходит по каждому элементу и возвращает новый массив.

```js
let num = [1, 2, 3, 4, 5];

let arr = num.map((n) => n * 2);
console.log(arr); // [2, 4, 6, 8, 10]
```

---

### filter

Возвращает новый массив только с теми элементами которые прошли условие.

```js
let num = [1, 2, 3, 4, 5, 6, 7, 8];

let even = num.filter((n) => n % 2 === 0);
console.log(even); // [2, 4, 6, 8]

let big = num.filter((n) => n > 5);
console.log(big); // [6, 7, 8]
```

---

### reduce

Сворачивает массив в одно значение.

```js
let num = [1, 2, 3, 4, 5];

let sum = num.reduce((to, n) => to + n, 0);
console.log(sum); // 15

let pro = num.reduce((to, n) => to * n, 1);
console.log(pro); // 120
```

Найти максимальное число:

```js
let num = [3, 7, 1, 9, 4];

let max = num.reduce((a, b) => a > b ? a : b);
console.log(max); // 9
```

---

## Поиск в массиве

### includes

Проверяет есть ли элемент в массиве.

```js
let arr = ["яблоко", "груша", "банан"];

console.log(arr.includes("груша"));   // true
console.log(arr.includes("апельсин")); // false
```

---

### find

Возвращает первый элемент который прошёл условие.

```js
let num = [1, 3, 5, 8, 10];

let 
fir = num.find((n) => n % 2 === 0);
console.log(
  fir
); // 8
`

---

### findIndex

Возвращает индекс первого элемента который прошёл условие. Если не найдено — `-1`.

```js
let num = [1, 3, 5, 8, 10];

console.log(num.findIndex((n) => n % 2 === 0)); // 3
console.log(num.findIndex((n) => n > 100));     // -1
```

---

### some и every

`some` — хотя бы один элемент прошёл условие.
`every` — все элементы прошли условие.

```js
let num = [1, 2, 3, 4, 5];

console.log(num.some((n) => n > 4));  // true — есть 5
console.log(num.every((n) => n > 0)); // true — все больше 0
console.log(num.every((n) => n > 2)); // false — 1 и 2 не больше 2
```

---

## Сортировка

### sort

По умолчанию сортирует как строки — для чисел нужна функция сравнения.

```js
// строки
let arr = ["банан", "яблоко", "груша"];
arr.sort();
console.log(arr); // ["банан", "груша", "яблоко"]

// числа — неправильно без функции:
let nums = [10, 1, 5, 2, 8];
nums.sort();
console.log(nums); // [1, 10, 2, 5, 8] — неверно!

// числа — правильно:
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

// копия массива:
let copy = [...a];
copy.push(99);
console.log(a);    // [1, 2, 3] — оригинал не изменился
console.log(copy); // [1, 2, 3, 99]

// передать массив как аргументы:
let num = [3, 1, 7, 2];
console.log(Math.max(...num)); // 7
```

---

### Rest — собирает аргументы в массив

```js
function sum(...num) {
    return num.reduce((to, n) => to + n, 0);
}

console.log(sum(1, 2, 3));       // 6
console.log(sum(1, 2, 3, 4, 5)); // 15
```

---

## Деструктуризация

Вытащить элементы из массива в переменные.

```js
let arr = ["яблоко", "груша", "банан"];

let [first, second, third] = arr;
console.log(first);  // "яблоко"
console.log(second); // "груша"
console.log(third);  // "банан"

// пропустить элемент:
let [a, , c] = arr;
console.log(a); // "яблоко"
console.log(c); // "банан"

// остаток:
let [head, ...tail] = arr;
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

## Итог

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
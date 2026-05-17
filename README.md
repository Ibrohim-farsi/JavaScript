
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
let fruits = text.split(",");

console.log(fruits); // ["яблоко", "груша", "банан"]
console.log(fruits[0]); // "яблоко"
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

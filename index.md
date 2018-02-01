# Список всех критериев интенсива Node.js



# Базовые критерии


## Задача

### Код соответствует техническому заданию проекта
Все обязательные пункты технического задания выполнены

### При выполнении кода не возникает необработанных ошибок
Во время работы приложения нет сообщений вида `warning` и предупреждений о неправильном вызове методов, `API` и прочего.
В пользовательском коде не используется `deprecated` API.
Во время работы приложения в логах не логгируются ошибки, а также приложение не падает при любых сценариях использования, кроме случаев предусмотренных спецификацией

## Именование

### Название переменных, параметров, свойств и методов начинается со строчной буквы и записываются в нотации [CamelCase](https://ru.wikipedia.org/wiki/CamelCase) 

### Для названия значений используются английские существительные
Сокращения в словах запрещены. Сокращённые названия переменных можно использовать только, если такое название широко распространено. Допустимые сокращения:
- `it`, для текущего итерируемого элемента массива/итератора `wizards.map((it) => it.name);`
- `i`, `j`, `k`, `l`, `t` для счётчика в цикле, `j` для счётчика во вложенном цикле и так далее по алфавиту
- если циклов два и более, то можно не переиспользовать переменную `i`
- `cb` для единственного коллбэка в параметрах функции

### Названия констант (постоянных значений) написаны прописными (заглавными) буквами
Слова разделяются подчёркиваниями (`UPPER_SNAKE_CASE`), например:
 ```js
 const MAX_HEIGHT = 400;
 const EARTH_RADIUS = 6370;
 ```
 
### Классы названы английскими существительными. Название класса начинается с прописной (заглавной) буквы

Неправильно:
```js
class wizard {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

class Run {
  constructor() {
    console.log(`О, я бегу!`);
  }
}
```

Правильно:
```js
class Wizard {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

class Runner {
  constructor() {
    console.log(`О, я бегун!`);
  }
}
```

### Перечисления (`Enum`) названы английскими существительными и начинаются с прописной (заглавной) буквы
Перечисления начинаются с прописной (заглавной) буквы. Перечисления названы существительными в единственном числе. Значения перечислений объявлены как константы

Неправильно:
```js
const view = {
  artist: Artist,
  genre: Genre,
};

const EndGameType = {
  lives: `lives`,
  quests: `quests`,
};
```

Правильно:
```js
const View = {
  ARTIST: Artist,
  GENRE: Genre,
};

const EndGameType = {
  LIVES: `lives`,
  QUESTS: `quests`,
};
```

### Название функции или метода содержит глагол
Название функции/метода должно быть глаголом и соответствовать действию, которое выполняет функция/метод. Например, можно использовать глагол `get` для функций/методов, которые что-то возвращают

Исключения:
1. Функции конструкторы (см. критерий `Конструкторы названы английскими существительными`)
2. Функции обработчики/коллбэки (см. критерий `Из названия обработчика события и функции-коллбэка следует, что это обработчик`)

Неправильно:
```js
const function1 = (names) => {
  names.forEach((name) => {
    console.log(name);
  });
};

const wizard = {
  name: `Гендальф`,
  action() {
    console.log(`Стреляю файрболлом!`);
  }
};

const randomNumber = () => {
  return Math.random();
};
```

Правильно:
```js
const printNames = (names) => {
  names.forEach((name) => {
    console.log(name);
  });
};

const wizard = {
  name: `Гендальф`,
  fire() {
    console.log(`Стреляю файрболлом!`);
  }
};

const getRandomNumber = () => {
  return Math.random();
};
```

### Названия модулей записаны строчными (маленькими) буквами. Слова разделены дефисами
Для того, чтобы избежать конфликтов имён в разных операционных системах, лучше применять наименее конфликтный способ именования файлов — строчными (маленькими) буквами через дефис


## Форматирование и внешний вид

### Неизменяемые значения объявлены через `const`
При объявлении новых значений, предпочтение стоит отдавать использованию ключевого слова `const`. 
Использовать `let` нужно только в том случае, если значение будет перезаписано. Использование `var` запрещено (<img src="https://eslint.org/img/logo.svg" width="24" alt="ESLint"/>)

Неправильно:
```js
let a = 1;
let b = 2;
let sum = a + b;
```

Правильно:
```js
const a = 1;
const b = 2;
const sum = a + b;

for (let i = 0; i < 42; i++) {
  console.log(i);
}
```

Неправильно:
```js
let level = getLevel(this.state.level, this.quest);
let answerNames = Object.keys(level.answers);
let answers = answerNames.map((key) => ({key, value: level.answers[key]}));
```
Правильно:
```js
const level = getLevel(this.state.level, this.quest);
const answerNames = Object.keys(level.answers);
const answers = answerNames.map((key) => ({key, value: level.answers[key]}));
```

### Используются обязательные блоки кода <img src="https://eslint.org/img/logo.svg" width="24" alt="ESLint"/>
В любых конструкциях, где подразумевается использование блока кода (фигурных скобок), таких как `for`, `while`, `if`, `switch`, `function` — блок кода используется обязательно, даже если инструкция состоит из одной строчки

Неправильно:
```js
(() => {
  if (x % 2 === 1) return;
})();
```

Правильно:
```js
(() => {
  if (x % 2 === 1) {
    return;
  }
})();
```

Исключения составляют однострочные стрелочные функции, которые можно использовать без обязательных блоков кода:
```js
const checkedCheckBoxes = checkboxes.filter((checkbox) => checkbox.checked);
```

### Список констант идёт перед основным кодом
Все константы выносятся в начало файла после всех зависимостей (`import/require`)

### Код соответствует гайдлайнам <img src="https://eslint.org/img/logo.svg" width="24" alt="ESLint"/>
- Отступы между операторами и ключевым словами соответствуют стайлгайду.
- Для отступов используются одинаковые символы, вложенность кода обозначается отступами.
- Однообразно расставлены пробелы перед, после и внутри скобок, операторов и ключевых слов

---
Не возникает ошибок при проверке проекта ESLint: `npm i && npm test`

### Сложные составные константы собираются в перечисления `Enum`
Множества однотипных констант собираются в перечисления

Неправильно:
```js
const EARTH_WEIGHT = 5.972 * Math.pow(10, 24);
const EARTH_GRAVITY = 9.8;
const EARTH_RADIUS = 6370;
```

Правильно:
```js
const Earth = {
  WEIGHT: 5.972 * Math.pow(10, 24),
  GRAVITY: 9.8,
  RADIUS: 6370
};
```

### Для итерирования по массивам и структурам данных по которому можно итерироваться (**Iterable**) используется конструкция `for .. of`
Там где не требуется индекс элемента массива или нужно обойти все элементы итерируемой структуры данных, используется цикл `for .. of` вместо цикла `for`

Неправильно:
```js
for (let i = 0; i < levels.length; i++) {
  const level = levels[i];
  renderLevel(level);
}
```

Правильно:
```js
for (const level of levels) {
  renderLevel(level);
}
```
Или:
```js
levels.forEach((it) => renderLevel(it));
```

### Приватные поля в классах помечены
Названия методов, которые есть в классе, но не предназначены для внешнего использования начинаются с нижнего подчёркивания `_`. Доступ к таким полям из вне класса запрещён


## Мусор

### В итоговом коде проекта находятся только те файлы, которые были на момент создания репозитория, которые были получены в патчах и файлы, созданные по заданию

### В коде проекта нет файлов, модулей и частей кода, которые не используются, включая, закомментированные участки кода
Нет файлов скриптов, которые являются «мёртвым кодом», который никогда не выполняется

### В коде нет заранее недостижимых участков кода
Например:
- Невыполнимые условия:
```js
const happen = false;
if (happen) {
  console.log(`This will not happen anyway!`);
}
```

- Операции после выхода из функции <img src="https://eslint.org/img/logo.svg" width="16" alt="ESLint"/>: 
```js
(() => {
  return;
  console.log(`This will not happen!`);
})();
```

## Корректность

### Асинхронные функции используются корректно
Если в синхронной функции вызывается `async`-функция, то возвращаемый `Promise` должен обрабатывает ошибочную ситуацию `.catch()`

Неправильно:
```js
const doAsyncJob = async () => {
  throw new Error(`Can't finish my job`);
};

const doSyncJob = () => {
  doAsyncJob();
};
```
Правильно:
```js
const doAsyncJob = async () => {
  throw new Error(`Can't finish my job`);
};

const doSyncJob = () => {
  doAsyncJob().catch((e) => console.error(e.message));
};
```

### Версии используемых зависимостей зафиксированы в `package.json`
В списках зависимостей в файле `package.json` указаны точные версии используемых пакетов. Версия обязательно должна быть указана. Не допускается использование `^`, `*` и `~`

### Константы и перечисления нигде в коде не переопределяются
Константы и перечисления (`enum`) используются только для чтения, и никогда не переопределяются на всем промежутке жизни программы

### Используются строгие сравнения вместо нестрогих <img src="https://eslint.org/img/logo.svg" width="24" alt="ESLint"/>
Вместо операторов нестрогого сравнения `==` и `!=`, используются операторы строгого сравнения `===`, `!==`. [Таблицы истинности](http://dorey.github.io/JavaScript-Equality-Table/) для JavaScript

Неправильно:
```js
const foo = ``;
const bar = [];
if (foo == bar) {
  destroy(world);
}
```

Правильно:
```js
const foo = ``;
const bar = [];
if (foo === bar) {
  destroy(world);
}
```

### В коде не используются зарезервированные слова в качестве имён переменных и свойств
В названия переменных и свойств не включаются операторы и ключевые слова зарезервированные для будущих версий языка (например, `class`, `extends`).
Список всех зарезервированных слов можно найти [тут](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)   

### Шаблоны созданные в коде программы корректны
HTML-страница должна быть корректным **W3C** документом в любой момент работы программы. Т.о. шаблоны не должны конструировать некорректные HTML-фрагменты

Неправильно:
```html
<div class="player-wrapper" src="${answer.src}"></div>
```

Правильно:
```html
<div class="player-wrapper" data-src="${answer.src}"></div>
```

### API встроенных функций и объектов используется правильно
Передаются корректные значения, которые ожидаются по спецификации

Неправильно:
```js
const randomNumber = Math.random(12);
```
Правильно:
```js
const randomNumber = Math.random();
```
Встроенные методы массивов используются по назначению.

Неправильно:
```js
let greet = `Привет `;

wizards.map((it) => {
  greet += `, ${it.name}`;
});

console.log(`${greet}!`);
```
Правильно:
```js
const greet = `Привет `;

const names = wizards.map((it) => it.name);

console.log(`${greet} ${names.join(`, `)}!`);
```

### Отсутствуют потенциально некорректные операции
Например, некорректное сложение двух операндов как строк. Проблема приоритета конкатенации над сложением. 

Неправильно:
```js
new Date() + 1000;
```

Правильно:
```js
+new Date() + 1000;
```
Некорректные проверки на существование с числами. 
Пример некорректной проверки на то, что переменная является числом:
```js
const double = (value) => {
  if (!value) {
    return NaN;
  }

  return value * 2;
};

double(0);
double();
double(5);
```

Потенциально некорректная операция взятия целой части числа

Неправильно:
```js
const minutesNumber = ~~(seconds / 60);
```

Правильно:
```js
const minutesNumber = Math.trunc(seconds / 60);
```


## Модульность

### Все файлы JS представляют собой отдельные [Common.js](http://www.requirejs.org/docs/commonjs.html) модули
Экспорт и импорт значений производится при помощи ключевых слов `module.exports` и `require`. Сохранение в глобальную область видимости значений не допускается

Пример правильного модуля:
```js
require(`colors`);

const HELP_COMMAND = `--help`;
const VERSION_COMMAND = `--version`;

module.exports = {
  isApplicable(command) {
    return command === HELP_COMMAND;
  },
  execute() {
    console.log(`This application does nothing. Accessible params:
${HELP_COMMAND.italic.gray}    — prints this info;
${VERSION_COMMAND.italic.gray} — prints application version;`);
  }
};
```

### Все необходимые зависимости перечислены в самом начале модуля
Зависимости никогда не загружаются по ходу выполнения программы или внутри условия.
Все зависимости загружаются ровно один раз и после этого переиспользуются

Неправильно:
```js
const initBusBoy = process.env.IS_BUS_BOY ? require(`connect-busboy`) : () => {};

const setup = (app) => {
  app.use(require(`body-parser`).json());
  app.use(require(`body-parser`).urlencoded({extended: true}));
  
  app.use(initBusBoy());
};

module.exports = setup;
```
Правильно:
```js
const bodyParser = require(`body-parser`);
const initBusBoy = require(`connect-busboy`);

const setup = (app) => {
  app.use(bodyParser.json());
  app.use(bodyParser.urlencoded({extended: true}));

  if (process.env.IS_BUS_BOY) {
    app.use(initBusBoy());
  }
};

module.exports = setup;

```

### Все значения экспортируемые из модуля экспортируются в конце файла
Экспортируемые значения не должны появляться в середине модуля, а так же перетираться или подменяться внутри модуля

Неправильно:
```js
const DEFAULT_CONVERTER = (value) => value;

module.exports.DEFAULT_CONVERTER = DEFAULT_CONVERTER;

const printError = (name, value, message) => ({
  fieldName: name,
  fieldValue: value,
  errorMessage: message
});

module.exports.printError = printError;

const exists = (value) => {
  switch (typeof value) {
    case `number`:
      return !Number.isNaN(value);
    case `string`:
      return value.length > 0;
    default:
      return value;
  }
};

module.exports.exists = exists;
```
Правильно:
```js
const DEFAULT_CONVERTER = (value) => value;

const printError = (name, value, message) => ({
  fieldName: name,
  fieldValue: value,
  errorMessage: message
});

const exists = (value) => {
  switch (typeof value) {
    case `number`:
      return !Number.isNaN(value);
    case `string`:
      return value.length > 0;
    default:
      return value;
  }
};

module.exports = {DEFAULT_CONVERTER, printError, exists};
```

### Модули не экспортируют изменяющиеся переменные
Модуль не должен экспортировать переменную значение которой может измениться в будущем.
Модуль не должен экспортировать значение по условию

Неправильно:
```js
let latestResult = 42;

setTimeout(() => {
  latestResult = 100;
}, 2000);

module.exports = {latestResult};
```
Правильно:
```js
const latestResult = loadLatestResult();

module.exports = {latestResult};
```

Неправильно:
```js
const isRainingToday = Math.random() < 0.5;

if (isRainingToday) {
  module.exports = {isRainingToday};
}
```
Правильно:
```js
const isRainingToday = Math.random() < 0.5;

module.exports = {isRainingToday};
```

## Универсальность

### Код является кроссплатформенным и не вызывает ошибок в разных операционных системах

Этот критерий проверяет минимальную работоспособность кода в разных ОС: Windows, Mac OS, Linux.


## Оптимальность

### Своевременный выход из цикла: цикл не работает дольше чем нужно
Неправильно:
```js
apartments.forEach((it, index) => {
  if (index < 3) {
    render(it);
  }
});
```

Правильно:
```js
for (let i = 0; i < Math.min(apartments.length, 3); i++) {
  render(apartments[i]);
}
```

### Внутри шаблонов-строк (template literals) не используется конкатенация строк
Конкатенация строк в шаблонных строках является антипаттерном, т.к. ухудшает читаемость шаблонной строки

Неправильно:
```js
const page = `${header + `\n` + main + `\n` + footer}`;
```

Правильно:
```js
const page = `${header}\n${main}\n${footer}`;
```

### Количество вызовов циклов минимизировано
Если задачу можно решить за один проход по циклу, вместо нескольких она должна быть решена за один

Неправильно:
```js
const wizardNames = source.
    map((it) => it.wizard).
    map((it) => it.name);
```

Правильно:
```js
const wizardNames = source.map((it) => it.wizard.name);
```


## Безопасность

### Отсутствие операций записи на `HTTP GET` методах
`GET`-метод предназначен исключительно для получения данных, таким образом, что модификация данных в таких методах является плохой практикой.
И может быть использована исключительно для сохранения статистики


# Дополнительные критерии

## Задача

### Техническое задание реализовано в полном объёме
Все обязательные и необязательные пункты технического задания выполнены


## Именование

### Переменные носят абстрактные названия и не содержат имён собственных

Неправильно:
```js
const keks = {
  name: `Кекс`
};
```

Правильно:
```js
const cat = {
  name: `Кекс`
};
```

### Название методов и свойств объектов не содержит название объектов 
Неправильно:
```js
const popup = {
  openPopup() {
    console.log(`I will open popup`);
  }
};

class Wizard {
  constructor(name = `Пендальф`) {
    this.wizardName = name;
  }
}
```

Правильно
```js
const popup = {
  open() {
    console.log(`I will open popup`);
  }
};

class Wizard {
  constructor(name = `Пендальф`) {
    this.name = name;
  }
}
```

### Из названия обработчика события и функции-коллбэка следует, что это за обработчик
Для единственного обработчика или функции можно использовать `callback` или `cb`. Для именования нескольких обработчиков внутри одного модуля используется `on` или `handler` и описание события. Название обработчика строится следующим образом:
 - `on` + (на каком элементе) + что случилось:
 
```js
const onSidebarClick = () => {};
const onContentLoad = () => {};

const onResize = () => {};
```
 - (на каком элементе) + что случилось + `Handler`:
 
```js
const sidebarClickHandler = () => {};
const contentLoadHandler = () => {};

const resizeHandler = () => {};
```


## Единообразие

### Все функции объявлены единообразно
При объявлении функций используются только стрелочные функции. Для объявления методов объектов используется специальный синтаксис для методов. Для объявления классов используется ключевое слово `class`.
 Смешение стилей в рамках проекта не допускается

Функция:
```js
const getTheMeaningOfLive = () => {
  return 42;
};
```
или
```js
const getTheMeaningOfLive = function () {
  return 42;
};
```

Метод:
```js
const GOD = {
  createWorld() {
    return `Your world is ready!`;
  }
};
```

Конструктор
```js
class Planet {
  constructor(weight, mass) {
    this.weight = weight;
    this.mass = mass;
  }
}
```

---
Использование объявления функций через `function` допускается, но не рекомендуется, т.к. все возможные случаи использования контекстных функций решаются при помощи синтаксиса для методов и классов.

### Используется единый стиль именования переменных
Стиль именования переменных сохраняется во всех модулях, например:
- не следует мешать обработчики содержащие `Handler` и `on`
- если переменная хранит какую-то структуру данных, то название этой структуры отражено в имени (например `wizardSet`, `wizardNameMap`).

Неправильно:
```js
const wizardNames = new Set([`Радагаст`, `Ктулху`, `Сарумян`]);
const downloadHandler = (link) => sendFile(link);
const onNewRequest = (req, res) => res.status(200).send();
```

Правильно:
```js
const wizardNameSet = new Set([`Радагаст`, `Ктулху`, `Сарумян`]);
const downloadHandler = (link) => sendFile(link);
const requestHandler = (req, res) => res.status(200).send();
```

### Методы внутри классов упорядочены
Во всех классах методы упорядочены следующим образом:

1. Конструктор
2. Геттеры/сеттеры свойств объекта
3. Основные методы объекта:
  - Методы объекта
  - Приватные методы
  - Перегруженные методы родительских объектов
4. Обработчики событий
5. Статические методы

Сортировка основных методов объекта свободная, подразумевается что методы будут расположены оптимально для конкретного класса нет смысла ограничивать порядок, потому что он может меняться в зависимости от особенностей объекта.


## Модульность

### В случае, если одинаковый код повторяется в нескольких модулях, повторяющаяся часть вынесена в отдельный модуль
Критерий касается структурных единиц кода — повторяющийся блок кода, либо функции с одним и теми же конструкциями, например, утилитные методы для работы с DOM:
```js
const bodyParser = require(`body-parser`);
const busboy = require(`connect-busboy`);

const installMiddleware = (app) => {
  app.use(bodyParser.json());
  app.use(bodyParser.urlencoded({extended: true}));

  if (process.env.IS_BUS_BOY) {
    app.use(busboy());
  }
};

const async = (fn) => (req, res, next) => fn(req, res, next).catch(next);

module.exports = {installMiddleware, async};
```
**Не стоит выносить в отдельный модуль функцию, которая используется ровно один раз**

### Название модуля соответствует его содержимому
Разные логические части кода вынесены в отдельные файлы модулей.
Имя модуля должно соответствовать его содержимому. Например, если в модуле лежит класс `Store`, то и имя модуля должно быть `store.js`


## Корректность

### Методы, которые не используют поля класса объявлены как статические
Если метод не использует поля класса в котором он объявлен, то этот метод должен быть объявлен как статический:

Неправильно:
```js
class App {
  showWelcome() {
    showPage(ControllerID.WELCOME);
  }

  showGame() {
    showPage(ControllerID.GAME);
  }

  showScores() {
    showPage(ControllerID.SCOREBOARD);
  }
}
```

Правильно:
```js
class App {
  static showWelcome() {
    showPage(ControllerID.WELCOME);
  }

  static showGame() {
    showPage(ControllerID.GAME);
  }

  static showScores() {
    showPage(ControllerID.SCOREBOARD);
  }
}
```

## Избыточность

### В проекте не должно быть избыточных проверок
Например, если заранее известно, что функция всегда принимает числовой параметр, то не следует проверять его на существование

Неправильно:
```js
const isPositiveNumber = (myNumber) => {
  if (typeof myNumber === `undefined`) {
    throw new Error(`Parameter is not defined`);
  }
  return myNumber > 0;
};

isPositiveNumber(15);
isPositiveNumber(-30);
```

Правильно:
```js
const isPositiveNumber = (myNumber) => {
  return myNumber > 0;
};

isPositiveNumber(15);
isPositiveNumber(-30);
```

### Отсутствует дублирование кода: повторяющиеся части кода переписаны как функции или вынесены из условий
При написании кода следует придерживаться принципа [DRY](https://ru.wikipedia.org/wiki/Don%E2%80%99t_repeat_yourself)

Неправильно:
```js
if (this.level >= 10) {
  this.timer.stopTimer();
  this.timer.stopTimeout();
  this.setResult();
  removeTimer();
} else if (this.lives <= 0) {
  this.timer.stopTimer();
  this.timer.stopTimeout();
  app.showResultFail();
  removeTimer();
}
```

Правильно:
```js
this.timer.stopTimer();
this.timer.stopTimeout();

if (this.level >= 10) {
  this.setResult();
} else if (this.lives <= 0) {
  app.showResultFail();
}

removeTimer();
```

### Если при использовании условного оператора в любом случае возвращается значение, альтернативная ветка опускается
Неправильно:
```js
((val, anotherVal) => {
  if (2 > 1) {
    return val;
  } else {
    return anotherVal;
  }
});
```

Правильно:
```js
((val, anotherVal) => {
  if (2 > 1) {
    return val;
  }

  return anotherVal;
});
```

### Отсутствуют лишние приведения и проверки типов
Если заранее известно что в переменной число, то нет смысла превращать переменную в число `parseInt(myNumber)`. Тоже касается и избыточной проверки булевой переменной

Неправильно:
```js
if (booleanValue === true) {
  console.log(`It\`s true!`);
}
```

Правильно:
```js
if (booleanValue) {
  console.log(`It\`s true!`);
}
```

### Там где возможно, в присвоении значения вместо if используется тернарный оператор
Неправильно:
```js
let sex;
if (male) { 
  sex = `Мужчина`;
} else { 
  sex = `Женщина`;
}
```
Правильно:
```js
const sex = male ? `Мужчина` : `Женщина`;
```
 
### Условия упрощены
Если функция возвращает булево значение, не используется `if..else` с лишними `return`

Неправильно:
```js
((firstValue, secondValue) => {
  if (firstValue === secondValue) {
    return true;
  } else {
    return false;
  }
});
```
Правильно:
```js
((firstValue, secondValue) => {
  return firstValue === secondValue;
});
```


## Магия

### В коде не используются «магические значения», под каждое из них заведена отдельная переменная, названная как константа


## Оптимальность

### Использование шаблонной строки вместо конкатенации
Если требуется конкатенировать две переменные со строками внутри, то используется оператор конкатенации (`+`), вместо оператора шаблонной строки

Неправильно:
```js
const left = `Привет, `;
const right = `Вася`;

console.log(`${left}${right}`);
```

Правильно:
```js
const left = `Привет, `;
const right = `Вася`;

console.log(left + right);
```

### Константы, используемые внутри функций создаются вне функций и используются повторно через замыкания

### Массивы и объекты, содержимое которых вычисляется, собираются один раз, а после этого только переиспользуются


## Сложность. Читаемость.

### Для каждого события используется отдельный обработчик
Одна функция не является обработчиком нескольких разных событий

### Длинные функции и методы разбиты на несколько небольших

### Для работы с JS-коллекциями используются специальные методы
Итераторы используются для трансформаций массивов — `map`, `filter`, `sort` и прочие.

Например:
```js
elements.forEach((el) => {
  el.onclick = () => {
    console.log(el);
  };
});
```

### Оператор присваивания не используется как часть выражения <img src="https://eslint.org/img/logo.svg" width="24" alt="ESLint"/>
Неправильно:
```js
imgGenerate(picArray = JSON.parse(data));
```

Правильно:
```js
picArray = JSON.parse(data);
imgGenerate(picArray);
```

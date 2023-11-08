# Nuke App .eslintrc.js Breakdown

## Определение окружения

```
env: {
    browser: true, // код разрабатывается для браузера

    es2021: true // стандарт
},
```

## Расширение правил конфигурации

```
extends: [
    "standard-with-typescript", // базовые правила и настройки для TypeScript

    "plugin:react/recommended", // правила, специфичные для React

    "plugin:prettier/recommended", // интегрирует ESLint с Prettier

    "plugin:storybook/recommended" // конфигурация для работы с Storybook
```

[Правильное использование слоев](https://github.com/feature-sliced/eslint-config/tree/master/rules/layers-slices)

```
    "@feature-sliced/eslint-config/rules/layers-slices",
```

[Правильное использование public API](https://github.com/feature-sliced/eslint-config/tree/master/rules/public-api)

```
    // "@feature-sliced/eslint-config/rules/public-api",
],
```

## Переопределение правил

```

overrides: [],

```

## Какой парсер следует использовать

```

parser: "@typescript-eslint/parser",

```

## Параметры для линтера

```

settings: {

    "import/resolver": { // настройка разрешение импортов (import resolution) для TS

      typescript: {

        alwaysTryTypes: true // линтер всегда должен пытаться использовать типы (TypeScript declaration files) вместо фактических импортируемых файлов, если они доступны
      }
    },

    "react": {

      "version": "detect" // автоматически определять версию React
    }

},

```

## Параметры, связанные с парсером кода

```

parserOptions: {

    ecmaVersion: 'latest', // версия стандарта ECMAScript (JavaScript)

    sourceType: 'module', // использовать import и export

    project: 'tsconfig.json' // путь к файлу tsconfig.json,

},

```

## Плагины

```

plugins: ['react'],

```

## Правила проверки

Определение порядка и группы для импортов в файлах.

```

rules: {

"import/order":

```

Определение группы импортов. Они могут быть разделены на встроенные (встроенные модули Node.js), внешние (сторонние библиотеки), внутренние (модули проекта), родительские (импорты родительской директории) и соседние (импорты из той же директории).

```

["error", {

"groups": ["builtin", "external", "internal", "parent", "sibling"],

```

Настройка пути, которые должны быть сгруппированы вместе. Например, "react" группируется как внешний импорт и располагается перед другими внешними импортами.

```

"pathGroups": [{

     "pattern": "react", // паттерн для поиска импортов, включающих строку "react"

     "group": "external", // Когда импорты найдены, они группируются в категорию "external"

     "position": "before" // группа импортов будет располагаться перед другими группами.

},
{
pattern: '\*.css',

     group: 'index', //  создать группу с именем "index" для найденных импортов, которые соответствуют этому паттерну.

     patternOptions: {
       matchBase: true // паттерн должен сравниваться только с именем файла, а не с полным путем.
     },

     position: 'after' //  группа импортов будет располагаться после других групп.

},
{
pattern: '@/\*\*',

     group: 'external',

     position: 'after'

}],

```

Для группировки импортов с паттерном "react", эти импорты не будут исключены на основе их типов. Даже если импорты с паттерном "react" имеют разные типы, они все равно будут сгруппированы как внешние импорты и будут располагаться перед другими внешними импортами.

```

    "pathGroupsExcludedImportTypes": ["react"],

```

Между группами импортов не должно быть пустых строк. То есть, все группы следуют друг за другом без дополнительных отступов.

```

    "newlines-between": "never",

```

Сортировка импортов в алфавитном порядке.

```

    "alphabetize": {

      "order": "asc", //  в порядке возрастания (от A до Z).

      "caseInsensitive": true // сортировка регистронезависима
    }

}],

```

Проверка, что файлы не экспортируют что-либо по умолчанию

```

"import/no-default-export": "error",

```

Предупреждать о неиспользуемых переменных

```

"no-unused-vars": "off",

```

Аналогично для TS

```

"@typescript-eslint/no-unused-vars": "error",

```

Все определения типов в TypeScript должны быть согласованы и должны использовать одно ключевое слово type или interface .

```

"@typescript-eslint/consistent-type-definitions": "off",

```

Использование типа any в TS

```

"@typescript-eslint/no-explicit-any": "error",

```

Явное указание возвращаемого типа функций в TS

```

"@typescript-eslint/explicit-function-return-type": "off",

```

Импорт React в область видимости каждого JSX-элемента

```

"react/react-in-jsx-scope": "off",

```

Добавление пробела перед открывающей скобкой параметров функции

```

"@typescript-eslint/space-before-function-paren": "off",

```

_Перед использованием нужно отключить базовое правило_

```

module.exports = {
"rules": {
// Note: you must disable the base rule as it can report incorrect errors
"space-before-function-paren": "off",
"@typescript-eslint/space-before-function-paren": "error"
}
};

```

Включить/выключить `Record<>`

```

"@typescript-eslint/consistent-indexed-object-style": "off",

```

Использование тройных слэш-ссылок (///) для директив `/// <reference path="..." />`,

```

"@typescript-eslint/triple-slash-reference": "off",

```

Использование типа void вне generic или возвращаемых типов

```

"@typescript-eslint/no-invalid-void-type": "off",

```

Проверка логических выражений,

```

"@typescript-eslint/strict-boolean-expressions": "off",

```

Проверка правильного использования промисов (внутри `if`)

```

"@typescript-eslint/no-misused-promises": "off",

```

Проверка единообразного использования утверждений типов (`as Type` или `<Type>`)

```

"@typescript-eslint/consistent-type-assertions": "off",

```

Запрет на использование определенных типов

```

"@typescript-eslint/ban-types": "off",

```

Предупреждение об отсутствии обработки ошибок в асинхронных функциях (пустые `catch/finally`)

```

"@typescript-eslint/no-floating-promises": "off",

```

[Проверка использования типа `void`](https://typescript-eslint.io/rules/no-confusing-void-expression)

```

"@typescript-eslint/no-confusing-void-expression": "off",

```

Запретить использование delete по динамическому ключу `delete container[name];`

```

"@typescript-eslint/no-dynamic-delete": "off",

```

Проверка, что любая функция, возвращающая промис имеет прописанный `async`

```

"@typescript-eslint/promise-function-async": "off",

```

См. выше

```

// feature-sliced/layers-slices

```

Проверка импортов между типами элементов на основе указанных правил

```

"boundaries/element-types": "error",

```

См. выше

```

// feature-sliced/public-api

```

Предотвращение импортирования подмодулей других модулей `import { settings } from './app/index'; ` vs `import { settings } from '../app';`

```

// "import/no-internal-modules": "warn" // ~ 1,

```

Запрещает импорт модулей из определенного пути (`@/shared/lib/server`) и сообщает об ошибке, если происходит такой импорт.

```

// disallow import @/shared/lib/server

"no-restricted-imports": ["error", {
"paths": [{
"name": "@/shared/lib/server",
"message": "Not allowed use server modules in client"
}],
}]
},

```

## Cпецифические правила для определенных файлов или категорий файлов

```

"overrides": [
{
"files": ["*.stories.tsx"], // правила применяются только к файлам с расширением .stories.tsx

    "rules": {
      "import/no-default-export": "off", // запрещает использование экспорта по умолчанию в файлах.

      "no-restricted-imports": "off", // отключает правило ограничения импортов
    }

},
{
"files": ["**/__mocks__/**/*.ts"], // аналогично

    "rules": {
      "no-restricted-imports": "off",
    }

}
]

```

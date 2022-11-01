### Вам предстоит сделать поисковик, в котором можно искать репозитории в GitHub по их названию. Допишите код в файл `task.js`, чтобы при нажатии на кнопку «Найти» отправлялся запрос на `https://api.nomoreparties.co/github-search?q=` и текст поиска, который пользователь ввёл в форму. Например, запрос https://api.nomoreparties.co/github-search?q=typescript возвращает объект вида:

```
{
    total_count: 325299
    incomplete_results: false
    items: [
        {
            id: 20929025,
            name: "TypeScript",
            full_name: "microsoft/TypeScript",
            html_url: "https://github.com/microsoft/TypeScript",
            description: "TypeScript is a superset of JavaScript that compiles to clean JavaScript output.",
            stargazers_count: 79871,
            language: "TypeScript",
            ...
        },
        ...
    ]
} 
```

### Запрос должен отправляться по событию `submit` на форме. Используйте для решения задачи `fetch().then().catch()` конструкцию. Для успешного решения задачи необходимо выполнить следующие действия:

 - Перед отправкой запроса нужно вызывать функцию `onSubmitStart()`. Эта вспомогательная функция нужна для «оживления» интерфейса.
 - Функцию `renderCount(total_count)` следует вызывать только при наличии результатов поиска. Вместе с ней нужно добавить в `resultsContainer` найденные репозитории, вызвав для каждого из них функцию `template(item)`. Обратите внимание, функция `renderCount` принимает аргумент из ответа сервера: `total_count`.
 - Функцию `renderEmptyResults()` нужно вызывать только при отсутствии результатов по запрошенному названию, то есть когда `total_count` равен нулю.
- На случай ошибки, произошедшей на стороне сервера или же внутри клиентского кода, — вызывайте функцию `renderError()`. Вызов этой функции добавит пользовательскому интерфейсу информативности.

## Подсказка
Задачу можно решить несколькими способами. Для отрисовки результатов поиска пригодятся конструкции `for..of` или методы массивов. Так же, стоит обратить внимание на событие `submit`, по умолчанию страница будет перезагружаться, от такого поведения следует избавиться. Не забывайте, что `fetch`, который следует использовать для запроса, — асинхронный
# Консоль кода для 1С 8.3 (Управляемые и обычные формы)

Для работы внутри 1С требуется версия платформы не ниже **8.3.14.1565** 

![](https://github.com/salexdv/git_images/blob/master/bslconsole_view.png?raw=true)

## Как работает?
На основе [Monaco editor](https://github.com/Microsoft/monaco-editor)

## Основные возможности:
* Подсветка синтаксиса языка 1С
* Подсветка языка запросов
* Автокомплит для глобальных перечислений и функций
* Автокомплит для метаданных (Справочники, Документы и т.п.)
* Автокомплит для объектов метаданных (СправочникСсылка, ДокументОбъект и т.п.)
* Подсказка параметров конструкторов и методов
* Подсказка для типов
* Вставка готовых блоков кода (сниппеты)
* Вызов конструктора запроса и конструктора форматной строки
* Загрузка пользовательских функций и сниппетов
* Выделение строки, при выполнении которой произошла ошибка
* Сворачивание циклов, условий и текстов запросов
* Всплывающие подсказки для глобальных функций, перечислений и классов
* Подсказки через точку для реквизитов типа справочники/документы
* Подсказки через точку для объектов типа ТаблицаЗначений/Массив/РезультатЗапроса/ДвоичныеДанные и др., в том числе для объектов, полученных через методы других объектов.
* Подсказки для источников и полей в режиме запроса

## Как запускать?
1. Для запуска в браузере достаточно открыть **index.html** из каталога **src**, либо воспользоваться [ссылкой](https://salexdv.github.io/bsl_console/src/index.html)
2. Для запуска в 1С можно использовать обработку **console.epf**, выкладываемую в [релизах](https://github.com/salexdv/bsl_console/releases) или сделать свою.
3. Редактор используется на сайте [Paste1C](https://paste1c.ru/).

## Функции для взаимодействия с 1С:Предприятием

### Работа с текстом (кодом)
| Функция                        | Описание                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| `setText`                      | Устанавливает переданный текст в текущую или определенную позицию                             |
| `updateText`                   | Полностью заменяет весь текст редактора, игнорируя при этом режим *Только просмотр*           |
| `getText`                      | Возвращает весь текст из окна редактора                                                       |
| `eraseText`                    | Удаляет весь текст редактора                                                                  |
| `selectedText(text)`           | функция без параметров возвращает выделенный текст, с параметром - устанавливает              |
| `getSelection`                 | возвращает [selection](https://microsoft.github.io/monaco-editor/api/classes/monaco.selection.html), аналог GetTextSelectionBounds|
| `setSelectionByLength`         | устанавливает выделение, аналог первой сигнатуры SetTextSelectionBounds                       |
| `setSelection`                 | устанавливает выделение, аналог второй сигнатуры SetTextSelectionBounds                       |
| `getLineCount`                 | возвращает количество строк                                                                   |
| `getLineContent`               | возвращает содержимое строки по её номеру, аналог GetLine                                     |
| `setLineContent`               | устанавливает содержимое строки по её номеру, аналог ReplaceLine                              |
| `getQuery`                     | Определяет текст запроса в текущей позиции и возвращает его вместе с областью текста          |
| `getFormatString`              | Определяет текст форматной строки в текущей позиции                                           |
| `findText`                     | Возвращает номер строки, в которой находится заданный текст                                   |
| `addComment`                   | Добавляет комментарий к текущему блоку кода                                                   |
| `removeComment`                | Удаляет комментарий у текущего блока                                                          |

### Управление режимом работы / настройками
| Функция                        | Описание                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| `init`                         | Инициализация редактора с передачей версии платформы                                          |
| `setTheme`                     | Установка темы редактора `bsl-white`, `bsl-white-query`, `bsl-dark`, `bsl-dark-query`         |
| `setReadOnly`                  | Устанавливает/снимает режим *Только просмотр*                                                 |
| `switchLang`                   | Переключает язык подсказок с английского на русский и обратно                                 |
| `enableQuickSuggestions`       | Включает/выключает режим быстрых подсказок                                                    |
| `minimap`  				     | Включает/выключает отображение карты кода                                                     |
| [`enableModificationEvent`](docs/modification_event.md) | Включает/выключает генерацию события, возникающего при изменении содержимого редактора|
| [`switchQueryMode`](docs/switch_query.md) | Переключение между режимом запроса и режимом редактирования кода                        |
| [`compare`](docs/compare.md) 	 | Включает/выключает режим сравнения текстов 						                             |
| `getVarsNames`	     	 	 | Возвращает имена всех объявленных в коде переменных                     				         |

### Взаимодействие
| Функция                        | Описание                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| `updateMetadata`               | Обновляет через JSON структуру метаданных (Справочники/Документы/пр.)                         |
| `updateSnippets`               | Обновляет пользовательские сниппеты                                                           |
| `updateCustomFunctions`        | Обновляет пользовательские функции                                                            |
| `setCustomHovers `        	 | Обновляет пользовательские подсказки                                                          |
| [`addContextMenuItem`](docs/add_menu.md) | Регистрирует пользовательский пункт контекстного меню и связанное с ним событие     |
| `markError`                    | Индикация ошибки в указанной строке                                                           |
| [`triggerSuggestions`](docs/trigger_suggestions.md) | Принудительный вызов подсказок											 |

## События, генерируемые редактором для 1С:Предприятия
| Событие                        | Описание                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| `EVENT_QUERY_CONSTRUCT`        | При выборе пункта меню "Конструктор запросов". Возвращает текст и позицию запроса             |
| `EVENT_FORMAT_CONSTRUCT`       | При выборе пункта меню "Конструктор форматной строки". Возвращает текст и позицию фор.строки  |
| `EVENT_CONTENT_CHANGED`        | При любом изменении содержимого редактора. Вкл/откл через *enableModificationEvent*           |
| `EVENT_GET_METADATA`       	 | Генерируется при отсутствии метаданных. В параметрах передается имя запрашиваемых метаданных  |
| `EVENT_XXX`                    | При выборе пользовательского пункта меню. *addContextMenuItem('Мой пункт', 'EVENT_MY')*       |

*Перед началом работы с редактором из 1С Предпрития желательно вызвать функцию инициализации и передать в нее текущую версию платформы.*
Пример:
```javascript
init('8.3.18.891');
```

## Продукты, использующие консоль:
* [Infostart Toolkit](https://infostart.ru/journal/news/news/infostart-toolkit-1-3-teper-s-novym-redaktorom-koda-na-baze-monaco-editor_1303095/)
* [Конвертация данных 3 расширение](https://infostart.ru/public/1289837/)
* [Контекстная подсказка в 1С КД3](https://github.com/GenVP/TipsInCD3)

## Проверенные платформы:
* 8.3.15.1830
* 8.3.16.1148
* 8.3.17.1386
* 8.3.18.891

## Известные проблемы:
* На платформах до 8.3.16 могут не работать горячие клавиши CTRL+C, CTRL+V и CTRL+Z и т.п.
* На платформах до 8.3.18 команды копировать/вставить работают только в пределах окна редактора
* В веб-клиенте недоступно любое взаимодействие редактора и 1С. Можно попробовать только набор кода. Иногда для этого в браузере надо предварительно открыть данную [ссылку](https://salexdv.github.io/bsl_console/src/index.html)
* Работа в linux на данный момент не поддерживается.
* Из-за особенностей реализации подсказка через точку для реквизитов ссылочного типа работает только тогда, когда подсказываемый реквизит выбран через Enter

## Благодарности
Выражаю благодарность команде [1c-syntax](https://github.com/1c-syntax) и их [проекту для VSCode](https://github.com/1c-syntax/vsc-language-1c-bsl) за подробное описание внутренних конструкций языка в JSON, а также за коллекцию сниппетов.
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

## Публикации
* [На Инфостарте](https://infostart.ru/public/1266087/)

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
| `setContent`                   | Устанавливает текст редактора. Игнорирует режим *Только просмотр* и не генерирует событие `EVENT_CONTENT_CHANGED`|
| `getText`                      | Возвращает весь текст из окна редактора                                                       |
| `eraseText`                    | Удаляет весь текст редактора                                                                  |
| [`selectedText`](docs/selected_text.md) | Получает или заменяет выделенный текст              								 |
| `getSelection`                 | Возвращает [selection](https://microsoft.github.io/monaco-editor/api/classes/monaco.selection.html), аналог GetTextSelectionBounds|
| `setSelectionByLength`         | Устанавливает выделение, аналог первой сигнатуры SetTextSelectionBounds                       |
| `setSelection`                 | Устанавливает выделение, аналог второй сигнатуры SetTextSelectionBounds                       |
| `getLineCount`                 | Возвращает количество строк                                                                   |
| `getLineContent`               | Возвращает содержимое строки по её номеру, аналог GetLine                                     |
| `setLineContent`               | Устанавливает содержимое строки по её номеру, аналог ReplaceLine                              |
| `getCurrentLineContent`        | Возвращает содержимое текущей строки                                                          |
| `getCurrentLine`               | Возвращает номер текущей строки                                                               |
| `getCurrentColumn`             | Возвращает номер текущей колонки               							                     |
| `getQuery`                     | Определяет текст запроса в текущей позиции и возвращает его вместе с областью текста          |
| `getFormatString`              | Определяет текст форматной строки в текущей позиции                                           |
| `findText`                     | Возвращает номер строки, в которой находится заданный текст                                   |
| `addComment`                   | Добавляет комментарий к текущему блоку кода                                                   |
| `removeComment`                | Удаляет комментарий у текущего блока                                                          |
| `addWordWrap`                  | Добавляет перенос строки к текущему блоку 	                                                 |
| `removeWordWrap`               | Удаляет перенос строки у текущего блока                                                       |
| [`insertLine`](docs/insert_line.md) | Вставляет текст в строку с указанным номером                                             |
| [`addLine`](docs/add_line.md)  | Добавляет новую строку с указанным текстом                                                    |
| [`getPositionOffset`](docs/get_position_offset.md) | Возвращает координаты текущей позиции курсора				             |
| `jumpToBracket`                | Переход к парной скобке `CTRL+[]`	                                                         |
| `selectToBracket`              | Выделяет скобки и текст между ними `SHIFT+ALT+B`	                                             |
| `formatDocument`               | Форматирование выделенного фрагмента кода или всего кода `ALT+SHIFT+F`	                     |

### Управление режимом работы / настройками
| Функция                        | Описание                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| `init`                         | Инициализация редактора с передачей версии платформы                                          |
| `setTheme`                     | Установка темы редактора `bsl-white`, `bsl-white-query`, `bsl-dark`, `bsl-dark-query`         |
| `setReadOnly`                  | Устанавливает/снимает режим *Только просмотр*                                                 |
| `getReadOnly`                  | Возвращает значение режима *Только просмотр*                                                  |
| `switchLang`                   | Переключает язык подсказок с английского на русский и обратно                                 |
| `enableQuickSuggestions`       | Включает/выключает режим быстрых подсказок                                                    |
| `minimap`  				     | Включает/выключает отображение карты кода                                                     |
| [`enableModificationEvent`](docs/modification_event.md) | Включает/выключает генерацию события, возникающего при изменении содержимого редактора|
| [`enableSuggestActivationEvent`](docs/activation_event.md) | Включает/выключает генерацию события, возникающего активации пункта в списке подсказок|
| [`enableBeforeShowSuggestEvent`](docs/before_suggest_event.md) | Включает/выключает генерацию события, возникающего перед появлением списка подсказок|
| [`enableSelectSuggestEvent`](docs/select_suggest_event.md) | Включает/выключает генерацию события, возникающего при выборе пункта из списка подсказок|
| [`enableBeforeHoverEvent`](docs/before_hover_event.md) | Включает/выключает генерацию события, возникающего перед появлением всплывающей подсказки для слова|
| [`enableBeforeSignatureEvent`](docs/before_signature_event.md) | Включает/выключает генерацию события, возникающего перед появлением подсказки по вызову процедуры/метода|
| [`switchQueryMode`](docs/switch_query.md) | Переключение между режимом запроса и режимом редактирования кода                   |
| [`compare`](docs/compare.md) 	 | Включает/выключает режим сравнения текстов 						                             |
| `nextDiff`				 	 | Переход с следующему изменению в режиме сравнения											 |
| `previousDiff`			 	 | Переход с предыдущему изменению в режиме сравнения											 |
| `getVarsNames`	     	 	 | Возвращает имена всех объявленных в коде переменных                     				         |
| `switchXMLMode`	     	 	 | Переключение в режим просмотра XML с подсветкой и обратно               				         |
| `disableContextMenu`	     	 | Отключает показ контекстного меню 						              				         |
| `hideLineNumbers`	     	 	 | Скрывает отображение номеров строк в редакторе 			              				         |
| `hideScrollX`	     	 	 	 | Скрывает стандартную горизонтальную полосу прокрутки           				         		 |
| `hideScrollY`	     	 	 	 | Скрывает стандартную вертикальную полосу прокрутки               				         	 |
| `openSearchWidget`	 	 	 | Открывает окно поиска 								               				         	 |
| `closeSearchWidget`	 	 	 | Закрывает окно поиска 								               				         	 |
| `nextMatch`	 	 	 		 | Переход к следующему совпадению в поиске				               				         	 |
| `previousMatch`	 	 	 	 | Переход к предыдущему совпадению в поиске		                				         	 |
| `setFontSize`	 	 			 | Установка размера шрифта 							               				         	 |
| `setFontFamily`		 	 	 | Установка семейства шрифтов 							               				         	 |
| `setFontWeight`		 	 	 | Установка насыщенности (толщины) шрифта 				               				         	 |
| `setLineHeight`		 	 	 | Установка высоты строки 				               				                           	 |
| `showStatusBar`		 	 	 | Включает отображение строки состояния в нижней части редактора     				         	 |
| `hideStatusBar`		 	 	 | Отключает отображение строки состояния						     				         	 |
| [`renderWhitespace`](docs/whitespaces.md) | Включает/отключает отображение пробелов и табуляций			     				 |
| `hasTextFocus`		 	 	 | Возвращает признак активности фокуса						    	 				         	 |
| [`setOption`](docs/set_option.md) | Установка опциональных настроек редактора				    	 				         	 |
| `getOption`		 		 	 | Получение опциональных настроек редактора				    	 				         	 |
| [`disableKeyBinding`](docs/disable_key_binding.md) | Отключает любое стандартное сочетание клавиш редактора		         	 |
| [`enableKeyBinding`](docs/disable_key_binding.md) | Включает обратно сочетание		                                      	 |
| `saveViewState`		 	 	 | Возвращает JSON-строку с текущими настройками (положение курсора и прокрутки, а также свернутые блоки) |
| `restoreViewState`		  	 | Восстанавливает настройки. В качестве аргумента принимает JSON-строку, полученну ранее через `saveViewState` |
| [`setOriginalText`](docs/set_original_text.md) | Устанавливает или сбрасывает оригинальный текст, на основании которого строится подсветка изменений |


### Взаимодействие
| Функция                        | Описание                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| `updateMetadata`               | Обновляет через JSON структуру метаданных (Справочники/Документы/пр.)                         |
| `clearMetadata`                | Очищает структуру метаданных                                                                  |
| `updateSnippets`               | Обновляет пользовательские сниппеты                                                           |
| `updateCustomFunctions`        | Обновляет пользовательские функции                                                            |
| [`setCustomHovers`](docs/set_custom_hovers.md) | Обновляет пользовательские подсказки, показываемые при наведении              |
| [`setCustomSignatures`](docs/set_custom_signatures.md) | Обновляет пользовательские подсказки по вызову процедуры/метода       |
| [`addContextMenuItem`](docs/add_menu.md) | Регистрирует пользовательский пункт контекстного меню и связанное с ним событие     |
| `markError`                    | Индикация ошибки в указанной строке                                                           |
| [`triggerSuggestions`](docs/trigger_suggestions.md) | Принудительный вызов подсказок											 |
| [`triggerHovers`](docs/trigger_hovers.md) | Принудительный вызов всплывающей подсказки для текущего слов              	     |
| [`triggerSigHelp`](docs/trigger_signature_help.md) | Принудительный вызов подсказки по вызову процедуры/метода          	     |
| [`showCustomSuggestions`](docs/custom_suggestions.md) | Показ пользовательских подсказок									 	 |
| `showPreviousCustomSuggestions`| Вывод списка пользовательских подсказок, ранее показанных через `showCustomSuggestions`	 	 |
| `hideSuggestionsList` 		 | Скрывает текущий список подсказок									 	 					 |
| `hideHoverList` 		 		 | Скрывает активную всплывающую подсказку для слова					 	 					 |
| `hideSignatureList` 		 	 | Скрывает активную всплывающую подсказку по вызову процедуры/метода	 	 					 |
| `addBookmark` 		 	 	 | Создание закладки в строке с указанным номером						 	 					 |
| `removeBookmark` 		 	 	 | Удаление закладки из строки с указанным номером						 	 					 |
| `goNextBookmark` 		 	 	 | Переход к следующей закладке											 	 					 |
| `goPreviousBookmark` 		 	 | Переход к предыдущей закладке										 	 					 |
| `getBookmarks` 		 	 	 | Возвращает массив с номерами строк, в которых установлены закладки	 	 					 |
| `removeAllBookmarks`	 	 	 | Удаляет все закладки	 	 																	 |
| `setActiveSuggestLabel` 		 | Устанавливает заголовок активного пункта списка подсказок			 	 					 |
| `setActiveSuggestDetail` 		 | Устанавливает подробное описание активного пункта списка подсказок	 	 					 |
| `revealLineInCenter` 			 | Переход к строке по её номеру и позиционирование по центру экрана	 	 					 |

## События, генерируемые редактором для 1С:Предприятия
| Событие                        | Описание                                                                                      |
| ------------------------------ | --------------------------------------------------------------------------------------------- |
| `EVENT_QUERY_CONSTRUCT`        | При выборе пункта меню "Конструктор запросов". Возвращает текст и позицию запроса             |
| `EVENT_FORMAT_CONSTRUCT`       | При выборе пункта меню "Конструктор форматной строки". Возвращает текст и позицию фор.строки  |
| `EVENT_CONTENT_CHANGED`        | При любом изменении содержимого редактора. Вкл/откл через *enableModificationEvent*           |
| `EVENT_GET_METADATA`       	 | Генерируется при отсутствии метаданных. В параметрах передается имя запрашиваемых метаданных  |
| `EVENT_XXX`                    | При выборе пользовательского пункта меню. *addContextMenuItem('Мой пункт', 'EVENT_MY')*       |
| `EVENT_ON_ACTIVATE_SUGGEST_ROW`| При активации пункта в текущем списке подсказок [(подробнее)](docs/activation_event.md)		 |
| `EVENT_ON_DETAIL_SUGGEST_ROW`  | При активации подробного описания пункта в текущем списке подсказок [(подробнее)](docs/activation_event.md) |
| `EVENT_ON_SELECT_SUGGEST_ROW`	 | При выборе пункта из списка подсказок [(подробнее)](docs/select_suggest_event.md)			 |
| `EVENT_BEFORE_SHOW_SUGGEST`	 | Перед появлением списка подсказок [(подробнее)](docs/before_suggest_event.md)		  		 |
| `EVENT_BEFORE_HOVER`	 		 | Перед появлением всплывающей подсказки для слова [(подробнее)](docs/before_hover_event.md)    |
| `EVENT_BEFORE_SIGNATURE`		 | Перед появлением всплывающей подсказки по вызову процедуры/метода [(подробнее)](docs/before_signature_event.md) |
| `EVENT_ON_LINK_CLICK`		 	 | При клике по гиперссылке																		 |
| `EVENT_KEY_BINDING_ХХХ`		 | При нажатии отключенного сочетания клавиш [(подробнее)](docs/disable_key_binding.md) 	     |

*Перед началом работы с редактором из 1С Предпрития желательно вызвать функцию инициализации и передать в нее текущую версию платформы.*
Пример:
```javascript
init('8.3.18.891');
```

## Горячие клавиши
Все горячие клавиши описаны [тут](docs/shortcuts.md)

## Особенности
* По умолчанию редактор не подстраивается под размеры окна. Это не ошибка, решение описано [тут](https://github.com/salexdv/bsl_console/issues/27) и [тут](https://github.com/salexdv/bsl_console/issues/80)

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
* На платформах, выпущенных примерно до ноября 2020 года могут не работать горячие клавиши CTRL+SPACE, CTRL+C, CTRL+V и CTRL+Z и т.п.
* В веб-клиенте недоступно любое взаимодействие редактора и 1С. Можно попробовать только набор кода. Иногда для этого в браузере надо предварительно открыть данную [ссылку](https://salexdv.github.io/bsl_console/src/index.html)
* В linux пока возможны проблемы с некоторым функционалом. Для сборки под linux необходимо использовать ветку [webpack](https://github.com/salexdv/bsl_console/tree/webpack)
* Из-за особенностей реализации подсказка через точку для реквизитов ссылочного типа работает только тогда, когда подсказываемый реквизит выбран через Enter

## Благодарности
Выражаю благодарность команде [1c-syntax](https://github.com/1c-syntax) и их [проекту для VSCode](https://github.com/1c-syntax/vsc-language-1c-bsl) за подробное описание внутренних конструкций языка в JSON, а также за коллекцию сниппетов.
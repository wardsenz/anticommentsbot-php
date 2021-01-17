# anticommentsbot-php

#### Комментируешь? Будь добр вступить в чат.
Именно этим и занимается этот бот.
Удаляет комменты от пользователей которых нет в вашем чате и просит их присоединиться к вам.

### Создание нового бота
> Подробная инструкция описана [тут](https://core.telegram.org/bots#creating-a-new-bot)

Перейдите в диалог с [@BotFather](https://t.me/BotFather)
1. Пишем ему `/start` и получаем список всех его команд.
Первая и главная — `/newbot` — отправляем ему и бот просит придумать имя  и короткий юзернейм нашему новому боту. Единственное ограничение на юзернейм — оно должно оканчиваться на «bot». В случае успеха BotFather вернет токен бота. Он и нам нужен. 
2. Добавляем бота в нужную нам группу (супергруппу) и отправляем BotFather следующие команды: 
`/setjoingroups`  - `Disable`
`/setprivacy` - `Disable`
Это отключит возможность другим (и вам тоже) добавлять его в другие группы (`/setjoingroups`) и даст доступ ко всем сообщениям (`/setprivacy`)
Боты по умолчанию видят только сообщения с командами (с / в начале)

> Бот возможно попросит выбрать, к какому боту нужно изменить настройки. Выбирайте последний созданный.

### Конфиг
В конфиг-файле есть несколько переменных, которые нужно настроить и можно отредактировать.

1. #### `$BotToken`
- Тот самый токен бота.

2. #### `$ChatId`
- Идентификатор нужной нам группы. Самый простой способ узнать его - добавить [этого](https://t.me/MissRose_bot) бота в группу и написать `/id`. Бот вернет айди группы.

3. #### `$AdminId`
- Идентификатор владельца или админа бота. Узнать свой айди можно всё так же у бота Miss Rose, написав ей в личные сообщения `/id`.
Админу доступна дополнительная команда `/config` для проверки работоспособности и состояния бота.
4. #### `$HookSecret`
-  Секретный ключ для доступа к обработчику. Защитит от поддельных запросов, если кто-нибудь узнает адрес хука. Можно свою фразу, но лучше воспользоваться [рандомайзером](https://onlinerandomtools.com/generate-random-string)


Это самое важное, что нужно менять в конфиге. Остальное трогать не рекомендую, если не понимаете что оно и как оно работает.

После изменений должно получиться что-то вроде этого:

* `private $BotToken = "12345678:ABCDE";`
* `private $ChatId = "-10012345678";`
* `public $AdminId = "0987654";`
* `private $HookSecret = "h73nf10dg";`

### Установка вебхука
> [Документация по установке вебхука](https://core.telegram.org/bots/api#setwebhook)

Раз уж с конфигом разобрались, теперь нужно указать Bot API, куда телеграму нужно отправлять новые сообщения (события)

1. Соберите ссылку как тут:
`https://api.telegram.org/botТОКЕН/setWebhook?url=ССЫЛКА?hook_secret=КЛЮЧ`
Где - 
* **ТОКЕН** - наш токен
* **ССЫЛКА** - полный путь до файла hook.php на вашем сайте/сервере
*  **КЛЮЧ** - тот самый секретный `$HookSecret`

    То есть получится примерно следующее:
`https://api.telegram.org/bot1235678:ABCDE/setWebhook?url=https://example.com/mybot/hook.php?hook_secret=h73nf10dg`
2. Перейдите по собранному адресу в браузере или отправьте запрос с помощью **curl**:
`$ curl -s "https://api.telegram.org/bot1235678:ABCDE/setWebhook?url=https://example.com/mybot/hook.php?hook_secret=h73nf10dg"`
Телеграм вернет ответ в формате JSON, где сообщит об успехе или ошибке. 
`Webhook was set` - успех.

На этом всё. 
Напишите в чат или лс бота `/ping`, чтобы удостовериться что он исправно работает.

#### Помощь и вопросы

* Открывайте issue или свяжитесь с автором в [телеграме](https://t.me/hydrugz)


> Написано с помощью [StackEdit](https://stackedit.io/).

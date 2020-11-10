<img src="https://github.com/ICQ-BOTS/mailru_im_async_bot/blob/main/logo.png" width="100" height="100">

# Mailru im async bot
 
Асинхронная библиотека Python для BOT API

# Оглавление 
 - [Установка](#)
 - [Api](#)
 - [Настройка](#)
 - [БД Tarantool](#)
 - [Class Bot](#)
 - [Class hendler](#)
 - [Class Filter](#)
 
# Установка 

```bash
git clone https://github.com/ISQ-BOTS/mailru_im_async_bot.git
cd mailru_im_async_bot
python setup.py install
```

# API
<ul>
    <li><a href="https://icq.com/botapi/">icq.com/botapi/</a></li>
    <li><a href="https://agent.mail.ru/botapi/">agent.mail.ru/botapi/</a></li>
</ul>


# Настройка

Для запуска боту необходимы конфиги logging.ini и config.ini



# БД Tarantool
Установка базы данных - [тут](https://www.tarantool.io/ru/download/os-installation/ubuntu/)
Руководство для начинающих - [тут](https://www.tarantool.io/ru/doc/latest/getting_started/getting_started_db/#using-a-binary-package)

# Class Bot
## self 
### /self/get
Получить информацию о боте
```python
await self_get()
```
## messages
### /messages/sendText
Отправить текстовое сообщение
```python
await send_text(chat_id, text, reply_msg_id=None, forward_chat_id=None, forward_msg_id=None,
                        inline_keyboard_markup=None)
```

Параматеры:
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* text (str) - Текст сообщения. Можно упомянуть пользователя, добавив в текст его userId в следующем формате @[userId].
* reply_msg_id (str, list) - Id цитируемого сообщения. Не может быть передано одновременно с параметрами forwardChatId и forwardMsgId.
* forward_chat_id (str) - Id чата, из которого будет переслано сообщение. Передается только с forwardMsgId. Не может быть передано с параметром replyMsgId.
* forward_msg_id (str, list) - Id пересылаемого сообщения. Передается только с forwardChatId. Не может быть передано с параметром replyMsgId.
* inline_keyboard_markup (list) - Это лист словарей с описанием кнопок.
```python
import json
await bot.send_text(
        chat_id=event.message_author['userId'],
        text="Hello with buttons.",
        inline_keyboard_markup="[{}]".format(json.dumps([[
            {"text": "🌎 Visit website", "url": "http://mail.ru", "style": "attention"},
            {"text": "🤖 Make a query", "callbackData": "RXhhbXBsZSBjYWxsYmFjayBkYXRhCg==", "style": "primary"}
        ]]))
    )
```

### /messages/sendFile
Отправить файл
```python
await send_file(chat_id, file_id=None, file=None, caption=None, reply_msg_id=None, forward_chat_id=None,forward_msg_id=None, inline_keyboard_markup=None)
```
Параматеры:
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* file_id (str) - Id ранее загруженного файла.
* file (obj) - Файл, не может быть передан с file_id
```python
with open(path, 'rb') as file:
        await bot.send_file(
            chat_id=chat_id, 
            file=file
        )
```
* caption (str) - Подпись к файлу.
* reply_msg_id (str, list) - Id цитируемого сообщения. Не может быть передано одновременно с параметрами forwardChatId и forwardMsgId.
* forward_chat_id (str) - Id чата, из которого будет переслано сообщение. Передается только с forwardMsgId. Не может быть передано с параметром replyMsgId.
* forward_msg_id (str, list) - Id пересылаемого сообщения. Передается только с forwardChatId. Не может быть передано с параметром replyMsgId.
* inline_keyboard_markup (list) - Это лист словарей с описанием кнопок.
```python
import json
await bot.send_file(
            chat_id=chat_id, 
            file=file, 
            inline_keyboard_markup="[{}]".format(json.dumps([[
                {"text": "🌎 Visit website", "url": "http://mail.ru", "style": "attention"},
                {"text": "🤖 Make a query", "callbackData": "RXhhbXBsZSBjYWxsYmFjayBkYXRhCg==", "style": "primary"}
            ]]))
        )
```
### /messages/sendVoice
Загрузить и отправить новое голосовое сообщение
```python
await send_voice(chat_id, file_id=None, file=None, reply_msg_id=None, forward_chat_id=None,orward_msg_id=None, inline_keyboard_markup=None)
```
Параматеры:
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* file_id (str) - Id ранее загруженного файла.
* file (obj) - Файл, не может быть передан с file_id
```python
with open(path, 'rb') as file:
        await bot.send_file(
            chat_id=chat_id, 
            file=file
        )
```
* reply_msg_id (str, list) - Id цитируемого сообщения. Не может быть передано одновременно с параметрами forwardChatId и forwardMsgId.
* forward_chat_id (str) - Id чата, из которого будет переслано сообщение. Передается только с forwardMsgId. Не может быть передано с параметром replyMsgId.
* forward_msg_id (str, list) - Id пересылаемого сообщения. Передается только с forwardChatId. Не может быть передано с параметром replyMsgId.
* inline_keyboard_markup (list) - Это лист словарей с описанием кнопок.
```python
import json
await bot.send_file(
            chat_id=chat_id, 
            file=file, 
            inline_keyboard_markup="[{}]".format(json.dumps([[
                {"text": "🌎 Visit website", "url": "http://mail.ru", "style": "attention"},
                {"text": "🤖 Make a query", "callbackData": "RXhhbXBsZSBjYWxsYmFjayBkYXRhCg==", "style": "primary"}
            ]]))
        )
```

### /messages/editText
Редактировать текстовое сообщение
```python
await edit_text(chat_id, msg_id, text, inline_keyboard_markup=None)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* msg_id (str) - Id сообщения.
* text (str) - Текст сообщения. Можно упомянуть пользователя, добавив в текст его userId в следующем формате @[userId].
* inline_keyboard_markup (list) - Это лист словарей с описанием кнопок.
```python
import json
await bot.edit_text(
        chat_id=event.message_author['userId'],
        msg_id=msg_id,
        text="New button",
        inline_keyboard_markup="[{}]".format(json.dumps([[
            {"text": "🌎 Visit website", "url": "http://mail.ru", "style": "attention"},
            {"text": "🤖 Make a query", "callbackData": "RXhhbXBsZSBjYWxsYmFjayBkYXRhCg==", "style": "primary"}
        ]]))
    )
```
### /messages/deleteMessages
Удалить сообщение
На удаление наложены следующие ограничения:
1. Сообщение может быть удалено только если оно было отправлено менее 48 часов назад;
2. Бот может удалить исходящие сообщения в приватных чатах и группах;
3. Бот может удалить любое сообщение в группе, если он является администратором.

```python
await delete_messages(chat_id, msg_id)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* msg_id (str) - Id сообщения.

### /messages/answerCallbackQuery
Ответ на запрос обработки нажатия кнопки
```python
await answer_callback_query(query_id, text=None, show_alert=False, url=None)
```
queryId (str) - Идентификатор callback query полученного ботом
text (str) - Текст нотификации, который будет отображен пользователю. В случае, если текст не задан – ничего не будет отображено.
show_alert (boolean) - Если выставить значение в true, вместо нотификации будет показан alert
url (str) - URL, который будет открыт клиентским приложением
```python
await bot.answer_callback_query(query_id=event.data['queryId'], url='mail.ru')
```

## chats
### /chats/members/delete
Удалить пользователей из чата
```python
await delete_chat_members(chat_id, members)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* members (list) - Список пользователей

### /chats/avatar/set
Установка аватара чата
```python
await set_avatar_chat(chat_id, file)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* file - Файл
```python
with open(path, 'rb') as file:
        await bot.set_avatar_chat(
            chat_id=chat_id, 
            file=file
        )
```

### /chats/sendActions
Отправить действия в чат
```python
await send_actions(chat_id, actions)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* actions (str) - Tекущие действия в чате. Отправьте пустое значение, если все действия завершены.
Available values : looking, typing

### /chats/getInfo
Получить информацию о чате
```python
await get_chat_info(chat_id)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).

### /chats/getAdmins
Получить список администраторов чата
```python
await get_chat_admins(chat_id)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).

### /chats/getMembers
Получить список участников чата
```python
await get_chat_members(chat_id, cursor=None)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* cursor (str) - Идентификатор для получения продолжения списка пользователей. Cursor можно получить из результатов первого/предыдущего запроса getMembers. Поле cursor.

### /chats/getBlockedUsers
Получить список пользователей, которые заблокированы в чате
```python
await get_chat_blocked_users(chat_id)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).

### /chats/getPendingUsers
Получить список пользователей, которые ожидают вступления в чат
```python
await get_chat_pending_users(chat_id)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).

### /chats/blockUser
Заблокировать пользователя в чате
```python
await chat_block_user(chat_id, user_id, del_last_messages=False)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* user_id (str) - Уникальный ник или id пользователя.
* del_last_messages (boolean) - Удаление последних сообщений заданного пользователя в чате.

### /chats/unblockUser
Разблокировать пользователя в чате
```python
await chat_unblock_user(chat_id, user_id, del_last_messages=False)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* user_id (str) - Уникальный ник или id пользователя.

### /chats/resolvePending
Принять решение о пользователях, ожидающих вступления в чат
>Должен быть указан один из двух параметров: userId или everyone. Эти параметры не могут быть указаны одновременно
>Для вызова этого метода бот должен быть администратором в чате.

```python
await chat_resolve_pending(chat_id, approve=True, user_id="", everyone=False)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* approve (boolean) - Положительное или отрицательное решение.
* user_id (str) - Уникальный ник или id пользователя.
* everyone (boolean) - Решение обо всех пользователях, ожидающих вступления в чат. Не может быть передано с параметром userId.

### /chats/setTitle
Изменить название чата
> Для вызова этого метода бот должен быть администратором в чате.

```python
await set_chat_title(chat_id, title)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* title (str) - Название чата.

### /chats/setAbout
Изменить описание чата
> Для вызова этого метода бот должен быть администратором в чате.

```python
await set_chat_about(chat_id, about)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* about (str) - Описание чата.

### /chats/pinMessage
Закрепить сообщение в чате
> Для вызова этого метода бот должен быть администратором в чате.

```python
await pin_message(chat_id, msg_id)
```
* chat_id (str) - Уникальный ник или id чата или пользователя. Id можно получить из входящих events (поле chatId).
* msg_id (str) - Id сообщения.

### /chats/unpinMessage
Открепить сообщение в чате
> Для вызова этого метода бот должен быть администратором в чате.

```python
await unpin_message(chat_id, msg_id)
```

## files
### /files/getInfo
Получить информацию о файле
```python
await get_file_info(chat_id, file_id)
```
* file_id (str) - Id ранее загруженного файла.

# Class handler
## DefaultHandler(callback=func)
Обработчик по умолчанию
Параметры:
* callback - фукнцию которую вызывает хендлер

## NewChatMembersHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик входа в чата
Параметры:
* callback - фукнцию которую вызывает хендлер.
* filters - Фильтр.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер

## LeftChatMembersHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик выхода из чата
Параметры:
* callback - фукнцию которую вызывает хендлер.
* filters - Фильтр.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер

## PinnedMessageHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик на закрепления сообщения
Параметры:
* callback - фукнцию которую вызывает хендлер.
* filters - Фильтр.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер

## UnPinnedMessageHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик открепления сообщения
Параметры:
* callback - фукнцию которую вызывает хендлер.
* filters - Фильтр.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер

## MessageHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик нового сообщения
Параметры:
* callback - фукнцию которую вызывает хендлер.
* filters - Фильтр.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер

## EditedMessageHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик редактирования сообщения
Параметры:
* callback - фукнцию которую вызывает хендлер.
* filters - Фильтр.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер

## DeletedMessageHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик удаление сообщений
Параметры:
* callback - фукнцию которую вызывает хендлер.
* filters - Фильтр.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер

## CommandHandler(callback=None, command=None, multiline=False, ignore=None)
Обработчик команд
Параметры:
* callback - фукнцию которую вызывает хендлер.
* command - Команда.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер.

## HelpCommandHandler(callback=None, command=None, multiline=False, ignore=None)
Обработчик команды /help
Параметры:
* callback - фукнцию которую вызывает хендлер.
* command - Команда.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер.

## StartCommandHandler(callback=None, command=None, multiline=False, ignore=None)
Обработчик команды /start
Параметры:
* callback - фукнцию которую вызывает хендлер.
* command - Команда.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер.

## UnknownCommandHandler(callback=None, multiline=False, ignore=None)
Обработчик неизвестной команды
Параметры:
* callback - фукнцию которую вызывает хендлер.
* command - Команда.
* multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.
* ignore - настройка приоритетов команд, на вход получает хендлер.

## BotButtonCommandHandler(callback=None, filters=None, multiline=False, ignore=None)
Обработчик кнопок
<details> 
<<<<<<< Updated upstream
  <summary>Параметры</summary>
   <ul>
    <li>callback - фукнцию которую вызывает хендлер.</li>
    <li>filters - Фильтр.</li>
     <li>multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.</li>
    <li>ignore - настройка приоритетов команд, на вход получает хендле</li>
    </ul>
</details>

=======
    <summary>Параметры</summary>
    <ul>
        <li>callback - фукнцию которую вызывает хендлер.</li>
        <li>filters - Фильтр.</li>
        <li>multiline - Обработчик многострочных команд.На вход функция получит помимо (bot, event) объект user, через который можно ожидать следующий ответ пользователя.</li>
        <li>ignore - настройка приоритетов команд, на вход получает хендле</li>
    </ul>
</details>

# Class Filter
## message
Филтр сообщения
## command
Фильр команд
## file
Фильтр файлов
## image
Фильтр изображений
## video
Фильтр видео
## audio
Фильтр аудио
## voice
Фильтр голосовых сообщений
## media
Фильтр медиа файлов (image, video, audio, voice)
## sticker
Фильтр стикеров
## url
URL фильтр
## text_only
Фильтр текстовых сообщений, не (command, sticker, file, url)
## text(list)
Фильтр сообщения по тексту
```python
bot.dispatcher.add_handler(
    MessageHandler(
        callback=hello,
        filters=Filter.text(['Ghbdtn', 'Привет', 'Прив', 'Хай'])
    )
)
```

## regexp(regular)
Фильтр сообщения по тексту
Параметры:
* regular - регулярное выражение
```python
bot.dispatcher.add_handler(MessageHandler(
                            callback=hello, 
                            filters=Filter.regexp('(?i)^(привет|хай)')
                        )
                    )
```
## mention(user_id=None)
Упоминание пользователей
Параметры:
* user_id - id на который будет срабатывать

## forward
Фильтр пересылания сообщения

## reply
Фильтр ответа на сообщения

## callback_data(callback_data)
Фильтр кнопок
Параметры:
* callback_data - callbackData

## callback_data_regexp(regular)
Фильтр кнопок с регуляторным выражением
Параметры:
* regular - регулярное выражение
>>>>>>> Stashed changes

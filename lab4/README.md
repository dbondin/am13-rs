## Лаб.4

TCP/IP IM

\<LF> - возврат каретки ('\r' в C/C++)
\<CR> - перевод строки ('\n' в C/C++)

\<NL> = \<CR> || \<LF>\<CR>

message = произвольный текст без \<NL> в UTF-8 (ru_RU)

### 1 Регистрация нового пользователя

C: register\<NL>
   name\<NL>
   password\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>

### Аутентификация (логин)

C: login\<NL>
   name\<NL>
   password\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>

Любая сессия работы с сервером начинается с register или login.

Успешный register или login может быть только один за сессию.

Любая другая команда до register или login должна завершаться с Error.
 
### Получить список друзей

C: listFriends\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>
   count\<NL>
   friend1\<NL>
   friend2\<NL>
   ...
   friendN\<NL>
 
### Посмотреть историю сообщений

C: historyMessage\<NL>
   friend\<NL>

S: Error\<NL>
   description\<NL>

S: historyMessageOk
   count\<NL>
   message1\<NL>
   message2\<NL>
   ...
   messageN\<NL>
 
### Заслать новое сообщение

C: sendMessage\<NL>
   friend\<NL>
   message\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>
 
### Проверить, нет-ли новых сообщений для меня

Клиент периодически опрашивает сервер на предмет новых сообщений

C: getNewMessages\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>
   count\<NL>
   friend1\<NL>
   message1\<NL>
   friend2\<NL>
   message2\<NL>
   ...
   friendN\<NL>
   messageN\<NL>

### Добавить друга

C: addFriend\<NL>
   friend\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>

### Запрос списка предложений о дружбе (кто хотел со мной дружить и с кем хотел я)

Клиент периодически спрашивает сервер.

state = IN || OUT

C: getFriendRequests\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>
   count\<NL>
   state1\<NL>
   friend1\<NL>
   state2\<NL>
   friend2\<NL>
   ...
   stateN\<NL>
   friendN\<NL>

### Keep alive

Сервер считает клиента отключившимся, если не получал от него этого сообщения в течение 5 секунд.

C: keepAlive\<NL>

S: Error\<NL>
   description\<NL>

S: Ok\<NL>

# Pixplaze Core Plugin REST API

---
## Server

Методы для взаимодействия с Minecraft сервером.

### **GET** `/server`

#### Описание
Возвращает статус сервера в настоящий момент в виде объекта.

#### Параметры запроса
- view="[full | simple | status]": str

#### Тело ответа
```json
{
  "name": "Pixplaze Vanilla Server",
  "max_players": 20,
  "difficulty": "normal",
  "map_address": "127.0.0.1:25567"
}
```

#### Описание объекта


#### **GET** `/server/status`
```json
{
  "status": "online",
  "players": 15,
  "uptime": 64852
}
```

*Поля:*
*string* **status** - статус сервера. Может иметь значения `online`, `maintenance`.
*integer* **players** - количество онлайн игроков на сервере.
*integer* **uptime** - время с последней перезагрузки сервера в секундах.

## Player
Методы для взаимодействия с сущностями игрока.

### **GET** `/players?view=[full|simple]`

Возвращает список UUID игроков в виде объекта.

```json
[
  {
    "uuid": "069a79f4-44e9-4726-a5be-fca90e38aaf5",
    "username": "notch",
    "icon": "...",
    "status": "online",
    "playtime": 78532
  },
  {
    "uuid": "f498513c-e8c8-4773-be26-ecfc7ed5185d",
    "username": "jeb_",
    "icon": "...",
    "status": "online",
    "playtime": 92861
  }
]
```


*Параметры:*
*string* **status** - идентификатор статуса группы игроков на сервере. Может принимать значения `online`, `offline`, `banned`, `whitelisted`.

#### **GET** `/players/{uuid}`

Возвращает общую информацию об игроке в виде объекта.
```json
{
  "uuid": "069a79f4-44e9-4726-a5be-fca90e38aaf5",
  "username": "notch",
  "icon": "...",
  "status": "online",
  "status": {
    "playtime": 78532,
    "status": "online|offline|banned|whitelisted"
  },
  "playtime": 78532
}
```

*Параметры:*\
*string* **uuid** - идентификатор пользователя Mojang.

*Поля:*\
*string* **nickname** - игровой ник игрока.\
*string* **status** - игровой статус игрока. Может иметь значения `online`, `offline`.\
*integer* **playtime** - суммарное время игры на сервере в секундах.

#### **GET** `/players/{uuid}/stats`

Возвращает статистику всех действий и полученные достижения игрока.
##### Отложено.

#### **POST** `/players/{uuid}/action`

Добавляет действие, которое необходимо совершить над игроком.

*Параметры:*
*string* **type** - тип совершаемого действия. Может иметь значения `kick`, `ban`, `unban`.
*integer* **time** (необяз.) - срок действия в секундах. Необходим только если `type=ban`.

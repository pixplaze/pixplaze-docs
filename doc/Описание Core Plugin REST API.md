# Pixplaze Core Plugin REST API

---
## Server

Методы для взаимодействия с Minecraft сервером.

### **GET** `/server`

#### Описание
Возвращает актуальную информацию о настройках и состоянии сервера.

#### Параметры:
- **view**="[status | short | full]": str - вид запрашиваемого ответа. При значении `"status"` возвращает данные о состоянии сервера, а при значениях `"short"` и `"full"` его статические данные в минимальном и расширенном вариантах соответственно.

#### Поля:
- **name**: str - название сервера в motd.
- **max_players**: int - максимальное количество игроков на сервере.
- **difficulty**: str - уровень сложности игры.
- **map_address**: str - адрес для доступа к интерактивной карте мира игры.
- **online_status**=["online" | "on_maintenance"]: str - онлайн статус сервера.
- **players**: int - количество онлайна на сервере.
- **uptime**: int - время с последней перезагрузки сервера в секундах.\
*Примечание*: список полей этого метода будет дополняться в будущем.

#### Примеры ответа
```json
/server?view=short
{
  "name": "Pixplaze Vanilla Server",
  "max_players": 20,
  "difficulty": "normal",
  "map_address": "127.0.0.1:25567"
}

/server?view=status
{
  "online_status": "online",
  "players": 15,
  "uptime": 64852
}
```

## Players
Методы для взаимодействия с сущностями игрока.

### **GET** `/players/{uuid}`

Возвращает общую информацию об игроке в виде объекта.

#### Параметры:
- **uuid**: str - идентификатор пользователя Mojang.

#### Поля:
- **uuid**: str - идентификатор пользователя Mojang.
- **nickname**: str - игровой ник пользователя.
- **status**="[online | offline]": str - игровой статус пользователя.
- **playtime**: int - суммарное время игры на сервере в секундах.

#### Пример ответа
```json
{
  "uuid": "069a79f4-44e9-4726-a5be-fca90e38aaf5",
  "username": "notch",
  "status": "online",
  "playtime": 78532
}
```

### **GET** `/players`

Возвращает список объектов игроков.

#### Параметры:
- **status**="[online | offline | banned | whitelisted]": str - идентификатор статуса группы игроков на сервере.

#### Примеры ответа

```json
/players?status=online
[
  {
    "uuid": "069a79f4-44e9-4726-a5be-fca90e38aaf5",
    "username": "notch",
    "status": "online",
    "playtime": 78532
  },
  {
    "uuid": "f498513c-e8c8-4773-be26-ecfc7ed5185d",
    "username": "jeb_",
    "status": "online",
    "playtime": 92861
  }
]

/players
[
  {
    "uuid": "069a79f4-44e9-4726-a5be-fca90e38aaf5",
    "username": "notch",
    "status": "online",
    "playtime": 78532
  },
  {
    "uuid": "f498513c-e8c8-4773-be26-ecfc7ed5185d",
    "username": "jeb_",
    "status": "online",
    "playtime": 92861
  },
  {
    "uuid": "08ab9edc-9f72-31e0-8050-88ee2c6d6b91",
    "username": "pazik98",
    "status": "offline",
    "playtime": 85427
  }
]
```

### **GET** `/players/{uuid}/stats`

Возвращает статистику всех действий и полученные достижения игрока.
##### Отложено.

### **POST** `/players/{uuid}/action`

Добавляет действие, которое необходимо совершить над игроком.

*Параметры:*
*string* **type** - тип совершаемого действия. Может иметь значения `kick`, `ban`, `unban`.
*integer* **time** (необяз.) - срок действия в секундах. Необходим только если `type=ban`.

**Отложено.**

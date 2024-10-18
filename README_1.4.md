# Документация API

## REST API

### Сервис управления устройствами

1. **Получение информации об устройстве**
    - **Эндпойнт**: `/devices/{device_id}`
    - **Метод**: `GET`
    - **Описание**: Возвращает подробную информацию о конкретном устройстве по его ID.
    - **Безопасность**: Bearer Token
    - **Формат ответа**:
      ```json
      {
        "id": "string",
        "type_id": "string",
        "house_id": "string",
        "serial_number": "string",
        "status": "string"
      }
      ```
    - **Коды ответа**:
        - `200`: Успех
        - `404`: Устройство не найдено
        - `500`: Ошибка сервера

2. **Обновление состояния устройства**
    - **Эндпойнт**: `/devices/{device_id}/status`
    - **Метод**: `PUT`
    - **Описание**: Позволяет изменить состояние устройства (например, включить/выключить).
    - **Безопасность**: Bearer Token
    - **Формат запроса**:
      ```json
      {
        "status": "string"
      }
      ```
    - **Формат ответа**:
      ```json
      {
        "message": "string"
      }
      ```
    - **Коды ответа**:
        - `200`: Успех
        - `404`: Устройство не найдено
        - `500`: Ошибка сервера

3. **Отправка команды устройству**
    - **Эндпойнт**: `/devices/{device_id}/commands`
    - **Метод**: `POST`
    - **Описание**: Отправляет команду устройству (например, «установить температуру 22 градуса»).
    - **Безопасность**: Bearer Token
    - **Формат запроса**:
      ```json
      {
        "command": "string",
        "value": "string"
      }
      ```
    - **Формат ответа**:
      ```json
      {
        "message": "string"
      }
      ```
    - **Коды ответа**:
        - `200`: Успех
        - `404`: Устройство не найдено
        - `500`: Ошибка сервера

### Сервис телеметрии

1. **Получение последних данных телеметрии**
    - **Эндпойнт**: `/devices/{device_id}/telemetry/latest`
    - **Метод**: `GET`
    - **Описание**: Возвращает последнее полученное значение телеметрии для устройства.
    - **Безопасность**: Bearer Token
    - **Формат ответа**:
      ```json
      {
        "id": "string",
        "device_id": "string",
        "timestamp": "string",
        "data": "string"
      }
      ```
    - **Коды ответа**:
        - `200`: Успех
        - `404`: Устройство не найдено
        - `500`: Ошибка сервера

2. **Получение исторических данных телеметрии**
    - **Эндпойнт**: `/devices/{device_id}/telemetry`
    - **Метод**: `GET`
    - **Описание**: Возвращает исторические данные телеметрии для устройства за определённый период времени.
    - **Безопасность**: Bearer Token
    - **Формат запроса**:
      ```json
      {
        "start_time": "string",
        "end_time": "string"
      }
      ```
    - **Формат ответа**:
      ```json
      [
        {
          "id": "string",
          "device_id": "string",
          "timestamp": "string",
          "data": "string"
        }
      ]
      ```
    - **Коды ответа**:
        - `200`: Успех
        - `404`: Устройство не найдено
        - `500`: Ошибка сервера

## AsyncAPI

### Сервис управления устройствами

1. **Изменение состояния устройства**
    - **Топик**: `device-status-changed`
    - **Описание**: Событие, которое публикуется при изменении состояния устройства.
    - **Формат события**:
      ```json
      {
        "device_id": "string",
        "status": "string",
        "timestamp": "string"
      }
      ```

2. **Отправка команды устройству**
    - **Топик**: `device-command-sent`
    - **Описание**: Событие, которое публикуется при отправке команды устройству.
    - **Формат события**:
      ```json
      {
        "device_id": "string",
        "command": "string",
        "value": "string",
        "timestamp": "string"
      }
      ```

### Сервис телеметрии

1. **Получение данных телеметрии**
    - **Топик**: `telemetry-data-received`
    - **Описание**: Событие, которое публикуется при получении новых данных телеметрии.
    - **Формат события**:
      ```json
      {
        "device_id": "string",
        "timestamp": "string",
        "data": "string"
      }
      ```
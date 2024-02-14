
### Использование API-ключа для авторизации

Для всех запросов необходимо включить API-ключ в заголовки запроса. Это обеспечивает авторизацию и аутентификацию запросов.

**Заголовок запроса:**
```
X-API-Key: <your_api_key_here>
```

### 1. Массовое добавление новых автомобилей

- **Эндпоинт:** `/new-cars/batch`
- **Метод:** POST
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Тело запроса:** 
  ```json
  {
    "cars": [
      {
        "price": "string",
        "relation": "string",
        "use": "string",
        "model": "string",
        "structure": "string",
        "code": "string",
        "store": "number",
        "view": "string",
        "equipment": "string",
        "sku": "string",
        "passangers": "number",
        "weight": "number",
        "chassis-length": "string",
        "region": "string",
        "salon": "string",
        "vin": "string",
        "color": "string",
        "vin_original": "string",
        "engine-type": "string",
        "year": "number",
        "drive": "string"
      }
    ]
  }
  ```
- **Ответы:**
  - **Код 201 (Created):** Успешно добавлено. Возвращает количество обработанных и необработанных записей.
    ```json
    {
      "message": "Новые автомобили успешно добавлены.",
      "processed": 100,
      "failed": 0
    }
    ```
  - **Код 400 (Bad Request):** Ошибка в данных. Возвращает информацию об ошибке.
    ```json
    {
      "error": "Некорректный формат данных.",
      "details": "<подробное описание ошибки>"
    }
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```

#### Передаваемые поля

- **price:** Цена автомобиля.
- **use:** Использование автомобиля. (грузовой легковой комм)
- **model:** Модель автомобиля.
- **mark:** Марка автомобиля.
- **code:** Уникальный код автомобиля (1с код)(нужен гуид)
- **equipment:** Комплектация. 
- **passangers:** Количество пассажиров.
- **weight:** Масса автомобиля.
- **chassis-length:** Длина шасси.
- **region:** Регион.(Город)
- **salon:** Салон.
- **vin:** VIN номер.
- **vin_original:** Оригинальный VIN.
- **color:** Цвет.
- **engine-type:** Тип двигателя.
- **year:** Год выпуска.
- **drive:** Привод.
- **reserv:** Резерв (булево).
- **gear:** Коробка.


#### Рекомендации по использованию

- **Пакетная обработка:** Разбивайте большие объемы данных на более мелкие пакеты для избежания перегрузки сервера и обеспечения более высокой производительности и надежности обработки. (рекомендуем передавать по 100 автомобилей за раз)

#### Редактирование информации о новых автомобилях

- **Эндпоинт:** `/new-cars/update`
- **Метод:** POST
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Тело запроса:**
  ```json
  {
    "cars": [
      {
        "vin_original": "string",
        "update": {
          "price": "string",
          "model": "string",
          // Остальные поля для обновления
        }
      },
      // Другие автомобили для обновления
    ]
  }
  ```
- **Ответы:**
  - **Код 200 (OK):** Информация об автомобилях успешно обновлена. Возвращает количество успешно обновленных записей.
    ```json
    {
      "message": "Информация о новых автомобилях успешно обновлена.",
      "updated": 2,
      "failed": 1,
      "failed_vins": ["vin1", "vin2"] // VIN автомобилей, информацию о которых не удалось обновить
    }
    ```
  - **Код 400 (Bad Request):** Ошибка в данных. Возвращает информацию об ошибке.
    ```json
    {
      "error": "Некорректный формат данных.",
      "details": "<подробное описание ошибки>"
    }
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```

#### Список всех новых автомобилей с фильтрацией

- **Эндпоинт:** `/new-cars/list`
- **Метод:** GET
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Параметры запроса:** Необязательные параметры для фильтрации списка (например, `model`, `price`, `year` и т.д.)
- **Пример запроса:** `/new-cars/list?price=3204900:8875000&model=Tesla Model S`
- **Ответы:**
  - **Код 200 (OK):** Возвращает список автомобилей, соответствующих заданным фильтрам.
в полях «от-до» разделитель “:”

    ```json
    [
      {
        "vin_original": "string",
        "price": "string",
        "model": "string",
        // Остальные поля автомобиля
      },
      // Другие автомобили в списке
    ]
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```
  - **Код 404 (Not Found):** Если по заданным фильтрам автомобили не найдены.
    ```json
    {
      "message": "Автомобили по заданным критериям не найдены."
    }
    ```

    
### 2. Массовое добавление "бу" автомобилей

- **Эндпоинт:** `/used-cars/batch`
- **Метод:** POST
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Тело запроса:**
  ```json
  {
    "cars": [
      {
        "used_cars_type": "string",
        "used_cars_modification_id": "string",
        "used_cars_mark_id": "string",
        "used_cars_group_id": "string",
        "used_cars_year": "number",
        "used_cars_run": "number",
        "used_cars_vin": "string",
        "used_cars_color": "string",
        "used_cars_availability": "string",
        "used_cars_wheel": "string",
        "used_cars_custom": "string",
        "used_cars_seats": "number",
        "used_cars_state": "string",
        "used_cars_haggle": "string",
        "used_cars_engine_power": "number",
        "used_cars_engine_volume": "number",
        "used_cars_engine_type": "string",
        "used_cars_gearbox": "string",
        "used_cars_extras": "string",
        "used_cars_body_type": "string",
        "used_cars_loading": "string",
        "used_cars_drive": "string",
        "used_cars_images": "array",
        "price": "number",
        "content": "string"
      }
    ]
  }
  ```
- **Ответы:**
  - **Код 201 (Created):** Успешно добавлено. Возвращает количество обработанных и необработанных записей.
    ```json
    {
      "message": "Бу автомобили успешно добавлены.",
      "processed": 100,
      "failed": 0
    }
    ```
  - **Код 400 (Bad Request):** Ошибка в данных. Возвращает информацию об ошибке.
    ```json
    {
      "error": "Некорректный формат данных.",
      "details": "<подробное описание ошибки>"
    }
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```
- **Пакетная обработка:** Разбивайте большие объемы данных на более мелкие пакеты для избежания перегрузки сервера и обеспечения более высокой производительности и надежности обработки. (рекомендуем передавать по 100 автомобилей за раз)

#### Fписание полей для массового добавления "бу" автомобилей:

- **used_cars_type (Тип транспорта):** Категория автомобиля (например, "Легковые").
- **used_cars_modification_id (Модификация):** Конкретная модификация автомобиля (например, "1.4 MT (140 л.с.)").
- **used_cars_mark_id (Марка):** Производитель или марка автомобиля (например, "Skoda").
- **used_cars_group_id (Модель):** Модель автомобиля (например, "Octavia, III (A7)").
- **used_cars_year (Год выпуска):** Год производства автомобиля (например, 2015).
- **used_cars_run (Пробег):** Пробег автомобиля в километрах (например, 101795).
- **used_cars_vin (VIN):** Уникальный идентификационный номер автомобиля (например, "XW8AC6NE0FH022811").
- **used_cars_color (Цвет):** Цвет автомобиля (например, "Серый").
- **used_cars_availability (Наличие):** Доступность автомобиля для продажи (например, "В наличии").
- **used_cars_wheel (Расположение руля):** Расположение рулевого колеса (например, "Левый").
- **used_cars_custom (Растаможка):** Статус растаможки автомобиля (например, "Растаможен").
- **used_cars_seats (Количество мест):** Количество пассажирских мест в автомобиле.
- **used_cars_state (Состояние):** Общее состояние автомобиля (например, "Отличное").
- **used_cars_haggle (Торг):** Возможность торговаться по цене.
- **used_cars_engine_power (Мощность двигателя):** Мощность двигателя в лошадиных силах (например, 140).
- **used_cars_engine_volume (Объем двигателя):** Объем двигателя в кубических сантиметрах (например, 1395).
- **used_cars_engine_type (Тип двигателя):** Тип используемого топлива или технологии двигателя (например, "Бензин").
- **used_cars_gearbox (Коробка):** Тип коробки передач (например, "Механическая").
- **used_cars_extras (Дополнительно):** Дополнительное оборудование или особенности автомобиля.
- **used_cars_body_type (Кузов):** Тип кузова автомобиля (например, "Лифтбек 5 дв.").
- **used_cars_loading (Нагрузка):** Максимально допустимая нагрузка.
- **used_cars_drive (Привод):** Тип привода автомобиля.
- **used_cars_images (images):** Список изображений автомобиля.
- **price (Цена):** Цена автомобиля.
- **content (Описание):** Дополнительное описание автомобиля.

Эти поля позволяют детально описать каждый "бу" автомобиль при его добавлении в систему через API, обеспечивая полноту и актуальность информации для будущих покупателей.

#### Редактирование информации о "бу" автомобилях

- **Эндпоинт:** `/used-cars/update`
- **Метод:** POST
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Тело запроса:**
  ```json
  {
    "cars": [
      {
        "used_cars_vin": "string",
        "update": {
          "used_cars_year": "number",
          "used_cars_color": "string",
          // Остальные поля для обновления
        }
      },
      // Другие "бу" автомобили для обновления
    ]
  }
  ```
- **Ответы:**
  - **Код 200 (OK):** Информация о "бу" автомобилях успешно обновлена. Возвращает количество успешно обновленных записей.
    ```json
    {
      "message": "Информация о бу автомобилях успешно обновлена.",
      "updated": 3,
      "failed": 0
    }
    ```
  - **Код 400 (Bad Request):** Ошибка в данных. Возвращает информацию об ошибке.
    ```json
    {
      "error": "Некорректный формат данных.",
      "details": "<подробное описание ошибки>"
    }
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```

Таким образом, оба метода позволяют обновлять информацию для множества автомобилей в одном запросе.




#### Список всех "бу" автомобилей с фильтрацией

- **Эндпоинт:** `/used-cars/list`
- **Метод:** GET
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Параметры запроса:** Необязательные параметры для фильтрации списка (например, `used_cars_year`, `used_cars_color`, `used_cars_mark_id` и т.д.)
- **Пример запроса:** `/used-cars/list?used_cars_year=2019&used_cars_color=black`
- **Ответы:**
  - **Код 200 (OK):** Возвращает список "бу" автомобилей, соответствующих заданным фильтрам.
    ```json
    [
      {
        "used_cars_vin": "string",
        "used_cars_year": "number",
        "used_cars_color": "string",
        // Остальные поля "бу" автомобиля
      },
      // Другие "бу" автомобили в списке
    ]
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```
  - **Код 404 (Not Found):** Если по заданным фильтрам "бу" автомобили не найдены.
    ```json
    {
      "message": "Бу автомобили по заданным критериям не найдены."
    }
    ```



### 3. Получение информации обо всех актуальных бронированиях
(возвращает все бронирования со статусом кроме "завершено")
- **Эндпоинт:** `/reservations`
- **Метод:** GET
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Ответы:**
  - **Код 200 (OK):** Возвращает список всех актуальных бронирований.
    ```json
    [
      {
        "vin": "string",
        "model": "string",
        "reservation_date": "string",
        "status": "string"
      },
      ...
    ]
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```
  - **Код 404 (Not Found):** Если бронирования отсутствуют.
    ```json
    {
      "message": "Бронирования не найдены."
    }
    ```

#### Обновление статуса резервации автомобиля
метод API для обновления статуса резервации автомобиля. Этот метод позволит менять статус резервации на новый, например, из "забронировано" в "выкуплено" или "отменено".

- **Эндпоинт:** `/reservations/update`
- **Метод:** POST
- **Авторизация:** API-ключ в заголовке `X-API-Key`
- **Тело запроса:**
  ```json
  {
    "reservation_id": "string",
    "new_status": "string"
  }
  ```
  Где `reservation_id` — уникальный идентификатор резервации, а `new_status` — новый статус резервации (например, `order.status.shipped` для статуса "доставлено" или `order.status.canceled` для "отменено").

- **Ответы:**
  - **Код 200 (OK):** Статус резервации успешно обновлен.
    ```json
    {
      "message": "Статус резервации успешно обновлен."
    }
    ```
  - **Код 400 (Bad Request):** Ошибка в данных запроса.
    ```json
    {
      "error": "Некорректный запрос. Проверьте данные.",
      "details": "<подробное описание ошибки>"
    }
    ```
  - **Код 404 (Not Found):** Резервация с указанным ID не найдена.
    ```json
    {
      "message": "Резервация с указанным ID не найдена."
    }
    ```
  - **Код 401 (Unauthorized):** Отсутствует или неверный API-ключ.
    ```json
    {
      "error": "Неавторизованный доступ."
    }
    ```

#### Статусы резервации:

1. **Новый (`order.status.new`):** Начальный статус резервации, указывает на то, что резервация только что создана.
2. **В обработке (`order.status.processing`):** Резервация находится в процессе обработки, например, проверяется наличие автомобиля или подготавливается к доставке.
3. **Оплачен (`order.status.paid`):** Указывает на то, что резервация была оплачена покупателем.
4. **Доставлен (`order.status.shipped`):** Автомобиль был доставлен покупателю.
5. **Отменен (`order.status.canceled`):** Резервация была отменена по инициативе покупателя или по другим причинам.
6. **Завершен (`order.status.complete`):** Все условия резервации выполнены, автомобиль передан покупателю, сделка закрыта.
7. **Ожидание (`order.status.pending`):** Резервация ожидает дополнительных действий, например, подтверждения оплаты или поступления автомобиля на склад.

Эти статусы позволяют точно отслеживать каждый этап взаимодействия с клиентом от момента создания резервации до момента полного выполнения всех условий сделки.

```mermaid
graph TD
    A[Начало] --> B[Кипячение воды]
    B --> C{Есть ли чай?}
    C -->|Да| D[Заварить чай]
    C -->|Нет| E[Купить чай]
    E --> D
    D --> F[Пить чай]
    F --> G[Конец]
```
---
```mermaid
sequenceDiagram
    participant C as Клиент
    participant A as Приложение
    participant S as Сервер
    participant D as Водитель
    
    title Процесс заказа такси

    C->>A: Вызов такси через приложение
    activate A
    A->>S: Отправка запроса на поиск такси
    activate S
    S->>S: Поиск свободного водителя
    S->>D: Уведомление о новом заказе
    activate D
    D->>S: Принятие заказа
    S->>A: Подтверждение с данными водителя
    A->>C: Уведомление: "Водитель найден"
    deactivate A
    deactivate S
    D->>C: Забирает клиента
    deactivate D
 ```

---

```mermaid
classDiagram
    class Book {
        -String title
        -String author
        -String ISBN
        -Boolean isAvailable
        +borrow()
        +returnBook()
        +getInfo()
    }
    
    class User {
        -String name
        -String userId
        -List~Book~ borrowedBooks
        +borrowBook(book)
        +returnBook(book)
        +getBorrowedBooks()
    }
    
    class Library {
        -List~Book~ books
        -List~User~ users
        +addBook(book)
        +removeBook(book)
        +registerUser(user)
        +findBook(isbn)
        +lendBook(user, book)
    }
    
    User "1" *-- "*" Book : borrows
    Library "1" o-- "*" Book : contains
    Library "1" o-- "*" User : manages
```
---
---
# Диаграмма Ганта
```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title Разработка мобильного приложения
    
    section Основные этапы
    Подготовка      :a1, 2025-11-20, 5d
    Дизайн          :a2, after a1, 7d
    Фронтенд-разработка :a3, after a2, 10d
    Бэкенд-разработка   :a4, after a1, 12d
    Тестирование    :after a3, after a4, 5d
```
---
# Продвинутый
```mermaid
graph LR
    subgraph Frontend
        F1[React] --> F2[Redux]
        F1 --> F3[Router]
    end

    subgraph Backend
        B1[Node.js] --> B2[Express]
        B1 --> B3[MongoDB]
    end

    subgraph External Services
        E1[Stripe]
        E2[(SendGrid)]
    end

    F1 -- API Calls --> B2
    B2 -- Data Read/Write --> B3
    B2 -- Initiate Payment --> E1
    B2 -- Send Notification --> E2
```
---
#   Диаграмма состояний
```mermaid
stateDiagram-v2
    direction LR
    
    [*] --> Новый
    
    Новый --> Подтвержденный : Инициализация заказа
    Подтвержденный --> Отмененный : Отмена клиентом
    
    Подтвержденный --> Оплата
    
    state Оплата {
        direction TB
        [*] --> Ожидает_платежа
        Ожидает_платежа --> Платеж_провален : Ошибка / Отказ
        Ожидает_платежа --> Платеж_успешен : Успешная транзакция
        Платеж_провален --> Подтвержденный : Повторить оплату
        Платеж_успешен --> [*]
    }
    
    Оплата --> Оплаченный : Платеж_успешен
    Платеж_провален --> Отмененный : Исчерпаны попытки оплаты
    
    Оплаченный --> Отправленный : Отгрузка со склада
    Отправленный --> Доставленный : Успешная доставка
    
    Доставленный --> Возвращенный : Инициировать возврат
```
---
# Экспертный
```mermaid
journey
    title Путь пользователя: Покупка билетов в кино

    section Поиск фильма
      Пользователь: 1: Поиск фильма
      Пользователь: 2: Просмотр трейлера

    section Выбор сеанса
      Пользователь: 3: Фильтр по дате и времени
      Пользователь: 4: Выбор кинотеатра
      
    section Выбор мест
      Пользователь: 5: Выбор места на схеме
      Пользователь: 4: Добавление в корзину

    section Оплата
      Пользователь: 2: Ввод данных карты
      Пользователь: 1: Ожидание подтверждения

    section Получение билетов
      Пользователь: 5: Получение QR-кода на почту
```
---
# ER-диаграмма базы данных
```mermaid
erDiagram
    USERS ||--o{ POSTS : "имеет"
    USERS ||--o{ COMMENTS : "автор"
    POSTS ||--o{ COMMENTS : "содержит"
    POSTS ||--o{ LIKES : "получает"
    USERS ||--o{ LIKES : "ставит"
    USERS ||--o{ SUBSCRIPTIONS : "подписан_на"
    SUBSCRIPTIONS }|--|{ USERS : "подписчик"

    USERS {
        int id PK
        varchar name
        varchar email
    }

    POSTS {
        int id PK
        varchar content
        int author_id FK
    }

    COMMENTS {
        int id PK
        varchar content
        int post_id FK
        int author_id FK
    }

    LIKES {
        int user_id FK
        int post_id FK
        PRIMARY KEY user_id post_id)
    }

    SUBSCRIPTIONS {
        int follower_id FK
        int followed_id FK
        PRIMARY KEY follower_id followed_id)
    }
```
---
```mermaid
graph TD
    A[Клиент открывает приложение] --> B[Выбор ресторана и блюд]
    B --> C{Проверка доступности}
    C -->|Нет| D[Уведомление о недоступности]
    C -->|Да| E[Оформление заказа]
    E --> F[Оплата]
    F --> G{Оплата успешна?}
    G -->|Нет| H[Повторная попытка оплаты]
    G -->|Да| I[Уведомление ресторану]
    I --> J[Приготовление еды]
    J --> K[Назначение курьера]
    K --> L[Доставка]
    L --> M[Получение заказа]
    M --> N[Оценка сервиса]
    N --> O[Конец]
    D --> O
    H --> F
```
---
```mermaid
sequenceDiagram
    participant C as Клиент
    participant A as Приложение
    participant R as Ресторан
    participant K as Курьер
    participant S as Сервер
    
    title Процесс доставки еды

    C->>A: Выбор блюд и оформление заказа
    activate A
    A->>S: Отправка заказа
    activate S
    S->>R: Уведомление о новом заказе
    activate R
    R->>S: Подтверждение заказа
    S->>A: Статус "Приготовление"
    A->>C: Уведомление "Заказ готовится"
    
    R->>S: Статус "Готов к выдаче"
    S->>K: Назначение заказа
    activate K
    K->>S: Подтверждение доставки
    S->>A: Статус "Курьер в пути"
    A->>C: Уведомление "Курьер выехал"
    
    K->>C: Доставка заказа
    C->>A: Подтверждение получения
    A->>S: Заказ завершен
    S->>R: Уведомление о завершении
    deactivate R
    deactivate K
    deactivate S
    deactivate A
```
---
```mermaid
classDiagram
    class User {
        -String userId
        -String name
        -String phone
        -String address
        -List~Order~ orderHistory
        +register()
        +login()
        +placeOrder()
    }
    
    class Restaurant {
        -String restaurantId
        -String name
        -String address
        -String cuisineType
        -List~MenuItem~ menu
        -Double rating
        +addMenuItem()
        +updateMenu()
        +receiveOrder()
    }
    
    class MenuItem {
        -String itemId
        -String name
        -String description
        -Double price
        -Boolean available
        +updatePrice()
        +toggleAvailability()
    }
    
    class Order {
        -String orderId
        -String userId
        -String restaurantId
        -String courierId
        -List~OrderItem~ items
        -Double totalAmount
        -String status
        -DateTime orderTime
        +calculateTotal()
        +updateStatus()
        +cancelOrder()
    }
    
    class Courier {
        -String courierId
        -String name
        -String vehicle
        -Boolean available
        -Double rating
        +acceptOrder()
        +updateLocation()
        +completeDelivery()
    }
    
    class Payment {
        -String paymentId
        -String orderId
        -Double amount
        -String method
        -String status
        +processPayment()
        +refund()
    }
    
    User "1" --> "*" Order : places
    Restaurant "1" --> "*" MenuItem : offers
    Restaurant "1" --> "*" Order : receives
    Order "*" --> "*" MenuItem : contains
    Order "1" --> "1" Payment : has
    Courier "1" --> "*" Order : delivers
```
---
```mermaid
erDiagram
    USERS {
        string user_id PK
        string name
        string email
        string phone
        string address
        datetime created_at
    }
    
    RESTAURANTS {
        string restaurant_id PK
        string name
        string address
        string cuisine_type
        string phone
        decimal rating
        boolean active
    }
    
    MENU_ITEMS {
        string item_id PK
        string restaurant_id FK
        string name
        string description
        decimal price
        boolean available
    }
    
    ORDERS {
        string order_id PK
        string user_id FK
        string restaurant_id FK
        string courier_id FK
        string status
        decimal total_amount
        datetime order_time
        datetime delivery_time
    }
    
    ORDER_ITEMS {
        string order_item_id PK
        string order_id FK
        string item_id FK
        int quantity
        decimal price
    }
    
    COURIERS {
        string courier_id PK
        string name
        string phone
        string vehicle_type
        boolean available
        decimal rating
    }
    
    PAYMENTS {
        string payment_id PK
        string order_id FK
        decimal amount
        string payment_method
        string status
        datetime payment_date
    }
    
    USERS ||--o{ ORDERS : places
    RESTAURANTS ||--o{ MENU_ITEMS : offers
    RESTAURANTS ||--o{ ORDERS : receives
    ORDERS ||--o{ ORDER_ITEMS : contains
    ORDERS ||--|| PAYMENTS : has
    COURIERS ||--o{ ORDERS : delivers
    MENU_ITEMS }o--o{ ORDER_ITEMS : included_in
```
---
```mermaid
journey
    title Путь клиента при заказе доставки еды
    section Поиск и выбор
      Открытие приложения: 5: Клиент
      Поиск ресторана: 4: Клиент
      Выбор блюд: 5: Клиент
    section Оформление заказа
      Добавление в корзину: 4: Клиент
      Ввод данных доставки: 3: Клиент
      Выбор способа оплаты: 4: Клиент
    section Ожидание и получение
      Ожидание подтверждения: 3: Клиент
      Отслеживание статуса: 4: Клиент
      Получение заказа: 5: Клиент
    section После получения
      Проверка заказа: 4: Клиент
      Оценка сервиса: 4: Клиент
      Сохранение в историю: 5: Клиент
```
---
```mermaid
gantt
    title План разработки Сервиса доставки еды
    dateFormat YYYY-MM-DD
    section Анализ и проектирование
      Исследование рынка :a1, 2024-01-01, 10d
      Проектирование архитектуры :a2, after a1, 15d
      Создание ТЗ :a3, after a2, 7d
    section Бэкенд-разработка
      Разработка API :b1, after a3, 30d
      Интеграция платежей :b2, after b1, 10d
      База данных :b3, after a3, 25d
    section Фронтенд-разработка
      Клиентское приложение :c1, after a3, 40d
      Админ-панель :c2, after a3, 30d
      Приложение для курьеров :c3, after a3, 35d
    section Тестирование и запуск
      Тестирование :d1, after b1 c1, 20d
      Исправление ошибок :d2, after d1, 15d
      Запуск MVP :d3, after d2, 5d
    section Пост-запуск
      Сбор обратной связи :e1, after d3, 30d
      Доработки :e2, after e1, 25d
      Масштабирование :e3, after e2, 45d
```
---
```mermaid
pie title Доли автомобилей на российском рынке
    "Иномарки" : 45
    "Отечественные" : 30
    "Совместное производство" : 25
```
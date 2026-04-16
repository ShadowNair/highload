# Аналог Steam
## 1. Тема и целевая аудитория
### 1.1 Тема
**Steam** - международная цифровая платформа для дистрибуции и социального взаимодействия, которая позволяет:
- Покупать, скачивать и автоматически обновлять игры из каталога более 100 000+ тайтлов
- Участвовать в многопользовательских сессиях с голосовым чатом, приглашениями и системой друзей
- Обмениваться игровыми предметами, коллекционными карточками и внутриигровыми ценностями через **Торговую площадку**
- Создавать и монетизировать пользовательский контент через Steam Workshop
- Транслировать геймплей в реальном времени и взаимодействовать с сообществом через обзоры, скриншоты и форумы
- Использовать облачные сохранения, семейный доступ и кроссплатформенную синхронизацию
- Получать персонализированные рекомендации на основе игровой истории и поведенческих паттернов
**География и покрытие** - глобальное, с локализацией на 29+ языков и региональным ценообразованием
### 1.2 Функционал __MVP__
MVP включает в себя:
- Регистраци и авторизацию(двухфакторная аутентификация, OAuth, email-проверка)
- Каталог игр с фильтрами(цена, жанр, рейтинг, поиск)
- Оценка/отзыв об игре
- Страница продукта(трейлер, описание, системные требования, обзоры)
- Корзина и платежная система
- Список друзей(статус онлайн/оффлайн, в игре или нет)
- Библиотека пользователя(облачное сохранение, установка, запуск игр)
- Система достижений и игровая статистика
- Уведомления(скидки, активность друзей, вход в аккаунт)
### 1.3 Целевая аудитория
#### Ключевые метрики
|Метрика|Значение(миллионы)|
|:---:|:---:|
|MAU|132|
|DAU|69|
|PCU|41,66|
|DAU/MAU Ratio|52,27%|

#### Региональное распределение
```mermaid
%%{init: {
  'theme': 'base',
  'pie': {
    'pieSectionColors': [
      '#3B82F6',  // 🇺🇸 США — синий
      '#EF4444',  // 🇨🇳 Китай — красный
      '#10B981',  // 🇷🇺 Россия — зелёный
      '#F59E0B',  // 🇧🇷 Бразилия — оранжевый
      '#8B5CF6',  // 🇩🇪 Германия — фиолетовый
      '#6B7280'   // 🌍 Остальные — серый
    ],
    'strokeWidth': 2,
    'strokeColor': '#ffffff'
  }
}}%%
pie title 🌐 Топ стран по аудитории (млн)
    "🇺🇸 США" : 13.7
    "🇨🇳 Китай" : 11.4
    "🇷🇺 Россия" : 9.5
    "🇧🇷 Бразилия" : 4.9
    "🇩🇪 Германия" : 3.6
    "🌍 Остальные" : 88.9
```

#### Демографические данные пользователей
```mermaid
pie title Распределение по возрасту
    "20-29 лет (Ядро)" : 44
    "30-39 лет" : 33
    "40-49 лет" : 13
    "18-19 лет" : 5
    "50+ лет" : 5
```

#### Гендерное распределение пользователей
```mermaid
pie title ⚧ Гендерный состав аудитории
    "Мужской" : 60
    "Женский" : 40
```
## 2. Расчет нагрузки

### 2.1 Исходные данные для расчета

Дальше все расчеты опираются на следующие публичные показатели платформы и смежные ecommerce-бенчмарки:

* Steam указывает, что платформа имеет более 132 млн MAU. В открытых агрегированных оценках для 2025 года также используются 69 млн DAU и отношение DAU/MAU = 52,27%. Выручка Steam за 2024 год оценивается в 10,8 млрд долларов, при этом 61% выручки приходится на продажи игр. Средняя цена игр в топ-50 Steam по количеству проданных копий к октябрю 2025 года составляет 21,41 доллара. [1](https://partner.steamgames.com/?redir=country.php%3FcountryCode%3DCN%26dateStart%3D2024-08-16%26dateEnd%3D2024-08-22&utm_source=chatgpt.com)
* Для расчета воронки магазина используются следующие ecommerce-метрики. Средний conversion rate в сегменте Toys, Games & Collectables в феврале 2026 года составляет 1,86%. Средний глобальный add-to-cart rate составляет 6,07%. Средний documented cart abandonment rate равен 70,22%. Среднее число страниц за ecommerce-сессию составляет 2,6. Для оценки сезонного пика store-нагрузки используется рост add-to-cart rate с 5,85% в июле 2025 года до 7,46% в ноябре 2024 года, что дает дополнительный коэффициент 1,275. [2](https://www.irpcommerce.com/en/us/ecommercemarketdata.aspx?Market=19)
* Для оценки пользовательского поведения используются внешние агрегированные данные по Steam: 5,2 логина в неделю на пользователя, 1,4 часа на сессию и 1,8 запущенной игры на один DAU. Кроме того, Steam сообщает, что пик активности приходится на окно 19:00-23:00, то есть на 4 часа в сутки.[3](https://sqmagazine.co.uk/steam-statistics/)
* Для cloud save используется доля игр с поддержкой Steam Cloud. По данным SteamDB, в каталоге сейчас 67 225 игр с признаком Steam Cloud. Открытые оценки общего числа игр на платформе дают 125 494 тайтла, значит доля cloud-enabled игр составляет 53,6%. В проектной модели принимается 2 cloud sync-операции на игровую сессию: чтение при запуске и запись при завершении. Сам Steam Cloud официально описан как механизм хранения и синхронизации пользовательских файлов на серверах Steam.[4](https://steamdb.info/instantsearch/)
* Для уведомлений используется официальная статистика Steam Events. Valve указала, что за 2025 год разработчики опубликовали 436 592 Steam Events, которые суммарно дали 3,13 млрд player views. Это подходит как нижняя оценка нагрузки на чтение продуктовых уведомлений и событийной ленты.[5](https://steamcommunity.com/groups/steamworks/announcements/detail/528746884222682053)

Принятые обозначения:
* T_day = 86400 секунд в сутки
* k_day = 24/4 = 6 - коэффициент внутрисуточного пика
* k_sale = 7.46/5.85 = 1.275 - коэффициент сезонного store-пика
* k_store = k_day * k_sale = 7.65 = 8

### 2.2 Продуктовые метрики

#### Количество покупок в день

Purchases = (10.8 * 10^9 * 0.61) / (21.41 * 365) = 843032

#### Количество созданий корзины в день:

Checkout = Purchases/(1 - 0.7022) = 2830866

#### Количество просмотров карточек игр:

Product = Checkout/0.0607 = 46637007

#### Количество store-сессий:

Store = Purchases/ 0.0186 = 45324301

#### Общее число просмотров страниц магазина:

Page = Store * 2.6 = 117843182

#### Из них поисковые и листинговые переходы каталога:

Catalog = Page - Product - Checkout = 68375309

#### Логины в день:

Login = DAU * 5.2 / 7 = 51257143

#### Открытия библиотеки в день:

Library = DAU * 1.8 = 124200000

#### Cloud sync-операции в день:
Прнимаем две операции в виду начала игры(загрузки) и конца игры(выгрузки)

Cloudsave = DAU * 1.8 * 0.521 * 2 = 129398400

#### Чтение ленты уведомлений и событий:
Notifications = 3.13 * 10^9 / 365 = 8575342

#### Отзывы:
Нет данных от самого стим, но возьмем допущение 1 отзыв на 40 покупок по статье.

Reviews = 843032/ 40 = 21076

#### Сводная таблица продуктовых метрик:

|Метрика|Значение|
|:--:|:--:|
|MAU|132000000|
|DAU|69000000|
|Purchases|843032|
|Checkout|2830866|
|Product|46637007|
|Store|45324301|
|Page|117843182|
|Catalog|68375309|
|Login|51257143|
|Library|124200000|
|Cloudsave|129398400|
|Notifications|8575342|
|Reviews|21076|

### 2.3 RPS по основным методам

Пиковые коэффициенты приняты так:

* внутрисуточный пик х6, так как основная часть активности происходит примерно в 4 часа из суток
* для ручек покупок есть еще сезонный коэффициент 7.46/ 5.85 = 1.275 * 6 = x8

| Метод                   | Действий в день | Средний RPS | Пиковый RPS |
| ----------------------- | --------------: | ----------: | ----------: |
| Поиск   |      68 375 309 |         791 |       6 331 |
| Страница игр        |      46 637 007 |         540 |       4 318 |
| Библиотека          |      124 200 000 |         1 438 |       8 625 |
| Авторизация и регистрация      |      51 257 143 |         593 |       3 560 |
| Корзина |       2 830 866 |          33 |         262 |
| Платежи |         843 032 |          10 |          78 |
| Отзывы         |          21 076 |        0.24 |         2 |
| Облачное сохранение  |      129 398 400 |         1 498 |       8 988 |
| Уведомления | 8 575 342 | 99 | 596|

У аналога Steam основная серверная боль живет не в JSON API магазина. Store/API-контур для MVP укладывается примерно в 5 тыс. avg RPS и 33 тыс. peak RPS. Настоящий highload начинается на контуре доставки билдов, патчей, кэшей, манифестов и объектов Steam Cloud.

### 2.4 Сетевой трафик

Для контура загрузки игр и обновлений используются официальные данные Steam. Valve сообщила, что в 2025 году пользователи Steam скачали 100 exabytes данных. Это соответствует средней нагрузке порядка:

Traffic_cloud = 100 * 10^18 * 8 / 365 / 24 / 3600 = 25.37 Tbps

Таким образом, именно контур delivery/CDN является главным источником сетевой нагрузки в сервисе класса Steam.

Для оценки сетевого трафика storefront-части можно использовать поля в логической бд, которые мы передаем. Расчеты производились исходя из нее.
|Тип запроса|Размер ответа|
|:--:|:--:|
|search|13,9 KiB|
|product|8,1 KiB|
|login|1,05 KiB|
|library|36,1 KiB|
|create|0,5 KiB|
|payment|0,5 KiB|
|review|1,48 KiB|
|notifications|5,4 KiB|
|cloud|0,34 KiB|

Для расчитанных ранее нагрузок:

Traffic_search(avg) = 791 * 14276 * 8/1024^3 = 0,084 Gbps

Traffic_search(peek) = 6331⋅14276⋅8/1024^3 = 0.673 Gbps

...

|Тип трафика|Размер ответа|Средний|Пиковый|
|:--:|:--:|:--:|:--:|
|Каталог и листинг игр|13.9 KiB|	0.084 Gbps|	0.673 Gbps|
|Карточки игр|8.1 KiB|	0.034 Gbps|	0.268 Gbps|
|Авторизация|1.05 |	0.024 Gbps|	0.142 Gbps|
|Библиотека|	0.575 Gbps|	3.45 Gbps|
|Checkout + payment|	0.0027 Gbps|	0.0218 Gbps|
|Reviews|	0.000008 Gbps|	0.000047 Gbps|
|Уведомления|	0.0079 Gbps|	0.0476 Gbps|
|Cloud save|	59.91 Gbps|	359.44 Gbps|
|Storefront/API без cloud save|	21.91 Gbps|	174.05 Gbps|
|Storefront/API с cloud save|	81.81 Gbps|	533.49 Gbps|
|Скачивание игр и обновлений|	25.37 Tbps|	48.8 Tbps|

Из расчётов видно, что даже с учётом cloud save основной объём сетевой нагрузки для сервиса класса Steam создаёт не storefront/API, а именно контур доставки контента. Поэтому при проектировании инфраструктуры необходимо физически и логически разделять application traffic и delivery traffic: использовать отдельные слои балансировки, отдельные пулы серверов и отдельные стратегии кеширования.

### 2.5 Расчет хранилищ

#### OLTP

Объём аккаунтов:
S_user = 132000000⋅2KB ≈ 0.246 TiB
Объём активных сессий:
S_sessions = 69000000⋅1KB ≈ 0.064 TiB
Объём заказов и платежных записей за год:
S_ord/year = 843032⋅365⋅1KB ≈ 0.287 TiB
Объём отзывов за год:
S_reviews/year = 21076⋅365⋅2KB ≈ 0.014 TiB
Годовой прирост записей библиотеки:
S_lib/year = 843032⋅365⋅128B ≈ 0.036 TiB
Каталог и поисковые метаданные:
S_cat = 128950⋅64KB ≈ 0.0077 TiB
Суммарный объём основного логического OLTP-хранилища:
S = 0.246+0.064+0.287+0.014+0.036+0.008 = 0.655 TiB

Добавляем 30% на индексы, служебные поля и т.д. :
S+ = 0.85 TiB

#### Steam Cloud
По данным SteamDB, поддержку Steam Cloud имеют 67 225 игр из 128 950, то есть около 52.1% каталога. Для расчёта принимается, что облачное хранение активно используется той же долей MAU, а средний активный набор сохранений на одного такого пользователя составляет 10 MB. Это именно проектное допущение, а не публичная цифра Valve. Официальная документация Steam Cloud лишь задаёт ограничения: 100 MB на один write/chunk и предупреждение о снижении производительности при размерах свыше 256 MB.

S_cloud = 132000000 * 67225 * 10MB / 128950 = 0.641 PiB

Если хранить предыдущую версию:
S_cloud = 1.282PiB

## 5 Логическая БД
```mermaid
erDiagram
    USERS {
        _ id PK
        _ email "AK"
        _ password_hash
        _ created_at
        _ updated_at
        _ last_login
        _ region
        _ preferences_json
    }
    USER_PROFILES {
        _ id PK
        _ user_id FK "AK"
        _ avatar_url
        _ display_name "AK"
        _ bio
        _ privacy_settings_json
        _ created_at
        _ updated_at
    }
    SESSIONS {
        _ id PK
        _ session_token "AK"
        _ user_id FK
        _ device_info
        _ ip_address
        _ created_at
        _ expires_at
    }
    USER_WALLET {
        _ id PK
        _ user_id FK "AK"
        _ balance_cents
        _ currency
        _ created_at
        _ updated_at
    }
    WALLET_TRANSACTIONS {
        _ id PK
        _ user_wallet_id FK
        _ amount_cents
        _ transaction_type
        _ payment_method
        _ status
        _ created_at
    }
    GAMES {
        _ id PK
        _ title "AK"
        _ developer
        _ publisher
        _ release_date
        _ price_cents
        _ genres_json
        _ tags_json
        _ system_requirements_json
        _ created_at
        _ updated_at
    }
    GAME_MEDIA {
        _ id PK
        _ game_id FK
        _ media_type
        _ media_url
        _ resolution
        _ file_size_bytes
        _ created_at
    }
    USER_LIBRARY {
        _ id PK
        _ user_id FK
        _ game_id FK
        _ owned_bool
        _ installed_bool
        _ cloud_save_enabled
        _ playtime_minutes
        _ last_played
        _ created_at
        _ updated_at
    }
    REVIEWS {
        _ id PK
        _ user_id FK
        _ game_id FK
        _ rating
        _ title
        _ body
        _ helpful_count
        _ created_at
        _ updated_at
    }
    FRIENDS {
        _ id PK
        _ user_id FK
        _ friend_id FK
        _ status
        _ since_date
        _ created_at
    }
    NOTIFICATIONS {
        _ id PK
        _ user_id FK
        _ notification_text
        _ type
        _ status
        _ read_bool
        _ created_at
        _ updated_at
    }
    CLOUD_SAVES {
        _ id PK
        _ user_id FK
        _ game_id FK
        _ file_path
        _ file_size_bytes
        _ checksum
        _ version
        _ created_at
        _ updated_at
    }
    ACHIEVEMENTS {
        _ id PK
        _ game_id FK
        _ achievement_name
        _ description
        _ icon_url
        _ points
        _ created_at
    }
    USER_ACHIEVEMENTS {
        _ id PK
        _ user_id FK
        _ achievement_id FK
        _ unlocked_bool
        _ unlocked_at
        _ progress_percent
        _ created_at
        _ updated_at
    }

    USERS ||--|| USER_PROFILES : has
    USERS ||--o{ SESSIONS : has
    USERS ||--|| USER_WALLET : has
    USERS ||--o{ USER_LIBRARY : owns
    USERS ||--o{ REVIEWS : writes
    USERS ||--o{ FRIENDS : befriends
    USERS ||--o{ NOTIFICATIONS : receives
    USERS ||--o{ CLOUD_SAVES : has
    USERS ||--o{ USER_ACHIEVEMENTS : unlocks
    
    USER_WALLET ||--o{ WALLET_TRANSACTIONS : has
    
    GAMES ||--o{ GAME_MEDIA : contains
    GAMES ||--o{ USER_LIBRARY : in
    GAMES ||--o{ REVIEWS : receives
    GAMES ||--o{ ACHIEVEMENTS : has
    
    USER_LIBRARY }|--|| GAMES : contains
    
    FRIENDS }|--|| USERS : references
    FRIENDS }|--|| USERS : references
    
    ACHIEVEMENTS ||--o{ USER_ACHIEVEMENTS : unlocked_by
```

|Таблица|Описание|
|:--:|:--:|
|users|Таблица для хранения основных данных пользователей: email, хеш пароля, дата регистрации, последний вход, регион, настройки предпочтений (JSON)|
|user_profiles|Таблица профилей пользователей: аватар, отображаемое имя, биография, настройки приватности (JSON). Связь один-к-одному с USERS|
|sessions|Таблица для хранения активных сессий пользователя: токен сессии, информация об устройстве, IP-адрес, время создания и истечения срока действия|
|user_wallet|Таблица кошелька пользователя: баланс в центах, валюта, дата создания и обновления. Связь один-к-одному с USERS|
|wallet_transactions|Таблица транзакций кошелька: сумма, тип транзакции, метод оплаты, статус, дата создания. Связь многие-к-одному с USER_WALLET|
|games|Таблица каталога игр: название, разработчик, издатель, дата релиза, цена, жанры (JSON), теги (JSON), системные требования (JSON)|
|game_media|Таблица медиа-контента игр: тип медиа (скриншот/трейлер/обложка), URL, разрешение, размер файла. Связь многие-к-одному с GAMES|
|user_library|	
Таблица библиотеки пользователя: принадлежность игры, статус установки, облачные сохранения, время в игре, последний запуск. Связь многие-ко-многим USERS-GAMES|
|reviews|Таблица отзывов и оценок: пользователь, игра, рейтинг, заголовок, текст отзыва, количество лайков, дата создания и обновления|
|friends|Таблица дружеских связей: user_id (инициатор), friend_id (друг), статус связи (запрос/принят/заблокирован), дата установления связи. Само-референсная связь на USERS|
|notifications|Таблица уведомлений: текст уведомления, тип, статус, флаг прочтения, дата создания и обновления. Связь многие-к-одному с USERS|
|cloud_saves|	
Таблица облачных сохранений: путь к файлу, размер, контрольная сумма, версия, дата создания и обновления. Связь многие-ко-многим USERS-GAMES|
|achievement|Таблица достижений игр: название достижения, описание, иконка, баллы. Связь многие-к-одному с GAMES|
|user_achievement|Таблица прогресса достижений пользователя: флаг разблокировки, дата разблокировки, процент прогресса. Связь многие-ко-многим USERS-ACHIEVEMENTS|

### Размеры данных и нагрузки на чтение/запись
|Таблица|Расчет|
|:--:|:--:|
|users|16(id) + 255×2(email) + 60×2(password_hash) + 8(created_at) + 8(updated_at) + 8(last_login) + 10×2(region) + 500(preferences_json) = 1 190 байт × 132 млн / 1024³ = **~146 ГБ**|
|user_profiles|16(id) + 16(user_id) + 255×2(avatar_url) + 50×2(display_name) + 500×2(bio) + 300(privacy_settings_json) + 8(created_at) + 8(updated_at) = 1 958 байт × 132 млн / 1024³ = **~240 ГБ**|
|sessions|16(id) + 256×2(session_token) + 16(user_id) + 200×2(device_info) + 45×2(ip_address) + 8(created_at) + 8(expires_at) = 1 050 байт × 138 млн / 1024³ = **~134 ГБ**|
|user_wallet|16(id) + 16(user_id) + 8(balance_cents) + 3×2(currency) + 8(created_at) + 8(updated_at) = 62 байта × 132 млн / 1024³ = **~7.6 ГБ**|
|wallet_transactions|16(id) + 16(user_wallet_id) + 8(amount_cents) + 20×2(transaction_type) + 30×2(payment_method) + 15×2(status) + 8(created_at) = 178 байт × 3.5 млн/мес / 1024³ = **~0.58 ГБ/мес**|
|games|16(id) + 200×2(title) + 100×2(developer) + 100×2(publisher) + 8(release_date) + 8(price_cents) + 200(genres_json) + 300(tags_json) + 500(system_requirements_json) + 8(created_at) + 8(updated_at) = 1 848 байт × 100 000 / 1024³ = **~0.17 ГБ**|
|game_media|16(id) + 16(game_id) + 20×2(media_type) + 500×2(media_url) + 20×2(resolution) + 8(file_size_bytes) + 8(created_at) = 1 128 байт × 500 000 / 1024³ = **~0.52 ГБ**|
|user_library|16(id) + 16(user_id) + 16(game_id) + 1(owned_bool) + 1(installed_bool) + 1(cloud_save_enabled) + 8(playtime_minutes) + 8(last_played) + 8(created_at) + 8(updated_at) = 83 байта × 528 млн / 1024³ = **~41 ГБ**|
|reviews|16(id) + 16(user_id) + 16(game_id) + 4(rating) + 100×2(title) + 2000×2(body) + 8(helpful_count) + 8(created_at) + 8(updated_at) = 4 276 байт × 13.2 млн/мес / 1024³ = **~52 ГБ/мес**|
|friends|16(id) + 16(user_id) + 16(friend_id) + 15×2(status) + 8(since_date) + 8(created_at) = 94 байта × 1.65 млрд / 1024³ = **~144 ГБ**|
|notifications|16(id) + 16(user_id) + 500×2(notification_text) + 30×2(type) + 15×2(status) + 1(read_bool) + 8(created_at) + 8(updated_at) = 1 139 байт × 10.35 млрд/мес / 1024³ = **~11 ТБ/мес**|
|cloud_saves|16(id) + 16(user_id) + 16(game_id) + 500×2(file_path) + 8(file_size_bytes) + 64×2(checksum) + 4(version) + 8(created_at) + 8(updated_at) = 1 204 байта × 276 млн / 1024³ = **~310 ГБ**|
|achievements|16(id) + 16(game_id) + 100×2(achievement_name) + 300×2(description) + 500×2(icon_url) + 4(points) + 8(created_at) = 1 844 байта × 5 млн / 1024³ = **~8.6 ГБ**|
|user_achievements|16(id) + 16(user_id) + 16(achievement_id) + 1(unlocked_bool) + 8(unlocked_at) + 4(progress_percent) + 8(created_at) + 8(updated_at) = 77 байт × 345 млн/мес / 1024³ = **~25 ГБ/мес**|

## 6. Физическая схема БД

### 6.1 Общие принципы физической реализации

При переходе от логической модели к физической используются разные типы хранилищ в зависимости от профиля нагрузки и требований к консистентности:

* PostgreSQL используется для транзакционных и сравнительно компактных данных, где важны строгая консистентность, уникальные ограничения и связи.
* ScyllaDB используется для самых нагруженных пользовательских сущностей с большим количеством чтений и записей, где требуется горизонтальное масштабирование.
* Redis Cluster используется для горячих данных с TTL: активных сессий, счетчиков непрочитанных уведомлений и кешей.
* S3-совместимое object storage используется для бинарных объектов: файлов сохранений и медиа игры.
* OpenSearch используется как денормализованный поисковый индекс по каталогу игр.

На физическом уровне вносятся следующие изменения по сравнению с логической схемой:

1. SESSIONS физически хранятся в Redis, а не в реляционной БД.
2. GAME_MEDIA и CLOUD_SAVES делятся на метаданные и бинарные объекты. Метаданные хранятся в БД, сами файлы лежат в object storage.
3. REVIEWS, FRIENDS, NOTIFICATIONS, USER_LIBRARY, USER_ACHIEVEMENTS денормализуются под основные шаблоны чтения.
4. Для GAMES.title и USER_PROFILES.display_name не вводится физическая уникальность, так как такие ограничения создают ложные конфликты. Уникальность сохраняется по техническим идентификаторам и email.

---

### 6.2 Схема физического размещения данных
```mermaid
flowchart TB
    subgraph PG["PostgreSQL 16 + Patroni"]
        USERS["users"]
        USER_PROFILES["user_profiles"]
        USER_WALLET["user_wallet"]
        WALLET_TRANSACTIONS["wallet_transactions_* (partition by month)"]
        GAMES["games"]
        GAME_MEDIA_META["game_media_meta"]
        ACHIEVEMENTS["achievements"]
    end

    subgraph SCY["ScyllaDB Cluster"]
        USER_LIBRARY["user_library_by_user"]
        REVIEWS_GAME["reviews_by_game"]
        REVIEWS_USER["reviews_by_user"]
        FRIENDS["friends_by_user"]
        NOTIFICATIONS["notifications_by_user"]
        CLOUD_SAVES_META["cloud_saves_meta_by_user_game"]
        USER_ACHIEVEMENTS["user_achievements_by_user"]
    end

    subgraph REDIS["Redis Cluster"]
        SESSIONS["session:{token}"]
        USER_SESSIONS["user_sessions:{user_id}"]
        UNREAD["notifications_unread:{user_id}"]
        HOT_CACHE["hot cache"]
    end

    subgraph S3["S3 / MinIO"]
        GAME_MEDIA_FILES["bucket: game-media"]
        CLOUD_SAVE_FILES["bucket: cloud-saves"]
    end

    subgraph OS["OpenSearch"]
        GAMES_INDEX["games_search_index"]
    end

    USERS --> USER_PROFILES
    USERS --> USER_WALLET
    USER_WALLET --> WALLET_TRANSACTIONS
    GAMES --> GAME_MEDIA_META
    GAMES --> ACHIEVEMENTS

    GAMES --> USER_LIBRARY
    GAMES --> REVIEWS_GAME
    GAMES --> CLOUD_SAVES_META
    ACHIEVEMENTS --> USER_ACHIEVEMENTS

    GAME_MEDIA_META --> GAME_MEDIA_FILES
    CLOUD_SAVES_META --> CLOUD_SAVE_FILES
    GAMES --> GAMES_INDEX
```

---

### 6.3 Выбор СУБД, индексы, денормализация, шардинг и резервирование
| Логическая таблица    | Физическое представление                                        | СУБД             | Индексы                                                                                             | Шардинг / партиционирование                         | Резервирование               |
| --------------------- | --------------------------------------------------------------- | ---------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------- | ---------------------------- |
| users               | users                                                         | PostgreSQL       | PK(id), UNIQUE(email), INDEX(last_login), INDEX(region)                                     | без шардинга, чтение с read replica                 | 1 primary + 2 replicas       |
| user_profiles       | user_profiles                                                 | PostgreSQL       | PK(id), UNIQUE(user_id), INDEX(user_id)                                                       | без шардинга                                        | 1 primary + 2 replicas       |
| sessions            | session:{token}, user_sessions:{user_id}                    | Redis Cluster    | key-based access по токену и user_id                                                                | native Redis sharding по hash slot                  | 3 masters + 3 replicas       |
| user_wallet         | user_wallet                                                   | PostgreSQL       | PK(id), UNIQUE(user_id)                                                                         | без шардинга                                        | 1 primary + 2 replicas       |
| wallet_transactions | wallet_transactions_YYYY_MM                                   | PostgreSQL       | PK(id), INDEX(user_wallet_id, created_at DESC), INDEX(status, created_at)                     | range partition по created_at помесячно           | 1 primary + 2 replicas       |
| games               | games                                                         | PostgreSQL       | PK(id), INDEX(release_date), INDEX(price_cents)                                               | без шардинга                                        | 1 primary + 2 replicas       |
| game_media          | game_media_meta + файлы в bucket: game-media                | PostgreSQL + S3  | PK(id), INDEX(game_id, media_type)                                                              | без шардинга, файлы по префиксу game_id/          | PG replicas + S3 replication |
| user_library        | user_library_by_user                                          | ScyllaDB         | PRIMARY KEY ((user_id), game_id)                                                                  | распределение по partition key user_id            | RF=3                         |
| reviews             | reviews_by_game, reviews_by_user                            | ScyllaDB         | PRIMARY KEY ((game_id), created_at, review_id) и PRIMARY KEY ((user_id), created_at, review_id) | partition key game_id и отдельно user_id        | RF=3                         |
| friends             | friends_by_user                                               | ScyllaDB         | PRIMARY KEY ((user_id), friend_id)                                                                | partition key user_id                             | RF=3                         |
| notifications       | notifications_by_user + unread counter в Redis                | ScyllaDB + Redis | PRIMARY KEY ((user_id), created_at, notification_id)                                              | partition key user_id, TTL по старым уведомлениям | RF=3 + Redis replica         |
| cloud_saves         | cloud_saves_meta_by_user_game + файлы в bucket: cloud-saves | ScyllaDB + S3    | PRIMARY KEY ((user_id, game_id), version)                                                         | partition key (user_id, game_id)                  | RF=3 + S3 replication        |
| achievements        | achievements                                                  | PostgreSQL       | PK(id), INDEX(game_id)                                                                          | без шардинга                                        | 1 primary + 2 replicas       |
| user_achievements   | user_achievements_by_user                                     | ScyllaDB         | PRIMARY KEY ((user_id), game_id, achievement_id)                                                  | partition key user_id                             | RF=3                         |

---

### 6.4 Денормализация физической схемы

Для уменьшения числа тяжелых join-запросов и повышения скорости чтения используются денормализованные представления.

#### 1. Отзывы

Логическая таблица REVIEWS разбивается на две физические таблицы:

* reviews_by_game для чтения отзывов на странице игры;
* reviews_by_user для отображения отзывов конкретного пользователя.

При создании или обновлении отзыва запись пишется сразу в обе таблицы. Это устраняет дорогостоящие выборки по двум разным ключам.

#### 2. Друзья

Таблица FRIENDS хранится как friends_by_user.
Связь дублируется в обе стороны:

* (user_id -> friend_id)
* (friend_id -> user_id)

Это позволяет мгновенно получать список друзей пользователя без обратных join-операций.

#### 3. Уведомления

Уведомления хранятся в notifications_by_user, а количество непрочитанных дополнительно дублируется в Redis-ключ:

* notifications_unread:{user_id}

Это позволяет быстро отдавать счетчик уведомлений без чтения большого раздела ScyllaDB.

#### 4. Облачные сохранения

Физически CLOUD_SAVES разделяется на:

* cloud_saves_meta_by_user_game для метаданных;
* объект в bucket: cloud-saves для бинарного содержимого.

Таким образом БД не нагружается хранением больших файлов, а отвечает только за метаданные, контрольные суммы и версии.

#### 5. Каталог игр

По таблице games строится отдельный денормализованный индекс games_search_index в OpenSearch.
В индекс попадают:

* название игры;
* разработчик;
* издатель;
* теги;
* жанры;
* цена;
* агрегаты по отзывам.

Пользовательский поиск идет в OpenSearch, а PostgreSQL остается источником истины.

---

### 6.5 Детализация физической реализации по таблицам

#### users

Типы полей:

* id — bigint или uuid
* email — varchar(255)
* password_hash — varchar(255)
* created_at, updated_at, last_login — timestamptz
* region — varchar(16)
* preferences_json — jsonb

Особенности:

* таблица хранится в PostgreSQL;
* email индексируется уникально;
* preferences_json не выносится в отдельные таблицы, так как не участвует в частых фильтрах;
* чтение пользовательского профиля возможно с реплик, запись только в primary.

#### user_profiles

Типы полей:

* id, user_id — bigint или uuid
* avatar_url — text
* display_name — varchar(64)
* bio — text
* privacy_settings_json — jsonb

Особенности:

* физическая уникальность по display_name не создается;
* профиль читается в связке с users, но хранится отдельно для уменьшения ширины основной таблицы пользователя.

#### sessions

Физически вместо SQL-таблицы используются структуры Redis:

* session:{token} -> hash:

  * user_id
  * device_info
  * ip_address
  * created_at
  * expires_at
* user_sessions:{user_id} -> set токенов

Особенности:

* TTL устанавливается по expires_at;
* массовое удаление сессий пользователя выполняется по user_sessions:{user_id};
* при перезапуске кластера используется AOF.

#### wallet_transactions

Физически таблица партиционируется по месяцам:

* wallet_transactions_2026_01
* wallet_transactions_2026_02
* и так далее.

Это нужно по двум причинам:

* таблица накапливается во времени;
* типичный запрос почти всегда ограничен временным интервалом.

#### games

Типы полей:

* genres_json, tags_json, system_requirements_json хранятся как jsonb.

Особенности:

* PostgreSQL остается источником истины;
* пользовательский поиск не идет напрямую по JSONB, а выполняется через OpenSearch;
* обновления каталога проталкиваются в индекс асинхронно через event bus.

#### game_media

Метаданные:
* id, game_id, media_type, media_url, resolution, file_size_bytes, created_at

Файлы:

* хранятся в bucket: game-media/{game_id}/{media_id}

Особенности:

* media_url содержит ссылку на object storage или CDN;
* сами изображения и трейлеры не хранятся в PostgreSQL.

#### user_library

Физическая таблица в ScyllaDB:

PRIMARY KEY ((user_id), game_id)

Колонки:

* owned_bool
* installed_bool
* cloud_save_enabled
* playtime_minutes
* last_played
* created_at
* updated_at

Особенности:

* основной запрос это “показать библиотеку пользователя”;
* выбран partition key user_id, потому что библиотека читается целиком по пользователю;
* наличие game_id в clustering key позволяет быстро проверить владение конкретной игрой.

#### reviews

Физические таблицы:

1. reviews_by_game

   * PRIMARY KEY ((game_id), created_at, review_id)

2. reviews_by_user

   * PRIMARY KEY ((user_id), created_at, review_id)

Особенности:

* обе таблицы заполняются синхронно из одного события;
* сортировка по created_at DESC позволяет быстро отдавать последние отзывы;
* отдельные агрегаты helpful_count, rating_avg, reviews_count можно хранить в кешируемой таблице или Redis.

#### friends

Физическая таблица:

PRIMARY KEY ((user_id), friend_id)

Колонки:

* status
* since_date
* created_at

Особенности:

* связи записываются в обе стороны;
* запрос “список друзей пользователя” читается одной операцией по partition key.

#### notifications

Физическая таблица:

PRIMARY KEY ((user_id), created_at, notification_id)

Колонки:

* notification_text
* type
* status
* read_bool
* created_at
* updated_at

Особенности:

* старые уведомления удаляются по TTL, например через 90 дней;
* счетчик непрочитанных хранится отдельно в Redis;
* горячая выборка выполняется по пользователю и временному диапазону.

#### cloud_saves

Физические сущности:

1. cloud_saves_meta_by_user_game

   * PRIMARY KEY ((user_id, game_id), version)

2. объект в bucket: cloud-saves/{user_id}/{game_id}/{version}

Колонки метаданных:

* file_path
* file_size_bytes
* checksum
* version
* created_at
* updated_at

Особенности:

* бинарный blob не хранится в БД;
* checksum используется для проверки целостности;
* новые версии добавляются append-only.

#### achievements

Таблица остается в PostgreSQL, так как данные сравнительно компактны и редко изменяются.

Индекс:

* INDEX(game_id)

#### user_achievements

Физическая таблица в ScyllaDB:

PRIMARY KEY ((user_id), game_id, achievement_id)

Колонки:

* unlocked_bool
* unlocked_at
* progress_percent
* created_at
* updated_at

Особенности:

* выборка идет по пользователю и игре;
* game_id дублируется физически, чтобы не делать лишние join с таблицей achievements.

---

### 6.6 Балансировка запросов и мультиплексирование подключений

| Хранилище     | Балансировка запросов                                  | Мультиплексирование подключений        |
| ------------- | ------------------------------------------------------ | -------------------------------------- |
| PostgreSQL    | HAProxy/Patroni, разделение primary/replica reads      | PgBouncer в режиме transaction pooling |
| ScyllaDB      | token-aware и shard-aware routing на клиенте           | нативный пул соединений драйвера       |
| Redis Cluster | cluster-aware routing по hash slot                     | встроенный connection pool клиента     |
| S3 / MinIO    | через CDN и S3 API endpoint                            | HTTP keep-alive и multipart upload     |
| OpenSearch    | round-robin по data nodes или через coordinating nodes | connection pool HTTP-клиента           |

---

### 6.7 Клиентские библиотеки и интеграции

Если backend реализуется на Go, используются следующие библиотеки:

| Хранилище  | Библиотека / интеграция               |
| ---------- | ------------------------------------- |
| PostgreSQL | pgx + PgBouncer                   |
| ScyllaDB   | gocql или Scylla shard-aware driver |
| Redis      | go-redis                            |
| S3 / MinIO | minio-go или AWS SDK S3             |
| OpenSearch | opensearch-go                       |
Если backend реализуется на Python, аналогичный набор:

| Хранилище  | Библиотека / интеграция |
| ---------- | ----------------------- |
| PostgreSQL | asyncpg / psycopg   |
| ScyllaDB   | cassandra-driver      |
| Redis      | redis-py              |
| S3 / MinIO | boto3 / minio       |
| OpenSearch | opensearch-py         |

---

### 6.8 Схема резервного копирования

| Хранилище  | Схема бэкапа                                                                    |
| ---------- | ------------------------------------------------------------------------------- |
| PostgreSQL | ежедневный full backup + непрерывная архивация WAL, PITR 30 дней                |
| ScyllaDB   | ежедневные snapshots + выгрузка в object storage                                |
| Redis      | AOF everysec + репликация мастеров                                            |
| S3 / MinIO | versioning + cross-region replication                                           |
| OpenSearch | snapshots в S3, индекс при необходимости пересобирается из PostgreSQL и событий |

---

### 6.9 Итоговое распределение таблиц по хранилищам

| Хранилище     | Таблицы / сущности                                                                                                                                                     |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PostgreSQL    | users, user_profiles, user_wallet, wallet_transactions, games, game_media_meta, achievements                                                             |
| ScyllaDB      | user_library_by_user, reviews_by_game, reviews_by_user, friends_by_user, notifications_by_user, cloud_saves_meta_by_user_game, user_achievements_by_user |
| Redis Cluster | session:{token}, user_sessions:{user_id}, notifications_unread:{user_id}, hot cache                                                                              |
| S3 / MinIO    | game-media, cloud-saves                                                                                                                                            |
| OpenSearch    | games_search_index                                                                                                                                                   |

---

## 8. Технологии
| Технология |	Область применения |	Причина выбора |
|:--:|:--:|:--:|
|Go|	Backend|	высокая производительность, простая эксплуатация, зрелая экосистема|
|PostgreSQL|OLTP|	транзакции, платежи, entitlements|
|RedisCluster|	cache/session|	Подходит для хранения короткоживущих данных: сессий, токенов, счетчиков непрочитанных уведомлений, rate-limit ключей, кэша популярных карточек игр и других hot data. Кластерный режим позволяет горизонтально масштабировать систему и не перегружать основную БД частыми мелкими запросами|
|ScyllaDB / Cassandra|	wide-column OLTP|Хорошо подходит для библиотеки пользователя, уведомлений, достижений, статистики, отзывов и других больших сущностей, читаемых по user_id или game_id. Позволяет горизонтально масштабироваться на много узлов и выдерживать высокий поток операций|
|OpenSearch|	catalog search|	полнотекстовый поиск и фильтры|
|S3-compatible storage|	Объектное хранилище|	Используется для хранения крупных бинарных объектов: медиафайлов игр, патчей, depot-объектов, трейлеров, скриншотов и облачных сохранений|
|Kafka / Redpanda|	асинхронное взаимодействие|	Позволяет развязать сервисы между собой и обрабатывать операции асинхронно: покупки, обновление библиотеки, отправку уведомлений, обновление поискового индекса, обновление рекомендаций и аналитических витрин|
|ClickHouse|	Аналитика|	Используется для хранения и обработки больших объемов событийной аналитик|
|NGINX / Envoy|	edge/L7|	Используются на входе в систему для TLS termination, маршрутизации запросов, балансировки нагрузки, кэширования и базовой защиты от перегрузки|
|Prometheus + Grafana|	Мониторинг и обработка|	метрики и алерты|
|Jaeger / Tempo|	tracing|	Используются для распределенной трассировки в микросервисной архитектуре. Позволяют понять, как запрос проходит через API Gateway, backend-сервисы, очереди и базы данных, а также находить узкие места и деградации по задержке|
|Kubernetes|	оркестрация|	Используется для развертывания, масштабирования и обновления сервисов|


## Источники данных
- https://steamdb.info/app/753/charts
- https://steamdb.info/app/753/charts/#max(для выяснения регистрации и авторизации)
- https://icon-era.com/statistics/steam-game-statistics/
- https://worldpopulationreview.com/country-rankings/steam-users-by-country
- https://store.steampowered.com/stats/stats(офф сайт: пользователей залогинино)
- 

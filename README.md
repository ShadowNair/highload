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

Дальше все расчеты опираются на следующие публичные цифры:

* выручка Steam за 2024 год: $10.8 млрд;
* доля именно game sales в выручке: 61%;
* средняя цена топовых продаваемых игр на Steam в 2025 году: $21.41;
* средний ecommerce conversion rate: 2.58%;
* доля сессий, доходящих до product page: около 50%;
* среднее число страниц за сессию для ecommerce: 2.6;
* средний cart abandonment rate: 70.22%;
* типичный диапазон review-to-sales ratio для Steam-игр: примерно 1 отзыв на 30-60 продаж;
* средний weekly playtime на платформе: 7.1 часа;
* медианный пользователь Steam за год играет в 4 игры, а медианная серия активных дней составляет 6 дней. ([IconEra][2])

Для отзывов принимаю 1 отзыв на 40 покупок как рабочее проектное значение внутри диапазона 30-60. Для библиотеки, логина и cloud save добавляю консервативные проектные коэффициенты, потому что публичной нормальной статистики по этим операциям Valve не публикует.

### 2.2 Продуктовые метрики

Покупки в день

[
Purchases/day = \frac{10.8\text{ млрд} \times 0.61}{21.41 \times 365} \approx 843,032
]

Сессии магазина в день

[
Store\ sessions/day = \frac{843,032}{0.0258} \approx 32.68\text{ млн}
]

Просмотры карточек игры в день

[
Product\ views/day = 32.68\text{ млн} \times 0.5 \approx 16.34\text{ млн}
]

Запросы поиска/листинга каталога в день

[
Catalog\ page\ views/day = 32.68\text{ млн} \times (2.6 - 0.5) \approx 68.62\text{ млн}
]

Отзывы в день

[
Reviews/day = \frac{843,032}{40} \approx 21,076
]

Для остальных действий приняты проектные допущения:
* библиотека открывается в среднем 1.2 раза на DAU в день;
* логин/новая авторизационная сессия происходит 0.9 раза на DAU в день;
* cloud save используют 20% DAU, и у такой сессии в среднем есть 2 sync-операции: при запуске и при завершении игры.

| Метрика                | Формула                           |    Значение |
| ---------------------- | --------------------------------- | ----------: |
| MAU                    | исходное значение                 | 147 000 000 |
| DAU                    | исходное значение                 |  69 000 000 |
| Покупки в день         | (10.8e9 × 0.61) / (21.41 × 365) |     843 032 |
| Store sessions/day     | purchases / 0.0258              |  32 675 659 |
| Product views/day      | store_sessions × 0.5            |  16 337 829 |
| Catalog page views/day | store_sessions × 2.1            |  68 618 884 |
| Reviews/day            | purchases / 40                  |      21 076 |
| Library opens/day      | DAU × 1.2                       |  82 800 000 |
| Login/day              | DAU × 0.9                       |  62 100 000 |
| Cloud save sync/day    | DAU × 0.2 × 2                   |  27 600 000 |

### 2.3 RPS по основным методам

Пиковые коэффициенты приняты так:

* каталог: ×8, потому что распродажи и баннерный трафик резко разгоняют browse-нагрузку;
* карточка игры: ×10, потому что релизы и скидки концентрируют трафик на ограниченном числе hot keys;
* библиотека и логин: ×4, вечерний пик и выходные;
* checkout: ×8, распродажи;
* review: ×6;
* cloud save: ×4.

| Метод                   | Действий в день | Средний RPS | Пиковый RPS |
| ----------------------- | --------------: | ----------: | ----------: |
| GET /catalog/search   |      68 618 884 |         794 |       6 354 |
| GET /game/{id}        |      16 337 829 |         189 |       1 891 |
| GET /library          |      82 800 000 |         958 |       3 833 |
| POST /auth/login      |      62 100 000 |         719 |       2 875 |
| POST /checkout/create |       2 830 866 |          33 |         262 |
| POST /payment/confirm |         843 032 |          10 |          78 |
| POST /review          |          21 076 |        0.24 |         1.5 |
| POST /cloudsave/sync  |      27 600 000 |         319 |       1 278 |

Суммарная пиковая API-нагрузка для MVP получается порядка 15 тыс. RPS без учета выдачи бинарных билдов. Основной highload тут живет не в JSON API, а в доставке игровых файлов. Исходные входные метрики для расчета взяты из публичной статистики Steam и ecommerce-бенчмарков. ([IconEra][2])

### 2.4 Сетевой трафик

По Steam Year in Review 2025 пользователи сервиса такого класса скачали 100 exabytes данных за 2025 год, то есть в среднем 274 PB/day. Это соответствует средней нагрузке порядка 25.4 Tbps только на installs/updates. Сумма региональных пиков со страницы Steam Download Stats дает ориентир по глобальному пику около 58.6 Tbps. ([Steam Community][3])

Для API и cloud save принимаю следующие проектные средние размеры полезной нагрузки:

* search/list response: 60 KB;
* game page: 120 KB;
* library: 50 KB;
* login response: 5 KB;
* checkout/payment: 8 KB;
* review write: 4 KB;
* cloud save blob: 5 MB.

| Тип трафика                | Средний трафик | Пиковый трафик |
| -------------------------- | -------------: | -------------: |
| Установка и обновление игр |      25.4 Tbps |      58.6 Tbps |
| Cloud save sync            |      13.4 Gbps |      53.6 Gbps |
| JSON API суммарно          |       1.0 Gbps |       6.7 Gbps |

Вывод неприятный, но полезный: download/update CDN полностью доминирует по сети, а API и БД доминируют по числу операций, консистентности и hot-key нагрузке.

---

### - GET /api/catalog/search
При запуске Steam точка входа каталог(сделано в целях привлечения пользователей к продуктам и их покупке) => __~55% пользователей__ как минимум один раз реализуют запрос + __~50% от 55%__ продолжает просмотр продуктов и просматривает минимум 5 страниц. Также во время распродаж, скидок, акций достигается пик количества запросов(коэффициент пика = 40)
__RPS_среднее = (0,55 * DAU + 0,55 * 0,5 * DAU * 5) / (24 * 60 * 60) = 1537__ 
__RPS_пиковое = RPS_среднее * 40 = 61493__

### - GET /api/product/{id}
Как выше сказано, пользователей, которые заходят для просмотра продукта, __0,55 * 0,5 * DAU = ~18975000__. Просматривают примерно 5 страниц различных игр для сравнения и последующей покупки или выбора => __18975000 * 5 = 94875000__ запросов за день
В день релиза долгождпнного продукта может произойти БУМ, в следствие чего лягут сервера, данного сценария нам надо избежать
__RPS_среднее = 94875000/(24 * 60 * 60) = 1098__
__RPS_пиковое = RPS_среднее * 29 = 31844__

### - POST /api/review
Для расчета ручки написания отзыва подсчитано среднее количество отзывов игр ~8240(В статистике стим есть количество отзывов за последний месяц) дальше умножили на 1000(топ игр) и добавили количество отзывов, которые улучшают статистику(у CS2 93106 отзывов) = __8 335 018 запросов в день__
Достигает пиковых значений после завершения прохождения игр, то есть по вечерам и выходным, также большое количество отзывов после релиза продукта
__RPS_среднее = 8 335 018 / (30 * 24 * 60 * 60) = 3__
__RPS_пиковое = RPS_среднее * 40 = 120__

### - GET /api/library
Каждый пользователь заходит в библиотеку. Внесем коэффициент 1.8 , который отвечает за перерыв между сессиями, смена аккаунта и тому подбное. Пиковый коэффициент вводится ввиду того, что сессий будет больше вечером из-за рабочего дня или выходные = 20.
__RPS_среднее = (69 000 000 * 1.8) / (24 * 60 * 60) = 1438__
__RPS_пиковое = RPS_среднее * 20 = 28750__

### - POST /api/library/install
Скачка игры, довольно редкая функция, так как в среднем пользователь сачивает 4 игры в месяц.
Пиковый коэффициент зависит от праздников, релизов, выходных ~200
__RPS_среднее = (4 / 30) * DAU / (24 * 60 * 60) = 106__
__RPS_пиковое = RPS_среднее * 200 = 21 296__

### - POST /api/cloudsave/sync
Мало игр использует облачное сохранение, однако игры, у которых пиковое значение используют этот функционал: CS2, Dota2, PUBG and other. Следую ранее сказанному примерно 10кк пользователей играют в игры использующее облачное сохранение(из стим дб).
Пиковый коэффициент в отпускные сроки, выходные и вечера = 6
__RPS_среднее = 10 000 000 / (24 * 60 * 60) = 115__
__RPS_пиковое = RPS_среднее * 6 = 694__

### - GET /api/notifications
Пользователей, которые проверяют уведомления примерно 80% ввиду того, что приходят как скидки, сообщения от других пользователей и уведомление о входе в аккаунт. В среднем 5 уведомлений.
Пиковый коэффициент: 5(вечерние сессии)
__RPS_среднее = (69 000 000 * 5 * 0.8) / (24 * 60 * 60) = 3194__
__RPS_пиковое = RPS_среднее * 5 = 15 973__

### - POST /api/payment/process
Оплата производится крайне редко, так как емть много бесплатных игр. Примерно 0.17% от DAU, однако пиковое значение может быть очень большим. Пиковый коэффициент: 1000
__RPS_среднее = (69 000 000 * 0,0017) / (24 * 60 * 60) = ~2__
__RPS_пиковое = RPS_пиковое * 1000 = 2000__

### - POST /api/auth/login
1.3 пользователя может несколько раз авторизовываться в день. Пиковое значение постраспрадажное = 2
__RPS_среднее = (69 000 000 * 1.3) / (24 * 60 * 60) = 1039__
__RPS_пиковое = RPS_среднее * 2 = 2076__

## 2.3 Технические метрики: RPS по методам

| Метод / Эндпоинт | Формула расчёта (средний) | Средний RPS | Пиковый RPS | Коэф. пика | Обоснование пика |
|-----------------|---------------------------|-------------|-------------|------------|-----------------|
| `GET /api/catalog/search` | `(0.55 × DAU + 0.55 × 0.5 × DAU × 5) / 86 400` | **1 537** | **45 000–60 000** | ×30–40 | Распродажи, релизы, утренний трафик |
| `GET /api/product/{id}` | `(0.55 × 0.5 × DAU × 5) / 86 400` | **1 098** | **30 000–35 000** | ×29–32 | Релиз ожидаемого тайтла, сравнение игр |
| `POST /api/review` | `8 335 018 / 30 * 86 400` | **3** | **120** | ×40 | Вечерние сессии, завершение игр, пост-релиз |
| `GET /api/library` | `(DAU × 1.8) / 86 400` | **1 438** | **25 000–30 000** | ×20 | Вечерний пик после рабочего дня, выходные |
| `POST /api/library/install` | `(4/30 × DAU) / 86 400` | **106** | **20 000–25 000** | ×200 | Распродажи, бесплатные раздачи, крупные релизы |
| `POST /api/cloudsave/sync` | `10 000 000 / 86 400` | **115** | **600–800** | ×6 | Вечерние сессии, выходные, отпускные периоды |
| `GET /api/notifications` | `(0.8 × DAU × 5) / 86 400` | **3 194** | **15 000–18 000** | ×5 | Утренние/вечерние проверки, пуш-триггеры |
| `POST /api/payment/process` | `(0.0017 × DAU) / 86 400` | **~1.4** | **400–600** | ×300 | Крупные распродажи (консервативная оценка) |
| `POST /api/auth/login` | `(DAU × 1.3) / 86 400` | **1 039** | **3 000–5 000** | ×3–5 | Утренний вход, пост-распродажный трафик, 2FA |
| **ИТОГО** | — | **~8 600** | **~142 000–183 000** | — | Суммарная нагрузка на API-шлюз |


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

### 6.1 Выбор СУБД по таблицам

| Логическая сущность                            | Физическое хранилище         | Причина                                                             |
| ---------------------------------------------- | ---------------------------- | ------------------------------------------------------------------- |
| users, orders, payments, game_prices   | PostgreSQL                   | сильная консистентность, транзакции                                 |
| sessions                                     | Redis Cluster                | TTL, низкая задержка                                                |
| library_items                                | ScyllaDB                     | огромный объем, чтение по user_id, горизонтальное масштабирование |
| reviews                                      | ScyllaDB                     | write-heavy, hot partitions по game_id                            |
| cloud_save_meta                              | ScyllaDB                     | быстрый доступ по (user_id, game_id)                              |
| cloud_save_blob, game_builds, game_media | S3-compatible Object Storage | дешево и масштабируемо для blob-данных                              |
| search_index                                 | OpenSearch                   | полнотекстовый поиск, фильтры, фасеты                               |
| event_log                                    | Kafka                        | асинхронная шина событий                                            |
| аналитика                                      | ClickHouse                   | дешевые агрегации по огромному event stream                         |

### 6.2 Индексы, шардинг, резервирование

| Сущность          | Ключ/индексы                                   | Шардирование            | Резервирование       |
| ----------------- | ---------------------------------------------- | ----------------------- | -------------------- |
| users           | PK user_id, UNIQUE email                   | hash by user_id       | primary + 2 replicas |
| orders          | PK order_id, IDX (user_id, created_at)     | hash by user_id       | primary + 2 replicas |
| payments        | PK payment_id, UNIQUE provider_txn_id      | hash by order_id      | primary + 2 replicas |
| library_items   | PK ((user_id), game_id)                      | by user_id            | RF=3                 |
| reviews         | PK ((game_id), created_at, review_id)        | by game_id            | RF=3                 |
| cloud_save_meta | PK ((user_id, game_id), version_ts)          | by (user_id, game_id) | RF=3                 |
| search_index    | doc id game_id, inverted index on title/tags | 24 shards               | 1 replica            |
| object storage    | object key                                     | bucket by region/game   | EC 8+4               |

### 6.3 Бэкапы и доступ

* PostgreSQL: daily full + WAL archiving + PITR 30 days.
* ScyllaDB: incremental snapshots + restore drills.
* Object storage: versioning + cross-region replication for critical buckets.
* Redis: AOF + replica.
* Kafka: replication factor 3.

Балансировка подключений:

* PostgreSQL через PgBouncer;
* Redis через cluster-aware client;
* Scylla/OpenSearch через native driver и token-aware routing.

---

## Источники данных
- https://steamdb.info/app/753/charts
- https://steamdb.info/app/753/charts/#max(для выяснения регистрации и авторизации)
- https://icon-era.com/statistics/steam-game-statistics/
- https://worldpopulationreview.com/country-rankings/steam-users-by-country
- https://store.steampowered.com/stats/stats(офф сайт: пользователей залогинино)
- 

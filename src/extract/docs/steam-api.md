# Справочник Steam API (Микродокументация)

https://github.com/Revadike/InternalSteamWebAPI

### ⚠️ Важное ограничение (Rate Limit)

* **Лимит:** Около 200–300 запросов за 5 минут.
* **Защита:** При частых запросах Steam вернет ошибку `429 Too Many Requests`.

---

### 1. Основная информация по игре (AppDetails)

Возвращает жанры, описание, цены, скриншоты и разработчиков.

* **URL:** `https://store.steampowered.com/api/appdetails`
* **Метод:** GET
* **Параметры:**
  * `appids` (обязательный) — ID игры.
  * `cc` — код страны для валюты (например, `ru`, `us`, `kz`).
  * `l` — язык текста (например, `russian`).
* **Пример:** `https://store.steampowered.com/api/appdetails?appids={ID}&cc=ru&l=russian`

### 2. Отзывы пользователей (AppReviews)

Возвращает текстовые обзоры и общую оценку игры.

* **URL:** `https://store.steampowered.com/appreviews/{ID}`
* **Метод:** GET
* **Параметры:** `json=1` (обязательный для формата JSON), `language=russian`.
* **Пример:** `https://store.steampowered.com/appreviews/{ID}?json=1&language=russian`

### 3. Гистограмма и динамика оценок

Возвращает данные для построения графика изменения оценок по дням. Полезно для отслеживания ревью-бомбинга.

* **URL:** `https://store.steampowered.com/appreviewhistogram/{ID}`
* **Метод:** GET
* **Параметры:** `l=russian`
* **Пример:** `https://store.steampowered.com/appreviewhistogram/{ID}?l=russian`

### 4. Текущий онлайн (Current Players)

Возвращает число людей, у которых игра запущена в данную секунду. Относится к официальному Web API, но работает без ключа.

* **URL:** `https://api.steampowered.com/ISteamUserStats/GetNumberOfCurrentPlayers/v1/`
* **Метод:** GET
* **Параметры:** `appid` (обязательный).
* **Пример:** `https://api.steampowered.com/ISteamUserStats/GetNumberOfCurrentPlayers/v1/?appid={ID}`

### 5. Данные о DLC (Дополнениях)

Если у игры есть скачиваемый контент, эндпоинт вернет массив со всеми существующими DLC, их ценами и статусом.

* **URL:** `https://store.steampowered.com/dlc/{ID}/ajaxgetdlclist`
* **Метод:** GET
* **Параметры:** Нет.
* **Пример:** `https://store.steampowered.com/dlc/{ID}/ajaxgetdlclist`

### 6. Достижения (Ачивки)

Возвращает список всех достижений игры, их названия, иконки и глобальный процент игроков, которые их открыли.

* **URL:** `https://api.steampowered.com/ISteamUserStats/GetGlobalAchievementPercentagesForApp/v2/`
* **Метод:** GET
* **Параметры:** `gameid` (обязательный).
* **Пример:** `https://api.steampowered.com/ISteamUserStats/GetGlobalAchievementPercentagesForApp/v2/?gameid={ID}`

### 7. Лента новостей и патчноутов (News)

Возвращает список официальных объявлений от разработчиков, обновлений, патчей и статей, привязанных к игре.

* **URL:** `https://api.steampowered.com/ISteamNews/GetNewsForApp/v2/`
* **Метод:** GET
* **Параметры:** `appid` (обязательный), `count` (задает количество новостей в ответе).
* **Пример:** `https://api.steampowered.com/ISteamNews/GetNewsForApp/v2/?appid={ID}&count=5`

### 8. Список поддерживаемых методов Web API (GetSupportedAPIList)

Возвращает полный официальный список всех доступных интерфейсов, методов и параметров Steamworks Web API. 

* **URL:** `https://api.steampowered.com/ISteamWebAPIUtil/GetSupportedAPIList/v1/`
* **Метод:** GET
* **Параметры:** `key` (опционально — для вывода скрытых методов вашего аккаунта разработчика).
* **Пример:** `https://api.steampowered.com/ISteamWebAPIUtil/GetSupportedAPIList/v1/?key={API_KEY}`

### 9. Полный список приложений в магазине (IStoreService -> GetAppList)

Современный метод для получения актуального списка всех игр и приложений.

* **URL:** `https://api.steampowered.com/IStoreService/GetAppList/v1/`
* **Метод:** GET
* **Параметры:**
  * `key` (опционально) — Web API Key.
  * `max_results` (int, по умолчанию 10000) — количество записей за запрос.
  * `last_appid` (int, опционально) — ID последней игры из предыдущего запроса для получения следующей страницы.
* **Пример:** `https://api.steampowered.com/IStoreService/GetAppList/v1/?max_results=10000`
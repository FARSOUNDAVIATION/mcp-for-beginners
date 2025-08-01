<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "151265c9a2124d7c53e04d16ee3fb73b",
  "translation_date": "2025-07-17T13:01:04+00:00",
  "source_file": "05-AdvancedTopics/web-search-mcp/README.md",
  "language_code": "uk"
}
-->
# Урок: Створення MCP-сервера для веб-пошуку

У цьому розділі показано, як створити реального AI-агента, який інтегрується з зовнішніми API, працює з різними типами даних, керує помилками та координує кілька інструментів — усе це у форматі, готовому до використання в продакшені. Ви дізнаєтеся:

- **Інтеграція з зовнішніми API, що потребують автентифікації**
- **Обробка різноманітних типів даних з кількох кінцевих точок**
- **Надійне керування помилками та стратегії логування**
- **Оркестрація кількох інструментів в одному сервері**

Наприкінці ви отримаєте практичний досвід із шаблонів і найкращих практик, необхідних для просунутих AI-додатків на базі LLM.

## Вступ

У цьому уроці ви навчитеся створювати просунутий MCP-сервер і клієнт, які розширюють можливості LLM за допомогою актуальних веб-даних у реальному часі через SerpAPI. Це важливий навик для розробки динамічних AI-агентів, які можуть отримувати актуальну інформацію з інтернету.

## Цілі навчання

Після проходження уроку ви зможете:

- Безпечно інтегрувати зовнішні API (наприклад, SerpAPI) у MCP-сервер
- Реалізувати кілька інструментів для веб-, новинного, продуктовго пошуку та Q&A
- Парсити та форматувати структуровані дані для використання LLM
- Ефективно обробляти помилки та керувати лімітами API
- Створювати та тестувати як автоматизовані, так і інтерактивні MCP-клієнти

## MCP-сервер для веб-пошуку

У цьому розділі представлено архітектуру та функції MCP-сервера для веб-пошуку. Ви побачите, як FastMCP і SerpAPI працюють разом, щоб розширити можливості LLM за допомогою актуальних веб-даних.

### Огляд

Ця реалізація включає чотири інструменти, які демонструють здатність MCP безпечно та ефективно працювати з різноманітними завданнями, що базуються на зовнішніх API:

- **general_search**: для широкого веб-пошуку
- **news_search**: для останніх новин
- **product_search**: для даних електронної комерції
- **qna**: для питань і відповідей

### Особливості
- **Приклади коду**: містить мовно-специфічні блоки коду для Python (легко розширювані на інші мови) з використанням code pivots для кращої зрозумілості

### Python

```python
# Example usage of the general_search tool
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client

async def run_search():
    server_params = StdioServerParameters(
        command="python",
        args=["server.py"],
    )
    async with stdio_client(server_params) as (reader, writer):
        async with ClientSession(reader, writer) as session:
            await session.initialize()
            result = await session.call_tool("general_search", arguments={"query": "open source LLMs"})
            print(result)
```

---

Перед запуском клієнта корисно зрозуміти, що робить сервер. Файл [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py) реалізує MCP-сервер, який надає інструменти для веб-, новинного, продуктовго пошуку та Q&A, інтегруючись із SerpAPI. Він обробляє вхідні запити, керує викликами API, парсить відповіді та повертає структуровані результати клієнту.

Повну реалізацію можна переглянути у файлі [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py).

Нижче наведено короткий приклад того, як сервер визначає та реєструє інструмент:

### Python Server

```python
# server.py (excerpt)
from mcp.server import MCPServer, Tool

async def general_search(query: str):
    # ...implementation...

server = MCPServer()
server.add_tool(Tool("general_search", general_search))

if __name__ == "__main__":
    server.run()
```

---

- **Інтеграція зовнішніх API**: демонструє безпечне керування ключами API та зовнішніми запитами
- **Парсинг структурованих даних**: показує, як перетворювати відповіді API у формати, зручні для LLM
- **Обробка помилок**: надійне керування помилками з відповідним логуванням
- **Інтерактивний клієнт**: включає як автоматизовані тести, так і інтерактивний режим для тестування
- **Управління контекстом**: використовує MCP Context для логування та відстеження запитів

## Вимоги

Перед початком переконайтеся, що ваше середовище налаштоване правильно, виконавши наступні кроки. Це гарантує, що всі залежності встановлені, а ключі API налаштовані для безперебійної розробки та тестування.

- Python 3.8 або новіша версія
- Ключ API SerpAPI (зареєструйтесь на [SerpAPI](https://serpapi.com/) — доступний безкоштовний тариф)

## Встановлення

Щоб почати, виконайте наступні кроки для налаштування середовища:

1. Встановіть залежності за допомогою uv (рекомендовано) або pip:

```bash
# Using uv (recommended)
uv pip install -r requirements.txt

# Using pip
pip install -r requirements.txt
```

2. Створіть файл `.env` у корені проекту з вашим ключем SerpAPI:

```
SERPAPI_KEY=your_serpapi_key_here
```

## Використання

MCP-сервер для веб-пошуку — це основний компонент, який надає інструменти для веб-, новинного, продуктовго пошуку та Q&A, інтегруючись із SerpAPI. Він обробляє вхідні запити, керує викликами API, парсить відповіді та повертає структуровані результати клієнту.

Повну реалізацію можна переглянути у файлі [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py).

### Запуск сервера

Щоб запустити MCP-сервер, використайте таку команду:

```bash
python server.py
```

Сервер працюватиме як MCP-сервер на основі stdio, до якого клієнт може підключитися безпосередньо.

### Режими клієнта

Клієнт (`client.py`) підтримує два режими взаємодії з MCP-сервером:

- **Звичайний режим**: запускає автоматизовані тести, які перевіряють усі інструменти та їх відповіді. Це корисно для швидкої перевірки працездатності сервера та інструментів.
- **Інтерактивний режим**: запускає меню, де ви можете вручну вибирати інструменти, вводити власні запити та бачити результати в реальному часі. Ідеально підходить для дослідження можливостей сервера та експериментів з різними запитами.

Повну реалізацію можна переглянути у файлі [`client.py`](../../../../05-AdvancedTopics/web-search-mcp/client.py).

### Запуск клієнта

Щоб запустити автоматизовані тести (це автоматично запустить сервер):

```bash
python client.py
```

Або запустіть у інтерактивному режимі:

```bash
python client.py --interactive
```

### Тестування різними способами

Існує кілька способів тестувати та взаємодіяти з інструментами сервера, залежно від ваших потреб і робочого процесу.

#### Написання власних тестових скриптів з MCP Python SDK
Ви також можете створювати власні тестові скрипти, використовуючи MCP Python SDK:

# [Python](../../../../05-AdvancedTopics/web-search-mcp)

```python
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client

async def test_custom_query():
    server_params = StdioServerParameters(
        command="python",
        args=["server.py"],
    )
    
    async with stdio_client(server_params) as (reader, writer):
        async with ClientSession(reader, writer) as session:
            await session.initialize()
            # Call tools with your custom parameters
            result = await session.call_tool("general_search", 
                                           arguments={"query": "your custom query"})
            # Process the result
```

---

У цьому контексті "тестовий скрипт" означає власну програму на Python, яку ви пишете як клієнт для MCP-сервера. Замість формального юніт-тесту цей скрипт дозволяє програмно підключатися до сервера, викликати будь-який інструмент із потрібними параметрами та переглядати результати. Цей підхід корисний для:
- Прототипування та експериментів із викликами інструментів
- Перевірки реакції сервера на різні вхідні дані
- Автоматизації повторних викликів інструментів
- Створення власних робочих процесів або інтеграцій на базі MCP-сервера

Ви можете швидко перевірити нові запити, налагоджувати поведінку інструментів або використовувати цей скрипт як основу для більш складної автоматизації. Нижче наведено приклад використання MCP Python SDK для створення такого скрипта:

## Опис інструментів

Ви можете використовувати наступні інструменти, які надає сервер, для виконання різних типів пошуку та запитів. Кожен інструмент описано з параметрами та прикладами використання.

Цей розділ містить деталі про кожен доступний інструмент та їх параметри.

### general_search

Виконує загальний веб-пошук і повертає відформатовані результати.

**Як викликати цей інструмент:**

Ви можете викликати `general_search` зі свого скрипта за допомогою MCP Python SDK або інтерактивно через Inspector чи інтерактивний режим клієнта. Ось приклад коду з SDK:

# [Python Example](../../../../05-AdvancedTopics/web-search-mcp)

```python
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client

async def run_general_search():
    server_params = StdioServerParameters(
        command="python",
        args=["server.py"],
    )
    async with stdio_client(server_params) as (reader, writer):
        async with ClientSession(reader, writer) as session:
            await session.initialize()
            result = await session.call_tool("general_search", arguments={"query": "latest AI trends"})
            print(result)
```

---

Або в інтерактивному режимі виберіть `general_search` у меню та введіть запит, коли буде запропоновано.

**Параметри:**
- `query` (рядок): пошуковий запит

**Приклад запиту:**

```json
{
  "query": "latest AI trends"
}
```

### news_search

Шукає останні новинні статті за запитом.

**Як викликати цей інструмент:**

Ви можете викликати `news_search` зі свого скрипта за допомогою MCP Python SDK або інтерактивно через Inspector чи інтерактивний режим клієнта. Ось приклад коду з SDK:

# [Python Example](../../../../05-AdvancedTopics/web-search-mcp)

```python
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client

async def run_news_search():
    server_params = StdioServerParameters(
        command="python",
        args=["server.py"],
    )
    async with stdio_client(server_params) as (reader, writer):
        async with ClientSession(reader, writer) as session:
            await session.initialize()
            result = await session.call_tool("news_search", arguments={"query": "AI policy updates"})
            print(result)
```

---

Або в інтерактивному режимі виберіть `news_search` у меню та введіть запит, коли буде запропоновано.

**Параметри:**
- `query` (рядок): пошуковий запит

**Приклад запиту:**

```json
{
  "query": "AI policy updates"
}
```

### product_search

Шукає продукти, що відповідають запиту.

**Як викликати цей інструмент:**

Ви можете викликати `product_search` зі свого скрипта за допомогою MCP Python SDK або інтерактивно через Inspector чи інтерактивний режим клієнта. Ось приклад коду з SDK:

# [Python Example](../../../../05-AdvancedTopics/web-search-mcp)

```python
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client

async def run_product_search():
    server_params = StdioServerParameters(
        command="python",
        args=["server.py"],
    )
    async with stdio_client(server_params) as (reader, writer):
        async with ClientSession(reader, writer) as session:
            await session.initialize()
            result = await session.call_tool("product_search", arguments={"query": "best AI gadgets 2025"})
            print(result)
```

---

Або в інтерактивному режимі виберіть `product_search` у меню та введіть запит, коли буде запропоновано.

**Параметри:**
- `query` (рядок): пошуковий запит продукту

**Приклад запиту:**

```json
{
  "query": "best AI gadgets 2025"
}
```

### qna

Отримує прямі відповіді на запитання з пошукових систем.

**Як викликати цей інструмент:**

Ви можете викликати `qna` зі свого скрипта за допомогою MCP Python SDK або інтерактивно через Inspector чи інтерактивний режим клієнта. Ось приклад коду з SDK:

# [Python Example](../../../../05-AdvancedTopics/web-search-mcp)

```python
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client

async def run_qna():
    server_params = StdioServerParameters(
        command="python",
        args=["server.py"],
    )
    async with stdio_client(server_params) as (reader, writer):
        async with ClientSession(reader, writer) as session:
            await session.initialize()
            result = await session.call_tool("qna", arguments={"question": "what is artificial intelligence"})
            print(result)
```

---

Або в інтерактивному режимі виберіть `qna` у меню та введіть своє питання, коли буде запропоновано.

**Параметри:**
- `question` (рядок): питання, на яке потрібно знайти відповідь

**Приклад запиту:**

```json
{
  "question": "what is artificial intelligence"
}
```

## Деталі коду

У цьому розділі наведено фрагменти коду та посилання на реалізації сервера і клієнта.

# [Python](../../../../05-AdvancedTopics/web-search-mcp)

Дивіться файли [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py) та [`client.py`](../../../../05-AdvancedTopics/web-search-mcp/client.py) для повної реалізації.

```python
# Example snippet from server.py:
import os
import httpx
# ...existing code...
```

---

## Просунуті концепції цього уроку

Перед тим, як почати розробку, ознайомтеся з важливими просунутими концепціями, які зустрічатимуться у цьому розділі. Розуміння їх допоможе вам краще слідувати матеріалу, навіть якщо ви раніше з ними не стикалися:

- **Оркестрація кількох інструментів**: означає запуск кількох різних інструментів (наприклад, веб-пошук, новини, пошук продуктів, Q&A) в одному MCP-сервері. Це дозволяє серверу виконувати різноманітні завдання, а не лише одне.
- **Керування лімітами API**: багато зовнішніх API (наприклад, SerpAPI) обмежують кількість запитів за певний час. Хороший код перевіряє ці ліміти і коректно їх обробляє, щоб додаток не зламався при досягненні ліміту.
- **Парсинг структурованих даних**: відповіді API часто складні та вкладені. Ця концепція полягає у перетворенні цих відповідей у чисті, зручні формати, дружні для LLM або інших програм.
- **Відновлення після помилок**: іноді щось іде не так — наприклад, мережа не працює або API повертає несподівані дані. Відновлення після помилок означає, що ваш код може впоратися з цими проблемами і надати корисний зворотний зв’язок, замість того, щоб аварійно завершуватися.
- **Перевірка параметрів**: це перевірка, що всі вхідні дані для інструментів правильні та безпечні. Включає встановлення значень за замовчуванням і перевірку типів, що допомагає уникнути помилок і непорозумінь.

Цей розділ допоможе вам діагностувати та вирішувати поширені проблеми, з якими ви можете зіткнутися під час роботи з MCP-сервером для веб-пошуку. Якщо ви натрапите на помилки або несподівану поведінку, цей розділ з усунення несправностей пропонує рішення найпоширеніших проблем. Ознайомтеся з цими порадами перед тим, як звертатися за додатковою допомогою — вони часто допомагають швидко вирішити проблему.

## Усунення несправностей

Під час роботи з MCP-сервером для веб-пошуку іноді можуть виникати проблеми — це нормально при розробці з використанням зовнішніх API та нових інструментів. Цей розділ містить практичні рішення найпоширеніших проблем, щоб ви могли швидко повернутися до роботи. Якщо ви зіткнулися з помилкою, почніть тут: наведені нижче поради розглядають проблеми, з якими найчастіше стикаються користувачі, і часто допомагають вирішити їх без додаткової допомоги.

### Поширені проблеми

Нижче наведено деякі з найчастіших проблем, з якими стикаються користувачі, разом із чіткими поясненнями та кроками для їх вирішення:

1. **Відсутній SERPAPI_KEY у файлі .env**
   - Якщо ви бачите помилку `SERPAPI_KEY environment variable not found`, це означає, що ваш додаток не може знайти ключ API для доступу до SerpAPI. Щоб виправити це, створіть файл `.env` у корені проекту (якщо його ще немає) і додайте рядок на кшталт `SERPAPI_KEY=your_serpapi_key_here`. Обов’язково замініть `your_serpapi_key_here` на ваш реальний ключ із сайту SerpAPI.

2. **Помилки "Module not found"**
   - Помилки на кшталт `ModuleNotFoundError: No module named 'httpx'` означають, що відсутній необхідний пакет Python. Зазвичай це трапляється, якщо ви не встановили всі залежності. Щоб це виправити, виконайте в терміналі команду `pip install -r requirements.txt`, щоб встановити все необхідне.

3. **Проблеми з підключенням**
   - Якщо ви отримуєте помилку на кшталт `Error during client execution`, це часто означає, що клієнт не може підключитися до сервера або сервер не працює як очікувалося. Перевірте, що клієнт і сервер сумісні за версіями, а файл `server.py` знаходиться у правильній директорії і запущений. Перезапуск сервера і клієнта також може допомогти.

4. **Помилки SerpAPI**
   - Повідомлення `Search API returned error status: 401` означає, що ваш ключ SerpAPI відсутній, неправильний або прострочений. Перейдіть у панель керування SerpAPI, перевірте ключ і оновіть файл `.env`, якщо потрібно. Якщо ключ правильний, але помилка залишається, перевірте, чи не вичерпано безкоштовний ліміт.

### Режим налагодження (Debug Mode)

За замовчуванням додаток логуватиме лише важливу інформацію. Якщо ви хочете бачити більше деталей про те, що відбувається (наприклад, для діагностики складних проблем), ви можете увімкнути режим
Щоб увімкнути режим DEBUG, встановіть рівень логування на DEBUG у верхній частині вашого файлу `client.py` або `server.py`:

# [Python](../../../../05-AdvancedTopics/web-search-mcp)

```python
# At the top of your client.py or server.py
import logging
logging.basicConfig(
    level=logging.DEBUG,  # Change from INFO to DEBUG
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)
```

---

---

## Що далі

- [5.10 Потокове передавання в реальному часі](../mcp-realtimestreaming/README.md)

**Відмова від відповідальності**:  
Цей документ було перекладено за допомогою сервісу автоматичного перекладу [Co-op Translator](https://github.com/Azure/co-op-translator). Хоча ми прагнемо до точності, будь ласка, майте на увазі, що автоматичні переклади можуть містити помилки або неточності. Оригінальний документ рідною мовою слід вважати авторитетним джерелом. Для критично важливої інформації рекомендується звертатися до професійного людського перекладу. Ми не несемо відповідальності за будь-які непорозуміння або неправильні тлумачення, що виникли внаслідок використання цього перекладу.
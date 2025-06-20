<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7a11a5dcf2f9fdf6392f5a4545cf005e",
  "translation_date": "2025-06-11T14:45:55+00:00",
  "source_file": "05-AdvancedTopics/web-search-mcp/README.md",
  "language_code": "fa"
}
-->
# درس: ساخت یک سرور MCP جستجوی وب

این فصل نشان می‌دهد چگونه یک عامل هوش مصنوعی واقعی بسازید که با APIهای خارجی ادغام شده، انواع داده‌های مختلف را مدیریت می‌کند، خطاها را کنترل می‌کند و چندین ابزار را هماهنگ می‌سازد—همه در قالبی آماده برای تولید. شما خواهید دید:

- **ادغام با APIهای خارجی که نیاز به احراز هویت دارند**  
- **مدیریت انواع داده‌های متنوع از چندین نقطه انتهایی**  
- **استراتژی‌های قدرتمند مدیریت خطا و ثبت گزارش‌ها**  
- **هماهنگی چندابزاره در یک سرور واحد**

در پایان، تجربه عملی با الگوها و بهترین روش‌هایی خواهید داشت که برای برنامه‌های پیشرفته مبتنی بر هوش مصنوعی و LLM ضروری هستند.

## مقدمه

در این درس، یاد می‌گیرید چگونه یک سرور و کلاینت MCP پیشرفته بسازید که قابلیت‌های LLM را با داده‌های وب در زمان واقعی با استفاده از SerpAPI گسترش می‌دهد. این مهارت حیاتی برای توسعه عوامل هوش مصنوعی پویا است که می‌توانند به اطلاعات به‌روز وب دسترسی داشته باشند.

## اهداف یادگیری

در پایان این درس، قادر خواهید بود:

- APIهای خارجی (مانند SerpAPI) را به صورت امن در سرور MCP ادغام کنید  
- چندین ابزار برای جستجوی وب، اخبار، محصولات و پرسش و پاسخ پیاده‌سازی کنید  
- داده‌های ساختاریافته را برای مصرف LLM تجزیه و قالب‌بندی کنید  
- خطاها را مدیریت کرده و محدودیت‌های نرخ API را به طور مؤثر کنترل کنید  
- کلاینت‌های MCP خودکار و تعاملی بسازید و آزمایش کنید

## سرور MCP جستجوی وب

این بخش معماری و ویژگی‌های سرور MCP جستجوی وب را معرفی می‌کند. خواهید دید چگونه FastMCP و SerpAPI با هم استفاده می‌شوند تا قابلیت‌های LLM را با داده‌های وب در زمان واقعی گسترش دهند.

### مرور کلی

این پیاده‌سازی شامل چهار ابزار است که توانایی MCP را در مدیریت وظایف متنوع مبتنی بر API خارجی به صورت امن و کارآمد نشان می‌دهد:

- **general_search**: برای نتایج گسترده وب  
- **news_search**: برای عناوین خبری اخیر  
- **product_search**: برای داده‌های تجارت الکترونیک  
- **qna**: برای قطعات پرسش و پاسخ

### ویژگی‌ها  
- **نمونه کدها**: شامل بلوک‌های کد مخصوص زبان پایتون (و به آسانی قابل توسعه به زبان‌های دیگر) با بخش‌های قابل جمع‌شدن برای وضوح بیشتر

<details>  
<summary>پایتون</summary>  

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
</details>

قبل از اجرای کلاینت، مفید است بدانید سرور چه کاری انجام می‌دهد. فایل [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py) file implements the MCP server, exposing tools for web, news, product search, and Q&A by integrating with SerpAPI. It handles incoming requests, manages API calls, parses responses, and returns structured results to the client.

You can review the full implementation in [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py) را ببینید.

در اینجا نمونه‌ای کوتاه از نحوه تعریف و ثبت یک ابزار در سرور آمده است:

<details>  
<summary>سرور پایتون</summary> 

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
</details>

- **ادغام API خارجی**: نحوه مدیریت امن کلیدهای API و درخواست‌های خارجی را نشان می‌دهد  
- **تجزیه داده‌های ساختاریافته**: نحوه تبدیل پاسخ‌های API به قالب‌های مناسب برای LLM  
- **مدیریت خطا**: کنترل خطاهای قوی همراه با ثبت گزارش‌های مناسب  
- **کلاینت تعاملی**: شامل تست‌های خودکار و حالت تعاملی برای آزمایش  
- **مدیریت زمینه**: استفاده از MCP Context برای ثبت و پیگیری درخواست‌ها

## پیش‌نیازها

قبل از شروع، مطمئن شوید محیط شما به درستی راه‌اندازی شده است. این کار باعث می‌شود تمام وابستگی‌ها نصب شده و کلیدهای API به درستی برای توسعه و تست روان پیکربندی شده باشند.

- پایتون نسخه ۳.۸ یا بالاتر  
- کلید API SerpAPI (ثبت‌نام در [SerpAPI](https://serpapi.com/) - سطح رایگان موجود است)

## نصب

برای شروع، مراحل زیر را برای راه‌اندازی محیط خود دنبال کنید:

1. وابستگی‌ها را با استفاده از uv (توصیه شده) یا pip نصب کنید:

```bash
# Using uv (recommended)
uv pip install -r requirements.txt

# Using pip
pip install -r requirements.txt
```

2. یک فایل `.env` در ریشه پروژه بسازید و کلید SerpAPI خود را وارد کنید:

```
SERPAPI_KEY=your_serpapi_key_here
```

## نحوه استفاده

سرور MCP جستجوی وب هسته‌ای است که ابزارهایی برای جستجوی وب، اخبار، محصولات و پرسش و پاسخ را از طریق ادغام با SerpAPI ارائه می‌دهد. این سرور درخواست‌های ورودی را مدیریت، تماس‌های API را انجام، پاسخ‌ها را تجزیه و نتایج ساختاریافته را به کلاینت بازمی‌گرداند.

می‌توانید پیاده‌سازی کامل را در [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py) مشاهده کنید.

### اجرای سرور

برای راه‌اندازی سرور MCP، از دستور زیر استفاده کنید:

```bash
python server.py
```

سرور به صورت یک MCP سرور مبتنی بر stdio اجرا می‌شود که کلاینت می‌تواند مستقیماً به آن متصل شود.

### حالت‌های کلاینت

کلاینت در فایل (`client.py`) supports two modes for interacting with the MCP server:

- **Normal mode**: Runs automated tests that exercise all the tools and verify their responses. This is useful for quickly checking that the server and tools are working as expected.
- **Interactive mode**: Starts a menu-driven interface where you can manually select and call tools, enter custom queries, and see results in real time. This is ideal for exploring the server's capabilities and experimenting with different inputs.

You can review the full implementation in [`client.py`](../../../../05-AdvancedTopics/web-search-mcp/client.py) قرار دارد.

### اجرای کلاینت

برای اجرای تست‌های خودکار (که به طور خودکار سرور را نیز راه‌اندازی می‌کند):

```bash
python client.py
```

یا در حالت تعاملی اجرا کنید:

```bash
python client.py --interactive
```

### آزمایش با روش‌های مختلف

راه‌های متعددی برای آزمایش و تعامل با ابزارهای ارائه شده توسط سرور وجود دارد، بسته به نیازها و روند کاری شما.

#### نوشتن اسکریپت‌های تست سفارشی با MCP Python SDK  
همچنین می‌توانید اسکریپت‌های تست خود را با استفاده از MCP Python SDK بسازید:

<details>
<summary>پایتون</summary>

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
</details>

در اینجا، "اسکریپت تست" به برنامه پایتونی سفارشی گفته می‌شود که شما می‌نویسید تا به عنوان کلاینت برای سرور MCP عمل کند. این اسکریپت به جای یک تست واحد رسمی، به شما امکان می‌دهد به صورت برنامه‌نویسی به سرور متصل شده، هر یک از ابزارها را با پارامترهای دلخواه فراخوانی کرده و نتایج را بررسی کنید. این روش برای موارد زیر مفید است:  
- نمونه‌سازی و آزمایش فراخوانی ابزارها  
- اعتبارسنجی پاسخ سرور به ورودی‌های مختلف  
- خودکارسازی فراخوانی‌های مکرر ابزار  
- ساخت جریان‌های کاری یا ادغام‌های شخصی بر پایه سرور MCP

می‌توانید از اسکریپت‌های تست برای آزمایش سریع پرسش‌های جدید، اشکال‌زدایی رفتار ابزارها یا حتی به عنوان نقطه شروع برای خودکارسازی پیشرفته‌تر استفاده کنید. در ادامه نمونه‌ای از نحوه استفاده از MCP Python SDK برای ساخت چنین اسکریپتی آمده است:

## توضیحات ابزارها

می‌توانید از ابزارهای زیر که توسط سرور ارائه شده‌اند برای انجام انواع مختلف جستجو و پرسش استفاده کنید. هر ابزار با پارامترها و نمونه استفاده آن در ادامه توضیح داده شده است.

این بخش جزئیات هر ابزار موجود و پارامترهای آن‌ها را ارائه می‌دهد.

### general_search

یک جستجوی کلی وب انجام می‌دهد و نتایج قالب‌بندی شده را بازمی‌گرداند.

**نحوه فراخوانی این ابزار:**

می‌توانید `general_search` را از اسکریپت خود با استفاده از MCP Python SDK فراخوانی کنید یا به صورت تعاملی با Inspector یا حالت تعاملی کلاینت. در اینجا نمونه کدی با SDK آمده است:

<details>
<summary>مثال پایتون</summary>

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
</details>

در حالت تعاملی، گزینه `general_search` from the menu and enter your query when prompted.

**Parameters:**
- `query` (رشته): عبارت جستجو را انتخاب کنید

**نمونه درخواست:**

```json
{
  "query": "latest AI trends"
}
```

### news_search

به دنبال مقالات خبری اخیر مرتبط با یک عبارت می‌گردد.

**نحوه فراخوانی این ابزار:**

می‌توانید `news_search` را از اسکریپت خود با استفاده از MCP Python SDK فراخوانی کنید یا به صورت تعاملی با Inspector یا حالت تعاملی کلاینت. در اینجا نمونه کدی با SDK آمده است:

<details>
<summary>مثال پایتون</summary>

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
</details>

در حالت تعاملی، گزینه `news_search` from the menu and enter your query when prompted.

**Parameters:**
- `query` (رشته): عبارت جستجو را انتخاب کنید

**نمونه درخواست:**

```json
{
  "query": "AI policy updates"
}
```

### product_search

به دنبال محصولاتی می‌گردد که با یک عبارت مطابقت دارند.

**نحوه فراخوانی این ابزار:**

می‌توانید `product_search` را از اسکریپت خود با استفاده از MCP Python SDK فراخوانی کنید یا به صورت تعاملی با Inspector یا حالت تعاملی کلاینت. در اینجا نمونه کدی با SDK آمده است:

<details>
<summary>مثال پایتون</summary>

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
</details>

در حالت تعاملی، گزینه `product_search` from the menu and enter your query when prompted.

**Parameters:**
- `query` (رشته): عبارت جستجوی محصول را انتخاب کنید

**نمونه درخواست:**

```json
{
  "query": "best AI gadgets 2025"
}
```

### qna

پاسخ‌های مستقیم به سوالات را از موتورهای جستجو دریافت می‌کند.

**نحوه فراخوانی این ابزار:**

می‌توانید `qna` را از اسکریپت خود با استفاده از MCP Python SDK فراخوانی کنید یا به صورت تعاملی با Inspector یا حالت تعاملی کلاینت. در اینجا نمونه کدی با SDK آمده است:

<details>
<summary>مثال پایتون</summary>

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
</details>

در حالت تعاملی، گزینه `qna` from the menu and enter your question when prompted.

**Parameters:**
- `question` (رشته): سوالی که می‌خواهید پاسخ آن را پیدا کنید انتخاب کنید

**نمونه درخواست:**

```json
{
  "question": "what is artificial intelligence"
}
```

## جزئیات کد

این بخش قطعه کدها و ارجاعات مربوط به پیاده‌سازی سرور و کلاینت را ارائه می‌دهد.

<details>
<summary>پایتون</summary>

برای جزئیات کامل پیاده‌سازی به [`server.py`](../../../../05-AdvancedTopics/web-search-mcp/server.py) and [`client.py`](../../../../05-AdvancedTopics/web-search-mcp/client.py) مراجعه کنید.

```python
# Example snippet from server.py:
import os
import httpx
# ...existing code...
```
</details>

## مفاهیم پیشرفته در این درس

قبل از شروع ساخت، در اینجا چند مفهوم پیشرفته مهم وجود دارد که در طول این فصل ظاهر خواهند شد. درک این موارد به شما کمک می‌کند بهتر دنبال کنید، حتی اگر برای اولین بار با آن‌ها مواجه می‌شوید:

- **هماهنگی چندابزاره**: یعنی اجرای چند ابزار مختلف (مانند جستجوی وب، جستجوی اخبار، جستجوی محصول و پرسش و پاسخ) در یک سرور MCP واحد. این امکان را می‌دهد که سرور شما بتواند انواع مختلف وظایف را مدیریت کند، نه فقط یکی.  
- **مدیریت محدودیت نرخ API**: بسیاری از APIهای خارجی (مانند SerpAPI) تعداد درخواست‌هایی که می‌توانید در بازه زمانی مشخص ارسال کنید را محدود می‌کنند. کد خوب این محدودیت‌ها را بررسی کرده و به شکل مناسبی مدیریت می‌کند تا برنامه شما در صورت رسیدن به حد مجاز دچار مشکل نشود.  
- **تجزیه داده‌های ساختاریافته**: پاسخ‌های API اغلب پیچیده و تو در تو هستند. این مفهوم به تبدیل آن پاسخ‌ها به قالب‌های تمیز و قابل استفاده که برای LLMها یا برنامه‌های دیگر مناسب باشد اشاره دارد.  
- **بازیابی از خطا**: گاهی اوقات مشکلاتی پیش می‌آید—مثلاً شبکه قطع می‌شود یا API پاسخ مورد انتظار را نمی‌دهد. بازیابی از خطا یعنی کد شما می‌تواند این مشکلات را مدیریت کرده و بازخورد مفید ارائه دهد، به جای اینکه برنامه کرش کند.  
- **اعتبارسنجی پارامترها**: یعنی بررسی اینکه تمام ورودی‌های ابزارهای شما صحیح و ایمن هستند. شامل تعیین مقادیر پیش‌فرض و اطمینان از نوع داده‌ها که به جلوگیری از خطاها و سردرگمی کمک می‌کند.

این بخش به شما کمک می‌کند مشکلات رایجی که ممکن است هنگام کار با سرور MCP جستجوی وب با آن‌ها مواجه شوید را تشخیص داده و حل کنید. اگر با خطا یا رفتار غیرمنتظره‌ای روبرو شدید، این بخش راه‌حل‌هایی برای متداول‌ترین مشکلات ارائه می‌دهد. قبل از درخواست کمک بیشتر، این نکات را مرور کنید—اغلب مشکلات را سریع برطرف می‌کنند.

## عیب‌یابی

هنگام کار با سرور MCP جستجوی وب، ممکن است گاهی با مشکلاتی مواجه شوید—این موضوع در توسعه با APIهای خارجی و ابزارهای جدید طبیعی است. این بخش راه‌حل‌های عملی برای رایج‌ترین مشکلات را ارائه می‌دهد تا بتوانید سریع‌تر به مسیر درست بازگردید. اگر خطایی دیدید، از اینجا شروع کنید: نکات زیر به مسائل متداول کاربران می‌پردازند و اغلب بدون نیاز به کمک اضافی مشکل شما را حل می‌کنند.

### مشکلات رایج

در ادامه برخی از شایع‌ترین مشکلات کاربران به همراه توضیحات واضح و مراحل حل آن‌ها آمده است:

1. **نبودن SERPAPI_KEY در فایل .env**  
   - اگر خطای `SERPAPI_KEY environment variable not found`, it means your application can't find the API key needed to access SerpAPI. To fix this, create a file named `.env` in your project root (if it doesn't already exist) and add a line like `SERPAPI_KEY=your_serpapi_key_here`. Make sure to replace `your_serpapi_key_here` with your actual key from the SerpAPI website.

2. **Module not found errors**
   - Errors such as `ModuleNotFoundError: No module named 'httpx'` indicate that a required Python package is missing. This usually happens if you haven't installed all the dependencies. To resolve this, run `pip install -r requirements.txt` in your terminal to install everything your project needs.

3. **Connection issues**
   - If you get an error like `Error during client execution`, it often means the client can't connect to the server, or the server isn't running as expected. Double-check that both the client and server are compatible versions, and that `server.py` is present and running in the correct directory. Restarting both the server and client can also help.

4. **SerpAPI errors**
   - Seeing `Search API returned error status: 401` means your SerpAPI key is missing, incorrect, or expired. Go to your SerpAPI dashboard, verify your key, and update your `.env` را دیدید، فایل `.env` را بسازید یا بررسی کنید کلید به درستی وارد شده باشد. اگر کلید شما صحیح است اما هنوز این خطا را می‌بینید، بررسی کنید که سطح رایگان شما تمام نشده باشد.

### حالت دیباگ

به طور پیش‌فرض، برنامه فقط اطلاعات مهم را ثبت می‌کند. اگر می‌خواهید جزئیات بیشتری از اتفاقات (مثلاً برای تشخیص مشکلات پیچیده) ببینید، می‌توانید حالت DEBUG را فعال کنید. این حالت اطلاعات بیشتری درباره هر مرحله که برنامه انجام می‌دهد نشان می‌دهد.

**مثال: خروجی عادی**  
```plaintext
2025-06-01 10:15:23,456 - __main__ - INFO - Calling general_search with params: {'query': 'open source LLMs'}
2025-06-01 10:15:24,123 - __main__ - INFO - Successfully called general_search

GENERAL_SEARCH RESULTS:
... (search results here) ...
```

**مثال: خروجی DEBUG**  
```plaintext
2025-06-01 10:15:23,456 - __main__ - INFO - Calling general_search with params: {'query': 'open source LLMs'}
2025-06-01 10:15:23,457 - httpx - DEBUG - HTTP Request: GET https://serpapi.com/search ...
2025-06-01 10:15:23,458 - httpx - DEBUG - HTTP Response: 200 OK ...
2025-06-01 10:15:24,123 - __main__ - INFO - Successfully called general_search

GENERAL_SEARCH RESULTS:
... (search results here) ...
```

توجه کنید که حالت DEBUG شامل خطوط اضافی درباره درخواست‌ها و پاسخ‌های HTTP و سایر جزئیات داخلی است. این برای عیب‌یابی بسیار مفید است.

برای فعال کردن حالت DEBUG، سطح لاگ‌گیری را در بالای فایل `client.py` or `server.py` به DEBUG تغییر دهید:

<details>
<summary>پایتون</summary>

```python
# At the top of your client.py or server.py
import logging
logging.basicConfig(
    level=logging.DEBUG,  # Change from INFO to DEBUG
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)
```
</details>

---

## مرحله بعد

- [5.10 پخش زنده در زمان واقعی](../mcp-realtimestreaming/README.md)

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما در تلاش برای دقت هستیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است حاوی اشتباهات یا نواقص باشند. سند اصلی به زبان بومی خود باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حیاتی، توصیه می‌شود از ترجمه حرفه‌ای انسانی استفاده شود. ما مسئول هیچ گونه سوء تفاهم یا تفسیر نادرست ناشی از استفاده از این ترجمه نیستیم.
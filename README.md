# Stock-Data-Dashboard
Mini Practice Project for Beginners 

# 📊 Extracting and Visualizing Stock Data (Tesla & GameStop)

## 📌 Project Overview
This project is about being a **Data Analyst for an investment firm**. The goal is simple:
- Pull real stock price history for two companies (**Tesla** and **GameStop**)
- Pull their real business revenue (how much money the company actually made)
- Compare the two on a graph, to see if the stock price matches the real business performance

This helps answer a very important investing question: **"Is the stock price going up because the company is actually doing well, or because of hype?"**

---

## 🎯 What This Project Does
1. Extract Tesla's stock price history using the `yfinance` library
2. Extract Tesla's quarterly revenue by scraping it from a webpage
3. Extract GameStop's stock price history using `yfinance`
4. Extract GameStop's quarterly revenue by scraping it from a webpage
5. Plot Tesla: Stock Price vs Revenue on one dashboard
6. Plot GameStop: Stock Price vs Revenue on one dashboard

---

## 🧠 Key Concepts Explained (Beginner Friendly)

### 1. What is `yfinance`?
It's a free Python library that connects to Yahoo Finance and downloads real stock market data — no need to manually download CSV files from a website.

### 2. What is a "Ticker"?
Every public company has a short code on the stock market, called a **ticker symbol**. Tesla = `TSLA`, GameStop = `GME`. In code:
```python
tesla = yf.Ticker("TSLA")
```
This just creates a Python "object" that represents Tesla, so we can ask it for data.

### 3. `.history(period="max")`
This pulls the **entire available price history** of the stock — every day's Open price, High price, Low price, Close price, and trading Volume, from the earliest available date until today.

### 4. `reset_index()`
By default, the Date becomes a special "index" (row label), not a normal column. `reset_index()` turns Date back into a regular column, so we can use it easily (for filtering, plotting, etc).

### 5. Web Scraping — What & Why?
Not every piece of data has a clean API. Sometimes the data (like quarterly revenue) only exists inside a normal webpage, written as an HTML table. **Web scraping** means:
- `requests.get(url).text` → downloads the raw HTML code of the page (like viewing "page source")
- `BeautifulSoup(html_data, "html.parser")` → understands that raw HTML and lets us search inside it (for tables, rows, cells, etc.)

### 6. Why `soup.find_all("tbody")[1]`?
A webpage can have more than one table on it. `[1]` means "the second table on the page" (counting starts from 0) — which happens to be the quarterly revenue table we need.

### 7. Cleaning the Data (`.str.replace(',|\$', "", regex=True)`)
Scraped revenue numbers look like text: `"$1,234"`. Computers can't do math on text with `$` and commas in it. This line removes both the comma **and** the dollar sign using a pattern called **regex**, so `"$1,234"` becomes `"1234"` — a usable number.

### 8. `dropna()` and removing empty rows
Sometimes scraped tables have missing/empty rows. We remove them so our data stays clean and accurate.

### 9. What is a Pandas DataFrame?
Think of it like an Excel spreadsheet inside Python — rows and columns, easy to filter, sort, and analyze.

### 10. The `make_graph()` Function
This function takes stock price data + revenue data and draws **two graphs stacked together** (using `matplotlib`):
- Top graph: Stock Price over time
- Bottom graph: Revenue over time

Putting them together lets us visually compare: does the stock price move together with real revenue, or not?

---

## 🔍 What We Discovered (Key Insights)

**Tesla 🚗**
Both stock price and revenue grew significantly over time, especially after 2020. This suggests investor excitement was backed by real business growth.

**GameStop 🎮**
The stock price shot up dramatically in early 2021 — but revenue stayed roughly the same, following its normal seasonal pattern. This was the famous **"GameStop short squeeze"** (driven by retail investors on Reddit, not by the company's actual business performance). It's a great real-world example that **stock price does not always reflect a company's true financial health**.

---

## 🛠️ Tools & Libraries Used
| Tool | Purpose |
|---|---|
| `yfinance` | Fetch real stock price data |
| `requests` | Download raw webpage HTML |
| `BeautifulSoup (bs4)` | Parse/search HTML for tables |
| `pandas` | Store & clean data in DataFrames |
| `matplotlib` | Plot the dashboard graphs |

---

## ✅ What I Learned
- How to pull real financial data using a Python library (API-style)
- How to scrape data directly from a webpage when no API is available
- How to clean messy, real-world text data (commas, `$` signs, empty values)
- How to visualize and compare two different datasets on one dashboard
- How to read a graph and draw a real business conclusion from it (hype vs. fundamentals)

---
## 📚 Resources & References

- **yfinance documentation** — https://pypi.org/project/yfinance/
- **BeautifulSoup documentation** — https://www.crummy.com/software/BeautifulSoup/bs4/doc/
- **pandas documentation** — https://pandas.pydata.org/docs/
- **matplotlib documentation** — https://matplotlib.org/stable/index.html
- **requests library documentation** — https://requests.readthedocs.io/
- **Regular Expressions (regex) basics** — https://docs.python.org/3/howto/regex.html
- **GameStop short squeeze (2021) — background reading** — search "GameStop short squeeze 2021" for context on why the stock price spiked without matching revenue
- **Course**: IBM Data Science Professional Certificate — Python Project for Data Science (Coursera)

## 🧾 Data Sources
- Stock price data: Yahoo Finance (via `yfinance`)
- Tesla quarterly revenue: scraped from a provided course webpage (HTML table)
- GameStop quarterly revenue: scraped from a provided course webpage (HTML table)

## 👤 Author
Project completed as part of the IBM Data Science course on Coursera.

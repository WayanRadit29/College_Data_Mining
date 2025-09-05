# 📰 News Web Scraping with Python

This notebook demonstrates how to perform **web scraping** on online news websites using Python.  
It is part of my **Data Mining learning journey**, focusing on how to collect raw text data for further preprocessing and analysis.

---

## 🎯 Objectives
- Learn how to extract structured information from web pages.
- Practice using Python libraries for HTTP requests and HTML parsing.
- Build a dataset of news articles for later use in data mining tasks.

---

## ⚙️ Tools & Libraries
- **requests** → to send HTTP requests and fetch HTML content.  
- **BeautifulSoup (bs4)** → to parse HTML and extract elements (title, date, content).  
- **pandas** → to store scraped data in tabular format (CSV/Excel).  
- **time** → to handle delays between requests (polite scraping).  

---

## 📑 Notebook Workflow
1. **Import dependencies**  
   Load required Python libraries for scraping and data handling.  

2. **Define target website(s)**  
   Select the news website(s) to scrape (e.g., article list or category pages).  

3. **Send requests & parse HTML**  
   Use `requests` to fetch web pages and `BeautifulSoup` to extract relevant fields such as:  
   - Title  
   - Date published  
   - Article content  

4. **Store results**  
   Save the scraped data into a `pandas DataFrame` and export it to CSV for later analysis.  

---

## 📂 Output
The notebook produces a dataset containing scraped news articles with columns like:
- `title`
- `date`
- `content`
- `url`

Saved as a CSV file for further preprocessing in later steps of the Data Mining course.

---

## ⚠️ Disclaimer
This project is for **educational purposes only**.  
Scraping must follow the website's **robots.txt** and terms of service.  
For large-scale scraping, always consider using APIs provided by the news sources.

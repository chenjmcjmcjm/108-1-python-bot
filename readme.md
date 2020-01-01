108-1-python-bot
import requests
from bs4 import BeautifulSoup
from urllib.parse import quote
import urllib

q = input('請輸入查詢：')
search_list = []
keyword = quote(q.encode('utf8'))
res = requests.get("https://news.ltn.com.tw/search?keyword="+keyword)

# 關鍵字多加一個雙引號是精準搜尋
# num: 一次最多要request的筆數, 可減少切換頁面的動作
# tbs: 資料時間, hour(qdr:h), day(qdr:d), week(qdr:w), month(qdr:m), year(qdr:w)

if res.status_code == 200:
    content = res.content
    soup = BeautifulSoup(content, "html.parser")

    items = soup.findAll("ul", {"class": "searchlist boxTitle"})
    for item in items:
        # title
        news_title = item.find_all('a')

        for a in news_title:
            print(a.text)

end = input('Plese Enter any key')
        

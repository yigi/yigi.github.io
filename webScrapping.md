## Beautiful Soup

```python
pip3 install beautifulsoup4
from bs4 import BeautifulSoup
import requests

r = requests.get('any web site url')
#sağ click inspect element sayfayı yenile network headers user-agent
#headers_param = {"User-Agent":" Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.100 Safari/537.36 OPR/62.0.3331.72"}
#r = requests.get('any web site url', headers = headers_param)
r.status.code
source = BeautifulSoup(r.content,"lxml")
# buradaki r content elde edilen bir item ın içine girmek için de item.content olarak çağırılabilir.
source.title

source.find("p")
<p class="text_44214">Product Hunt surfaces the best new products, every day. It's a place for product-loving enthusiasts to share and geek out about the latest mobile apps, websites, hardware projects, and tech creations.</p>

source.find("p").text
#html taglerinden arındırır

source.find("a",attrs={"class":"tab_row"}).text
#o class ı içeren ilk elemanı getirir find_all hepsini getirir. limit=2 parametresi de head(2) gibi

games = source.find("a",attrs={"class":"tab_row"})
for game in games
  print(game.h4)
  
#table ın altındaki 2. tr nin altındaki td nin 3. table ı  
film_table = source.find("table",attrs={"class":"table_name"}).select("tr:nth-of-type(2) > td > table:nth-of-type(3)") 

film_name = film_table[0].find("a",attrs={"class":"ad"}).get(title)

#use copy selector with right click o item
```
```python
for pageNumber in range( 1, len( source.find_all("ul", attrs={"class:pagination"})[0].find_all("li"))
  pageRequest = request.get("link.com/page" + str(pageNumber))
  ...
  ...
  jobs = source.find("div", attrs ={"class: row"}.ol.find_all("li")

#use next :)
```

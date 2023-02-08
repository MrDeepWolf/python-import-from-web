# python-import-from-web
If you need a data from web page you can use these codes.

Requeired Modules :

pip install beautifulsoup4
pip install pandas
pip install requests



import requests
from bs4 import BeautifulSoup
import pandas as pd

url ="https://www.trendyol.com/sr?q=bardak"
response = requests.get(url)
icerik = response.content
soup = BeautifulSoup(icerik,"html.parser")
isim = soup.find_all("span",attrs={"class":"prdct-desc-cntnr-name hasRatings"})
fiyat = soup.find_all("div",attrs={"class":"prc-box-dscntd"})

liste = list()

for i in range(len(isim)):
    isim[i] = (isim[i].text).strip("\n").strip()
    fiyat[i] = (fiyat[i].text).strip("\n").strip()

    liste.append([isim[i],fiyat[i]])

    cikti = pd.DataFrame(liste,columns= ["Ürün İsimleri","Ürün Fiyatları"])
    print(cikti)

# Web-Scraping-Data-For-Jumia-Website
# Web Scraping  Le Web Scraping (grattage) est une technique utilisée par les développeurs pour extraire  (littéralement « gratter ») des informations d’un site Internet. 
# import data for one page in website jumia here is the source code

url = 'https://www.jumia.ma/smartphones/?page=1'
r= requests.get(url)
soup = BeautifulSoup(r.content,'html.parser')
ancher = soup.find('div',{'class':'-paxs row _no-g _4cl-3cm-shs'})
ancher = ancher.find_all('article',{'class':'prd _fb col c-prd'})
for pt in ancher:
        img= pt.find('a').find('div' , {'class' : 'img-c'}).find('img',{'class':'img'})
        name = pt.find('a').find('div' , {'class' : 'info'}).find('h3' , {'class' : 'name'})
        price = pt.find('a').find('div' , {'class' : 'info'}).find('div' , {'class' : 'prc'})
        
        columns['img url'].append(img.get('data-src'))
        columns['name'].append(name.text)
        columns['price'].append(price.text)
    
        
pd.DataFrame(columns).to_excel('data.xlsx')

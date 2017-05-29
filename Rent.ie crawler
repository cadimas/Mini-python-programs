import requests
from bs4 import BeautifulSoup

#request part
url = "http://www.rent.ie/rooms-to-rent/renting_cork/cork-city-centre/room-type_either/page_1/"
r = requests.get(url)
plain_text = r.text
soup = BeautifulSoup(plain_text , "html.parser")

#calculates how many pages to iterate
num = soup.find("span", {"id": "num_properties"}).get_text()
num_pag = round(int(num)/20)



#receives num has argument meaning the page number , returns links where it did not encounter the couples not allowed tag
def find_links(num):
    #request part
    url = "http://www.rent.ie/rooms-to-rent/renting_cork/cork-city-centre/room-type_either/page_"+ num
    r = requests.get(url)
    plain_text = r.text
    #transition to soup
    soup = BeautifulSoup(plain_text, "html.parser")

    links = soup.find_all("div" , class_ = "sresult_address")
    print("found :" + str(len(links))+ " links")
    print("analizying page:" + str(num))
    for link in links:
        target_link = link.h2.a["href"]
        if find_couple(target_link):
            print(target_link)


#tests if url given has couples allowed tag, if yes returns true
def find_couple(url1):
    url = url1
    r = requests.get(url)
    plain_text = r.text
    soup = BeautifulSoup(plain_text, "html.parser")
    couples = soup.find("div", {"class": "text"})
    teste = couples.find_all("strong")
    for i in teste:
        if str(i) == "<strong>Couples allowed</strong>":
            return True

    return False


#iterate through all pages.
for i in range(1 , num_pag + 1):
    find_links(str(i))

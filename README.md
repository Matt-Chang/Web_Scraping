
# Personal Website Articles Scraping




libraries import

    from bs4 import BeautifulSoup
    import requests
    import csv

Using requests.get to get access from the Web.

    source = requests.get('http://coreyms.com').text
Using lxml to work with real-world and broken HTML on the Web.
    
    soup = BeautifulSoup(source, 'lxml')

Using csv library to create a csv file and categorize the topic in three, headline, summary , and video link. 

    csv_file = open('Web_scraping2.csv', 'w')
    csv_writer = csv.writer(csv_file)
    csv_writer.writerow(['headline','summary','yt_link'])

I set up a variable to find all the attributes "articles" on the Web. 
    
    for article in soup.find_all('article'):

And from the attributes "articles", I got other sub attributes like "headline" and "summary" and printed them out.
    
    headline = article.h2.a.text
    print(headline)
    
    summary = article.find('div',class_='entry-content').p.text
    print(summary)

Here, I was trying to get the video ID from each youtube link in the articles. 
I used the function Try to make sure the code always runs till the end even without the link found.

    try:
            vid_src = article.find('iframe', class_='youtube-player')['src']

            vid_id = vid_src.split('/')[4]

            vid_id = vid_id.split('?')[0]

            yt_link = f'http://youtube.com/watch?v={vid_id}'
            
        except Exception as e:
            yt_link = None

        print(yt_link)

This is for separating each article.

    print() 

I put all of the three categories( headline, summary, and videoID) I just got from the articles in the csv file I created earlier. And closed it. 
    
    csv_writer.writerow([headline, summary, yt_link])

    csv_file.close()


## Authors

- [@Corey Schafer](https://youtu.be/ng2o98k983k)



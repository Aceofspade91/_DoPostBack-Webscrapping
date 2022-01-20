# _DoPostBack-Webscrapping
Data Scrapping of the FairFax Special Events
https://fairfax.usedirect.com/FairfaxFCPAWeb/ACTIVITIES/Search.aspx?category_name=CAMPS&place_id=ALL+PLACES%2fpage-3


#_DoPostBack()
Once you try to navigate to the next page after collecting your data, you will find that on inspecting the "Next" button that it contains a JavaScript:'doPostBack("ctl01$mainContent$bNext","")
That means that when the Next button is pressed the site sends a post request to the server that generates the new page as a response, and you have to simulate that post request in your code with exactly the same arrguments
Dealing with a PostBack server request is annoying, first you have to understand how the PostBack function works.

In most cases the post back function takes arguments (_EVENTTARGET="Something", _EVENTARGUMENT="",  _VIEWSTATE=VIEWSTATE, _VIEWSTATEGENERATOR=VIEWSTATEGENERATOR, _EVENTVALIDATION=EVENTVALIDATION)


VIEWSTATE,VIEWSTATEGENERATOR,EVENTVALIDATION are all uniuqe to each page and need to be scrapped using Beautifulsoup everytime.

EVENTTARGET is the first argument in the actual dopostback script in the 'Next' button.
An easy way to know what goes in the function is to open the NETworks tab while inspecting, then changing the page, you will find among the countless GET requests a POST request, this is the page sending the request to change the page number to the server.

If you inspect the REQUEST of the POST you will find VIEWSTATE,VIEWSTATEGENERATOR,EVENTVALIDATION and EVENTTARGET for that Page ( doesn't work with OPERA you have to use firfox or Chrome to be able to see the post request).
A dopostback is unique and can contain as many arguments as the page wants what's important is that you simulate the request that your page sends, if the request has a "_LASTFOCUS" you have to add one and so on. 

IF you get a response 500 server internal error it's because you didn't add in the headers = headers and quarying in your original requests.get(url)
If you don't know what the headers are you can use either Insomia or Postman and copy the Post request as cUrl into one of them, get the code out as python and just copy the headers from there.

#**Interacting with HTML and Web APIs**

## Python Requests Library

Requests library is one of the integral part of Python for making HTTP requests to a specified URL. Whether it be REST APIs or Web Scrapping, requests is must to be learned for proceeding further with these technologies. When one makes a request to a URI, it returns a response. Python requests provides inbuilt functionalities for managing both the request and response.

**Making a Request**

Python requests module has several built-in methods to make Http requests to specified URI using GET, POST, PUT, PATCH or HEAD requests. A Http request is meant to either retrieve data from a specified URI or to push data to a server. It works as a request-response protocol between a client and a server. Let’s demonstrate how to make a GET request to an endpoint.

GET method is used to retrieve information from the given server using a given URI. The GET method sends the encoded user information appended to the page request. The page and the encoded information are separated by the ‘?’ character.

For example:
```
https://www.google.com/search?q=hello
```

**How to make GET request through Python Requests**

Python’s requests module provides in-built method called get() for making a GET request to a specified URI.

Syntax –
```
requests.get(url, params={key: value}, args)
```

Example –

Let’s try making a request to github’s APIs for example purposes.



```python
import requests
   
# Making a GET request
r = requests.get('https://www.google.com/search?q=hello')
  
# check status code for response received
# success code - 200
print(r)
  
# print content of request
print(r.content)
```

**Http Request Methods –**
```
Method	Description
GET	GET method is used to retrieve information from the given server using a given URI.
POST	POST request method requests that a web server accepts the data enclosed in the body of the request message, most likely for storing it
PUT	The PUT method requests that the enclosed entity be stored under the supplied URI. If the URI refers to an already existing resource, it is modified and if the URI does not point to an existing resource, then the server can create the resource with that URI.
DELETE	The DELETE method deletes the specified resource
HEAD	The HEAD method asks for a response identical to that of a GET request, but without the response body.
PATCH	It is used for modify capabilities. The PATCH request only needs to contain the changes to the resource, not the complete resource
```


**Response object**

When one makes a request to a URI, it returns a response. This Response object in terms of python is returned by requests.method(), method being – get, post, put, etc. Response is a powerful object with lots of functions and attributes that assist in normalizing data or creating ideal portions of code. For example, **response.status_code** returns the status code from the headers itself, and one can check if the request was processed successfully or not.
Response object can be used to imply lots of features, methods, and functionalities.


```python
#Example :

# import requests module
import requests
  
# Making a get request
response = requests.get('https://api.github.com/')
  
# print request object
print(response.url)
  
# print status code
print(response.status_code)
```

Status code 200 indicates that request was made successfully.

What is status code?

####**Status Code**

A status code defines the status of the request. On entering URL, a mistake can be typed in the URL, or there may be a server-side problem. Status code is used to know about what went wrong and where you made a mistake. There are different status codes, and each of the status codes has different meanings.

Let's see some standard status codes:

200: This code is used for a successful request.

201: For a successful request and data was created.

204: For empty response.

400: This is used for Bad Request. If you enter something wrong or you missed some required parameters, then the request would not be understood by the server, and you will get 400 status code.

401: This is used for Unauthorized Access. If the request authentication failed or the user does not have permissions for the requested operations, then you will get a 401 status code.

403: This is for Forbidden or Access Denied.

404: This will come if the Data Not Found.

500: This code is used for Internal Server Error.


**Response Methods**

```
Method	Description
response.headers	response.headers returns a dictionary of response headers.
response.encoding	response.encoding returns the encoding used to decode response.content.
response.elapsed	response.elapsed returns a timedelta object with the time elapsed from sending the request to the arrival of the response.
response.close()	response.close() closes the connection to the server.
response.content	response.content returns the content of the response, in bytes.
response.cookies	response.cookies returns a CookieJar object with the cookies sent back from the server.
response.history	response.history returns a list of response objects holding the history of request (url).
response.is_permanent_redirect	response.is_permanent_redirect returns True if the response is the permanent redirected url, otherwise False.
response.is_redirect	response.is_redirect returns True if the response was redirected, otherwise False.
response.iter_content()	response.iter_content() iterates over the response.content.
response.json()	response.json() returns a JSON object of the result (if the result was written in JSON format, if not it raises an error).
response.url	response.url returns the URL of the response.
response.text	response.text returns the content of the response, in unicode.
response.status_code	response.status_code returns a number that indicates the status (200 is OK, 404 is Not Found).
response.request	response.request returns the request object that requested this response.
response.reason	response.reason returns a text corresponding to the status code.
response.raise_for_status()	response.raise_for_status() returns an HTTPError object if an error has occurred during the process.
response.ok	response.ok returns True if status_code is less than 200, otherwise False.
response.links	response.links returns the header links.
```



**Authentication using Python Requests**

Authentication refers to giving a user permissions to access a particular resource. Since, everyone can’t be allowed to access data from every URL, one would require authentication primarily. To achieve this authentication, typically one provides authentication data through Authorization header or a custom header defined by server.

Example –



```python
# import requests module
import requests
from requests.auth import HTTPBasicAuth
  
# Making a get request
response = requests.get('https://api.github.com / user, ',
            auth = HTTPBasicAuth('user', 'pass'))
  
# print request object
print(response)
```

Replace “user” and “pass” with your username and password. It will authenticate the request and return a response 200 or else it will return error 403.

**SSL Certificate Verification**

Requests verifies SSL certificates for HTTPS requests, just like a web browser. SSL Certificates are small data files that digitally bind a cryptographic key to an organization’s details. Often, an website with a SSL certificate is termed as secure website. By default, SSL verification is enabled, and Requests will throw a SSLError if it’s unable to verify the certificate.

**Disable SSL certificate verification**

Let us try to access a website with an invalid SSL certificate, using Python requests



```python
# import requests module
import requests
  
# Making a get request
response = requests.get('https://expired.badssl.com/')
  
# print request object
print(response)
```

Output :-
ssl-certificate-verification-python-requests
This website doesn’t have SSL setup so it raises this error.
one can also pass the link to the certificate for validation via python requests only.


```python
# import requests module
import requests
  
# Making a get request
response = requests.get('https://github.com', verify ='/path/to/certfile')
  
# print request object
print(response)
```





This would work in case the path provided is correct for SSL certificate for github.com.

####Q1 Check the status code issued by a server in response to a client's request
Write a Python code to check the status code issued by a server in response to a client's request made to the server. Print all of the methods and attributes available to objects on successful request.


```python
'''
import requests
res = requests.get('https://google.com/')
print("Response of https://google.com/:")
print(res.status_code)
print(dir(res)) 
'''
```

####Q2 Send a request to a web page, and print the response text, content, raw data
Write a Python code to send a request to a web page, and print the response text and content. Also get the raw socket response from the server.


```python
'''
import requests
res = requests.get('https://www.google.com/')
print("Response text of https://google.com/:")
print(res.text)
print("\n==============================================================================")
print("\nContent of the said url:")
print(res.content)
print("\n==============================================================================")
print("\nRaw data of the said url:")
r = requests.get('https://api.github.com/events', stream = True)
print(r.raw)
print(r.raw.read(15))
'''
```

###Q3 Send a request to a web page, and print the JSON value of the response
Write a Python code to send a request to a web page, and print the JSON value of the response. Also print each key value of the response.


```python

import requests
r = requests.get('https://api.github.com/')
response = r.json()
print("JSON value of the said response:")
print(r.json())
print("\nEach key of the response:")
print("Current user url:",response['current_user_url'])
print("Current user authorizations html url:",response['current_user_authorizations_html_url'])
print("Authorizations url:",response['authorizations_url'])
print("code_search_url:",response['code_search_url'])
print("commit_search_url:",response['commit_search_url'])
print("Emails url:",response['emails_url'])
print("Emojis url:",response['emojis_url'])
print("Events url:",response['events_url'])
print("Feeds url:",response['feeds_url'])
print("Followers url:",response['followers_url'])
print("Following url:",response['following_url'])
print("Gists url:",response['gists_url'])
print("Issue search url:",response['issue_search_url'])
print("Issues url:",response['issues_url'])
print("Keys url:",response['keys_url'])
print("label search url:",response['label_search_url'])
print("Notifications url:",response['notifications_url'])
print("Organization url:",response['organization_url'])
print("Organization repositories url:",response['organization_repositories_url'])
print("Organization teams url:",response['organization_teams_url'])
print("Public gists url:",response['public_gists_url'])
print("Rate limit url:",response['rate_limit_url'])
print("Repository url:",response['repository_url'])
print("Repository search url:",response['repository_search_url'])
print("Current user repositories url:",response['current_user_repositories_url'])
print("Starred url:",response['starred_url'])
print("Starred gists url:",response['starred_gists_url'])
print("User url:",response['user_url'])
print("User organizations url:",response['user_organizations_url'])
print("User repositories url:",response['user_repositories_url'])
print("User search url:",response['user_search_url'])


```

    JSON value of the said response:
    {'current_user_url': 'https://api.github.com/user', 'current_user_authorizations_html_url': 'https://github.com/settings/connections/applications{/client_id}', 'authorizations_url': 'https://api.github.com/authorizations', 'code_search_url': 'https://api.github.com/search/code?q={query}{&page,per_page,sort,order}', 'commit_search_url': 'https://api.github.com/search/commits?q={query}{&page,per_page,sort,order}', 'emails_url': 'https://api.github.com/user/emails', 'emojis_url': 'https://api.github.com/emojis', 'events_url': 'https://api.github.com/events', 'feeds_url': 'https://api.github.com/feeds', 'followers_url': 'https://api.github.com/user/followers', 'following_url': 'https://api.github.com/user/following{/target}', 'gists_url': 'https://api.github.com/gists{/gist_id}', 'hub_url': 'https://api.github.com/hub', 'issue_search_url': 'https://api.github.com/search/issues?q={query}{&page,per_page,sort,order}', 'issues_url': 'https://api.github.com/issues', 'keys_url': 'https://api.github.com/user/keys', 'label_search_url': 'https://api.github.com/search/labels?q={query}&repository_id={repository_id}{&page,per_page}', 'notifications_url': 'https://api.github.com/notifications', 'organization_url': 'https://api.github.com/orgs/{org}', 'organization_repositories_url': 'https://api.github.com/orgs/{org}/repos{?type,page,per_page,sort}', 'organization_teams_url': 'https://api.github.com/orgs/{org}/teams', 'public_gists_url': 'https://api.github.com/gists/public', 'rate_limit_url': 'https://api.github.com/rate_limit', 'repository_url': 'https://api.github.com/repos/{owner}/{repo}', 'repository_search_url': 'https://api.github.com/search/repositories?q={query}{&page,per_page,sort,order}', 'current_user_repositories_url': 'https://api.github.com/user/repos{?type,page,per_page,sort}', 'starred_url': 'https://api.github.com/user/starred{/owner}{/repo}', 'starred_gists_url': 'https://api.github.com/gists/starred', 'topic_search_url': 'https://api.github.com/search/topics?q={query}{&page,per_page}', 'user_url': 'https://api.github.com/users/{user}', 'user_organizations_url': 'https://api.github.com/user/orgs', 'user_repositories_url': 'https://api.github.com/users/{user}/repos{?type,page,per_page,sort}', 'user_search_url': 'https://api.github.com/search/users?q={query}{&page,per_page,sort,order}'}
    
    Each key of the response:
    Current user url: https://api.github.com/user
    Current user authorizations html url: https://github.com/settings/connections/applications{/client_id}
    Authorizations url: https://api.github.com/authorizations
    code_search_url: https://api.github.com/search/code?q={query}{&page,per_page,sort,order}
    commit_search_url: https://api.github.com/search/commits?q={query}{&page,per_page,sort,order}
    Emails url: https://api.github.com/user/emails
    Emojis url: https://api.github.com/emojis
    Events url: https://api.github.com/events
    Feeds url: https://api.github.com/feeds
    Followers url: https://api.github.com/user/followers
    Following url: https://api.github.com/user/following{/target}
    Gists url: https://api.github.com/gists{/gist_id}
    Issue search url: https://api.github.com/search/issues?q={query}{&page,per_page,sort,order}
    Issues url: https://api.github.com/issues
    Keys url: https://api.github.com/user/keys
    label search url: https://api.github.com/search/labels?q={query}&repository_id={repository_id}{&page,per_page}
    Notifications url: https://api.github.com/notifications
    Organization url: https://api.github.com/orgs/{org}
    Organization repositories url: https://api.github.com/orgs/{org}/repos{?type,page,per_page,sort}
    Organization teams url: https://api.github.com/orgs/{org}/teams
    Public gists url: https://api.github.com/gists/public
    Rate limit url: https://api.github.com/rate_limit
    Repository url: https://api.github.com/repos/{owner}/{repo}
    Repository search url: https://api.github.com/search/repositories?q={query}{&page,per_page,sort,order}
    Current user repositories url: https://api.github.com/user/repos{?type,page,per_page,sort}
    Starred url: https://api.github.com/user/starred{/owner}{/repo}
    Starred gists url: https://api.github.com/gists/starred
    User url: https://api.github.com/users/{user}
    User organizations url: https://api.github.com/user/orgs
    User repositories url: https://api.github.com/users/{user}/repos{?type,page,per_page,sort}
    User search url: https://api.github.com/search/users?q={query}{&page,per_page,sort,order}


###Q4 Raise Timeout exception in the event of times out of request
Write a Python code to send a request to a web page and stop waiting for a response after a given number of seconds. In the event of times out of request, raise Timeout exception.


```python
'''
import requests
print("timeout = 0.001")
try:
    r = requests.get('https://github.com/', timeout = 0.001)
    print(r.text)
except requests.exceptions.RequestException as e:
    print(e)    

print("\ntimeout = 1.0")    
try:
    r = requests.get('https://github.com/', timeout = 1.0)
    print("Connected....!")
except requests.exceptions.RequestException as e:
    print(e)
'''
```

###Q5 Verify SSL certificates for HTTPS requests
Write a Python code to verify the SSL certificate for a website which is certified.


```python
'''
import requests   
#Requests ignore verifying the SSL certificate if you set verify to False
# Making a get request 
response = requests.get('https://rigaux.org/', verify=False)
print(response) 
print("\n=======================================================\n")
#Requests verifies SSL certificates for HTTPS requests, just like a web browser.
response1 = requests.get('https://google.com/')
print(response1)
print("\n=======================================================\n")
#Requests ignore verifying the SSL certificate if you set verify to True (Default value)
response1 = requests.get('https://rigaux.org/', verify=True)
print(response1) 
'''
```

## Web Scrapping

###Introduction

What is web scraping?

Web Scraping is an amazing technique wherein you can get data from the internet just by typing a few lines of code.

We all know that all the data that is present in any website is simple HTML 

---

format data. Web scraping technique uses this HTML format data to extract information from the website and present it to the website. To Extract data from the website, we would be using beautifulSoup. BeautfiulSoup is a powerful Python library that helps to extract data from static HTML websites and stores it inside an object. We can then use this object to extract data


```python
#imports BeautifulSoup in your IDE or machine.
from bs4 import BeautifulSoup
```

Now since we are extracting data from a website, we need to hit that URL with a get request to get data. To do this we need the **request** library. To install the request library, just type the below command.


```python
import requests as request
```

###Getting Started With Web Scraping

Now that we imported both our libraries, let’s hit that URL and store the content of the page in the object.


```python
pageContent = request.get("https://www.worldometers.info/coronavirus/")
print(pageContent.status_code)
```

Now, we will store this content in a beautifulSoup object. We need to tell beautifulSoup that this is HTML document content and we are storing it in an object. This allows us to use the functions of Web scraping provided by BeautifulSoup.


```python
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
```

This stores the content of ContentPage in the beautifulSoupObject. The “html.parser” tells the beautifulSoupObjbect to parse this page content as HTML text. Let’s try to print it now.


```python
from bs4 import BeautifulSoup
import requests as request
 
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
print(beautifulSoupObject)
```

The above output does not look pretty at all, and one cannot figure out what it means. Fortunately, you can prettify the data using .prettify() function of beautifulSoupObject. Just type beautifulSoupObject.prettify() and now print the data.


```python
from bs4 import BeautifulSoup
import requests as request
 
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
print(beautifulSoupObject.prettify())
```

The output looks pretty now. It’s clean and one can figure out something from this data as well.

###Scraping the text Content From Website

The next thing we need to do is scrape the data. Let’s head over to the website.

![image.png](data:image/png;base64,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)

Now we can see the data we need to scrap. Right-click the mouse and click on Inspect Element.

![image.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAApcAAAEVCAIAAAA6nlmIAAAgAElEQVR4nOy9V5NlyXaYt1a6bY/35dpNj71D3nsBBARQJCBAlCgfFAhJP0B60a/Ao36GgopQBPWgkAkEgyKBEASQuOR1mItxPdOuvDnebJ+ZSw+7qrq62szMxQyAmjnfQ3edvXPnzu1yZa5cBokIrqC1hjVr1qz5VmOtTZLUWgvwXAcYRdE/+k/+M60NYwwAABARABAAypLXOsyyhJSSc36xgbQ2WuuLkogIREDWjsejyWRorf0mrigIwm5voJQqW7zmy8M5Z5zD9Qf7ShDBWIvIGOJzbwTCqypBhDzPAQCRwfkxdGXvOdYS0Wtej2fv4VXE9d/i+pY1a9as+ZZhreWcXco7ay1jjIgYY1eFoBDc973L3jPP8jTLrlUlpWi3WkKKUjxzxtIsGw1HhggAGEPOuTFGWwKgkm/iiojglTJkzWtxXDfPsi//WBhjggshRJ7nRPb8gSKe336iixfm+VMUBRApJQEgz/PL05WHb2wMOBcnJ6dZlr5qHMYYKqWyLLv2Cq1l9po1a767EFEURScnJ1tbW0qpq7sYYxuDviUiawEAGfN9/8GDz652sowxIaSQYrFYlt2r7/u+78GVMqUUv3ZexphXqfW7XcgTDTSbDKNEW2uJ6Gr9pWw+VwggQ0QAC0REYF87IEBEIOZ4DgDlWUZkr5ctVQTnLRSMgdbmi0YYCABKKSFElsfW0EULrxa4OsWELykapZSCs0IbIUWapM8uAfClc1NE4FwBGG3sq86BiJcKEmNed2mIWCqhBaIkqiHGRMvyNICO6xhdEHCGVheaAACIMQQgYzRZY7xe0fv3SXgAgFaLyQd89hHjijNJNjEWieDyKng5T87z85+cdzodz3Pf/973AGH36e7ZcDgcjl6qFK9UwvtvvPHRxx8nF7eoZC3F16xZ891Fa/3gwYM4jhFxZ2fn6i5EDMPw8eOnliwics7CMLg6zUJEIfj9+/fq9fpkMv3ss8/zPBdC+J6HF8UuBPD12RVjvH3n7f/0t37tR3/853//H/0Hf/qH//NpEuo0zrUNgyCKV57rzmYzx694ws5jXav4ZG1n+50OP/jxh6e1qj8Zj+er5FXXhcg7W3elnScF42ymDZDVFpjgzBpjCJQSeZKiUIKRW+mHYnk2STmjLEtfMzyQXnVnq71Y5E5Oy0iXopcRaSLBOePC6gK5YECFsUryPNdSStJZVlwfx1xCAN2tW91m+ODzp+++e/9nP/qpdB2yZufevcNHTzUZKBc1rAahOFitLRei3rsv873Tcax1QfYlzUXGmq2OlCIIw6OD/SiKXj9GIYAGwH8bBH9XyE+J/tfF/Awg6O+8+8b2p7/4caV3P8Tlo0f7xfMDMgJj/Xax8Q/RZEAWmADSfPIzr7X17tvvPf7g/5pE3vNT8+feBM/z3n7r/mAwKIo8z4v33nt3e7H4oz/+k5dK8SzLDw4OX9y1luJr1qz57sIYe+edd4iIc36xFv4cxhjXc+7eubNYLofDMefs6sK2UkpKub9/0GzUlVL5xRzrC0GGUrme71niYaV+691/8E9+/VdPRxPPcyhxtjfFZ7vjdHIqWr2NZvDk84P3f3D/8Gikgo5KHrbfC+4583/5//5/f/7Bw1fVL/2wU2cPPp0YgkZn0Os0BBQjHexUcbzMGFrlOKf7uxvbt4oi19rROb5/+90kWs2Hu0ens1dPoi2XruTzlXHffO8OJztL0zBbfLrAtwc1Hlbno3Gt6iZpEWk+aPjzRVQL3eHp7tP98Wsm5mRyt9aq1aee59V7t3d2Wkm82tjaKeZFpeMWJAEZs5mj3DzPdc4cgdoJJW26tXz30ZPCvkTmkbWr1WLn1u0kjt/53vsf/uKDJI5f2QAAC/CrSv3OYLv7H/1O+6OPP/k3/+ZfFHk0PlntbCKZ+WSmKoQMweD1Q5EBABQrQE4yBCYBII9mxydLjvTqtXIAgKIo5otlt9v9dz/+aZZmv/qrP5zN5q9aGldKdbud2XxeFM9d70ve2jVr1qz5LlBqsKWUSinOORGVW64VY4xtbW3+yg9/sL29dcWKDQAAEefzxaNHT+aLBb5szv1aUCmnWgk5Zzv9t2WxWC6TQPGf/umPXTX+s588vHP3Xi30zsbLoF4fHT6YzCZRmj19+LPVYrVMtLGv7b0JLKDjKNf1PM+bnh2QlCDkdHiySjIOkGeRX+mbeDKbR8pzXN9v1pw4jgy92s4LwRTp2dlZpbPd3+xJykbzFXcDz3Mc13OkTFYzEN5yuHdyOqpVa2kSAZkoSorrku+FxtricP+oXm1JwStB06SrdLWM4nhydsSCph+GYRiQrMWTk8k88vzKcnK4WCStTi+bTezLJuIAgIhKqjzLGOfj0UgXxeueBAAARcDiJC2GkzRJE2QEYLKMAMharYtXmiWWLwxjIBRxB3UCyEyR6xcWMV7aSMdRjLFet9vv9xzHcV3ndffpZVV+d+fi5bd67au7/IC/UTvPl556zZo1f82sVqsoii5/IuI1815jTKPZ0FrPZnOtNb3Qj198ywCA9ILt8WsgoixeTqbzMGRnp4efP/jM4J2Tk9Mim45np598yubT0ceffpZLl+loeLzstbJp7g4j2wu2WLSIbcVx+GvqL7JoOEu63b6xNsuToNpMFovCFKs4KSQmaeH6fhwPXbflymw+Het8Bswp0mS1WL6mWi6U53k6TZLlUtTrgWKz4WnQrHYDtopWqyxLUtuudWq8mAzPAqnny8LzlOP6iPgqhTYCpEmapaeJ16hVcb445agW86WczqsNb3py6khAsMNF1q1XvSKfTk7SLDVssfd0yvwq54sXzQ5KjDHD4ZlSznQysfaVKv3zSwP8UOf/+3z2g3/1x5+T+VCfS/3VYq4NGMiTFK198fkimIwvHmJ2ilSAzvjkQwAJBFm6IP2ihH3O9q00yzg+Pr5//x4RzWaz6Wz2qrm4tbYoXjKYeOWd/XZDZKeTkVROpVK7ut0YvZjPlOP4fnghZS/8RV4wO/ylTx5FqzzPqtXGtXH9mjVr/nqw1kZRdHR0NBqNLsfTiNhoNH7vn/y+MaWxOgZB4DgqTTPf94HID/yT45PsQm2OiJ7n/fAH38/z3PO8/YODNE2VUtbaw8OjUrQwxqSURVForSfj0Xh87mnGGHP8SrvVoCIFxlerZbXRMnlmjIlXaaUiZkvtu5Ir15G4WESKkwZGTISu0AYUx/FktFw9s3IKgkqv31fKuVyJRy5dJQGoKLRU0upCA2PWWMYk5wwhy3KpHASrjSVruHAYUp6l2rzS2QkZdxyHM8iyXEjFEPKikEoBAVljrTXWKuUAWW2skrzQVnCudV4U+jWyhguOiADMcWWa5kpKXeSMSwZWW2QIAKSNkY6L1mhtyFrggoEBJnSevXSWXPpuXT7u17wMQRhGqxUACEQPWch4SmZhrSUCQOk6psgtMMHOreQY40IIIUSSJGSNlSHJBupFaXiIJgdbIDImJJjUEhKB5/tJkgCR7/sEkCYJnbswsNJa8J133mLInjx9ulyusuzlVxQEwfb21uPHT64t3NwwKU5ky6dztdkXP88tOYkuR8TnTnjlz4sjCACttX/x8z9vNtt37r59UTMRUZ6nn3z8Qa+/NRhsAoKlwlChKWPABXMZCgb8xZv2TN7Ts58Xjbk0FKHLlu/vP5rPp2+++f7lJwdwtc1wOVi7duzXN30nIAAyAADIztd1/kr12fOqvhHoihfNF9+Ea1a+l5tfdP9Y852llOIHBwdnZ2eXbwtjrNlq/f7v/zelFL/YiOffNQAgXu1eSyvoarXKhQAiY2zpd5TneZok9kLlVn71xpjJeDwen12pAS8mBxczBQB43iX9vG2XxuBX3uxrvVAYVrq9/tUuZc2XxPMDXeRXJQRc6SyueoOXMMaQMcFFXmRlt00I+Lyn37WjHMeN4giIGOcAYJ9XHpS2k6Vges2AgzHGGHvR3v4madSJaD6fMsYrlZq1ZrlcCCF8PySyq9UCAYOwWrpVxElUFIWUwvNCx3GNMcvlTAhljc6LTEqplFsUhdYGAKy1eZbG8UprXRR5kkTGaEs2MeOj6C+G6YPMLDnKpnN7w/9+zdkhzRaLmZRK68IY4yjHDyoAlKZJmiaI6Puh4zici/LTTZIoSxNLVkrlur5SyhgdR6vx+Ewpx/cDx3G11nG80rpgjLmu77geEixXc8651lrrQgjp+6HjuF/PJ0oEOoH4BIyBYBOU91cTwAT5EiyBV/smJCVZyvO00BoAuFCOUi+1QjovTKSLnHFxqeegUgtmtQUhOFt3cWu+kPIluZwVlJSS9NoHaIyZzWYXUwUEPB+5wxWBS1fEOWMMvugVfNVufP1Pxi6Dh3zR9a15jixLlZRf+FwuISKjtTHmy4dXKYoCygln6bX4wrnMhf7jNY+vFCgvlrlhUnxv96Hr+WFY1Vo/ffp5GFRu33nTWnN4sCuEvH3bX0WL05ODPM8RkQCUUq1W13W9R48+EUJyxpAxIhv4FWs0kTVGT6ej4+MDaw1j3FqT55klvSpOHy//6DT5MBDdutrKbXSS/GKSPXqr9p87Re+Tj38ehFUpJAGRtZVKnXG+XM7LD5hz3h9s1estrfVweDydjMqxmrHGUW6vv2mMybJkeHaslNNqdZIkGg5Pijwv24aI9Xqz2ew9fvQpAAmpGHJLplZrbm7dkkJ98Z36QooF7P8JnP4FGA2tX4e7vwV6CVkMXhsYQTIFdMANIBkBKPAaUCzAFqA1hAOwKSQTYB64VchjcAJIV7B8AJGBzXegSID7YCz4dciXwBUUS9A5+H1wwy//nVzFWD08O0rSTCpV5Fl/6w1XMiLgnFuriUpHWgYAjKHRejI6dfx6GHrGGETMk2VG0rVxJuoVT1hruBAIZIwFwNIyed3xrbmEMY4IrxkpvpRnr9ArQ3awIAyRf1PqT0c5SjnrsF2/FKhfsbL+mkPgK4Y6FVx8Q2F5btYjpzRNGOMAZK3N0kQpRWSBKM9TY3ScrPb2HhFRv7/pun6e56Ph8d7ew35/O4kjxtit229Uq40kibUuAIGIVqvl3u5DJvjGYMdxPK2LJIktmeP4g6P45233/r3qf1hVg9zGB6sffz7/fx4v/uQ2/4+Xq1kQVvv9LSHFbDrZ3X0ohOz1NlrtnjHm6Gj3+Gjfdb3R6Oz4aLfd6dXrbcHlarU4Ptkv9nPGmecFW9t3lFSFzg8OnpK1/cG263paF6enR7tPP+dcxPGKMXarvxWG1TRN8GKo/zXMd5e7cPhz2PgN8HyYHsP8CRz/GMiC5rD1Fjz6I+j8A8AhzCYgFVTvwOIXQAEUJ9D6bRApjD+F6Aze+O/g5EfQex+Gu+AsYCnBHsNiDJ33Yf8jeO+/gpM/AxHC6gBkCM42vPlbv5wUJ0u5pkqtVatW9j772XQ2FTbRxnqVtk3O4hy5kGHgpRo6tep8NonilKl8eDIqDAGCyaIUvEFVpCYromGaZ9KtVFw8G82EkGGtWa9W+VqKrykhMMYYY7+qFP8ylG5p39ASJl5YP30z1a/528vNkuLP83zHS0Cj4UmaJG+9/X4QVjlj1pJS6tHDTxaLGRH1ehvd7oaUTjmV3997bKwZj88I4c7tN8OwhsjyPOVcEJiz5BOHV26Ff7/u7Ah0JPM3g1+Z5XvT9Gksx47j9vubzVYHAB3Hn83GRNQfbPt+YC1Zaw4Pns7n0+OjvUq10W4PynG6H4SNRvvoaM9xXCFkGFYY49OjkTF6c/O243iIIISs15vj0eloeMIY63QG7XZfKRWGNURgjH89Kut8CRhC422oNCC8B6N/DfkMNn8Dfvo/gf8/gNbQfgM++D/g1u+DPoThjyCew+Zvgx7C2c+gVoPVAYx+AoP/ErIj2J2Atw3FCCIHBIFsQK0NH+5CkcByD9w+LB5DsYDt/xqIfukRCJlsPFpFyym5DYFZbrDie8enxz5biGCT6dViHq20agRutJoXlpO1gIJjvoxWYK2qeiadzLRwaNXuDY73nkI9jDW0HYiWUSWs8LXH5ZpzyGid5cWrpfjXMZc+X+0+17RfX4h9cV18zZpXc5Ol+Assl3PHcSqVeqkjZQxc13ddL0tTAgiCqhDlkiqDiyWKJF45yvW8gHMOgIgMAQhsbpZKBL5scZSIDIEpHvqiPiZd2EgI6bo+5wIApFSeHxitHcdljCOS47iMsSSJ0zTe2r47m42Hw5PSeE0XWuuCMS6lLMPix3Hkuh4ifv75h+XXa86X52NE5vuBlJIx/jVPDJwqmBHMHkMRwt6/g0obSAEPQGeAAlQT/DqwHNAH7oC1gArcBugAzkawiKHzA1h+Aigh7MPjP4P3fgWyQ0AEFODUwQ2BNNgMigXUvw/37sPsA9j9Q7j12+D/Ujb5CIyrWr1aq9WUVIvFmdbCcdyiGJIi6bhIcZ7lWhtrjTEGUIDJx+NRpRJYIo4ohISMrDWE6LoB2sISCcd1FS/Sm2XfueavhReilyFiaRNqbYFckTHWWi4lAmltmBAI1hQGkJPVjDEC4lwyBK01IAFywVEXmgiRlYvjWNphAsCLxhpG5wBMSHnRlvU7uuaV3Dwp/sxsu5zbXbFdFlKlaWxMwdi547y1pihyxjgCIF5X6CIiFzJJVloXUjqXexlwT9Qjc7bKT3zRRORAlOn5Mj/lqFxRAzy7UgkgPmexgoiAiMgQWVFkjUbH88KymcYYrYv5fJpnaWlKLYRI0kQKtbN9rxyNW2OyPJNSHew/+eVU0F9M5Q7c/k3Y+1egM+j9Pei9B9kfw9M/hNv/PTR7oGPgEu7/Puz+cxABbPwuzD4Bpwp8E+pNEBlMPgZ/A1wfwu9BZqFxDxYTqBIEHGQHVA/aFdj9v4GHwAWM/wLyCXR/DRz5y03EGTLH9b2gEgZVAPLdynJ+fHI6a7Z72eTh8HTfc/1mvZcPT07PTg1y13E558jQWsO59FynSFbgeBUVYp7t7z7kYTvwpM6lkEzZl/Sha9ZcBRGV63G0eTS//7v/xeIv/qSxcb/RqCbT/Zh3my6u4gwEF2RGZ2dhp7fRbU5Gc1YM98bBu/cahjOpi88Pzn7lvTcePHi4u3uYGM0QB3featLqs5NxUGu2q/LgZAyADFHnSXXj7e+91fnZT35KLEiiVVasU02ueSU3S4qj6/pZlsZxlKZJUeRxvEySyBqrdRGElTCs7e09PDra73T6QkhjzGh0mudZuzOYL6YvKnMZ441Ga7GYHh3vd9o9KZ2iKIwxCHzgf//z5T9/svwTA0VVDjKzOok/mOV7fe/7PusgjL6wrUqpRrM9Gp6GYTUMKwCodbFYTLTOHcddLKbL5dz3Az8I54vpbD5pt3uMcbJ2FS2i1aI/2CndJL8R/yjhw+bvQOP7YC0EHWAM3vw9KDJQFUCA6h0QEnq/DpU3ATg4IbTvgPQB+tCwABqKFJCBqgLvQvU+yAD834IOAQNgLggX/u7/CEUG3AHhgn0PdAZOA35ZtTVy3mp1OC89StHza4MNZQmEVMfRYVAdNCpVJWUQhNoYwQUgY4wFYcVYy7hgyIzRXLAQJVBQFFoqhyF5xASSEwBnaym+5nUoL7j/5pvR6PggnoX1dpoxBNg/nfzm+2+D3/yTf/Gnb/3ghwM1+5f/+oM0TVKy1aq3+/jhD37j7/W24OTwsLvVKsiv1FbNqhdnmQEqXzi/Xr/f39LevtvovzUIQD6u9nY6nliO9v/0z/d/4997S3IeNrvBRv/ho8/T/CVB5dasgZsmxaHb29h9+vmTJ58VRc44T9P0yeMHAASI9XorDKtpsjE8O14t58px8jzPsqTZ6tSq9eNj9oI0RM55o9GO49XJ8cF8NpFSEVGaxYyJjvdeYsd7qx99Mv0/PVHPTZSbuK52blV+k6cBPu+XhS/YpSIi52Jz8/bh4dP9/ceeFzLG0jTRRdbtbXieGo9Onjx5EPih74fVamM0OonjpRDKmCJJEinKqAzfmHRBDjKEWnDRfADhlk7pz8owHyreeR4Cp0wCQeCc6xUvjkOQBIgg1GX2BwCAcACX2frK8n+F+S5D5jjPohIyzj0/LHu0Vu+2cCqe48BlUt3LE0kJVzzvL5BKnTsLyV+6QWu+YziO22u3Hw8PjWXxZGI4Y5z7niRrNTHHkSgAGAnBpWSly7ix6edPl79+dzVZZRvS2f38s2HCiMBemIYgAFgbL5fKdaPVokhgtoq3/k6/xXVVFo4/klIhYpTqu9tbB3tPs+IrpM5c852C/8Ef/MHfdBu+Ao7j+p5vrPE8f2PjVrPZJgLH9fr9rVqtKaX0g4rnBwBARI7jdLsbnU7fUS4A1GpNx33mb22tqVTrlUo1CCqVsCalEkIq5Var9VajE/i1qtqoqW2HVyULKrK/GfzarcpvVtUGA47IGo2WlOdOX5as4/iVSpUxDgBEZTakaiWsVaoNKRVZiwyDIOz1tprNju8HQVBljHHGfb/SbvcrlVq5+qWU02p1e71Nx/UAoFKtl6vm38ztxCtC7oX1Bigl4lV9AD4rebkL8UpJfO5YvFL+a286IiJK6Uoh8LIN+HwDXjYMWpsLrQEAIiqKYrFYRFF0NXab53n/7J/9b6WP4mVho4tllFiyaRypVjebHjhBvd0Innz64GCY9drB6cHe2Uq3W60snkeZAYL5dFrkDO30ZJLm6Wpv9yCz2K438jRbzueFsQDApcqX8/EqngxnlVZLIMSLeD4ZzWYTp94MHIxWGUPcP9hbrBL7iqica9bcsNhtQGStNdaU8RPKvK1ExLkobUpLWWitsZYYQ8YYY5zIWmsRGWPnPXvpPl+GXro4xF6GREZkjJe1GUM5gQVABpIzAYBAZIxhjF+e0V6052KEfZ4kuOwIrDX23NO/jL3DyjMao6EMA4TsohiVhuiXZdZhHNas+Sa4jN02HA4vNzLGms3mP/7Hv5dlOV41KEVkeJHomiErbWAtIUNAZk0ZURXLvqgM/kIAYAEYMQBEZsgCIEeE80AFcHEIEpaWGQTI8DxsDGB58Hn3stalr3kdN0yjDoiMc2TsSphSVs59L/afU0buugiGyvjzi7J4Je3BRUwlfKYDfpYbmCN6538/+weFYFerKo3VL7nmo8K5YOxZyoQrjZQAz7X8+TavJfeaNd8s10bJr4z/Q1dySRkyaM4XlSwC2nLxyBJehnkjvFh1smAAEE0ZQviaiZopU2sQmPP1Knpmt05QTh7K+r7Wi17zbeOmSXEAuC7hXvLd/VIi8KUHfT2y9BVV4xeWWbNmzTcEIoZhePW7Kwf3r/8SS93ehZS++B9ICKmkSJOkjCVY7uCcl4pBAEBkQnAiskQMEYG0MRc5LRljjKxFxpUSaZpd6M+vp89CRAD77LTPNYwxzoy+CLJ9rnska7/YUe1CTwnWmmtly5FNqRJ47hBAxhl8ufovKyEAhs9FG0VknOHF9eJrFA/leMtaw7hUSuZZ+tKcpBejMizbxhjjnOvCKFeR1UVxPQj5t4B1tIs1a9Z8R6lUKr0rdLtdx3lFNpHSdRRsbWPLwRfEAFG13W3UawxISFmr1wQD6VW2N/qh756Laqn6mzub/Xal1uz3+t1W43yiTVBrtgf9Xr/blFL1N/quUpwLvCapERlnblCreMICsTK3GMK5HLXW8YPtrQ3xTBGIYVi/vdkhQLiQwWQv/ihzt5xXDNL12t3O9lYXAS+908laIKxUKv2trUpwJYNDWRtCvdVu1+uM4DKHB9kya0G55VmWZ9cLdnYGlUqFQG5tdAyVKwVEFvub/V6/36xVW83Gzq0NIuDielQJvBiR9Lc2QVuvUm9Uq5Kfy2m6uBwAsITVWi1wHDdstKs+Aas1W/1+VzL0fbfTadELtjKc8+u3+qZxI+fia9asWfNX55rRySuy4QFDVms0BTPT8ThotIvdXRDPlSMC1/PsakqMN5qdms/zJKoNNh07TS9cva0uFplpgkYnZDqZR8nFnBAr9SZPk6ChxtNICME5D4NmTcWHZ4tSOCGicv12o6ZJdaq1VMN0nmwNuvFiGIMXejxdJbPlwvV9RAZkytX1xTR+687m4+OJ7zXaDX90Nu8MWkC0nE6dIKyE3vHRUaEBkYgxrbXlXLl+f6O3msyE63muyKL5KtZa68vk3ARYbbYbFW8yPNFFFvpVjovW5sBXcjqZBLWGiZfjebR5ZzOLlrPpggmJaC1Zo4220Gi3Bt3a4/1RrVrtdOtnh6N+r7ucTBmpKM6MNgSs299cTYerKCmfEKCo1xsc0vl8UWs0n9DTqlJgMktYa/aaVbVYxo7nO1JOjg9EvbPdbx3tHjc2NuziaJRgu92I57OCbB5HzVajjOZRLlsgMiKqNDshK47PxubGivL1XHzNmjVrXocbVPq9dhbHlgAKTRak47Y7bd9VUnrdbtt3HTgPSIV5lgIwzlAIqa8kmkQgQ5aIgCEQkb2SfoMx5jlKcMRz47hoPpZhu9+un6/HE27c3rHZKteUpyvyW66gOElXq6Td69Sq7VYFQ89Bxs4N5AAAwBbEBONc+IHfbLarQX2r545TuLW9WQm9atXPjdy5tbOz2VdgpuPJ4cmoUm/22s2NbmNja5Cvpo3OII+Wo+OTVXKeuFMot98MlstFVpgyzybjMgj8Wrvba9cbjZqjmPS9bqsuhKzUGju3t7f67TyND49O42iVzObC85hy2oONZrPVa9U4F4K7CGYyXxwennBOURT1+oPALQPOY1irtxpBlqSAqI0pPfWICMjcvnenVqu2W/1mIFc53Optthq1JM0Z0nKZuK5CxjhDsqa0QQZE6fidTrfqK6Hcbrfjue5qOuX17k63Zm+spn09F1+zZs2a11Hk6WIVK8/FJC2yhBwwRTFfrKzWlux8ttTlhBsRALhQQirGWLRa6SQyxpw7QnIRuorbHAtDnEkpAdPSpE2QzlazVNYQzlOOu34VdDpbXHjBIUxGk5oXFIVdxYllsVbpV3YAACAASURBVMkypjIueJ5m2oBNstJPx/fdbJ6Xa/NBzSPgNd8JKiEYDWCjaJVkBbCw3uxAHjGT7e/tldmcrbVAWORpEi9H03mFO1GSullBRJaeTVPJWm3RUU7GE9fzlCu8SlDxeKFtmqWLdFH3HVjEZ+OZ8rzp9ChKVmCNJSJLgEw6UhuoujLP0uU0Gi3juo6mccwtGEOEhMh8z18t52lW6jAojaMkcBzXTQudp4lzGZcCMYpiXM0XGVVcSlIwvkREjmCBFEPkEkGvVqsoTksvVAQwRT6fa7LaWJzNF7oovLAmdHw6i2+uZdJ1T7PXpChfs2bNmm8H1tosy8zz+SiJKIqi3/3df5gk6VVPM0QUSjGgIs+doFrES/38+ipZ29m+7aE+Pjpy/KrniNVqZYAzk2X63F4MhajXamB0kmnXkWCL+TIqd7l+4LtOniWG+PbO4GjvsCBEk+XalKvLiMg4l1ICMLAZCNfmqVCOK1CjAEtUpEwq6Th5Ei9WMQAAMt/zA9/Js8Qw5XAWR6lyYJXabrvVbDSkoEeffbZK9cWlAwAKKavV0OS5RUzjWDpuGq3s83EgPD/wHBWvlsoPFGdRnHi+B0R5lnHpkk6S3FQqFZ1nq1VEV2oHwLASeq6bxCtDLPCdaBVJ1+MIcbRKc10OYvzQT5PUGnOxbM+ElBypKAovCFfzeaUzqDt8OD4D7gauSLMcyGYaPI7ouBxtEudh6BPZxWIppNBaF7ltt6tBGOzunSBYuBK4ynE90nlhzEtt5W4E16V4lufPXKrWrFmz5lsIWQAy5loez1dJ8S9ToeMFSop4ubAEgC+Pw1HO9i5X358vgwAkpAwCP1pFXzJxNT5/ovMMK89VigDPNwVRSOk6DmewXK5eIroQ4Qt1y2WZMkUMEcKFa93FsS+25PK4S6FzpfH4lbzphHJdR6bxShvC67f6vCpEBHpmy4/IPN8FsnGSffHV3TSua9TlOsn8mjVrvgMYRK311+R3hEWWFhlS6Sp+abf2FaTTeT7D1XL15RWiLzaerv98iTm9KYqoKF56eFngy5z46umfneXSY/4VlZR+8y+U+WqPwBRZrIvSN+2FE72kAYiISEmcnA9qvtLJbgLXZfars+quWbNmzbeEryq8L2bP1vErOllds2cmoqDWbFX9w71dg1xIoQsNjAeuk+dZmhWIgFyEgU/W5IVVkiOZVXxupi6V4zpOnsVCeZ1O/eTwNCsKuDqXhPNMiZwLBlqbi/k8PRObQinXUdEqurDSQuW4SlAUZ/AK8/tn4W64UJJzhlGcXisjhBBKmTzLr+RVQ0QCcF0Prcny3F7Ovy9V85cJ1M9tBYTryCzTWhvfl8tVyrAsg67rcQ5ZnnPGuODRKmEMLRFc0zEgAJHrB/Fy5Vaq7UZ1fHaS5voyokd5gQSglCJjgAtOJsm14ziOEvEy6W12TZacjecvuwkEX2708reTtcxes2bNmteByBzXcxzFgNp33/IuJqKlazURAdmwXtM6J+ReEHbaLccRrf72vZ2N0D3PtsAYb/a3trrNaru3Oei3G9VS/ljg27d22s3G3TtbZK3r+UpKxw1DX11q9RFQSBWGQaXeHbQrQRj6QTDoDeoVzw+CMAx93/f94M7dW5KLy1TNQgTv3N8EzjmXrutyFGEQuK6npHQcN/ADLoTjOq6jHN9vttubg44QwvN9JaXreZ7req5TqQS9jUEYPHOjV46jlCM5qzXqg05PEFNKea4npXAcVzLBkPueK4QQQriu47nK9fzNzX5QqUg3uH930wAKqTzfF8J/581bre6g3203G7WtrT4BBmFFSXHt5nuuIxjceuMNY4zyQ9KFsSQd13WUUsrzPM/zleCOG2xubtTDsN4abLQrTLlbO9tbG13ObLSYV+p1OneIp4sU8uh6QXjVG/4GcpP052vLuzVrbhDfmhQAynU3N/qT4UmeIhhDGoUnPc8t0qQgFvpOGq8QURe5BRBCKSkEF5VqtcjHSVGUVkZkiukqZpQYVtVZGsWX/uKgtbGFbrU7zJ5YSwRIhL3BYDqajKbLci25MxhgtkpI+L7H6+1odBqGIRRRu7/tC1FEo9F0ZSzBpacZ0Wq6YrzJOK/Umhut+unhdOdubf8sabhYANYq/oNHR9ubPTTZ6dnw7Gw4YRhWG9tb3WQ242FtNTpxK5WDp3tRnBp9bkDAhOp2WkkUr5ZFmkR+2EQm+puDwKsspqcqqCbT0TjWt+9sjYdjQ9BqNSmPH+8f7+1leWFcx3c9n0vVHWw26/7oeKwLzZAphz/ZG01mc8ZQSLdeC0anZ0muEdELKt1WbToeFojWGg2ICKYoCOzOnTdcSlaJcSQsc3TTyFQqvisTxqWSCiWXxveceDYuCESeAmNSOb6jiiwqLIZBkMSxNdje2vSHpyfT1Q19WW+MFCeichHr2xc/b82abx9lNFPOr8fhuokgIGNMCAFA1hqUAMg444YxRowxxpBd2HURAQmuGNkkyyla5oW+8I1ijAsEhgR5miVpcVG5GY8ntVolXs70uZkYcSGU4OXfcJEVUEgJOcRxZOUAyWRZVmjtuq4Ahkw7SnHOpRRZnpfpGoQSXHBPyUqtEXie52WuMvPc3u03c+CoI9I6Wq2QdF4URZZrZEFVOJIttQlcd5RElXaPdJHrK2HYGPc9N1osjAUupHCECvxK6HCvqlajLDPVmjtNl0mWB5XKbDqNVitrcqN1UWgCNLwQjuM5SioFOrc6PhoWtVY3mkR5XugCEBkXkmEZ6+YiRivjnDMgssZcSixE9PzALheWmGQU57YXhJnvIWhEMsY6gWNMlJwb7RPBZU4NbhAZMiF4Wbkj+eriTt9EbkxOszKToDHfwii4a9Z8+2CMSSn/1krxclaQpunV/uRVNuqMMakUkS2yTIYNG88M4aUZNiKSNYN7b7J0cXI8FK7nSJElMQmH6Swtzg3okAs/CJg1uSGBQGSSOCFEInJcT0qRZykK9ca9nYMn+5kBAXmam4sY7MiFVEpYi0AZiIDymAkl0HLHQ0ukE0OCK5UncZymAADIlHTCwMmyjJjjSJbGuefaaQZbvW49DDgXh08+nSYangVMRSllGAZFmnHHSaOFdP14sbDPJ/z1fJ8R5mkqPVcKkcSp5zvIRZEmgAIhTwvruS6RTeIYkZVJIAmAAD3X8303jmMC7joijSOmFGc8jWNdev0R+GFQ5Fm5+A+IDJmUEsgUReFVa6vJtLGxHTI9HI+4ChSjrLCCUarJQ7RKCQZpkkrlMmaXceIqqfO80KYSut1+/+HjfUYEZAmAMWatVY7HUOeZNjdW13vDpPiXdMBYs2bN3yyIqJT6dkhxAHhmb/5SRyyiarvbrHpHu3sF4WXmj2vda5lx+OrpzqsuUxgTBUHY6zVPDk/SvHixZy7NwS4Mvem5BYvzmG9wVVt5WeDSBK7c6vpBp9lS3OztHxb6OVez80OumJK/vBmIQFTObS9ysZ436aoX2UuPvVbm2q24tv25Sz8vab2w3q5XRsOTNDdYhrsr7QDx3JUNnvnyneeFI4v9rZ7N07PRHJ7P1P6y090wbswFrKX4mjU3iG+dFP8CEJAQwL6YbuNLtaZc0X6W++ub7JYvpfsNtTS6SG721RpfDqFuirz7StyYdfE19llMZrxIl36eFhAvv8uL3OSXmQQvPT7spWqO82s2R+XLXXpcGGPxChd7zzMUlYGaEcEYezGgZoyd5xO8HGIzxsszWGvJWmSszAhVFiq9Ga21ZTZEay1cjNDLveVswF60qjw/lOtW5+tkrLwoZOf5msqE85fqx8tE0dbaiyBQ561gDI21cN6M88CQV9xV4DI34uWJgOhS28YYL29JmU3ysp3lrUY8v7RyC2MMy4yPa74lEJMO6OJ6zG0iJwx9Vy0mEwPIObfGWEAlhLW6MLZ8BzgvM5OiFJwxMMYyZMYaxmVYCePlNC+eiyCGiIgcwF7Nb/41XMMNF2a/XPtv6JDly7CW4jcDsjaNl4cHh8s4Caqt2ztbgmMaL48OjxZR4lcbmxsDm8xXBXbbbSlYkafHp0PX4cNJ8uadwZOHn0+ijCMLa807t7ZdR146dFprptNJYVm7WSedP378KNU42NxqNaqlKLZGT8fDo5PTwmJvsNVt1wXS5Oz08OSUUHT6G51Ww6azX3z4kEkBRNL133jjDU/JPI2Ojw6ni8gNa1ubm1WX7+3tM6+62W2SNWfDM8+v1WthkS4/e7i38+bbFI1HEd3d7gOAKdL9o7NW03+6O7m93Tvce7JMNTJEZBtbt9oVuX+22Bz0HCWyeDWazhvNNprkyZOnSUH1dndr0HOVBIDVfPr48aNcEzLmV5u3d7Z9V+4//DgRzTdv98EWe0+eOrVur1UF0sPRWDr+anR4NF5xho4bbGxu1av+cO/h7nBRmjB51fa9nc7DB5+3Bjv9bhPITs8Oj2f5Rrs2XqZ3twfW6tPjo9F0jtLd2bldC2+2E8saAABALgTnoPOstXMvevxxfH3GTbVW26FsMUXP88PQn41HLGj1PDqZzAttSoHs1RqqiCaxGWxt57OzlFQ15MdnM2TMrdQFreaRQGtybYhISEcw4l5DUTRfRFfVpoiIjEvJiyy/uTk81nxdrP3FbwBkbZ7Gn/zig9jKbrcbDZ9+8GBvtVx88tFHscZev2fj8Qcf/CLN0kdP9ldJQmRX8+nx8clyOfv00V6eRuPR0Kt1e71OOtn/8S8eZPlFtkSypwdP/+2//fHB8TDPst2Pf3oWkafYw4ePozglILLm9Gjv04e7YbXZaTX2Hn6yfzQ82X340aP9eqvbqIV7jz7b3T+JV+O942l/sDHo98zi9C8fHqZJ/NnHfzldFb1eT+Tzn/z4J6s43nvy8M//7U+jtMiL7Oz0eL6MiOzxow8fHRzu7h1bnX/26WeayFqzGJ0MJ7M0ix98thutVqPxJKg1NgaDqq8+/eiD+Xy6d3iS5ZoIsnR1fHy8Ws1/8m/+3DiVVqN2/PTJ6WhaTmni1WK6WDXanX6/tzjd/ezxrs7mn36298lHH6SF0UV+8PTRj378s2WSmSIfDYezxep491Ehq4PBQEL2i7/8cLmKJid7hagMBoONjY1Oq17k6acffrB7cJxrq4vi4SefPt3bn08nT/aO8jw/fPLp7sm00WyHQv/Zv/5RkpvXPdo1NwEh5cbmRr0aAoHj+ZhfVfyAsZaIuBB5lhOysNash54XhHfu3G53Wq7il5FJjHS4RNKF6zm2KJQX9Pq9esUjk6d5wRm6frC1vel7jhdUb93eciXnXEp2bgBfJgQnS5aIMd7p9LrN+jpO15r1G3ADIIDl+GCYsHu3dzrd7pvvvT9oBcv5ZJnS9vZWt9PduXXHx3ScIC+W4/nKFMViseDKdxUvisJawxivtzq93uDNd9+PT59O46zUzxNRmul6s4VUkNWHh2e9rY12q5kspqssAwJTpGfDSaXe7vd7vV7//pv3fWEe7Z3evnO33+tubG5tdGpHJydpmhlrlVJCCM6wyIssnp1Ok53bt3q93tbtN9pO/vTgDJjyWfLBp4+zvNCFNsZYnX386GR7a2t2dmRkWBfJ/nBVFPlwPAt8TymutdHGaGuFkFIKISQZba3V2lhrCcha0rqw2iRpoZTjBeHW9mboO6V1jjUGkAdBGIaVWuivlsuTgz2/M9jwzcODkdbagqy5+QcfP8wLo7Ux1uii8KvNXq+3c/uOLJajZVxojVwox3EcJ/BdIpIc0yxbRkm6mo4z5qI2Rhe6MDp69Phg5+4bvV536/a999+6s/7AvgUoxw09N0sTACyS2CJI1+v1eoGnhPIH/V7guQBQmpGlSWwJwRZRki5m0zLJRwnpwpxbtyNnDMgm0SJOM7ow7yrSlAtV9VS7v2GzOCuMNYUxFgjCWrPXbggu271uv90ia+Isr9WC9YrNmrVG/QZAROlyIryK7ykEUKIunezsYGSl77qulJz7fjX0x4nud+r7ByeDmrNcLFv9u4ImAOV6MuNcSCWlCB2m54tIFhFwWavXtm7fKezjKM2B8d5Gb3h0pF1YLZe5tkSki8xYW/FDKaXgrNFsR7PTRFMY+o5yEKEaBun+xBqerhaPHz1czmca1Q9/2KV0ZIXv+64Qgntesx4+nS+Qq7v33z56/Oixg5aIrJmd7s1tcFvyUTSbrdJ793Z+/tmj2rtbyyjp3dpQwpSzkCyODvafnkExnGdvv/Nu4Igr8ZAJCJhy3/s77x6dHU4sMS7dSqO0nCWgaDnb399zpIhi3eq0dveehu2N0O9+8vmDjfp7yPmtu3eOHz18fOAUxsK5czAXQqDjVFyMUqO1OTvaZ8mYc+xt3WuFWKnWGNnFfGFm+/XuZjbZL02HbRrHOdQbVcURgTY3B0ys5fiNJ02i49MhcoEIeRqTAp2lkyInawH0eJxZo+sAjHGGIJVinCPgfDpW6bLQz5QxWOTGkHBcrQsnDOZplhW+EqIoLOccCuRSzCej6SKi5ZNqs6mEyHTBwBBAvJwnQMbSbDJBQMYFJ3N8OjPmW7vcu+ZLspbiNwBEdMK6OZmmeSEZFMny8cG46kksZlmeK6byPI/ipNLxO/XK492fDyeVZQZ3mtV4Oi1rILLWWq21zZPUcgHFZDy1PKjWa1KIcjiPiL2tW3q8ItLK9R3BEJELxRlmWWKMBsLx2ekqSRxOUZxWfZcBRHGiHJdx7lXrb7719vzs8PPdI0SG0kWdpGnucKbzfLaIwnAQLwrlV773/lu/+OhzzURYTR8fHPb7zTzPGMJ8Nuvf2WAf/dnpyNcgq5UQYQ4AiOAGla07b9QcSn/+88KQkMroPC9yo2WRF8ZCkUVn8+ze/ft5mh7tPjoezdrNGgNEROX6jUbT95zB5pZJFofaujrLhOTFYjhZAKAT1N55950PfvFRIbxaq1Pa8hljiqJYZrbnsJiz3uat+1t1wZjj+SZfMelUPDGdjZfD6M47O08m++V9Zsr3JCwXkVNxkMyjB5/277xTD52/qTdnzdcCWbtYzBHIAi6Gx0RIRHSe1ZSMASBIoigQAq1dzibpkuVFYZMh0rP4FkSURaucLAEe7u8zsoWxSbI0WiOTEinNdBpnWQTaWoB8NhoikKW8AFuubZX1GGMQEImm06m16/gZa9ZS/CaAAEFzo+GMHnz2sOarydkhVbYGlUogT3efPKlVw9X0LCH/dq/pCrrVD//yowe37r/vOzJlCIDIsMiz0+ODYsqmo+Owd6vTrGE9BCY4XOShRWSMZavJKkUPi0qjETgOIgjltpuNxwdHu9wKpOPjk/72nTtbvd3Hj/K4x2wxHM77vQ0lYyFUpVoLHL6YDj99tPf9t3baVfX08aNmvZosxtNcfe/NzmerBeei0dq8vTH9ycdPVvXKNOO/+iv3GUIzVE9Pl4lmd7aaDx492bn3judIUyAAMMaEkGFQada9d95649NHTzb7P6w59PDh4367Oh2PhBd6rrMcHz0BqngiyYq65GXYK0T0grDT69UCF8g+eXhSabRv7dziDNHkw+PjMgRVtdYfdI8+fHxMyABhNjreZ8vVYprzoBV6KWIar+YzFJyJJK9WFWO82Wp+/vGHqnUrdBVemM5z6d3e6T/+7NOo0zDJcvdsObh3mRJizU3liswGk+cvKYG4nIxTwQ2RzbLiFbk9rTm3R0mTpPyjTI3KOMxHZ3lWmCsG6ubVXrWlUP/22lyv+WrwP/iDP/ibbsOX5Yqr1XcLBOBCVWtVnadJllebg7s7G4HvNeo1o/MkSd2wefv2rYrvcsYqlYohdvvWjqcEIDiO32k1gEDrwmhdbXbfuHsr8FzHcR3nQvwg8/wgDEPHC/IkQuVt7+xUw6D01/KCwHdlEieFoY2tW71Os1ZvhJ5arZYasDfYGvRaUgrHC9vNuuCi1qjluW62W61mE8nEcSL92p27d+sVnwlZrVV81w0q9UrgV6vVdn+z1266juuHIWMiDMJ6oyGE2Nze8RyJgEK43W7Ddb1aveYo4fqhq4T0qv1uC0yRZnlQa97a2a4EYafdKtI4L0yj09/a6DlKMEQEdD2/XqtKzoHIWKo12q1G3XVd3/MdJar1ZrPRcJUKKpVqpdpotnzPJau1NtILb9++U6+GjHNttNVFURTGskazrqTT6nQcKTa2d0LPUVLVG03fD5qNWrXelGiTJGWO/8Yb96u++91cuSx9Gv82216V2qlrG4ui+Kf/9H/RWn9VzwIiq7W+lsr7yx4LZLR+hbX5d/HlWfOVWEd9uSmQtbYoCmuJcyHLnD9EhS6MsYyLC8U4kaVcayEEZ8wao40RnGuttTFlZkMlxbUeqoxryzkHojzPCVEKee4YDkBExmitNRFKJTljCFAqnOEiVra1xlhSUpYe13lhBeeIoJ81jzNEbUzpsU1EuihKj+z/n733WrbkzA701vpd+u2PL2/g26B7ODSj4SjYEyONzAsoghG60RvoAXihd9D9KEIXUoR0pQhpIhikqKaG3exuNiF0AygAVThVx5/tc6f73dJFnlN1qmAaGJDNRmF/UXW2+83K3Llz/WYZwXnrFG6tawNHee+5kG3nxjjOmfe+VQnkvfMOkCGAtdZ7zziXUrZJGo3WnohxLoW49Ep3znkhROuD7pyjS2/7dtkcANtwykTeOY/IvLNtwEjGuRQSEbyzF2kZ8SKeNnnPGPPOMSHas4GInkgKAUTWGuc9IFNSfmv9xV+qqC+IiAy4lGmmZ2NkDDkncuQ8AhIAMqG6fVetbF0CEQAJlWW9bjE7MdZfauKLXGNEBAjYhkwnIGRBbwgssPN9cowBECIBIQEGMcYdZkpTFtBGIvuG3K7X/DZZr6h/U0DGeBA8f09EVOqFPVdEhoG6TIbIueIcABTn6vObfnarRQzC8MWOEYWQQsjnqgjBxbOLh3Nx0QYiAg/URYMviCcuqyCiCp77CBHlZTrCKweJSrGrEiJj4vL2+oKGwM8SnjHO2LOje15mfrUFxMuS4kXFw5gS8vnzx/lVAdjzd3ypgudO1ppvOMi46m2QCHqvv71856fe6GDrOrllNZ6oMCEiZ3V89wf29MHqcJ+cBQCpkhvf/9eHP/tfl4UPsr6rVkxFgoPRjTYQpRnaKl+ViOA9i2++AcGoeudRBmHKcG59P2La0jIZ0t7rYvFkefg46A2a8bH/9k5j1nwuay2+Zs2aNZ8PouzfTHZHxXgmsz6PtuPriigkQtTh4PVXgePio18545A9Hbyh0bPGcyFYmPX33vjncnmEG3fKo19icq3J58noOk4/eGx7Uvnq6FG5/x7jYczjH90Z9hg8GDdvZvCrhp+s8geP3mVmBZ5Ed0vGyWr/Q+/WEQjWPMfv7q7VmjVr1vxT02bYQB53meBkm/rkVHS7Js+dNoQhC2KZpZgMmAxFFCN4AAAi4FIIEcZp2t8ebG71Bxud0Y7OZ1H/xsbujZ2d7XqVU720+dzr2izOzeyJQLEVS91YjqxnnCXsQWNmx2aVk7M8HXzV0O5rviV8w+biL0H+mTVrvg28LHFnCQj0/PHy48p7v/j1z7yf5Q/ft8s6GG0wM539+m+Z4LrxKjKECGABGADJqFsev0eiWy7PTz/+tVmc2qPjxXSpP3mwtb1TVeX2/dc/+Yu/ICAiR548Ql41//f+fCBhf25yZg9IkzUIBADEZXP8QJ8f+bV3+JpP8U1Sitbab3oc/zVrviX8jtuof2XrttZmAhGcB45AgEwQ0EU6gos0PeiaqrVuYyIQQpB3RMSEJGcJwDvLVWe0e6fTz8rxk4NPHhLQ1U4kQ8nBWkIAB+CJ3IVJHEPOyLm1dduaT/NNmov/ztq7rlmz5mWGiNwVszILANC+81SpPq9d0Vut7aVnudFPm/FudvLwl6fYJjF9rhIRaUcvxN2/SJcHnux6Fr7ms/kmafGXZY1uzZo1LwOIwJhA8PbzF7oRWeuKyWXYy6LlYtYY98KMus1ASmQRGSJ4T8iY5Bw5T5K4WC5rbf7RD2bNN5ZvkhZf8yV5mh77059AO/7//AHR1boEbX6H54q/0PiV3ORfeph1uYj5eeU/vWlytbsv08OXL//U0uJpqtarFZ4eGlycifblejz57QYBETnjzrmkt5HR6mCat1ZwV5OHAqLgDLkadLvLxVSmo2HH5kuGSFebAgJkrDe8aeYfQDjgzC/zcrRzI/SrRV5mgwFZ3RgDgFd/OIwxarOb/fYPf83vGGst/rJBRFW+ABXHobowI0DES/Xkra4MJFFwNSTUUzVGREY3xtgoSds7kmkqYjJUki5DV+im1tZFUdSGf1nluSeIo2BVVN1uFwAAnws39VQRPtOPRE258iqKpGCMee/hUsT20TtXlKWUioFbrkoZhJ1Oxtp1TaMXyyUKFYdBVZbOU5LEuq61oyxLBQPdNMCDKGwTqJNpmjzPWRCFjIq6JoIoyaJAOl3N8zqKoiSJra7mq2Zj2AMAb81qVVhPQinmrfHUyTJydp4XkrOyrFQQREmWRF/gfr/mJYcz0R+OJLrzyVQIJUlc7Iq3+XcAAUgE8d7e5vz8tLRMBYpxzrnyegVcbm/sZEl4/vh4++7Npi5XqzKN4s5o96j8MBl2yrJI2ODmreuzT96zxmhHyBABkTEiaptniFHa6WfxdHxeNWatyr/lrLX4S8hyfEzdvThUuq7KunHeh0HQ1LUMAlqeHJjs/t7I6waFAFOVXrqmQM7jOKnLoizLqmlGI3LWEJf19NiG/V4kHVEUp05Xi9nUgBgNIEkTAJqcncxLfefWjYPDQ6mUaSpCKdCJMEZvdWMceeQ8DPhyUTLGEAGYNLPjMugMOmkgWFlqwRkXzFqbpB0peFXmT56cjDa3ytkpC1MqyjjNJAMAcLqqGtPkRcWpJhlzc1rUSSiqctmA6At9eDrJhjthIBEJyK3y+arU1XSxt7vprVnmK6EiwVi1XNQa6qoUkk9PDh5Nj60xcQAAIABJREFUzcawR95Nz88cD0PF8/nM6nq6XN1/5ZVqef7krL5zY+t8PL1+fY9/S6OxrbmAC5ll6Wp6Tp68MxaIcdnvdbyuFoUZDnu6LFQ6CMAUtWFcOWvbISwRCamyTjcQmCgVxWw8s6PNzWYxKStD5JqyFlLaVWEdLWYL63y7dc6k2uh3V6tck+hlUb6YW2tFECZRWDXrxfZvO2st/rJBRM5ach6AlovFsiyL5SLt9uuySru9xDbaJt771XyGUYz56aHLWDFN4rCoytm07GeyrsrZfG7K1UzDVmiX9bRZoQQ3UX1ulgBggZ5NtxFNuTwdT+u6WszGjfFNXacRbzCJoJwXNghkXRTD3d7Z8ZILTJPwdFZvRVajHp+Pfb3CsMNcYwmjKIjSDgAwwbhgVtfn43xnL2qssc5LZIgooiRzVJxXVa3DfhZKno+b7Y1esVpwIGRcCtEGlAVAcM45g2HqZk8M4+QMiiiNAkKMu0Mzn+SFnk3Hq0o7Y7wn8na+qrd3+ug1Mmy0tU25WK1WywI5F0ohYhRFgVr/ar7VWKMn44lkgAyNaWow3tl8uQRy5GmxWJCztZ0wyEIlKuPqpm4TQHDOnWkWsyk5uypKMZlWZbNS3FmI7LIhgR6EI2v0+enJqqwdl4wzBCRrZouFs9aRWThtnVMCV4t5vipfMJFb8y1kfT96KSEi75wrq5Jz4XUNnCdxUFZ1J+QcBCKAt411VBZWxApQcKh1ox0Lo3CxmGnrBGerorjeif3Kec5VIBtnvTFZmpYGpFStHudCbWxuLBfjojbOapQJ5ctgc/Ns/9SFAoEhY4IhIMog4oLiKKyP5yxRcRTWy2W+LIbdEWprGqcCJQQHBClVEEjGuJAi6/aa48PGuFAgEFhtFrNFnGaiyWvnSDhPNJtOUSW9JJTMB0pSm/SJABkSAFlDjAnG83KVjG4KwT1RvlwJqRirVqUOAkWucp4YMo5knJMIdVU0xnez6OzoMOqNpKsYPuOf+Otd80+KJ7/Kl4yhc74uFpoIyLfZydpg/gAEvh6PNQNynpZL573nTeGTEPxiOhkjgPP26PDMOdBVjoA4mxnNartERO/c6eFjSyi54OSstZ580+i2/cY7AGjqUlfk/Ho1fc1ai7+MCBWMZxN0DXlXGytkgIy5xiALRdxlkwqoHyXxfLawDoOAlWUhg3Aw7JM+n80WMozRO+N8GAQiiGNrGdiiccPNXjNvlvkqSLtlnqvhAAGCMOAiSaKgPJhEcTqbLXicJXGnG49FMoyYna9WPO5EMmhizjkopbIkERLni0UUxXs3dmaLZRCqTidSSjFEBGCMh0GoVLh3bWM6GbMw8aauUYWBLPPpdLFMgSdptpotp6VP03g6m8owaYwLI6GCwAuxmC96vS5nIgyixdk46PQVZ4CqkwTe6soQumayrIMw7A973FXzijhHBL6xMZguZt57JqJel6TKyuPJaNBZTjxnLI6j31kH6DW/PYg8XSQGddZepBm/kkccAIC88xcpwb33gFitJgdaGOueGrS7xgPAVRc25/TlkwYAnXPnxye6rtr1+Kvtf0He0jXfNr5JUV/WfBlaCzXrPOMciZz3CICck3fIhOSorQ+UBPKNNt47re18Otnc3Quk8NZYT20aLu+9BwwEcx4AvCdQUnlnrHVMSI4opGgTiwEiADWNCZS01hJjSgpnDDHBgYw1yIQQ6B0AEGNMGyuQrCcuBGegtWWMMc4YY5wLvIzIgcgQvNYGOddaCyGjMLBGa2sZ40JwZy9SsVljkDEhleDorCfExXze6/U4Z947rTXjUgpujJFKIpEjQHKNdlxwKQSQ18YFYQBERN5o44mwXcpEMMapQDrrheTWWKXUei7+EvCVor5c2IT7T8188XMSiV9+/KIb+affuWJ5+lkN4GXqs/Vdes3nstbiLyGff1O48v/SScw555wLgqC1Lf+Sl8MLmuyqlTsA4GUnF5Lgc3brV8V70dHrc47FOYfIOGdfeLleOosBWGOeBg676i32mTJ/5vtPP7rw7fn8Xtd8E/lKWlwIsbW9LaQan5+VRUEAyCUykIM9Oz0kT+Q9svZKvsiti1yIdAubqTGefEP+UhMjInIU3FvLhBRJjzGwRe5NQwTIgLwHZIhI3iNjorfpq5V3jnRJtFbnaz6D9Yr6S8iXnCy2W7yMMSnllTe/Vo8vdP2ZknyZMi98ejWl6W8WBuD5I/rsKl/y/bX+XsM5397ZvXPv/oMP3n/373/pmQw3b4Gexa//kX3yjrONznPV6Zv5kcU0TENXlSzsxDff9vt/U2rJ2Ko+P2uTiiIXqrfHFdXnJ6K7FW/vcBH42rjquJr7oBea5bmDMEg7ZErveefN368+/IWmiNOkOjm6jMi6Zs0z1lp8zZo1a74IIjLGLObzxWzmiWRnO9m+WTw6QxmSgej+22p5puK+Zr4Or2cbiXeRXR4Bl+3eVHzjDTTO5nMgz9LN8Ob95sm7QEb0rrn5J2zjNd+49I234ZQlHVcffGzVSHWHUVetnhwjemTo57PktdeprsrxeL2hs+YF1qY6a9asWfNFOOcOHj/+2U/+5vDgCRDYcm6KFY9Tsk19euSBAwA5Y5sm3rnFlEIR8CCRceSIWNC1y5PB4Nrbb//w/ndev7Mpq/mCpz1yMhiE1ckZmaY5PQaV+FqTd7bx0eY2MIlhwlQiw4C8F6NrvjgzZbVW4Ws+zXpffM2aNd86vqp1GyJeBm4hQMaDGNGzqGPnE94bkKmFjFy1xGTE0TltkSGT0uZjooCoCGQaR9KShaac10yG0ovdKF0Wh8c8znxp5LBr8lrFgatWLO4iIqD3jRVxoBdTUAk1c9+Y9e16zadZa/E1a9Z86/hqmUk/zWXmgCu2k639eRuG1QMiIJC/8DpDxhheWJu35msgEqSKrANAurR2b03jLqzbnlmMegAgv85ptuazWe+Lr1mzZs1X5CKkqoenOcZfLPD8qwvf8Yt0BOQJdE5Xil44mbdvXbFh+0edYxEQfjnzzS92JIGLHAjPt33Z8kUaofb5pbvKpz1HWmHo8hMiavMOta7yV8v6Z3XpYgT02+Xz3F4+u+jl06eeO//grLX4mjVr1nwRjDEVBJxxAmrq2nkPRIgoextmMSXyVx3AmFQ8jG2xfHH2jBinHaO10Q0QAJJUoTPGe/fU9/Nq6YuXn+uS/sx982pMmBerX/T84porIjIhk7S7Wkwvg9M8qxKnXWuNaep2GQAAsv4oirPJ6RPv3NMmLhIeMhanXasb3VQX4xHEtNOvy8LqBhC5CoLhFuka88lGKk9zTUTdUBlPy9p6IkTohjKWbFaZjUQJzsaF7kfSEZ0X5kY3XGl7ttLeEyIkSmxnwbiyJQYQxN5Zs5gCeQBAZEEYA0Jd5gCIjHEhvbPeucvRwPNn+Jlv7ecPlhCFkETk7EW8emQsihIArMsVEbXjlcvlGCY4t862Xz0i9jZ3yfvlfNLf2NF1mc8mF0MSIkSM0kw3jTX6azoQ8j/7sz/7OvXX/E7hyXoynpwn+1v/5wg8AiCuTSbXfAPw3ttPRUAzxvy7f/c/WWuvTraUUq+++vpb3/netRvXT06OjTYyTmWc9l/7oS2WFxo9jIkIOY83rqfb1/RyAsgY59TqSMQwSm7cf8vq2nsSQkoVvP7Df7mYnQF5FacM0F2qcxWEKk6RiAsZRCkD4Jwjcs4FkQdERKbCOIhixlAIJVRgdMMYa396YZwyxi+TGaIQIogzIPLetb6lQkgVJnGS3v3OP1/OxuStDON2jMKEFFJev/cGAHjnnDFtDCgh5Vt/8KOTR+8j4yqMyXuplFQxeRdE8a3X3wZwptFCKfA+iJJbr36/zGe6qoBIJJ3Bm/+MqXDHLf7k/vDD8yKU/Ef3N7Tz40IDgeL4w2u9G4O40O6P7w4jxqUUq8L9q3vDRW3f3Olkiq+0rYzjDF/byl7bSAZxMFH9YOe2CON6fAQAyFBKtXXzfhTHVbEMokwIuXvrFRXGVZGHcSqEska3zrVAECUdIZXgQqgAGW89/hGRIw+TDoLnXHDGlVI37r+lgrgqlkDURqbavHZHBoGuKxkEjAsECJIOIqad/vVXvrOazxBZECYIkA02NnZvzs+Pu8Ptzd0bk9MDGYRShd67KMn2br3mGfdS+ab+Olfyei7+8kBA8+bJuHzPkv7t947IIt7fjF+P5XDtZb3mZcI5t1wuXnnt9bOzU621yrrZrder08cy6yZ7t1V3qGfnTIW2yGW3D0RBmhEy8qTz6ergY/K+N9zcu/tG1ulXRT7au9Mdbj1+8P/t3n717OChtXq0d7vX2/jpn/9vKkqsrt/8/T8p8kWa9YrVYrC5Nz05EFIspxMuxcnjjxDRmvoHf/xvG13Xq0UUd+oyf/jrXyBj3rneaKc72Dw/2i9Xc6mCpi737r6e9TYPPnynyOdCKu/9zo17zrm6zDev3dZN5Y0O064Q8v2f/9W1e2+cPHmYdgej7eunh4+efPirME6bqigW4yCIVRiPdm7GWW81n6gojjt929Se/MbuTdNU1+9/T+s6n5wEcWewtTddLYNbb7m6WO7/evbez71uvK0463OOb25mvVCkgeCIhKA9LGvbT9QoCyMuNhL0DKdLLThPOOeEm0nwJKxnlZUM9zphIsR2Jv7fd8/0bI7k2qkw5+LVH/wLGUTlYixuv7514/709LC3sVMsZ2U+u/X6D6UKHvzyr73zAJRk3Ruvvt3UBWPMWcs4f+9nfxUmqTPmle/9oQdwpqmKvDfcOt5/sHXj1eX0bDE9I/KMcdNUWW9Y5vNbr32PcZ52BsefPNi+/erjD96Js+729XuzsyOpgu2br0xPnixnZ4xzImqKZbh7PUk7t9/8PRXGZ08+6ox2QqXm80myfSNIOvnBx59aLfiyrLX4SwKRr93ynfP/5dHiLx05erZA9jT42G8KBnnlo6e7ZQRfbFPzrBEEFonuDzb/9JX+v+WMrxX5mpcG59zx0dHf//IX8+nUWSsTybggZ73RdrWINq+zIPK6lmkW9Dero0cNWR6EMuvn+++1LYRx6p131gZh3BlsdgYbq9lZmc+bMu8Mt7LuoLe1C8CSbFAszoUMzg8+2v7D/wyQuFTOud07r3SGW5PjJyqMVRCsZucbe7cnJ09MVRbLyfH+x0Q+yYZNmXcHI2Nqo2shg7gzcNaYpomSLIwTY5oo7Vf5LEqyydmhdzafnufT051brwgVGWOiJBNCmqZ21qoo8c5JFcZZ33vHGLYr51IF1ugozfqbe8gFEs0np85Zhizp9OxsEqVdY7Sz2uvGWnKm8sY0s3MkYgFngIkS3VCUjc0UT0Oxkaj3zlYEFAlGnrqReDgpa+8b763zC20Xpc4iXhl3axDPSm09eaDjvHF1ZU0BcLEFj4BJZ7hajIUIOoNOlHbVfLKcnDpnZRB1hltAPow7ROCd6Qw3+pvbk6PHgDg5eVKuFlIFcdqvV4u0N6jK0hktpQyixDT1fHJiTUPko7TLGDNN5Z1TYayi+PzgYW+0TeBVEIdxPDs73LvzmrO2v7GbZP26XNZlLlUYhHEQJUKGKgiTbt9aFyaZt8YxRkTkvYg78DUC8621+EsCgc/1+dHq3WlzEiBrvFM8ta6w4COWVG75nM5GLlnsfOnJCRYiOUNPsxQzxXsBjwAAyJf2yNHn6WNkKBkK56s2PeIc9k+SX93t/WsG/GodIvJ0sdj+BZFWW/OWLzYbISIiTwDs85u6OB+tZUnrskP+N7YMbZILonZZkoAQ8Uva/qx5uSGipqkfffyR8568p+VsdfCR9644+BgYz/ffd00lorSaHOuyAPAun4bDner0sa2Kdr19tZzFWc/pZrWcAbJ8dm6tfvLhuzKImqqcnh6u5lNrmsnJEyB3/MmDMl8++fhXTZHHnen07EAGqi5Wq+V0OT1njCWdHpEXUtblanZ2uFpMifz09ACAzg4e9jZ2ZBAsZ+OqWAL5usgnJ/tVuVrNp8VywTmfnR8Loepi9eTjXy8npwDAZei9yxeTOOsGUTI9O5qeHsogsKYZH+8DUW+0dXb4kHGRL6ZRkuWzMSK3zuimRkAiPzs7NKYx1jTlKu70xicH+dlhXRYA9HRPQQn2cFrGkv9kfz6IBAEIxH4kGWLtaFaZeal/cTif1XZamV4sHpyv8sbk1h6N62mhd7Igr/GD81XRCY9XjXPuitpD7/3Jkw+lDKrVUqigrorl7NwZHSUdIpqcPDZ1Va4WdVkAwLW7rxIBV8Hs9HAxOStXC/JUV/uc4eMP3uEyaOoSvG2qyll7+vijpNNDhPn5MQAGQaCb2ntXrZar+fR4/6O6KsfH+8VyXubz8dFjLmSZz08ef1gsJ0yoMp+rMORS5sup83T48D1EvpqPu6Ptqlhqo91y2szOv46z2NrT7CXBkT0tHvz54/9hrCff7919sNy/1/+vx/n/ee7E60n//cWvEXzjGwAIeeKAb2c/yMu/q1zTUXcTyPfrA+9JMqG9G0Xfu5Z9X0GTm/FJ8VeVA0deoHBUe+CSCSBqXM1ZmKkbiRjMmnc8oXFF7fK3t/70j/f+eyWiC/1H3pM9GT8cFzPO1Ebv5iDtXZrFeEQGcOFIA6SPZ9Nu0o+DEBGIPCJ/QVUT+bI8ezLeN+T6nVubnQ2GhIDI+KXhq78cDQCRO5sfD7s7jPHTycNO71bMGSIiMCIPQG2tq+1P5h8dL2e3t98U4I6nR7ujW60Al3ZET7sAAGCMsbUFwDeWr+VphsgYb3OkAOPkPZBHzslZZAIQGedBb6OZn9myaNtnnEupCJC8Y1wQkTVaCAkARJ5xDoBNVbTNCxV4Z7mQQMS5tFZzIcl77501GgCkCq+/8h3T1PPzo6rInX3mR84Yl0o55y7eRBRCciGt0a19FiIKIZFx5yxjzHvPGEPGEcAYzTlvj7CVyuiGvG8bEVJ5Z9tVZWctlwoAvHcMGTLmjEbGAJl3lnNBANY0z0zhAABAcqYEI6LGeo6tIToIhqV1oWBK8MY4zpAAnCPO0BM5ooAz48k4H0ruHAGCYGgdmedz0yAyoRRnwjmLiMjQO0dEjHHvrZCB997qprUl3Ni9HmUD09SLyUlTrrx3l0b4jAvR2h/QZXyA9qxaq73zAMA4kzIgAPLeO8u4IKB2DcN7p4KovaEhY+Q9MIaAzhrOBTK0RiNyxphzlnNJ4J3zBET2a0UCWM/FXxou0mp7N+0l/+1GU42iN7h5T+ArKT96c/QmUnO4+tte/IOYscabSA0Cxvu8M9eLLfmK5xtTXdxN9/5u/O9X5mHh3oxhfF797Obov7P6IYASqDiUs0ZvxHtA+sH8z2/3/kvFIqJmI7oGqLw9/uXkf4c2Y4OnCyVOfrX48P3zye3Rtq4n4/xouXrcWD/IdieLT4TqjaL4JJ8AwKDTfXL28JgHabq50+0dnT+M0t29wTXFBVy6dhC59z75i7D7nZ5w5/PDTInD8wdcdkZJ3/Gol/ROzn4lRDRezaTKRhJ++ehv7u79s8I6X45lsr2YfDLXfqt/rSkP5mXd793a6W0yYEQACAwxL45+vf8zFW5tx/zo/OOAwySfxuluCGUYDct6mca9s/lUUl46tj28PUh766n6txEi7z6VGNQ8e/CM2bqCS90AAN65xlWXRZv2QX+6EQAAsLppqwCAgQYAWuX9rCtdP37wTitGm9Po6Ufeu6aunhUlskZfrU5E5vKlu/L3Us4rIplndV5oBACsNfA5vFDyWXvOm6dZWS+XBrUDAKiNr83zm3eXYtnLoUClL558ZutE3jT158lkzdVPaHxywMenrRp+fhjnP32kL+Cda1z5TExn4fIrA4CmLj+z1pU2zafe+bqstfhLhiefn2u+Eb0xq96N1LV70evT0m9HO7ltrnV7N9J7R6sHkeyGsrMZ3T+Y/M+W+g6oF95Ko5HXPwagxs1XZp7haa4PpMyaptqOv9fY80S9GbAjbc9J7O6l/+mGXP1q8cFG/L2O2q1coRkwFK1Ws7YuSy1VKCWdTB+N+m8N0+y42teG9scf3Nv7F6Yea09n539v4uyDJb22sbF//Itci53e6NHRT8G8crw8zLwYZZsCsamqxlKaRAyqT5b1j25fz5QKV9P9x3/tszuo5x9N34uGb8Vhsn/4t0nnZg3xcvZR99qrgvxydbJiHSjO8tXxg/13emmvNsvx7NFm78bZ/HCjM2TeFGXNZZDGIQFudLb2j36mdl/NV0ePTiuH/U/Of3x3tPloNi5XB9ud4alJqfik09lZlrP+Wot/W+GcE5H/zEgsbToypC85u0LGgD67MCK72GsCYIieqP0LANZoBGAA+LwavlIXW0m+qOtPeaBdEQmI/EWKti84kItdp8+QnyMCgLsi/Kd8ygGRAX5xQBtC/OxMhsg4XM6YL955wVfvU2cAEdtlBvLe6laJPu+ABwCXnn3sy3+FXyD9xSEjsjZOwH/M1/EbWS8JvmQgoppVH/SC69Pyby3bSmA6tbq202XzuDBT71e5frzQx9rX8+a4G94TTNb21KHcDLuHxYcXS8zU7nQjUVPbc+OWuTmY68faeW2XxlsJimEY8EggFOYcQA2jtxQqQAQCXc7f/dWvjk7HABjIsG5mtanqZjHOzysL3XRkzLLRellOar0ClkUycLbkYtDPtjkBgeAIi2KinfbOHT959ODDR0WlAXmIVDarslmMl8eTVZ6EXclkY8pVvSyr2aqZEYgs2RKevAglE5zzOOwCeGOLwphAJpIHWdir9WxVTY3z5WL2/nu/fnI8AQAAliR7u1n3w8N3tNe1zhkP0jAO4q3pfN9YezjZ3+oOkjAt60mlS+/Xu1HfRhhj3V7/5u073W6PMXaRfpwLZIyrMOxv8jAOh9uMC+QCGUfGL9QXIuNcSMW4YJxzIYVUvdF21h+1LzkXeJlqkCuV7N4OeiMuhOB4b5R0QnGtFyrOEEExFAw30+DeKOEMJUfBkTNUnCnBlFLRaDvZvYOsXSG/WCtmnDMuhFScCy7E1rXbUgWMcc4Fu9xBQMa6o+3+xjZjLEqy7mCTC8kYZ4y3QrZH2gqpsn68cyPo9CVjkqNgKDgqzjjDnSy42Y8DwWLFr/cixdkoUZHkrZCCM5lk0cZOunf3WS5gxrgQrTxCKsY5Mj7cusa5YIxzIZ5uc3AuhtvXO70BtgcmZNrpZb0BvzyxyFgYJ8Pt60EYtcePXKjeKL1+V0jFOZMcOIK8lFZcns9RFkjOQsH2umESCABQnAmGDEFcFmuPVHIMxEXdtszTf4ozyZngbKcThJKrtBNt7MbbN59eQq0vO+OXR8o453ywuctY+1R8JX/d9Vz8ZUOyFH1ZOW2tqa2Z+1Oy88bvdUQwrR+eVsuuum+8b0yeN5+Mojdi9jBvjiyjTvMB4zs9dAAiYKHHYUe94qxGCipnUnGXAxWkARPy3rqi8Pd3421P2rMhx8jYFeHF5cRltL29nWUJIuv17p4cvb9/tnQGI5WQ80Cu1svasECkHEVVnYxzCKJrkhLOeBx0AEiwwHlG5AGh0xtgSEpwj3h7tPPk9NcBZwbUqLd5NvlYgOt0ruf17PGZZnIgRah4EAcJAHBGnkTIJQWZFGk/Doz3EVeCC4DIeufJyTDa3NwK0piIBI8CoUadjcXqEx/tpJFoXCFVNww6IacwHC3KST8QJWOMFIGjT0esWvMtABE73e733/7B+dnZT/7DX5PzQX+Dca7zRXbjftAd5I8/TG+8Mv37v5aDTVvmTIV6MfG6YYz1N3Y7g43F5DSMM0SsimXW30Dw1Wq5feO+1vVyOQMVIuO2WMq0Q94mvrqZsu/v9X76eHZnEP9lNY2R3+5Hi8YyxLevdT9eVPd6kRLsZNVc64SSs+OKZkHC0y4iI3AAEERxZ7gpZZDPzgfb14vl3Orm9hu/t1rMkPPOYHNxftJGgOGIne4gzrrL2Xi0ezOMYialaepW2YRxZkyzXMxYnHhrGJcizkg3dzfTkOO00krwVPKzUndDudcNZ7XZ6wbXunHl/B/d6B8v61+d5q9tJCvjj2yIUcLjTjtvAMAwTnujbe+sNTrrb+TTM0+0d/f15ew87vSy3mhyclAspkTAOWTdHu91qrLsjrZUGDOA0c71o8cfW10HUaqbqinz4eauMzWFCQ9CsobJQCbdmovb/UAhTUrTi2QnEB9Nipv9qDJ+Kws84qLU41J/f7fzd8dLzvDeMFo1blHbYSzHpckC0VF80dhOKALO9udVInko2MGyudGLnPe5dhuxAoSTXP+bVzd++mTx2EYsSlGqp5dQnPaywYa3hrxPuv3J8eMgindu3s9n52l/M+n0zw4e1kVORO0w8YsvyLUWf/mwjd1/tDzTVJ0Vfz1B0q557M44gParuXksMPRkCMBRtdTH5AtDZpsnB6ufEyBHBgiVeV+DQ+Bnyx87v6pXP5EsIKodMSID+AmQmdl9idJRQ0AclfFL4y0AAIIKs1s3U0QO4I0PRunOqqkx2lUq7UWDusnDaKfPNE/7Ka4SzdKwp4T0Ho0pNno3hAi68QYTcSAE52Kwud3zwDnTtkqTW1TNPbAkSBUbUTVnKKMgkTK3Hq5tfEfJmJEedDat0cPBfcYzgRR0bzBiu4O7hpjkYTfeNJ4GQSYZhknn+o2kHfkGwSh2ubZua/C9juOKU6UbIRJr7N7wVcaDXjpy1nfijZCgH/UYfK75/pqXmNb2Qxud57knkknWvfPm6smH8XBTqACIyFRcKmRchHG8uWd1Y/I5InIuB5t7Koo5l6Od6wcP39u6diefT4IwiJLOaz/8T2bj09PpxHWHwMX4Z3++3P/AWft7d3rHiyqQzHiKFBeC3egGv3+td1Lonx8uAsEA2VvbndNCb3XCe8N4XthxOS/PnsD4mLxtBU66g+0br2xfu/3+z/6iv7FjdFOXeZR2ZBBmg83r9948Uu/LIFBRujg/tkYzzoF2+o6yAAAgAElEQVTI6Ko73AyjZLh1Lcm6+Wxy/ZXvVkX+6OCRunZPz8ezX/20mY+9s2+9tbkozfV+CIx/cLr6gxv9XxwtGQIAnBf2u7vSeBKClcZ1Ivmj+6PH86p4vDw5zQn407Xw3nBr+9arcZSMj/c5F+Ts9OxQBhEXYrR7a+fmK0EYT8+OENlyeqbLZdYbhkm6feP+aOf64YN3uZDdwcZgc5eQMcS//3/+D2c0FzK79mo43KpOn8zf+7menXNv/uXt3T//cDLKwk7Au6EcpUEg2LQwN/vRZif89w/OtSNEDCR/fSu73ZGW8GhZHy3NUjf/5pXe42l1e5iEgThf1N/dERwxEjxQ4g9v9PNaL7VfNm6vE4yLaT8Utbb1cuqXc7xc+Sai/ubuxt6dKI6mp0cAFCdpWeRhnAgpN/du7d5+1Rmtm8Zbs5ieus+xn3jKWou/JCAgR8mZcGRm9UeXP4yDKwU+23OcwAuWUP7jXB84spdFLtGHn27haqcXK++tZR0gR4XIGL8wGvcESdyLgpRerDPaarNGmMV3UrWTJk/bHnZGFwURlQyRMQbIOQCQFMGod23Y27vwSQMY9fauiPE0dPNFYMpRZ+uy120Agu7TlwAAnHElFDImGQMAIuqlm3HYQwDINl440kFn8+nzYXcHgCRXaxv1by2z6fQXf/vTxXzhvUOjTbkUcQZW8yBiKgDGUSo12KzHR8nebX34yLemTAje2dnZYVOVO7fuqyAERBVGcdZFdkRExXJWTI7N7JQAbF163ThPHKEXSiJgAJHgnVDeH6UMIZZ8GMtQsH4oGMdIcsmxH8qqtkVjvdaeLkyuECDtDqRSQRQjg3w+nhzvqyDmQmT9jSTtCiGlUtZoohwQgigN446QSgZhGKdlPt/Yu+2MLvO5aarl7KyentZ1ZevC1iU5Rwip4to6TRRzFgfCE/RD2Q1lJJnk2AkER5xWhjPmibyn87ypau0ac2lojt7b4dY1claFIREtJqfT8VEUd6QKs+4oihIhhAoiq2siYJzHnWGYdtPuIEoyIZT31nvHuXDWArLFfBxEWdzpl+VqfrKvZ2emyL013hrPUTGWSMYQBOdZIE5X9SiJF5VtrD9ZNDe70SRvQsFGkXIEtaVJqQEwUax1m4kCjggr7c5KfbMXnubNnVEgATnCeaE14VllRqmqrJ2WWnEgZ5y5YkPn7Gj7GnkTBANv9WJ2vpiex1lfBUlvuKOCUAgllSryuftytutrT7OXhDbqy0+O/sePF3/pyH/FNAqIeOF/9R8tAAKLePcHW3/66vC/4Hh1dPgFlxgReUfAGf+MSe2zQNFfqq2vzGe0/xWa/8fLbbDmt8DXzGnGLkd+bYABFoRcSG910BmSd6ZaqWzg6kIvp7IzcFVhdQ1EyFgUp85aa3R3tG2dc7rmQnGpivk4HWyapq5Wc+cdEJB37fXYj1VfShCwquxGpM4qHUiWCV56Zw31AnlU1IkSAlkvEX9wvVdq8+vz8u+OFlfsNijO+mHSkZzl8zEgr1bLIE47o+16tSCiIIzr1aIs8/YGkHaHMoqX4+M47YkwyicnYdJxujLGxJ2hs7rMZ9QevvMARAj/zff2PjovHs7KUHAJuHIuQJYpflI2keC9QB6saiVYyNik1tezsNDuvNLWXRGRqNMfiSBiRHVdOKObuoqzXpT1y+VUqFAFQVPkq3zenv+sv8m5qIpFmHQ5Y2U+C5KuqUsiL8PYNLXVddId1sWyLPKLDi4ixsNeJ2Qec+diwUPBTstmKw4q4wjBEqVC5NpshCo3LjduM5SldbX3CedzbVPFQ8Yq5zxCZX0qOHmIJJ+UepQqY3zpfe19R4lZqTcSZbQ/r7R73hK+N9phQjKgulwZrY2u46wfZb06n4kglDJYLSZNVV6kwPtNrLX4SwN58pPq40n1oSX7j5wM6TNAYKHINuM3UrW5Dpay5necr5uZ9AXwwv0ZuQDyRIAMAZDcxYL21YKXT9hziU3JAzIA8P5qMBMAAIYoED0AAnAER+CB2neAAAE8EAAygFjxe6MYAPZn1bjUz7lTM8YYhzZoUps4jCFjvNXFbeQWfxk+jHGByMhbQIbIfLtTdpH7hAMAXXGia3lllJytmmXjGAJHNJ44Ikew1IZyAk/k6cJYXSASgP2UdWgrJHl/afROyPjlBAMuhGy1GmIbwLyNfw4A5AmQAXkCuggjT4SMk3eX6V6ewRE5ogNicGFIz/AiMQoBtBvRDMETOCLBkAgcEcc25RpwREcEeLH6d6URQEB/EW4KiKDdU3D+RS2LjDPGWhv79lDbMPhPz2prSP8brrqnra21+MtEmweFfusqvIUhYyjXKnzN7z7/AFqcLnOOfYm+2kcE/IzybZyiz9udIQ+e4CIYy+dIcSVgshQMAJynTymOL8XFAhO9sOkGAMA+a2ZwscvmPUMgZC8UIO+JiH2+8M910o4h2Jcp/BlmpU+3C78q/lLX/sNy1WntN8vg4erlhgDOAwCxdnDxm6qv98VfKhhy9qnf0m8NfPpnzZqXGUSkKO1ESXc2PvbOPZ1iX0YQAgJsF9y5kL3RTl3mjDHGeD4fe9/OMhkQBWEUZ70oTk8PHnpq58N00QEAk0E42FRxZ/noXUB0dJFOG5GQwBEwhNuDeNHYWakjyW/2ogeT0jnfjhZad9FWRfnWqxiB6MKKpA1J6ICw9Y0GIgLBWCR4Yazz5AEEogfaSgPB8CxvrKcL5XSRCRwAgasw2b4JiPnhQzC6Fb51IY87/cHW3sn+A+c9edcGYCbvLwIjtxISAYAIk6C/wcN49cl7hNgmIb2Anj0yBCCIldjrho+mpfEeABggAY3igHEc57W/LN1OlFstiAieABEYgL88LUQQCHZvlLx7umLtaKSdWOOlqy22KwDtrP2ZLPh0CHcxNHt2qp+q7SQQxvmnAeYQoF074XjxBC4NeQjg7WudX52uvPcOgCEqhm9udc5WzfGq9vTU77d14wWiiwDXji6GVmst/vKx9n1as+YfEcYw6Qyu3XuDcQmIcdadnR9HcRpnvZP9D6Mkizv9fHae9UaM89ViunPr/umTj6MkHWxdOzt4VC7nWX9UFXm1Wly/96ZQQXe4HcbpajkzRlutAbExGgABkYex7PbJuzubnYDjycpc6wQIcLRs9rrBrLJv7XQOF/UgkoLBG5vpo0U9isWNXnSwbBBhFKvjvOkGPFXifKW3OwER7c/qzUwxgIfz+rVRsmys89SPhPbEEL+7lf2Hx7NPZtV3t7J3z/LdJPyDm/3jQqeKJ4F4Mq9GsUwD8c5xvpWqbigeFySSDnJ+qS+RC7F9/X5drfL5dOv6nfHhwzCI+5u7+fRMqDDp9MZH+0GUJN3B2eEnwDkAohA8CFXSRcbuDWMGdJzra93QEz04KwBAMLzZDw8WzSCWG4m61g2fLKpXNzPO8GylE8W/u9V5smoGkZCMOU8PZxVHyAJ+ljdAIDm7N4wr4/PG7nSCsnGPZiVnGAn++zf6oeSnK22d3+0ED6fV/WFsvF9UJg1EKPn7Z8WdQVRbVxqfBQKJPhiX1nlETANxdxhNS1Mav52qs1UzLjQCJor9569vTlbNx5Oy3R7gAIMkMN5PS7OZqkVtP5lVHMATbKTyza30waTcjINhok7yZhiq7+12/q8H5zd68SAS758XpbbtGOvWIIoEfzgtdrshEOzPKudprcXXrFmz5isgpBpt7wVRSt6/9Qd/MhufBVEcRimXwfTkybX7b508/kjK4M6bP3zy4J0oSTkXQRBJ2eYzu3b93ltWa6HU+PBhGKcEGCWZs+buW7938uTjrDc6P3kcb90C5KsnD4rDj6uT/UDK37vW+8njxWubmbPu9ii5NbDO0fUebqbqRj/6q4fTsrG9SAnO//jOMJG4kQahZO8crYjh93e71tHNXrTViw4mVRLKYcjLxivJf7DbPVs1WSj3Z9W/ut798aNpJxTGEQH0YpkF8t4oTRQPSvyv3tg+mJS9QGaBUAgfTeu393rvHC11o4uP30UE38ZpZ2zr+t2sP1zOzq1puJBcyO5wa/vGvSTrBlFqnVvNp/3N3bjTX8yn8f3vEcBq/4Pi8GHFZaL427udn+7P740SiexwWSnOuoF04P/w1mBaWePcrDS9SHHB/+jW8OGkuN6NtfeS4XYW3OyElmg7DbYnhScqGjteaQ9wvR/fHaY//mT6xnZmtB8bHQo+DJVH6kXCAfzR7f4Hp6u397qcsR/dH/38YPH9nW6urVRiFMs7g/h81ZTEjHXGusfzOnceEf7Frf600ATw+na2KEzjKFMy4qwwrh+J8bIWnL+6ETOG88Le3UiOF/UbW50QgRg+WR7vRGqpbW2oH6tQ8dvDdJSqVMmNWI4StdsJ+pFUgjGGvzhYOKLtLHhlI33/ZJWF8s2tzs+ezAFgJw7XWnzNmjVrvhptahJdV6auyLm6WHnrhrs3kHHvnZBKW7NaTE8PHqkwJqIgTk1d6Kq0VldFzoXMF1MCcM47o4t87gFWi7GpV0GwVyymzjhAphcTr7VHzaVwHgQD6z1DNM6X2gnGjPWzymJtI84sRwAYhLyxXiFb1AZRBZxxi86DcdQ4d5Trk6IJJMsbN4zU4bJx3heNBYYfzqvv7GST0kxK3S7Cm0u7am2p1K7Qzni/qA0R3RnGDNARBIIxINdUT/08yZOzFhCFVHHaBcC4M4jSjAsFBEU+z/qbYZzopuoFewxhdfgQAPRy5rR2aIJQOg+cofUUSAwEAyTGqDRkHIWSC46nueYMu4EojXu8aO70IkdQOyqtE4pr6w+X9V4nrK07XjatwZrxBEABZ+0uuOAMAJCRcX5SaiDQxvciyRkSwrwyx8t6K1GnheaNCwEa61e1a5AO5tVkVdfWAYAnMI4kR85QOxIcJUNDHjnVjd+f1QRYWWc9cIDKk2BoPRXayYDPC01EhIQIAWfOwyiSuXb1sm60n9WGEI7yphMIIGjsxbK8JTKelGSlc55IckRE5LS2bluzZs23jq9j3cYYTzq9/5+992pz5LiyRfcOkw5I2AJQKN/VXe3YJJtG5NGQ0tXo6F4dzXzzpD80v+Xcx3kcXWk0EsWRSB626Ns7dnWXN/AmfZj7EFVgtSFFaqQZSsL6viaBzMiIyAAKK/eOtffOFUpZEiMSwq1w2OOW4+YLrZ1HuUKZcSsaDyzH67V2Lcerzi6KLI3Hg3y5nkTjNIncfFEJkSZhzi9nScQdV0qZRaNSfY5Rvnn/RiYyAASljDybIK5WckKqsZAVh1OK7SCdca1hKhjFWKgcp0qpmmfvjmIFUPeswzAlBF1CuklWtjkj2E8yRmmUCYeRHKWU4O4wXig5YSol4kGQnio7e4O46Tu9KGuF6elqbqMXzeatosPbUZrj1EbsRFnOor7N7rSChm9biDujOMzkZBcPAblllRsLcRTILCtUGlE4AK3dXDEOBoiUO96432KW7eYK3YOtNE0A0NSFAwBKcLWSSzM5SEU9Z2dSbQ1CDSg1nKl6idQuJ0kq6zl7exjnHbY/TnzOHEZsTgaxyFtUKT1KxYxnC6V2RnGQCACwGV0uucM4UwBFi4+y7HCcEgSCeKrsKQWBlBYhBYfujZOyyw9HaS1n9ZMMAAnoqmOlQoZKD+IsTI4k54hQ8axGzurFIlO6ZNFunA1iAQBS6dmCU7X5MBNr1dxhmAoFL8z6H231AyGrDo+FfNiLGAGloezy5aLXibJhJhFBKS2VKtpsf5w087bvsEe9KEyEBrAZnSs4BHQrSGd9J87kwThRMGXxKaaY4m8P/8nKpAiTQiBGn6WPC4dM2hyFk5us6Cc1a6DVcbICE2lmWpsY6Jk0jqJg+ESdFSNAg6M4KDAxThOFlEl7BAAEQRp53XEWpGNp13HLEx0ez1ab+oMTLRgiKAUKNDE3CScUqxpMRZYjrdaRaOtJDjmWrh33asRux4kO9bGmCxH14+VMTt7pkRzPhI6BubsjDaGZpzohpJ8IwicjGcmbPBaSkckaIKI2+rIjJj7q8oSY6GhFjhV/BL9YSn0ibhCPdXxmtmb8yWmCR7F/RYd3ooxTdBlpjVMz1BdVVREBgCLqpwTt5rM2vD55biAmrOxoSY+1gTDFFFNMMcXXBpo6uU9WNHucj/QXR7WWcMxPJmzaSKiP4s++aKkGnQN8Vu4hfVwcDOALhbMBxaNoZgCQRsmsQeHxFL4Y5ynoJ189/j9Qjz0pACNomEr+IcNPH8edH3U3udMTAyICatR6opAHQ1STO0UAJKgBybE2G47JG4/yNWkCgIhKazyWiwMc6edNG416Ut3JPDlMYtSRECRUSyPGf2yREMnJdCvymKy10l/chKl4pp9YxCMp+VHUOMA4U0GWKIAo06PHOzAghFIvz5w8UjJJOqlPrLxKExUOIUtMCP1RRdfHP4Ipi08xxRRTfANQggXXSjMZZAKOudn80qvjiKCTGU2OjEjExbzbTbJBnFJiOAAIQa1BgzaJRBxKcjbvhanQmhEiT0R9IyLBo9wjCCiUAgCl9WLJHSZilAitNUUitXI59TgdxsK3aSxULJQxUtVxjPXJWPKjbpWmBAHgRC41YASNvtowZdmxCg572AuMISiUpoiIj11CCSp95IYwlERMgNwXFU6PhvMt5nDaDVMNUHYtrXQvzibGJQI4nC6XvL0goQBVh4+FAq05kASUFrriWr00k1L7Fh0LiRJmctZhlHqcatBBKnOE+h7bC5OqY3XCVChVsq1hlI3E0XKwnO8Ua3H3IAuGx9VDERE16JxfzJI0S6OjmrCUun4ZlAyG/aNkz0iQUnWyQLjWptiJloI5OQBQacwcD5TUSCkhWThSWgECUgpIdJYBaKTMKtVYzgetHMvinCul4iRNj3tGQGbZPF+I2rvySyqXw5TFp5hiiim+ESxGzzd8i8DDTmBz6hDMtM7ZjBEMUymlRoTNfjyIMgTI2XSx5CZCbY+SRtGxUip6aqHgcIb7w2TWd3YHccljHqdbg7iWs2YLzrVdWc05FPFwnAyiDBGR4NmZXCZVK8zmfFsq/agbZlIrwJcXiuNEHozjIJUFmw1j0chbiyX3053h+Xq+F6af98KSzV1OU6UKDpdK7w6ivWGiQVuMnKp4o1hGQtZzVpTJrX6slSYEKzmrnrOGqUCAkstbQao1vrRQ7IRJ3Xc8Tjd70XLFlVpv9qJ+kAFC2eMLRVdoDQidIPE4IwQ9RhKpEqkrHm+N05LLKcIolXmL5m0W7spTFW/etyOpDkcJIt5vB1JqpbXL6WvLpStbfYvg5WZhYxDvDWNUsFrJ3dgZrs3m7hyOo0xeauYf9KLdfnJ5sfj2w65ns2bBut8OmYYXFwq9h50XFwrX94ZVz6q71rW9YTASJpMb5Tb3S+moaz5Tyq1StUEICYa9tRe/228fjHutJA5t1xt0Dr2c73g5SqmbK2rUg9GQF6vRwaaMI601EkJt152Zi/stlSVec1EEY8IttzafdnfR9lUWkx4FJBo0sV1quXF3X4YB4Rbz8jpLLUZfOL82Go85t9rdnlJKSomUhGE0HgdAqFOpBzsPvyyIeMriU0wxxRTfAJRA3qZFmzmUnK3nOsOEMuI77MiLq/QgzKJU5SkliNzG0zO5W/sj1DrTyma05tsXGvmVivuz263nZ/OpUPMlp5HjQaYQiWcxQvAHp2feut8+2gsFcBi5PFf4/dag7juNgr3diyxKGp41SEXJYVrpV+aL/UQMI3Gx4e8Mopm8pQHKOWucCIvR55t+JvVswc5ZNMrULU72R4nWWPPt87X8/9nor1ZzDGCcSpfRmmv1UvHSfLEzTgSwhYJDEJq+/f720LNoo2AvlRwKtGDztZp3vz3uWLRAmQCo5Nh80S257CDM5gq2TSmnpGARofROmBU5TTL12mLp1sHI5TSS2uXUd/lzc4U4zhbKzkrJASC7w8TnLBaynwqC4HLiMJKzadnld1vBc7V8N0wZQyDQiVKKCAQdTm2HjqUcJVnOphogFPJ0xRskohWkqdKMkvO13DAS8xW3HWcjmYGGdNSXaSyTyPgMKGXl+pzj5rfvX88VyuNB1/byhWq9WGn0Dv9dq4wxPr96gdmeZdvhjQ+d6izRKtx7BFprQvJzK8gd3d1nns/zJRlH7uwi5Q61HWQMiY2EFs48n4XjpNey/JKVL3Zvf0QIIqUyCd187sXnLrz7/u/9fM7P52ZrM8PRWAG0u93rN28LkVl+USuJ9Nl8PS3KNMUUU0zxDSAVdKNsaxgzipnUUqooEUkmemFKCSqlk1SmQgapHKdCafA4LTis4LDTZXfOtxZLbsGmnsWk0qihlOOZUIzgrG/nLTKXt4oO55RUPG7TI8nTUSc2pQhFh5UcpkEHqUilijJpERRKI2DR4ZlUj3qRVFpovdELDQvalLicCKXHcTZOBSGoj9J8at9mBZsRxILDCzaVWo0SkUhJCJQ97nFCCRZsFgp1ruoWHVb1LI/TgkMjocap+HRn2AnScSrCVABCwaYK4MbBaLHo9hMxTIQSqhekqdT3O+FmL0qEut8K1juBz0nTt3MWzdvM5jQRWmuI4iwVKkhEnEnfpr5NV0sORTQZ7b6zULjQyCWZbPj25iAexqLp22ZD/WI9f3VnwAn+j8VinlOh9IVG/uOdQZ7TisOWS87GIKYUXU6PrVmtRCaCsRLiaDdaaymEmy8AYvdgh3IrGPaK1UYwHnLbmZldyhcrlHFAEoyHmlAtMiLTl1+6/Prrr62urEA0IpQRy7FLM1kwFHFIuUVtVwNQN2eX6zKNieUSy5ZJCEiTfvu4GCQgkCBO4iQZjsaFfK5Rq/p5D6ScKZfynkeORJPH+fafhalGfYoppvibw39Go84oKbicILiMEESXkFhJTonU2mE0FQo17I6ScSwAIGfT+ZKTSd2OstWSG0sVCeVzSilu9+OaZw1TwQj6FuvGGSdYy1lbg9izKENsB8kwPtp6X616QupOlDV8Wym92QszqQFgpewWHD5KhdS6YLNumA2TbLXsHYzTTOuaZ/XjrGAxi5FYKlNMJUzl4SjRoG1Gl0ruOBWxUFXPijK5N4jlkUedVz1rnEqtoeiwvXEy4/K8xQ6DxOPUZnSrH5VcvtUL4VgNUHL5QtEdZ2J3EK9WvVaYEo1lh0WZjDTEmQyTbKHktUax0nqu6BQdvjWIZ31HaR1nkhHUSm/0IyE1IORtdqaSE1q1w7Tq2cNE+DbliPujRCGkUg1jsVBwbEa6YZq32f4oYQTPzeTHqdweRksl70E3cChZLrtK6/1R2sjbo0QcjpNMPqPKCGU8XyzbtjfstSwvZ1tuHI1XLry0s347HPYL5RlAksYht5wsS8I4QsuGaNSo1SilQTDu9Qc0V8ricfHUc6PNezKJ3Oossaxs1KOOTyiN2ns8X9RKijikTi4bdLWSxLKd2hxqrbVaXpg/bLUbjTolhBASRbHrOoPhqN3pouWkg07cOfiy9NZTFp9iiin+5vCfrIZyHPKEGjQlZKIqxqM01yiOBcwIYGpaSA2MoD4q7XWUEPtYGQcE0WR0IYhSaQ2aIlH6CyEaIUgADMUioDyWzxFEStBIzAhBqRQY4TqAOirDdVRcy6jbzEQn3RpRm9JAEfQJdRsCUPLFtUJpdnwXJjpLKG0mf3JNzJy11gRRgQYAikTDkSzf3K9ZFkoQEeVxvnSjv0MEeayAN7XRAEGqo8kT/CLAzOjg6NGUNMLRMjJCtAapFTnufCIGNMq7Ly0Sg0gmQnRERGTccrx8OB4oeWSva61M0RqllZk0Of6SmMTvWmueL2XhEJRCQibRbwhg4v7hi0AAExpIuFew/BJSSgjRWpkqc5PYPqW01lrGQdJvm9R4z577lMWnmGKKvzX8p1l8Ein+9YBPVQr72lc+GZz0zM6nP+N/ahhafyKc7Otc9kUs/9dpTijhFmHs2co1DVoplSVKiq/4iKfqtimmmGKKbwBE9HI527KGw6GUR5W2jyqF43Gk9uO/yUiZVawmnQM4jnUGQgxFPOPXGRGUBEBknDo5GQdaySf6NNxOGGeenw67JsQZNBDGtFKm/jfiM6uJTvG1oP+44q7f8BqtpEwimT5701uf+PcVmKrbpphiiim+ARCxUp159fXvXrz0PKUUEKnjujNNwi0r53M3j5Rw27PcPGWcOx6zXCtfLJ29TChhls1zPrPd0qnnvOaK5eWd0gxl1kntEkHiL50FBO6XcnPL1HEt12e2Qyjjrs8sl1kO93xmu3ahml9cI5QxN2d5PnNz1RffcKoN7uac0gy1rK+QRE3xLYJ+NkA/lSbmWZja4n8Z0ForpdRx+WFyjP/ueX0tmMlrrf8L5my+/RMLyYxo8jn8Wced4m8IiIzSYrGYxDEiUsv2l86KKJBJVHnh78L9TRkHPFdMhz2LoDe3HLX2AcGdmSPcKqxeYk4u6R16cyuk35ZRwFzPaywON+6AyLTWyFhh9ZKIxkiolS+CUpbn5xbPRq1tAOBeITrczs2tIOXpqKM12JU6YbR86TWdJkmv5S+eSUd9EYdWqerW54cPb+sv30+d4q8DUxb/C4DZw+v3+51OJ45jACgUCtVq1ff9bz+RGwrf29tL03Rubs5xnD/rcEKI4XDY7XaDIACAfD4/MzPj+z6l9M867hR/Q9A6DINbN28c7O8LIZjnWn5ZxCGAom7Oay6ngw4opWTGvaKMgqR3wPMlwjnPFblfIoiU83TU1SLVUmgAXijliuWCzUDrcSZZvijCIXM8atlxZ58QSvNFj7EsGBIkGoDlS9H+Rjrq0VyB2i5z8naplvZbAJCFYy0yLSUSZhWryDhMWfyvHVMW/7ZDSjkej69evbqxsREEgTFqEXF2dvaFF15YXFy0bfu/e45/AEqpGzduDAaDH//4x38+FldKBUFw7969u3fvjkYjY44TQsrl8uXLl1dXVznnU4t8iv88tNb9Xm/QH2RZCsIa61UAACAASURBVBpkHI427gLjWunxzkNQMu13WM5HypJBNxn2svGQuvnx9gPieFopkSVR90B39u1yAwhVaTJ8eMvWIlcpIEBw2B4+uMGLVcItrVU27LGcH+5tgBLZeGD5JUQI9zeTzr5MY2J7cWsHmaWVSkeDpN8a3L+qAQllIhwNh93HsoRO8VeKKYt/2xGG4ZUrV373u981m81Tp07l83ml1O7u7vXr19vt9j/+4z/Ozc2dVMweqWyOZbTwuJL2uMjSUftJqaWT9PZl7U8e/KKwz+O9Pd2VwczMjOM4X63sPTnhJ+Y5+e+X+caNu+Lq1avvvvuuZVlnzpwplUpKqYODg9u3bx8eHv70pz+dnZ01FvlXdPjVY51csZMT/opTz1yWKf6iobVOkuSLt1LE3QMgFLQeb9zWSmkhyKCtQWshzFcg6bWz4AMAjaCzcJSNBlqpLBhpKUBrrWRKSBKGAJBlmdQ6DUaEkLi1p6TIwrHcvKuV0lqlg46WIh31tRSgIe7spf2W1mr08HZ4sCnCcRaOkTIlsiwag5STAKcp/ooxZfFvNbTW9+7de/vtt5eXl3/84x83Gg3OudZ6PB6///77v/rVr9bW1ur1OmMMAKSUWZYppQghnHNzUGudpqmxSqWUAGBZFiFEa51lmTFYGWMTO9XQoSEek853cnbSYDIQAJiBEFFKmaYp55xzPpm8GYJSeu7cOSGE4ziTX0DTPyJSSs0LxpjZIDjZ1cnhTJtJs5NQSnU6nV/84heFQuEnP/nJwsKCcVGMRqNKpfLWW29duXLln/7pnyilpkMhhJTSjM45Nx0a57+ZsxnrpPmulBJCCCEAgFLKGJt46c2dmnWbdGhu0Fxyclmm+OuDVgqUAkAZRwAAWkuTrftYYKxEqkSKiEEcTqTpMokmbaRSsZRHvQHoNNZaCwBA1FLKY426lOJktzpLVZYiwmjjrlZCK621ApF9o2Cn/wbo46Ixfz14KizhT9jb0XIdf6RPrduUxb+90FrHcXzz5s0gCH74wx8uLCwYUtFal8vll19+Ocuyer0OAFLKwWDw8OHD7e3tIAg8z1teXl5eXi4Wi4j48OHDa9euLS0t7e3taa3feOMN3/f39/cfPXp0cHAAALVabXl5eWFhwbKsIAiuXLniOE4ul9va2jIsePbs2aWlJcuylFL9fn99fX1vb284HFJK6/X6mTNnms3maDR66623zp8/f/HiRUOWQRB8+OGHAPDaa69dvXp1OBy+8cYbAPCzn/2sUCh4nre3t9dsNl944YW33nqrVqu99tprlmUBQKfTefvtt1999dVTp06labqxsfHgwYPBYMAYq9frZ8+ebTQahiYnayWE+OSTT/r9/g9+8APjPDfEXCqVXnrppTRNq9UqIgohRqPRw4cPd3Z2RqMRIlar1fPnzzebTcZYEASPHj3a2Njo9/uWZTWbzdOnT8/MzDDGsixrtVoPHjzY29tTSlUqlTNnzszNzdm2rZRqt9vr6+s7OztpmhaLxeXl5ZWVlXw+r7W+fv36nTt33nzzzeXl5f+Wb9EU/6X4oqbkkyRKGNdSaqWO2iAiIVqpE4lA9JM9TV7qJw8dnzGuI9AqffoyAABEwjgiAa0QQIrMHDPPEYRQrZVWX26vI1LClFZaSUI54lEPXw9PlzWfzMjWWguRwHFddkAEQHiq3PiXdfKssf6oYHxEQEKQKpXpo1roaBbniVrxpjHjdpbGhFIkVAlhXB2EMkq5yBKtJLdcIRKtNWOW0lopgQCEcn1USN4sPiiZHslvKWPczpIQABi3jQyYUkspgYQQpFKmlFlaaSUTQi1CWJaGAJpy24wIAPSf//mf/4ibn+K/AEqpbrf77rvvUkp/8pOfTDzSxix2XXdpaalWq1FKwzB855133n///SzLLMtqt9t3796NosjY7rdv3/7Vr341HA4BIMuyhYWFw8PDX/7ylzs7O4wxKeXGxsb9+/er1WqlUhmNRr/97W/v3LnTbrfTNA3D8MGDB5ubm6urq/l8PgzD995778qVK8aCHw6Hd+7cOTg4WFtbk1K+/fbbcRyvrq4avt/Z2fnNb37j+/7CwsIHH3ywsbFx/vx5xti//Mu/bGxsGA8BY6xWq/3iF7/QWp87d86w+O7u7s9+9rOlpaVms/no0aNf/vKXhlbjOL5x40a/319ZWbFt+ySLB0Hw61//Wgjxox/9qFarTU4RQhzHmZubm5ubsyxrNBpduXLlgw8+EEIwxkaj0a1bt9rt9unTpy3LunPnzr//+7/Hccw5D4Lg7t27vV5veXmZc76/v//WW2/dvXuXMaa13tzc3NjYyOfzlUoliqK33nrr1q1biEgI2d/fv3btWqlUajQaSqm7d+/euXNndXW1Vqv9d3yJpvhSGE/JEwezLPvf//v/FUJ80x0Q5ngaNCGEUKq1JpQRzkEryrj50c8vrqksBiEIZ4hIGPdq8zKJ9LEJTiiljAMoQpjxQiESACT0CEdtKFPq6BJE5JaFhCAAZQyPk46ZFGNICCLxl87axYrr+vlCPUsCQJIr1AgloHV1bk2msVaSMoaEgNaMW0gIaKCMaSWREL88Sy1bJGG5vmw5fhINzFigNCIwbmmtzDd/sqPEuE0oQwTKuSklzrhtTlFmUcZL9dXizFIw2CeUMsaQkFyhxixHZAlhjBzdDqeUISGMMUSCgJRbCEgIoYwBaCSEcgu0JoQyboHWSChlX6zSid0EZNwilGrQjHFAIEedIwAUKnN2vpQlAaOcMFaozAOCVoIQQijTWjHOCWUAQBmbPXU56O/55aZXqKXxiDAGQGyvNLNwPo3GoLPGqZfGvV1CaG35eQAl0ogQWp49TTnPFWu25/uVeSdXiIK+eXjyCtWFs68PW5uIOL/2KmWcMl5ffhEQyo3V8uyq1nL+zGuMuxqyUn21ceryuL+XK1Zri5eCwYGSGUxt8W8zjOc8juOZmRlK6RM/K4yxfD4PAFLKBw8efPrpp2fPnn3llVd83w/D8IMPPvjoo4+Wl5fPnj1rHNSNRuO73/2ubduMsffee284HP7gBz84deoUAGxubv7Hf/zH73//+7m5OeNFH41G3/ve906fPq2U+uijj957771Wq1Wr1QaDwfb29urq6quvvuq6bhiGv/3tbz/99NN/+Id/KBaLq6ur6+vrh4eHnuelabq+vp6m6crKinlWmER/Gc/zK6+80mw2KaWEEOPfPnnjpo3W+v79++12+8c//vHi4iIA3Lx58+DgIAzDQqFwcjXSNB0MBvl83qzJSRBCJgcHg8H9+/dPnTr1yiuv2LY9Ho/feeedW7dudbtd13U3NjYGg8H3v//9ZrMppbx27Vq73VZKJUnyySef7O3tfec73zl9+jQhpNVqvfPOO+++++7y8nIYhtevXz99+vQbb7zhum63233//fejKFJKUUovXrxYq9Wazeaf/vsxxbcDSKldrlv5YnCw6S+uifEgHfWtQkWlcTbs+afOiTBMx32nOpuN+8zN28WKllIMu+WLr2Yf/kZmKWiNiIVyrVitR6O+55eTJBp3Dz2/hIzJLKvUm8NuS8qMMDscDYbdQwBAxGKl7pdnRoMu5zxfKAfjAWWWyNJg1Md8iRdn4sNtGQegpO2VZprnbCcXBYNibXXU3R73dk+9+P98/vHPEdFyXCSsu/+wVF8ZdrazeFyozLd37lDK86X6qN/SStWWnuts3a4vXkrjoFhtjgZtrYRpL7NEKTFs72olC7VF2yvli/VBe5M7nlaKW24SDSmztJKW7SXRSKRhbnbV9gqV2VOE2eGwU5xZTKOxFFmhtsgYT6Mx41au2BBZwm0nS6Jg2KbMdnPFaNRmdm7U3WOWbXsFBEyTqFBpdvcfFKoLWRIokXLHE2kyaG9H4z4iOrlioToXjnuM2dzxKGW50iwoGY57g9ZGbfn51uaN6vw5xytGw05t6bnO9r1xf5c7Ob+6MGhtVptnonF/2Npw8iVCOWWWV2yYJxXK7X5rE1AXqnNB/zBBVaovd3dueoXZ+tKlAyVLjVXQ2p9Z6O7ccXIVSontVdJkPOruSky0VoRgsbbEiOWV6+XmmtI6Gve9Yh1A5UqzTq6UBN1cqZFEAQ5olga253NuzZ56mTLL2O5aqSmLf6thmOyZW6oT2ZSU8ubNm0qpV1991RiOSqkoij777LOtra3V1VUAMIb73NwcY2xvb29jY2N5efnixYvlchkAcrncxsbGzZs3e72e2U6enZ29cOGCcdd3Op333ntvPB4rpSzLunTpUqPRmJmZMaxsDNw4jmu12pkzZ27fvr2xsTE/Px/H8Z07d+r1+tzc3GTXeTLzUql09uxZo9QbDAbPvDvzglIaRdHe3p7nebVa7dKlS8Yr8HR7w5rPDL2bWAm2bV+4cGFtba1Wq2VZlmWZ53lhGI5GIyMdCMNwa2vLtu2ZmZnnn38+DEPbtuM4vn79um3bhUIhjmPTj+d5t2/fHo/HxgXXbrf39/fNynz/+98vFAomVH12drZer3/7AwKn+KNBKPMaC1pIUIrlCjxX4LkCdbzx5ucI6DVW+vc+A6UIZdR2qZu3CmXm5nudXWq7MksmruDG4unq7GL/cAcILbnzqHWhMpMrzrT3HjWXzyXhuNw4HYyDfvvgyMeLSLlVmGnmSzNJNPbyhfGgu/zci/c+e18IkSvX3NllEQzCnYdaKXfeQ8JypTlm5xFRKSFEZnslpXSpvkgIFmsrg/1Hhfppwuze3l1EgpTarm975e7BRq5Q11IqJRbXXtNaUcqqi1Rkcb7cLNZXRBa3Nq6Fg46SWXn2jFtqerkSAGiAfKVZrCzc/fj/qy+/SAiljO09+CSOBsb+nj39nSSOlbqHlGoAxyvUV17m3ErCgWW7hNmW7SKhIkuTcJAJMbt4bufe/wFig6bl5ikg3MsVRv2DQnUxGHaXLv5frZ37IGPKrc7OXco44w4gFGfm3dzMeNArzZ+SIqvOnS03VuOgN+zuIBLO7STsL1/6IbXc/fsfUMalFpS71fnn6suXkPClSz/Yf3g96O+VZ1dbmze1Rg1oewWlZL6ygJSHvT0phRRxEoZeoermK/nyLLdsZjmV5jkAzWyXcNtyco5XdIuNLI3srZvuTCUKetGopWSGlM2f/zvu+F6hfrh5Jxi28uVZbrlaZ4TSvc8/zpUa+XITCY56O55fKcwsiSzOFWqIJE2iKYt/e4GIuVzOtu1ut/u0rjvLMkO6lmUdHBx4nletVo3JTggpFou+7w8GA2PUcs49zzNcEkVRmqa1Wm3ionccp16vf/LJJ6PRyLIsRCyVSrZtm/aWZRk3MiL6vj8zM3Pjxo3xeBxFkZRya2tLCGEYdGFhoV6v37p165VXXhkMBjs7Oz/60Y8KhcJJO9vcl+u6xiX+FX5LQ6svvPDC9vb29evXb9686ft+qVS6ePHiwsLCEwtiWZbv++Z54ul+Wq0WpbRUKvm+v7S0ZNzycRzHcdxqtdI0VUpxzs+fP7+5uXnt2rUbN26YQPNz584ZeWC32yWEvPPOO2Y/Xmvd7/cppVmWVavV73//+x999NGvf/1rznm5XG42my+//LIZfZpz5q8eSopwb8Mu1QmzxLDH/ZKIxki5XaxGSRS2dsbbD6xiFbSy/DIQwv1SdLCVBsOk1+JeQSQRHG+vpmmSxFEmZNXLZ1mSZanIkmDYb+9vjwcdZrsa0C9Vk3CkNYDWaRqnScwZD0fDcDRo720WKrVcsZKlSbB5N9p7lIWBUhK01lol0RhAIaFKxOXZ02k0jkbt2tJzhFDXryRR4OQrtlcgMBePOqXmmWB4WJxZJsxizJo/+z/aWzcI40rIXLnR3V9vLF8adXaScABAi7VTrUc36iuXRRI4uZKbK2dZhIjF+umofzBi3ZmFCwBAmEVtlzt+vdQs1JbDYYsQxrgr00jbXqlxmhDml2dFEig75xRm0mgkslSDBkDXrzhANKBWWoqYOX6+sqCUAi0cz0dEgpjGY8vNJ6Mki6Nw2ELE5uorUoQyCwv1FUUYUlKsLKRJLESaJqHKRHn2zLD1iDHLdgsaCKFs3N2vLz0f9Fv5yhzlNuU2oZbl5EqNVUotDQop1SIm1KHcc/2KFgmIDIAQSpunv+Pka6XZs47jW24Jge4/uAIAXmG2PHvOcf0o6I+6B7aTd7yKlCEhUG6c8QqzzbXXRp0DJRUSVplb8wrVNBgw7iEyyl1qWbZXDEdt1y2FwwMldWfnc786R5klsoAQPWXxby8QsVAozMzM3Lx502wMT2TnWutut/urX/2qXC6/8cYbhBCT2W1yrXk7kYBNUpiZ1wAw8W/DsQfbCLbNuCe1Y3gME+H229/+djAYNBqNSqXi+z4AbG9vm26LxeLKysrvfve7Tqezvr7uOM7i4qLxDTxxaye57WSg2mQyE+J3HOfv/u7ver3e4eFhu93e3d09ODjgnL/wwgsnE7nYtn3q1Kl33nlnZ2fHRJSZbqWUQRC8/fbbSZL89Kc/PTg4eOutt6IoqtVq5XLZcRzbto3Ez2gGv/e97/X7/YODg263u7Gx8ejRo2KxaAzr2dnZy5cvTwSGQRBkWZbP5wkhZ86cKZfLnU6n3W4fHBx88skncRz/5Cc/MerCKYX/dUNLlfTbIgqVyML9TTjYlmlEex1AIkQ2fHgbEGUc9e5+prWyy3VQarRxTyno3v5IxtFERbV57zqhTGaJBuwebIMSfnnmYHt91O+EwSciDsfjEaFcCXGsddPReLD9+U2CINJUa6k1bD+4zWw3jQKRJSfKr2iRpmkcEkK1UgiAQuXL8/2DDdCQypBQHo16XqkZ9g+VSLxCHTQWa6uWW5BC+jPLWgN3S5Tycf8wDodZEh5u3MySEJForeJRj9sFym0AlCId9/cpIVEwsEa9JBonaWLZ7jgYcNtllkcoRaCj9i6h9uBwCwCZ5SmlRRJS7vZ272dphIhSCkKwt//AzVUBEAlBQkatLSGO0pv399c1gMxCxi0phALd3Vs3E9Ba5ssLiMjsHGU8QxYHA8ZsKeIkHIkkPsxuKpGJLOGWg2hZbjkctgAIUpalCU8Syu1w0ErG/XjU6x8+SsIBs5w0SfzykuUM7FxJZjGlPOwdpnFsOUWRZvnyou0VO9v3AK00zfr7jyizpXAAQKRpFo5FEqVxoIRIeJ87BZkSxn3LLfb2HxLKk7gfDtoA2nYKMk2zJAr6Lco4AOPcSeOQUEsKxSwfqUyiEXR2me0jZQA4ZfFvLwghnuedPn365s2bV65cefPNN6vVqlGRRFF08+bNDz/88O///u8RcW5u7saNG/v7+4VCwQRudbvdwWBQLpef2FA3drDnebu7u2EYep6HiFEU7e/vu67r+/5J8n5iPkKI+/fvb25uvvnmm5cuXcrlcgDQ6/UmJM05X1paIoTcvHlzfX19eXnZ+OS/GiamK0mSLMsMhXc6HaN9U0rdvHkzSZLXX38dAEaj0fr6+r/+67+ur6+fP3/eSOEMLMt6/vnn33nnnU8//XRpaWlmZsbog6IounXr1meffbaysqKUWl9fv3bt2k9/+tNLly45jpNl2e9+9zuzpEmSPHjwIAzDF1988cUXXwyC4JNPPvm3f/u3ra2tF154oVqt2rZtXPGImCTJp59+Oh6POeej0ejq1atGnB/H8f7+/m9+85v19fXBYGCecoxTYcrlf73QWmkRjgAxSSJEBESZxEfhmlkChMgsFr0YAWUcGlIH0HGvZR5jwYhgBp2TnXLLPtxaj6NQZKkOAwTQyZGfCY9rrmRJkpm4TfMPMYmjOArhyb9fHPf2onEfJ5Lvo1CmO6A1YRSAKJGdCG7CI/U4oHkS6O7ePyEW05MGTxzRSjHbptQChDgYdHbunRSZc9sm1MrSUIkvlPnHwx13orXWinLO7RyAikY9Qq1JDycaT45obrmUW1HQ7+8/fLwBANw3R9o7dx8f7mjy5olcySy79VuCLI1HUioEPKpBB6CVjIb7MsuyLDILgATScCBEqo7qlJ+Y/FMRAide66eOfNmpyduv6O0xTFn8Ww1CyMWLF7e2tj788MMoitbW1nzfT9N0a2vr6tWrKysrly5dcl33xRdf/Pzzz9999900TUul0mg0+vDDDwuFwvLysjHfJ0DEYrG4trb28ccff/jhh2tra4i4vr7+4MGDCxculEolk7j0yyjHBGulaWpId3d39/79+xM3ACLOzs4uLi5+/PHHURS9/vrrhumf7uTka8uy6vX61tbWtWvXZmdnB4PB1atXJ7Rn2NS4681bxph5OnlioRYWFt58880bN278/Oc/P3/+fKVSMQ7/zz77zBjZtm0bcz/LsiRJkiTZ2dlZX183od6I2Ol0PvvsM0pps9lUSsVxbPbCc7nc5cuXP/jggytXrly6dIlzvrOz88EHH5gNb6XUvXv3+v2+Mc2jKEqSxPd9x3GUUhsbG7u7u+fOnfs6DzRT/GUCKbUIpVImaLmgpRJCg3rsjwgRAQjjKkuOa5HDEw0IIYhUSWHOSpEFowGcaPf03+Qz/06feVCK9MuCxCbOsK95t1+NLA1MLbUna4IhpAlBRK2eDid7AhpTkkRDw+g6jb6qLUKWBPC1uv3yPhCCfnzciTq50ogw7Magwbg6AAARU8Q/suLZnwdTFv+2o1qt/vCHPySEfP755xsbG7ZtGw15s9l88803TRD54uLiG2+88fvf//7tt9/O5XJhGALAm2++OT8/b1KXcM4nW+ae512+fLnT6Vy7du3BgweEkCAI5ufnX3vtNcdxTJzVyWwnlFLbtk2ek+Xl5Wazef369VarZbTllUqlWq2Ox2PzJ5TL5Z577rkbN26Uy+W1tbVJuhjGmOnE0Pakf/P2pZde2tvbe/fdd40zwAjZTHYX8xBz5cqVUqlECBkMBufOnTt//vwTij9EdBzne9/7nmVZV69e3dvbc11XKRWGoe/7Rm/PGFtZWTl9+vS1a9f29/fNE0mtVtvb2xsMBpZlnT59+v79+++//76xocfjsRHTOY5z+fJlE1a3t7fHGBsMBoVC4eWXX7YsK5/PP//889evX3/rrbc8z4uiSAjx+uuvF4tFAPj8888/+uijarU6ZfG/VlBmlWorfnWuvXXDXlgV0Tg+3BZprESqNQAiZUwJoaX0Vy4O168TxkAppSQyBhpAK0ACAMyyrepsuLcBGpASrRTPF0GrbDyknMkkOYoN/+Px7Gv/VPw96e3ZCeMMEX7dTpSWXy/rnAal5R9u9geGA/1YJ/qxU1I83vhPu2B/AuC3bkZTPA7jWDZisXa7nSQJIpbL5bm5OZO1zTiFwjDc3t7e399PksS2bRMh7bouAOzs7GxsbJw7d25mZsZsimdZ1ul0tra2er2esc4XFxdNPFsURXfv3rUsa21tzejV2+32rVu3VldXm81mlmXb29tG0Wbbdr1ed1330aNHS0tLy8vLxjDt9/sff/xxoVB45ZVXjMUspbxz504URRcuXLAs68qVK8a6neRDDcNwfX394OBAKVWr1arV6ubm5qlTp0zE18HBgckhb+R1y8vLJkr+CZvDLNR4PN7Z2Wm1WmEYmq36ZrPZaDSMas/Y39vb22maWpZldsfv3r1brVafe+65LMv29vZ2dnbMWKVSabIsUsp+v7+5udnpdLTWRvM/Ozs7SaW3tbV1cHBglqXRaCwsLORyOa31gwcPdnZ2nnvuuSmLf6tg9m7iOD75A2jkDv/zf/7fURTj1w0r0LlibfHsG16p3t2+0Y8HWRSkg7Y7u6izNGjtuNVZarnB/gb3Cv6pC6NHt3Lza9HhloxDb+5U2j2kjsv8okxiFUdufaF/99P88jkgREaBOzOrlerd+shtzKssDXYfTfOiT/E0piz+lwETxp2mqUkOapRuJ73Kxq2dJInJeDoxfI3EWkppWdaE+YyULMuyNE0BgHNuHZciNilItdYTjboQIkmSSQ5RKeXJUUz/jDHTg6HSKIoopRMNvFLK6MCNLj2KIpOMZULD5u6SJDHjIqJhWcOR5nKToOPpG396oSbtEdFMe+KfN+lXJ/M3yWhN8Jh54jHXZll20mcwuQuzm6CUMq6Fk92aVTJafXPKbLeb3mzbnmZg/Vbhq1k8jOKvGRyotfYrzdOX/5dWctR+uPX5J0qkWiuvuVJYPte58X7x9PNx9yBq7ZQvvDreeoCEls6/HGx/zmxXCRHtb/nLZ9NRF5glgmF+cW348Fbl+e+Guw+tYkXGAQLp3b9ql6r5uZXenU/TUe9Pmulzir8GTD3qfxkwrPAVTGAaPLELDsdB0k8fNMefPjXJEjWBSV3+ZW8B4OSsjND9iXhuw9mTt09vlj99d5PXpkNDsV8HX7YOk96env/J+ZixnjkcIcSyrJOSupPdPjNT+pct8hTfZhg919c3b2SWSiUdrxAnkcoSpSRSigCjzfsyTcKDLaTMKlQBSdzZ5/li0mshYDrqMScHhGTBMDrcliJzqk0lUup4hHHQOjrcVlli5coAQLgV7D4SSTzZU59iigmmLD7FFFNM8QUY446DJonpV8LwvGYURNSNVYJaWZaltEKCatxTQjAENWgTZlmFUnawYXFGZJbtPZRZorIEnDxVIuvsEC0RNMZBsv05Aa0Gh7J3mEVDRCLiiCPoYUckMSfI/myFfaf4FgK/lt9FTz3qU0wxxd8cvsKj/pN/+Ecp9Vd71LXW4jjjAqXM9goaQIo0iwL9LFuZMEtrZXRSZuMJ4Lg41YkivwCAhFA3J8LAFEr5ovEUf3ughFL6B54m5TQD6xRTTDHFSSilhJBfzeJGPjIJsIyiEACOPfHPIF3EBJ5whWv9BIsfh3yBDgMEPPKdIzzWZoq/JZgIo69uI4SYsvgUU0wxxR8PrfUzWBYJsajWTIsEviyUeWKFE4KASikNGpBwxsVRbPczDfungEgsT0sBKvuqMqNf2QNQC0EgYSpJnvLjmpqagIRSEI/bMwAAIABJREFUAlLIp27nKLealikAAWCOZ8ssTdPk2VHu3EHQWgst5OPpXJ4uY4oIRMPJBUREACQAykS0Uca0Vkqpb/isg0AoEkTKVBqZkQmzgVIi05OpLY+gkVlcCvHMoqXPuEcEJETJrxkF94cqqyIityFLtdZIGTKmkqMweq31tEjDFFNMMcU3AwIgoWD++0wKp3l3aY6XmtSyDMmZiyizkFDCLMoYAFLKKWXUK5Vn6kgoZRYwO1+qEsoZ44TSo0sQkR3Vx3wcGpFS2/EWLzC3RC0LEJAw0EAIpYwi4ZRbRs1KCNWAhDwjvoNQyyqvOIUCLzcM/xync6CEcURKuQWEOqVGqVw1QRuUccosSpmJ1OBuoTCzaDOBCE55Zf7U2dr8EiXPYCbKLbtx1i41WM5HAkiYyTpHmYWEIOWUcURCCKecIyV+aZ5TRphFKQEklHHCuFeezfs+ImhgTs63HPeokikQyixCiUakzCKEIKGU8WfwOyE0X7FKdbs6SzhHAESWry6VVy5WZwqUccY4YZwyBgCEWYg8X5xBytnRQU0YZ4xppJRxRCQEQSOlhJhboLS8sIqUImWUUiSMMI6AgGDSTxOKaGqpMkY5p5wjEso45Y9/ymbvhTr2/GliW4DIK0u5pbNw4nFtaotPMcUUU3xTELexGLd3nIVTwf1b+mQSNmrZM3OUFfKL+TF3mEVlGqOK037XKcz6niuBaxVYfjVoH1bq8zIeBVZ5teaGyfVStRmKtFr2tTdb9XA4jhAUszmnKoJ80lof9jonrVKg3FtYgzTNLV1QseD55vjBA6c5E2zvVeYWUAvG7SSTnuuNB2GpVtrfelQt57c3Hn6RawEJcYpOpWY1L2In0+XTqIkmiFE/C8PK7GoWDSynIOWY+zOZpmUajYYjTZzl82vhKGVKx3FHW0WK2qs0O+F9nVq5+qlCWfJcqb1577FUq1rz+optUXvxouo9VO5y/Og6q6xEDz5zS/VcoZqEnXy5GQ2HzLItziWzxGi30nxldHhNUs/zaLs3qlfKo/HYn1vDwf04eiQFy/tlVq2TYV/bftof2KWcTkfdiNR8OxDCIkRGg/2dHYBj2kNEQnh12S43CCriucg8PdpHr9FcvVCq1AafD9FfdZmWKtXUOrh9vbRwFhJRqJVTLM3P5ce9fiYyjYhaaStPskRTYqnx7na0eKYWo2+jHvdaq6/8fTIaeuWGQ1UUuQ62WwcHktDyTD3JoF61DrqklIc0HCiet5xy1N/3ikUlRX/3URgFX3zQGpA57tI5ziE52Kf5kjM7N7r9MaDJFDtl8SmmmGKKZwMZ51pmQBiAQiRaCqmMMl2zyoLjFd0iDwj5giEAiJ2zq3NqGBDGrdnTQDNSqGW719POXu3cd8L7H5WXVoa9TebPz9hurTYXDrsqtTiXXqHRXLs0CsezRSvO2UW5Ld25uflqEg44g6EuHxzee3x2gHbFW2yMb39OcwVenLHrFSkdzocB9/xyXSvqu+nudqexdjnXG1QX5rxcDpPO9sZjKdZ5sc4rFSCIjFtzZ+R4bNVK4d1PkJDm8tLDGzfr842DrX711Kujg5uu5c7Mk2CsF1Yb9+6FBQfzGfGXX1r//VtA7Fy5kUcf8jmpB0abBSfStWlB3ZXn1O6nQCxeqKjqLISJM18PH9zwSw2baUXq87XSoyhurL5Ko92hKBRLciS8Yn3ZLdcsCxL7sJRjmudy+VLYk35tGTNSKhecM89nd66oxnN2/jCBOF+YdXC+Rg7bMeQd0rp3lRB8LKGcFu7Sc7Kzi7Znz69m48StVxSrlWdmZsr10UYuP7OWl6Ms6yr3XLz7qLlykURpfrbYS7pzC2JbWTNzje0Ht/sxnl9d3n60k2+cqeDOztbh4tqZdlwgcWARbeUKyq2dunhZRoNwXNfdn48Ks45nVRdWFPqNhov7wlWHg47KN0475ZVw946Vt0bDaCYZbO4EJ13sCAQJpcVZLtKkuweLSye/CFOP+hRTTDHFM4CENeYXXJuW6vPFkl9rNDxuH1uxKul1c2cvh4/uwBN+Y61BS81Qi1SnoQwGxPakULW5VZkA4VyBJkgRdJal0fAwHA2zwTCLMzs/o1WqAJSUKkv7B7tZNAalR539zt5mHA7jcfDUZq3UGoE5Oot1FkQH27nl5WSvXZlbFPE4HHY0ak1JNDjkFnR2thora929TST4+HQlaI2gQUgZDuR4jCIBwOpMSSNBBAVIkOs0EGkah6NRv5NmcdDf7XQPRr19KTOVKUol6Cwej0b9AeMYjUdZKgjhJ7fFETVIAUhAC5XGydYDXltONj7N1U47jqMpB62AUCAg0nE47obdLmUyDAZKZlHQ3t/bjcO419rKolE6HksF8bgbDPsiy2QWjwatYBwQnQTdVprpNArDYbff2o2G/WA8fnxzHgFRS42MgNYqTbP2Hcg3RH+jt/XgYPf23t52Eo1HvdawdzjuRV6haBFTZ1EomY26W0k0RgsJKoZKKqVRyXgALF9ZrGkpk2A46HW1yMaDEAGj4aC7txHGo+FwKxr3xr3DbneU4/FuG3M0HA0HYZo5FOM0pYwj5YAqyxJ84nNWQoy72XgEQHSWqcdzy0/DGKaYYoq/OXxFpNmP/9dPskya2iT5YiEJBtTxQSaU8SyMUilNPkEsrxTOn2u/8zP1eMZvpJZVqCBj1JZC5FTQZX4lG7bzthMnxPGIBgJaUNuLhj3XtkSWZSkplPNhKhzHSWTmMhzHhIQtTR03l8/SUMlI2aWktZU9ppZCoNSpz0Miac7Phj0lE7s8E+9vu6UqpKFIE69UzgQQlRHuiiQszNTbj24n2YlOEImds/IlYufkaB9z1azfYy6XcZi3LbRLadjnbg6kIJxHYchAjIdD5G6l5vYG0qNAGaFWRetAAxm3HgnFveqCw1EIMe7sy5NqO6VZtWlRAtxXaSCzmBUqovWA2nWLa8LdLOp7xUoSRIgIIhHS8rw4TPKcCSAolU4SYWOikVOeJxD2Oy0laKFaZOVq1toFr+7oJE5jy80FqcpbOI6i/5+9N+uS5DjuPc3cY4/cs7L2rburNxAUN4AQKEpDXR4daR7m6oVP82n0WTRfQPfOjI44OtQckRoQACkSO3qrvSozq3KPffFlHrwqu7qWRgFoCmggfg/dWbF6REaGuZub/c00tNSfZGnyTHwcQa22oBmGzHJ0rKy3pTducO/YoIZm6v64b9UWNZYKkUhthqQDpz6Tx0y3jYmXlEwvyYhVKedJJjknui05E5xZjptl0rZ4lCFPMypSUl7I/Z5m2pL5HGsy3oojlAiG06yWzZi5lpZkaZKzpFKdZdQ2NaM2Vx/sPxgfH2dZJiVomqZrOiAgMfRmU+QcRcaS1Kw1ku4+nMppF1b8m8PFr/KrqoZ5zZa82M2u2Zjn7Ht2yz9FSwq+PjzPiv/t/5rl7DMyzSSQ6izRZNQ+uFD8Q8WSIYCUEkEKQAQJqpwXUiqlQEJQghD8JDhZIlIqQSAQKQUiSFUlBUBFyknJJSDIC7HuCIgnQstqH0QihUBCpBQAEoiGCJKrEwlEKsWFkiSquYhScDg598liCagWEEKEKgqCqILykRAp5NPZdUqlEKrwFyISqkkhhDgfoY2ISLTTC5GACEIAoQASCZWCK7GdaaQ9opSSIJ7k1qsc+pM15KSOGSICISAEIFGNA0QpBVEnOg0pv/AeIEioFAIQQHJA8rTOCQIiUXmDgASkmMYwSilPEvjVnQepTisFx5OwwdNaZ1LCidNDzZ+fOk5O78MZ4QCJRCOEGFbVLhl+/zBnJ63VdV0JTSIgEISpch/i9BYVmWbfEFT2ahAEURQp/XBVa8u2bVUuZbpZFEVKJv3s7iqEtVQqXSpcmud5HMecc0KI67oXy5CcRSm0p2mqGqMkx0ulkjr42ZbkeR6GYRiGU8HzUqnkOM7ZzdSrNgxD3/eVjroqgm7b9lTe/PktSZLE8zz1stZ1vVwuX3UJUkrf90ejkZRSFVU7u41SRJ82GABM01QNfv4NKXjpQERKNULwOYrlRAoe9JmQmq49W2lbBVyfvL0vhK+f1qJGRAAptWfyrJACAMhpDPnZ3Cp69XALT9OUzlXsPiMs84ym8qXvfHUQDS7mO02f7efJjyhjT6cHR8Szf54/F9BLimcjANCTNPpnLufct3DZfbjyVj93yhgRpGrJ8+3gxTLhJ7vjSbagBKBPldaebfwZUYCrz4KIgJKHsRcQapjkZP9nakbgs804fU4IIYUVf+lR1UcODg5UIa+pjalUKktLS6rEp3qUOOdbW1u+71+04oZh3L9//5z+uTKE4/F4Z2dHlTz5zne+c2nJ8LON8X3/4OBgMBhEUSSl1DStXC4vLi4uLCyo4iKqdLeqPBYEgbLimqap+mMLCwvTOi55nh8eHh4dHXmepzYzTbPZbK6srFSr1efURJkWgjs4OFCF4FRLarXa8vJyq9U6p6WgjHS73d7Z2ZFSzs/Pz8zMnO1MJEnS6XS63W4QBJxzADAMQ91hVVnu831nBV9jsjwNw/gztdvkFSUqNU1zHEfTiuI3BV+IM/mEiOTZIIZLQCys+EuOGvg+fPiw3W6roqWqlFYcx57nqbLf8/PzyuCladrpdMIwFM9KQ6iKXhsbGxcPHobh3t7ewcEB59yyLNVFeE5jxuPxkydPjo6O8jxX78E4jn3fV7U+FxYWNE3L83xra2tvb08NkSmlqtRYEATj8VhKqew9Y2xvb29zczMMQzjt00ZRpEb59+7dq9VqVw2CVUs+/fTT4XCoWqJqqYVhGASBpmnTIq3Te9jpdPb394MgIISoUm9TGGPtdntzc1OtNQxDSul5nud5vu8DwMLCQjEc/2YgpQx8//i494W/T8MwyeycZX2Gr6ig4DNBFHAN2ZjCir/cCCGOj48PDw+zLKOUNhqNSqWiyof7vj8ej7e3t5XFUmZMyUaqsqFTM6bGuOeGtsqb3W63VdlsODP+uGrOWFXvVibcsixVBXw0Gqn+RKfTqdfrruuORqP9/f0oitTguFarMcYGg0EQBEEQbG9vV6vVarWqinaHYUgIqdfr5XI5yzJ18KOjo0ajUS6Xr/Jmx3G8ubnZ7/eFEKVSqdFoUEr7/X4QBJPJpNPpNBoNtaPy2B8fH+/t7SkvxcUBVpZlBwcHqks0NzfXarWEEO12ezgcjsfj/f39i4P7gpcXznl+Wsb76dMlz0wXw/llZyGEiKvE2goKPg/XfIoKK/5ywzk/Pj7O8xwAqtXqxsaGMop7e3uPHj1ijPX7/SiKVD3NMAyVN7hUKt24ceMkbkLpBmjauQKaUsrRaLSzsxNF0XVaonzpx8fHqj+xsrKyvr6OiEdHR5ubm+qAakr+6OhIjcIrlcrt27dVg23b3traStN0Mpl4nlepVJSznVLquu7Gxka1Ws3zXJnwLMtGo5Fae7ElUsrBYKA6H7Ztr62tLSwsqEl95TBXBdcppVmW9Xq9TqejJiMuvS7VO5lMJqo++q1bt+r1uvp1eZ6XZdl4PFbTDcXY65sI2o6NUiZJLOTJW5VQShHzK/xSl6mEEUQUgn9xy34yBXvl/i+oaAoSShCAX0M3FAlKIVWXRS2RF2awP/fpUUnLSS64kp9DBM45ktPQs9P7gIQQRCmEuOyqn3O3zq2aitk/t1WEEHIi8nrdCyFXKepfinKgXmd7RDy5BiEkIkH8zFn9gq87iFgulxcWFoQQrVar0Wgof2+9Xtd1XQih4sjU8zH1pZdKpcXFRfVymXLWIqpQr8ePHytPOFyjV6jmoZX327bt5eVlVaV7fn5e0zRCiG3brusq7/3CwkKe561Wq9lsGoYhhGg0GoeHh2maCiGUQ7tcLm9sbERRNB3WG4bhOI5q7XPaI4To9/vqqkul0sLCguM4ALCwsKA8ENOgvyiKdnZ2hsMhY8x1XRX995xrVNXH1Y0yDOOad6bgJYVQrb5w4/XvbqRZenyw2R96g5EPhM6urM+55MHjbc65EKCiwYW4YprcMOuNpkaJP+yGCRNyaurw1PBJFc8MeKKablhlYEHGQEqhgpm5Zs9XjMFwcoXRgsZMfTgYn8Zsk7ORzMqzr3bTDUenLIqzyw6CILWF1cUkCP3xOMtP+ihSSoJEglTxodQw0jhGQmdbtX5/bJlmlqVZllNN0yw7C3wAOBMrDoAguURKTqPPnmc3DbeyMFNLMx5HXppjtVZCxMjzNdvmaeQHkVOd09PROE7LjVbZRM7EUfdISAAEKSUhKCUAoOk2TPD8MJcAQkhEREAhBQBxXCfLUs64lKDpJgHOWM65vGr6GRGdSqNZL6VxNBoO05zh6V0F1R+QSAjK08siSHTLooiC52mSCikJPl17KRKgtbiaeb2RH4EQSjtecImEqAQHBBCnHlBq2KZGnEp1fLTHiek6ljQqhRV/uaGUrq6uzs/Pq5GiYRiqdzz16anAMQAQQigrrp4GZboopaVSyXXdc5HhWZbt7u72+33le0+SRA33n4MQwvM8VUVA2dper6fG5dVq1XEcFdoGACsrK7Ozs5zzcw2eVohSjalWq+VyWTnzKaWMMc/zxuOx+vOq6LZpWLu6UtM01ehfXaxqydlwvyzLELFery8uLl41IlcB/+PxOM/z4XCoadr0Ygkh5XJZuToKvmEgIev3v//du42P93o/uf3zcDT6+IP392L7jTdfb+qZ7tRcW3+0dXhrZe5gf2f3oMsv5HABErdUrVZc3wuB0kqzQQTnHCyDEl2Lc05YLgToBhWCx6nUIANC63M3Mdo9Houya4ZxQAybWI35qhiOvEs026UkiM25meHQL1XKlu2EoW/qhDGJmqETJATCKCFC6JZhlBeadvTg8f6lRVOQa3NzlS0vLrllP8waDSvOqA5ZTjRLpwCEZXml1TzY3uJAF5ZmB6PQLbuU2SWJug6lmYXO9qZpWKYuolRzbIzjVKJmUMpFgrqDIieIeZpOPP+y242GW224VpdltZkFjWIch4zz5sKy6egy9OK4t3zjNjv42EvyWmveSDrO4noYxoZlZBwMJFnuc3RsDYm74HBmlZ0syzWq5Ynn59pMyUwT5riWn4hqSc+yDHXLoRB4IVIIQi9JLnnFIYJTbdaqJLV0ajtxEKY5cwyaxpFmlwhIKWSaxE65kox9t1kXgrv1Zh4GkT8w7TKlIBgjmhGHXhInl3bBKLVaC4tY1fzH+7bj6MByaeqaZDmnugk8YGDrVOaM6ZaNkmoyX1i/ZUI0SknVtURlubDiLzdqZKlGvXDqWEuSZDAYKLursqEQMcuyaXbsYDBQRggRXdedn59fWlqybZucygh0Op12u63G99VqdX9//zpWPI5jdXzO+aNHjyaTCWOMEKKG/ouLi6ZpIqJlWZZlTRsMAFmWDQaDNE3hNJcMThJ+qLLxk8nk8PBwMBhMJhNKaavVmpubu8qJrRzvav4+DMOHDx+qligrrqLK1fSBpmn1el1FpNu2PZlMLh5NdQXW1tYYY77vP3r06Pj4WAgxGAyEEPV6fX19vXCnfzMRYni4dbzk1CpVu1TTqfmzvzS28uVGNb2xvFxprZYrpfm591Zajf83GO23jzm/kDhOqG6YmT/u98dmeXapYXkRrzXnID6G2rJ5tKeZsxaVQ39YWriZHnqE+KijZpa4z1c27ts0j3OeJ5NehJp2dUIjAqWEUFqp1mpzK35vx602kyioNBrdrR23tVROgyyMSo3qJDJ0LbmqfBYCUkoFY83WjFXVG06uV+cyv5+ZFRqNMlrB8IhrhhAAFCklhJBS2bXMkpZleeqhYdfr85WqU3L1cSA0CKyU1pv1xAvNCglSjQVj29C84eByKy4BEOLQG4zihbWbjTJ+dLCTZqzUWNLAt+rVemYjzwihhBBCNUI01EhtrmXpum6XWJRqWqUfagt1N4itucbGoD9OOMUssZrzNb0phvuWXWs0bTYkawuifRyXXDvx/PrsHPA4S6MELn/FEUIpQZZmtdlFNt5s3bwZ9jqubVQXlo83t0vzt0w5NtxqbE9mbi49/vhTqpuai1KDlbm54dg3dJIy6B0mSZJe7IQhksrMfB6MmgvLzWFo2bY/8VYX59vtdmNusVJ2ZTaKsCrCcSqwXLLiWBg8MExTt5xapTbrkh43Civ+0nP2ty2ESNP04OCg0+kIISzLWllZ0XVdTe5ObZv6oIa/cRzHccwYu3HjhmVZUsrJZLK/v58kiWVZa2tr0+H781GDYPXZ933P81SXgnMex3GSJIi4tLQ0dURP98qyrNvtdrtdxpimaYuLi2cT3tRBfN/vdrtqhG2aZq1WOzeLf/aAnPPpDJbv+yrhTXVukiSJ45hSOjc3Ryl1HOfGjRuGYRiGkef5VZepwuvUVL3v+3EcA0Ce5yqcsFqtfubNKXgpQUjjYH977/b3v59E4+HRZOnm7e+Z8M6D/ZX5xTxJjv1JGIZRqVSplPCSSWEppeA8R8swLUvXdUIkFxIJiZNIZiwLPDBqhoGCC0QUXFiuBcDiKJJ5Zmgk8r1UGroQgnPGrihTepKjjIZhO5aRcqEhl5qt6wnPc8YyKYEKqduWaRhxP8z0/KopIAkySxKeZwmDmWa5t7+1WJ3xvAmt2XkUpqZTAh7GqZQCJEiJmqYTQmSWCaLrGsRRQgmyPB5NUi7tLAlBq+g6GUaTHA2OThwGUtTKrnXFDLqUQgChhqHzJPSRaLoBSEUeh3HEHKPVdDrtbk1yIQRneZommGSEyjTNdFsEwcQ0qOOWAUAKDkRDkBqlTHAJmm4aYZ4TQyoHXhb7cSJKrpGmKUpG7Yp5dTY8Z3kS571eb6bcCCdBU6MsZ9SkhmlwxgAJAknDIIyTpuS+7+vlyNI0SYgmpT/2LEujVtXStcnlJUxJqWSmSTIYRdWymzHJOeg6ybNcILA8Cb2Y6WgaDk0CADBME6MgzzLGuDSAIHKWF1b8m4MyVIeHh1tbW1EUKVu1tLSkQieSJBFCEEIopcomqTHuaDQKgmB3d1fNqas4836/TwhZXl6em5vr9XrXb4D6kGWZ67qtVgsARqORCljb29urVCrNZvPs9iojXGWxE0Kazebq6urFeG81/a/ruud5eZ73er1SqWRZ1lX6LfJUaEnFqNfrdQBQMerD4XBvb69er1uWZRiG8vOrllx1XepGqRh10zTL5bIK5WOMDYfDWq02nSwv+IahGTrPkq1P3w+ixLZLdWmOP/6P3a0RBJ7g0qJ8tzNkcdIfDi83sUJEgafRimVZaTgYGzXB8l57n6Uh5IcsTvThoGzUdd3y27t+mIPuSJ4Gadem1tHerqmJMEoty7RR9ofx1dYX/Elo6CSOIp4f8yirlNI8DI+OB4amJZOjJEysUkmOR2kUeholiJfOrwNh/Z6HBLzxUMN8OJnw/QMWhTLrQhpyXTIecwoaQcbZYOAZOg28IANKiY55nJM+5FmSIoDMMg9ESDSW5wlPoyD0pRayJBacMpLgJSItAAB5FAS6rRGY9DsjoIaha5o5Om4DSBwnrq15kwhoLqX0hz1diPS4GycxchHEKeRpEnKdIUcRxxB5gWaVLYtohjHoDZNB6hItCSftdpgkpJOGUYR9mXAmiGSS+2lyRayihNgfHQWx5wfkqJsja+8fWgC+51XSXDetYHQwTGLTsqLAP9jdy7MsnIyYriextx2yJAqzFIwMkiSdxj2cBRHjySAKI9nzmhWac6IB7x6PDcMIxoNU07LQR1tyLcvTUHCWc5RpkHTbnItw1Gv7JORmYcW/ISgplb29ve3tbWXCW63W+vq6CuxSfuylpaVKpWKaphrvqmH3Bx98oDKw+/1+rVZrt9vKlz47O7u6uno2eHI6fH++bpoSYrt58+by8rKUst/vf/DBB1mWKVs+TfFSHYt2u/348eMoihBxZmZmY2NDRcCdPaCy7iqDrtPpbG9vD4dDACiXy89JGVc4jnPr1i3Vn6hUKg8fPozjuN/v+76v3Puf6WaQUgZBoPoZlNKbN2/Ozs4KIfb39w8ODsbj8dbWVq1WK5fLz9cJKXjpEJx3dp4MDyiA5BIac0uWY3307nvH4+jwySNVFpIxsf0EOMuviOuWWRIP0kRKQIA4iU7inKQELwaQmBxpJPWCIMsykBBHI0CQEnwQAB4ASIDQP9FvvSKOEoWA9v6BlOBPABA13dStgTcchFGKUiIhUkrPP/GNdUMpzkvGAqguOGHt/Y6UkpAoCiZCiH7nUEqBGAACyCAAAPClFBJgf2dfSvAJSqVHiwDSPwnMfvqjirzxUEiBQAA9KWUgA3KFCQeALPQOwslJpB1AqMRUTzT00BuBkHIopQSY9LpSSkImJzppE19FAuJTX70k1HNLFZGEQZIC+qE8FbOTGKOQEuLwVAFVAl4xyyCljP1hDBKQTHpHIIH1ur4UUnKjfTga9PnJ61ECQLATCCEm/SNElCD9sS+EQIIwmoAUl55B8nw0UNVm426sVHQl+J6S0QUlrOuHAAAoAQCVGt3YkyAAIACUsohR/0YwlW9TiWGaprVaLZUTpcaIUkrXddfX11VOlBo7qqDTRqOhPNWe56Vpuru7q6a3EbHb7RJC1KSyOsvBwcFkMpmdnb1oa89GuVuWNY0M1zTtyZMnWZalaRrHscpWV4Hoh4eHm5ubURQRQhqNhjK3Z8VYpq8tdSghhGEYvV5vMBiMx+N+v3/Rm62aMW2Jcgmo3Vut1sHBgUqa931/Zmbmmvd2OBxOJhMpZaPRWFlZUep1Kp/N9/0gCAaDgeu6hRX/ZqCkk9RnnmfRqY9meNx5+zc9zwukEJcEeQMSchKlDACnCUFnPEMASsHjGaFUlMPhkEshxcV3vDz736l6+OVSDWoKSf1ccpn0Oh3OuRRCRalcvMBLL3z6cxNCgDrgyfJLrL6Qzxz7mS0udDfkGe0SLp9zIeLC/uePJc8sPRdOKKU82xAhhD8ZSSnEJff2wqnDZsY+AAAgAElEQVQ/697iqXS5PLkU0m935CkXmnHmz9OzXzpiOLO7fPpFcf7M3/LsN3jJd1FY8ZeeqV96c3MzjmNd1xcXF9fX1+v1+lm7wjlnjE1DweH0baU0yeE0YNv3fbXB8fFxr9dDRCEEY0xNe29vb6twuYs+ZJVCpvr7mqZNk9FVhti0DeqpVSZ8a2srCAJK6fz8/M2bN+v1+lTKVG2TZVme54ZhqE6D0k1zXVdFlgVqbHCBaQkBAKCUqtAz1SrVkrNT+J95b9WsvPJAlEolXdfVXbVt2zTNIAhU8H+Rb/aNwTTNcrlyMTUIEYWEUqkCV40lAQDA0A3DNKmmXzfcEZFKfKE1ohEACKVFtxIQUeKf6jacdtP+NEf/HBRW/OVGniqsqVG4ruvz8/Orq6ulUmnq/VZh3r1er9vtZllm2/bt27dd11WBYCr4CwBM01QS0Ocs3PRPlQM2nYpWJhlOewMqaU2dK01TleetmqemnKcpZJzzXq+3vb2tzPDs7Oz6+nqlUpmeSzm6j46OlMBLtVq9ffu2itHL81wJzQKAMtXqKlQLVQa8ugrVEhWZrybapy1RvYHr3+RpH3raC1Gdm7PpfF/0Cyz4eoGIjuMSzSBf9DslhOi68fkeiRf9/ExHfy/2sC8lX+4mfPbOX4ObXFjxlxspped5m5ubaryo67pt21EUJUmiNlDzzZqmJUlydHSUpqlpmq7rLi0tAcBoNBoOh1JKFYZtmuaNGzfO6Ud6ntfpdJQauZpZdxxH+ZOVPEupVKpWq4SQarVqWVYQBCpEzjAMSulwOFRJ2IZhqMF6GIbb29tKDU3VGUuS5Pj4GE7NYbVaLZVKYRiq84ZhWK1WG42Gyvz2PA8ANE2bGv7RaKSy1MrlcqVSUeF7h4eHat9Op6M6GYPBQInSGIahktk+E9WfUN5yFUYQBIHqE0wmE5W5pzYoDPk3BkKppsnLYs6vC2MMrufsKfiac3Z65WvD+SJvhRV/ucnzfH9/XwmAI2Kapnt7e2eDtgghP/jBDxqNRr1edxxHZVttbW2pTLDRaKSmpev1+szMjGVZ6+vr55zDSqBUJVYtLy8ruRUhxPb29ng8JoSoob8qSjYzM6MKkqpiJ5qmKbEUNfNdrVallIeHh8PhUPntOednG6x+M3fu3CmXy41Gw7IsZYkfPXpUq9WklEpJBhGbzWaz2UTEJEl2dnZGoxEArK2tqSizVqtVr9d7vZ5aq/z2qriZWlupVK5pd1XLS6WSknl//PixipVrt9txHCsT3mg0vn4/9YIvDmdPkxULvs1QSl94iYSrw/subnmJSKWmUUq16durqEz60pMkyXA4nHYYVV742Q2UxUXESqWysrKiQsyiKNrf31fbK0/4+vq6GnFetEa6rtNTdF1XzzTnXLnNlZ6M6kNYlrW8vBxF0Wg0yvO83W6rUyiBs9XVVdd1GWPdbledVx3/bIPVPLqSo6nVamtra9vb23Ecj8dj1e3gnKtSp2tra9Np+CzL1LyAqkAKp6HpSu4tiqKDgwPlA1fCL6urqxd1WqbzAudugpoOX19f39nZUXVTlH6c6ky4rnvjxg01lfDCvtSCr5TTiCVBdVOjGkguAEAKKSXn4kTQ+2nd6K9+WrTgT8fF7xcBkFBd1xnLz3b1ToLdr+D0bYOGYVACSZoJIREvf34Q0TQNwzADPziXnYaIjuNUq5Wc5QgopazVaoUVf7lhjClJ0aveJoQQlRKt6/ry8rKmaZ1Ox/d9JXIyreo9Nzd3VZfTMAw1jj8bNUYIqVQqynxODZhKCbt79+7BwcFoNFL+dl3XK5XKwsKCElRXYjKNRuPScylTqpTdDMNYXV01DKPb7SqlOXU0pZbabDbVDD2ltFKphGF4tiUqVx4A2u22qpsy3XdpaenSobPSmGs2m+rD2VW6rivxnG63q9LEVcy/0qSbn58vTPg3ECnKs3Mlw2TRONVsEzjVzSQYTyYhQZASCEEpRJazq6TQCr6JoGGZhBoLi0ve6NjzPCAaJciFAM6ZBA1Fzi4pe6Pphq5pUsrWwlrF4ptbewIQQeZZxp/1+qg3dq1Wq1Yqu2maZdm55H7LMpUP0jKtJEkd2y6s+MuN67p37tx5TiVEZZNUT1Bliiubp+K8VMi367pTkfOLlMvl27dvK8UYZV+VA3x1dZVSur+/f1aOTdO0ZrNpWVYYhmpu/uwpAEDXddXgS8+ljjzNcVcNrlarqsGIqCTNz2qhG4axvLysotim8fbKuquMuEAl4wKYpjnd9+J5lWycSmdXqeRn11qWdbYl6kKUIX/OrSt4iZHSdEsaIou525ozg4nbbDGHglOfcc0k4brOvfGw1xsXo/FvDxL1lZs3x71hs7XQaNbH7V1ZnbMgT5ggLBqmmhUfHfb9p/GFqpwdkKX1mzrw8eCIg3RLJd20l27e1ni8u/XEC+KzpzBNY2am1WjUSqVSHCdHx8fK2XlmE8zz3DKspcXF7Z3dnLHCir/cnNUk/0yUFazX67VaTdnRaVmz5+xlmuZFuVO1S5qmlmWd9Scrc1ipVJTAGZwOr6en0HX9rHzb8yGEqIopakJdNfXcwFc51dM0VR3Y6YmU+6FarSqVus+8WOX2vyrqTZn2aUsuXlfBNxBEKaQUzCzXiO8JAXmW1Fa+U4qOgdKamwz67PpznAUvPwhIGzOtaOQhCq5ZS/MtObvGxj2LcctqNoi99Yf2tIIcImq6ValVPT9cXF6eHB1QohGkplNySu7swqIlon5n75wVV6ZfzeshueR9dTJ9aZvlcknXdQQsrPi3jktt4edlqgAzPz9fq9UuWtYXGNuJz1ZNPUeapkr1fWVlpVqtXpzt/i9rScE3jCyO/P4oy3w9DEmScN+jRA+PuwZEXpQRxrP0MvWXgm8sEkCM+4M4CrsH+5mUVS3JI2JDPh71NadWdejIj8526xCIaZrUG7cP2xYCEo1n3PciEPnx4Z6JPM3yc2VLkyQ5ODiM47harR4ettVM4lkNTUSUEnr9Qc6YikwqrHjBF6RUKtm2PTc3Z1nWVzgkVdF55XJ5fn7+Uln1goIvAtKg3xNZLgUOth6RLAZvYhha6HdZtZRlWehlacaK6LZvFSiy7SePpBBBFALIIYKQA0qAM4Z00EFgZ+TkJECex0ftA8n5wdZjSogQAmEy6iGXfDQcA0iWs3NvLKUW53leEqfKhJuG0ZptHR62TxXreKnkSikYY45jE1rEqBd8ISilKysreCrk8hW2xDTNlZUVQshX3pKCbxQE8yhUo6R4PFDLAikRsXccwWn8BcCXSSwv+FqDlwg6yTw754BBpjzoF4X05UlaAwCIPGNw4mtHdkn+2Ln9kiRNk0yC1HV9dXV1dq7VbnfUqjAMz8TOy3a7U1jxgi+CmmL/qlsBcNqSwn4XvCjUFAwBcl6W69ybt3jkvgVcQ8Lv+s6YU8N7Pf+NyjGjlDLOjo6OpnspXeqzWxZWvOClpzDhBS8QgqToFxac8FU/B5zzTqerItquCsoprHhBQUHBU4QQnPNCA6Dg64CqYvX8AXxhxQteGBKuoz4tr1NioKDgq4IxlsQpEgQABCC6TgDyLAc8PzA7WwtHAiBIxKexxADqAGobJRVz+jJG1ChFkIyLadnS6THdcs0kfDQJih9KwXUo+psFLwYpRZZnz5/yYSzjgn9pravzBX0LCl4wCIRS3dCRoO2UZxfmQUhKNV3XEYhuGIZhUKIEiTVEouuGrmlUM2daM7qmTY0vEqIEjO1SuVJ2NI1STSOEEEJtp7YwVwZCqKbp+mlgpgTO5Pd++OOaZRWd3YJrUozFC74M03GHZDwf+oOZ6ixBwGlk0KnktIr2PB7tWFal7DQo0eA0TRKRqPSKp/LU6hM8XSukgBO5A5JmYcYz16zgCQRADZOKt17Bi4FQWq3PlFzLG/XTNLAqS5R06s0Zt+SOu8PWcgsRJqNIzZ5PRkFlpiqyJMxgZW2ZZflkPOISENG0azMNy5t4pcZsSct7gxFSEwRL4iScZOurbnfEqtW6pctet5vmXEowjPr64swH7wSEoCh6qwXXoLDiBV8CKYN4hMTQZDRIZBRPLJ2GqQ9g1V03YhkRiSQli7AMKw3HOh5tAbWr7ky9ssRZ4lpVLxrPVOdBijAeePFEEmemVBl6RwK1itOIol6rvprEIz+LhOBMMMOoJeHBMAln3BmClFLiuEvIQ6q5jukUZrzghUCIVqk2LANYbKVpSqhm2qVKuWLYVmbnrWadEY1gokEUCygl0rBtaptRd0B1nWW5RGKZRpbnum5alpUliRBCSsaYdF236tCDwy5nQqOa4zqVapUiMzSa5hwATausiSzOOeKXdloVfDsorHjBl0H2R7uSuiJ8MiDr6WQrjI/9NJYsrdVuRNEBlWFMl5sw1Jtv1m0zZ3EQx3k2OBwPSxqvV5cPh0eN8ixnwf7xhxGjEm0R5Qd+YpLccxcP2m//1ff/98Hw4ZPhASFu1Sm3/c21EvXSsD/4tF65adJQhqkmxrXqDcd0vuq7UfANQQgexyEKEsWpU6ohZ4ZJsjwTMvPjaDIe50SPvMS2ZJIkURwxT2qUpHE0GoeGaZAsq9Uq/cGIsyTPDUox9Cd2zUWUWZai6wohqjPVjOsUkjRJII/SXNUjF+NRF0oVIoQsZjsLrkdhxQu+BEgcwzwYd/rjwe31Vx8fjTOIJVg6Hw2iBT3upVpl7B8kRP5oxZIgAbBemZ918J2tJ9XZxf3ux055Q4LMWRCm43rjNZmNjgefOs03qqLTi8dhPIrzMEonceZVKkvLs/c+bP/yTvNuCcQokvMztwwZfXrwiWk1Ws3riskXFHwmQrDxoJdYRpZmGmrHhwdJGqeD1DSMLIv292OBlKW5YeqIkKRxNIgJAsvzw71dIrng3PN8IQRn6Wg4zNIk51IKxvNMM9hwOMrznGrR4WGcJkkcJRoFxoWanKI0e7x5sD7ffNzpFXNEBdehsOIFXxwpwbYqSfQ7tJYtCoQapqYHaQxS1Cwjz2iOuo1H0rqrIcuYFMCDqCcy3qguVizzcOTPzjo5S7iQBPXhZDfNvKpVn/htjhHRG65p7fU2g2hMkOiagYQYmiUkz1lKqW1Q6uqzBn6USLB0s3jjFbwwhEyTKE0iRIQsg9PMijgMASALUrVVmsUqwhxVURRE5k/gRGCLIWLCwzQ5OaQ/GQMAE55gOePc9yanRjqB0xMgAtXwwz/8p0Pywp9ecE0KK17wxRGSZ0I4dsM160nm1ast09B0LZJQLhmQlRZMoGguSaPshUeUoGVWZJ6kgi7WW8hH5dKslPEw6EqRW2Y1SAPdsGy7FAcjRoySoc/N3IlTTzebTUuaGgbRYKnekIi65mglk/FUELTspq5VQObXy3MrKPhskFDbcRF4miRcSLg6XhzxdOWzpWxPPlzYPktjAHx282c2RcTIH4Ugi4F4wTX5DEHXgoKrkVzwIB5GqY9IAFBKAQhSCIlIkZw+WlJV2QUAIbiUUiIaRPP9jjTqruWgFCpGnQuBiARRSCElEEIRpFoIKuMWUQiBCFJKBDR1E3K/HUSN6mLNLtmGW1jxgmsipWSMJUly9gWoRKp//vO/SXO+sHKzWSZbm9tRkhcvyYKvM8VYvOALg5RoFWem7Kh64acxtZfLuqhF8kQdQ8qK0yJUp4SeLD/9Z7rh0w/ThXA+bFfwplNGneoEsTDhBS8KKUWSZbOzS4PeUZJ5nBdWvODrS2HFC74UqDSunln0/B1O/qUGPb8pXvb5uUcjGtEK413wJyCOI0Cj4rjH6H/VbSkoeB5FNkPBV8ULsb6FCS/4EyCBEAqC5zkrgswKvuYUVrygoKDgGZBguVTKsngcBEo3sKDga0thxQsKCgqeAQGB5/sHnSBMisi2gq85xbx4QUFBwVNU8nevcyBBEsSiRGnB15zCihcUFBQ8hVCq6UBOkh6KwIuCrzuFFS8oKCh4ihSCcyYQpZRfz0J5VzVMLaSUcH5SA/C/umUFL4izpes/k8KKFxQUFDxFCCEEt23HcZw4jpMkEeJpgBsimoZhWlYQBJzz6fLTQruXQykFgLPbn9nxqa29zlubUlqv1UbjMQDYtm2a5mg0klLJKWGlUmm1ZnZ2djnnhRX/2oKI5+w0IhqG4ThOFEUIUK5UojAMw1Cerr14kOkjV1jxgoKCgmfQNO3O3Tv3793/5JNPjo97XPA0TQmiYRjD4WhldbVarTx69FjXdQDwPM9xHEJoFIWVSiXPc8YY59w0TSmlpul5ns/MNCklx8c9xpjjOEEQmKapaVoQBHEcE0Isy2KMEUIdx1Yz8Z7nlctlxhghRNNomuWB70spNU37bz//+f/31lthEKyurq7fWP8f//Q/CUEAkFLevn27Xq/t7e0zxr7im1jwXCqVSpIkynITQhDBNK179+699/7783OzMzMzTx4/CaMIpCSEmKbpum4cx7quU0o9zyuVyyCl53mlUqmw4gUFBQVPkSANw7x/7/5rr7+uadS2HUTc2d3N0mRpafk3v/mPRqNRrVZvbcjFxUVK6MOHDxYWFo6PjyzLrlaruq4LIdrt9sbt21maIkIYRq1WS9e1//zPPywtLc7NzT958uTOnTvtTqd3fLy5+UTXjdXVVcPQDcNcWV1N0xQB3v/g/fv37zPGqtVa7/jIspxf//rf0zTVNP2V73wnCMPxaJRl2fLKCp6O1UzTuHP3zu9/9/s8z7/qu1hwJYiIiK+99tpwOGg0mjdv3dR1I46i999/r95oVMqVn/31f3vy+HG9Ue90u+qr/OEPfxjH0Xg82djYiKLwo48+fvPP//zo6Ojjjz++detWYcULCgoKnjKV8k2SJGfs5uKiZVo5Y1mWrq2uPXnyJMuyaq0mpTQMwzSM5eWlarX66NGDN998pdNut1ot13U5Fzdv3vQmk3b7sFwue97EMIw4jm7cuGmaZrVavXHjxu9+9zspZa1Wt22bEPzxG38uOC+VSptbW0fdbqNeX1tdkyDn5+f/n4P9mzc3NE1L01SCTNM0SZKZ1syTx08EF6Zl5nkupUQkGtWEEFOHbcHXE0Ss1mr37t3TdX1ufl7X9dFw+NFHHwrOXcehiHme3drYaLfbANjv9+6/cv+3b70FAK7rzs62dnZ2KpUyErK5uSmlLKx4QUFBwTPkef748aMoinZ2dpIktUyz3++bpglCehOvXC6FQeB5XrfbNU0zjqIszUql8ubmpmWZh+1DwYVpmttbW+PJuNPu2LYVRtHS4qKuG48fPy6XS51O57333tva2kJEy7KTJA3DcDIeB37AONve3t7d3V1eXhoM+nGSNBoN23YePXqohmWcsY8+/HB/b6/ZbBqGcXx8VK/Xjo6OpZRxHB/3jhuN+vb21zEor0ChIhjah4eLCwthGO7v7em6HoZBo9GwLLNWr+7sbBNCRqPx3PxCs1H/+GN51O0uLS4NRsMoihqNRrVaSdPUNPRyuVytVoouW0FBwbeO59c0S9LMsm1d0xjLDcNERM45IYQSEkWxrmuUUjX5jYQIzpUXnXFumoYQUgihaxoAMM4ZZwSJEMI0jSzLCSG6pmV5TikNggCeBpbTUqkkhACQaZrlea7rum1ZOWM//elPP/zwo8lkFMeJEIIQ4jpOzhghBAF0XY+TOE0zdQlra+srK8vvvvtulmVfxX0tuBaEkMWFhUajoeopI0EhRJ4zTaN5zgAkpVR9p7quh2Fomqau64zlhBBN0+I4tiyLcxFFkeu6hRUvKCj41vF8Kx7FyZXh4k+Xy/MS64hw7nWK+LQM39lVeCYV/XSvaUump1aR547jMsYYy6dr5RXbA4CmaYZhJkl8Nq7+KtSO1zQBiKhOe52Nr3nAc0u+PcbotNoyfh5BgnPFIp/+WXjUCwoKCp4Bn5P0hYiuDXkuM/aMSVMqMfLZZaYJlECSgHj2DaxpaBoyitA0gRCZpCDExTOqMKg0Tc4uNAxD17UgCM8mKRFChBBSSs55HEeXmsOLk+WlUilNkuyzQuHU8S3LjqLLj3xNzqVXGYZBKU3ThBBqWVaapmp2/wsf/yXizGV+ruuVl/5ZWPGCgoKC60EIVkvGK3fzTx+jJUDTZBSjY0suAIS2tsS292WUAGMAgLqmf/8V0R/ybg90A6UA0wAAyHJwLLq6lL/zR1KvklKZdbqACDlDShwknPOpk4BSWq83NI2maUoIQcRms7myuvLeH//IGNc0qnKGb926tb29nWUZpZSxfDLxVHvL5bJhGGmaaho1TTOKYtctcc7SNNU07Y0/f+Phg4d+EAjOVbAe5zyKY+X8Bylt287znFDSbDTn5ud/+9ZvOReU0mq1KoVIs0zTNMsykyRzS26eZWmamobBhZhMJsoZUCqVbNtWl1MqlaIoMgyTUsIYazTq5XL5k08+XVlZnl9Y+OD9D0zTklIGwbelFOyL6rIUVrygoKDgWqCmaRs36J1bvNvDcomUXTEY09VFMfZkHBlv/FBEsej0gFPgEhtV/fXvZ797jzBOV5eAUlqrSAliMJRZrt26kb/9RyQaqVaIH9Cbq7xzrBFcIHqcJO3DQxUDZVnWX/3VX4ZhmKapYRiaphFKvvvd7yICJVoUR/V6o9vt/Ox/+ZmU0i2VwsCv1er/+q//qobmP/rRj8Iw8H2/2ZypVisTz7t581bvuJckiZTiRz/6keCiXq97nsc5t21bCLG/vz87N7u7u9tszrRaLW8yMQyjVHJL5cq777zLOTMM44033oiiaHd3t9WauXVrY2tr+979e91OZzweN5tNz/Peeecd1QNYW1u7devmzs6uYRgbGxs7OztLS0tRFPm+TyltNBvbO7s//OGPKpXKwwcParUGgHz06NtixV8UhdB/QUFBwbWQQsjRRI49mWaoa1JKOt9Cx4E8l34o/VCORoBAWjNYKUsvhCQVgxGp18h8S7+9Tufn0DZJtQw5Q8tE25KmAY4lOaf1Gl1ZkEmS5zk741immtZoNB8+fCgEr5TLlXLZsZ0kSU3TvHXrFgIuzC+Mh6M4jrM0XVpcDAL/xs2bSo5GSnnv3r3JZEIIrdWqlGpra+tzs7OM5Xfv3XVsizFWqVTW19ebMzPz8/NJkpZKpVqt2pqZmZ2dvXf37myrNTs7u7i4yDgTnJumsbS0ZJqWaZrLK8utVmtlZe3O3bvLy8uVchlAzs7OVqvVtfU1jWpLS0v1el3X9Uq1urKysrK6Mjs3W280lpdX2u1Ov9+P41jl4o8nk16/Px5PsiwlhHxLnOovEPoP//APX3UbCl4O1Kwb51ycYSr9+EIUp88G7AghpoqVX08564KXGiHERYGzPM//8R//D8bYFY+chJwDAt9vk2oZHZvvHgDjojeUQQhZBoYuJ4HwfBnFEKdYdsV+mzg2EpRhLMYTcdwXXoAEkBIxGqPrkIorJx4QQMviDzfnZmaEBM+bAAAiUkJs2/74o48D36/X62mW7R8c6Lo2Go673a6ma57vP3z4wHVLYRRmWW7bzmDQ39rcUpPQruvath1FESK4rrO1vZXn+e7ubpalQkqQ8PDhwyzP9vf2/CDodrpplo7GIykEz9lhu53n+d7ubpbnmq4fHx0lSfLaa68fHR1xnhmGEUWxrutZmrTbbc/z2u1OnudRFJmG+fjJ4+FwFEWxYRhSCkLo4cEh52xrcxMRP/zoo+Fw2Gg0bNvqdDpxFE887+Dg4Dvf+c6tjY0PP/zwRb1PviUUMeoF1yVJkk8++SQMw+kSQkipVGq1Wip19Uv+8FTYcJqmSpKw1+vt7OxsbGxUq9WiOmTBi+X5MepxnOBVjxwlSFDmHA0dKJVphlSTgoOUCBJMQ6Y5nMaHo6FLzhEJ6BqoAG8hAQA1AoiSMQBEjYJp0LUVvteWo7FG6bn+q67reZ4rnW0A4FyYlsFyxhizLDPLcs65YegqHU4Z1+nuhBDXdbIsRwRN05Ik1TRNrTUMXUrJGNd1DZFwzhjjaur9RF5GStu2GOMAQAgKIRYWFhcXF99//wMhGAImaWYYOiGY50ydXdM0TdMYY3EcqwZYpqkbRpIkAGBbVs5ykJhmKQCYpqlRmqSJCvwTQrz22mtCyHfeebv4vX8uinnxguuSZdmvfvWrKIrq9br6manheKVS+dGPfnT79m3btr+MIc+y7PHjx71e7yc/+Ylpmt1u95e//GWlUqlUKi/uIgoKvgTq6dY0BJSMQ84AQOa5Wi4JQpKe3VxmOQBIlKDMKkGkVDIucwkIgAQpEUmKEvhBW4zGICXL83PjKk3TTNNU0W2UUiFSEFIlrIfhSdB4kgjlycqy7Oy4TAjh+ydZ6Wmaqb6LWqU0ZPD0A5ypo6VMOAAEQXi2Jb1erz8YRFGonHCIGMcMzrjQLvo2kjRNs0xtoNZON1amfbqEELK5uen7fmHCPy+FFS+4Loyxbrdbr9d/8IMfWJYFAEmS7O/vf/LJJ8fHx7qu3717V9VuUlyaz3pu1dm1SZK89dZbjLHXX3/dMIwoio6OjlRFqekP+9yhnnOKgoI/AYiGob1ym7e7MPEBUKYp6joAgJSk1RC9ocwZSAEAYOiQ5UAIahpQIhlHXSPzLdHpSc7R0EHT6ExD9IciTgih6LqQJDqAOGNrKaXr62vLy8uffPLp4sKi7Vi7u3srKysszx88fBiGIWNM2VS1/VWu1at8rvLCPuecE2dXeZ539qd28ZiXnuVM2648EQAIIXq9XvFD/gIUVrzg81Gr1V555RXHcdTU9f3795eWlv7pn/7p3//939fW1hzHAQAhRJIkQRAIISzLKpVKmqZNJSbU5JnyuRmGUS6XKaVCiOFwqCQtB4PBNMhFCDHd2HEc13WV008IkWWZ7/uMMaV7ZZqm2itJkjAMbdt2Xbd4KRS8SCilayv6nQ3RG5KlBXQdMRjR+VkRRTKOzZ/8OP33t0RvKAUHidrtG+LwCMsuaTWBUhmEoj+gsy05GNOlFSw5SDFl6YEAACAASURBVAiZaYqxxw87xqv32O6B3D+cL1XTLD0+PlbPvwpEuXv3HgCurKyUXHd1dc0wDCklF3w4HHY63bOTXH9S/tS/puLX+sUorHjB54NSapqmZVnqJ2dZ1muvvfbb3/72wYMH/X5/aWkJAI6Ojh49etTpdDjn1Wp1Y2NjfX3dtm1lYp88ebK3tzeZTDjnruveunVrY2ODMfbBBx8Mh0PDMN5+++0f//jHKm5uMpn88Y9/bLfbjLG5ublXX311bm5O0zTP8x4+fLi7u6sycBYXF+/fv99oNKSUBwcHf/zjH//sz/7s7t27xXuh4AWChJBGFQydlFxScsDQ6UyTzM3wnX0hOBq6HI0Bkcw0IGXarXU5O4u2SRbnxMRDLrJ/O0LDQMfRX70n8ww8HymlzboMI5BSJgkyZhg6E0/LkKtxdpblrdnZZrOJhDSQaLrmeRPHceMoUv3jIrzp20xhxQu+FKr27cbGxv7+/uHhYavV6vV6//zP/zwejxcWFiile3t7n3zyyU9/+tM33niDMfbee+/96le/ajQa9XpdCPHkyZM//OEPv/jFL27evGlZFqVU0zTHcabvpt/97neO4ziO4/v+xx9/vLe394tf/KJSqbzzzjtvvfXWysqKbdu+7//bv/1bp9P5+7//e0JIHMe9Xi8Mw+LVVvBikXnOPnoAQvC9Nt5YQUTuD2Sa8W5P+gF7so2uI8MTpTbRPqILsyBB7B5IQD4cgWUBApYcNHQ0dX7UF0Ess1xOfJ4zoBpQLUmS7IxYm67rcRzt7e16vh/HEUE8PGzfvnP7YG//4GC/1Wqp57941L/NFFa84MuCiLVaTUrpeV4cx7///e93dnZ+/vOf37lzh1I6HA5/+ctf/uY3v7l7966u65ubm6VS6W/+5m/q9XqWZZubm//4j//4+PHjV1999Xvf+97vf/9727bffPPNarXabrfVSPov//Iv5+bmfN//1a9+9dFHH/3sZz9zHOfTTz/lnP/4xz+u1WpCiLffftvzPCklIWR1dfXv/u7varVaMRAveOHIJGUPN0UUsXYXbUsMR2g7MkmA8+y9j9EwZJrJMALEPM/ZQQcJiiQlhiGzTDLONndknovjPhAEJOzxYykk5JwLgdUS5FkUR3nOplZZCJGl2aeffNLr9+v1GiIZDodH3W6SpkkSv/rqd/f2DgoT/i2nsOIFL4DpnPdkMnn8+LFt22p6W+Wf1Ov1jz/+uN1ur6+vv/LKKwBQq9U45yrsVkqpAlONUyzL0nVd5Yx+//vfv3PnjmVZtVrt7t2777///mQyQUTXdff39x8+fLi8vDw7O/u9732PnlKv1+v1+ld9Swq+iUgps1zmHgCI/lDFacsgPoldj2KhfguIIKUce2J8ooQqEUEIiSjHE6Akf+9T0KiMYzGawLTGSBgi4iCICCEqnFPFf3S7XQmAiEEQgJSA6Ps+ALiu+/vf/77X6xVW/FtOYcULvixSyn6/r0bkWZaFYZgkybvvvqsssZQyiqJWq8U5p5TWarVHjx49ePAgSZIkSbIsm0rHXHrwZrOp4t4R0TRNAGCM6br+F3/xF5zzBw8efPDBB5ZlLSws3Lt3b2VlZRpGV1Dw4kFEXSNL83LsiYmPnAMSAHGSNlYuwXjyzMbyJKOMzDTEaIyMAwBI4IMBAkiVVj6tb4aIiKZh3Lx5s9vt1OsNw9AHg8FwOJrmf08rqiFAmqadTuc6tcsKvtkUVrzgc3PW6Aoh4jje3t42TXNxcTHLMkLI/Pz8m2++aZqmGkxEUQQAi4uLnuf9+te/fvz48dzcXKPRWFhYcF33ww8/vPQUAKAEKM5U8YPpSWdnZ//2b//2+Ph4b2/v8PDw008/ffjw4eLi4srKCqX0bOmkgoIXBiFktmm8+Xr2zn8SSpBSGSVYcmSeAxPGT17Pfv2WiFKQXOWkkVpZRrHMc/07d7Lf/hF0HUuOTHM0DdQon/imkLZleZ6njDGldG19/X/77//9//6//s+f/OQvhBDtdntz80mapGEUapquaVqv13Nsmwvh+35hwgugsOIFnxclLMU5VxY6DMMHDx50u927d++2Wq0gCBqNRhiG8/PzCwsLhJA0Td99991+v3///v2tra333nvvjTfe+Ou//utqtcoY29raOhdhqw7+nNG5Eth6++23bdt+/fXXX3311TAM/+M//uNf/uVfDg8PFxcXlbSFkpH6r7orBd8OCCGzMwiAjNPVZbRtyZi2PM8Pu8Lz6PICll0UgBVXphmapvHmD9nmLnu0RRwHNQ0dU7u/wY8G2p2boFPc2rP3Oo1aNQxDZY9d9/9n772/60que89dVSfenC8ySAAEGMAEkt2tZge1pLb6qSVZz2OP7OVl+Zf5df6W9zeMZ9njWcse60myXyuzg5qxmUmAIHK8uDmeXFXzQwG3QZBNsXNAfVavXpcn1KlzcO/51t61a+/w4YkJTVX7+wd6e3sLhcL4xPjwgeGVlWWMsKqqZij8m1//Oh6LBZS2223pS5eAVHHJxwIhVK/Xp6enhZ3tum6xWHzw4EE+n3/llVfExhMnTvz+97+/ePHisWPHVFWtVCqXL18WdRFUVRVZqMrlcqfTaTQa9+7dE6MBzjkhRNO0arX68OHDgwcPPv6G6hrlhJBisVgoFAzDSCaTlNJOpxONRtPpNAAUCoWFhYWhoaGhoSGZB0ryWcIo2yzSVIpbNsSj3HZA01jbYvUmbzbZ6jqvN4AhUZ+cuy6r1ZGhA2Xc91FI54xxz+fNJgCwWp07DqNBEHxYpxwhVKvVSqUS56xQ2Go2G612KxQKd9qdeDzBOeeMcc5VTTUV80t9EJKvEFLFJc8KxjiRSDSbzbfffluoo5iui8fj3/rWt0ZHR8Wqs1OnTjWbzbm5OZGJKQiCZDL50ksvRaPR4eHhqampxcXFCxcuGIaBMY7H4/39/SIITlXV0dHRUqn0/vvvizi1eDwuqjMJNE2Lx+OappmmeebMmXfffffy5cvC5R4Ewfnz5wcGBgBga2vr2rVrmqYNDAxIFZd8ljDOag3/zjSrNwAjpGusbSFd4x2b+z6/fhsZBm9abKsMAEghdG6JMw4KCeYXOWcQ+GyzwFtt/8YdhIBW6j6AbdvdAWu73b558+bm5ma73Z6fX1AUomna+PhEsVhcXFpSCCGEMEb7+vo4B4DpL/NRSL4yyHQBkmfFdd3bt2/btt21iYUMZzKZRCKhqqoIOBce73K5XCwWgyCIRCI9PT2JRELTNEppq9VaX19vNBqqqqbT6VQqtbS0hBA6evQoIUTIP6V0YGBAUZSlpaXx8fFEIoExZoyVy+X5+fnR0dFcLue6bq1W29zctCxLUZRMJpPNZiORCOe8VCqtrq729fUJl/6X/dgkX0U+eTUUsZ1zwHh7MujDFjggBGxnC0JIhGhwhjAGQAAcIYw4B4wAEA0CvB0DxxljwLm4KMYYI8QBMEK6YeTzubW1tYAyBFyUOD98+PDKykqtVmVMvr0lUsUlz4yoTLonBbrQ8sfTm2+/mAAAgBDSPUBs79Y/EO707mdxCfHP3cd02xRre4Q2d5sS3njRme5hu8+VSPbwyVUcIUA7LnCEgAOKRYFR3ukA33WMiK/caRZ2fizpdEp8JTnjrXYHYxyLxSzLMgwDIXBdjxBCCK7XG6lUilFabzREQbPur0k4ruTwVNJFetQlz4qYkH584xOP3F0hePcxopHdMeS7tbZ7icebfbzkcFfOdx8vKxNLPleQriFN5a6HVAUUwtsW6cshXQ3uzSJDBwTc8VHI4JSythWNRh3b7hYNI0QZHh7cLhBA2cbmVjabfe6552Zmpvv6+jc3N6q1Wn//gG21b9y4+cqrr6wsL9+/PyMmlbrJ0kVqoy/r9iVfQaSKSz4GH0sgn3LwHl3/PC4hkXzGcADG1ONHWLnMbRcn4sjU6UYRmm18sB9n0zidRLrOW22cTrFWy7k9MzQ0uLa6Vq/XxdgSISAYU8ZgO/+BdvDgwZOnTtXrdUqppmrxWNz33HA4Yui653mqpsXjcUUhCMHCwuKXff+SryhyTCeRSCTPAueUKmMHeRAgXUeRMKgayaRBVUBRSU8OQiEUieDePFJVVqyIoMtHaoaK6XLxH0KEENM0MMYdy/rggw8oZ9lsdnZ2VtP1vv7+mzduaIra05NHALquy6lPyUchbXGJRCJ5BhACRfHvTONclhXL3PNRNBIUlpXhfs45q9VRLstdh65uIE2npQqjQSqZqlaq3QYoY+22xTkDAMZ5p925efOW5wfXrl1Lp9MY4cXFxWg0allWobA1MDDguO76+vrY2Ojg0NCd23cVVb6uJU9ARrdJJJJ9xyeMbkMIMAaFAKWAMWAMfgAKQRhzSgEQcAaMA0JAKXCuqqrIkrRzNtZ1rRub6Xk+xkjVVM/1EEKYEEZpN0JTVVVx4rlzZ9vtzq1bt76I5yL5GiIHdxKJRPJscA4BhYACAoCd3OaU7rKEOCAMqgqcA6WB54tQ9e26KZy5rru7PVXVVUX1PM/3ffB9hET4O4KdZAwA8MEH1z3vkbMkkt1IFZdIJJJng2BkGIAQBAEgBIRwx0WqChiB7wMhQDAgRAb6WbnC603QVEQZuK6h657vI4RCIZMxZtsO52AY+sThw329vTMzM6urq5qq2o7DGAd4xD/qOM5HdUciAaniEolE8kyIsPLnTyNFoRsFzjnpyfnX7ygTh7jn8mIF9WRwPErXt8ihA+C6EIngXJp3Omhu6eDIyMPZh4SQwYEBVVMfPpx3XTccjhyfnAyHw4SQarU6cvDgnbt3ZYETycdFqrhEIpE8E0jXlZEDOBIGReGOowwP8lKZDPf7N+7gvjzuyeJYNFhYBdcHXSeZJA8YCYV5KOz7AcYIIRSLxfr7+7a2iqWSK1Iae54HAJxzP/DlQnDJJ0B+aSSfhKfUHNt9wLMf9on78FmFZ362rUm+mVBKN7boRoFbNtI03rG457FCKVhc4baDs2nOOcIIfB/pKutYrFSh9RZGKBKJAAfOWb3RmJmZrdcbnHPbtmZmZirVysLCgqIoh48c2V01QCJ5RqQtvr94ilA9ux3QLR4qapY8Mf0qpbRbMhlj/MTGu+2ILGyPN/WUuxChv+JcRVF2t/8sYrw7xdvu1kSHn70nkm8kHAAeL1HPOetY3pXrQAh3XaQboCq8VkdbFe4H3HHo6joiGAjxHy6C73PHAS8ABCyg62trlFJOYWVlxfN88WXrdDpXr16Nx2NbW8VMJuv7wZd1v5KvNXKl2T4iCIJSqdQtZtwFIaSqak9Pj2EYf7YR3/c3NjbW19cBoL+/v7+/f3cZb9/3W61WpVKpVquu62KMI5FIJpNJpVKmaXbfiUEQtNvtSqVSLpdd1xXly/L5fCKREDXKnn4X7Xa7WCxWKpUgCDRNS6fTuVwuEomIEz3P29ra+qiYIKH6+XzeNE0AoJQ2Go1qtVqtVj3PQwiJDqfTaV3XpYfzm8rTV5o5rqfrOgD4vr93ovqRLycC4ELzkWmgSAgAeKvDXW/PxWBnQLDnfdvdGIvGMCGtVrMbmi6RPCPSFt9H+L7/zjvvbGxsUEr35EBNJBI//OEPn67iwsZtNBqXL1++d+8exvjll1/u6ekRKi4s2q2trRs3bszNzdXrdd/3McamaeZyudOnTx87dkzoImOs0WjcuHFjenq6XC4HQSDE/tChQ2fOnNkzLNiDOPf69ev379+vVCqinmkqlTp9+vSpU6fC4TAANBqNP/7xj6VSCR61pbrJ20Oh0E9+8hPDMCilW1tb169fn5ubazQaQRAAQCgUyufzZ86cOXToUCQS+bQPXfI1BGHc09sbCYcXFhb2KD08IsO7RgCWzTsWwE7Rs8d4or3U3dho1EGWAJB8IqSK7yNs256fny+VSntUHGNs27aIsvkohEi3Wq2bN2/eunWr1Wrpur578StjrFqtXrhw4caNG0EQCPtelCItFoubm5uEkKNHj2qa5nnetWvXfv/734srisPq9frW1lapVPrpT38ai8WeaAQzxlzXvXHjxu9+9ztxaUVRLMuqVqvFYhEh9NxzzxFCgiAoFArr6+uPu/oBACEUjUZ93+ecVyqV3/3ud/fu3RP+AFGmpd1ul0qlzc3NN99888SJE9K7vg/hjLVbreHhoXK57HneM9nHIk/6J+UjS6hJJH8OqeL7iHq93m63fd/XNC0ej3eVEmOcTCafbgHbtl0ul+/du3ft2rVGo9Gde+4aE0EQLC4uzszMOI5jmubo6Gg+n+90OgsLC+VyuVqtXr9+vb+/P5PJ1Ov1q1ev2rYdDocPHDiQy+Vqtdrs7KxlWTMzMzMzM2fOnHmiinPOy+Xy1atXW61WKBQaGxvLZDIbGxsLCwvNZvPtt9+emJhIJpOEkGQyuXtQIubpG42G7/uEkGw2KwzxhYWF2dlZx3FUVZ2YmMhkMo7jPHz4sFKpFIvFW7duHThwIJFISBXfhwSBryqqaRog//iSrzZSxfcLwvQUNmhPT8+rr77aDYhFCOm6HovFPupE27Zv3Lhx586d+fl5YQQ/7h70fX9lZcVxHEVRRkdHf/jDH+ZyOcuyLl269Jvf/EbMppfL5XQ6XSgUACAcDh8+fPi73/1uLpcrlUq+79+/f59SOjs7e+LEiScG6zLGHjx4UCwWOeeDg4NvvPFGPp+fn59vtVqFQqFUKs3NzZ05cyYWi7388su2be8+sVwuv/POO+12O51Ov/jii2KFz9bWlmVZhJCBgYEf//jHqVTKdd133333t7/9re/7W1tbtVrtoxwDkm8wCIAQwhijlIEMHJJ8tZEqvl8QhqyYhM5ms+Pj4yJOW9O0p4SRixNbrdalS5c2NjYURRkYGGi327Vabc9hiqL09/dPTU212+3Tp0/n83lVVRFCBw4cEC37vu/7PkKop6fnBz/4QaPR6O3tzeVyiqIYhmEYhgg4F515Yk8YYwsLC8K9OTw8nMvldF3v6enp6+srFouMsaWlpRMnToRCoUOHDu2qJcWbzaaY4IxEIufOnRsfH1cUhVLa399/9uxZ27YnJiay2SwhRFGUboeDIBAz5ZJ9iK4blmU1Wy0Z/yv5iiNVfF8gXMrVapVSijHmnC8sLFiWpWlaNpvNZDLdAO8nnuv7vnCAHzp0aGxs7MqVK41GY89hmqadPHlyYmIiCIJIJCIkHAAsyxLyrOu6iG7L5/OZTEb0hDFWr9dXVlY2NzcxxoZhHDp0iBDyxG54nifUGgBSqZSmaQghwzDE7AClVMxihsPh7uyAmM5fWFi4efMmpXR4ePj06dPhcBhjrOv65OTk2NgYpdQ0TXFRzrllWeJcXdc1TfuM/gKSrxMcwLKsubm5TrstVVzyFUeq+H7B87x6vS7i2mZmZqanp13XVVU1nU6fO3fu9OnTYpXX4ycKe/3w4cP9/f1Hjx61bfv69euPS74IRxcmdbdqU7PZvH37NqWUEJLL5VKpFOxUViaEUErX1tYuXrw4Pz9fLpcjkcipU6eOHj36RBUXtyDGBEKDMcaiKV3XRWudTmdPjJ6Iab927Vqn04lEIpOTk8Lm3t3h7m1SStvt9p07d4TPIJPJJBIJ6U7fbwgfVafTAQDxZZMyLvkqI1V8XyBCr7tWZhAEpmkqiuI4zubm5ttvv+04zssvvxyPxx+XZ7EO7fvf/76u66qq+tuVl57A7lQqQRAI+Zybm+Ocx+PxY8eOdafeu8tk19fX796963meOGZ4ePgpd0EpFS5useZbNLL78+M+cM/zZmZmNjY2AGBwcFD40h/vsPBV1Gq1a9euzc7OilseHx+PRqMytG2/gTAmioI/Xcy5RPKFIVV8X8AYazabjDFVVXVdHx0dHR4eDoJgaWnp4cOH9Xr94sWLIyMjsVjsiSounOHPfjlhhX/wwQeXLl2q1+uGYRw+fPjYsWN7HNScc+HWbjabq6urlUrl4sWLuq4fPXr08cvtzsi2e7iw+wDG2J4cHc1m8/79++12W1GUqampRCLx9A6/++677XY7FAqJ2YGnxO1Lvqlwkcivm9pPDDp3+9URwhhzxqSzXfIZg5CIHN5+vz3bF0y+pPYFou7C888/v7m5GY1Gjx8/nkqlGGPj4+OdTmd1dbXZbC4vLx86dKg7n/2JEUbt1atXL1261Gg0hB/75ZdffnzqnRAyPj5+8ODBdrt9+/bty5cvLy0tXbhwIZPJDAwM7Dl4T87UPSm3YJejvrudMVYoFJaXlznnuVxudHT0ib56sVr94sWLH3zwQavVikQiR48e/da3vhWPxz/Nc5B8TeGcI4BoLGZblu/7kUjEDIVKxaL41omsQZlsdquw5Tj2n29OInmc7XEh2k4chBBGyDAM0zQ7nQ4hJByOdKyO1ensftEhhLrvut3bpYrvCxBCyWTy3Llzvu8ritIN5tJ1fWxsbH193fd9ETgm3lOf+EKU0maz+f7771+6dEko4smTJ1977bVMJtNV0G7dEeG4Fn3DGM/Pzy8sLKytrS0sLAwMDDzeuKIoYgWaCLgTLYhUmsIEV1V1d1yb53lra2vValVRlMOHD0ej0T2T3N1sdJcuXXrnnXdc1w2FQlNTU6+88kp3+lyyDzEM49SpU5sbGysry0eOHj18+PC//j//6nkuACCEent7Dx0aL25tfdndlHxdQQBmKOR5vqoqhqFjhBHGqVRqcnLy8uXLA4OD2Uzm/v37CwsLAIAxVlVVVdXA94miIADHdQ3DYIw5jmOahlTxfYH4ezebTdd1Rei1kChhWAgzt1sO5BMjFPHixYt/+tOfHMeJxWLnzp176aWXdseICd+1ZVm2bSeTSeHixhhHo1HTNMX8dL1ef+JgQtO0SCTSaDQopY7jiEg9kQ1bqHgkEuk67Rlj7XZ7bW1N+O0nJiYej1MT4QIXL168cOGC67rxePzcuXPnz5+XQW37HEVRBgcHD42NXbp0sdNupVJJQjAAiLI9qVTKsixZvETyyUAIAaBXX311dXU1n88fPXpE1/VOx7p27aphGOFI9MUXv3Xx4kURVizikM6cOatpSmFr69DYIc7ZpUuXXn75lVq9dvnylWPHJqWK7wsopXNzczdv3qzVaslk8gc/+EE6neacu65bKpWEBIr1WmKjEEhFUf5sbZIuYqBw586dy5cvW5al6/rJkydPnz4tErWKgYJw19+8eVMkWj99+vRzzz1nmqZIrNbpdMRbUtRNoZSKWhTiREKIqqrZbHZzc5NSWiqVbNsOhUKdTqdWq4kOixXkoj9iuFAsFgEgkUjkcrnHb6TT6XzwwQcXL14U+eZOnDhx6tQpVVUdxxE9UVVVRMJ/pn8NydeAdrvdqNdjsdjMzAwA6LouEqozxkKhkOt68ksh+cRgjDRd//a3v00IyefziqJUqlWEEGMsEg5hhHVNO3fuXKfdxgQXClvHj0/+8Y9/8H1fVRXDNA3DMA3Dj0R0TWs2m1LF9wUic8vs7Gyz2YxGowMDAydPngSA5eXlubk5EfU2NDRECHFdd3FxsVqtEkKGhob6+vqeUcMopevr61evXi2XywCgaVo4HF5eXl5ZWYGd5WojIyPxeLxard6+fVskQ02n04ODg5Zl3blzp1KpIIRM0+zr6wMA27YfPHgg0qMODg7mcjmM8ejo6PT0tO/7i4uLKysrvb29KysrGxsbjDFN00ZHR7tJ3zjn1Wq11WohhLLZrK7re26EMba6unr58uVmswkApmmqqrq0tNQ9LBQKiQ5LFd9veJ63vLwc+L7rOD09PWtr69FotNVqiQIBxWLp4MGDhBDf97/snkq+fgiX5/LScjaTsS272Whout5ut8LhsKKQcCg0O/vANM3C5kY6k85kspbVWV5eHB4e2twslMvlgwdHQqZZrVV1XTcNvbe3V6r4vkBkRR0YGHjw4EGn03n33XcXFhYQQiLJqK7r4+PjQ0NDCCGxHHx2dlZV1e985zu9vb3PeAnP8+7du7e5uSn+2el03n///W5ImvCZRyKRZDJ5+vRpsfprdXX1rbfeyuVyjuOsr68LC/748eODg4MIoXa7/d5779VqtVAo9O1vfzudTotouP7+/sXFxUKh8NZbbyWTSZGkXYxCDh48uNt1X61WxfS5mJXfLcaMMcuyZmdnC4WCSAYnarXtDkrPZDLxePzx2XTJNx7XdWemp0XYhGGaG5sFMYMDAJzzUqn4UckVJJJngTG2vLxYr1UZYxgjhDGjlDG2srzsuh6dD0zDbLdbnEO9VmeMX//gejgcdl232WisLC+3220/CHzPsyxr9sED+UXcF2CMc7nc888/X6vVKpVKvV6v1+sAwDkX+nf+/PlkMilcOpZl1et1RVFs2358plyEggtn+25vs+M4CwsLokGxpdVq7e4AQkjUKu3t7X311Vd/97vf1ev19fV1sZibc24YxsjIyGuvvSbqgYp6aLVazfM84czEGGcymRdffFGkgF1ZWVldXe3enThxt+K2Wi0RtZ5IJPaEqokZcTFrLl7HjDGR6KOLYRgyA+v+RGQQEt/tbkL+bmqBSqXSbF592rz4npVpnykionP3eo09EcuSrz6c83q90Wg04NmK7bTbnXKluntLtVYXH1rtjlTxfYGQ3snJyVAodOXKlXK5bFlW13195syZAwcOCDHTNK2/v79cLjcajSeWJNE0bXBwUKhjOp3ebftmMplwOPzEFwpCKBwOiyQqqqqeOnXKNM1bt24Vi0VRFTQcDo+MjJw9e7bbpmmaBw8eFLVHu7F4qqpOTk5ijG/fvl0qlYIg0DQtk8mcPXt2YmJit1SLKKTx8fEgCIQ3frctLj4nk8kjR4581EOLx+PhcFi60/chaFdl+se/AIxzz/M5fLhQ6BEIRobBfR+8x/ztpgm+D2JoKM7FGDACxgBhEKkO/pweK4oSjUZF1IhpGkFA2+22CG2RWv41olsV8tM3JQdx+wgRAd5qtSqVSrvdXFliLwAAIABJREFUBoBIJCKSqAsJF6u2SqXSe++9d+fOnb/+67+enJzcY8X6vt/pdMSMYCgUMk1TiK7neY1GY0/SlS4iWCwSiYiMp4yxIAiazWa5XLZtmxASi8UymYxoTbw3HcepVCqXL1++d+/ej370o2PHjolRBWPM9/16vS4qoem6LlKl7lnpLqqhu67LORcB8Lv3inVo7Xb7Kda2qqrhcFhka//kD13ylUR81YWPZ/fGTqfz3e++btvOEwp+I8CEqPEYwph7PiCEVIW1O8gwEELM9ZCuIkKAczI8QLfKvN5AusYpZZYjsgyqx4+ycplV64AxUgl3fJxJIlVl5SrpybJGi7XbgDHCmHsBMnWglNlO2DA91/V9nwMHDqZpHjl6NBIO1xv1XC4XDofffedd8aMAgCAIVFVxXU9VVdd1xff/C3yuki8BaYvvI0TYeTKZTCaTTzms0WiUSqV0Op3P5x8XMFVVn5gBTRRWecaeYIyFDZ3JZJ7S20ajsbS0FI/HhTHdPVfX9Xw+n8/nn36Jp6Rt+QQJ6ST7HARIj0YPvPE9rCp0qwyc40wqmJ4jBwbAcVmzidMpFDJ5oYgH+oLoBgAn2RTrWMHSGsIYONcmj4Ln0VIZDB1TygJK0ikUMuniinLkEFvbpPUGGDoKh3izQ/rzzHH8hZXJwaH1tTUxRKaUloqlrUJh4pVXBwcHMSFjY2OiHPBWoaAoqmkaju00W81sNre6tvZwdlZM50u+wUgVlzyCiAz3ff9b3/qWmCn/snrSbrevXbuGEDp37lwmk5EhZpIvFw5ACfFSCRQOM8bA0HFPnlaqQTzK5hZQLovHRiDw2cIS9jxGEIRDyAtAUWk8ykMG1BrUthGlPJNCus6XVmBoAIplFPisWkWlCrTbXCHI0FDY5PEYjkWYa3jahuPYnut5rss4Y5QBwIkTJyqVsqZpumHW63XTDBm67iVdADwxMX7jxnXPEwd/2gwQkq8FUsUlj6Cq6ujo6MGDB8fGxr5cZ7JpmsPDw88///zg4KCsECr5KuA7zvrdaRI2aaWKIhFcrQYLC7hW86cfKAiUeg15nm91SL3ObItXyrzZQZjQcpnZNiCsMYYySVoqk3gMFIX+6TIPAmVkKCiVoFpXDvTTYhknE8ixWbGCkgmggTM/P3bkeKFQqFarnDMA6OvrT6VSCwsLruPk8vm7d++02+1jR4+trq5qun7hwoWBgYGVlZVkIvlgZvbLfmCSLwI5Ly55BJHXQgSEf7nmL9upNiHm1L/Enki+eXySeXEAAECEAALgHBACQMA5cMYpU8YO4v48UhT6cIlubgHn23Fq3fbFgFiEr4uCaZRuf+AcOANMdprl26HLO4mKdxoRZTK2S/nBTnGBoeFBQzcfPHggolIIUfoH+np7eu/evduW9dH3AVLFJRLJvuPpKu64XigUAoTcneS+T20LAAAUgkwdOOeOB59mKvrRF3L3H7uXlsEjIfRiBYrSrSYggk4Y577nfyYh0JKvONKjLpFIJB+CMNI0NZ1Ox2KxldVV91GlfxqOBwCAEHz8hDB7yvR9XEQG4u5yEhGvjjF6luXI0tH1dUequEQikXyIqqqKilzPa7XaqqIg0/z8UrgIOIDrOrZlfa5XeSJEUcLh8Bd/XclniFRxiUQi+RDGuO/7QRC0Wy3YcUlv53f5fOScc95qNsuloohf+yIxDNM0zC/4opLPFqniEolEshsRlQZ896QyQk9M1PZZXZExSmnwxUcpUSZXk3/tkSoukUgkT0NV1Vg02mq3Pc974gEIY4wQB84p50/VehFVvmcWnHMALqLaOQAoqqpgTDnHCDHKiKpgxG27m4UNIYQIwQhjYCygVES7aaqKgVMKGHPP/8gBgUj9JPZSSoHD7qzskq8jUsUlEonkaRiGPjg4sLi09EQVRxib4Wg0EqaOVak3EewsFUM7HvjtDQgA6WZII9DuWLCzkPJxItn+wxltoWwP9ma3itVULtebQBfeuxkEAUIYAUck3NMT1YyQ1ahVas0gCKhqjB6ZUDu1xXX/xOHw5VsL2+vXOEUIi0GDiGDXdb23r8+yLIzQ1tbW5/nYJF8QUsUlEonkafi+X6lWvcermwAAcFUzkqmc2674lJmRqKYSN6C6omBMeOD6jCjc8zlSVIUjbEQiEU1V6nWMeLVcZU+qGQhG8i/fOPsfN+qvnxucWy0qqnn+ZE+p6jcaVdWIRHXUcHp//HrPnYeb1WYmb9mV9ZVVX504+cLJmPcv/3PuL17tKdh6JqZZPu9UtqLpXqdVqbWs4mYBAAzDOHPmTDabu33rVrlc/vwfnuRzR6q4RCKRPA1N1fK5XLPVsmx7r+uZg66CoqPN1SYgdPzcufL6WiiWGkqHllcrI32xtSrH9RUj31faXI72jxG7FM8OhiO6Ec/YF9/reE+Ylg7Ky2zo/zhmryqIvHh28vKVmVzfgYlDx3NZUqgHLz43+Yv/62o2qs1PT4++9P0hg8yDtbba8er1yKHJ00doPhv9b//7iYzidny1uXhr7NxfVGYuXZmZ+cNmAQCCICCEjI6OXXz/felI/2YgVwpKJBLJ0/B8v1Kt+p7/RNGjHABBOGxquqFi5Ng+Z8yzrFqjiRUdvE4okTFVcAPstTtEUYiiIDDapdIT48o4QBB4H9zeONFrbBU2TUIq1U5lc25+YT05eLC3r1/Vo7RUbtpty3G3FpaT2Ww4FkIArtN698LF8VPjuqLkYhGrVrt748aBwy92qhuJniGnXBLtK4rS6Vhvv33BMAyZ8uubgbTFJRKJ5GlgjFRVxU+0XBFyHK9VrYXCIde2V1bWdA1Z1eJmEwVOZ3Njs2O5gcOClhLWFGY3ixWr1QjAdxkLvOBJ68o4D3zv+nu/Nyrp2aXNSqmwtLj+7vvtYmn9zo2btsUqhdXNztLdeRVzbrVLd+/dr9Zr3OmsrywH9XIZoc2YNWfNx5A9d39WjyerD66lBg4srRVE8+12+9133g6CAGNMKVUU9fN8cpIvApmBVSKR7DuekoH1+2/8N9+nuzOamabZ25MvbBWtj0jMghDChHDGOABGiDGGEGKcE4w5IASMMb59AAcAwBgjBN3a9oyxeq1aLG7trBdHRFF0TfEDqmLsU6ZriuP6mq4RogCjrm1robDvOkAUQ1OsTttnoBICjAFRdAX5HBuqYts21nTuOVhRPdeh7AmvetMMDR8Yka71rzXSFpdIJJKn4TjO6uraU5ZWc87pjiTTnS0glnLt0D0AACh9ghUu6puIz4wGth2I1jhAEPgA4NhUNA0AQafNAcD3fRc4BwQ7YwLm0QABgOcCcA5iY0BhV+r1R6/6LA9A8pVGqrhEIpF8CNpe1P2IvgX0o4XwU4MxVlTVMMwv3jOqa4bMo/51R6q4RCKRfAhRCCYKxhi+KD8z5zytqvF44otXcVEA7Qu7U8nngVRxiUQi+ZAgCPbMi3+DYYw5jvNl90LyqdgX31SJRCL5/Hl2S/pLjCmW4czfNKQtLpFIJE8DYYSJCpxhhEQqU8oYAgDONVVjjDEOigIceEAZMOAAGCsAwDkFAISBs+14N4SxQgijAeM7IXBPviRCCCPEMQYaPJJ0HWGiEAVjzgFRRlnAnlAJ7YmVWxBSFBUhYJxhTAjirh/wJ8XZAQACjlQVAso4RwgAIf6kEHfJVwGp4hKJRPIUuBaKDI4fac7dH516bu7ucm+ffm960dCI32q+8ZO/vPKfb3lm+vCo4YXSSx+850IMgEXSx1JaZXmzhAmOxrRWw2YMHNsCRTsyeSLsNO+vbgSexwkBzihFqopFlRTf9/yAqkYkm0yHQyoinZWVsk/BVFXPc13P02PhyfHTpub6Zqi+ulnYWO9YrmGqlDJACAP4AdMMFRgH4L7nASaaQlzb8Xxv+NDZA/nYWq0UisRyYfPK5febTVtRVc45JpgxoimIcUoZVxAbfeWNrbd+0YnFOPUjuaxbKrsMFIwd1/F3xdtLvnSkikskEslHw0HV9f6RsWTQPnz0WHmxPjSc42Y6n4h0Ht47NnWWlmoWj/Zkaxvh/NDcSO7ICJDA4gcPpOr5Og+89thQcmOr6XvBvatXO0Zs/NAhq9Z+fWJ0eWY5lM1Q6rSaoQM55oWT3Gotry0uLq5mho78+JWzKyuFREYZTN9Z9JPH8pHV1aU7t+5Pnvl2wrr/9qWF4XMvHD9+cmT88L33H0y9NLa2uaUQiIQShfWtQ8fH7HaLA95cnNPT/T1RbW5m+sHM9InnpjYv/uHQqRdVe73W9FAAiqaNjo10LLu/v7dQjk8MWK2O4yOscHb4xImrV67kXzoXlAp9L75aevt37XAqa5I7d24sbRSZnI39yiD/EhKJRPJUOBBVjSZSuqoCi0weGx/oT3uq0ZdOs8Bvl4uDg0MmxtnRscOjp+LIC8di0UioWSl3gmzC1Kv1uhrSErGUoite4NUqBds2+lLUDiXjvKNF4wd7xxNK0wmnDU4j4YiqkHarYttWo9VcWa6MH+55/oWXYmEtFEkoBBKxWLVWIxgBY7XalpfpH0oNJuMJXQkFfoeGhkdHekKxEPPBdVnv8ODp585FTDUSDxFNWbj/MNLbZ/r20twC15On+lJYUdK5XCqTGRsfTeUOE/BIKPrC1EStWnYQSaXSuZ6egXzKYqxW906eOBoKG+GwJiPav1JIFZcAfxJfdqckkq8KnNFmaWtx9sHqxiZlXqPV9oDkMymEUa1UKG9uOo7jOp7dajertVAqm4xGPNda2yjWijXLcrxApzbVwslYGILArzfrjVazVFpvNKokmlTBaljVYrNcLpXLW2XbcjgDu9lxAw60vba21va9wtYWo6zTrFHGHz64PTh+7uiRI9lUrFIoFqt1xGilsrVRa5jRlKk465VOoVTaWN8sbxWY71TKdT9wm40OBW2rsEoVrVHcDHgEc6/j+cBZ0/Z6+vtDKkYIxeNJFfnrpXIyk9cCJxSJmQqhrl/bqqWykVq95bjtZtNlXOr4VwiZgXVfI/JQBkEgag8LEEIYY0VRCCHfsNSMYoDi+764wW/Y3UmenY+VgZUQxYxEfNsyQlHP8SJJ00zmzxw/Urhzfb7S7FTqRjSJwPaNsNrwjpyd7EuqV68/WC9XCNIJoYqmqIRwhFvVLZcrpm4gILoatC0/EouxwA58BSOPEhP7TsCZ6/mM4kw2FXiO5bjRKLFcJRbS2u1Op91RFMWMJzQIfOC+EyAtROwAm8xyvEjYJIA7tq9oOHA8hEFVCCDN0Hmz2bJsLxSOmobqOq6i6qrK6pU2x1wzzHAorJAgPfS/JdmF+/NbPqW6pmOiu61WKB7xHccJsKkjLwBDCeqNtutRmfTtq4NU8X0NpXR9ff3+/fuU0q6kYYxN08zn8/l8Ph6Pf5MWznLOW63WjRs3hoaGhoeHv0m3JvlYfCwVB4DdYd+KpiVzPSEUlCtV2/EYYwgQR4AADDPRk094nVaxWvOD7fSr3V/WE1+2CMHO5kciyxFCHLbzrQIC9Oi7GiG0055onD/WwO5LfHiu+Cx61G0PIUAIzHAvBDXLcQG4kAYESLTJge/ch1SMrxwyum1fQyl9+PDhv/3bv0Wj0XA43P2Z+r5PKZ2amvrxj3/c3f4NgDFWq9V++ctfvvbaa4ODg1LFJc/Mh9oVeF5pbQV2qSPfETrbqi0u1narJvw53dt94KPbd/1zu/kn7n3ksI+4xN7O7OkR58A5dFqbuwYCH97Xs92H5EtDqvi+RvwuE4nEa6+9Njo6qigKiApL9fo777zzpz/96ciRI5OTk6qqwq7pc9guyoT2NCXc8gjtTUPNGNu2GhASwtltZ/eRYmN3S/dyexoUF+r+U+za3bfHO9DdK3pICNkTAfB43mzJvgUhTBTA6IvLwCqRfBqkiktA1/Wenp6RkRFN08QWMVk+Ozu7sLBw5MgRVVUppb7vt9ttz/MURQmHw4ZhCC3nnFNKHcdpt9uMMcMwIpGIoigYY8ZYEAS2bXc6HQAIhUKhUEi01mw2ASAajXbnpy3LarVa8Xhc13XOued5rVbL931VVSORiK7rYgRgWVa73TZN07ZthFAsFtN1XVyl3W4jhAzDCIfDogNCp7tNKYrieZ4YGQCA6EYQBMlkUk6TSwSccxpQjqXhKfl6IFVc8iE73rYPLVdhpApH9MWLFx88eNDpdDRNGxwcfOWVV/r6+gghlNL5+fn3339/Y2MjCIJoNPr888+fOHEiEol0Op07d+5cv369UqlgjJPJ5JkzZ06ePMkYu3TpUqFQeOONN/L5vDCOb968+cc//vEf//Ef8/l8qVS6evXq9PS053mGYYyMjLz44ov5fB4hdP/+/bfffjufz6+vr6uq+p3vfOfIkSPT09OXLl0ql8uc80Qi8cILLxw7dsw0TcZYs9m8ePHirVu3RN96enq6iaM7nc5bb71VLpd/9rOfxWIxqeISAAgC33VcJGdbJF8TpIpLwPf9Wq22tbUlPOqU0kajcfHixUgkMjExgRDqdDq//vWvP/jgg6mpqXw+3+l0rl+/XiqV/v7v/z4ej29tbf3Lv/wLAExNTZmmOTc39+///u8Y49OnT9+8efNXv/rVwMDACy+8AADT09P/8R//QQg5fPhwPB6/evXq2tpaJpNBCNm2PTMz4/t+IpGo1+tvvfXW8vLy5ORkNpstl8u3b9+2bfvNN9+MRqNiZNDpdF544QVVVePx+P3793/5y1+Gw+GzZ88SQubm5n7+858DwOnTp23bvnDhwtWrVw8fPjwwMFAqle7evWtZlrhxjHE0Gg2CQE6QSz6EAxcTxRLJ1wGp4hJoNpvvvPPOrVu3EELCl+44jqIor7/++tjYGADMzc1dv3793LlzP/jBD3Rdp5Tm8/l//dd/vXHjxpkzZ65eveo4zt/+7d8eO3YMY3zq1Kl/+qd/mp2dHRoaunHjRiaT+Zu/+ZtMJgMA4+Pj//Zv//aLX/xicHBwaGgoFArdvXv3+PHjGOPNzc1CoXDixAlCyMrKyu3bt994443z589rmuY4Tjwef++99xYWFo4fPy6C71588cVXX32VEFIul//X//pfoVDor/7qr3p6ehBCJ06c+Od//uf/+q//Onz48MbGxrVr144fP/6jH/3INE3LsqLR6FtvvSVuPBwOf+973+Ocd931EolE8vVCqrhke168p6cHY7y1tTUzM5NIJF5//fVjx46pqup53vz8fLvdDoLg0qVLYrK50+lQShcXFycmJtbX1zOZzMGDB8XUcjqd/su//EvOea1WK5fL586di8ViwsrP5/MTExP/+Z//WS6Xx8bGBgcHb968aVmWYRjz8/Oc8yNHjnDO19fXHccpFouXLl1CCFFKS6WSZVmrq6uTk5MIoVAolMlkVFVFCLVarfX19Xg8fu/evbm5OeH/9zyvUCg0Go1KpVKr1SYmJkzTJISYpnn48OG33367G6NnGAbsWgskkUgkXy+kiksgHA5PTU0dO3aMENJoNJLJ5JUrV8rlctfB3mq1OOczMzPz8/PduLBoNCo03rKseDwu4tgRQoSQgwcPep43PT0dBMHuFeeKoqRSKQDodDq6rh86dOjKlSsPHz4cHh6em5vr7+/P5/MA0Gq1XNednp5eWloSJ1JKVVUV7SCEVFXtBqOJDjiOY1lW90K2bcdiMVE7WQTciQw2hJBYLEYI6d671G+JZJ+zZ2Xg1w6p4pJtXdQ0TVVVXdfPnz9fKBR++9vfZjKZs2fPiiQwpmn+7Gc/y2azIhLN87x2ux0Oh0UMueM4lG7nuGCMCdtdrCuzLKv7C+mGpodCIQAYHh4eGBi4dOmSrusbGxuvv/56NBpljJmm2dPT83d/93cHDhwQDXqeZ9u2aZqP+70JIbquP//88y+99JKmaeIHWa/XKaW5XG51dRUAPM9jjImYedd1dyeqk0ieBVVVNd3Acsz3TURR1Vq18mX34pMjVVyyTXcxdyaTOX/+/Nra2i9+8YsDBw7E4/HBwcErV67Mzs7m83lN0xhjm5ubP//5z8+fP3/8+PG+vr47d+6sr68PDQ1hjDudzq9+9SvHcX7605+mUqm5ubmTJ0+K9svl8sOHD6PRqIg2j0QiJ06c+OUvfykWevX19YlFaL29va7rlsvlAwcO6Lrued7S0tK1a9defvnlZDK5p9uxWKynp2d1ddW27UgkImLx/vSnPzUajX/4h39Ip9PpdFqY+6FQyHXdhw8fOo7T9SjYts05F/52aZdLnoj4afie63nel90XyWdPNBb/VOcjhBAR6e0+/sl8u4mPzNnz55EqLtmLpmnHjh07ffr0H//4x7fffvsv/uIvjhw5MjIy8s477wRBkM/nXde9ePGi4zjZbNY0zampqenp6V/96ldnz57VNG15eblYLL722mv9/f3Hjh37wx/+8Jvf/GZkZIQQMj09vbGx8dprryUSCXGho0eP/vznP79+/boIRxdO76GhocHBwffff7/dbvf29lar1atXr5qmKc6CR93giURiamrqt7/97S9+8YuTJ08SQhYXF+/du3fy5ElN03p7e8+ePXvjxg0AGBoaqlarN2/eFIvXAcC27StXrjSbze985ztiBPCFP2zJPqH7lt79AXYnSnsGDXjGwwB2UqZ+7G7++Q7I38ijcI61kBIdYBxzkbAWAACQ+EtzAABROwYBAII9qx8QiJMeUXEOgBEAAON7HzfbzqaHukciqeL7HIxxJBJJp9O7ndUIIU3TXnnllWKxuLGxUS6XR0ZG3nzzzQ8++GBtbW1xcREhlMvlpqamRkZGFEU5cODAT37yk5s3b968eZNzbhjG97///ampKV3Xz549qyjKw4cPr1y5QggJhULf//73xUYhmel0empqam1t7fjx4+FwWFw9m82++eabt27dWlxcXFhYAIChoaGzZ8/mcjmMcSgUyufzIioNADRNO3XqlKIod+/evXr1qpgdeOmll5577jlFUSKRyPnz53Vdf/jw4drammEY4+PjnudFo1ERplcoFEqlEsgJcskzg5CiaFHEvSCwsRrGzPX8j7TREVZUPYqJCrTjB1g1TObbnAPRDE59325QrqR6D3aqc763u5Ygf1TmESBMtFA4Eu80ijTwd13hEWVFCAMgNRTFSHUam0DIzrhhuzWEENZC3LcZY0+QZIQQwpxz4OzRPiBARIukDAKtZoXLOakdOKdq7EDquf8z4CGf4W6xN8RBwcA5pxxxBMABIU4UCALgbPsIBAgj8QEAEBMCzThHSFeBAfjetvYjkW8fgCPE2fZCSA5o+y/ztZ7Vl3xKGGONRqPVaiWTyXA4vHvW2fd9ERmeTqcTiQTn3LKsarVq27bI35JIJET4GwAEQdBoNGq1GmMsHA6n02ld18UUted5tVpNxMfF4/FEIiFmr7sdKBaLtm1ns9lQKNTtAGOs1WrVajXHcTRNSyaTkUhEVVXOeaPRKJVKvb29kUik21vXdZvNZr1eFx1IJpOhUKibyVX0vNPphEKheDxeqVRisVgqlQqCoFQqiYVzu3sl+cbzlGoo3/3u67bt7M76Isa14ssMAAiFe0a/m0yyxTt/MPtfjvH5pcWF7Rfq9mu1m6mcmMkDmf5DnlXFQZtkT9P6jGv5sfyY215knNSWrthBbPLVv9m4/X+3mpwxxgFhxDnjgNGOSQ0IsWj/S9xezfRPbM5eduwW53znxY4QFq9xBAgQ5f0nvlcrrpihTOXh21xVARBwBkjcDieqGs4fd4o3fE90EQNwBBwQYowjRY/lRqlV7jSKwDkgYVIy4AhUIzZwKqX7K3O3WOB/k2QjGou3mo1PdCpnNDAHXs29/j8UM+76EFBhVwPnoBIOHAKGOALEASGmqOB7nHGEMSAMCIBxIckcOOIccwSIcwAwDaAcPBd2Z7LnCAAB3skWzSgwxrm0xfc5CKF4PB6Px+ExY1RRlJ6eHhEUJnaFQqGuBbwnjzohJJlMdtvp7hWvv2w2K9aL797V7UA2mxUN7r66yMcirPPdlxMpVyORyJ7jNU1Lp9Ni1nxPHnWEkGmafX193ZTsQv6F1S6WmD9++xLJR4EQVhUteehss7Lkh7NhVEsNpNI9A5X1+ViMlwrVaCrtBapXvucwLZY9Ym9dLpdKgZ/91pnB29P/6TlsYPJbSyuXWtVNDgoAUvQwIaTn2Pd08OrVRiiRCIejrcLtVsfLDJ5QdcNqFPsm32xtXFaM9IGpvFN5uDRzCThODJ7J9o04lTstPxbUl0P5QwQZ4+feXHlwFeFMMp4trV72gnDv+KTXKRfWC4NjhzkLGpVOanDKSAzqCqzfv6BnJtKZAQB7+vKvDDM7fOrHtHJraXllYHDMc5rFxeuR/JFYqq9Zmgn0mBZV+45mQjp5ePF/MoVIBzsAMA6OB4bGTRM7NgsCzBECDBwBcMQRbLvVOWDOFQIcIcY5pZyyHT87IMQRbCu4GJwBEuIO6EMV58A5BBwQcAVxQhAhiFIuM13sa4SsCvbIGNqpMt5d3yX+KXhcjLt794SJianuJ+7q7hXb9+z6qMvt7tVHdeDxMYHog9i1+4pii0z5Ivk4IAR09cHt1IHnNc0IJUaSw6csX+npHc9N/nWy/+Xe0ZcGx6d8rmPCSSgZuDWMiaJWF25cGj3zg9zg0Pr8nYHJ7/aNP4+xGEESLX2uv683QLHM8Ku9+fza7EL/6b/KDozTziYyx3Uc1Kv1ZnGJIFpcmM4ef1PXdURCBOt2Rz/0wn8P5SbD4VRm+Ayrzzp2q7K5xIJate0MHzjRP/UjtzqvxUaj/WeHxw7WNuaN3InMwCTyyx45fGDiVLrvaKNYyg8fD3yfBna7ttZseQdPfK+yeN3D0dEXfhYJx4rzNwfP/GPIjOjxfjOS6rQdhPEnD8f6ZsEAMY48n3suN3SsqhwB44wzDl0JBwCEuJhIDCgPAk45AGAADIA4bIs9RzvO8q7HfNtU364xt/PMEWPIDyAIxIBDA5XxAAAQO0lEQVRBIpFIJB8Dzjm3yjMrS5sDI+MqMY1YGrjbrky3LNw7OhpwonAbIcYCRq1qJHtEC6dDsbxbny6sLkd7p7hVWLjx6+jQy6GwCQAAmJgpVTUQd512s12ZcytbyEioRoj7Hd/xmNtxOxZjzGoW3faiTYlCNMWMp3qGEAsUI8N9ZiR6dDPE7LLrusy3WpWN6ta8qcd0zfTsOg18rJpOZdbx6hwQ9TtWY8kuNfVwnChK4Htippszz3OanGBMwHVtz/dVM8WYHwQt32eKprvtotVopYaPKHIq9kM4B+AceT74AVdUICpH2wrOARggjjHHGFHKg4AzhriIfhPGujgWECDeFeqd80XkG9pWexEfAQgB4ghxwIyhgCLpUZdIJJKPAed+u77kBeV2daaYy/mlmzZKEeI365vNe79Oxo1OxyKsFfgOpbyxdTPVcyCeDwUdV4+HOeXNzVktklXMRGPpT47lAuDy6u1GYVpBntMsOk7ZVYoM2lsPLjmNrVB0KBQxGxutztZtXVGa5VXfc6qL1/zAp9BqVVewElubudjaWkrn0q3iQycICov3DV21GuvMaxS2Zuura9HkiNdaaZXrBYcGjm2V7nKlaTXboNwrQotpLJIdBuZiTFjgtsurpoY3Hl6L940x1lq89v/q4WQ0N16d/f8aTScSiwQ+bxYChqQ3fRshvsLcdn1OGFdVhLZtaIwBEAZgEFCGMOLbh6Mdq5p3J9IfdZ9vN70dGid27Mya77AT3yaj2yQSyX7j00S3ASBMVM4pZwFRw4gHHBFCMA08zjHGwDgHzhgNxKFENTBGnHKsEM4YDXyiKAhj6jlBEAAAUTTOAqyZiDNGKeeUM4aVSCw7nhkYNcKxh5f+KaAEEHBGGQ0wUanvIoSwqhGsAPAgCBRFBUCBbyGsE4ID32M0IArhHCm6wQI/8H1CgDGGkCrqCQMommlmR74bDkf9zvz8nYvAKVY0jBDjTFF1zgLftRXNxEShnsUBY6IgjBFjvufwb4pL/VNGt2l9ryZe/R/YiHEsYsmZikHXEAbmB8hjKGAcGCAEmgaeD5R1q94KG1wY1wyAIsQIcITANBAD8Fy240lHXGg9bAcjPuKo/ywegkQikewfOKO+eLfSwEYAAD4LAIT/VKwj2hkccMaoZ2/nNfTFMeJ08SrmAEADDxBw19reyAEAqN9ulaa95qrrNhgNOPe7jVLfFbYb9V0GnjjL77bJbBYg0TgNOELg24Go1CbGFRy8nRVknmsFxYcXCAbHbiKgHDijnrgDnwbb3fMd6osGGWPBTgj+N0TCPz0Ig6IiQnZWeQMCYAFliQhhFBoWBwSAEQbQMIACVCwZRwyAE84JUI3QiIniYYibKKQTVcOqhjgHTgFz3l0CLKx7nwFjgHa+PYTIGHWJRCL5eGwvawAQYvp0+OOHCAnEBANHjLEd7d5zGA98iwY253sWZyNAiCDEOBfLlHa3ueczQghj1M2OvL1z53/Cleu7NY/v6iTf22A3uGq7TYKf2F+EECaYUfbs/l2EMELwcTMiI4wJxpTSZ7kQxhgQMPY5lprlHDzKCQP04X0gRqBtcaIgIMA8zihgYBhjz+eUYwRcQdRQ/JjJ0lGUipFwiHCEmM99n7XaASGIUQ6cayoJ6Shk4JCOdBUzzsu1TsOltksCjjhHGMt5cYlEIvlYIGyEIxFT58Cr5TLnbDtPl3BwIrGkcedYhIUMd3fvbEehaFIHp1xrIwSP7gTYXni+o66ci1h2kZXF18K9Omw1W7x7IOw5cRus6PlcbG29iD/0zMLO5CtCgMLRDPPKtsPEVUT3t5O+CdlDjySf4RRS+azTrncslwMTK6nEmigjFI5EQ/VKxffZ9iCHA2CsEBz4dNuA/3AHAgDFDMcVXum4wALx1DAgytnjOeI4B7TddRyLpwwFKpUa5cHuRw3dnm//E2HMY6lU4DqdtiUMWdHIx/tzPwNoO1fb9lNWCAIOjs8QxYQgQ0UO286UwzlwzlQcZGN0OIfTcRU41Jr+wrpbbaO2BZ7HOQVdw5RxL6AYY02BiMnTUZ5PqumEChj5frC8aRfq4ASKqipSxSUSieTjgEk8nTZI0LTx+CFtpWCHdUQBa5rRqm7x/7+9c2mO5DjueGZWVT+nZ6ZngMFr9v3ikqt1yGLo4AgfFL45/NH8lXz1wSEFKXm56+W+QAILYADMs9/dVZk6YLlByrIlhngRA79zdXV2XrK66p//ojAZ9rqqyDY56HB662a5OG6cCQKzWSzqthOgwXDYizzwBpM+AJ1uinowTNE1ZdVEgyHadr5YJoNR4Omy2DCZfhxnq8uittFoZzqOX2d8Zxzx+Wyz3kT9oafgYjZjwLjXq/LC7w3RVVHSB9dtsqbXT6ZhCvl8dn7pJ0NpCkDtR6Hvh1W2iEf7qm4XmwbISFd68TDUuFwum7ZTfrQ1GtZVgcoEQdBWWV51SW946+6d49dflbX1/ChNB9lq7YU9X4FDlY77znEQROV60Ynq93tM3s290fM/PCst+55xLQ/SMK9k0I+5qyvWvs8P7n26Pnpzfn4xvvVgmujD04uyzH3je1GsiFxb5nXX7w+4LVfrTEy4N71JXY7GuKboxAsMZqtVOBgp7YFrEGC9WjWt7Q22b0wT8HtN1RbrxXK+jJKhRrtara39q/7jfwTfbaWjXPmxiWMgImB0VjwPvQDbhhHAkB16brqr98de1/Cbo/py4/JaNZ1mJifEwoSMSIzUAIPj2nLW8MWGDmfcC6tRX6a78dPHuH3evDvpNq25ruLXXHPNNT8CRFIK6iqfHy+e/Ou/bORyZPJ1JXG6d2dHnXVbxHV/Mnr58rUj7UcJ8Wis/EXRPfps/MWXL8JkezeNGkTlBX5kdvfEXa7i/mC8vVUtzyjseXGv/uL5/fu3s7zsj0dp2l9eVPu76Ze/f4kmCGOfyjYaDlKmXrozGYRr1gFW315U09u3vnnx9f6dX2B9GEYjY8zh28PtSVouRTUbAeht3UhhsenC0Hdeb3L/VvL20ktHO8rLKdlplmc3793tioYIT07PTS8ab21TsB/6/vzk23uf/PLNi3fpKPEDXylFSqWTg+3UYwru7qYZa78rM1L3H97L1nL/7vSbizzAqrR6e3vknLAJhqM0O6+f/MPtr15VN/Yi27Vn6ybGVZyOy9N3AGL8cJTos2rSS3pGm4P7n8xePYP03q5xqL20H3z5X/+ZAwE7Mr1PH209e/n29sG0LOpQw/7TX5+8fDW9cbfIM018Nlsiqf4wyToT+tx/+CT4+tno1kON7evfP1u58ies4gIAzHhlkIdABN+dKggIOJamFeNhHCh07ShpH90M4li/P6vfHttNRS1rAQWgCAWRCS2JIyQArYTlyhIGdMfYtrCp5XxtTxblgxve3f1oJ7W/e11cV/Frrrnmmh8DAiARaS/uN9lCHFeuHaa7nmcG/STPg+M373u7Q0K0rs3XheeZvChXJ7Pp7V+JoN+L16t5XteDya11feG8uL9zcytC44dsaDZfad1Pwz66TVZyNE57oclUNp+vBLiq82bjmpqWh+8bFfWnEyOFLNZF1QGgNr6nVRhFbeOKzcpLtz1fKYXFchlUlQAsZqf3fvWgWlaKuRf5/WSICyClPc8zUeRgO/HwZJ5XVQ1gxwcP4hjYeOTKs/Pzyaef98PzarXwouSqi6qu6mh/ezyOlWptlll2MhyHATVFPl8WnvEWx+9LnVZV2ViHBo0xXihR4AGUebZQ4UBpjxq7KaumaYFUXealonK5uvfk4ezwCMEuTy7CW4Odybht6/nFhWXs2OVZHpiwzsrGEtpquSpHxmjojt7NBuNeUXUmMIDQZXleDavW1asLL9iOw6SX+Jcnc+vsT3tGjiIKRaNc+bp8OApBMRqBxQIAAFtnfJlO4OZuSIjPvs6PL9lhIJqMOBSnyXmKfd32Qo48iiPPOVe1LmtcXkndqc4qJ0ocKfCr2nv+ul6v8icP4998Pryu4j8PhMU5aS23LA4AFWpNvkKNqH44jJ20lhsWh4CKPEMBIv2J/4+AsHQd144tACjShgJC/RdtggRExDnpOm7ku0iMCgg0Iv1w2MdIGAAIlaFA4dWwP3NwZbntuGRhhcZX8fdn+78iYbGO244bACAkQyGhph8k5GPqus596JxRqDUFiv70Y1ncVU5YGEDoQ4bN/5rwmp85wtw2btQfRwN48bsXXrpTQINe1rUWmnxZ0HR6w6eWmdlKU2/QOROE+3fuXnzzTiHki/PR/nZCuMryjavEMPd03jrT2HKT12Wnlos2X/T50c62bqrNyVnRVHVRlsLs8sLtpAGWy6IptW2PG06CqqqLqgaHl/P15OAA7TrLSna6AV1X9fxi0VVV7AeEyOXiaFa6bIZBUhBBXdU5L8oi6KU+dBdnR8d0UBVl23UgwK7arDrRBLa2lpez08VqsbU3QemapgVhBZBvVvP1koZpVTdtU2DTnma+dFw2hcNga+/W6en5fF0noZc1NbNsH6TLy1VbbXLpqIW66qDr+HxmPB9YqmzdTKael7dl1+aZE9q7fbPk6u2b170kaeqibSwqqsrC6W6BrtlsyvHWuO8vTk/1bMbSrlerpu5c24iIw6osHYitysouLl2+7E5jm2c180+uc3MOkEUTMmBnQYBEgAQEwQKgiEEeRM3daVTV/OJddb4yFpQDIIBA8SB2W0MaJX7khVoBOwCCq+toFIJlqBu3WLfna7vKVdtpFnDiH83b9n/yXz6MrvvFfw6wuHVzfFY8W9bfNq5ChNiMJtEnO9HjQPc/FkURzruL9/kXi/qwsYVCnfi7B72no+CuJv9780nHzaz46rT476JbImBsRge9p5PoU0Xm/9eGOOmy5v1J8dWyPmxdQ4iRSXeiTybxZ4HqfXyWxebt+Wn5bF6+bVyJiKFOJtGj3fgXge7/2bXCZfXq6+V/tK4c+tPHo3/zdIh/IRK7qN6eFH9Y1cci7KtoEj/eiz+LzPj7n8DiVs23Z8XzRfXOcguAsTeaRA/34qdGRR9fISB5ezYrX1yUrxpbAEKg+uPw9kHvH0MzvPZA/Lvjb+0XJ1JExtNlWSERiBCpKzvVKNkeT4bQ5kdH760VpTWKdYJE5LruSkRG2qgP0vEPYjNFyg+8uqwYBFAJqP2DncCPbLO5mM2tY8eWWUBAGc0CyIxEH1RoAGxbAUKkKI7b+mrxjYAoLIrQOSGFjh0IICkQRiSlSISdAwAhIkJw7K6uLLiSfyOiUvpKmsfsSGm2lrRBBGetiBApRWCdRTL0UWouQIqYnQhqrWxnSSlhZmEkUqQA2PEHsd536nckQOcsIHmeF/fHSc87O/rm8ee/PvztlwW01oFSClGsdQJAVzeBETjHRJqQrXNKa2tZK5KrDW6+6gLQiMDOAamrHW8E+aFiH+Bv6xcXZ9XeP0f/9O9emPi+1zGyfFArehociHWi2e0Mus8f+Y7d87fdvDB1C20HAHYcu9s7dDDxgXC5bpZr3pRStaCIGIDZBUb6MW4NVJp4juH9ZfvmxC5zADS+QaN5GJZ/BMD3k/EvO3NLAAAAAElFTkSuQmCC)

Now click on the arrow icon on the top left of Inspect Element box.

![image.png](data:image/png;base64,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)

Click the top-left button. This will enable the HTML selection button. Now select the data on the page which you want to extract. In my case, I want to extract the total number of cases in the world.

![image.png](data:image/png;base64,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)

The selected HTML element tells me that there is a div with class “maincounter-number” which contains my data. Let’s try to extract the data from beautifulSoupObject. The find_all() function is a great function that helps to extract all HTML element that contains a given value. It takes an HTML element along with some attributes that tell it which class and id of div we need to select. Here it is visible that I need a div element with a class attribute of maincounter-number. Now let’s search it. We will store the result in a new Variable called mainCounterDiv.


```python
from bs4 import BeautifulSoup
import requests as request
 
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
 
mainCounterDiv=beautifulSoupObject.find_all('div', attrs={"class":"maincounter-number"})
print(mainCounterDiv)
```

It provides us with a list of HTML elements. Now if we look at website data and mainCounterDiv data we can see that the first data of List is the number of Total Cases of Covid-19, the second data is the number of deaths that have occurred and the third data contains the value of total recovered cases. One problem is that the find function is returning the List of HTML elements, however, we need the text, so what to do. We can use the get_text() method of BeautifulSoup. It gets the data that is inside the HTML element rather than getting the whole HTML element, We will now create three variables and store text HTML elements in them. Let’s see how to do that.



```python
from bs4 import BeautifulSoup
import requests as request
 
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
 
mainCounterDiv=beautifulSoupObject.find_all('div', attrs={"class":"maincounter-number"})
totalCases,totalDeaths,totalRecovered= mainCounterDiv[0].get_text().strip(), mainCounterDiv[1].get_text().strip(), mainCounterDiv[2].get_text().strip()
print(totalCases)
print(totalDeaths)
print(totalRecovered)
```

We have used .strip() function as well. This will help to remove any whitespace (if exists) in the HTML element. Upon printing these variables we will get these values.

###Scraping Table using BeautifulSoup

Now let us upgrade the task a little bit. Scrolling down the web page, you can see that there is a table, let us try to scrape that.

![image.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAw4AAADzCAIAAACgxNZAAAAgAElEQVR4nOy953dbWXYveG5AzjkQBJgzqUAqVklVqurq4G6726Hfe2t5tcNf4H+hv/mDv/ea5Zllrxm7x+OZfh53V3WVq0otqZQp5gCQBAiQyDnHe3HvPe/DllBoiqQoiRIhm78PWqR4AWzss88+++xIYIzRKU5xilOc4hSnOMUp9gPd+sm3Hfin//f/pynyha/BGGOMCIIgiH3+Kgj4yoVzZyfHpFLpMRJ6LMAYC4JAEARJvvhrniAwsBgBk/fj8luBIAgnTkMLwJPOIUYQBIqiTpqQl0BLqDpc+PcAWE2SZCes+x50lEy2Axa6M2k7CC2aO0c+36Et08kaqWO3yVGAn4FoeZWKhYJaoznKizmOY1hWLBKJRKJ9H+hkjmQyGZ1O15ki1Y5Go9FsNuVy+QmSWqvVMMZSqbRD2JXL5dRqNU3TL370zSOZTFoslpOm4uVQKpVIklQqlSdNyEtAEIRsNms0GjtQqzAMw7KsTCbrEJlsR6PR4DhOJpN1yOY9ChiGqVarer3+pAn5FpVKhSRJuVx+0oS8GB2rkRqNRq1W66hlfSlUKpV6vf7tDucF4YjKCGOMBQHsxDdG3ptC66LwTuDEST1xAtrRUWsHLrd3C53DvZeC8M5qmxNER22Wo6PTaH6H2NjJGuld4eFBEAThW7/iy36Zd1RzvUNrduKknjgBe9BR9HQUMUfEO6T33wmc8vN40YHM7ECSDkLHkvqfYJv8nql0ilOc4hSnOMUpTnGKPTjOEHsrE/kY3/PtoGXzvovEv2Wc8uoQnDLnFKiDNWH75f5w8jrnK3QOJS0cnY0njlONdFw4NlOJ5/lms4kQEolEL1WugjHmef6k8iIxxgzDtOSJoiixWNz6055yOSAVY0zT9FuWPIwxx3Hw0S2Ovf26DI7jgAyEEEEQYrG4nTkcx7Vn+mOMm80mSZJvaHGBGIlEghBiGKadmLcPnudZloWfCYKgabr1rSHVpn1TAK/gsZMh9xkZzWYTyOB5XhAEkUj0TqhU2AI8z4O22fMn2LY8zxMEQVHU2/xGQBjHcQghkUi0b0r1m94XB4HjOFDRAKlUukcgW5tXEASO43iepyjqlUWi2WxSFPU6W7JFBkLohZTALoPV3/dJWBoQiVcmCdYOSEIIkSQpFotbn9Uitf15lmWfl9K3AEEQWJZtHW00Te9bhvW8doL/hLLTzi/9e2s4nr3KsmwsFguHwzzPu1wuu93eMjheiHQ6XavVXC7Xnv9/OwqOZdn5+fl6vQ6ljFardWxsDP5Uq9VyuZxKpdI8KwwUBCEajXIc19XV9fZbIYTD4WKxCIyKxWIOh0NzaMXim2BgJBIJBoPNZhN214ULF1QqFfypUCik0+mBgYHW53Ic5/P51Gp1d3f3sVOCEEqn01tbW9PT0xKJZGFh4cyZMwqF4qCH36g4YYxLpdLi4iJkVorF4qGhIavVCn8tFoulUslms7VUVbPZ3NnZkUgkTqfzBJWRIAherxch1Nvbm8/nS6VSb2/v4YLdIYYUx3GRSCSVSo2MjKjV6vY/VavVYrEol8tLpRJN0xaLZd+j8Q19EZZld3d3Y7EYTdP9/f1ms/n5T8cY7+7uajQak8l0FDKOi9RoNOrz+dCzJgLvv/8+XDMwxsViMZ1ODw4OEgQhCEKhUPD7/cVi0WAw9Pf3t/b484QdlIOCMd7a2nK5XEql8pXpZxhmZ2cnGo1ijPV6fV9fn1ar3ffdMMaxWEwsFnMcB1IBX60dgiBEIhG5XG42m1+NHoQQz/M+ny+ZTIKFYTAYRkZGZDIZ0BAKhVQqlV6vbxHJsuzCwsLU1NRbLjvFGNfr9eXl5VqtBtZhd3d3f3//80/m8/l6vW40Gts5ViqVYPXfrWrZN4pjMJUwxsFg8NatW5FIBGPsdDq/+93v6vX6fD7P87xer4fLgU6ny+VycMmrVCpg45tMpt/85jdKpVKhUJRKJYqiaJqWSCRarbZUKhEEodPp3qh2BlGOx+OVSsVkMg0MDEB5rVKpDAaDc3NzFy5ccLlc5XIZY6xSqTY3N1mWNRgMb9lUwhhvbGzMzc19/PHHOp1ubm5OIpFwHFcul0UikVarzefzJpOpUCgQBKHRaBKJhMPhOPZraywWm52djUajEolEJpPpdDqNRiOVSrVa7VdffVUqlUwmU61WYxiGpmmtVjs3N9fX1/cmTCWMcSQS+dd//VdBEKanp3/729/29fUJgpDJZCiK0uv1lUpFoVBwHFer1XQ6XblcVqvVb6joF2NcqVTu379fLpdZlu3q6iJJslarSSQSuVy+tLTk9/u///3vy+XyYrEoEokkEsnS0pJOp4Mn3wRJR4EgCE+ePInFYj/5yU9SqVQkEjEYDKA6VSqVTCYrlUpmszkcDhsMBoqiisWizWbrhItmqVR68OBBIBAgSXJ6epphmFwu12g05HL57u6u1+udnJwsl8twhqlUKoqiKpWKTCaDul+tVqvVat9EFX0oFPriiy9isZhEIrl48eLVq1ebzWa1WlWpVGq1OplMQvcNr9fb19enVCozmUyz2dRoNDqdLhqNWiwWjuOy2azJZMpkMlDtb7FYjoXniUTi4cOHqVRKoVDI5fLe3l6EkEgkUqlUd+/ejcfjVqtVpVJVKpUHDx7Mzs4SBKFQKK5evXr+/Pl8Ps+yrEqlAhkGCdFoNOVyuVwuy+VyrVYLPxMEYTabCYJ4/PixxWJ5nbMWDvv5+XmlUkmS5KVLly5evMgwTKPR0Gq1crm8UCjUajWxWCyRSD7//HOHw6FQKJaWluB/bDZbs9nMZDIYY5PJJJFI5ufnZ2ZmXoeHGONAILC4uJjJZBQKxeDgoFgslslkGo2GJMlf/epX09PTFy5cyGQygiAolUqpVPrFF1/09PS8fZuDYZiFhYVIJFKr1axW6+joKEmSUqlUr9dXq9VCoSASiWQy2eLiYiKRuHbtmkwmq9VqoNV3d3eLxeJBJvJ/TVA///nP4ad6vX7EgwRc3zRNg67hOG5+fp7juJ/+9KeXL18mSVKtVq+urt6/f399fb1arQYCAbfb7XK5Pvvss3Q6HY1Gv/jii2Qy+eWXX5pMpnv37hWLRYTQv/zLvxSLxVAoFAgErFbrrVu3isViX1/f8ZpK1WpVJpO1VI9EIpmZmenp6clkMn/1V39Vq9Vu3rzp9/szmUyxWHS73TRNl8vlmzdvzs7OomehX6fT+aZNJfA8tzy3GGO/3x+JRJrNJk3TpVJJp9PNzs4+evRoa2tLo9H827/9W1dX169//Wuv16vX63/5y19evHjx6L69fdEeUYX/cTgcly5disfjH3300YULF+7cueN2u30+n1KpfPToUTqdttls9+/fv3fv3tzc3NjYWCgU0ul0TqfzWBaxVqu1N3mKx+OBQCAejw8MDKysrExPT8/NzX355Zfb29uCICwsLJTL5e3t7d/97ncajebOnTsmk+kYe3uUy+WWKgHz9NKlS3K5XCaT/emf/uni4uLc3NzOzk61Wg2FQsFgkKbpZDL52Wefud1uqVQKWqmvr+9tWh6NRoMkydb1URAEt9udTCZJkuR5nmEYpVJ58+bN+fn5cDgsFos//fTTwcHBv/u7v5PJZIVC4d69e+fPn3/LphLGuFarKRSK9jBHNBpdWlqy2WzZbLa/v9/v93/11VdLS0u5XK5QKHg8HrlcHovFarXaxsYGx3HpdHppaalUKj18+HB2djafz3d3d4Mh9TrYs0kRQslkMpPJjI+PT0xMaDQahmFu3bo1Ozsbj8cNBsM//MM/7Ozs8Dy/sbGh1WrT6fTXX3/t8Xh2dnacTucvfvGL8fHxaDT6T//0T11dXf/8z//s9Xrz+fzg4OBBHewOpw1CUS3aurq6rl+/vrGx8eMf//iTTz75zW9+43a7NzY2SJJcWloqFAo2m81sNieTyUePHn3ve9/7yU9+otfrSZJkWfaLL764e/cuGExff/317Owsx3E0Td+/f//+/fuRSESn092+ffvevXs+n89qtVar1VKpNDw8/Lx353CaoZkc/Fqv11Op1Ojo6M9+9jOKouLxeLFYnJube/z4caPRkEqljx49+vrrrzc3N0mS3NzcjMVier0+FApls9lbt27ZbLbNzc1f/epX29vbSqXSZDItLy/PzMy8lFZkGAaibPArRVFDQ0MjIyPJZPLP/uzP1Gr148ePV1dX4/E4z/OLi4upVMpms/37v//7/fv3o9Ho+Pj4kydPZmZm3oLZsUcjyWSy8+fPW63WfD7/l3/5lz6f78GDB6FQSCqVrqysfPbZZ4lEgmXZaDQaCAQ4jlteXr57926pVDIYDOFwWK1WH9dle8+yvnNgWZZl2WNgBMRE1Wq1SqWSSCTj4+Plctnv93/wwQcajebTTz+FCxykRJAkSVGUyWT6i7/4i7//+7+vVqtnzpwxGAzd3d1qtfrP//zPc7ncl19+GQ6HC4XCtWvXXp+8FwLcyBBDgds/bEKz2Tw2NjY5Ocnz/NTU1Pb2dqFQkMvlr2l/vDIwxkNDQ7Vaze/3QwQnk8nMzMx4vd5Go2EwGPx+f71ez+fz6+vrExMTb0I02y2e5eVlq9X6ySef/Pa3v00mk6Ojo4IguFyueDze09PzH//xH9ls9k3XiNrtdrVa/c0330Cq0IMHD9577z2e5wOBwNDQ0PLyskQioWkaol1dXV1vlBj0LB8ilUqVSqW//uu/3tjY8Hg8o6OjEolkamoqHo9fvHjR6/W+Bc4cESRJnjt3DgIKCoVifX2dIIjr16/fu3cP5Mfj8Wg0Gq/Xq1arZ2ZmOqGfIcMw4XC4UqnodLp0Or29vQ3n0w9+8INKpQL29Pj4+OrqqkKhUCqV+Xw+FosNDAyEQiGZTHbp0iWPx1OpVA6K5rwOHA5HMpmEUOzIyEipVOJ5/uLFix6PB+7xH3/88ejo6O7uLkmS33zzzXe/+92xsbG//du/DYfDYA+RJCkSiXieN5vNExMTIpGIYZj2vKJXRiteBveuSqXyN3/zN/fv39/Y2Dh//nw8Hp+cnGylr1ksFolE0tfX12w2wR7VarWVSgU8XqOjo6BwKpXK2bNnY7FYMpmkKGpiYkKr1dI0vbu7a7fbX8HC2wMgmKIotVotCML6+rrJZDp79mw+n49Go5AIsby8bDAYrFbr2bNnwZfzJ3/yJ7du3fL7/RjjycnJ/v5+iqLK5fKxNJNsLUSz2VxcXLx8+XJ/f/8vfvGLc+fOmUymH/7whxzHzczMZDKZ+fn5VlbTCYLn+XQ6HQwGwd21vb0tk8mmpqYcDofRaBSLxRqNpr+/f2try263G41GCN69VBbNfwUcwwWRpmkIrq2vry8tLT148CCVSlEUxTBMrVaD/NZGo5HL5arVKrxEoVC00vQIgqjX65CfC55Mg8GwuLgolUplMlkqlXoLnbWIZyBJstFo1Ot1sO3AGe52u8Gjjk46V0OtVo+MjEDuC0VR9Xp9Y2MDXPqDg4Nra2t2u12r1a6vrw8PD785UoFXNE0LggChSbi5MgwTj8fv378vkUhaLEVvhmmt9/zkk0+CwWCLDDg4rVarzWZLp9Mcx/X393u93rcQM22RBDmSlUoFXICQMxuLxVZXV/P5fMtBcuJ5P0CAxWIZHh5Op9Mg9vl83u1263Q6lUrV3d398OHDK1eu5HI5sIBPlmD0LC0MfCHxeJzjOEi3ajabzWZTJBLBYQ+1GhRF9fb2ZjKZbDZrNpsVCkUqlfL7/SqV6vVP8X1RLBYVCsWVK1f6+/t3dnYKhUKhUPD5fBKJRCwW0zQtl8tbKbRgBkEMHWzQfD6fz+dJkjQYDIODg16vd21tLZlMJpPJer3++uS1iyhJksViEbxiLaZB0A2ixh6P5+HDh8vLyzs7O5ubm7DlLRaL3W5PJBJra2u5XA5uxWCgjI+Pcxy3vr6+u7sLwdzX90nAMe/z+XZ2dhBCSqUymUyCy7NQKKysrIDnDB6uVqscx0mlUpFIJBKJBEEYGxtTqVSrq6tLS0uRSMRutx+LT7S1f2maZhimUqlAoQ/serfbvbKy0m6In+xOh0+v1Wrb29ssy1qtVpfLRZLk8vKy3+/nOI5lWYVC4XK5KpXK0tLS9vY2OKVOXEF1FI7BqwQ+yWQy+fjxY4yxzWabnJx0uVyhUEgQhL6+PpPJtLi4CFk+MplMLBY3Gg2IWUCSXTgcrtfrkA0nk8m6u7sXFxdv3LgRjUbD4fAnn3zyRn3+UMml1WrBuPZ6vSqVymw2d3d3Q66rQqEAz5lKpZJKpSdSaQUqTBCE4eHhQqEQj8f7+vqgaIVhGJPJZLfb5+bmhoaGSqXS8vJyd3f3GxJ0giBa7sPHjx+vrKw0m83h4eFQKOR2uyuVit1ur1aroCjVavXrhzkOglQq1Wg0ZrP5ww8/vH37tlKpnJ6eZllWLpc7HA69Xu90Og0GQ29vbywW2zel8XhBEAQkbRiNRjD3BUGYnJyUSqVwLGm1WtDskET15jhzdKhUKoVCMTo6CscPuAbVajXLshqNZmpqyu12T01NQZDu8DKCtwOMcbValUgkP/vZz9RqtdvtDofDWq0WLvFKpRKyqQqFglgslsvlVqsVctQggQbMFJlM9oZOAoZhNjY2stksQqirq8vlcoXDYbguwiUQ7ocajQb8W4FAIJvN2u323t7enp4ej8eDENJqtfV6vVAoWCyWQqGQz+cDgcDY2NjztS+vAK1WK5FILBbL/Pz84uJiMpm8cOECwzDBYDCVSnV3d2u12vHx8QcPHoCFNzU1JZPJ1Go1RVFyubxWq1UqFbVa3Ww2LRaLSqUC60SlUgUCAblcDsmpFEW9/vwoiqIoigoEAolEgqbp8+fPi8XicDgsCALkyzcaDZ7nlUqlWCyG0KHNZtNoNJBsCv5djLHFYslkMrlcbnBw8PUZCIRBstTExEQ0GoXEUJvN1tXVFQwGId2HYRiDwUAQhF6vPylfLEEQkJxkMpnOnDnTygMGB6fRaARGgfUJmlMQhFqtZjQa91RLnOIYcpUQQgqFwmazGQwGl8s1PT1ttVqdTidCSKvVnj171ul0Qg5Hf38/nGFGo1Gv10ulUqvV2t3dLQgCuAHMZnOj0djd3S2VSh988AFCiOO47u7uYzRN9uQqPeUCRWk0GofDYbVaIR/57NmzOp1OoVBoNJru7m74Kxy9JpMJduNxkbQvnk+DEIlEBoPBYDAYjUaTyeR0Oru7u3me7+/vt9lscrlcpVL19/ebTCabzeZwOF7/JHg+VwkgkUhMJlNXV5der282m+fPn7fb7QaDQRCEnp4eq9Uql8vHx8cNBoNOp4Pb/GtSAtiTqwSrZjabbTabSqVyuVxDQ0MQixwbGxOLxZAmZbFYTCZTb2/v8ToS2jMDAGBz63S67u5uSCl1Op2Tk5NwMBuNxu7ubqVS2dfXZ7VaYRFVKtXbvLrtyVVCCInFYkjh0ul0Nputr6/PYDA0m80zZ85otVqFQqHT6QYGBrRabW9vr8FgeGuktrAnVwlCnFAPJZfLlUolLD14DUdHR10uF/inzWaz1WrV6/UajQYesFgsYCFNTk4eS/Tt+U2q0+ksFoter+/p6Zmenu7v7wf7cmRkxGQygekmlUolEonVah0aGhKLxYIgfOc731Gr1V1dXeAEdTgcfX19EHIaGRmBu4fJZHqp1ODnc5UAkO+s1+t7e3tLpdLo6Ojw8DBYGxqNRq1Wi0Qis9kMsZgzZ85MTk6q1WqlUmm1Wnt6epxOp06nEwRhdHQU9jhJkr29vQ6Hw2w2cxxnNBrHx8dNJpPJZHpZr9KepBZIQzYajV1dXWfPnh0bG7Pb7TKZTCKRDAwM9PT0SCQSs9nsdDqtVisUnNrtdovFYjQa4YVjY2P1el0kEn300UdSqfQVYoJ7cpUAcCmyWCw9PT1wDr733ntarVan0zWbzZmZGUEQBgYGurq6LBaLRqM5lljkC/G8RkIIwXHmdDptNhvHcQ6HY3h4WKVSgQU5OTkJvLJYLBaLBcju7e01m83HeMb958hV+rbaM5vNHlEVsizLMAy4lI+XJkEQ0un0gwcP1Gr1Bx98ACGM16ntfB6pVEqv13fgeMs9aDQaYOafIKnVahVj3DkTNzOZjEajeQtK5yiIxWJ2u/2kqXg5FAoFiqLercIW0Akmk6kTKu/24O1s0lqtls/nzWbzS0k+ZDWc7Lztl0Wj0QCH9EkT8i0g1eG4LntvFB2rker1erVaNRqNJ03IK6JSqZTL5c6yGMA1ff36daVSKRKJdDrdSVN0ilOc4hQnCblc/u7eyE9xiv8c6DhTSSqVvv3ujieO08HppzjFKU5xilN0Jg40lfAzIITah3scBGiF3v5wqzC1vRjqTYNl2WazCSXiLMvyPC+RSA4nHnrhA50vNZLldQC9XkiS1Ov1pVIJ+m3KZLLDy0ZaTAY6X5PUVud7SF6BzKT2Pv2HEICe9e8/6OHWfIkjCkCLGCCAZVmomn59Ylpy2Pr3hauMMW40GgghKOWDFJ+jc+ZNC1Jrb+75FOiNBNlIgiDAZIlDojYtyYdfj0WoXkg2elZB2fp/SAWAOC/LspDw/sIFegt7FurCgDaSJGGixVH0CZSItwiDXQDbobUjYHDEQRK77/q2A7pjQHoc0An9e1/IN57ngf7W1KYWbW86VMfzPPRlhbbaLMtKJJIXfmhroduFp10NviZJjUaDoiipVAopNQcNAAHs2TIIoYMm57QofB3y2sEwDGTQQ6cr0NsvXO6WILXoaW3D49o4oC0FQZDL5TDIBcTyiNrypcanAP/h+db7t581r/ClQAZomobEQZiR9fyyHnYqZ7PZYDAIXZH6+voO+TCGYba3t7e3t2Hox8jICHTjMJvNHo+nr68PGs62EjP3vPwYNR1Eu6HUqFgschwHHWYPWgzo77y4uFgul41G49TUVHuXQqKtc/8hP78CnRzHBYNBkUgEHXuj0ShBEEajEbqS7PuSer2+ubkJHVlGRkYgqxG3zZI8ys97vnu1WhUEAczKSqUCiSyHSPn29vbW1la9XqdpemxsrK+vD9TK8ytbrVbdbvfo6OjW1pbRaOzp6dmz7ns+AogBWec4rlKpkCQJpXYHHSfRaHRubg4OifHx8aGhofZVbl+jcrkcjUbVajVkv0Hj2kOIgTIrqDbnOK5UKkH910GcEQQhl8vdvXsXJruZzebz58+3knD3MOcg4Wl5Fg9qudT+V4Zh7t27d+nSpfaqNJ7nofKcpulqtVqv1yUSCcSy931DQRAWFxdDoRAcn5OTk729vXD0oqMJ0vM0E88Nu2h/wO/3Mwyzp3lxo9GoVCrQTKhYLMLYHLlcfpAQwp5dXl4uFAomk2lycrI9u+V492yLNoQQNEkCfXKIBRMMBjc2NqrVqsvlGh0dhRRajLHH49HpdCRJ5vP5np6e1dXVycnJ9iQYoq3vUT6f93g8MzMzB5VJ8jxfrVbhmIHNC323D7ldYIwzmczc3NzVq1c5jvvmm28cDsf09LTf7/d4PCMjIyMjI3uW7yAZeCketsBxXKFQgMq4crkMhURqtfqQk5Jl2UAgUK1W+/r6wuFwNBodGxvTarVQeAs9+fZd2aMoQCCpXC5LJBKRSFStVqFwRKVSHaSEeZ5fWVkJBoMwDNRms50/f74lDy0yeJ5fWFiA1X9ldrUDY1yv10HxomeiCPXFhyw3HBk8zw8PDy8vLzebzQsXLlQqleXlZcjZb022aSfyFbZMtVptNptSqRSaXyCEYIrDQYRFIpG1tbVqtQrl84ODg61ak4MUCLywXC4/ePDg448/hg4X6FkuYyqVcrlc29vbIyMjrWj1ESUWZABs0Hq9XqlUpFKpWq3eIwP7CwTHcYFAYGVlZXt7GwrRe3t7D9FcwWBwdnYWbgyxWAzspHA4fOHChUePHpVKJagjs1qtkUgkHo9DaaXH4yEIAg7d47KWWiYzzFKFbisHnT0gTPfv3w+Hw3K5PJFIIIRAd8B4Co1GA5PXbDab3W6HVuM6nc7hcORyuWg0KhKJent7NRrNy9IP17uWLwScFs8vTwswrmthYQE8B1CvyzBMIpGQyWQDAwPlchmsqNHRUalUurm5WSwWR0dHoX9gPp83Go0DAwN77nDALvBANJtNGEFzSLb+zs6O2+3WaDQY40QiodVq8bOBVoODg2AeEQQxMjLidrtv377N8/za2prJZEokEjabzWQyhcNhyFF1uVx7vmzrDgRrRxAE6KODeJtIJGZnZwcHBwVB+PLLL2GMkdvtlslk8J9bW1vQyq9QKNy9e7e3txf2FaSOWq1W6FhjMBicTmf7mdRiC9zXgZjDOVMoFB48eDA8PCwIQiwWg7KsQCAglUph4ko4HK5Wq11dXUajMZFIxONxjUZjNBpLpZJWq4X6dp1Ol0gk8vm8y+WSyWSRSKRardrtdoxxOBw2Go2Dg4PQVYiiqG+++WZ8fLzdVGoxsLWgrdvkQUK1traWyWRgjlC9XofBJqlUCkpmSqWS1+ulKGpycpIgCK/XWyqVnE6nWq2ORCL9/f3VahV6Eu7u7iKEXC5Xs9mMRqM0TSuVSjjCoeg1Fotls1mPxyOVSvcUc7VYDSO3wd9w0BkA6vLJkyeBQEAikaRSKYIgzpw5EwwGG42Gw+FQqVThcLhUKoHCgYEter2+q6srm83CpLDBwcH29t8HAbcBaIMNcohMplKpubm5TCZDkmQymVQoFKB/ZTLZxsZGX1/fzs5OLBb76KOP1tbWBgYGOI7b2toSBGFqaoogiI2NDZZl7XY7x3Gzs7NQPnk4ebDWMKB3z7zqPUin0998883Dhw8nJycZhrl582Z/f//ExMTCwsLCwoJIJBoZGYH2zcVikWEYs9nc1dVVKBR2d3elUml3d3ej0UilUlDN5HQ6X2FYR4tmcB8CSw8ylViWhW77crncaDRubW3Nzs5C1duTJ09YlnU6nXq9HpqnVG5aroMAACAASURBVKtVgiAGBwdhuE0ymTSbzb29vdC7v1Ao2O126Ce0L0mwvnDvOmR8O8aYYZhMJuP1eh0OB0VR8/PzCoViZGQEIQTXSNgXX3zxRalUmp6e3tjYoGl6aGjoNVNv2482WHGwTg4SRRhsMjc3B+Xbc3NztVrNYrFUKpXf/e53Y2NjY2NjIpEIdGCz2VQoFFC3Dm3qXC6XQqGIx+PlclkQhP7+fjD0D6IN9ExrJPPh2yQaja6vryuVSmi+CK0ootEo9HLLZrPVarVcLuv1epvNFgwGXS4XQRB+v1+r1d6+ffv69euJRCIYDCoUit7e3lu3bqXT6ffff9/r9Tqdznq9vrOzQ9N0b28vx3EwQ5AgCCjePIh+9CyyAZIAp3M7/Qd6lViWTafTMMrt8Lk50BxZLBZDe+67d+9GIpFSqQQ2CoyOqtfr0WgUtqXFYrl79+4nn3xy+/btnp6egYGBQ978lSEWi6EL2eEO80qlsrm5+Qd/8AcOhyMWi/E8D760QqEQDof7+vrW1tagRUetVguFQrVaLRqNVqvVYDAIfQdggN0rl2WB3xs6XkBnzn0fazab29vbWq32ypUrMPFKEIRQKJTJZMLhsFQqXVpaQgiJRCKNRlOr1Twej16vv3nz5o0bN7744ovh4eF8Pm+1WvdtjQOGGlS9Hl7VCIXBly9fpijql7/85e7uLthJXq9XKpVms9lCobCzs5PP5yUSSb1ehyMQ2ngEAoEzZ87Mzs7qdLpGo6HT6fYdMwLOW+DJ4QE4giCsVusf//Ef8zz/j//4jzCOptFoiEQiaO8Ea7S9ve10Omu1GkKI5/l6vR6PxyORSDqdjsVisFcVCoXD4dj3I6RSabVaPQox0LOE47h4PA6syGazEomkWCxKpVK/30/TdLFYtNvtOzs7YDxZLJZkMtnX11ev12FWA5z9yWSyt7f3zp07AwMDUqkUmhRvbGyo1erZ2VloenSIDQTrCCPNDy/OguoenU7HsiyomN3dXaVSeefOne9+97v37t2TyWThcFipVMIN1WQy3blz59y5c4uLixKJJBqN5vN5i8UCAxPS6TS0/B4eHgYlSxBEuVzWarW7u7vg6zqEja09e3gADrrqv/feey6XK5FIwJ6FvZBIJAwGQzAYhEtqvV4HP9bOzk6j0YC7GTTFkUqlRy9bIwhCJBKJxeJms3l4ZCEYDDIMc/36dYvFsrOzI5fL7969K5FIRkZG6vU62I5Qxg/jAh89egQHuUgkMplMwE+v13vlypUjhsNgrRuNBnDvkCfhygoHAEEQGo2GZdlEIpFMJluzCBuNxurqaiaTsdlsYHEmEgm4/WcyGYRQIBCAli4sy05MTLxa6R90AYAu5IcoZ+hKA70VEEJisVihUFQqFdhQLadFMpl88OCB3W7P5/PValWv17vdboPBcO/ePZIkZ2dnRSKRxWK5efPmT37yE6PRuO/yHXHL0DR97tw5i8VSrVbfe+89MCsjkYggCHAttNlsGxsbVqsVHNjz8/M7Ozsul8vv9x/XUCDQ1ehZesC+z4DxB2oWnoEA98bGhkqlgt5aEMcMBAIejwdm0VQqFZZlYaHT6bTdbodems1ms1AoXLly5YXFs63Q1eHBQRAAjUZTqVSgpxeMhQUPYiQSqVQqBoNhc3Nzenr6/v37YEvduXPn+9//PkVRgiBsbm42Gg3wHcCe4jgOupH5fD5opgrV7ouLi3a7vVgs1mq1y5cvv5AqqO5/PgB34MqBcQ19qA4vlWy1ZzQajTqdDmQRmklAaw0IySUSCbfb7fV6odNrMpnMZrO9vb1vqK90SyMcHr/neZ7jOGhy3d3dDVMq0+l0o9GIx+OQRZHP58vlcjAY9Hg80Wh0Y2MD9gZ0h4Mw7SvTCTINORCH8BliqBqNRq/XQ7tViECxLJtMJguFAkKoUCiUSqVqtbq4uAj3qidPnkCT30QiAdtg3zeH8wOcWweF3lvUQgdFk8kklUrD4fDq6mosFgsEAltbW4FAoFKp8Dzv9/t7enpkMhn0HTGbzUNDQ5lMhmEYnuczmUy5XIbLx/PvD8SQz3C4bEDE0GAwaDSabDY7OzubSCRCodDKykoqlYJu3YlEQqlUgl8BXBq9vb0Mw8A450KhAIHafV2PezhzCCUIITCSvF5vd3e30WhcXV2NRqO7u7vr6+vhcBimDYJFXq/Xp6amJBJJLpfDGMdisfX1dYqiwuEwTLUDZ0+lUhkbG4ORYfF43OfzbW9vLy0tjYyMDA8PH6J2SZIEsT9KHkClUvF6vbVabWpqKhaL+f1+IABufpOTk1euXIEppFar9dy5c4VCIZPJqNXqxcVFn8+nUCg8Hk8oFAqFQj6fL5/Pi8Vil8tVLBa3trYikQi0nG40GoODg1ar9RA2wrofZc/yPG+1WsG/azAYcrlcNput1+vQc7zRaBSLxUqlsrOzs7W1FY1GYUBYa7nr9fpBnubXpK3RaEDGIbRWgnuL1Wrt7+8HPwo0sIHJ1gzDLC0tjY2NXblyRaPRpFIpmKcL8Z0jEkY8y9Z64ea1WCxXrlxp2QGwMWdnZyFjEl4IekatVo+NjcHgjkQiMTY2ZjKZYHoJBAEgesAwzMuw8Fu05BO4etBjYrG4v79/eHgY7m8EQVgsFjCU4YIKj4EnYHh42OVybW5uwjgjuN5vbGyUSiWj0TgzM5PP5yORyFFIOkRECYKQyWQKhQKGdG1vb0cikWg0ura2Bv7+dDpdq9VsNptEIoFoSb1eBzfJy4rcQYCPPlwU4Y43NTXldDrhc2GoeSAQSKfT7ddCCNNPTk6KRCKfz+fz+bRa7ZkzZ1KpFExR7O3tHRkZCQQCpVLp8K9APJtdBsw8/FvAhZ8kycHBwVqt1mg0xsbG5HJ5JBJJpVIqlers2bMsy8ZisVwuB86qQqHQ8l35fD7Yzul02uVy6XQ62FOFQsHv94+NjXV3d+/u7oLZ19vbC7fQw+lvKfn2npHfsn3f12CMK5UKNKqGftCHfABN0waDYWVl5ZtvvtFqtWtra93d3TDKGyjTaDQQsIdEXZPJ1NPTA41BYQbN4Tw9OvDv4ygvkclkKpXq1q1bdrs9Ho8TBAGeeaVSmcvloEkmLAlki+ueAZy0MF6qu7v7paZCtiIOLb8lRVHQWu2gl0D/SejuDwE4s9lcKpW6urpgdAZ0Gy+Xy16vF2MMze7gEg+RxFgsFg6HTSZT6z1bNBydXQghSBMhCAICfEAYQkiv16+srExNTRUKBXDtwPMkSbYuMRRFWSwWhFC1Wo3H49BAucWT1g9HN53L5fLc3BzEvC5cuEAQhE6ngwzNRCIB2U6wIeE9aZpWKBRwwSJJ0mw2S6XSfD4P/XZb27udLUckhiAIlUp17dq13d1duIVDEKp1D+M4DgL54FRodQjs6upaWlqqVqsQKIRJ8gqFAgb7KJVKeDeTyeRyuSDUCwmeewz09nU8+moSBDE8PGwwGNbW1hBCkBJuMpngyAc6YSoR5FxDeBSakn/22WcGg6Gvrw8CjiBaMK4cEqTkcrnNZpNKpc1ms1arQcPGPbS1r/sRaZZKpQqF4u7du11dXdBGXCaTYYzBnw+dBhuNRiaToSgKXH0wMYkgCK1WC72JnU7nCz3B7fw8InlGo9Hn8z1+/Fin0wWDwYmJCYSQQqEAXxSxX+o0LGWxWISe1Eql8oUf9wqKDiGkUqn2aPKhoaFPP/304sWLEL9rWUsAUHEQ4IMPgnguhCcO964dRDN6GWaCVmwdEBhjg8FQrVYbjQbYoK0neZ5v1THQNA0Et8KRLMuCJO+bfvCybGwBzFNQvNCvGJIKNjc3Z2ZmQOcolcqenh6SJP1+/6VLl145cf4VtjZ06AWpQwjB7IRYLFapVFwuVy6Xaz0J/gLosQ6uJpAHkiSBsTzPEweXdrVoeymXgdlshlal4AWsVCrwQcA30BUQBSNJshWkgtdCbGdychI0Nqwybsv6B7Jhu0HiEVS67Ev8Ec/B/U0lkICenh6bzYYQOnxKBmRmFYvFUCgUjUb1ev34+DgEShOJBCh9aJIE6d61Wq2/v99oNJrN5uNt3cYwDMMwgiDUarWjRMTAMLp27dri4iLchsfGxhBC6XSapmmTyQSzhCDna2BgoFgsZjIZo9HocDjS6XQ2mxUEQalUvuy34HkeDPZms5lIJARBgC7PhzCZpumJiQkIKAiC4HK5IHbDsqzFYoE8p0QiUa/Xu7q6JiYmVlZWYJIlZKGCzdTeq14QBPCiI4Sgoe1RKFcqlc1mc2triyTJc+fOTU1NNRoNhmGge7Lf7y8UCpB/o1QqNRrN5uYmECAWi6E/u1gsLhaLcCS0vm+LGIwxhBJeSAlcm0Qi0erqKsb47Nmzg4ODN27ciMViNE2Pjo6C8wNuomAQh8NhmJ8qkUjUajV0Q2YYBvxk7cRA+z744YjjR0Qikd1uHx4etlgs9+7dKxQKU1NTkUhEJpNByNztds/NzYGDIRAIzM/Pi0QieD4YDJrNZhhQijFuNpt9fX0wHYWiKIfDcebMmXq9brPZenp6rl27BiNs93RDhhgx6Lh6vX6UYwy8v93d3ZBiFY1G+/v7GYZpNBrQa/jq1atzc3MwuPry5csLCwt37951uVyDg4MMw9jt9q6uLhhktLm5KRKJHA4HKDi5XD48PAw5Xg6HQ6vVut1uj8dTLpehIX6LBvg4SOo/4p7VarUXL15cWFhYX1+XyWQweiybzcKUBhi+UavVVCpVb29vMpnM5XJWqxVSvmC7HaUTMcYYgpKgT47YhLCnpyebzXq9XkhqVKlUer0eCuhgFIZarQ6FQjAiTSaTXbt2bXl5uV6vT0xMgMsELpM0Tev1+kOKURiGgbm2UPN4FNrQM8cMGEAmk2lwcFCn0w0NDUWj0fbEo1wut7i4CGPdwGUikUgGBwcLhQLEBBBC0BX9iJ+LntUcYIxrtdpLXY9hrIpYLFapVBqNBpLBrVZrNpttmWs8zwMbp6amDAbD0tLS7du3FQrFxMSE1+vN5XJ37txxOp1Op7N9X8CWgdyURqNxdCsExp5qNJoLFy4kk0nwaREEARF/nU4nk8lcLtfCwsLg4GAoFMIYH7KaLwTGmGEYcJ7VarWj21sEQcjlcmjbCwOXwOgxm82tQkiEUKlUWlpaEgRhfHy82Wzu7u4mEgmn02kymXZ2dmDM6OjoqFqtfl6rwIJCzlmlUjli+hr4IHp7e2E6b39/f7lcXlxc5Hl+YmKiVqsVi8VHjx6p1er+/v5arQYZqAaDATLV4DqUz+dbgYLNzU3YUwaDAUZlw4kJ2gAqHvY1lSBMCf+2yqT2xYGmUldX140bN2CTv3D2k8FguHr1KlhC4HSBskaJROJwOGDnf/jhh2BC5nI5vV6vUqn+8A//UKvVHoWzRwT4Ttv9ui+UfrFYPDk5aTab6/U6xJVgMgZYo7A5YXqX0Wgsl8vZbFahUMCIHLVajTGGOR4vRSdIMEyGkslkDMPIZLJDymoANpvt2rVr+XweIWQymeD4Z1n2zJkz4D+H6UsOh6PljbDb7QqFYnp6ulAowGS0dhrAWYp+v971cI6NjIzA+AKSJGEC1Pvvv59MJmUymVar/fjjjyFHuNlsajSaH/7wh1CsrlQqpVLpBx98AIdHsViEOQntxMCStW42R1FbTqfzxz/+MTh+rFarSqW6ePFiKBQCq4XjOL1eLxaLYcCfTCZrNVZWKBQwT6rZbMKJBSOl2jlzkA9gXxAEYTQav/Od78CIgA8//BAhJJPJrFYr5EkQBKFWq+v1utFo1Gg0Wq02m80qlUowx9977z24AsKRUKlUYH0//PBDMMSvXbuWTqeVSqVSqbx8+TJMoYfpHM8vKLiRn/ffPA+Koi5evAhzV6anp6FfP1i6BoNBqVS+9957kUiEIIienh7w0NTrdbPZDClZ3/ve98D1NTw8DJn+JpMJY+x0OiGZHTKcYH6LQqEoFovge2vXp61ga0sIX0i2VCodGxszGo1gwZhMpnq9DkyGAUpmsxlyQg0Gg91uz2azcrkccskhPc5ut7+weVsrFtO62h7+PAAGEbpcrkajATNVwLNI0/TVq1flcnnL6/ajH/1Ir9dfunQJhpq5XC7wssPUd6PReOPGjYMUy56g21EIA9A0DVpXEIQf/ehHJpPppz/9qc1ma7dfRSKR1WqdmJgApQeDksRiscFggBzhkZERrVbbvmWOgj0RLrDpXwiQPUiynJycBBUB6QoQKITHwHmj0+lgZaVSabFYVKvVFosFYwwJ/rAce968fctAFP4omgeGScConHg8LgiCzWYDbkBthEql+t73vletVh0OB9RqvWyz9T10trIRjq4eEUIikWhoaAjqMC5cuCCVSvv7+zHGMpnM4XBArStJkuDFgNsXQshgMEACeLlchpGsMHZsX2ls15btX/AQf3xrTWH5QHmeO3cO9qnBYPB4PBaLBSwHk8mkVqvT6bREIjlz5ozFYvmjP/ojjUbzox/9qNFoKBQKiUQCV3FI8TabzQaDIR6P0zQNESGLxaLT6SYmJvYlCZa+9S8EvveNJ3TWYJPXBNzIIVJGUVSj0Xi+tX+HDDaBIkGwb8ChDcUyrQfewswEoa2vErhzIK+tJSJvc7AJXJTxsyZPrWll7Tx5a4NN2okhCKJWq0GUp33zdOAYAagdA75BvE8kErVf/TtwsAk4bziOg15o4M9r3wvCKw02OURTvyxtUGdEkiRk2rVvhxOcPgSZMQRBQGQBGsO059K+2mCTarW6vLwsk8nOnTu3h4E8z6+urpZKpQsXLrxa93BIvIXKfHDkyGSy9u38aoNNdnZ2IGl6j2MeYiu//vWvp6am+vv795UH2CZwDdh3y3TIYBNwLIGNSFEUODv3NMF5BY0EqeiVSmV6evp593k6nV5cXJycnLTZbIcnsIJjGN4BsmPbb/4vNdiE5/l79+7p9fqhoaG304wa1h0Kd1rupfbqk04cbPKaIAgCykDgS0ql0mPRmG8CMJMSIQT5WydCA/lsciqwCNTfSbELrDT0rK8G2CWdQAx6tu07U5Da0cpGhKve4Um+HQI47FuRFNizr18odCxf/A3RdiyAPB70LDnjuERUKpVOTEzsKzmQgQvhgld78/awOxSaHcsy2Ww2rVb7/ORpcMZcv379kMYQ78qWAVFEzwQbluD1RZEkyYGBAbDAnv+rVqu9cOHCC9tqQC5Ei7aWWL4ySWfPnoWC01d7h5dFuwwQz5KVn6f/P5WpBGh9yQ4/3jpB57bz58R51VEL105AJ6zUEdFRPDw6OpnsjqXtTRAGgeCDPu4VGik9/yatH46L5kNmYUFw5+2T9CbwJjTS4WsqEon27eey7/u0fn5N2giCON60nCN+aOuHg2TgnTkDTnGKU5ziFKc4xSnePk5NpQ7FKxSvnuIUpzjFKY4Xp6r4FKjdVHpZgTgVoFP8l8Wp8L9NnHL7vw5O1/rVcMq3N41vc5WgfOwor4Em4kdpBNyBgHZbnS9Y0J/mZEmFT3++2+FJARhy0lQ8BbRjOWkqXg7QQeDdIhvaIUKLppOmZS9agyY7UJ+0aOuQzXsUQOPBjpJPOOk6iqSD0Gmsa6EDl/Wl8HQUaWuTJxKJSCRyxIb6kP30Dm3CFjDGNE0ffW7ACaITmEyS5Ku1sn1DIA+d//qWAU13TpqKlwAUcJ24UL0sOnnPEkfrBXUi6LTN+0IQR+4Y9DbxDrGxMzUS1KF3lOp+KRAE4XA4vvUqQf8lGCN8+CuhgQdCCLo7vFkyjxVQ1kiS5FG+5skC2ntAm4cT2aVQPQtTKaDJ0NunoR2ttjG1Wu3E1641TAP68Z8sMUcEtNKAmaDQT+ukKToSWr2+OnDPwgaBtkadRptYLJZIJO/QWsNCkyQJ/fBOmhyE2rrPABtPmpzD0MkaCc6yZrP5CrMXTxzftmlokZ7JZFrj6A4HmNjvYvQNIQSzwTt/wWAhTpbJnUBDOziOO/HeoS2wLCuTyTrwDncIYAwW3JJPmpajAkLAB41wOll02gZpRyfTdgg6ao8jhGAAyDuxZTpWI0EMXSwWd+AWPgo4jjMajd8KJXgRjvLK1li7t9DE+diBMT76mIITBAz8O1lS4W7XOW3ZIBDTIWsHZse7tQVa3f9OmpCXABxRMAb1pGnZi07YpAcBEiw6Z/MeBXDMd9QQCBi014Gy9zw6ViNBjuk7wcND8Oo7/B3agac4xSkAp9v2GHHKzOPFKT9P0YEAsey4y9ApTnGKU5ziFKc4Refg1FQ6xSlOcYpTnOIUpzgQxxA+hCxvAhEESQg8jxFBkgSBsIARQZDPu1QxxljAJEW2fhUwosiTcr1ijDHPC1DNiBASBF4QEEEgkqRIkkAYCxijtgRJDBOrMSJJmBeDBQFjjCiKJAgCCwIvCARBPvvrs+/I8xgRFEURBKRfQAUlgVDr3UjyVZmABZ7jMUKIIAiKIhFE/QmCIqkW/zEWWl+TQAhjzAsCAc2xgIQj0IAx5nkeY4QIRLelQQBPCPLptxN4HiNEUhSJEEaI53mCIMjfJ0YQMAauPv0FI0QQJEESJMYCxpggSXI/+XktYCTgvemurc8nKZIkCJ7nBAEjRMCv8MeXIwZjAWPhqRiQCMEKo2fvgOG7UyT5exIi8E8/h0AIY5BCeAZjDPLSRgEWBCwIAkGSFBQzf0sn8fQTMfE6QvXSaH3rZ58KBdbE7wdWnqoLgoDvJfA8erZbnr0HcRSaW8Ulv7cfv33lM/4QJEkSggArgDEiaIokCOLZftyzBALGmKQoIIUXhHa5xRgLGB+zTGLM8fzTlGGCoEgS9g5CiCBJ+lneCYgHQk91FP5Wup6yscXS46PsMKJbsge8eMo3kvxWQjEWsCAIuKUHBUEQWrx9+hLUzv/jBaQStygErQXqUeB5AbQN8a0A4Kci8nTXvwmSTvFOg/r5z38OP9Xr9SPWQ7aUFAgZz1QDvkitIaiVIvfiYrxYVWk0uBxfjhQlUplMTO+RO4GrLc+5zV0WkiAQxvViaDlQ6zKp3o588jzfnuoo8Hwmtnv/wZNopqTV6wm2sv7k7teP13eDSUyqzAYF32xEwjvpQkmv1cOLmo3Kpntt1ePDIplKISunQk/mV3zhpFyllktE6bD30ZOVdIUz6DUimoIDo15KP3z40BuMm6w2CU3yTSafDG0nscUgY2ol7/rS0sYuFkt1KgXZbny0MXkfPDUuCIRQfnfts9/Nrbs9sQzR3aVvFBP3v7kfTFXMVrOEJhFCWOCLmdjDx3PRbMVsMpKYS0Z3ZhdWinXOoNdy9bLPs76yEUQiiUYpbx03rSKab4+TWvqzr+/OL65vR1NWs0kmkTw915vN7YXbnK5XISaYSu7xw4ee7aBUbVTLRaVc/NGjJ5F0Sas3SMQ0AcTkUsuLC4F4TqnWFNOxB/cfLq54Fpc9VRaplWL/5vri6gaHRGq1iqa+tWn2rN1R0cYoXuDSoWQiklFZdNTTP/L5ZGR5edkbTIlkcoVUtPL47sPZ+aWVgFSrV0iQ172yuOSuYbFOq2wnptlsHpAfjZtsLezfnF1Yz1UYg0HP1Ypez+qaNyTQUq1KVsrEV5YXg4miXKmRS8WgqMu5+PLCsmc7LJErFDJxKuybXVgJJst6g14iogSumQisZAmDVv50Nwk8F9vZuPtgrSYQBr2GZyq+9aW5dX+tifRaVTWfWlmc3wrGSYlSrZC3zAdB+PZKcFzAcAQh3GRroe2NuSV3nSe1Gg1J4EY5F08VmkikkIpaDzeZuj8QIEUiqVRSKyQfzc7tJPIarVYqFmGBL2XC28mmSStvX+Xn113gm/lcJpLIaLU6nqkGvBuLa5tNRGlUTwWGbzI7vs355bVCralSiH3rqw8fL6yue2bX/SaTUSxUnzx67Asn1FqDTCKCd+bY6sqTx4vrPoXBrJLS2fjO/UfzkWTeYLJIaAohIZdLu7e39UabiPz2u79gk74QfOOrr79eWPK4PRtL3lCXQXXr5lcr6771jc1kUehxWkgCYYEv5ZOrC4u+UEqm0cloFA/vzi2sZKusVqcVUUSTqfr9fp7H7aNP8bML3rHbInyTjez6FpfXig2sVqswW91YX11Y3eBJqVr9dI8IHOv3LM0uepq0QqdWIJ7ZWHryaGlLrDHolNJGpbD05PGaP6rSm1Syb5O4wQR8/cRkzHOJ3Y0HjxfzrMhq1BCNwv/368/dG75APGsxap7cufN42b3m3vSF0309ThFNCjyXS0WXFuYDkZRYrlHLpcSb3DJvCAdrpBMGLOu7m9YtCIJUKj0GCaAoIlVKJotptlGMp8IebzhfrMd3AlytQiKBZZhGo8E2OSwILAs/N3b8IQELTZZtsGytkAxGCwRxIqWYuFor/+bzb8ZmprvU6M7D+XKFyeYbF69cfv/KVG+3Ggt8Jh589OCJdyf7lD7cXF9ezVZ5l10d3A3FIsGHsz6D2TGgE1Y8gXwm8sU3m4Mjo0x4ZSOW43gBIYSFxtef/4ehf2JYz/761jrm2a3lR//7P//PaKGCOTYVCbmDlSGXObi2lKy8ROuOZqNcqtY5XsAI7axtdg0Mv3/t6qXz3WKi9s+//G3PmRkTH769GsEIIYTZRvXRw7muwTELXbr90FPIZZZWfX2Dg3Q1tbDiC/gD2/HqaJ85H9vdjuQP+dBicgcrdOcvzly/eEatkIFCEThm6d7X/8f/83m+ISAk3P/qa3nP2MxE/72bn2VL9YX7j/S9o1Yld//BMkYYIdQo54N+n6CwqChufnZOabJevnLp2qVRi0lNU2TQ76vz9NnJgZ0Nz24w8rpigQWWbRRKFQFjLDQTocCv/+fnt+57Wm1b+Fp6ZTPISy1ONe/178QyiXyVHhic+O4nl51WbXTtSaopPTtzduXWV9FchT8CNVjgs+nEujd29swwVY3dfLgWiYRTJWRXiYNrK7uxxPZOhFBaZVzJ79ssMzxCYgNvlgAAIABJREFUCAuN2cerErVhrFsxu+KOhTwP1mMDI+MGJvS75VCtzvqW7v1ff/9/RkoMguXEQj0f/b8/X7p45ayoEp5b82eigcfu6vREXz3pe7K6seNbLUq6XAbZ7uZyovIGm+TyXLNWLjZYDiMUDYXW1zd6+hzlVNizky7n4ndvfvr1vYeZ2rdSzdYKD+5+/m9fPExkq0hgbt6aNdh77NLqonu3znDxwPIv/7d/XInkDi/MFvhmMuT97b//+6P5DV7gdgOBDV9saKC7kAqvb0fhjItuuGOpUv/YWDUT3wnGu/oHP/jw6vSI1WzQScSir37zpcTicmm5Rwu+GgP8wav3vk6LLJfO9Hz9m89rjdKtB0uT56edOnT71ixGuFHOux/fe/Jkmz3eWmxKdPHixY9vXJ1wyiRyg1avf//69etXz9pUhEKnA+9WrZTzbXqaCotSiuceP4pGQoFgxO7qqmYTa+v+Rjk3d+fmp1/NhrPVt+MMyUYCkWTR7nIGtrc3Nv2b66sMIZs+O7z2cD4aScDKRdcezEf4iYnBhdnHxRrjffgfnqryvQuDn37+VaPJLd3+bVXpGHWoPrv58Pjpw7ic8N5di5+7cD48fzucZ8r5BEsaPrx++b3pcaVCeebixRvvT4+61BKpUkyTCKFqIbPj35baBvVStDb3qPSutpU+xRvEMRh6hEimRDTLNlPJpLHL1UhV2Xo5kqsZexTNUvrR5na1UtZ1D50ZsDx8Mot50tLTy2OM+ab7yf1wFdONlKA4//pkvBoUCuV/+x//TSkXxxp5FC+zAltuFEnMNBhSrSKqxWw2W5AbrXq9FJ7n6xUWUzRJkWLVQJ/KqFPd+G6XSESVUxyRrQqk+s9++n0a8UkRIQhP1T1TzjdInYZo1JXdH8+YecwLlPInN8a2eIQRxgiLRFKxSCwWEfwR205g3OSamcBDX8My1Ddo0ip2i0J3T7NebyiVqkZ6mzcMk9WipGv8ot6AMSIQ5hpVhpT2d9srCtp3++ty/TIl1/Q6u+ICm9lYl9tdWkOX0WzKpgqlWEJwGQ6woIl0JK8U6bgmywkIPbt58WxDZh86M7JBkgTC6OInf6BQKuulnFhMkCLJhY++J6FRaCdFIEZABIlwucqUq3h4ZoBL+JlSucTSDr0+FtqRq7Uj40MyxBEkRfB1GY0IxGECvbIVjbHAMfVUPLIezHxw5QJF8LRMPtA/itta7JMS/eXLF0mSKsa2YjG2kU2wErImCI0mr8Koa/Kik5aQiDdKhCZ/tM4qBGmwdH30cZeYZLIKpZASevpHunpQanuDoohKNktRhKWnR11it1L1bLmmkqoIJLp64wMRTTPFqNifp6WmH3xnWCKiEiWjJ8gKTU6QmT7+6AxLEBDPQhg1SjmddMCgVQtmq39lZ+b71/+7Y4zkKkqlskCqRs9dH6PFhdh2tlRuNHmE3shdU+C5cj4T9q5RrukBixoRBC2WSqRSihJhjmN41N3bq+SVZJtQ1yvVnuGzldqmkha4chaJdWa9XtetC9x80uR6Cw30wx+//6D8AqeCwDVJAg+dv1isVJDA8oIgltscNkswlclmkgThxBhZBsfMBEHTqBAKEQQpV2rEQm09VRsbGjPolAItFotFYlqBee6p05Gr+wr8pX5prsJ+9Mn7YrHqBz/8A4VMnG7oyGawyTHJVDzMKnr6yGO+0hG0Tm/imdIX6/Ef/uwHYjGp1xvSkXyW1fx4zAFxwEq9kauyPVY55kVd3a5SIcMjQSwSO1y9JpOxwVSc/X0JLkm9rdumrqv3vBXzbHnLRxI0NTw8Q1EUITAyOYlJCLkSC+70yMyZBsNfvjitlIk/305c/t50rlT/0UfvEagZSJSun5PUauiTq46nIn2siHgD3UNDpUJp8r0PTQo6Hw2L9ZZyuaLUyimK1hkM+TQbi5au/PAGTREIIbnGMHH+EiUShzYLWbLMcAISvwNupFO8TRyLQJA2o4jDTU+oKJaqdBJRo14oVwgFwa2tuS09Azc++U4msJrM5NfDudGzM0MOPUkQtWxwPsJ//8aHow7NyRnxBEnQCoU0nYq73b6egXGCa9QzjUohv7G+/GhpPRSKJItNk0HFMAzb5BFCzSabSEbDqUwqEfFs+HJlVioV1Uu5hQWvvduk1qkVUklgY9ETr8uf5qXgZrPkW/UlC0x6d/PRko+iZWOT40qZGCNEEBQtFlfzO48WVws8rZbQR9F2mGOC/u31rVTAt7Pm8ZYqJQaheo0pJQJf3nmcSuXjCW+OaUa9S8veJIEwRkjgBBEWP03mEBPNJqKxhCAIgiZpuYSmyULKv70dCIWileZhJGTqXLVW5+u5W7fvxTIFMB5ECs34yKBERCNEIESqVKpGtex+cl9mmdLJaYVMnAr6FlY2ZQYTEjBCCCMskIiiSDFF0QTVaPKNcrZS5zVai14mkkolhND0zM1zcr3GaHudo6nZaOx6N9bc3uBO0L3hq7Ck2eJwOYwU8a3Yk7RYKqaZSm59M65RyDWSZrNexAK7Mnt/ZTssUFIScxHfYsIyYlFL98aS9wNBkDQtEYvwzu6uN5w+f2lcJBYz5Yzbv5PnCTFGFCbFNCGWSHiSanI8gRAiablUwjGlx8vrJmePxmiWialyJv5wMXhl2q5Qyccmp9RySetIIQhCobfUBd/2bijg28yVCUokoTEb3glGE7XJEYdYLGYrGV8kUyX0Tq3k1Tl4CDBfLaaXV92b/tiGZ3M7GFfIpYTA/u7W42S+bDKpTGZ7T0+vVEQjhNCzRdRaHD3dXUqpCCHEczzNSwlMkSRF0E1eEMYmZwxqBXpRwIiWyC3OEZdZQ5IIURKxSNwoRdzbgZ1wtNR4Kr4SmYwkiLh/q8hwKo1OQpPZ8CarMGp0ehFBjPZrV+cXbt9fNVp0NE0hjAWOjQa2N2OpZil26/4sT9BKmSSbSszNz7vOnytnUm7P7thoP9tgWebQHfIKIIjY6j3Uc8UkIxFCbKOxubA4cH5GTIL+QLVqNbAbiKQSkdDO3Mp6Opvd2Y2kk0mfe8MfiGlM1m6HQyEVvQGTY3+IRBISMd711XKxJpEpxBIp5psbjx6IVVaNSk8ihP4Xe+8dJNeRHnhmPv+q6pU3XdVVXe29QcM7EiBohuSQHM6QIxPSSYq9jdDFrWLjInS3F3F3ETtxG3dxt1a3Uqx2NZqRZjgUNfTegAAIb7vR3vvu6vLePZ95fxQAAhyCaIANojGq31+NQr1630vz5Zf5PgP1kpyanV+Ry+kLFwZy5VIiEZmdW9OlzLETF0WtsDIaXg4lc4m1kxfHNj8pIcS5fGpsfFZD8sCJL9bzSjmXk6SyLuePffxpvKjqipQKzUiOdrfx2haCpCiWZUuZ6EoqjRx1LkPVTqryVTbn9aHd450KL0dCqUZ/TUstuxBeybAuyBhJmjLxLMOwNlbQVOSxm008TxISBFAUc4zdT1KUrbZeSD2Qt28AAICQHg8vX7h6xdV4oK/eqcrCk7/zu3YrN7nAfHFpvCxQeZ0tLqYhb68P5Ou9FoKkbFanxVnT2ewbGBiQpWw2WT517JK7vbsx4KOxksqozT37a5zmTwYXGr02yNA0bfL76/t62rHsfffX76tw9zWtBqEql1PxVe+2p/YHiYXZyYnl1P6OmjsLTRCC1ex0msuy2eWwMCR95KknrFYLDcShd49B1uuw1vW1t+k+4e0vxhBoBrpOUKQOVFXTdVVGGmQYqGNZ0zRNUQDgAnV1mqym87KzttYkMLfXuLhrx36C53iOkdfeL4iSqiOCJACAN2tpqZi5fOqLGOl/6WAHRlq2UKpp6T1i85y+eKXY0WDmIAEhiYGkqEhTFaTzLJmKJjAB3HU+AIAiFseHhyIi1dfX4rHy36ZzCYoUbDaXWM5r0OEwMxQBKz7G1710K/71uWTk0sVxg8vf2tZEa77DboLjuLhJPpcWA7l8aXV8KCY/t3+3xcht7LZYU6SVhemphbX2nY/UmilJlCij84nH9lyZmJ9ajTXVWmRZK5XLBNJYmkIIQQiKucTg5XOEvamjwW+gQDK8dObESOfBI36nhSQgvmnrXQkzoI2OZx7pXVhYr/EFa0lRk8tzY6OT89lDzz1mZWEhEx0cmyhRjiO7OynyPq2gkGZ4t8uOpBzhsFiNRCyWzGLfH/9+/9Tk1NLcnN+5Hd4kNULXXbkBqHxM0rQKJR3rqqxgRF/3+d+4tBAAAAHpC9RKcjmVLzqdHgNvqoSJYE1ZmB6fXki09/bU+ZwQgMm5mCfYYRUMUE1dmM5973uPeQTw5ifnuhq9NMmRJGXw+Xf39lk5OLP462xZJfNrp05drNl+uNPDL0xOhDJqZmg0nkr7AhFnT90mNioE+PiZ6SN/+kylBJqilmcT2h/W2eC1EYoojnfXN/X2bC+Fl2Zn5zFta26u79+5e3b0UllNqLiNhXfVbt8WSRJVnerefVgpf5aJhVN209rEcFQy7tjR5rTxFWdqI8E0dPe1B1zy6lJSxDazqbt/Z9BKhwaHkzLrb3D07txGFvJLVz4rAyBssoCEycB2tW1rafIK+bnRaPJQx+Efmaw8oUvrs6vpgmAjx8dXdzz/CADXphPGKBsPDU3MIMF3eEfbJotT5beCzTGVaMFuhGMGjmYMNofJcGlwwlXntzpthhU2mcoQSMlitdHIciwNIYAQ0gxltvm5/HA86U4tLUpM+3c51b8EY7GUO338M6HtUJOTSWezUi5x8sLsI4/0qcXy9q6+nZ1BpEpzS4tFjfS6DblcDgJgEgyiVApHwzphpCE4feqi0efzOQ1iuQT11OfHF3fuatOzBbfbTmBlZT0TrLHavTAciRPiOu1uYwDAEEKSoklIkCTPmfRiKpnhJI20GDd0AABJxlPjN4KSoAo+t9tISe+/e6xr+y4ro3rMDkdto5M6E02m5MSaw9sIsLK+GnV5bQYGrK2HcTFi9PWbjUaIpbX1cLlQEBzBTDyaKihNflsyWxTcNd/QExOXLuoOb7DWlqOEOiNfTMVko10wsBBCmmZJCABG4+c/X1I9T+8IpJJpnqdOnTrTvWMnlLJGowUiJZPIQoqxWZjVtVVaFTWD2WUk5lUC0iaXgcZIm58aC2XEYGMzBTVRVniOveeRQdFsjb/eaBJ4ezEYCFS2igRFkAwFAdDkUlFUANYGBsZkkmuttUrlUnJ1ZiGr1QZqs/FCo9dfWp+8upjp6+3UxKJoNBrYO58rYYRSsdDg0FhT/wE7qWSzqWQ0HMqCZjetI9LX4CF0MR5aJySF5iwWDqYzOY6Gg+fPlmhHq9OmiKWSUjp2/Eqwu9fMokJRtJkNEBIkyVAEBACo5Wy8RLoN4vkr008+9WhsZdZZ25YMLZ+6NPfEc4ehVMgoaG56Yi2jHd5VUy7mKdJace3fZCDBmazNLW1WE086GjwCFPM5msrE4klZwwaTAAEEkCBIkiQgwlo2nadZ3iQYIIQkRREEQQs2mpUS2VRRTQreRoZmIACQIOkNSQsJgqBICgCcjMdTqbQ/GGSTWZPLVcjnVISVdHh6cd3qCwpGslwWTQaoisDCURwFAWCsZi6XywFJMxitJAUjoZCztrbPY10OR30mCFkTg8vHjn/h6NzfbCVyZa2xa4+/VUum4uMzM40N3s2NKSRQPsz7AgIJMMBY1wtJaKkzQIwBliUxncibzcZ6wRhaX0flEhAEn8uWiCrhcKhcwrxgpyGGAFIU+V0FEeNYaGk9WXB7a0VMGXl+dXo4lJMbm5qQrkiKIuZypFHo6AyuxRN2Rk3ownae6WtvXV1ZM8pMlq1xG4z17b7V5XUzUSIa3d9qM3Qb/G3tK3ORlJVajqGGXba5s5+l6rd1u9mYYtpmN+q4kAXmgI0GAKiqUsxldQBmpyYLummn357P5SwWK32/NhhVHlY2IQKu8juKrFicDq/PY+C5UhEG/D6n3eJxmBOxaCQcDbb1+d02HQO3w0lThKLg2oYGN69OLkdUyhhwez0O0zfdcvO4NZoG62J+fiXP00oilZYQ3VgXsBvR0lrSYLH3dLYaOJZhaEgQRqNgE9j5qflCCbW1Bsr5XDie89c32E1ULluWJTGXSZV1yu311whqOJEoYWHHtlYDzv3jp8M7+9oDHsvM3FK6qO8/sJOnSQAA0nXA2bwOM2cQ5EwokVdMDl97fc3GI+AYk9NuEWiKAATTWGtfXQmnc1Jf/zabxR6sYWcWVosat2dXNw3Kn775efueHR4zO7ewqkJ++/ZOE8cZOTi/HOFMts6OJhPHYDkfyas13kDQa78hw29GwHnravKpWDSWCrS217odM5dO5Tm3w2IgIZQl0ekLmkhlajbMG2AynsgUJb+/rr7GvDC7oOigs7eflrOzI5egr8tj4bKRNZ3im9s6bDypY503Gm1mM0BqPBkvFvJiqZjOlk1Wq8nA3Xj+e4mAgwTLG90O241rNKRTBsbmsknJlYX1cF7CUBPLilrMpso6UdvYaIBKIhal7YH2+tp0NKIhvZjPJ+JRwe03cfSN9eh28SYYacVsai0mYq2YzhYo3uL3OLRSKppTanz+ruYGlsL5dEShhLpgvZEsjk+EsK4UJCRJUjGfyYo6jwpZlVDFUiaVUKHRaRMoktBViTF7bTxVjk59MSN2t9Q5Ddr8epqz1XY3uHLJaFbFaimbyZc0TKuFPAJELp0UVWSyOgwMeaNDNzech6QZweYycRSAlMHA84S0vJ4UrI625kaGJjBGGFJGk8Az2uTwlIKh3WmFGGuqbrHZOF6otXNroWhOpno6GysGN0aqRgle2x0i4AAACCOCoOw2u5GjMVLXEwVXjb+prmZleTaeSQONksWyrIjJZIY1mMxGWtEZp9tlMLCAYGsdfGg9msiUu3t77Rbu+Lvvedt7moK+9cW5eDzVufOgmRCXogkaqclkWsG01+fmGIYkSYKmalyezYyAAwBoCibIhtoaACDAWFVkgnfXegQAcDqeuHhytG1Pt8CxidCyTjAtbd1+l4UA+urKuuD0NLU2cxQBMJI1ZLVazSbDjV+9bxFwUDCbsSJF1kMmd6CxobaQTYhiqVQsplIFm8u6PDohM4b65jYlG4nFEjXNnXUuq6+uPh2aj8TTLdt3+6zGmhrv2uJcrqRt27ndch8i4HjBRcqJUCRKu1p7Gr3uxrrU8kwql/e39de5BYBUnWDrvS4AoFTMry3Oi5S5mEroGKWTSUUHFrvzxp6oGgH37fntiID7slxuKpUqFAobvLKivB6KAfQVZFmmafoeJMdISySSkGScTvtGdY9eGpoM93U3EfCub7dZ5aUQUifGpnr6eu/h2jvWgIssTlGuRruJ3eAeTCoXk7Gwxd8q3NOMvue++3phiplcSebNTjN/L3O4XC4bDIY7f+8b0aR8LCOaBIvF9PVv9+ANP5/rf0nZyFqBaQk47uF2D6qgFUZqJBrneKPdZr3razFWFIVhmA0t+RinkwkVA6fLvfFzgenR4YauHvbuV+hN04RfdvMtlErFtVCkrb3lHjy2H1ANOBwNrTBmp8VkvIdTLoSQpmnVGnD3xqZopPtBpQYcy94fp8n7j6qqFoulaiptHIwqmTY3rnowrmTGu/t7bWIlTozQPcpwR1Op4pew8Z++sQu/B2HAZptKFUclePdWbIVNUUz4es6nu2hDhPDXpnbdAA/MVMIYg7ucOzddexemUmW432UyRoTQvQ2q+60JK95096xAHoipdMMp7R4urppK34aqqXSfqJhKD8EI2DLc/foE4QNLQn6TEPfPoL3bFeI7TCh8ZyCED8ZD7lYZ7laCu7JNtwgQQvhdNfU9DPctu+XbStNlgzyMw7NKlTuzRXVElSpVqlSpUqXKVqBqKlWpUqVKlSpVqtyWezSVHrpz4YcOeJ0HLUiVr6faNVWqVNk6VDXSfeUWX6VKYOQdr6nE/oGHsG/wTTxoWe5ApTL2g/WiqLTSFmmrLdV3W0eSjXND4IdR7K0pM0Joy4q3ZQX7Bm6054MW5BoP0ZTZyt19LZXqxqyLrcYNa+dLUwlCKAjCRh6m4tBOkuRDERfwFYrFIs/z3z51x/1GVVVd1xmGeYDWkqIoGONNDDr7lpRKJY7jtk7fCcJm5xm+z4iiSBDEwxWKgjEuFosmk2kL6llN0yoRW1tkgtyMqqoIoa0zeTeCpmmKomypMC5JkiCED8uU2ZoaSVVVRVGMRuODFuQeqYyBL20dgiDsdvtGrlRVVZZlhmG2VFTnBoEQWiyWrW/kSZKkadqDterK5TLGmOf5LaJtSZIUBGGL9J2u606n80FLcXfk83mCIEym7yjd66ZQ2dI5nc4taCrJsqwoCs/zW2RM3sxWUCB3iyzL5XLZZrM9aEG+pFgsEgSxpay327FlNZIkSeVyeYPWxRakWCyKorgllsAqVTbC1jxerlKlSpUqv91UTaUqVapUqVKlSpXbUjWVqlSpUqVKlSpVbkvVVKpSpUqVKlWqVLktm+KNiPMFqaQgs4njKZDIlEmGsZiYYr6ULCgUy3ptPEsTEIBioRTKKH6vxUhv6ez3X/GJwfiWqkZf6zFT+c71f1wrmHHtkw242GAMIHz4ki9U+IbnqzzR9S/c1ELXQ3BvbtWve/yHtElu4TYD5pYe37gb1j+RQbVxvtISNzdppQVuf2Hlf7+mRSH8sjjmzX9/5RabxW0686vz5dZLAABfnT73r6+/FOD6PSoR4JWb3iTexofnV35vc7nl/jdroWudDiHYwKz8hp++jb66iW/qvS9vdOv/3dJ6t/nO19/jjtxxmtzuRpXV7I6aalOmCcagUizyppsD8Bv/vKllb5LxWs3pa3/DW74Abr7k625x4y64cv1vyn5nU+mOYwJjvLyaHE2q2zu9rQI8M7ouuO1BA/54JLKQliFJPra9/qk2u4nBV0dXX5nMvfxYx5FG85Y1lpAmL06NXR1Z2PPsC1xh7dzp00tp2Nu/48D+XgNFAACykaUvzl5aSqiPPLKv3kGcO3NlNZpWddXq6Xru6e0L509eXY5phPDCy8/Wu20kATHAi4Mn3z07CQnhpd/7YY0JnP382PhqwtfU+czj+5RM+PixL9YLenNn3xP7+zn6ITvnw1gbOnb0/MyarmuFInjhD38nwGZf+4fPVZrqO/zMoW4/ADiTXP/svaMtjz2/o9ENIY5HQl+cOBZJiqqqeYON9XWexfHBVEHXMNG9fXdvg3X46uDkSmbnnn27tnWYOPpBP+K3A6NkePXcuXPL0XJHz7YDe3vDc8MXLl8tAfu+/Xt7OoIUBACAyPLk6VNXInnw+LNPtAU9oyePX5ldkVW1cc+Tj/fVDZ98Z2A2xTT0/enzBwkIIQCaqp7/6INLS1GDge/Y89juRvPFY+8PR3BTz7Zn93bGVuaOHT2jmBw79+3Z3lq/Vafa5lDIxAbOnx+dizf19D56cI+FIwEAUiF99vSFsZllZ13Twf27zFru2LHz6+nctsNHdgRNR4+dCSdyuqZBi++PX37aZjZCgMu56PtvfBApyO0Hn3lmVxPStND4yOdXFl/6ox8bcGli8NyxwZW6+pZnnzxgNmxm5C/GWNfLH/63X1gPvfBoV60qiRMDZ8cSht/74QEWQACAJhfnxoeOnh5lLbaenTtteubcuStFFWKS3b53d5vXcOXilZlwcde+fbv72g3sfYnFQ5oyOzqwnCh27TkUsHEQoJWJ0YHp1a7+/o6mANDkC2eOJ0Tnvr09LrsBQqCVEm++czSSLvTtPXKgv+6zN/5hOaUgpOezxD/78//ekBr/m384xwoc6W/+lz88sunDUy7nPn3nreWkJPgaX37hewIDIcCaLJ79+PXBFdEd6Hz5hwflTPzoB++v5zSr07370GN0evH4qQGVN3fv2vPYtpbbaWGpmPjik1PzobiCNKMt+Nwze1cmh4anVxTS8sMfPOm3MZ9/8vHUatIdbHvp+4/zNAQAKFL50qnPBycjdm/zD390BBeTF06fmlrOB5t6v/e9/tji5OnT5/LI2LWtf//OHo6CGOPI4vjp8wORsuGxQ3u7W2rnh86eG5wqC/7nj+z3WYjjH34+uxZ1tG//weGdgoHbUItglEtGTn9xai5S8jc0P3Vkv81USX+A84nQpaFxoyu4d1tHLrJ87uKlqbVU7+6De3pbQ+NnLw7NSSb/i08/4nfZIAAY48XJS58dG5YRPvzDH/fW2SFGg6c+Hk96/rsf79al/Il3X5+MIU+g/YcvHDTSdxd6qYrSsfHIVLRcX2t/pM3JyvKHI+FQUdvR6tnXaI3HEh8Np2WCfGp3sMvBQQgwxnJJfH9wLVxA9UHH0+2OeCL7/kiMJOk9HTXb/ALE+vx6eni11N/ua3YwAABVkQfn4pcX8yab8GiH20OqJybjC0mp1mc73O6E+cLHU8mEiL/XX9tRY6LJWwbmNy3MWNeS0fClwbE7bRFwviitZsS8ggBCoVQpXlQGF+IREe1q83RYialQtihrmih9NpsxA+XTibisoa0Zy4QxSidCn37w2tEzl5KZ9OToyNBcmiel4ZHBqUgBAwB06er5y4uRAg/SV4ZGIgXc2NrS3VW/Nj1flGQ5Fz0zMuf013GZyQ9OTUqKBgDWxfwrP3td8DeVZq++eWYsGVn86Nj5Gp/7/PvvD86szE+Pnh1ctBrpgRPHVtPFB90Adw2EhCsQ7Onp8oLSqaFFliEvv/f6WJmvEwq/fO3jggakcvHc0Xfe+vzsciJfuYI3mFraOlqCNcVMfDGcdXncbR1dtXY2GgknsoWJK0Mr4SyjFc+cuzwfim/NcbJxdE1aWVxcXkphpFwdGFhcXLgyOB4rgHRs+crAULakAAAwls6f+CJT0g04ffzscDSRPX/utEJQjc0tQbdZjo+/9/lCQ3PD+CevDITKlW2gqipnTn+hsfbm5iafjY2vzHx6csHpMC4Mnjg3Ojdx+cJqAWuZ6KmjJxNl7WGrWtWOAAAgAElEQVRvw28Ca8tzM1evjhs4avzK5UvD85VPY2sLS6sRi8O5MjEyNj4+NjIUK8pGmDl3ejSWQ02trT1dbem18VRZx5AAEGCgX37vlemiMVhjLuezsqrOXPzoL/7u1c8vDJRUlImuff7JBc5uzS4PnhxZ2dz2VAvJv/iP//61T45Or6dVKX/87V/+7avvX7k6d63bMC6kk1OTk6TNSSqZ82cuQ8HV1dNtZfX10Fq+pCxNT0SzBTmbHBoaDacL96OvdSk3dP6Ln/70lVOXR9MlFWBcSoXPnD72wWcnI9EEwDi8MPHZBx+fvTBbKCqVSyYunBkJ5QM11o/efy+VFxtaO/t6O7nS0shqnodobfzUcFJtbW7sbqgF90Hi5NL40HKhvbN94OhbY8uxylFCKb306cBcjc8xevytyWgpnYqdGx7yBuqbGutpOTs/PaWxVkbNDZw5Fytot/tlkuaDzc09va2xmfl4tlzMxS9cnnb765SlkU8uz8bCi8dPTLW11X36xquRTAkAgDHKp1Y++OyCx++eHTh+fGAmtDxzdmDabGGuXjxxdWJ2eXE+o3IsVAYvXVhL5gEAWMlePH81FJdYKTwwPLawOH3yzIROCfmFgYuTC/NTw5NLSbfd+Pnrx6O5ItpYg+i6EllbmZ6P1zjMiyMDF2fXAQAA4NjKzHtvvvbK20dnl8O6Ll25cGE1lHQ5rFiR8tHpU+dmKM64PnT6wvB8QdQAAACXP3z7Q4Wzm/Xw6+9elNXyu//lP/38lffOXVxCSMssXX7983lvrXPy9MeXVnJ322uxWGYmVjTR+sW5xHJSHF+MhYqqk5A/HItnyvK5oQhgaCaXeW8sgcC1g72Z2bXTYTFop+WSnM2XL46shTXgNhAFUdUwTmVKnw+sfDqdipcrHYrjsdzgUlaHaG49dXElM7mSWi+oXgsxOBefDGUvz8ZSOlHKZU/Opgqy/hXxbm8qYazK5bVQJBpN3vEhrx1dXT/MIiAIukyqqs4nSiLD9ftNRgbGQokYwf/OLu/iSjJcULdm3LcmFtcXpkMpzWAgMAQahiwvON1WBFWEMcBYk0pz62mHL/Dk/s5sNJEuwu7+HfVm0tHYsW9vl8vt+/7LP3rmyYNOTluLZjUdYQwgxIqq2f31FgMWVS2XChV0ft/unZSeuzoXRjqgMOmv9RCqjL/2UHirQ/jbOh/Zvy0WTT77uy/WOQUIVcZsra8xyaKMkJaKLn8xGHFYjddPR4FgsfX3bw/WOsw2+yOHDrYEgzt2bDMbjYH6ph29LZFU1Gi3PrqrLZuMrsXTD/s6T5BMsKXj4P5+BssqxRl5QkKEyeawCryuadfaREzNrRU9TZ379rSFFmYy0bmZxejq0uLI1WFVQ7H5C1lH46OHDjdx+eHxEAAAAKwryYmp5VRkaWp0RFK1eHQ9a214Yl+vgyxcvDAXC2eD3b2djZ5YfH0pXb4fq9EWAetSNpWUkXX33m0aLo8vrlQ+t9UEn3z6qacPbyeQms2Watt7v3e4TSxrBiNjsNj6t+/obRB0Q/DZw7sFIwsBAJp09tJYMpoYHx5JlTQMcEFC3X2t2bKGdC2bSq0W8LNHdgcc3MjI4uaOSbWY5t0dTgePMUZY1zDV18pL4o03B4A3O3YeePzFJ/d7LVwmmbHW1O3Y3iVYzIHGlh09rU2d/Xu2d3KkCimKYe9LojukKiRDuT1egaYwAEiTp6fncvkCZ2Q1hJRS6urUKgI6TRGVHTDGeHpivLa+9dCBvaXlhUhB6dyxd9/21lC09Cf//CUzDS+eG1PLqcmR8UJewvdhdFpqGn78Oy89srcnu5zMFEQAAASQN3te/NGPLKBQIlkzhfLRxfn5zPzs1MxcRLDa+/Y88uKzj9bZDYVEqqzeViSaNXX2b+sK2ghXYP/+vlqf/5kXvv/0kQMWohxO5WiT+/f/6Hfo3HSJchtYEgMAsC6lQqsly74De71mdWhkIpuKFSjvrp09JMguRQvtfbte/MHT9W5HPpopiQoAQM5H1lMFd2P3wf76VCQxPXQphoi2Hfu2B0yLMxHE+b7/3BEW5SmzQJPUBg/kCIKqqWt+8eUf7Oxq1MvZVK5U+VzSkNlu8TttQNKQmJmZXZmYXV9ZXExk85nYbFIj27fvafWwiwtrhZKEMQCQ1KWSpcbrFgxI1QGQJVHY0c6pOgIAAIIqAiYY9JGEiO5+MbPYzc/011gJSACCpsi6gPOFXme+rJs4iiLJXT11R4L8XE4Jmq8NcoT0yfnUYkZciBajJUVUpNHlbC4jzSXKeUVHiroSyUzGJYGHN96yQYRJANxG2khCRcNen+PZHYFHgmZFUvIKaG3xHaozllTdwNIEAb8i/u1NJQhIhne4PTxzx2M0SBAQYIwQxhggBGkSOK2mp7s8e3wGqGgnp5LJonR5PpXJi58vFYvZ0oWlrL4Fz5WQFg2vDU1F+nftNvGAIFkjz+aiM6fPjcsy5zQxAACkaRKBGZ4SjAZV0WRZwUg6e/pKbUNDQ8DNmyxdbYHpM8c+GpQf3d7IMRQAAJBss898+tMPJ1bzAaeN4wUlV5hdXkoW81lR5gVTqRQ/fea8xDKG+6PpvgNSq5Pn1so/ONzHkqTdH4yMXfjk1ITD71GL6VMXzvQceLzGRAII8HUXB6mUXVpZ07ia/jY/AUEuHlqOpx21DU0+h91Ep1PJodm1bCarqeoGt01bFkhQTk9NW3d7wO3iNCknYjOjLU9cmZoOc4yBpQmMAVDEsk5DhuN4ThWLGDC/+yd//NIPX6jlSx8evZSIRGinmaJok4kvJAuVn2VY4Y//xb/44TOHHHThrQ8uliWZMJt4mmIIShM11kQuTc+uRSJZUc6KKvjtfQEHCYqmGbmcnplbXE1kippacUYQbC6Pg7/06elkkfY3NAQbGoP1Ld3dDeVyrlQWMcZnjh93tva01rlpkgAAA12NFiRTY8vhfe0nPjhZ0si2/gOHdrSqCgIYy5qmGkgbT5M0Uy4U9U1VXazN99LzT7uMNISQZk17HzuyrcmsaaAyVwAGrMHk9Xris8PnB6aC7W1WFsZW5hOpQl1br8cuuH2BxoaW9nqXLovZXOl+bLZI3tLatW1PX4uJJjHA6ytzoXTJ19Bsd5hUpE4MXcW8pbnJb2BJfH07VBJLZhNP0wylqyUFYYBXBz5bZzoe3d5AktTuZ/7gz/7guc6g48NXPszdhxlutPuavKZ3f/FzxdvdWe+qyMQYHTt7O/2BoNvErUZyvvquP/uz/2F3X0tycWhoPufxenLrU2eHph1NLR7TNy55WB08e8Ze39DcWGsSrB2t/qtnPz0ZQns66y02V/+OVl/9tjo6s5YuVfxeKN5M5hOzs/NrkaIiSwxrUNORhYXlRLKsaNDl9qjptUtXRg2ehlqngDHWpBIiMWPgeZ5TJCWfSmKOYjjWYODEjMQa3S3NweaOdjORSObLG1xGIUFZ7Q6HAM+cPxvF5r4mX8VFye2r37N3X32NHSIMNCmjAJO3sbXOvTQ7ny6QmpJZWZxeSRYz+aKu6wBgAEivwzp6+eyJC1M1QQdBGB//vR/1Nxt1AACEtMFj1lY/O3oiLAs+0107TpgEY7PH0uY3s7paEhWXQ2h0m7v9Qi4vlhXcFLTXuoR+L7+QKFcsDYxxQdQtgnFb0Dy5kEgU5TKCLrcpYIED86n5SHYsXNzW6rYxoDIAMAYsT2GsD67kwmVk5mi33eQktI/G4gTP1zkMjV5Ls8e0w2NI5cWyqn/Fhv+GF3CQpGhBEMg7O2dBniFT6eL5icjnI+uDKUkniNHFxKWlbEHGRqBNreWS6dzxdclmZrM62eThjk7EilvvuEApZyevHP37Nz/85NPjV4dDn732q7XEmiW447nHd/CoNDsTwRhAgiDKulLSJE2kOYphaCm+MJ4EvoDfbOQAAAMnP/rbV87u/8HzB/rqaRICjKVi8tR65uXnnvrBE+7zJ8csgc6Xn98xculS0O400jAeXeVq24/s2enA8tx6+uE8AMCTl8+aWnZ5LTzE4uXjZx79/guPf/+pyKVLCzOTb73yzqlP3hmcWD/z4afruTIAAGCUia7HI/FAR6+ZIwHWVuZmC5Je39bKMczuA481OAVVzGNSoCFFPuTLvK6K4dDyakpsCtbzqjw5MVwsSy39R/pba/O5RCJfAgBgiqaQrMuKpuo0Z9Jk0WB1dnZ3tzd5wpF1guLkRFFDSBVFzmmqLJ+qKPEWV19/T2Odc3V9jSCgliupSEcEcrQ19B84UGfTYsmMz8hZuIfV/t4QBNva07dzd0s4ErIIZid17WwbycWTH392ZmRl96ED29prV+emwlnUsX1bfj2US2V1MXZyINzR3GDiWVh5PUNSNSRl8wd37esXl+dFFVpstmuOgxCSGIKMUtJ0ABTeaNzcMUlyJpflWjJogqDtDjt1k1bGACBdnhsfeP3dY+bWnc8d2U1jeW52uazCrs4moMuLC4uJvNLX7ZUL6Ugsg+6DBiEoxmAUjBwFAMBYHbly9p3XfvHOh18MXx65fPHiq6+8/8YvfvnZqYlLl78YX1guyToAgKDpUknUdF2nCYGFEOvvfXB092OPmFkSQF0FVFdnV1drfT66Xr4PphJWxU/f/MWvvwj96b/8I7/NCCovwmKzQ5OhYFt3Ww156cqioqr+5taezjYro0VDyaXJ4TffPkEGel98cr+R+Sa/FKWQvDidaGqsc1pNAOhj547/19c/f/SFH+ztrCslV6+MLzR272llCqMrKQwAgKTF2/bHL+8euzpm9jgMnKWhtfup/Q2zUws2h5VlyfXF6bfe+qDIOF948bDNyAAASIrGqi6LsqopLM8YBSsuqaqsaKrMONlEeHEulAp2bHOJ0floXtmo2Y6LmcTxD98/NxN9+kcvtnitlU953mAyCUTFmZHmTAxb5/F0tDfoUo4w+p8/2JtP50lCNQsmkiABAFhMDC6k9z12+Ps/ODRx/ryiEu6Aq3L+gnQtMntJq+1/7snHejzowoVVcJdDMZ7ILcbEWo/NCLRkSZxcToXzem+9U0oXc2Lp8nRCpLiD7dYr8ymEAQYYAMJioEyCsStgJyVJ1IDAkg6nqdHDpWL5yaXEG1fjpyYTF+dz5ydjWUUHGEVSRUxQh/p9ASORjJdS6fz7V1aGM/jxXl+TlZ5eSpchdaDRupwsZmX9KwPzDj6AEEKavqOfIGwIOHoixfPL8UkM6r22Hq9ZcFJL6dWTU1EJgSO9NThbMgmmP9wbdBtptZT9t+8traRFq9e4pdZBihO2P/rC/9O4f21+9OT5od59u7XI2OrcBMqwCrIzWv7td97ABndznfXs2MXJq4qvaVtdrSO5eFE1OewOK0PCcnTmb175NKJSufjM0GhNn3Xh/3pl5X//Vz8StNTp0xel2YSj16zmU2dPXIJOq8aanu1rLM/H4stzl/hCoiwd4tmH8wBAnrw80frk/0SRJCAom8X62clzwCsSNpe/sev/+Df/dzaXef+N11q398nJ1b999fPmwy8785lkXjrS7IcAYk2NRosUwQd9NgDQ+vLsxMR0MlUINvbXB2oemqIMtwPpa3PTHx27TJIA0rZt/sBEeGV26SLOl3xt/aXI1M+Oznd197UH+clLn46U8t7uQzaH6Y033jt1xhSfWO5/7qXGTsZw8hev/ix2Isz/677A3Mn/9sZEw5/9uPmTd391YahVXg0/+uTztV6df+MXP301JUnMDw5Z1qfPDA5OC1ZjQ0dju5t/KMfURsGpSHji8kBchTZffVdP64kPPsiU9IDP+OmxM3GdW1+ZW151xmdGB0fXAUwDISBYLUpqLqfbPC47RRFAifz5n//lP/9X//Ohp/f/5zd//vMRom73PruBAABBgBFQCZJyetz1hvxf/PU/2nR59/OtG33tsTEgrITsyAjfmP0QAgyQujQ18Nq7x59+6Xc/e/udwVD+0drExPg009scK0nAaK618xAoa1NXLo/O50tF2tHkdVnJ+6RBIMQAIIAAoHY9+mygdWd4afLjCxMtbR39zzwpyfLwybfHo+6A0/zeL/6DpeeZrq6+nx07I65cIWvavIIR4PJIKPNnbbUQAITw5IX3P7owZESlmj17HJu/GcJLQ5/89Befmpq3LQyf9Xkd5NKJn10p/a8vdr7ys9cbm+tWZ0oH/1ltOjL6yruDHq8jWTY97kaffPDu2bnkPptzempSsOxzGm97KFLIJhIa57EKPE0UorOvvPp2vEQW1meHJvxdjtwv/ss723YGL0Wp/zFgnzz3zq8u5/7VHz527tTZMmsFInr2x9syqdili1dEwsibXK1e7tzn7528MNO52zg/O0lI9rHxCd7m8dsMwxc+nkY42LO3b39b5M23Tr/3ajiRPvziIUGK/+PPj1ms5KwoPO4x0xtrPV0RZ0cvv/7+CdLfFp+fnmRgJrywmlT/4A+fhxAggBBAJGvvaLCcH7n49qJqcPfYzPyF4+OL0UwsB1/ubqSU1f/t35/6k5ceN7Jo8MIFkzJPmfuv2VgYQgggJHiByy1eOXsBrq5LB763oXqyN1PMFd8YSxEUWFKIPUYuFk28O6wKlAYEg4Wnzp9fOjFvwoVcR9BJAOlf/83Y77/Q1dls/+Wp2Ju8RFss9Q5zR43hg5Gw6KDqG5z7e10NwZqlcPr8QrrVa7g6sbqSwe0OKleUwvN6Iq843WB0Lvb2dMZkNS8lCo0WcnIhMjtJKvm802a1suRXomHIn/zkJ5W/JEniuK+609MU5XDaOe6WYoEIIV3XSZKsVBcqy2okLWKMfVa+0WlstnOkpkmKLnC038Y3u4x1FgZCwiOwRgKrkqIoyCOwAafBbmK/+0BmURQ5jvvaomaQoIxmu7/W63G5/IFgZ29/vc/nq7E7vMFde3d2NbuTyTjNC7t39TsdNpe3Ye/u/qDXASBweX0tQZ+RY8RykTPZ+/ra/TUuu9Pltgojo1OPHDnc095O06y/ue/Zp/c7zWa7w+yta9y1/5He1nq7wx3w2u0e/449+7ubAwx5TTBN0x54tUtVVQEANE1/86CHGGGa7+zq8lg4ApK1zS1mnnZ6A08980RLXU2t3+/xuGtqXB3dvQ5GjUdXkLuj1SPYXO7G+qCRIQHGJMV6/YE6v4cmSZY3mq0OX0PrwQO7mgKV9yPXEEWRZdktUpCuVCptpJgaJEmjYHLYzQ5fYMeend3tLb4aj8tmqW/v2ru332djVsMpl8u3fXuPWTB76loP7N3u9/pq3VaWN7T07Tq0p8ft9jbWOkhO2HP46R2ttVoxM7euHNjfV+e1k5y5vW/HoT09Tru9IeAy2jzbd+/raQ4YzRaHw9He3bdn906PxXSj92RZhhA+XKUbMcaiKBoMhtsNQoZlrXZnTX3L7l07Oxv9uWRMg4S9xuvyeNo7Wnwel7umpqGx3mww2Dy1jzy6v7HOQ2BsdfvbW+uMLA2APn7lavOuAx0dbTUWzuJpePqFJ2usBggBQVDOGm9Ha4NZMNbV1/IGS/e2HTt7mtjroT26ruu6/q0nKYQAGAVTsLGlxmaEkKAYi8cfaKxzl1OZ5anVlj27LSzb2dXdVOd1OJ1Op81oNAbq6v0eB0GSVqvVbLZYPMH9e3e1Bmto6r4oEAgAybJ2j8/v89a4HDW+WpfT4Q3Ud3d2tjTX+3xep8PW2Nbe0ugtxReQta6nuyfgMgk29+EjjwZ9ThLqHOfq7uo0cjSEhKe2jqMpT7D1+08edJn5G3fRdV1VVZ7nv0GSDYDy+ZIz0LS9r91ps7i8PhPOjc4XnnzsoN9lZU3WbXsP7tvWbLPYnVbB6vbt2n+wtc5O0WxbR0drnc/hdLlcTu56FyuKAiGk6S8tJ6RrVqenrSkoGDi5VCRNtm3dXXU1TrvLXRfw13osDG/a8dgTOzuCSE6OXF0/cmS/w2ZxB+p37D/Y31lv5Di73RZobN6zd29jrR0QdH1rW3tz0Ol02i2GXCbHGV17d/XaHbaa+rY9O/vq/D6/12USzC29u3b3dfhqvXab0SAIe4882dsS4G6ylb5BI2FdUxTF5g1s62qvcdntDntZKudVraejhYSQN5kDwTqXy+Hx1jiddre/ae/eXY11PovF7HJ7tu95dEdPm8Ci6bnV9o7u3dvaOc5QE2h95qnDNXaBICAkTd5gfVO922jxNdU6TFZn7+59+/qb+OttqGnaRrrVYGAtLCEw1N42T3etxec0WSgsGNjHe7yNTlOdm6d14HFZvr/Na+PIhamIt9HTXGutN1NWI3eox9fgMnkdJjcLgx7LI501fruh1s67BTpgM7T6rGqhVBT1zraaBhtnZcieoGNXg81IwBoL3+UxeYyU12Zs9JiMJHRZTE901/gs3I33aYqiaJr2ZS6EbDZrtVo3MhK/Ui5XR1hWtLv1PWJpkrnLYMJNIZVK3bFcrq5rmqqRDEsCpCqqijBD04QuroSiBG8OeF2aqugIMAxNkiTSVFXHNE2RBKFriqxolSYlSBoX1y4vqAd3thIAiZIMIGkwcABjTZUVDTEMS5EEwFhVFVXHNE0zNx3gbYVqlxsul4slUSJolqEIAADGSBIlhAHL8ZX3ZxghRVUIkhZL2cXFZV9Lr4MDmo4ohiEhBBirqoowoBmagBAjpCiKjgHD0NStz55Op81m8xYpTRqLxTwez0a+iTFSFUVDmKYZiiSQrquqggDBMLSUjYfTJburxmExKLKsY8gyDEFAjDRJVgmSZhkKQqiriqSoFMMxFBFfGo9qrt4WD9ZVUdZImuYYGmOsa4qsIpphaJJASFcVBUOSZRniJgvjIS2Xm0qlvqFcLsZIU1VVQzTDkFAPrYUURPp8NUCvvOOHNE1TNKnKio4wwzIkQWKkyipiGJokCKAVzp4e6d2/R2ApRZY0HfMGnoAQAIx0TVJ0juMIgHVdkxWVpGiGoW/IsXnlcrEiSZhkWJoEGOuaquiAY8hcMja3GOvZ0YNVuaJfSZKiaUrXdQAgw9Dg+uhSdcwwDE19OV82W4FgXdM0hCmKrmy3ka4pmk5RVGWSaqqiY0gTYG5yQvAG3HYb1hRFRyzLUiSJMRLLMstzlWsxQpIkYkjyHHtzt25SuVysyLKqXYtgolk2tTwRx/beZj/SVEnRKIZhaQpjpCmKqmOaYQmIFPlaCxMkxTDMjSOF3yyXW3lwmqJJ8laFT9EcQ1c+oRiWocj4wui6butvDeiqIms6TbM0RQCMtYrCZxgSAkVRNIQgAARJamIhkcpwFpfXYVYUVceAZRiSJJCuyYoCCYqhaQiBpiqqqlEsR5O3eMd8g0aqPKys6RAACAmItVgyWdbZjkYfQEjVVABJhqYqY0lHgGYYkoC6pqqqRlA0TVNqIT65km5qbBB4SpQUDCDHXetNTZFVBDmOuba0qYiiaZb50rjceLlcVdVVHVEUSZMEgEBRNA1hlqZIEgKMJFlHEBoYCgPl3GC4r7tOYKGq6ioCLENSBEQIK6qGIcFeG6RA15GmI5IA0XguL4PmoJ1ASNEQQRA0ReiarlbeYELAUCRFQFnVEQYsQ958plQpl7sJptLDxUZMpa8FY6RpOoQERW1U9SBdkTWCv6dMJw+VqbRRENJVVaMZ9t4y/TykptI3gHRNR5gkKWLDLaIpMiJohrqXHvmtNJVuBauqBsBG3AZuXIFESeFuXbM3yOaZSreRTNdVDbH3FO3xgBQIVmSFpGiSvJfxuUmm0lfRFAkTNL1hvX0zv2kq3dV9EckwG24KpOs6QgRJkvekb+9q86ZrOobExtsE65qqY4qmiLufJhs3lTYMLksaz9IblgVrGkIY3NvpTMVU2hKrzkMBhAR9l/khCZLhH3pfm82EIEiWrbbIlxAkRdxle1AMe+cv/dPllnclG7uC4PmN5fH7roEEST1s0wUy7JYbnxTzYPr3bu9LkCTxndi1EBLUXa5lkKTuHAr/3QENd5eaGG78gON2bAm3jypVqlSpUqVKla1J1VSqUqVKlSpVqlS5LVVTqcod2HjlyypVqlSpUuW3j39avko3qmE/aEHuzNYRcotIsqU67qE2Hx9q4av8dlMdnPfG1m+3LaXA74EvTSWEUDgc3sg1uq4jhAiCeIDBWfeMKIqV7DIPWpA7cCMtygMUtZJXiaKoLdJckiSVSqWtk1dJ179aUnGLI8tyXsnLUHnQgtwNGBAaURmKW41KXiWKorbImLwZTdMwxltn8m6ESgIeSZIetCBf8pt5lbYsW1YjbcFuvSsURTEajV+aSgRB+Hy+jVz5UCcLSCaTVqt1iwScfwOSJKmqajAYHniyAI7jtohNnE6nBUHYImprU5IFfMfk8rlySZSA/KAFuRswgBL0er1bcMm/z8kCvhVbIdvI3XKfkgV8G75NsoDvmC2rke5DsoDvlEqygC23GbrfbEGFezu2iKhbRIwKW0qYKlWqVKnyT4F/cqZSlSpVqlSpUqXKxqmaSlWqVKlSpUqVKrelaipVqVKlSpUqVarcls3xRpRlVUGAZSia/BpfEqTpWUk3smSprBpNN5Ui3IJgrCNdVXWSoiiKhABgjHVNwwBSNHWz2JqqYghJkgRIVzUdY0yQFE2RAGBFUQEk6FvL5WCMVUUhaZqAECFd1XTy2vevVeQBBEndU+GkLQLSNVXHlYq/uqZqOqYZmiQgRlhRFECQN9cZRUjXVA1DSFE0CYGma5qmAwBJiqJIQtNUXccURZEUuXWHyoap9K+OMElRJAExRpqmAUBQ1Jel3zBGqqohDK4PG6wqKoYEQ1MQQoCxrmsIfFmzCemaomoAAAAgQZIUSeiaqiMMIUFSFEmAG3f8jgcVQjpCmCApAgKMEEIYEPCmmlZYUzWEAEWT8FqUFsAAQ0jQNAUhxLquIfyVuXavYE3TAIAkSUIIVEVFGFMUTRAQQqDICgawUqEZAAAwVhQFVSKuIWRoBgKkKBokSYamAMYI6WVxxNIAACAASURBVIqmkwR5F9Xl7klmpOuKqhEESf/GfAGQuPHh9XphFEnASqtiCCmS/E6c+bCu6ZquQYKiKLLSgLqmIgzJ6/+sfKJqOknRFElACFVF1hFgWIaAEGOsqYqOAV0pmP3dgDFCmqIikqJoisQYV6YMSdHXZuUNjfTNCxTGqqbqOqYZmiAIrGuqpgNIXFN9qqIhDACgGIYiCPDVqUqQEFwr5QthpdgwxkjXdYxvWWIqVdoIkiAJQtdUTdcxBgRJURRZKVxM0jS5OSsp1jUdYXCt7zDWNA1DSFRC3a+Vfqdo6qahhbGqKoCkKQJipCuqBgmSoSld07RrIXiw0sjf3IyVhrr5Ka5VtyUJkiAABJqq6xjQFEEQEGCsqDoGkL3JyMAY6BWNQZEUATHGiqpDSNAUAQDWdaQhDACkSFhRg5Xfr6RVIAkCAIyuzXlAkSRJAPVaqTjiN0vdkT/5yU8qf0mSxHG31KxBSJclSdV08lbNhRDSdZ0kyUpsBcZofDp8ejbNGjgTTSiaLikIQEhCiHS9JGnlRPKvTodcAv3h8SVXwGphiIKoSapOf51A9xtRFDmOu11wryKXV+YnRycW8mVFsFhYilTF0vz0XDiZt7sd1HWtqsni9PhkqiCaBCEdXhybnF5eCZU10izw+VRodHRyYSVisNqN3LVQf4yxUs6eO3WetXqMNF6ZnRqbWcgURIfDTgCUTyVmp+dLkHOYv4yzuJEs4AHGIVcitDeSsAAjPTQ7PrSQrPO71XJ+bPjqwtJyGbF2M5+OrV6+MhZPZnir3cDQEAKkK8nY+ujIeCiWBjQvcMTqwtzoyHg4ngIUDXV5bmZ6Zma+hKDRZGRvmm+iKLIsu0UCs0ul0obqzmJczKVnpyZnlkKyBs0mQzoWmp6YWI1kKdZgMnKVAZJNrE+MT82vrBMUb+TZdCw0MT49uxI2Wew8SyticWHiakhka+xGCCHGuJCMDAyNra2GFheWcxplNZKTQ5dnFkOpTI7kBELJz01PzSyuKQjYrJYbs0yW5bxaUMDmJQvASJbEQlFmWRpCqClSbG01vJ5kBBtN6LlYZHUlpkPm2mNiLBezC1OLSwvrgGZoqC3PLoVWwmsLS7G0ZHNYCV2Nzs8srotuj+Xm+sGERnhtdxsBh6VScXZ6OldWjIKglrMTIxOz88sayZqMhnI+Nnp1fDkUYQSrkWMICLEmT44OzC2GlhfnZ1cTNd6aXHj+yth0JJm3O+yEroQWpgbGF3IFyWqzMtfHZCVZwCZOUqSpkaXpS6OzqVTe5LDzNAUAQJqciIaGhyfiqTwnCAaWxkgPrywtLK8zvNnIM5oizU5NxjNlk9l8Q7b7p0BUsbS0MDc5PRPNlDmD0cgzSFMWp8ZXoyVBEBiGggBoUml2empmdi5RRC67WS1mBwavLC6FAWeymLhSJj46Pr64uKayJudNSk/XdVVVeZ7fXIEBAABgTZMXJobHZpYyRdXhtKnl7OTo8NxyWNRJq8Clomujo+OhaEojOatguDH6vpIsAGMk5pPTUzNTM/M6zZt4Zm1hZmpmfnk9abZaOYaYvHJ+cmk9HFpnbC4Lz2CMivGVy8OTobXQwsJKTkS0khoan11dXl1ZiyDa6DAbpGJ2fnoullMcTit5ze5UUtHQ7FIUUpzJwK4sTE5MzayurcuQMzB4cWp6emYur5A2i+nmjdBGNdKt6Kq8ujizEk1zgo2jCU0qTI2NpssIqOWFubmFxeW5ubmMDG0W87VasxhrcvHKuXMS57AbyMWJodHZpWg8ZbI58qGF4anZtdXVhcUVjba4bcbKLSrJAm7uVoyxWJamVrM5GdkEpqKgNEWbW0tNrWXyKjbxtKKok0uJ2UgBU5TAUfl84epseilZYg2siaUgBBgDRZYnlxNzkUJGAU4Tnc0Vr84lYwWFNbAM1lfCmcHlbKogIUhYDAwEKJ0pzqxlFqOFuUhe0lCpIC6Ec4uxwmy0SLMUlOWxlfR8pECyjImjblhkiqJomnZbUwljJBYzi4tLqXSONgoG5ssI7a+YSgCgxeXkaFIRGGIlnl+I5ceXMgokrQZyJZS8MJ+KpYufLBV3N9llWW0IWIuJzNGp1NRaljHxLiP9HdtK32gqofDK/D/+/Gejs8uTYzN8Q3e9g12ZGvnr/+9XkxFl3yO9HEEAADBGayOX/+I//X1EYzs7Gi5//Ou3Pj23Hk8L7oDfRv7d3/x0YHzq7OmLXLCzxWu/NpSRNnTq3f/l//zbnkeesIPUf/x//3O4KA0cO+7t2WVA+c/ee+vVf/yUr+/sqXffEOUhMpUwxmI+/F//w79962r+pWd2Tx779b979Yvk4uhQRN3dVX/qnV+9dXx6bexiwlC3vbkGQljOhL/45O3XPxlYWphbjJc6Gu1H33rj3Q9OigRpd7sjc8PHTp5bmp2+MB5yeWtrPbYb934YTSWkK+MDV95++/3hyan5xURdvffKmRNfnDxz7spEERg62xsYEgKsvPfLvzt5aWh65NJsjKn38r/++3+4OjF26uQ5Q6C3wc1cPXbsr//6L+eNPU/0+CGEAOBiJnL6/JXVhen33vgc+dvrzdpf/rt/Mx0uIkA6XY7FodM/f+2jubnJeF5s7+ozXC+NucmmEsaaUp4bGfzg6ER3bxuJ5NDs5Js/++XA4Erjzp0gvXbs1V8fPT5h8TUEg3YIAMb6yNHPjn82Nn51cDFSrnFbw8tr0dXV47/+YF3it/U2hC5d/Ye/+KuRZfMjj7ffvAbcg6mkiPnhc6f+6qev5YGhs61p/sqJDz47PzZ4ZiqMm5pqT779qzND84uj5+f/f/beOzyP4zr0ntn27u7bG+qL3jtAgmDvFKlC0VRzi+0Up9jJF8e59uc4TnydLzdxnDhxruJeZVmyGiX23gtIECQBgui9l7f37WW+P8AuUSItUgQT/J6HDwFyy9nZmTNnzp4zRzZX5nsMJAE0ubP1RP/ozPE9bx3vVR5bUfrGf/1r61Ty8vEjmqswheLeeulXJ7sne1vb7IUVOW7L7F3ut6mEuIj3x//ynfNTieHmxoizoDbHDRGKBSaO7Nm2p7F7uKfbx+NVZblcaHr7G68dPNuXW1yR6Wanh9p/8tNfj0ZBWVmxhb26gcsDUyDI13dl7/6jHQND55paAWMtzPNEp/p/+ZOfnO/SKioKHTYaQjTacvzFV/YPD3Sda5tauqRm9MS2Hx9qS45e2dMWfWJ5xclXXny1sXe4s70nSa6rK77+Zh+cqYQQ4kLj3/2XF/2R0KEDp4qXLePGLv/wF29NT4w3tfaVV+S3nth/oLFreKindyJaXVPFkjemyVtMJU06vevNfSebm86dD2mmXBf5+q/eHI9EmvYfStqyS9LJ7/3NN9sCXDIeLaqsdZpogDQuOHDqfPvwQPfO7Udxe26eM9nc0t1++dKx0+2ZZTUFaab+tuZf/GLbDE8taigjIQRImx7q3bXt9d3HhtKz8nIy2Dd/87PDp5qCEc6anosH2l56/cTkxNDO3c3Vixc4rcbrVt3vYCohhEKTA6//6meNfYGi6gVuFhvtav7hf/ynH9mzXZaRge6B/s7t2/Yk2Kzq0jwTTQIAENIHWw/87f/7bdvCDeVO+Zvf/HcOYF2ndo2RxdkocLGja7CzdduuM5lVK8pzrqrud5tKHMc3d0x8/+Q4T1ILc2yzPgj/VOCVS9O9M7Ezo4ksl6mnf3xXT3zUGz45zi/Ituw43N4Y0EbGfefDcH2hDUKIkD7YM/IvJ6YCSal5nFuQaTzTPPj2EB+JJqY4mMWCPc3D7wzzBIG7LUyG1QABCkaFbi/XMRnd0xPEadpKwuGw0DwQODAUzU8z9nZNHBjje0f9XQmtKsNipK5+05g1le7oTNY1lYuFGGemUQ20tY+uX1b2gc3Ox7hD/UGDzWzkk50RmVLNr5+bdqfapASnKRqQ5f2t3qKq1EtNo17KyHlD+2bUNz5dOoeyvxFiTdalGz5O4omzF68gVU2G/Z3dXVORZEXpjS8IfNR/prU/lIiVMgConD8imszW1JSMTLdVCY52jUoLFqSXFDU05KeS+FWXUmx6YOeZ/hQXDXQ96B8LUa5v/MFnjvz0/zZ2DBmz0Pn+abPT9NE72O4XuipdOH4kghkAgQEknd1/NLNmY5qarF+/iqaw7LKG31/A9B7foytXt0eTeEGUtLLly9Ik/0gkGg6GkrLCpmWkp6XarXYML3zhE5WM5P3Bq2f9wbiKAPWoNswsyJGZ89jTzwcmevtmeIRAWc1CT37huRMXKEVFOgAAIE2IReTi0nqr7m0LCdGxS13TYmVVdmFZw4LiFD05frx52GGzomvWA4SYK6vkjz+f03Zqd/8M+bknauOj7THeXJaanuJMp4TYUGc/mZZbn+fKqV1mMTwoy1KWxLGu9s623oGuSG/7QKqVGO/p8ccJZxoNkDTePzw9FjaaPQBAgACAACr8wMBI3rKGyjTh1e2Xw0L9yifWxwZbelumNm9dZWfldw5dYK0uEd6HfYBCU6O9kwEZQzShAaBb3LnPfjx3tOVsZ4JESuhyj3fj73+hwDD67Z9dTK6tt7IUpNj1Wz6/PD559tDZv/jKZxghemlS/5cX/7Dj9R/sPd22qnT1wjWP1ZP0ueNHFf3DS3cHEFIEfiZGPfXJjaELO8LBOEIAAD3kD017hc/80WejnY2n+3t8sYaZ7t6RyRmzLRtCJMSCl9r7/XEulSEgmG3pBwsyuVY/ucVho7a/9Jt4MBSNhC83tyVEnnaT19zu4NyFi87UVBNBrW5YZDUyvrTSL31hbahl33inrGjKvsbG2g2f0gV81aq6ByzsVSAAOATrP/lHmUbp1d+8rSjIZbW98Jk/lEODJy8MqZApqVpWtT5loPlEc4c/lJCcdzDXFD7R3DNlNJurF+UsbSg3m5hVm7dWlGYf+q//uDjhjwcMfmApSrXbMwudrAEgADHCkbv4839QceHYzt4Q/rlPbbAb4Gczyw/v3YmlGNcsKIj6R3p7uuIalklgsy8PAbH7crd/0m80FiAAdCkST0KjyelOyUmzmUcPtWfULHp+Zf4/ff1rHZPh/AwX8zt7GxCSkrGu9o6pSZ+1rBQCkAjNtF7pCyWlQgNhzyvdUlHS2bhv1GfcunZBio2ZPSUeGN+55xxrNRMYpsra5s9+cd2KsmM/Dxy8MvLFv92SVVV3cvdrEbJuy7LsO4uFpnzxwUASMxCGmxZAkKY3L/AIkdiefh4gvWM8UZuXvixd+9Lbk0GOHwtq9QudjqT2WlCZ/Wam63pnX4i0sh47W5brQJo44BOfXV2eKobeaQn5U4kYr2aYjHaWdJhICACAWHaGPcNtPHRBwglybYm7PIWpl4UfRxJZWe6aFHZ7t1KVk2pPwqakqmi3735+RzWKE5TbU5RpI5K8bLWZ76LdAQQg08ZuqkrfUGrDIQr7E4LBsKoy48/r01ia0GbvpuspbitLQQzCpKh+8GU/SiDuSMlcVF8UD8zEZAOtxPq6OkJJbcmSOhqJswFJmiJ2NF/UTM6CkkxS41RJyciv2PDkJjea2XWoeXgyyCdClKvY23V0z7leUdYQQqoYP7BrX83qp+00kiVR5uNGgsUwCCAe4OW80uo//f3Puiz0B4s3N0H6zED72QFly7JSWdckUYgI2Iyfq8mn/uvF1yRoqlu8KEWdGeNwOwVVHSGEGIvDZXeNNZ643Dtjd6YZaaaseuHHnlrtHeg9caI5vbA0xUqfOHwJZ8w5HtdH7XW832AEnZdfUJLlCE76MMzAWuwVFaUsgRKcZDRRAKkIAIAZ83JcQ/1XDp7oTvc4SRgJcAFbSs5026FdjT2qIfOvv/HFujwHBgECAFwbwiIfP3Lw6PpPPOukCZZmVzyxuaG2oPfisf1nRyM+HgeYIopn9u8dj4kPqORBMhI6/NuXd795tP/8+bd+uX14Cm/Y+NTzz62ymCgAqYrVq5/5/NM5mZYbJ0DcYmZj/uDkRNAXEwVJRUhr3HUic+mi7EwnTlk++c2/WLuwgLgfARj2jKLnP/6xFQtzSKgAgBdW1uSlYJOJKGYAuCxwOmFgcIIiFS6pazq6WhcC9TUe4rNqVld6MJJyGkF376BPkhWBo52Z9YsWid4RAXNQSNcfUINCSJltFcXMnp37Lw+hqpxUABBAkDQYDAZibHjUH47JkjjW3zfhC2fml7poXBL57itXJMRk5+QRSFU1DTzwAhcwIyevKDt1+ErLaFB2pzi8A5cjwFick20kgaJpsxU2FIGb8CeqS1Ne+tmrk6F49ZKVJSnEpcujKW63rInJSMQrMJmm+H/++O2PaBd2iLGu/A3LyscGegRTGoX09LzamkLnyNgUZk4xGdjC8mLZN3KpY8CY4Um1Ge50GVWTtWhYIJ14YnL34XNRlV1cXzLR17J3JLK4JAsjqCWPbdq6cV3frl8cuDIJrr4MxMWCTecubXrhM3YDBEjzeSd7hqaXbdxIyvG+nv6ETC2sKhBl5Vqgj2HF5qc/8cn1GQ4KAYBUvax20aanntD8nfuPtfC4MREKjExMIUgEk6KGfnfLHWnKWE/HREjMqlhgJpHER9taWnSTPbe8AEJN0zRVjJ9pbFmwZkGOJ3XWUNAU4fju7c76J7LTTaosETbPk6sreptP7TkxvW51FUR6PDRzprH/2c9sMLzfxqcw1+N6fmnuogwjjm5UZElJsVZ7WF9MxgEgceA0kqGYMBYUFUHhdHxZtrFxIHBwIFHvMUEIAAII6WFe9XJ6hR3+8tigNyklNZRqpDUA4rKCE7As27Up3xzxhXa1+5VrgzYZTXb6RXeKrcjNAgBmJkN+CZZn2dxWpjKV6RoNHhiOZdmY657469zRVEIIySI3PT0d4Ymq4rvYxRsCAAAGIQYBBBACQFAEoeuxpDgZFXUdzf4jkJLfb5rOT3OsyDHOuVIFSOcSkcmwuGDF2ooMw4GdB0eHhoNJTIgFZ8LR6Rm/IPDhwHT/jF9IRDBdGZ8JheJSaU11w4LapQsLk9GEBjCatldXla+sTxsd8osCH40lE8HBxp6oSQ8kRHV4ZEQFpKBIsqbLquo0GSnGyFKPzHa67wbpysWTp01p9tGJgBb1DfuSNhrzVC+qXrxInx4Nx+Ljk1POklXPr6s5e7AxIShcMhny+QLTodo1Ty2tzYoGxpO4vaSmbunShdmpLiUpBP0zxw/sa52IrlizvCQn7RG3lICuyaGQX6Asq1csY7no5c4BrzeYXlBVXZ4+PTUyHYxyHCdx/s6xWFH1smc2V06MDfIy5WTdZWWVS2rzpgZndGAwslfX6wAhRUzGk7yua8nAQFeAWVKeAyButKc9tmHVwqrS/AyL3xexuOxp+aV1RVm0rk3FHtTe3FZ32qe++o0//quPV2/c9Jff+sKiZZkGI0tgCAIAAG4wGAw0AQAACCBdFThBRETlglrFH7x8cQwoOEMRetJ3ZShZVJJlZA0AN1gsNITwvrhFaJZlaAYDEEAAgOadmkjAjOe2PuXr6ff6YzjURFGRBJFgWQzTY9GYoupI4Y8fOrn06Y/RODQ5XJtWFB8/cKx7WjTSrMLFvMHYgrXrFxZQx5q6HtQKDyEhGuwYT/zep15YXmi72NovyVIimbSnplVUFnS3NPeN+g048s5Mj457oS7P+MIzYwNdg1OBUBgp/PSMNxiJqw/O6XUNVUq2XWzce+pyfsOK+prc7q4hLhZJ8nIgOB2OxePxuCDJFGHIyi+sqqlzK4mwIE+N9Mc0x5e+8sXWQ9sDIsYazHW1VZVlFcL05EdT7QIhJMZ9o9OJNU8/vzSV23myNxqYSWrGJzetcyV7m7tmJoa6dx84HmMyn3x8vYW6swcBJwAylRUXrVuenQhH4kl+uOvCiy/tqVj9xLq6IpPFuXr9ioqKsgXp7n5vWJb4eILXNTXoneiKsxuqMgEAqizMTM+EcPeyIncsMDM2PMhBQ8jvjUYiPl+E4zhR1hmWpemrH1IRwdbW1SyuX1hfmZ2IxrPqG2gxdO5Sayyu2Fnqw3yLUMXw0PjwpD+EqeKM1z/R29o74QuHErqgTI/5IpFY2Ds0oxgL0lPMNKGrUjyR5ILjp4ajDhCLi2Ckt5+Tpd7W0z/96bbSrS88tTgXaap/tCtsyanMsL+/XAYDSRuul/pAgqgIkhqN8dNxsG6Bh9alsZC0pNDJxfmLg3GJwAyY3Dia3FiW+lyZ9XRfUNP1eEJUNGRh8JxUW2me26ZISQkZMBjiZaQhmsStZqa2JG1piTPDQfEJkRdkTlA0XZ/wJzCCyE01URhAuto9HrPZ2HQ7AxSlfZpfmOf6eKltOJCIStpti447foBDuhoLeyd9fFFRniLJBuL93B4GmrSzyEiTDqPGEjhhIG1GzJ5qLfdL/WPhAYm3MyRL4alWxmAwVKUaZ4IJMaFnG4mPxGF81yDVNzX0xo6TZYXF0aSWX1KSnooSwzNd0XicMEcj/iveMVGDntzs8bGpcDyJMD4ZC1y81Gpwe1BsKjOnKDOvIC/17OWLbfq0VFqZoUWG95z3P7Emt6Gh2Dc1wSsoEo9b3KUM2XiutX1KxZYXZkB4zQU5Z5rhHoGeqipu1DsdjSm8FJHx2lUL2y41XTa6PRWlJEoe2ve2klrr5H1ZhVlSItjR3oYYp6pq8URM1yVIUb7poeGeHoJ1BuOCM9szcqV5/9GLmTWLjDRIJJO03TqHEyY/GF0Re7taz3ZMZdKURjEWUmw+cyIkE4lA0uLOwYXQ+aGerBQzxFA4HCIMOtKROa0s2zLR23o5MSEUV2UbDOSNDgKBf+B885Rjy/rymc4WNa06xUohVZge7njrUFtVTUlAxBYsKbYm1MGurjbZwThcWdYH5bDECcLmTskqyKsQHC63nSYB0GQAr66JrooMAYBAF+KdbYMmd7rRaM2ryBfCtCnbmOK2Jia6Zcbsdhlvzhu5T8bS9ftDgNT2C2eG/SjFqllTnOaUrMpc22DrFb86lVNVw1Dy/h1HVz69JQ0Pnr0c/rtv5UMIIYSW1Px6C5WcvALzSwXv+O539qdX1sSjekFR2oNLy0Q6ghLh980ISIeaFpoZudjaW79ytdWRWlVFxsIRwDiK8jLEeGxseCCeFCUJZOVkjE1ORRMJ2cCIovTgi6aiiaGubXsOJ8j0JXZWSPKZ+fnjE9MT8WQiTkmi0Hr+pDmnJje//FLTeHMrY0jPSzHR7ftf70M5VWkwNbfMwTKLFy9qvXBZS9fyqkseRAj3e0mtx2d6fvvGpYaltT6BLsiwjHU3H24NFOTYBcZpZvgTBw9d6glu2tqgc5GkaDXT7718pWhTZWXawMSoMB7IyCmg5OCbr7w9Ay1PZ5imgzGbOPSLt849u375sIIvzEuZGe44NyS9sHFRZLKXMhZaaAJCoIhc1D9ptuawBNRMttSsbGFsYjielI1ixOf1j0cZe2Zdaf71YSREJ48dajI4UsNj4czcApPJWFxeCjUlWJqoznZRxIf4vA6JzKxMf0Id6ZqIJ6CoYHnZGdOTM/E4DyAnCZJvohuzZRptDgwCMTJ56MLIwpKs5XWV8XAwwSuxYDgZHPu/3/tRzL24Nt82POorTDeNtrQ5yzcY72xr3rj5rG6AQNf07qEAMFBA5M9NJFMslIzhDiNJ4qjMYwGqtJg0ptE4ThKhhKyogMQBAMqBcyNL6nOKcuzbO6KXx6DZafHYzPlu+lT3dDWt5WdaEvHkkXa/y2FK8MjjZsZ94RAH6grso2EeJ0mPjQEAIFnpC0opWXa3iQKqCDA8LkiUBiCGo3fpoPcJ60YSx6sIKIoMcMpsvNGlbwvrVjQ9KqgQwy0MyZCEiSZ0AAiSsLFMjo3yJ5VUp8llpt0mA0PgdpupzEZO8WhJoYOCsCzD/KFe9r3zfmHdECdJCsW8nZ0T7pyizR/bWFpSWl1VZjcas7OzFtflt7a0ccC0Yd3a+roaE6aWV1bULKyzQrmzZ9AH3B/btDw/JyfTgbVd7hEcZZ/YtJgRx36x7cqTWzctXrCguroqEfRt2vJcfqbLqgqtPcNZ1Q3rF9dQOFRkmecFT15Rltt6XZZHJawbYnhmdkFVdU2By5Aw5X9qw8LUrNzYcNuQT9r4qU9UeFxGUmu90KGTlqeee4qWQheazpCFi8oyjQNdfQncuGDlyhXl2Uos2tE2aMvOX7miOuHzJgQFAygQjLnT091O2/WZ6VEM68YwgoIgOjky7OVKautWLF2AqfxQX69KpSxdtjjVyJ+51GVyZdfk2UaGR6bC8uqNmyrKKrJSiN72Ht5S9MLTS5xmGkIQD3kN6aXVWU5//9EDrWD10qL4tB95ipYUZ2IEQdJUZLS7Y5LPrly8dUO9zWZKege8IrN45crKnJQHlwEHccLuTqsszyWvphIjiRcQQWUW5FsYXJMESSNcnnSnUbtwvl2nTA4j0dfaNR1Slzy2tCAvTUlEeWiqqMhnWQMAAEIoRiOqKaWsKgP/sBlwAAA9Gok4XBnZWXlWMzPWNzA6FWp4bH1lSUF2hrnvcpc3YXj2uccy7dhvf/J62YrVdoM+MiE/9tRSFoMIaBP9PS09Y4b0sheeWG42MRoXbe0es2UUP/3YIiN1dYV5n8O6ISRZxoQrrR39mMm99ZkNWnjyyJHT1cuW896RprYBo8uzacO60qL86tqaTLfVnZpSu3jZgpqK2tpqE0UUFZfWVpaa6KuyPSgFgsDI8JA/EDYQZNA7zdgzG5Yua1hYl2KGLk9FXVV+5/mDkjmzYVGNMDPeORFYsX5TbUlWust6ufVy33TiuedfKMtx5uVltrd0hDTihWefzXAYr1/7wYV1Qwgpo0Py9l3onnbkL/rk5nqWZWcG2gcDUlHDmoUey3D/IM6wQiwkqDAzJ9dyrRlvC+uGGJmebp8YG5uIUI9vWOWiuN7xuJOhIn4vZ3AsrCjWwxOXrgxlL1q+ZWV9ePjSiP6UfAAAIABJREFUzsbhTavqkhEvbi2rrUjHANQUiYvFzKllpfkuxmjJKyypKiswmy0p2QV1JdbLVzoERJfke1QxwWt0Vk6OJztDiXm7u/p5S+HTG5Zk28GlSx09A4FFGzfWl+XQ5A2T7l7DunGKTc3Mq62pTLWyaTn59SvX1VWU1VaXkbhaWr+wqqJIDvmBK7Moz2OhSTEysf1YS82CRcsWL6qrqVQ5/5Knnk2RvRfGJI+D9k9Pc8hSWZQWnp5Jq6grTr+lit+7w7oBAEjXY6LmtBnznMzlXm9SA6XZ9lhS7PbyJbmuxfkODCkXhuMzPNqwwFOcYvVYwJWx+JgEP7s0J9tGvHZ4oLg4vcRj5WPJgai6piarNstsYvH+iThmYB9f4Em3UqIkdUzyqW7b+krX1HRkICAWZNokSbWY2eJ0M41DXdV8MTUvw5rjZEgSczL4wExinEMbaj3lKey1qO6rYd3w+qfCaDRqs9nupolvK5fLS8p4gIsk5TuuBW/zHKEbf5d6rA7THT8MPwhCoZDVan2f8pbXG+S6akYIQQB0TZ4YnwQk7fFk4Ne2AAAAwOsPNJubdJPbThVCjReGV65cSNz64fY9b3FbebO5UO1ytlwuwzB3qW3RTX9mmc1sv/4zn4iMjQ4xWdU5VvJOx9zcgLe1STgctlgsc6Q06T0Vp7z5oeBNDSTz0bHpkM3hcjtuWMmzvphrW/zcMqgQAongyOAMqKvKhRDePLCu3QICAG5uxZuvEIvHJrmpJEjepdi/G7N5vNfvjhDSFWl8eJK2WFLS3djVQINrBwCIwG1v/JYuABAgRGJBXt3vsGMQQgjeNFRv3OHmMYiUi6fOFi5ZbqNJcNuQfM/jbxLjQZTLvSEqQvFwcLBvtGJpgwG+x92vP91tP8/y4BTIra/nukgIAIh0fXygG7OlpTod5LWZ5tYGvO0F3yL1gy6Xe4d3evOIvF2m9yyXe0d9dSvJwEj7mLisvgxc82/euMK7PKcIAUWIT3kDJGv1pLnAe/deeJt2vfkKv3u5XITA7XoGgVn/7jUxFT7aPTSVX5BvYhn4rj5ws3i3PSl433K5CACg65PTYUBQqW4zObtAgtee89r7uRZ9cP0m2uX2yawij4vBwbVchptPgfC2iUif9kbjgp6b66IxAG5q/Nttk1vvOMtsudz7MMJZA1nqucXGuqGzb+2D8F2/zkHerZHh1S4D0zIyIXFjz7TrR8I7nk41LF34blV1p1s86sCb/tz4x5sejWLMWfnlJiN1+4k3HfPfoylu47aHuv4LRjA52VkkRb1Xl3jP6wCScVVWmCC8vaFvvcLDbMWbteg1nQvTc7NwgsRu+++bjaabT7hPwHcN1Xf/F0CoeOESC3276/T9f31w3HQjZLRYShbU0Bh4T2X5sEbNHe41a6MDd1a+wWDA37Xx6VwY43d+p/cmz10+C844G+ot73nAu/8JQoCRhoyMDIKib7vybUP7nkS9K+5iPoI4VVJSTF37Un7np77HlgQAAeh22XACkrd+2H7XTHJDTARgfn66jcVvOvT2U245HQGX0+xAGPOuJf9t4r5Px3wgC/T3ebGP7jQICcpwj61Fshbyg4/6HwRBEKa54ROaI5CGew4kYkx3kY46x/gdxs5HB2awWj74qIcAxAiKvuctBR8u8HYHzP9kWLP1gw+6CYI0EHN1wiAM7AMawRCDNH1v14YQs5lvX2+//z0MdxE+9f7MibCPeeaZZ5555plnnrnJvKk0zwdwXz+JzDPPPPPMM88jxv84U+kRmvgfIVE/MubbZJ555plnno+YG98IEUIcx93NObO5f7OJnQ9MsAeFLMs8zz/EtLK7RJZlTdMAAA8xN14URQCArutzJD9fkiSCIGT5/lV7/RDIsnyX42XuIImSLuvvyviZ2yAANMDz/MOW4z1QFEVRFITQHNQnswoEITRHBu/dMJtbPaeGlSiK75/mNneYsxpJluW59lrvidl58JZwqndnnM4zzzz/nbAZbA7qPbJ25y4IiZw4r5r+hzDXjJL5jjfPbJ+8YSpBCFmW/cBugRBSVRXDMIqiPrDm/FwDISQIwv3dB+VBMLsWfOj7Ks1KQtP0XFg0I4QkSaJp+vp2cA9REgAASZKPVrLP7MhlMMZkMj1CXiUd6WE9fDeq6aNHkiQcx2manmv6ZO4okLtn1jmn6/rcGVYIoVmf+twR6T2Z4xoJw7A59Vrvidk+IIriLSP8bly18CYeIdfuLDcL/7BleT/grTxEMa4L87BkuE0YDMMeujBzqlnunlt61KMjONTnbmvP2Z4wRxTIPTEHBZ6DIr0nc7YfzvJItOGduC75I2brzPPR84h28XnmmWeeeea5L8ybSvPMM88888wzzzx35H6aSo9O/MM888wzzzzzzDPPXXEfqzwCcL362718sbm5YNw888wzzzzzzDPPnOK+mEr62GTk/EhkRkIAgAyHaUWhI91MvYf9c2sF3cnRqbNB/GMV5gOXfGsXZduZh59FgnRN5JPhuECzrN1qxgDQVJkTRIwwmNir5bqQKsficVGFVouZNpAAqeFwVNaAzW6jSVKXuWAkjlEmh9U4WzNSVYSAP6IDAAAgKMblsuqSEIzECQPrtFuArkt8MpIUWaPZZnkkcwQAAAipQV9QQdCVkkJiAACgiokIj9wOCwBAVeV4NGG2O6mrxRaRIkmxWEzHSKvNZsCBIPDxWJxgTBazmcAAhJBLxGQNGI0minw08nfeB02Vk4kEJ2lGk9lipCEAksgLskozRpq62ucRQromxxIiy7IGitA1ORyKqhjpdlhxDOPjkRgnGliLw2qE14qN6zLnDSUY1mS3mgEEAOmSKCR5yWqz4kjnkomkpJktFhNjeKhP/9BACPGJuA4xhjXiGIqGIoKsWW02mkDhaFxWVAAAJCi3004SOAAA6WrQH5R14E5LJSHQZCEQihEGxuWwAgAUWYyEohjN2G1WAntQKzuEkCpygUiCMjAOhxW7uuhEsiTGolFA0Da7jYAAII3jeBVhZrMR6moinuBExWq1siz9gCRDCMkiL8kaxRoNBCbyXCKRJFmT2WTEgJ6IRjlBMtsdLGPAr/XPRCSYlDSb3cEYSAAAQHo4GDTaXQYCQ5oWDPg1jHK7HcQDyQ1CiUgoLsiMyWo3s9eGjC5x8VBcYIwWu8UI4Ky253lJszusmizFYzGEU1abjcLvoRV1RQqGozokXA4bjmMCF4vEeaPVbmUZCAFASOLjwRgHEAAQowy0AaoJQQYA4ARpslgYEuOSCV5SjWaLiaGveRmQKktJQTIYGIamNFWKRmIKIOxWM0USipgMR5MkY7ZZWPzDtR7S1GQyEedkk9lkNrFIk+OxhKxjVosZalI8wcmqBgCgGKPNaiJxHACAEEK6HAwlbQ47RWAAAU1VQsGQ1e2mMCgkY1FOMlpsFtbwOwS5JhJCUlRp1mBmSBxCgPRoQjTQFEMREAKE9GiMxwy0hbk6kegIcRyfEJDJTJtpXFXVcETESMJ29QhdlBRRBhaT4Wr5Zl1P8nJCUHQATEbaxJA4BDwvCiowsRQFUTguyjpwWhnyXYMc/4d/+IfZn0RRpOlbindqqhL0ecNxwWwx3XyaruuapuE4jl9tO71v0Le/yz/Oa4IoXxwOMQxtxlCC42eCPCSxSDg5GUhKAGNJND4dmwpx/ijHqwCqQlCEmRb0/f0jy2vSLTTxEfiWBEGgafoOuXsoMDX81q9+cfT85Z7BEcKUkWKC7RdPb9/TKEFnQY4TAgCQ1nvh5Nu79u070izpZHq6o+Pswd0Hju87eDRqsGWnWo9tf3nfifPHznZkFxQ5LCwGoZj0vfPbbS2dnTu27enxg4VlKTteefnw2Yvnzpx251eg6NQbL79+8uLFjq6BvLIKM301E15VVV3XSZJ8iGmGs1uMfuCWEAhpV07s/PWu042Hd/uJ7Op8dzww/ebLPz7RrayoL5KSoSP7dr9+8Gz1wgazAQMAyHys5eyxX//mnbau7qRuSLdoh/ftf3vH/o7+UdLkykyzq1zo7ddev9QX8GRlWU03ZnpBEAwGwxzJu+Q4zmT64GKmSJN721veev3N0xdahyf9aVk5pBw9sm/n4XMDdndWqvOqcawK8abjh97cfzY1PdNhMxzZu/P4iVM7du+FaaUpZORH//GjK/19h3efyWtY4mBwCIAiJXf++mc7TlzqbB3KKiu1saSYiJw8sOu1Q+31dSXTvW1v/vaNk03np3yh/NIymrjaYpIkQQgp6l4qTT5sZjf4uPfNAjTfSM/Lr749FVdzsj0zvRdef23Hqcajw2GUYadOnDh+4cLFk4cP7r00s3RBuZGhAACDlw5+9yd7204f99Kp5Rmm42+//Kv9ja1Nl+05RWZcOLHrrTd2n7jS3g4duTmplllRNE3TNO3+DVIkC9G9r/7spYMX+1uuUFkFWQ4TAEhKhptPHvrlq3u7evpkwpiT7pga6nrlVzsHp8SKqpyRy+d27Nyz59Bpf0JNz8gwsdSsbPdVgaBExHd89/ZTl3oceaVG1X9o34Hde450Dk5b7Y7YSNs7u/c2Np7rGgt7MtOtJgZCGBhs+f6v37zc1Nw2zleW5Boo0H3u8N996826jUttFHZh3+u/2nGg83L7jGSsLEi//mZntzVmGOZDShvzDr74nz/uGejbd6qpsmaRmSYAAEIi8PMX//1cS9eFpq606hoXg3MR377t27Y3jS6tzbpy7sTLr+y+0tUjQSY/J/16k8myDCG80wYlSBWP7Hj7wOmmA3t2MZnFKZT4w+/+pGXg8pFj3XWL6owGHCEtPH7pjR1HLl9u3bvr6GQYNyVGD5w6de7MmaOnrzhy8jjf4Nvbd5w61jg2Gs4vL2EpHCAkcdGmk4d2H2w3WlPSXdTpY/v2Hz66/+AJ0ZrmZtT9b751+uyZXQdOllTX2s3s9WFxlxrphvBIH+pq3b5t2/GmC4PjIZPFMdl/afee3UeONvOQNcjRpsbT5y8079y2czDJluZnmRgSAKAL0eN7d768u7GufoHJQACAxlqOffUbv1n85EqS9/7w3/+tqa3vYvtoeU2lkbq6yp3ds/oDX2vAG3qlabxxKNQ8FndbGacRDvbNfOf4WLrLlGo2YBhMhsP/Z3uPbLaUuRgIAUIo5A18/+hIx3Tk6HCyNt14uWP0p03e3pmoTFC5dsrnjbx9fqwrpJR5bLOyyJJwuHViV5t/MCKRBirVQmOquL1x+OQYl+VkJodmXrnsO9Q5o+Fktp2hrppXQJZlVVXvOIp0TY2Gpif9UV0I9o+H3v8hVVWDOkhhqTyLgdYBDlBT98R/HRnY0R260j3+kzNjOzum/nlf32iQ6xqPHev3/vOOnre6wsFAZO9gFCEUFVRNnwORTroqyqLmzt/85AY7KTY3NXa1NL350rbu/slwVJw9RBPizVdGGHfuqoqUro6e3u6eI42DvAZL6+prcjOJ2MTJFt+SNesXuLz72gYFRQUAGIyuJ7Zu3bKhfmrSv3BxZcQ7cqJtND8jtbJhVaoRjg519Y6Fc1My6xoabMxcrSv9viAh8vrr510ZrqzixUsqMpAS+eG//ldzV/9YKCqLyaYDr/32YOvUcEBRr75iWRA1CautW+xmDF3tA1ODQ35vZMGypQZN6OwfElTlyrmW802XpkOR2TXNI42uygrSMysWrq+rFqe9l7u6Tx85snfX0emZoCipVw9C6MShbfsOH20fGE8KohToP352TDOYaurWlafbBf+Mu6Bh69Zn3WD45NkhAAACSAyNHTw3vvmZp4qcgd2n+jRVnhjpeXnXqclIJO6b6WppndCNJYUFVbUL2Y9iATLnCE70bd9x8PDplmAkqunylaZm6PCsXFrX3d3hTaLVazdsfnIdF/AvXlhpZA0AQoiU0ZnQwg2PL8rSjp7v0WQxKokbNmy0JMbbR7zBiYl9R3pTCwqLy+pKPLYHJTRCfNh38MTAps0bPZbQqdbhWaUoipKkE/VLF7uMoLNncKq/fd/bO0+eH/D7Y6oidbQNQYNzRXHW2Oj4qD/yICJG5bj37LFDr+88PeENCYo22dnlDybrV6+ECX9376A3JpRW1219Yvn0UP/QTFBBAAAw7fNnFteuXlrUdvE8J0ide9/4wZtnhnr6RE3XNO3w3n0VS9bXlqXv2n/q/osLYDI07SlfumXrs+pge8vwNAAAID053XmqD2548jEDP3iux6vJ4nD/lW3HL02GIuGpqeEr3UUNS3Oc5KULF4K8fpd3SoYnj10eNBvIqqVrC9KdIh8RXVnPPr6+u+VUOCkCACDEbZmVH9uyeVFFjj8SWbmmvmjR0ic2rve4LKrOeGxopLd33I/llZZV1dUYZx3yQGg8dHDXW3t7B2fiSZn3dV7omBQRU96wtNST6ms53hNHBsa8ZuNGx60ujHsGKZykunPKn9ywIhz2Xmpp6ugYZh3F9WUpVy5dCiv06g2bVi0q5xVDRUH69SXr7t/8bO/Jlo6hGVnVEQKqEPr5D94ZGvVJqirGJgyZxWtXLgx2nZvh1Pe/+bsJ8WpKiuXx6nSYTA4GuIvtYy9fmWmZiHOSihBCunawabhrKh4Wr04Kuo66uqamNQxjmMdLnRjUIwreUOD0EGrbVNwbSOw6O3R0ND4Rl7Vr+5qKnDga5PySnuEyeuwMiek9/d7GgeBIRJIkNSzqdQUphYzeO5PkldstkjuaShDDLfbUPE+KKvEJ/gNKSSAAeF4amIxcHgknFB3iWJSTKIZZX5Fak+d0Wg3D3njTaCggoMUVqUwiOalja4tsiqQEOBXdfJWHC0akZRY8v+UJhwFNTkziRmtmQdmTT28ozzZfF01XlVhCpI22nBxnMhaempoKe8cCCX2wpfVK7+j0jDeGm/Kyc/LTzePt06qsAQBwgs7MyfH3tVmr1qytzkoGx0c6R6dF8sKJI32Twemxkc7xYFASzp5oDHLyQ2+D3wGJ40KRnv4xIdLTfKBlGELisedf2FyfqmAAEobsyuV/9omVlHjD6GGszprFi7McaGR8LCUrw52RRuDa2ROnZmJKisPFTfWPRmI2l9NhfCQNx9vASKa4rHbTqgYNCd5k3MiaKhuWb9q0Mt1K3azmiqqWPfPkSrfTpCEU93V1T/YnFdB9/kjLWMDoqXr22fUumm/tCtrdFgAAQCgZ8idIpqY4N81pGewbCwR8Z08dW7BimZ2QuLgw3DUSCoTGpwNnz55PKner9/87gdOODU9tXLk4j8ZlAIiCwqzpieHDh87YnWl2hzMjI0Od6AK5y9YsqTDSJAQAQKJh9VOrc5S3L40triomWeu6J543Tbb3x6miTCcXD4Yio5MTkcH2i63DgQdle0JImWxlucz+vYdbh9Wq/HQIEADQZHPVNyxOMwi9g15nRp4lxbN644YVdYU4RJAgc3NtwcD4oYs9tNHispofhFwYwVYubHh60wq3kYQATQU5hWQKS/PsjB6PJ3Oqly5bsliOxxIJncLw2e8WRTXLn15VfOrgWU9JNUNTlqyqL/7Jp9LMSQAAhmGLG6r2Hzh14WJncV31gxDYnVf3zNPrrMjbPapaWQYAACA0OHNTtPChg0c74/SCHHvIN9NyrnXp8kUMpsmixHGSOyPdbTdFY9FwXLo7PYy4mG+iqz+gsBdPHu8c9TKO3D/97NNNe14351e4rAwCAEBIMvY0l9U30Fu+6dNVhSkWp5PBdX84tv4Tz1iANDrSMxGJTHunmlpa4pIGAEAAK6pp2Pz4kpw0FgEU9U8PjwwmRL37zJmeofHBXv9g14CO4Tvf3u+LJD7M2IaQLCqv3rh+BanysVicJGCYUwizOzPNmYx4JU1LTXWN9fVVrFlTW1lIXwuEKF6y+vMvLAcQRwggpO955Ud5m7ZmmZIAw60Z1VufXNd5+VzCVZphJO51LsvJdDxRlZaCKxMJFWLQbrf83lJPiZnEAUAADHePjgKmxk3iECCAAAA6Ugdmkp1+3q6J71z2QsKwoiwtjxDPe5XyVLPRSC+vyNhUaJHQdcsCJTmFgDDHjLX2+84Oh0OByDm/RJoIO4tBHF9Y4cnHhIGQnO1gr3vir3NnUwlCgiBJDAgKAKr0AY0OQEaa7fc3lH7rhaotBcYBb3w6qaRY6Qy7ob3XOxVTXljiKWUIiIAYDOwYFv5kbWFlKgtuCwB/+KtfSBCkEJzYtu2dpKn4qbVLnakZhaXZRuZ6uAzCGUt1obX74tGXdpz2hnhMB2LSuHjR4qdWpvV2jwZDCQQhBgCGY0jT0dV9VBFQont2Hd/68S0shesQU10FW9cuKaNRY88EoMiUkrLHGqoZMdgzEX6YT/8h4ONo4+aNW58oObHnPI+bqusqXGYKAUAQZE5hWXaaHSIEAEAIIIQwnDDandWLlyyrr/L19fRNxXScLiwttTN4PDR17kKHBilPhlsWBUGU9bngbvwQQAwncTjc3nzgVLOnsn5heWFGVo4nw00S8PoQRgBk5RblZmVSJA4QAAhZze7lq9aurHVfbOxSAanz4//05R+lLH92Q3UqAAAhpKkagAADAGK4nIwPt18a5LNKM6yarCSSAm4wF9UuWlWZKwe8Pd7ko92CvxMWhzuvINdpYzCgA6T5vWGXK7WyslgRkqIg6rpysLG1YXF1msOMQYgQQgBarPaMgupv/NWnz76xOyxhztTMunWPPb8ud9eBc5KCaNq25dl1pVlsS3Pvg1rQIKBKQlBUFtTU5NhYny+kz+67jZNWZ8rCpUtWNpRNdrYpjCOvIM9uYSBAuq5FOcHmclWVZSCNT3ICegArTpwxp2fl5KbbKBxDACgIaWB2A2IEEGIYduRK0yvbGqsaFhXlZmAAIIRYk8Xlyv7cFz4f6W0eDyfSSsuKstMpXIcAIKTNBMerqkvz89IDM1MPwm9MMmYlPPj33/zZ4udfqM1zgdkgsERYZNnKisoMgEYGxzuaToVcpZlWRpEVwmJzZbv3vP7bg42XdBXdfRsiiBLGjPWrl6/LMJ3rGtMgmeKwb/7cl4uliROdEwAhhADS9WjIf3Y49MLjDRQOVFmcnp5KQtuqqiwIEE2byssXLizJF0MTU4EIQggAKjM3N68gnaYwAABCqtHobFi6YnmVs69zIhTkLHllax9fl6tOt40GJfVDGUu0gZzqb39t7zl7dsXqlStKs239Fw9uP9gYigsY0PmYt2syXluSnWplrwbNIVRUXpeT4Zr9ZhroP3uwnVxSmY5hejSawClTZmbOk5u31ph9+5pG71UamiKTgcjPzkxmZjiqMs15mc78FJORwCAAOpf4xcVgfb6DxgGXFCXt6rwKISzLca+pSJd8YR8n221sVVnGUxXW5m4/JIjiLLuLJRAAAM1OPcCV5vzk2pI/3lCQayJCM5F9l2cYDPdYaUVWBUVjGCK/IP3z9SnNI0Evr9xWYueOkdS6poQDkxGZdbtS+oZnAMh9/+f0hpM7W8cbDXBoKl5bZWEIDMcgBkGSk3kVxvzJMVlXFeHX5yasFnOxEU4HeXTNOoJzwUwCAAAU9k7seXunnyr8i9/bmuU24Th2vSyArojhSAxheF5l/cfSiuMTV1omsJT0VLtFhxhmgDrB4FaXk4jHo4LsnQyml67QxdhQQM7JzUxMjzRF7H9dkQohMJtTrIBTSAONQ5ZhrJiLlUcxiqVxSJIYQHOlLe4eg5F1WSxxQWcMFDQAAsNIkph9CgghThAQAAgghEiW+HAwJAjCYE8Xk1NuMZqQGJmeDsQFffGGRX2Np4LTk4oJGxpom/H6kqq1orahIMvFUI9wZDfS1ZGetp1HztqrVn3yydU21oBh8Fq4LpD5RDDGG80Wi5HGsKuBhKaUEoN0hQQ4TUDcYFC48C//7UVYueR//flWK0MkQ96QiJmdTiyWmEpIsYjflbs8Fh+PzwweGEuOROQLQwOODDbAqYSBNuDwv0Fc/O8AjuMQ4BBAAAFAwvDohN2zqKHWfeHnh2LhuGKJdE/i9c9kGkgCaMLIyIwr1bX/7V+nLvtkTZpbCke48Myene+s/fjvOaxUYkRhbGYjQ4syoGkKonetN+8TCOlcJDwwoXziywtmlKH9Lf3xlQXxaBwAra31UnppvcXM6iNBgOE4flVva7I44gvSVveS/LTtx4Z9/qhemHbfxYMQwzH8WuQGTLcTvTOizxeNSqSTZWJjba/vOJ6/fM2WJ5e5zFRwZhIw1o7TexPmkhUlNkmQEUAERSnStYAkXTrfMbD1r7+Sypn3/uAMB4D1PsuLxOjUj773fUv1+j//7BNmA5kMe31JHUxciOKeJYvrkz0Xmi4M1Fl9kwO9vdF4QKIu909XN6xw51cO9nVNhJHDfLfR8Uajy4bJOklSBKQpYrqvadfl8Jc+vZGRRUnVExFfkIfZKdbAeE8Sy853GwEAYjIyPTpozl5opXGJNRvNThCUSNpGEISuiH6fj6BNDqvpaoQZhFZ3JgF6gA4pXMcZPKPQdqFPJggKQEBTxIfZHxgBMNXXuXvfaVtW1Wc/ti7NySq1Cx0ZRYGxKxenNMps9Q22SXSmw5FG4pjCx6ZCfIrbxRgo8VrEcyQYpbDYa6++EVD0t/acSFnmONILtj5WweJCUtXvdS7jI9FfnRvHrdYXFnmyrTSBQ1m9er7ASZA1HOnw90Q0usO7ZUGKHkzYnaZMO5WIqiaaABBxyeSb7eOevFQHi0uSBCAkietR8nosIfKyHo/zgyGxwGPGAZB1BDF8wJscDnNhEfZlRXp7pouK02w0Lkjau5fodzSVIIYzJtvMwLCIk0U17+8mhS63pTJXmZQQBsCaBTkbylIiM7hIMQxJrFyQM9oe5I3Mn9STNop0pzsLBXRyKOJx6UtSnGsQbqAMm6rTTIaHr9B1OTnQduLnr+4yZXi+ExhavnHz5zevBroOdA1ApHG+3Xv2AVt2oUnavvvQlGx+/tnnqqqrYWTi5V3LQO8oAAAgAElEQVS/iSqWP/qTDXml+Ztqj734z38vmvO+8VSxNnnsb/9z9Mc//2oiPCUyFieNQwhSc4qfWer6h298K6Ow/K+X15Bxa+6Js9/+wc8ali2vyXE/ijtjQ8b+h1/Y+k/f+8fDBtP/842/MQCgAwAkgGY/V0OoAz2miAgB//jgGy+/nvvEp50698vv/DNhd6x/+uMrSyy7Rlt/8J1vG1Pyn3nhk6tqCzRF3vfGz0aT1oI8D/2Iz/RibOb8qb279h1LzRqIDPZveea5NYsKFFnhk7KqgOh0z2/2nV+0ZM3ahiqANA3pCADGVfaxtbm/+tF3VNXzV39X3XfqzdeOX3J7gt/62ukNW79ah73z00sV//q3Gx5f5Pjal76WkVH5la8vzjAvXbQmeaW5+Z0d57c88Xh8pLX1pZd/0p2y9skt5W72EexT9wlORwaEMGPt4kUvvb7v0J5kxdInPJ5UKXxGwVirlcFxCOTA1//mW1//7n9W5Kb80z/9rZZIPv4XX011mO0Y97df/l8Wk+sPv/IVTwqxanHuj7757Yr6hk9/oe5eEqTuAYhh1rSMJUWWb3z16+lW4/N/9uRMz4UfvrzrL77xvykp8r1/+Eery/34859w0piuIF2SNaiQNFtVlP/O9gMH3gov2PBEcUE6/oBWWhAqQOd0VUWgpGbBld4dv/y379pLFiwt9pzc9dvTp06Z+gbbLjT/yRc/27r/JdeiF2oyXbtf/vE2n1a09MlspxWbLaWjyjoCBM4+tnbdr//57wnauua5T5nuv8D6hT1v7DzZYs+J/13/6Y//9TczfUf/7UT8h19+Ilf+P1/7WpvR6Pzi19eVOtevS8TPnTqxs3FieW1ux5n9v3qjye4pePoTz7jZu7Q2ocmd83ubSn7x7/8isa6vvlCW6VC5V7Z94Qs7mZSyz5V7+pp++70T0Zf/vz+Le4ctjsJZw0YUuGAg6FzswSFkLO6K8tKW3775Uj+9eu3mFDK2c89pi6f6k4+vAjpCSAMAGdOq19d17njzhzEq60//uKw2Z+Hg5Ivf/d//21i0rD4/xfAh+iISQ+cbD+/YvduU5hka6n7huS1ubmDbroNePvWZT79QlpfWvW+KtLtYsxGDIDHT8W+/OvmXf/rHJVmpUNcUXQYQ5Ndv+MfyFULU39/0l5/aut5GRiZ+8e0vH6ZSixr+Zkn2Pc5l2umO6TMDEZngRsYjn1xftK7ESQKkKzpCgHU5vrbZpmvSv78astd60ijlz1+98qXP1dfV5Px2e/c33olUlXkKXSbfuO97b3c4HMzmpYVmCgMi0DWkqggg5Wz3ZKcfbal1ewPR1xtHnSn255Z46jJYTUN7zve1RGCxx6bMyL851DOdUJ5ZXZhuom6TH16v5ByNRm22WyIWEUKaqiIAcIK8OXNOURRJkiiKmk2liSSls4OhvgA367aEGEQ4hDqCECAM0xGCqg4hBAhhOEQamvVvYhgAGAA6RDjEdbQgz7Ey/6MoeB4KhaxW63uXt0S6JAqxOAdxHMdxiqZNDK2psijKGGEwENqVy206yZSWFCmSpCGMZRmaIlVF4jhBQ5jJZKRIXBaSnKgAnLIYGaCFfv7iwT/88qcIoEU52WkzQwgR0kWe40WFICmTyQiQJnCcpOoGmjYyzPXXI4riQ692yfM8QohhmA9MolFlMZ7gAcTMFjNJ4AAhSUgIKmGzsAAgVZESSclstQjh6cutTVrJxmWpBM+LAMNphjUQUBQEQZIxgmRZ1kASAACR51Qd0AxD4DduHQ6HLRbLHClN6vP5UlNTP/AwpKs8z3G8jOEYjpMMw9AGUhYFSdYMNA2kcFNbf7ontyg3E2lyUpBpmiEJXJYEXpAQIMxmVpP5eFLEMAzDIEWblEj3oQvcx7culXkuKSoEQVnMRgyDACFFkQVBNpqNSFN4jlMBTjMMY7gRFBWPxzEMu6c0mYeOruuhUMjlct3rAhohJHAcwHCaoTVF5jhe0xFFMyxjgJoc5xWjkSUJHCDt7Z//eNELf5TBwgQnIARYs4UmMUngOUHGMNxsMeMQSKLA8RJJGVgTcz2/XZIkWZbvY/ltpOs8lxRkFccw1mSKTE+dPXZm3Wc+zWgix4s4jjNGo4EkkK4JnKgDjDXRmiILgiArOs0wDEPj1zT1/VYgSBZFWdUphiUhEgVBkCScpBjaoIi8IMoAYhiOG41sX/MJ2V1cmp2qyZKqIQPNsqwBgxDpejQSMdntBISyyHO8CCBGs0aWvpGPKUkSz/N2u/1DiipyyQQnQhzDIKSNZiXY98457x88u4ZLxGUNYDhutlgIDCKky5IkSJrFzMiSyPMSRpAsy1DkjbeZTCbft1wukkWe4yWEEWaTkcBAMpFQNB0jKIuJTXq7X90/9IU/eloROUkjLWYaAKBrqiDwkGJZigAAqIrM87yqQ5pmCD15pasfY50LKos0WRQllTTQBgqXRYEXRB2SJiNL4lDgk6KsYBRjZhn8pon5LjXSDdF1TeS5JC9BDMNwgmEZHKm8IOqAYFnGQBGKyEsIYwwGAodKMnTgxMUly5e57Ragy+GEZLWYZxPqka5FIzGT3Y4DjYvHZR0SJG020dd956Io8jzvcLz//I5ESeVkfdYVxdAETeAQoDivMAbiauo+QglexkiSJcH+w+1F9eUFNiIhKDqABur/Z++94+M6rkP/mVu394626IUgwF5FUhQpq/dquciyZVkucZzYiVNt5/nFv7wkfj87iatsWZZsFUuUKEpsYi8gQaKQ6L0vgF1sr7ffeX8sAQIkQYISKS7l/X744Qe7O/fOmTNnzpw7dwquIjFeEBOcjGFQpSBpHAKEWEHkZaim8J5+70SMX7Y4j0YSK0gEgasogsQhAIDhBEEGSgoHMkryoiQDtYKkiRnxQSKRYBjmcqHSfFwQKskIiRKS0fmJF2ngpf6e7e3Q9PcQABzDyOv0sDaXy4VKAEwf0gwAOH/4GUIIQihzyViSxWiNVkXN/f3cNbOSg3RB2eBoAFpyTErsAi9/LpN5bgAAuNlCJXBxGRCaNRPtXFUzDBMMR+12x8w7jHPpp7U+WwVptc/O4mYMlcAck5pT5RCAVDzCyVCl1tIXDZ7N0ufsG4CQd5zQ2fVqElzSbqYHvS/x059ZqAQAALPeAcwo8cL7SPHBkWRevo0473/mWOXMRlYXX33NQ6XZcgIkscl4IIlyHab0D+DCBgLmtJ65BbvODuS8mLP9PJAlfyCg1RsU9MweH5eqt0tq85qFSuCCJhOcHKOMDp2CBOc3SZ6lxrSJzCPSlUIlcKH6Z+Uc8IySNqeeIi++7cXXQwjZZJzheKVGn95ubbYDRAhd1F9ceM+rDZXARa5p3jYCABsLJGRKr9WQ+OX6gvlMcQGhUvryGWkuN9iIkDDkSRXk6LBZkeJ073vhtQgAIIuROCfIuNWoOPfVRWngTOLZHRcAYDpUugYtHIOQ+uQsSL6ESZ87WJhW6alLb+4y98vzn5TmvNxLtpELv/sknEh7cZlmf0j/r1SqchTKeVV85e9uSi5jMyqtQXnZBBffwOTImfl8KU1eLtM/P2Z50vkUgmsKCzVXbNcfmz7PZwQJpcaQO/OC6iIB4I2s6zl5nv8TJ6w2+5Xlue4Sz8nA7Mw732QuTvpRRZrP/QNLbv5C7jqTRqHW0CpwydY9bx4fjQtudJn7KrRmegH5fkTJFng1hGRhrv6SiS/tETHCoCPA+bq+VJqZP+aRISMe0G8Srt4Msv3VRWRVMoesTd14MlijGSzafGSgyDdKpE9U484w0a5Wmo8ufUZsfJwlk5kzlp0lS5YsWbL8mZENlbJkyZIlS5YsWeZlzgu4BY4foFlcH6muFzeR5JkgaibIcIEwsixnjjCZIMnCyajaXDjo3OalmShzJqs0k2Wbj0wT+CbSYSbLOeO6M+wl3kJJa/V8qCTLcjQaXciV6UMNeZ6/gYuzPjQMw2AYliFHrl4GQRDSer6BovI8n5YkQ0ycYRgAQIZYHcuyC2wvmQPDMBBCSbqZTtZDCDEME4vFbrQgl0CcJgP9SSY4kKslvbY6owRmWRZCmD44PMPJWI+UrtYM8dsfApZlz+/6CgCAEF52SeR5RFHEcZwkyfnOW85kOI5TqVQZ1RovSfo0Y5qmb6CFpSMkmqYzRF3XfGH2RyGZTKrV6sx8jJsPWZavtPI545BlmeM4pfJSCydvNDzPC4KgUCgysBvgOE6SpBvrQK6W9LNZRtknQgjDMKVSeaMFuTIZ65E4jgMZVq1XBUJIFMU5oVJ6n6QrAiGUZZkkyQWmzyiIaW60IFdAlmUAAEVRN9DTiaKIECJJMkO8LUEQmROgp4W50VJcHQRBYBh2czVbWZZxHKcoKgNDpfSbBZIkM9CfpN933FgHcrUghARByCj75Hn+ZmkyGeuRZFnOtGq9KtLDFhkxWpAlk8moLiqjhMmSJUuWLH8OZEOlLFmyZMmSJUuWecmGSlmyZMmSJUuWLPNybUIlhFB6ETdCQJaRjM79QwgghCQZSXLmTTZbMAuZKDc3zSXSX34h502snQUwX9nnLXQGL3z96My/rPfCb+akuZQ2Zt/n4tt+UhW4cC5vRZf4KYMN7/JS3XCZryzApWz1ekp96bvP9dMfPvt5br7Qgl0hwUV3uTaamke2y/uZSxb0QjnPH1yILuPXPyLz3RpdlAbN/Xi1uVySazIbEQVCiSAj28xqAwkHJ2OkkiZkPinjLpMKsWyrL+Uya/IMCgK7ySaaiDwTCvrjHLRYrTq1Ii29LAsh31QkyRosNqNOg/jkhNcv4UqHzaygSCEVGZv0k2qT02ogifSESsQzybFRD1Dq3LkODAI2ERufmKK1RpfDjCQhHPDHGNFid8xkcdOBZMnv9VB6h15NQwAQkgPecZE2OowqLhUfG/dhtMrldCopHACAEOJSCf9UQCYVdrtNQeIAIDaZiCZSSo1WRWH+KX80niRolcNu06gUN7pw1xIumQj4/XGWQwhqDEarxaQgCQCAyKcmJ6c4GdptdrWSFoXU5LhXxOkcp4Mm8XjIOxmI6qy5DqN6+vRWmY0FR7xhjdZkt+qT4YA3FEUAEITCZLZqFCDon2Jk3GyzG1T0lYS66ZElIRZLSAgzGXXTp5aKQX8gGIrIOGWz2XRqKjDpTQmyxW7XqBSyyIyPTYoY5XI6FDSZbnQiz4wNj3AyoFTa/LwcAgJJFAJTk6TOZlRTTDLuG/fhWp3DZqOIj3cwHsmpVMLnC+CU2uG0EkCOR4L+aEKrN1uNOiQJQb8/wUpmq0WnUV+nuXwIISYRYzhRqTeoSBwAwCbjkQSj1mo1NBEM+MNxzmqz6bSq80eDI5SM+KMcYbMacCB7J8eiCZBfmKsg0UjPIAcAAhhFqQqKc6/5lHgky2HfhD+aUJsdLosem24yqVjQ44voTXa7WSuLQjjgjTCS2e4yqCgAAJtKJJKM2mhWXXR29WxEjvF5fYyMOR02lUIBIZBFdmQ8YLPbARMcn4pKsgwhZnDmO/TKtDDJeGjcF9IaLHaLEQI5GYv4/CFaZ8yxmTEIZZGPRKIiICwWIwaAyCb9AX80wSIEFGqdzWoCXHIqGAak2m4zKyg8GvAHIjG9zWXWqfEFd6mSwIUCvmA0RdBKs81hVNMAAFkSo6FgOJbUmS0mvVYS2Kkpf4pHVqtVp1YKbNzrC0BKa7caaepcLYlsfHjMK+JUvsuFi/EhzxRCCEJcY7S4rPpY0OsLp/RGu82ivfCQ+KuvxGCcDTOSQUObVCSSBU+AYyF0m1QK8lwDlCTZG0qmZOjQK2gMTYRZVkIAQiVNOLVUkuG9CYHAMKOGNmvI6fN0UTTBSQDq1BSJQQBANMGmJGBUUySSJ6MsKwGXUamk8Aukx3/wgx+k/2JZVqG4sFuSRCEZjyJCOds5yLIsSRKO4+m1FQjJTa2ju7vCerPWSUl/2N/rEzH/uO/UJGdRYc2dnlfbQy6LLkNCJYZhFArFQla/I4kfG+zav29fc+dgSiRtDhtNYBDJE8N9xw4fa2hu40iVxaQbPHP64PH6tu4htclq0lJNR/cePnW2s99jzckzaJQYhEjkT+97e9+JluaWTldhqRrn6w7uq29oHZ0I5hTkJvyju3fu6ugZCCWkvDzXjBcWRTG9zPAGLtRP7yZCkuTlJ1NLIjvc3fXaH1+Btkq3XQcAYKL+l198YUS2LHJpmo/t3Xm0yeMZ56Auz2nCIBTYeHdr0559R/sHx4BC67SbZYHtaDq579hpUmPUosjO3ftPN7WH45zNZtXrNDN5MwyTOTsXJJNJjUZzlRehmG/iTMOphjPNx4/U+xKooLBAq6QAErvPnDpw+PjZtjYO19kMyvYzDfUnTrd0D1hyC9Uo+v47b51t6zzb619UU0XjEAIkMPFD72871Ng1NuhRO1yJkY4DdafaW1rqGzuUBrsYHti151DH4HBCwvNznOR0u+M4buELXTOE9L5KKtWlT6oGAAhcarS/e++BOm+ULyvKTx82LjGh/Xs+OHzs1HgwpjeahPDYoX1Hms+ciQOlzWLobz6+52BdZ3sbMOQ6zToCwxBCkfGu//nZH/zhgD/Ol5aXEkDye3r/8NIfBUuxSwOajh89fLRhPBg2OPNNmnPRpyRJkiRd50aKuFSs60z97v2nhkYmCK2eEmOnTxw5VN/oDTMWiyUyMVh35PjJhhYGkVabVTF9dPk1dCBIliJB38lDB850jehyi0wqUhbZjsYTew6fVumMFBc6fLyuvqElJuB2m0VJkemKEvnEgbdfP9qarF6UHx/renPXge62/jCkipyqfW++2z7Q33DiREN3eP3GJdR0zaY3gvroK/MT/qF33ny3a3DgTO9oSWmZmiYAAHwquv/9d0+e7RrzRJyFeYx/ePd7O1u6+/0pOT/HyUUD9UcP15/pNBRUWNTn15HxPA8hnFlZhiSh90zdwSMn6htbaZ3FZjESOBrpavj5q7vzSypFf8f+Yw29Pe3vbd+rqVheatdBgNhEeO/27SfOtA8PTTgKS0EqVH/48KnmltFQvCDfrSRhYHxo7659w0GuvNxNQMhEfGcaG041nak/drLPm7RZlN0N9Scamru6BzGtWSlG9u3a33ymsWeCKS7OVU4H+uAKHglF/eOH3n/zWNtQJJ5QW512vQohFJgcOXnk8OnGs2FWMhjNvoH2g4ePNp1tS8mUyaDuOVN/vP5UW+eYye4w6DQ4BoEsNOzftft4U+9AbwrpzDD0/r6jA309B3YfjKnsZVa44623znQODA8FnWVFOno6uhLFD1GtgUBkX7u3ZTjs50G+SdHVP/5Ba7B1LCSQdKFJCSFACE1OBF8+MTrqjwcZZFfBY+3eFk/0dL9/IC6VG8im7on3usPRJE+RpNOgwCCQJckXjO1pGhuOiU6LRkViIsftbx49NcG4DAr/RGB3h79pMEgqaLuWJqeDpSuvgEOyFA/5OtqaA6krDGJhEGI4PDfYhUOIQQLDRJ6rbx19uy/x2Cr3BrdOQdz4OOmqEJlgS2vzUJRymxQNR491jIQBQkhMnTxwtGXIS6qU8VgiFvJu21Wnc5U6Ke/x5g6vZ+D1908tWr5OFTmzr3GAFSQAABK59pbm0rW3Mt1NJ3snAuMDr7y+T2e3CqmQLxju62xpGRWqip1Hd+8YmIpl4tD/lYgHR3fv+eDA0WZfhAEIIElortt3+MjZ8akIzyUHhj3Va2+tsMG3tx9iBAQAik2Ntzc1YpZCtRzfu/NAhBH93pH6+hPN7YPhOOMfGegf8kG1rbyy1GjU3WRGcwWg1u5cc9vtt29abdDpaUqlVlAAACSzB3cfwpRWt5o/fLJtdLDt1TcOcKQScKw/ziQjnl4/v3r5omPb3phKyQAgBBAXm3z5zaNL123kRxsOd/vzq1c+dP+9S8rdHCB1Sr7jbMMIq3VpyebjhwPMzbTh5NWDwlMTdQf3Hjx2emQiMP0iAMWDU539wyxULKood1g19Xt2xQl9qUu7a1/d0Livo7U/p7iSTIyd6hxheCl9jae3sWmIceUUVlfX0BDxqdiRfTsP13VNheP+0aHt2z4QLXbIscFY4mNtpAgFJ8eb6puMBSW0GHhv56Gzbe2dQ94Sd8Fod9vRxvYTp0+FZMKlJk+dbOwbD1ybNzVzkdhYb1vjzp37W7r6k5wEkDw1MXzyxMlTDa3BQKip7piPIZYtyj15snHAMyWD9O7q8nDH6V0HTp5tnRQE+fD213x4wb1byl/4xatJWbn1scfuvXOLGhe1BbnXYcwTxfwDPmS4/4F7u3e/2TISAAAAJEcnW1/b3X3rbZuCPYc/qO8bbK8766dqSl11773VPugd7GjetfPA2dbuBHe59oIkYWSwT5/nxmNTrb3DMZZnor5de/a3numKp3iLe+lDDz+ypio/zhFFVi0AACHEpmI9vcGlS6r6mo50eIIjAx079tSpDCaQjASTPJsMd55pOHTk7Lg3kjZEhd6+4pYt991xq8Wg12h1JEpNhLnqFWsNwuSx010jPX1+RlFRWnBoz9GrMEUkRwLe1rPdlCmvpKg036gBAAAkdJ890zfsL60oHOntamztOnnsNCsqCvSgobGtq6tl7/EOZ2E1Hu5pbOuNMwIAAMhsc3P/0rW3bSxRvPL6btxY+Ohjj92xcWk8yubkOWKe9jc+GFq9dmXPiV2N4/GPZoiorm3sjCehJMBUmOEE4fUjI1qLZhnF/7bRl57PgxAK+KMcRZfS8s7OAKZUbal1bSnRqwRBr6JSLN81GuRlUGhR5Rnp9NMiG0+d7Z7c2+bt9TO8CIAsD4z6D3dNdU8mGY4f8iW0OiXOJhtHoklBvkD++UMlhHgm5RkdjsTi/JWc7Zz+DEECAxgEQxOhI31RBiPNWpK4cDTrJkBkY1wqqjC4cnKsQoqZHA4CACSWCQTD4eBU0D8Vj6US4dAURTly7cvKTd4R/+TQSEphcefmLCkx9naMC4IEAICU+rPf+mG1LhXloEZJR0PjAT/j94z6Akme55OJOKFxWs1mTEiO+xPX7T3vdUTkhdI1G6pz9RgECCD/SNvBpom1xbkIQLXW8sjnnltXqBsbDyhpEgAAEGCTbCrG5ubnms2qJBPxTEx2d/cnJczuMCJZiiVEBSFHPb1HjjeP+aPyjS7dtYWkaJ1WPTE8husMy1bV6JQkAABAwmxQJyMhjy+h16iEUJ83kfJOTUZCsVRKUNkWf/sbz4rxINRaSOycPiCp0KsUY6OjYY6w6VVKjYaE4tjwcPWajVVuh1qjE6NT/mBCqdBfNJD8SUNCRJ7bvW5pKT6rk0umkjSJcfHI8aOn+oeGvaGwUqsrKHGPhoKhOP/A55+5pcIe4nGtYkY9ctAXdRUYulvqdh9qZlh+pKv59IhQXmJBkpSMhCf8gVRwMhCMCvzHapIIgFSKD8ak/AKXWaeIhv3j4aQIUUGuE8qS1+v1cxyhVhbarWw4FgrHrodwSBb1JktN9eJcgwoAwMYDHZ09MkEY7UZRkkaCYZtFV1tVApLRSCKZ7u/j3pFDR7sWL7JgNI4AahkYX764tKCgmJgYm+Ixk9nAR0Z6o5qnH7gFB9fcPqG9dONfPveYEA/EeQ2OAQAAQnJ84iywl5e4c0ty9B0NfbGwl3blOR02WgJDQ1Nag6G2ttalvULkBgnF5gc/v7YyH8gyRdNQ5ltOHiVtLh0PoIxolc5qVO3ddXjlo5+psOsgABBiOkvu17/9ZTUfi0gaGoiRwGR/gPOOe/0RHvGMZ3hw1OO1uVzSdNeMk5ROp4tMjopKzdIliwqLax779KOLCiwJRgAysC1a/aWn7ybFpFKrwuFCd8xCsiwISMDV4eHu40frR/xRAACSmXgsSWDG8opKQUKBKb9Bq+QSsXFvXKVUwviorNTa8ooqS2w+byCZYhECAFM9/Vd/ccsiu2ciTBMYqVBZzabO+oOWFZturcolVQadUhwe9YhKtYkmPkpfhoA8EGB5lh8PsylekgEo0NNTMXYkLrh0dNpkMAyrqCr45np7f5jXqimKwHVqKppITmH0vVVWCAAn46LAnx4IdPhSae1KCORY1YtzNDoCIICikXjTWBKSUKPAIEZuXlW0tUCDEFRQl3gBNm+oJEtiJDA5ERa0SpJNMZctFyRwjOPEBMMnGT7CIxyHJA5EnNqw2OlC7OHuQIgRb7oYgFCareYczjvY3NaX4AWAJASAjJAkppwl1RtXlY0ODvWP+kWU3u0HIlEWBBFBCCCAAMqCND3bDeIEQZJkZanmbPOAIMspXH3Hg4+bwz11fVNmmwMmBhub2wWJkOSbMjAw51ZtWVtLkzgAQOaZd998BWlsMseFvZ4IK8pc4uCePXVd4c1b1yspiABQG01ml623talraByJ8kB3a2tLu4SUXCIWDEfVLvfDn/3MNz53b3BktKNvXLgpVXI5mOhUz6BXZ3SU5Nmmu2mRVqlDkZBnKkkSMgZ5HsNvvfPBKnPqQF13ipNIglBbHGZdqqfPDwAACMgi0GqoieHhiKxWAVkWed/ESPckf+vaKgwjMYyUU/5AMEpSSlH8xGlwDtCRV7By3Tq9WjEzAxUhoNJbb7/rvr/4+hd0cqK3dyy3rDw0Pnr6TC/PMjgAGI4TpLIs3zXa3cuyfHouqqNs5bf+6ptfe2brgdffHp2YfOftbUZrIZ9ITo1PJDhOoaJXbNyap00eOtH9Mfsyg0GX7zC0NTX1jfowgNmMFoUkNjS3+YNJAiPdNmtyarJ5cCDOCeDCJ+FrA6mxlC1eurjMgUGAkNzX3tTe1iOIpMQk/OFYgmMgkDAIAUAyAggAJHPH3n+3L4KTQE7FJicjKV7icQyDEAIgSzISeKbp6OHyDVvsWsX1mFyFk2TY0/v7F/5oWb25Jt8KAAAIiTwDyfSrDQhJyppTDjzd9U3dPJIIWl9cvXxxhePKjxUQYDhBEGRhvtYz6hvpbuVYTSoAACAASURBVNp+4KxBpUBIGh3z8JIUm+g6Nobdv37xdLkQBJAgSZXSmKdX9vWOCBKiDK6tW28lIp6jdacbTzf1ByWNUgyFIqFQMn2JxMXOtg/pjPbSohySIPiE/8B7e3oDxPJlJWajiiAIk82lT40NBeKCtLAah9Bgy3noiS8+9+RdGm6srn0EzazAwnAIoSwDSZQoWhGLxTy+GIYhHHIAQxgGAYAyktNtBEGMgsLh3Tt21k/cfe+nlBQupqa27Wp/8P6tFAZFGSq10sjwGFBr6Y96FAySZaQx6Z9YZm/t8/virF5B+qPscFLS0lh6tjZCCMcgRRBGqy4VikdZIZbizg6EK90WuwbXaujNK9zPb3bnqkH9QJgXEQBAY9BWl1jzjTQEQJbExh7fWEKCFBlNcWFGkCEkKbLYph4JJOK8dMH47OVewGEYZrWZBUG40gk4mNWglAX+veaxX5wYG2BltZLCESjNMW2uzfn8clt7r7dpLMbdbC4bV+hc+W6jSpz0BQwmncWkGPeMTobiaq2JQjhEJE2SKrVaL4jRYHTYGzc6DWanneJigVB4ZCrhKrLKqamzLb0ME/vgzW28tqimXOMZD6h0VqOOYhmGVukwkrLn5LuM9IgnoLWYbUb1tX/E+lhIh4cAAFlgo7LBrhG9MSYyNeEPh5vqDr91sG3jHXetWpTDJeKDfb0JQOW7c1EqHIhxBq1WoaAhjgMxGQqGo5FoJBSJhcOMyBMKkrh5NhpeKAgEvWMcTjoKitQE4JKRweHhoH/87IC3sGrZg3ctHR4a4KDZhtMCyyNSqSJAfLJ7976GnMLFbrXoCyRivoHOvgk2Mtbt5x957IG1buxE0xCXSkwN9lDORU69igkFJofH85ZvuXVFaSLoGY2yN91TylUx/WwCAAQISb5xj2d0PBFPhUOxaJzBCYKkVe7ycgrjfaFIgdFkoNGxvfvHUkRlZV4kMCXw8eYzrdEEF40ForE4I0KaViKREVR2ExYOJ/jglF+mNTqlQWJ5klJT+Mc68gsh1BiMhcX5bMQXTkkGo6WoKM9pN0d9kxipNJpt5YWFGhwEo0GVzajVaa7PnCkIz2/+KicEiJOYKKRi4VgswapxVSTKjoz7AK3RKoiJoZ4Jv3+KJ/NspDfMJeNT/iiTZzH3j0wEAj7JYDPRGMtET571b1lTiV+XWegoFfK88fJLHtH6zKc/paHxmH+spX9MZS6R/WPeQHgqnHKXum15ZQ6lODw+RetUjlz9tAO7ApLANh096o2DomJzMhEL+afMeYWhqSAvcuOTXl6UepobnJXL8gwUACDqHzvbPZQIje/cf1yXX1iYQwdjcb3BlKfieVZQ4TgvSJgs6bWkPxBKxONTPt/o6MiEP5wIDMVEaLIX6JWkyESP7Nt1pG10zZbNNUWu8HD74dNdZnepgeDCCW6BK8sRklku6YtHUzxHKAgSyt6JyeERP6mgJSk+OTFOkVCvwXrG/ZaiqgfuWh4JjkcYCqSYSMA3MRU1Ggw4YDt6BuLJZPPR/S+9U7/69rs3LsnDIAwNHosYastcBiSLoeHGIF786MN35uPhhk7/R6lCCDCnniIh4GWowCEA/KH+xJZFrkcX6w91+2VZbO8PRFJC34D3yBi7Kk8ns2yKF+PJVF9EWl5ggADwghhNcDwnIgAoDAUiiUFfgpMQAGlXAZAkMQBXE1AW5HCcC8VSp9onx1JyuUURY3j2oueheRcfYARpzSvRW5M+DUZbdZcplSBJtFpZYlMdGo55gqDaZbCSMEmQDhWRSgpGs3axJeYPJrkCveJjXjny0YBARhDTGk1Kk8XkzC8vUJxpakRq6+IVNfWne9ra4iVlFZVVlXJgcnSkP5mklq0ryy9xbVrc1H62MZSy3bq5GCRGtr/X/s2/eGSyv3sKkTGf5qH7Vjkd2juWu06ebsIsRZuq8gHv1+n1NpcTowylTv3NGClBCAGCVrtNq6Jwhe4LX3qe5wVdbMLjXKaD7K7mZoXRQkvR1p7+Epum8cRRTfUGF05YLQ6bPcfmLtmwompF9SJPf7u6ta/YnYNx3vauNlHC3SUli4pd5M1kMlcGAcQynNFsdeY6AQBszFff2FZWWrJkcZEnONoeSFRXV+aU1W5aER7sPJNK6jfdUUXjkz1nG5jEhGRbsm5ZbnBg57523RceKFlfZT918qSItGuXFsmiyDJSUXWJAoey3pRfVOwbGu5nyZySyhzdzTSJ+0MBIU5oDAaO1wEkDnR3hpNyvsvQ29nCAxI32CuKC1UoYLBZdSxdUlPucph6TxzqnZhSyOENt27UKuXfbn/vkS9/NRYYb+xNeKjA1ifvz88veO7ZryQSMT42YV22uKjIsm51WfuJphyrfsO6CvLjbaVIRgRG2uxOh5N2FlWpKaDQGGwuzKk1LllUiCXHdVabDeCL3JVFOZbrtZ09hLRWr7fwCpIoW76uuKJ2crANansrytz5pPlk18iJpt6SqvJ8q6Ht2Du4e92Whx4lIRpuEFi9rsypz7v77jcaeg4liI0P3WGmsHicwS35uQbV9YmU0GRPW0tfuHhdjafjjF6rJSc73q0P/+1Tm9aV9B+vq2dV7tvX5oPkiMZkMimVIlld7TZBiGiN1mi3XaGTQnJ4cmy8b4RhU8tXrKleWr50NZLYyd6uwLLaRUqSiEQTS8trMQwCgPyeru1HJ7752NqezjPxeCgFDZvXLHOpYkuKO1rbOmlr7pqN65xqkIxM1dWdDiCTRSe1tLQqze4qbVxnNjtybAQGo97Rs+3DtEEjJnwDQ+N6IdTRMuQdJpSVq5cVWil8Yf4RoVQi1namyecwYdqC5aXOvp4uT5BdWlkaiEbaWjqszpxF1bU6jO8dneoc5t3FJSU1tQLfMN7XOsVoN1QWKmB836Fj996+/vDhBrXVrkWx+vaeO9ctjXi85atXaCkMItycv6jSfKL+1FnMVL68zPLRKhdbU26faAs2jkary6wOjWZzlXFgPDQhSfdUWTAoHagfun1LRSrJHhuMxC1kVZnDqSL8cVGlUzuMCggAz4v946EeL62hqFXFeo8vNByWb1umsikwnZoWJIqmqY3VrpWcdKIb9sVgnlHhGZzqDjCIY9eXmG0q4gL5r7ACDsMJldaonvvq7oIVcIIoM4Js1SlWu42biky1Lq2awjUahcugoHCAIFHi0OYbFRa9glhgvV5PFr4CDmK4gqJoKKvMztqaWpsKeP0BSm1YsqTGpKU0ZvuSJdUuu7mgwCHLoqOgallVsU6jKSpwphiuuHr1ktIcyI639ifWrlu+eOniVGjKXr5y68pKhUpdVJwvsmzlivWLihxKhUKBS4TKuHLNGotOOaPmm2gFHAAAAKjWaPILigxapUqt1mg0OpM+t7DEZVBBUlFSkEeSuEpvNGuIqakRc8mKYrtBliRHXvHKldValVKt1mi1GovNXpCXV1JaqlXTUKlbuXJpYa519nPnzb8CDkCIIEaZbfYcp1VJ4lwi4gslrI78FbUVBAYUpryNa5a7bPaS0lye5YoXrVi+KN9ozS3K0UWSwqotd1e4DDH/qI/RrVi+qLzQlkgKhdXL1i0tpwhCodPn5eWZtUqCVpodNq0S05hdK1atzDdpZlT4iVwBBwCAEFOodXaXw2rQ+KemZIyuXLI812HAcbKqZklFmdtq1gs8p9S5Vi5fbDWby6uKEc/qXUXrV9fqFOhsXXf12tU1NdUKMYGUOffds0mvpNUajUajMVsM7qKyHKvZleekMOBeVLukIm9mhfbHsgIOEiRFq2hRFHLc5auXlWtVahrHAKmsqqkpL3CqNWokSWqTY2lNtcOsn3HU19aBQABxWmGyORxWi06jUqs1Wq3W6nC58/PyC/I1ChyjDWtW1uZY9ZPDAyqbuyjfZdRrtTqdM8/tzrVYcwuNFM8B0wN3b1TTJISY0e4szHddMCXk2qyAg4hJcLb8YruBxnHMnleAx30TSWrNspoStz2W5Jes3lRVYKFoJQ1kUmNcu/4Wq4ZKF9BodzjtNtWs57MLVsBhBJlX6MaBpHW41y1fbLMY1Wq1RqPVms2V5cVaJUUQdF5Bic2sAgDEJoY9QXzD+lUVha5Eiq9avnZJRb5Gq8vJceEYVrl8dYXboVKrtRqt3mjMzcu1aqlgMKrWWXIdLqPJnuOyqRUkx3Bag81hM6sUhFZvK6moclvVggxWb9pS5DTPVuBlPBLECL3BmOc0yoBcvGxVWa7BHw5ygFq5fIlJqyEoTdXimpKC3FyXTUkTlN6xZuVyd25OnssiSrK7cuni8gIapYY8wRJ3rtpgLna7FBSOafTFOU4C0+QWFuZYtBiGqfTOIpuWlbDFK9fXVrhmXPeHWwFn0KlsakKm6M0VNptOWZ6jYUWgNGgfrrErSdDWEygrc5bmGa00BArl1kV2o4rEMNxkUBVa1CQGtSo6x6REGFGSZ1ySq/EHkwkBluYZFDhUUKTDpLbpFRolqVFRBiWZY9UWWDRlLh2OQY1Bs6HUYlDOrBs+twIOzqyYiEQiBoNhIWUQBIHjOIqi0j4XISRJ6PIjgRACAscy4QCvYDCo1+uv6nhLhBCEQBZYfzCMUUqL0QABALPKktbhTOkQQhBChIAQH+rxgEUVBRiGzUlzbgoTnJvFHOWwLCuKolKpvIGnXaZSKYSQUqn8CN52zoocJhX1eT3mvCodCQGECIFLW0Ra4+DCIfFQKKTT6TLkaFKfz2e32z/iTdh4OBznNHqDZnr3o9lWBGYZTHpGHAIg6huNiDp3juHCNHO55E+xWAzDsA8R4d1AZFkOBoMWy4LGS5AsBgJBCeFWqwWDl2iV51PO6EdiWhuGypaX0QQOIbioIZ6/4iJ7BBzH8TyvVCo/Bpu8yIGcf2N0ybr+OB3IeQGQNDk6qjRadFrNBdvqXMZWZ+A4LpVKGY3GayVSmoh3NIq0bpcJnG9Jlxbp4jpOJBIYhqlUqotvfgWDRCg6MRzgtUVuc/oLeFmHDwDgU/FwNEGpdUader6yTG+rhi7O/4oeaUZsSeRCkQgnkzk2E5wrzEV9GQAAQQhFJurxx+x2u4I6v5PCxUWYzxRTqZTJZLqMbJcTe7pSEAAAAQgBQlJXf8hdaFUSAF6yZc69HCDZG0wyIihwaC/ZGOZkcSkbYBjmGoRKNxcfIlS6IXxSQqVryScvVPqY+cSHSh8zH2eodLVkggO5Wq5hqHStuGSolJlkrEf6iKHSDScdKmVEF5glS5YsWbJkyZKZZEOlLFmyZMmSJUuWecmGSlmuwA0/iTNLlixZsmS5gfzZhUo3Ucd/E4n6sZHVSZYsWbJk+Zg5PxsRIRSNRhdyTXpJJ8dxGTiZ8YqwLBuPxzNknvJlEARBkiRRFG+gqBzHpSXJkBm1DMMAADJkmirDMAtsL5kDwzAQQlmWb6KIEyHEsmw0Gs0QI5yNOE0G+pO0AxEEIQNlmw9RFFmWzSiBWZaFEF5pE+aMIGM9UjpaiMViN5HbmQ3DMDiOn491IIQ0TV/RHyGERFFMbzVBEEQG+q/LkN6jhabpDOlu5yO9elMUxRsrKkIIIURRVCaoCyHEcRxN05kQoCOESJJcSHvJHNItF8Mwmr4OR5ReH9IWmN4LLQNVnd50h6KoTLDJ2aQdiCRJme/rZkAIYRgmSdLF2/vdKBBCkiRhGJY5Is1HJnukGVO80YJ8GNI2IEnSnBa+QINIh9g36WYBJElmoGu7JOng9QZ6OkmSEEKZ421TqVSGhEoAAIIgMt+BXgDP8zdXqAQAkGWZIIjM7APSZI5NXsANf9a6WmaeD2+0IOe5iZ4uMtYjpR/SbgodXhJRFLObBWQ0Gds3ZMmSJUuWLH8+ZEOlLFcgG7FlyZIlS5Y/Z7KhUpYsWbJkyZIly7xcs1AJoVn/rtVNM4OFzNufk+RS6T9hOrmYC7Q0++N8CpwvDZrmWsuYIcxXusuV95LamH2Xuff8ZCtwoVxeAzeXeq5UlhtQmNl5LsxJznUR11yghUgwq13MaSNX6XPmTbmw+6C5uvvQaa49F2V0xZw/TtO7YlYLkeXyaeb79ZrMRpQ9k9HTY3EvLwMEKl2G5bk6Hb3QIIxjmf0twQ1LnDo6A6cfnjf7ue+hzpsxBGD6qGAIIUSyPH2q3/krZloPhmHnbwlnkqDp4w9v1lddsiwDAGaOv02XL72kZSbugRC7QCEgfU4hhGCWSi5wNDevTi7JBZ56xgSmv7/wm/TC6Wn1ztbhOUObUfqMzudmN8cOP8HM2M/sb2Yb1ewjRi9osxenn3Uo6dws4HVXJ5o+eXx2VucbEYaB6Yo+V5ZZTeZjq+lpfZ4TIG2fYM4xq7OVCQAA58x19h1m/3xdRJwj0oyQFyRJ28VMF3nlJoPOnw0PIQQAgenRgdkGgwDALrRGAOG5nM51BzOWeWGmc/qdcx/QdHYzpny1urtIJxd8fU6ui07Pna+ZzCRBCMxs8XCuM/uwxjirmc66G4RwxoRmqfW8LkD6GF2AznnVWfeaW2A0LR+AEEzXf/p6CICMZizgQsEuFyrJksRxnAwAQVI0OW9KhND4RPhg47hXggoI3m+ceHZryadKjTgGKQITeAlhGEVAnhNFGVE0SeEQyVKSlRCAGhWFZIRLoizLkoiSnIRhUEmTOHbjvTuSpcGu02+9/kp3SH/7Pfc/8qnVNIEBAGRJ6jt7/J19ratvu+2WFRXtR977445DQcz+9S99prbMse+1n7x7rF90Vf/z85/PtxswCBGSuw6/9h+v7mcp+4++/092BfPHF1443jOSX7Lx23/xpEGBpUK+/Tu2nYoo/uZrXzLchKsEEqGhH//gJ55UzJS76e//7rPI1/7Nb39fYXKaS5d8+6vPBHvq/+vnf5Ap9T2f+/q960ohALLAnjl54MUXf8fgxqVrNzx03x1NB3e//X59Ue3Khx68zXP68L4jJwOJOEuanv3aV25bXUPeeFu4VqDJ7tYd27c3DYwG/OGKdbd/8elPlzoMAKC2k/v++PbuSX/y/qefu31trRpyu9/+XeNE3je+dLtekfzlP/1/rdE4oIp++B9/61AREAKeZd/4yY+2nx1x2myb7/rCLbW63/70f7dPirmFpSs2bA617W1s98QjEWNh9Re+8Zdr3As6BvsmBclSwNP/7p5Dst79zKN3kDgEAPHx0LZtbx041lSyauuj992ujg2/+OLrvd6pzY9/8b5bV3rOHPjd67sirOa573x9RVkuhWMAIF/P8X/88WuRkPyNH/7jrZW5AKCwb+j/fu9H1U9/9/7F5kPvv/HLna0ratd85StPOPTK61QWLhXd+cqvXzveU5Bje/L576xwmwAAIhNrqDvwq5d3GVy5Dzz56ZW5yg/2vP/OwdaaVRuefPx+Otz71vZ3j3UH7n3w8ftuW6dTklfM5SMicLGTe3bt3HPAry36/FOPllDhV996p6N3vGrjnZ956K4cixFCkPS2/fv//c3oOLfqnic+//At/HjjP//nb+Jxcu1jn3v2ntWt+//0sz/sxVW2rZ/5zOO3Lr3m7RshxMe8P/yXH5be/vzn7lyMQShLYucHr//k7aOyyIejqQ2Pff2Jdc7/+sm/TUZgTlHZyltvGzu2ra3fHwlH8qtXffWbf1lqnWcpGRJbDu99fceB8cnUPV/8wp0blqlwcecf/7sxWvztL97tbXr7f948wfHcSO/ww//ys69urkhfJAlcX9PBn/zs9b/8yYt2YWL7n1471jJSWbvh+ece9vY2v/mn1zyM/ra7HnrotiUEBhGSexoOv/XOewMR/ZOffmTTmrKG/a++u/dEzFD99c8/Vu6k3vzpL4539+evvferT91j0i30HF8kS97R3p3v7USuJc8+vGUmFhCY6J7tb3SH8XsffRKNNL3+znuDE9E7Hnnqzo0rWg68sutQY5h3Pv/NLy+rzCcxCABoOvLur17eKUD0xDf+6faa3Pd//fd/qgvo9bXf//fn7Spa4lPNR3f9dFv/z376HQN9taaIUpHYz/YNFhTb7lzk0NI4EoXX93b0Qs03NhWwvsBPjo6MR4SHNlc8WmPFIEAIhQKRf323i0H4LSvcj1QaG1qHflEfsBmUd6wsWJ+nPNI8/FZzpLrU/PgthQV6CgDApZLvNYy+3xpw5VqfWJufi1IvnxhtmWSKC22fWZurZmMvHB1r9TG3ry17vNainzt2g//gBz9I/8Wy7JylhrKUCHsbzrYSJA0JWqU4vy+ALMuSJOE4Pr0MFY2MhaYk/P71xZ9fbg/4w4BW9vSPnxhLuszUu/u7jkSQHAj+7tDQ+83je0aZdW7NzsPtvzjh3XF6hMOVhTrx397uX1Fl2X2g479Oeo93egWCKrerr1P/mN6jZSG7nIkJ76kTp71C3qYaa3dnP+kozTerIBQbDr3/ymvb2kf5miU1+Ubp968cqNmwdZHK0xom7Fj097s7P/v0Z9j6nb20u7bQQeJQSoV/9L9+/eTf/EMp07itF6/Uxd/ae+arX32m8b23cHd1qU3V09H0099vU5lyN65bpZyOSEVRlGWZJMkbuCFbelcIkiQv/5A12HxwEiv9ypef2PXivzqXbkXe5r0t7He+9dym9WuUcnTHb3/l3PzUnesW2+1Ws1GHQSCw0a621smw5gvPPbN62ZJQf0vX0OSKTetivtEgT229a+vGjeuwVJg2FaxetcJuPG8J6T2xMmSHumQyqdForvIiqNQby2uXLqtyh8JcTmHV2uUVNIEhMfLmK+/kVKxaUaw61R4tytfv/M0vdh5qikL3lvUVybH6lrDpua98zlf/+gi+aHmZBQDAc6ltf/rTsrs+8+h9ty+tcccjE/sOHLr3qa/dtWVDbXlhdc2yVUsrIZRxU+5dtyxTkuc0xnFceh+ga62M6whCiGEYlUo1jxGisZ7W13732/1nxl157pW15TgGEQIjHScbusIr1m6M+7sRhAHPKGEvXlmqPdOWKMrXbntrx8q7HlukndrREFxVW6pWkEBmfv+f/6fwwW/cWzDx47d677lzLeSSe179xY6z3kUr19rk8La3Tj367BOaeGdrSLeszJkWJb3hyjVrpEhO+CcOnuj69HNfdKKJnY3xjavLCQBifl9vW6+zfLlNwfd5IlqJ6ewPbPrUuojPNxUVvf19HGXZtMTeN+ZXmZw5Zm1aUdfPgYw0HT3ZPVawbMOmpRW5Tutgd6cmp/zezctOnGgz5+XnOMw4hB11x6ZURQ9tLXln+9Fbblm94ze/hovvevb+mv/41TsP3rfpyPtvr3vsy2tLjC//cd+d92+mpms2vWemUvlRI9F4cPBf/+FHZ3pGSpZuWl7uTI+/GHKK1q1fV5FvbG+ZePKLj0mxyYOnWp9+5qtbNt6yuLigZumK2qoiQeA1OZW3rV5ETj+rp7fOIslzvb7AxE6ebKpYtWFjhbz39GRRruW9V1/Yc6BFNBfctqrKnl++dv0ty/LJfR3hrz79mFlDQQAQkmOB8Vd+9T9tA8FNDzwcH2s9frr34UcfGO9vTRJ0aGQohApWVdsGe7pzSxYZ1RRifDt3niAs5evKyT5fjETRYyfHlt3yKXO0Y0TUyaOn68Lap564q+Htty21q50mHT7dLC7nkWTJ09f+ws9/1jQQsxeWr6oumn6fIfW1nXr7rbcjuLV2cVHT4cMqU9HqSltnX1ANIodPT6y+7U5VtGsKMxfl56hpAsnRn//4hdUPfnG9M/nagcDWJZrfvd/y5W/95eT+37DlWyrtquB4/0/+86UxXPPoXRsU5DnRRFFcSLWGpoL/vX9oT2eoLN9U5dQqcNjXPfJS/WRcqby1RPvC+51VZc7by4x2g8qpV0AIZBk1NfScAfqvrzZvqxuryNV0D0dqanKrTfIHHWG7CjT0hjctzSGEVG8c1eRoMYj8U9HRELfYpfVHGZHEBIaRaPU9iw1n+4MKmjjeNmGwGbaWmYpNCodBQUwP2PA8L4rivK1IRohJMUxSQjJQqa9QSATAhC/68tH+H+zqqZvgjSoSgxIryDJCSBCSgnSk3xcnyLtqnM8ut5JQ3HU2VOM2Pb2hcE2+WkYgKck4BpeUWu+v1E4FmVOjMTEDphHwTDiZmqItzrwch5RivaP+9ICfNb/y8ftWVOXrBQEko9EJElid5vIik2/QNznm5aDKYbMW6Oz9Z8Z4QQQAMKloL2QW5bkqS9T9Tf3RhF8mdE6rXamhOke8Qe/EmZNNlWvXJxLyTTqjqXjF3V/8zO0aEPXEFTiO99bXBROJV37181++fjAej7YM+0+99/Yf/vTq2eFwesSTiYU8vR2t3X2/efHFN/bXT4SYlEgUF+YqKTQVjMqEChMiwxGxqqaqONf8yRlRAgAAQJCUTqfxDPYrjaZVa1doKAIAAHGNy6ll2cjoUMzlsGjU1JItDz/5qWq9mgQQ2Ms3f+VLD9k0aGzURyrTUQ6SmIn2luGW4/t+9V//U9/jSXiHT7eE9u5488Xf/GkkzGi12kgwEE2wt2/dYlBk4pY/1xCV0bbhjq13b1iE89L0d3LAOyFrKWdVhZLnYuHwks133rHcfPhkr6vYblVLgYRosttKipwDI4MMyyMAgMB3jSYLC1wVFSXDA0ORKOcf6/qgT7E034QkKRqLh1XUsrJco1Y/1ucRLnyTc42AmM5R8JVvPl9q0Xj6pyRIYBAACHX2nFvvuTtPlWjqGHZULAqm4qJCXlycR8vyhGd8RIjTRlV1iYUPR4L+mHTlbD4iaMwfb2/t3r9zx6vb9456I2u33nXHbRspSUgmOQzCdPey6NZ7nr6v9r0/bC9cvV6tVlTXuKcGJ72TY9q8AgWlfOKr3123uDAe8cYk+XrMupAl7OGv//WaMjOGwZlXZaRSo1PRPQ11Vfd/psJCJca7ejv9b732yi9//WaAlbUaVXBqKsHhd96xWUnM63UIhe7ux57YuG5pNCRwEsIhWnrrgw9vWKJSUggAGHxOJQAAIABJREFUSqkxm/U73tx/3+e+VGxRnQsUOKbr+FGicKXBSMkCl4oEGVWx22mzkHh/fx/D+E3FZXadUWSSgVgcAMBEvDFJMLjyStyueCA+2NrMaChrvrsw1+zr93fW9zntjjy320Gy/ZMRXlygLSKtwXLrnQ9sXlkoofOv0hJ+z6jHp1Tb8rQ0xFVms1aWYqMjUZPeaM0rMKmIVGhqNIFsJr0i/VoJqkvydD7vxPBQrLwyh9Tn/cs//93UyXdbYM7KfAPHMHUH9uRv3mShOQCuujcTBXj/qoJbi3RqHCEA+FRsT19siUWhJTEgJob9fH1n4MW60dOTKRkgBABC0shkKi9Xb9FrcZblCfqhzRWb8zXJCMMgOZrk/DJWXqBTUTAaZkUJAQBtDvNdS1xMik2IqNCkWV6Z9+CKXDMECU4UBckb5Y92T71cN3JyIsleFILM/8ABAaGkCtxuGqRON3VdsZyQwCkMBRLi/WsKNleYafzc20VRRjJCD61wO5Tid9/v/fbbHeMM8fWtxR2941/a1vXfR8fSEy4S8cQvDw71xMmnlhjigowyIGZQaF1qtW2gcc97B0/1jUegKAIAACALikpKCnNpEgMISLIkYRDDIIHjEiPq7DlYbOD9Pfv3DvWnwiyQAQBAlkUBwygMw3EoJSW1MTc6OrRj3/6uQU80Gh7oOxu1FGwus517233jyvthgQSlEONj//Ltfy9Y91BtoWXzs99/87f/9tff/UrXoR0TgYREYLc8/exT92w4sftgnJUBABqr+9Hnv/vyS//n8U+tSQ52izgtxUJ/+P2u1tYhGcmyLPU1Nyo1tsKiMhrPiAGkawkEbCzQMxjRG51l+aZzj3ZQlgWip6W9obUzLog4ZaxZXm01q9MPZRhB43L05//y7930hofW5gMAIIAqQ+Fv33n9X7//nfs3lWx/74S7dvP2d1/+x289W2Hl9x/oFpjw5PgkD/Mq8iyf9IlK0GR1VFZVaxX0rPmlSBREGcMwkoSCLIkySStM+cue+8Ldff29IzHgVIC6D/a/ub1RFBmY7kxp1a1Lcl95advvf1+n1sipWOj193Y89fRjahpACCQkIwpQGAYAFAT++jVSiOEQie++9NvdrexnH15DAAgAwHBCqTeuuGX91rXVY6dPhwUB4CKJYwDJoigICECIEThEvCgK0sfgQHhBVDjdjz/9uUoDPtA7xADKP9Dyi9++ZXFXF+bk4AACAEhaodfnPv+33/QdPT4RjGMk7O/t2nvoDJVUQABomm4/suu/Xzjy6Wc+ez32TNRZ85dUFikofK7to3hkqq4xeP9tNTStWbzhkTfffOGvvvq0i/bXnR5iYsHJySmlubzUprlMi4EYplBSbYc/eOndrrWrl+YWFCytqTTp1DPzZ4Spzn0D8M71S9JDEkgWg+OdezzsXRuXYBiCUJYlCeF0+leeY2XA4TQJIZBlWZRkAIAs8TIm4ySOY5gkiRzLAAzDCBzDMJEROUYkCBzDMBzDGV5aaE+JEXqrs7qqVEHNenASmYbW7rE4XLmkkiYgxGQkYgOdPc1n28IcByEhCZGGhpPdXWFJkM81EyBDmexubTzZ0s7jGICETqfd9OBnHyrWvvF+o6fhYFvSccfyUgyh9GS/BdcYAABYnKaKHIOBTteauO3YcH6BrcympHCIJDkiw9tW5v/1BvM7TRPSufnAMi8hgsDT87kkAIEsHT47+JvO5D01DjUOJQBJAiKAJPncbDIcx1Qa1V0rcuxKrGMsxiOY8gf/5/ioymQos6plCW2udf/1etfZodBkUrhAtfM/cSIEEdA7HAopgQ0PXL6QEIBcm27jsjzk97/U5s03q7Q4jMf4UCg5HhMFC+jxpZZVFj5zS/7fvNI2HkmMT4l/9fCyv/JNfm23n7/NChAQUtwEgx6vMJ055SdV12sqwFWB0boNm29Tmu0dXd21Gq3CpBdFEUCMwCCGQQgggEBB08qwxDJiPJlSFuaonUXf+9YX97b7NtQ4Ol1OiMkcL5CkQhMEQUFIJgVNpSMvf9H3/vmLR4+23VZdJWuplrqj2+uG3uBYtd6+bUfdM4/fcrMNAiA+Hvj/f/i/QuZVP/7up5W4uHP/TvOq+yuUSiDzBK3KV6ogxDUaLc2PSDLieT4S8rV39RgKqymKArLsqlhSmGft6uxrOCOY1EpSSjZ1eLTu6oJcE/jk9fMI+McHYqJQ5CxQ4BDJkijJMDbaPJZYdfdjiy3RX75xMjS12GUqPDdTEQCJZ379b9897i//zc+/oVPgkihIMmD8o69ua//Cl7fSNM4xsfGB1o5JcWNtDkkgUZCD457xsZG8ZfdpMnGpxDUGwyCO4QCem5YqCgJCslKjhYNR1h/hjbRFRzQd3qvPKcu15ZGRE2IK/cV3vvbm7iZdbtXEySSJQZ7jCYK45/m/lnYfIOVVtv4zEutrO9m5c/d3WZGzeV7RPX079HJ+hkeINVgt5HUL4AWOOf7O77Y1+v7uR/9QnWOQJVGSpGh4qr2zLadimdGkFXuHRMYoxGAoxUKSMqgNJMMKSTmWlHCLVm1QfQz17VAq7BRF0golhQNZDo92vPDiHxQla59+fGuOWSUKPMTwxiM7WH3l0gIH5KNxUXhnx6Gnn/vneyqUn33qu33RLyj7d33vv9783Df+6dFbyq+HhBjEAHa+oxNFXpIhASVv18GYfVmOQSWyqZGWhlHBWZWnIDAkiILfMzY56SvZcjuJX87nIIQGGg/86tU96x58+I5blmoUFDw3+/pcgsbjJ22Ll+TqCACAJAo8x/WcOnD0g7OHd+yWJfl3P33pkbuLQbQvydekILLa7CgmRD0hPleiaUKnoAVBwEg1YlAsnEwoEmq9yuLSDnSGmUSCS8WVRcWWqK4rGuNYNsInKi0acsEPkxDCcxNm0s1EFFP+obHu+j9s75B5VgakiLgIj5VtuG9NgfzmrlMdR3tihPWRz3823rbjTN9AsLaYNGlxxnOky/vM338vh2/723/bHl2nf/Hw4NNPP1BSrj90xqsaO3uyru/gu4KIYT/8xRs//tbnrq7WMIiw6dfsqVTPFFt/pispSKyIKlwVGgxBDKjVBBBlgADPiQBCgxrvizByHs7jhBbIZ7vHft8UfWpL2Z0VppY+VoHkcEzEAaZQkgjIgoBGp2IDUb7YpdCTUEzyoangS8cGU0rD82vzSvVAo8IAAXRKYs7Comnm7ZchhmMEPdraTCoo99Lay9eCVkMXmzCbinIvzgnEee9UfK3b0h2YfKV+QkOTZXq61oq/VTfwxyBfU1O0MkdvTYb/91stvIR978kqNQ6W5motDuOjVcHfH+xdXaAtg8T/Y++8w+S4qkR/b+XqnNPkrCxZwYq2HGVjW86LSQsssITdZRfYJb0Hi9mFB+slLgYbszbghKMsS1bOcaSRRpqc83TOsaq60n1/tCyNZEse2Qot07/v0/f1tLq6zw3n3FO37jnn9NH1qwhSckeb9z3zwibSWrl45S3LKsXfPfk/wNz0hY/ehRBUkQIQ0tgrb5mr2fDCH4Ix/LNfuclJpb/5X09IrCbLOr/zyGy+96UHf9jxl1f+8/O3VX7v29/NRuP//IMvpv3Dv/zhr6n6Klxj/M4dN7gfuvXzQvLQ3s1/3h968N6V19zKhpDa/MpTf97uX3nr6GP/8f8+8ZV/MIPcT/7l23UOZdZdf1tfU73i9qW/eOw7JxvKFq39cny841f/+8fa2z9l9Pc+89SLBqdx3qo7DNnJ9a+9fmw0WlU7b8G8eZSSi0JmhsFgoIrgbP+lBgE1HggDmrVUl0MAQgPNj6/bv3zljXPL4J51f9jIZxtXPGC22SCESJUAUAAA/Vv+9JtXvQtWah//6Y9W3PbFyuTvf3l47uPfuzE4sP6fv77fJGv/7t++QOTHt//pt5vMlTZrzef/cU7c1xPNSivLbfBqK9EVAQKAJKSIqqrI3Lpnnw+l0dr7VhMtr/7xF49aa5cuWTlf9ra+8JvfpoRwxfL7XRWO9X/4jwOjeZIn1/7TP5jZ2D1r/vZH//t0fNuTL7QEbHj6I1/91qym+c+88moyFv7tT79bcc/nVs/SB4/v+tq//XS2p+JvvzrnMikpUpXoWOcvf/8aZ67e8vxTY9ctbrKjXz/x0td/+JPgQNcTz7xhNRqW3n7PzbPNb052fu8/ftPYNO9v1ixiQ+2vbtrxzQ2xVbffM7PadfmD4GDN9fOt3V0v/PfP6fL6h29w7Xt9XcuxAXed9PunYh/7xNodz//ctvzTMwnlj3/41UuySjQuqrXqV9+w6umnf3JApzHNXu4mc//y1V/GWeeJA6/6+jr+8Vuf0V96GQFEQBBysoIAQCc3/fbft2c2/Owbk70j7oX30QQEAJNA7uUnf4iZXXrH7H9dWR/obE4K6k3vdXuWTwf+/Nyb3cNBRG/m06GPfnRtuc2kijwnyYVoLN9oe4X1Y4XQtpZNT/5oa3zD49/b+Teyb+j4d3/w2Oe/+VVLasAg7fzxLx532Gq/+pkbfJ0HD7z8dBdmmbv4Nr04+fhvnzZUzp3XaNu87bldcfauhx5afsv8pP/365/6L79i+/KX6hZW1Hb96KkfH90k2q6bU2Wmz/+s8F1AqizKIq8I2fj61zb0+/Lf/u73PvGl/N71f2nz5W954OHRva9v2/HCXiFft/CWhqXzR1579fknfxoPpu/7wr/A7MDHvv/K977+5aVN1t899iNcDs6+5Yt6q2P40GNfa92fC6Cv/uLzSysf/JIiDnQd+/FvXv/elx95X7YHIQUhhIDG8INPXa8CdGh351tZ+q4md5OQ+e3+4a2YfPfSBhxyjzx64NtfWrFwrufZN0d/NkFbqxyEkn9mj3ciT54cCKdTwkfq9TW68GNv9NQ6tWuXs1ua+9uC6r3zrZ29vj/vFnQ67f3X6473hbeOZj027NlDow8sLFvTZH6qdWIXl1+xuNqjJc+ZCPC0/5RMJk2mcyNl3jUGtVAo+HQNuAwnjgeTqYxQCBqE8FTY3tthuafC8zAMFo5iFWLxCmcNVQUBCDAMKkohTBoghFiaqK+0GrWXJRgsFosZjcbp1WxCYl5IxGJ5FbdarSyhnDjRqpC6BfPn4xIXS+YYnU6vZYHIBcIxGWOcdjNNErlkPJxIaUw2m1Gn8vE//vHlv/3S37NAHvcGEKWrLnMgVU0lQvFM3mJ1mvQsAACpSi6TSgmK0+E4fcMqCIIsyyzLXsUSThzHIYRYlr3QyVCkRIKBdC6vIgAhsLg8Jg0RmPQJKvSUVzAElGUx5PMjinW5nEJi8mTroXztR24oI+PRiIIxNoeDwVEmlYwl0nqTxWI2KKIQTaRZjdZoOHcnPB6PGwyGIqm3FQqFnE7nRV+G1GwmxQmK1mDU0ISUCe0/1uOprG2ssIcicV4BLoddy9IQwkw8kpEwu9WUTYTiaV5VEYRQb3ZQ2bHNzaGPffQWJZecCKV0RrPTZlQVOZuMxzJ5o8VmMTB5LpfOZFiTTc+cdYI7nU5jGHbxp9GvJqqqxmIxm812ASdAkfOpVEYGhNWkHejsSObUmdddR0jpWCKtMZhNRj0OlWgwnM0rNoddxzIon/GG4pDSuB0WAkov/++fFz/06Ro9nPT5FYytrnQXnHRFkeORIKaxWPRMnksHwimN3uiwmU4/bcnn86Iosix7SeYkQojLxAOhBAIAw3BGqwW59MFtB2/+wqcNChcJRyCpsTsdJFRz6VQ0kdYZTFaLESpSIh5PcpLNZtVrNac76fIZEIQQn03H40lSZzQZmGQ0nslyCACIEXanbfzEnqxl5rz6qnwimOQVh9OlZSkIQWBilBOBvaJSh+VHxwIFc0+QTFlV2elAqXw+z3Gc2Wy+JEJG/BNQa7UZtWlfx4s7xr/0mbsSkbBM6B0WHYRQkaVULJISFLPNYWAJIZfN5Hi91a4hz+qubDaLYZhGcyrQTMpnw+EEL4gIAoJknS4bS5HZRCQl4U6ricCxWHBSoU0Osx4AkAp1P/vHtn/6zichQlI+FwwnLO5yFldz6WQsmdObLVajTpbyiXhUkDGLxUahzIn2HoyxLJxTG4/FeQWzWS0ahpL4bDgah7TeZjaQBJZLxaKJjMHmNumYqaHi72mRZCmfSiUVjLUamPbuXl80fefNqwigZtNJXkJ6o4lEYjQWz+aBw27RaZh8LhWJp1SSddksuJp5c8v+ZStvdBnICX9UhUR5mYciMIVLjgVjWoPNbTcW+l3gspF41u1xksSpnhQEgeM4i8Xy3qOmqrF4DqNJg5bGMQgQSqdynIJZTQwJYTCU5CFRYdcRUN2ytaN68cwmG5WIpdMScFh0JFL8sZyMAACQYUinmRVFMRIXNDrGqqcGhoKTKXHh/CpWEmIpgdayZi2VTnNpTkIAAIhZTRoDi0XjOU4CbruOnrK7mM1meZ5/D1fpXTnHVTrVyKmvzspA9PaLCwVRTfkAurxPXS7GVToLRchEElmC1dtM011p+NjQcM4+q9yAXfz+yDXjKl0EKJvLBILR6uqaC+9yn48Pg6t0NrlEOCsBvdGsmXZgbWi8X9VXuS3v54zHh9VVOvNhRYxE4wiSDrt1ujonZ7o6g41za0nioiflpXWVzgGpCpdO+GNCfV35+9CWq2NAVGl83GtxOHTnjVi8EJfQVZpKcKQfs1U4ph1XP5VzXKXpgxAKD/eqrlqXlplmT/DpRDrHa0xWPft+tgmmb5EUkY8lUjKhc1svdDBrKkI6EswoLruNpi5qIwuAi3GVpglCYsdAanaDnZjeuoRUOZrgRAXzXPAg2vm4xK7StcL7dpWuMB9GVwmAdzjSF8WHz1W6wnzoXaUrzGV1lQA4k1/0fVAMBuRiuUyu0gfhfbtK7w80Jf3jxXJRFulKHnC55K7SFabgKn3oIoxKFDdFt9yVKFG0FJ93WOKycsXuB0oT62IpuUolSpQoUaJEiRLnpeQqlXgP3i1wskSJEiVKlPhr4axH7Be7KF6Li+i7VhUtTk7XyLzaghRRdxVJhxQoHkmmyTU0+c+hyGUuZvGKWbZ3UlQKDorJCE+HYpazmGW7MAXJial/i6I4nSsLJV1O1eu+1iiUGVKUy18A4IMhSVKhn6+iqJIkIYQwDCuSsmuFDnlnhfCrQmEiXVsqIMsyQujaEhshpChKoRTX1ZblXApKKopiER6dLpgOURSLRHmngyiKBZmvtiBnkGUZw7BrQmWK1iKdXsuKULbpIMsyOGdXieO46dij095GkcQiXRSiKPI8X/zmo9DDBU/lasmQz+fBBwvKuLQUxq5IliVRFDmOu9pSXBz5fL74Z/45FG7heJ4vkkk4lcIaoKpqkczJqRQMiKqq19CIF2KreZ6/2oKcoVBh+ppY44vWIkmSVLSyTYd8Po/j+BlfB0L415AsQJbl4gk4vwCCIEiSpNFornqyAIZhimQlUFVVr9efrvJ9dcnn89PUl+KhsEF4zSULkGXZZDIVoat02ZMFfACu3WQBRaVWVzhZwAehaC2SIAg4jhenbNPhrzRZQBEa3PNxDYl6xSj1SYkSJUqUuML81blKJS6WkndSokSJEiX+mim5SiVKlChRokSJEuel5CqVKFGiRIkSJUqcl0tyGhFF49mRcC4jIwCACrAZZYYyE3tOuUqkyN3jcbPN7NKfVSz1ShajuVhUWcyk09m8ajQadZqpJQxRJplUMVyr1UFFiMbTKk5bTQaKxPO5dCyZwUiNzWok8FOeKJLFYCiMSK3bboYQIFUVuExOxq1GraoquXQyw8t6k9mgeT9VEosLVQ6Hw3lJRQhgBOlw2DCgREMRQNI2m61Q3VDMC8lEvPAZmtWYzCaawESBy/J5mtFoGJLLZNKZHGsw6nXa91VXt3gRBS6VSvOiDBBgtFqjwUCTOABAVcR4LCED0mwyUBQBARD5TJoHJqO2MIvkPB+MZjwee6GsPUKqmEuFEhyj0dqsJgwAVZHzfE5AlJbGUokEL8oAIZJhjSazhrpmDvZeWkQ+lxUkVqNlaRIAlEsnRUTqdBoSxxBSk7EopjHqWertLlXioTAnQ5fHSUCQ5zKRWApgGKs1mA0aLpNKpDmcILR6g0l/OQ/5IlXOc7GMbLeZpppQWcpnczlIMAYtw+eyyTTHanUmg1aV88lkOsfnCZo1m4zstOsufxARuWwmleJYvV6v1+BITSUTmaxoslm0GuZU0XMkRwMRQVZUjHA5bRSBR4M+XgI2t5slcQiAqiqZZFyl9Gbd+yn8/H6ERqqYS4eTOa3OZDFpkarwXDaR4jR6o0nPSnkhmUwokDSYLFr6PfQFyfloMqc36BmKlPN8JJbAWZ3VqMMgzKXjiTTP6M02k/btrkCikInEMqzOZDFqAFJ5LptMcRqDUUfj6VQyK0gAAYphjMYzw4dUJZ1IQYrS6bSqyMcSKUhrTXodiUMunUxmcnqLXff21J0mqiLzHCciwjylcrCqKtlsDmK4TqtFqphMpEQFM5oMDEXwmXQqm5NkRWswG/XaM+WkkRqPhnGtxcCSEEJJyMSyqtNmRKqSjkXTgoTjuN5sM7AfaCoiAJIpLiuqViPLkrgqif60iBAgSMJtPFWBWFXlcFwQEcAxzGFiAFKjCQGSuNXAEBDweTGRkVkNadJQp1UJAcRxooyghiF4TswIkoIggNCsp7U0AQFIpTmMInUMcU7f4o8++mjhlSAIDHPWrFUVOZ2IpjIcpTlrxVJVVVEUHMcLsRUIoLGJ2LaOwObOYPt4sieYRRAvt2oIRfYl8wRAQzEulRUSyexze/ppm90GpfGUaNSQEie0+bJ5gOkJMBrM0BoaqqovluUArqcu13YXz/MMw0wngBap0sRw367dezu6x5JZ0ep2ashTKsTFAts27fZnJJfD2Hv88MFjXa3d/RqT2czCnVu2n+wd6W3rw+1Oh1GLYRCpcs/hnVtbBk529drKqswaIuIb3rF1zwRPzqi0hr1jmzft6h2dDIaTZZVlNHHqJwpByCRJXsVYX0mSAAAkSV7EcSVZaD60v71rdKD3xOG+0OymGm/P0Y1bWib94yJp9dgNEKJ0Mnay5Wh711BHZ6cvmi6rqdFg8kBn24GWDkJnpPKJg0dajx7rjGTyFqtlapFtnudpmi6S4OdcLvc+QskysWDnyfaTXQMnjrdHMrKrzK1jSADU7pNHDx052d42oNA6q0Wfjwf27Nl9coivr3EyFIFUuffo3v/d0n7Dsnk4BiFAEp/a+MYbbQOBiZEhwlJmZqF3oHvXgeaYqnPoYMeJ420dQ10dnSOBqLWixqI5ZbMKkc/XVuAqQojnec3FV6pHSr7jyOGD7SN6i81q0ChCYsemTcNJ1eO0sxTBxcdeef410VjhsRkIDAIAImMnX3ujZWiwK0tbKm26obb9r2/tjMWiKqGzGYm2w3u27+9LpFKExui0GQqiKIqiKMolVFKkKqmof/u23V2j2Vmzq4i3m6wqsn9saM/u/VmVstJKS0vLnpauaCJrtFiU5MTeQ0dbO0dTvGK1mg3aUzb88hkQPhk8cvT4web2EX9cZzQo8Yndh463nuwOpkWH3aJlKACAygWee27ryIRvLBivrakIDhzbuLtlfGRyMJCYWV+FQZSJ+d549c0Y4270nAmMKqShYVn20goMAAAI5bnkxjde7xjwD/WNW2uq1Ex45449nb0j3mDCajeOdrXu2HNycHwiI6Jyj+t0yfpCQq+pUbeikOk81rytudftcRlYvGX3vqMdAx09/XZPOaWkX1u3cWQs1No9WFVbq2dIAJCQS21/c+PJ3rHhwWFrZS3Kxg5u33W8Z8wXTphN2tGejmPtA50dXWP+uKO83KQtmDuU9E9s2rA/peBut6Gj5eCR4x0nBiaMFiurxHdsOtDR09c7Gq+q9rA0eVorLmyRFCnvHe7bvfdoTCLryu0FbVIlYXyod8f+Fk7BK9zWwZ72Q4ePtbUP5iFtMes7mw+1tHYPj00AjcluMVKnOgVx8bHnnv4LcDWUW7W58MSWzdvah6X5cyokgdu87oWu4UgwHGHt5Q79KdNdSKp0scPqD8S3doW6fanRrFJlYRPe0MtdsUCKjwuw0aHFIEAIcanMnw6MBzgpkJHKDPTQeGhTd9Qb53gMN+DK0Z7AvsFEOJPX6hgzSwAAAFIjieyeDr83ozgMTCCcbB1PdnsTx8ZSRgPr0FFCNvfSkXEBEm4je3pHRxRFWZbPq0VIVdLx8LgvlIyHfeHUBZoEAXQ7Tbdc56k2MzU2w62N5j5vcjiSS0eTmztDk+HE60fGtncGB4PZYE7KZrn1R8e6Ajkul33jyPjJ0fiW4+MjkezhE2OtwVw6x711dMKfKYoUZKqY6+lsbz45KqTCLceODkRyhdwaqiJ2HW95c93WroFJjsuNjfklhA21Heoenkin40MTEa3Bkhk9/taeHl6UEUKKkHnx+Zeg3ir5j768u51LRbdv2bpr597OkYAsCqP9nbsPdSNROLxrpzdxrWaeOANG2B1uh93Sc/JoOIcgkvxjIzkRRQZ7DrQMKgABAEmKsTpcGhJNjg37k3mSwOIhb/P+fXsOtfqDkc6WYwebW/qGff5ALC9KV7s9lxiKYaw2h4ZQR8YmoymeIHAAABKTO3cc9MX5TGBg8+7DgXDg8M492zZtOXB0lBdkBFAmPLp5y/bX9hyTEQIIAQTEXLp3JGKxmOKjJzfu6YhHJte/vH773gNdk3GCpCw2h5ElQr4JbyRLk3+dW0ooOD6we+e2HUc6QskcQmr/ycPbNm460TvB5WWk5I8d2Llh3VtD/oSsIgAAUsWD6/8ymqWsTO7ZP7+V4vNtB/bsPd4biCQZLctnkkf37z3SMRRP52jm8u2CIFHMHti6aeuOHS2tI8qZVD4ol4q1Nu/fvvvQ4MjEWH//seNdCpB6OzuOtA97R/oPHWlpH5iUFJUkicuf/weN93W3tvUKqnTQ/OuLAAAgAElEQVT84IFjJ7pbDh/uGg3ISnbH7sOTgWghBVFipHfz3qPd/UMKTuIYNjnYxeFGh5l58cnnIoIsi/zxg7s2b9/T4U1dmZRFCKm58OCzrx9gtGzHgbf29/vGupvXbT3qC0wEg/F0NhMJhkSMzUb9h/YeiGTPa3YQkvo6Tu7ctWfngdZ4OsdnQus370YEEzy+/1DXWDLqHw5k7E5H1443Dg+ECsoq8un+AR9BgCP7tvb4Ev7R/j17TkAIuo8d6fUlTVabgSX8vsmJcJokTz3kkcVc14mW19ft6Bn2Z6PDuw60JnkY7D92qGPA653wRbOYmt/8xu54Ojfd9qtKPOTbtXXr3v2H+sYCp1sT9I4e2L1lx+6DA6N+JZ9uPnx8yJtIh8Z27Tk0OuE9euhwy/ET/mgaxwkcO+21i4d3bV6/bvNoOKOq3LbnX9+2dcuhoxMqQEI2un79pp7BsQyHNMwHfWB1tMfbFhEIXPzLMV8kK7b2BQ6OpQZTko4lTm/XhYLxdV3RiZQEKTyfzx9u8w3mUSqdebMrHM/kfTFekOWesUhP6NTazWe49v7AhhPeNl+GU6Bex7psmkgyN57KKwAAJLf2+te3B/qjnKSeOy3P6yopkhj3jaVFlSIgJwgXbBS0mLSLai01ZrraqllWrs3m8vGclOeE/nA2lRPGfEmcZhrdeg2JHe32bhxKNbn1qWD4qZagkBdP9ni3j6b1hLylI5xKpDsDvENTHElKIGRprYGhJQJQeq2OxAACAKDw6FBfIEfpcD0jA4xeeduaZfOrHCaTjmFw2vzwIw995KZ5Oi2pinLBCAhcqj0hPXTnqgdXOdpa+kVFJrT2BU1uBBCAGMWwFhaDUNbq9BSJXQOZzi4MTs1btGTJbEcob/zsQ2vMOu3spbfed2sjRhBGkwYiAADQ6Y3zr5tfXWExO1w3r16pU7NDwyNJXrJaDaosTfr9ClAq3AaGIVHxPpt9n2iMtjkL5npMVGVd1dLlC6w6GgAA8qlkBtU2zV21tD7oG0un4oC1L57hYmkcAKCKXPP+Zq2nUk8iUKhMAgClMX/605+66foGUsJkSUQA6azu+fVWhIBGa5i7YH5jnd1ss6xefWO54dp/qnvxiFyyra1XRpLFplURSPmGWrt8RkanYyiE0ETPiU6fbHHqSRICABAAQBGOtQZvfejme+6+IdLZlcjysayycFGdHmb8kVRe5EVIz5lXRkipaDJ3+ZQUIRUQzOolrrwMUEEwAGSR906OjIfSLrdNldVQMkXptQ/fscyhJX0TvmgO2ayOahuRS8ezQh5cfgsSDqdojWH1qsVVRiUejym0QUNguCzojDqCpFBhDQskqxorGmos6UCAk+QZS+/87MO31zlpUSBkVQ2NdnUMpRprLOgKiPs2EKccBouqcorJaIRicLyPo41VHgtLQ1Znum7VTX+zdmmZhQGKorxjmTwDUkQZm9FUYzToAELZZChHMTesXHxjjbNrLIjrXH//uU+tnOsmRVFUThUVYPWmBz/10RkuHWTNBlLOZGKYs/G2VQsrDKQvzjfMntNQYbFaTCtvWukysQAAhBTvcL83ljaaWC2ppEKDeY1l4cobb5nj9o9GJbLigYdvr3ZQFpfxYjJmIVUFOotjRp3z9LxCCIgKsLmcDVVuQlFVMZPj1IraWSuWNOTi3oh/DGiYihoPqWQzqaysnKqJNNF5tM0P3GUGDIMIyHnMcvsyhwwQQKrCRUlTbV21I5+OpVMX9hneS1wAzFoSAqTKqp0lCQiCvDrPoXUDcSTGFewgQiCdy1e79JUMioSzMkJ6hiRVRABgZSmLUXPzXPciO0PjZx5SybJq1FJVFlaLQ4hh5Q7DQieDYdjKRnujXRMNxLsTqoMCDAbBO6bmeV0lVUUil9dpWQVBicu+Z9sgPHdZk2SEEAAI4BjWUGEqs2pIHPoyAqkChoCZFJenaKueWT7L49HTcxtso0OhrtGEzW22a4sixyBCgCAhjstcTsJkklJVAJDIJU+caJcwyu0289mUICO7y2U06MvchkAgKSLSaoA7X9nUEdTdtLKRoXAAgKyIAglJCHECKjmRMtnvvPM2u0GDEAQAQJyQIMlzHEHCK2g3Lh8IIbWnebe2bsWsSgtOUA63x2YzGj32uHecF5VCOSU+HZvwBklrw+wqy9jIYP+oV2+1s4SSzfG8kGV0ljlNrsGevr6RoPxh6JOzEDKxgbGA2epoqnKeUhnaWOPRD3QcPdY1yvE8jutuuuuWphobhUOE0GDr4dYJfkZtGaWI4XgaAAABIFmdRYe2vrZ+IKlds3qezVl17wO3OPVkQQklLjk+4RMoz4Kmsr/CVA9IlYY7OydCOZvdoQViNhHds/9QjjRZbTYpl0nF/Ft2HjCVVZlM2nQ8kZdkgBBQlISIMRSOcJyUJQippXes/dQDaxod5JubD2Ia6y333P/wHav0ILvzwEnxcpUagjRjuPmujzS4aEUBACCAEEJqNORvbetgzC4ji+U4PpvnEcyTOI5UJCuorGHO2nvX3r2ibqx/sHc4KF9+I+IpdwExfehA80QwIiuI0mBIFbmcAAGBQOFuCJhrZn3y4w/eveaG3oPbh0IZi7siMtD69PPbVz14rxWm17+x1VjeZGGJfCrBSVemThEEEGp1MJvOyZKGlWUxL2q11rraukBvS/8kp6WJvpNHjw0GGxZc5zCcdwGCkJq3+PqFs+o1NIkAUCSBBDiEEMdwLi8xeosJS//puReFqkXLGp0AAAghSesrK1xajc5lMo6PTMqSJBAsjkEcQUlWRC4zMjahkIZFM6sKi3Eu6j9+ojsPNGUuM5fNJOMplQAYgeM4pnASqzM57RajzWGE8clYVlKmN9wQt3kqVq9eZTVq0Nu+EoSgvLph2YqVTrMeqgCjDG6b1jvYfqxjMMPxOE7fuOYjDzz4QJlWPNbRk8xwCCEpG9mwba+7foZBR6ViMUllHvjix+qchXtayOqdn/7CZ+64ZQVKDO4+MvzBtguRnsAURc1yqgYDAILFsys/vrT8xjLqxSOTgooAAhBCl9v+5dU1y6qN7X3+ibRE4hBKCieqFAYZmnJZdXYjzTJYLJUvuL8ao25Bo6PJoXn72Zo6NhnnMLLWbaDV/IHusFbHmGkim8sLknKOJp3XVcIwjNHpWZ1Rr2Giwcj0WgcAABSB0xgaDKb3jKWSggwhAAAjCQyDQFXRqrkV11vgzr4Ya9TqVMWgZxgSq7ewVrvZAYRNQ9nlTTYaKwrrrvCJSNhHORpvXzafyCaHhnxen290fCLB84mIP5lMjkyEgpOju3fsFglzUznjj0ZyuczuzW/tOT5+y4P3LG4sQ3ysrXsMkoxNkIM50RfkLVU2CidpioAQAghkKR8O+URzxU3LriN4/3goc7Ub/YFBAInpPXsOrb5pFYmBPJc6vHO3X7Atmlk+0TOYyWQnx0ZiGT4W9EdC0frZc2lcTSVS8WAwEY16J4OxRAIgVkebrAYzjqAkf+g8JQRiwYm0jNvKavUULnKpkfGJGIdqaittRi0GFZPNSTFaiiIx7NTNh29yVMXknp4hIGY7+0YykdGewbAoZndueKN5IHbnxx+4rsaO4xRNk/DUcR6UCIeDvpCnYab+A2+DX5Oociye4LlkLJnxT3q9Pu94NJfPhCLJ9OTISMA/GeLVTGA0ns6PdPdn+FR3W29GxKrt6thYko8FJZOVAmIkGNUZDSYdywuCkM0m4hmD0aRlaeFyViiDEGMY+u1hRFw6PtDXF0tlQ95ALhkd90biibgkACRi/nhGxaBGQ+dSUUmWzEYdBEiSlMv/OAvaHK4yj5uicBnXalhqYmjE4iq77ZYVSiwUTyTGRoaC8XQwEpZVzGwyYwDJihruPfHMn9/Q1i35+0/eTIiZfm+aT3vH/KnIxECcuxI1LhFSM/5On2y9847bZ+ml1s6AyeqgEGm2mnUMSqUS3W1Hth7qqpq//JZVi9kLxJJAjKIoHDt15JdhDUKe5yQllI6XW7SqkNzw8l9aAvDzn/9UpZnNxP3d/aPpyOj6bc3Oprn1TqxvKEwxGjwbzAj5rCyZDdp0PBxNpCyVM8wsLue5Se/k0NBIKp0NhcOxeHTIG+IRA7OikE5HEmmdUxcebj94bKh65gI6Hoik+emON4Q4TlCFB3wQqKoUCoXGvCEMJ0ji1GknSGnKK8odFj0Eis5iB0hOZ3iG1Zv1WlmR83xqoH80EQ6FeJgLDMcy8nBnNycBVkMXMu8hpGbi/qyALGaTkYEZQf4g4wWBenIyW23R3zHTloplUwI3GRNJirLoSEVCKlK6xuIZQYolhTzETQYaADUrCMNRYUG9fZ6H7fclx4OJgwNRrVHrZuFELBdOcuORnIwgQZy2rADJUqc3YzVp3UZGFsWwgqdzUkJEwxEuLcjq2X17XkuKk6TFU+6PJBJIqayvuUCrVIQUWZVVVG7VQpKmNezKWqM/J8o4McfJ6hhqbrlBTwBJAbM95hkek82Otg/zdKPtkVk5byQrSYqGJmiaWFzOrIuR17m1sqqS+NU/uovROofNebJvcH92gjWXuUywre2ERBjmL1laHU+omYhicOj1Gl/XiTe7OnM5bu6yWizn33PgZBKQ4wMt+yliiSf7+huD//qNhx9avfCNF57LxeB9axcRECoQo1iWpUmCoOxWhzbfvONADlrrPeZrIH3+e4KEdDBFPTDLAwFESE1EJrYd6bWalOtvXa5wsaMH9jgW32XPCQoka6ttGEbU1DfhpGZsdDAtIovV2lRr3ne4Y/POFltZbUOlgygKt/kSomZTKVant3s8EAAuETh0pHPG7DkUhcliTlAMN65YareZIIQ4xZoMNI7DGUtu0FYmY94hm2Wy3GmJDDZvand8co1l255jWY1zrOfYAUy66fr5EMNpRqujCABANieKCphT4/yQxQ9OE4iRDfMXMDant+9EUk06nO6GObW5bOpEKkrRLpurcu2dZj6b8vZ3WircLMa/8PqbD375K7ffc9uruzbE2ehND91hpFF0vPeFZ/2kwN97x80UEEe7jp3sG9QA/NZV88nLaZwgxAjKaDbRAMlR78jWzQfu+MSnb71tTSAU5LIpncM6e2ZNLh3bsGm3wehYObdWjvYfazuUFQRrecOMGhdx+XcRIcQIiDJpvqJh7tyZjaJPOt47smt80OCy2Uxs++Et2qbV2lzmwP7jrTRVNveGOgd78NmN3WOxRRWJTa++cvfDaz/+yQdFgcuMduWd7vcMN7tEMkONraqGGdiwYVOOMC6eXVdpMpad2LZx617aNbPCpLRsOTLijWvMA8dbmKUrVjr1Fwp9gDipZVkSx3XWykWN7u2b3kxwmjtm18ZGO7Yd6qUdle0Ht8j4vc5c+/oDga88smqos3l8uFvi2dV3LHAZspW6tg2bduKsY36DR4gPIYi7q6shAEImeqL1OCKNy1cuj0ZiYjzBemxlDYtnT+5v3bcpzsMbP1JtgdHNe/adPCqj6vkzy63U9M/sQwAxjGZYhqYUUejp7fIm5Ec8TohhjJYlNRQAkCKhKnN5Rbto0aLKckfLgcMnW1sycX7BzU0aLPvqjiN3rFl1/913ikK2/8QRd4WnEISEUyazmYIAqqrUsW/PSJ9ZhGW3L6/7YDMR1pTpD49ltuZgmctoYKh0xv/awSwOxHuXlNGYvOnAyH23NwmCsLMj2m0kq6ucTXZdxM52DUeCNJrnMeBIGRwLHR4idDQ+v1435o+OJ9CtiyrsNKRJjMEwCIEqykkelbtYq4agFc1N8zwpQQn6IkYzo6Hwc+JIzusqQQzXmW0uiOcVaLFZL9AmUVJiKT7Hi3ajBmBYPCfV2PUmrcSSuIigrGLzK02Az3slOLPCwsp5QLNzHDCeVa5vsAVSIsPqXVp8Yjw6kELL6m0on08puM14GYIgLhKCNc9ZvBKnLWFOrqlvqi8zpGNepDE0NM2iIHJbTQqlKSsvc2npjr6hPG5ctGAmraTvfvDhdCajqrLRoKG0UMtAkmTv+OhHNUfbwYIlqxfUQABIhp274pYy3ELQbNPcJR/F6FBaLqtpqnMarvmlDQJImz/+xa/UGAkAAa0xLL9tDWnugRrjgkULCS7EsCROM05rw02stcLMQgy3ucutrvK6htrG+XGj1eU0kqRWP+pP1DY01nqs13yHnAt0VM240VJr8xgBADhBGrQammRdjY2cgonQvGDhLIuOAQBUzFm9toLVa2nWMsNTDfgZtYS1fm5DVVDoM+hJVmu97+OfFCUJYMCg0wAIGJ15wbLbeMYNIbSVVdx42232MjP4K3z8BgDACKenyuGubKz21Ed5u9NjN+sgUMtspgxmrCp3a2gCqbJJx7DuGWYtNGoJkiJm3bD2TngsIWJLb1yh01N33PfQsc4BxuRedv18BlPW3HN313DA7q5eML/ucjqgECOY8lm3PmInKYhhBKOlNFab1eZZ3phN1TY0QNZS4zLRLGkfCbgqamY1VasVJpw2+lNC44yZdWXWK7Ajr7HYGpsacNbkqqyf0VAJa+wai90fyVQ0zawtd0QNepwiZi1aQTK6QJxvmL3AY9bXLr7hH2euEAQOQoLRmJYvX6HI+TKbUTLVmZkr4yph5srFn/kYHAonzEsqliyuI2T3Iw+j4WC2qmFOlYUEK2+tnMtLYt5kPDuZzbuhd9Y8eLeuzGEhNZp71t59srufWrxyfn0ZHxI+9tnPKvmcrKo6lmAVhmW0elvlw/et6R4KWt3Vi+ZV4zJ35713D05EymqaapwmjqpceSNrKLMBADCc0Go0jMU1Y+5sJOWddidlMJWVl+luRZbeIUXnWdRUbWSqbgX0hD+yom52ndN0MVsKkNVbFi67QSBNGIbRDMMyEgYArbEsXb4Co/U4RlbW1GYEKafo58yb6bbrWAx2D4wBxrFo4QwNiOtNLGu01DfUY0jW0biuan7hxqxs7l0f9xhwDLfXLLz/bjQcTbuqZy1utH2Q8QIAWzarnNUkw7xym9vkNmjvXFbVOpIRcHxZvY2AyEIjnCBnzvB8hIgnFWxmhanCTN+6uNrkzZI0OafCZNfgty6APeG83aKd49EODQsspuI4BiCxoMEjIMJEYxBRN84v15s1LAEJgp5dTgOAzLCONmhtOvIcVTpTMzmZTL6/crmSomZ5URTVKTmS3rkreL73AQDQqCX93liLn1802+WgMRzDdB8sJcMFiMViRqNxmuUtp0ZnIEWMxhKQYKwWI3aeWtPn1KCWuPigNzujoeJ0hoapjiqa8u+d/1sM1S4L5XJZlr24eGOE0NS2nO4RCPJcNhwJ6x3VJgY7x2d/+1PwfB0CAIjH48VT6jgUCjmdzvd16ZlUYvlcKp7mtQajXnM6rur04xcEpvTA6V7MxPxxgakqs5z5vinddKoTEXpXJymdTl+L5XJjsZjNZnsfBXZOT6p3dukZPUX5ge7RiqYGdkqo4NRZCCFEU/V0ihyXr1wuQgAglcukgqFkVUMNAcH5IsUgBOhdRLu8BmSqMFMFAEgN+72k3mLUa8+f8gfCKc2ZKnOhXK7ZbL7kAp8j9Llj+k753uZ85XIRQudOpHeQjflCObKu0nHWl589taZ+lSTkEsk0weotRt3U/jn/0J/Vw9O0SAgAJIvxZEpQsDKHtTAWZ2nIu6GIWW8o5XA6WIo8LdLUHjinN86ZihzHWSyWd/neC8o5padOv1XoQWVwNO4pt2qnbPBCOOWSc90NNZ7I8RJwOvSFI8FnDObZlvLUN5x98LpQLvcSaDiJYx8wjRhCqLzC6vQAljnXlbu6nDUXcdJqs0GIF0zA+Qz31PcJWt9Yb8HP0yQ45d+HinO6ZsqfFKN1e6rIdwtfn/KpD12HnMuZBpKM1sHoMAx/52w6Xy9qjHad5byZrk675JdK1mua88/Eqa/JmqYGkjx3vx2edSG4wtMSQgAgZHX6Sq2h8Az6Ap7ilR/td3Ts6ZeY1enBcAJ7Lzt+FSpLnv2TH3BMT3/ZBRrCGhy1VupdVPs8X4VTjNVOYxgOzjtXLwEQAIATZrMZwFNm58z3n/+XMJItL9Pg2Klb3POJdwlFfZfxObNEYFUVFvodD8LPvWSKXCaj1gjAKVWa+pFzto7e+aNvUxQ36BBCiiKLPC8ehBh+kSeoMOKyZdK8NsEwrEgSSBYJGH7RCkgUu6Jca0C8WFNyQgwnrjFtgZAgiyJ+uRggLnJiFZykK8D7WcuwopqK8CLTxUH8Az81L6bmlyhRokSJEiVKFBklV6lEiRIlSpQoUeK8lFylEu/Blak8ME2KSpgSJUqUKPHXwJmjEgihaDQ6nWsURZFlmSCIqxic9b7J5XKKohT/iRlJklRV5TjuKooqiiIAgOO4q3AG893gOE6SpCKZdblcbpr6UjzwPI9hmPAedYqKC4RQNpstkhl4DrIsy7Jc6NWrLcu5FIMBuVhkWc7n84pyJZJSTpNChWmOuwaqcxatRZIkSRRFVb0yadkvPYV4/zOuEoTQYDBM50pZlkVRJEmSvAZP8CmKotfri2S5vQCFasY0TV9FUXmeBwDQNF0k1hYhpNVqiyRZgCiK09SX4gFCiGGYVqu92oJcBKqqFnS2CL0lURQlSWIYpgjtScHnYBimSJR3OoiiiON4UalVLpfDMIxlr36ev/ekaC1SPp/neb44ZZsOuVxOluWzVh1qeif2IYSqqpIkOc3PFxUEQZAkWSTL7QUo+OAURV1FKyzLMkKIJMkiWQlwHKcoqkjGriDM1Zbi4iBJEsOwa0tsVVULXV2ErhJCqKAgRTInp6KqKoSweJR3OiCEJEkqqvkpiuK1ojJFa5FUVS22Yb0oCtsW18wNR4mrRREuUSVKlChRosQVo+QqlShRokSJEiVKnJeSq1SiRIkSJUqUKHFeSq5SiRIlSpQoUaLEeblkpxERAgigU2Xm4IeljtfZFRbf8fa7VjY9p87pWZecXVPw7Cs+vIeC3q1Hzmnzu3TBmSKOH0YuVevOUxj3Uv7EtcvUHjhPhdcL9dCFdPaK804lOqdi65WR7JwufdfXUwU+x0heoFbuFeEsO/OuFamnKdKU9p5ru9A76q2+s73nlBQH4KwarueT7azC2Bev3e8+h99t9XqPxezsRp3TtEvLO6vfvvNnzvrM2/14AWlODxA6+3r4drncd23KpXGVBgcD6076+jMKROi6Bvf917nLDdQ7m3H6nWvCfot8Luj3heJZCBHJ6twej8OsBwAoQnbC60vk5PKKcqvZoOYSQxMBQBury50sTcrZWM+wjzY4ayvsJFGIPUESl+npG0CUed7sWoDUVDQw6o0ZHZ7aMhtS5FQ0OBpM2ZyeSvfF1V4uJhASku2D0Vlz6kkAEFKGenqcdbOMDC6KucGeQZXR1dXVa6hTVjOXTU6OT8i4xlNRadES8WjY6/WzJqenzKOlMABANDCZkzC7w6Fhrr2EFBcCKelUIhqNS7KKIGY0W6wWM0XgAABZzAUCYUBpnTYLRRIAACGXimYkl82syoJ30iepCGJkRW0tiwMAgCLLk6ODeQXiJGl3Vxs1uCKJiViUU/AKtz2XSQVDEVZvdrpsxF+lw4QQigb9CkZYrDZCzg2N+VJZnmC01W5zIBjh+DwAADK6WQ01DE2+bWfFnrbeilnz9BQS0vG+oXFSY2yYUUchNZeODY4GTXZndZnj8i7wqpLPxkZC+Yb6CuLthZLLZibHxhGtr6qtLox+Oh5JpLJGm8vAQL/PF8vJ5eVlVqPuMgoGUCoWSXOi2eHW0XieSwejGb3RaDHqkJIfH/Xp7HaLUV94ToEQ8o30hVJSbX29Uc8CJHS19ooQqBgzf34TpshDvV0yY5lVX/3Bi3O9u6wIBScGJcZR4TCd8tVUNRv19U/GrM7y6jKbKouxoNefFDyVNXYDI+e5oN+b4EFZeaXV+B6pAVQhPeyNO91OvZZNBCYmgnFJVq2eqiqXBcdgzDuawo11HuspSVQlHfMPTMS0JvvMWg9S5WQsPOlPWD2ecocFAKCKfDgcFRBVXu4kIAAAyXxm0ufnEFvhcRm0VCzo9YdieUkxuyrKnVaaxHOp0GiIa6gup6npmkdZykdDPl8kZ3G4qj22whxWVSkcCAQjGWdZmctmUmTeN+lNC7Ci3GPUs/l0dHQySBod5S4bM7XmmqqMDvWSlmojSPePBQpehtbiaqp2A0VORQMpVVflsXzAcUUIRKMJb0J0OIxOA61yXJcvqyBEsezcCuPpDBiqqsaj6bgEK8zUoDeVVwEAUKOh6t1GikDJDJ/OIY9Df1p8Lst7IxlEUmUWTSbNhVKChACAsMJptLHYaCCdk0FDhUlLn+sa4Y8++mjhlSAIDMOc6Q1ZCo/3Hz3ZNekN8BKyW4xn/ktVFUXBcbwQhooQmJiIHp7IqFqtx6wpd+gpgZ+MJFsH4wqGhfzxg/3RsIDseso3Fu6K5wf7gv2xfKVDiwM4MRx4qzsq4aRbT/ICt/Ww18vJ5Vbt5VEfAADgeX6auUbEdLyr5dCugwcP7Nix6+iQqXpGU7kFKMK2dc8989KbR5r39QSyLod10/NPvLnj0LoN62lrRZXL8MRjP97e3Pb6uq0Vs68rs+lxDCKJf/yHX3vl0PDOdetFR30Vm/vBv32neXhy+4Y3K+ddz3v7fvbjXx/pOXnw4P76BStterrw67IsFzIyXMW0KJIkAQBI8rx17E+TjXp/8dP/fOaNwfseXE3L6ed//5v/eOL1lbevNeL89pd+95Mn3hodONwd1i5dUINDmItPvvXKn554bkd718lef7qMkV559rkNu5sPH+vkce2MuvJ8bPy3v3zicG+isaneYjgzJ3meL54kT7lcTqe7+JVJVWIh//DIyMjwQFtnL64xlbmdJI4pUmbf9u0D/QPHW9s09nKLSS+kA1s3vDmShPWV7qz35EtbmoEqZ3JSZX0lCQBAKpcafu7PGzkPdhYAACAASURBVPMYkRcES1m5hkDBycENb74VylNOLdi/a3vX4MSkf5JTmQqXtTB+hXx611bULkKI53mNRnORDorc27z7xz/7QyBPzmqsTQ4c+8kTL3V092Uktdqp379v34m2k3s2b1jfHLz9xkV6DQMhUPnk80/86tH/fv7mhx/RSdGf/+Df3moZ6mzZMoHK6wzin3/+0z/ubBts67LUzSqznhp3RVEURbmESqoqsnew4z9/9NihLuG2268jIQQA8KnA7o0v/ur3b/X29cby1LwZlWIm8voLz7+86URFXcPYyR3Pv7Ru/YYdvqRYVVNr1NKFbrrEBkSVx/o7n/jlzw50TdYvWKLJB1977rnfv7TN4fFUuUx733rlu99/0VZf11DrLixJo4c3futXLwyeOLr+qHfV0jlYqOXuz/5GBfGxifz1i2ese+o/n9509OSBLcN527I5VafHVVEUSZI+eBIjhNTeQxv/4Rs/xV3zF81wQwgRQpn4+Ne//PWu4ZGtb+w0LFkO/Z0/efRHx7r79rcNLZzf1Lpn4+9+/+KBAwe7hv1Lli2l315ZRVEs5Fw4/eVcKvzK07//zUsHZs+b5bJp1v/Pf/1lX7t/coz21Nc4zeOdu7/+hf8Tc89eNauisIGWCI987x++1THpPbx3F29q1PH+3zz2X7tPdLce621ctMjEYsNdrb/79TPDMbDk+hkkhEjhN7303IvPv7Jp58EMoGuqKta/8NuN23ePTfhwa0W500aB/F+e/MXP32i+deVio05zWrALWCRVEftOHH3sx7863j9w7GiHvXZGmVUHEOps3vHHp363dffh3qGI2VU9cHjDS6++umPbHr/EuByaV5763Y6de154Y4ejuqHCbSewU1tx8bH9n/nk1wwLbq0mgi+t3zrQ3/XqU88PULW3L6jo2rXlx7/49Thdf8PsstMKK8vy+xjW8f6xH+6ebPfGnj4Ru6HW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)

BeautifulSoup has an inbuilt function that allows the user to select an element just by specifying the element name. For example, let’s say that you want to scrape a table. Then you can simply type table in front of beauftifulSoupObject and it will get you the table.


```python
from bs4 import BeautifulSoup
import requests as request
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
mainTable = beautifulSoupObject.table #get table on the page
print(mainTable)
```

    <table class="table table-bordered table-hover main_table_countries" id="main_table_countries_today" style="width:100%;margin-top: 0px !important;display:none;">
    <thead>
    <tr>
    <th width="1%">#</th>
    <th width="100">Country,<br>Other</br></th>
    <th width="20">Total<br>Cases</br></th>
    <th width="30">New<br>Cases</br></th>
    <th width="30">Total<br>Deaths</br></th>
    <th width="30">New<br>Deaths</br></th>
    <th width="30">Total<br>Recovered</br></th>
    <th width="30">New<br>Recovered</br></th>
    <th width="30">Active<br/>Cases</th>
    <th width="30">Serious,<br/>Critical</th>
    <th width="30">Tot Cases/<br/>1M pop</th>
    <th width="30">Deaths/<br/>1M pop</th>
    <th width="30">Total<br/>Tests</th>
    <th width="30">Tests/<br/>
    <nobr>1M pop</nobr>
    </th>
    <th width="30">Population</th>
    <th style="display:none" width="30">Continent</th>
    <th width="30">1 Case<br/>every X ppl</th><th width="30">1 Death<br/>every X ppl</th><th width="30">1 Test<br/>every X ppl</th>
    <th width="30">New Cases/1M pop</th>
    <th width="30">New Deaths/1M pop</th>
    <th width="30">Active Cases/1M pop</th>
    </tr>
    </thead>
    <tbody>
    <tr class="total_row_world row_continent" data-continent="North America" style="display: none">
    <td></td>
    <td style="text-align:left;">
    <nobr>North America</nobr>
    </td>
    <td>97,234,007</td>
    <td>+749</td>
    <td>1,451,249</td>
    <td>+43</td>
    <td>93,381,984</td>
    <td>+471</td>
    <td>2,400,774</td>
    <td>7,079</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="North America" style="display:none;">North America</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="total_row_world row_continent" data-continent="Asia" style="display: none">
    <td></td>
    <td style="text-align:left;">
    <nobr>Asia</nobr>
    </td>
    <td>144,826,271</td>
    <td>+232,493</td>
    <td>1,413,596</td>
    <td>+493</td>
    <td>123,494,225</td>
    <td>+80,133</td>
    <td>19,918,450</td>
    <td>14,416</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Asia" style="display:none;">Asia</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="total_row_world row_continent" data-continent="South America" style="display: none">
    <td></td>
    <td style="text-align:left;">
    <nobr>South America</nobr>
    </td>
    <td>56,486,386</td>
    <td>+93</td>
    <td>1,291,354</td>
    <td>+2</td>
    <td>52,398,800</td>
    <td>+599</td>
    <td>2,796,232</td>
    <td>11,093</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="South America" style="display:none;">South America</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="total_row_world row_continent" data-continent="Europe" style="display: none">
    <td></td>
    <td style="text-align:left;">
    <nobr>Europe</nobr>
    </td>
    <td>185,444,461</td>
    <td></td>
    <td>1,794,668</td>
    <td></td>
    <td>166,358,684</td>
    <td>+287,783</td>
    <td>17,291,109</td>
    <td>9,474</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Europe" style="display:none;">Europe</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="total_row_world row_continent" data-continent="Australia/Oceania" style="display: none">
    <td></td>
    <td style="text-align:left;">
    <nobr>Oceania</nobr>
    </td>
    <td>6,348,694</td>
    <td>+63,060</td>
    <td>9,869</td>
    <td>+62</td>
    <td>5,730,650</td>
    <td>+11,686</td>
    <td>608,175</td>
    <td>161</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Australia/Oceania" style="display:none;">Australia/Oceania</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="total_row_world row_continent" data-continent="Africa" style="display: none">
    <td></td>
    <td style="text-align:left;">
    <nobr>Africa</nobr>
    </td>
    <td>11,816,300</td>
    <td></td>
    <td>253,358</td>
    <td></td>
    <td>11,053,054</td>
    <td></td>
    <td>509,888</td>
    <td>957</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Africa" style="display:none;">Africa</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="total_row_world row_continent" data-continent="" style="display: none">
    <td></td>
    <td style="text-align:left;">
    <nobr></nobr>
    </td>
    <td>721</td>
    <td></td>
    <td>15</td>
    <td></td>
    <td>706</td>
    <td></td>
    <td>0</td>
    <td>0</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="" style="display:none;"></td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="total_row_world">
    <td></td>
    <td style="text-align:left;">World</td>
    <td>502,156,840</td>
    <td>+296,395</td>
    <td>6,214,109</td>
    <td>+600</td>
    <td>452,418,103</td>
    <td>+380,672</td>
    <td>43,524,628</td>
    <td>43,180</td>
    <td>64,422</td>
    <td>797.2</td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="all" style="display:none">All</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">1</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/us/">USA</a></td>
    <td style="font-weight: bold; text-align:right">82,192,880</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,014,114 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">80,052,061</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,126,705</td>
    <td style="font-weight: bold; text-align:right">1,559</td>
    <td style="font-weight: bold; text-align:right">245,753</td>
    <td style="font-weight: bold; text-align:right">3,032</td>
    <td style="font-weight: bold; text-align:right">993,285,213</td>
    <td style="font-weight: bold; text-align:right">2,969,875</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/us-population/">334,453,530</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>4</td><td>330</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,369</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">2</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/india/">India</a></td>
    <td style="font-weight: bold; text-align:right">43,039,023</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">521,767 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">42,506,228</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">11,028</td>
    <td style="font-weight: bold; text-align:right">698</td>
    <td style="font-weight: bold; text-align:right">30,652</td>
    <td style="font-weight: bold; text-align:right">372</td>
    <td style="font-weight: bold; text-align:right">794,525,202</td>
    <td style="font-weight: bold; text-align:right">565,851</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/india-population/">1,404,124,784</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>33</td><td>2,691</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">8</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">3</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/brazil/">Brazil</a></td>
    <td style="font-weight: bold; text-align:right">30,210,853</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">661,710 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">29,167,518</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">381,625</td>
    <td style="font-weight: bold; text-align:right">8,318</td>
    <td style="font-weight: bold; text-align:right">140,355</td>
    <td style="font-weight: bold; text-align:right">3,074</td>
    <td style="font-weight: bold; text-align:right">63,776,166</td>
    <td style="font-weight: bold; text-align:right">296,295</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/brazil-population/">215,245,721</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>7</td><td>325</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,773</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">4</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/france/">France</a></td>
    <td style="font-weight: bold; text-align:right">27,310,055</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">143,777 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">24,492,534</span></td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,673,744</td>
    <td style="font-weight: bold; text-align:right">1,541</td>
    <td style="font-weight: bold; text-align:right">416,755</td>
    <td style="font-weight: bold; text-align:right">2,194</td>
    <td style="font-weight: bold; text-align:right">260,504,402</td>
    <td style="font-weight: bold; text-align:right">3,975,327</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/france-population/">65,530,304</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>456</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">40,802</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">5</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/germany/">Germany</a></td>
    <td style="font-weight: bold; text-align:right">23,116,402</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">132,906 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">19,444,600</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+265,300</td>
    <td style="text-align:right;font-weight:bold;">3,538,896</td>
    <td style="font-weight: bold; text-align:right">1,980</td>
    <td style="font-weight: bold; text-align:right">274,345</td>
    <td style="font-weight: bold; text-align:right">1,577</td>
    <td style="font-weight: bold; text-align:right">122,332,384</td>
    <td style="font-weight: bold; text-align:right">1,451,840</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/germany-population/">84,260,248</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>634</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">42,000</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">6</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/uk/">UK</a></td>
    <td style="font-weight: bold; text-align:right">21,715,116</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">171,045 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">19,973,929</span></td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,570,142</td>
    <td style="font-weight: bold; text-align:right">385</td>
    <td style="font-weight: bold; text-align:right">316,916</td>
    <td style="font-weight: bold; text-align:right">2,496</td>
    <td style="font-weight: bold; text-align:right">511,698,520</td>
    <td style="font-weight: bold; text-align:right">7,467,868</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/uk-population/">68,520,023</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>401</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">22,915</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">7</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/russia/">Russia</a></td>
    <td style="font-weight: bold; text-align:right">18,030,579</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">372,512 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">17,299,263</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">358,804</td>
    <td style="font-weight: bold; text-align:right">2,300</td>
    <td style="font-weight: bold; text-align:right">123,458</td>
    <td style="font-weight: bold; text-align:right">2,551</td>
    <td style="font-weight: bold; text-align:right">273,400,000</td>
    <td style="font-weight: bold; text-align:right">1,872,017</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/russia-population/">146,045,714</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>8</td><td>392</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,457</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">8</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/south-korea/">S. Korea</a></td>
    <td style="font-weight: bold; text-align:right">15,979,061</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+148,417</td>
    <td style="font-weight: bold; text-align:right;">20,352 </td>
    <td style="font-weight: bold; 
                                        text-align:right;background-color:red; color:white">+318</td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">962</td>
    <td style="font-weight: bold; text-align:right">311,194</td>
    <td style="font-weight: bold; text-align:right">396</td>
    <td style="font-weight: bold; text-align:right">15,804,065</td>
    <td style="font-weight: bold; text-align:right">307,786</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/south-korea-population/">51,347,631</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>3</td><td>2,523</td><td>3</td>
    <td style="font-weight: bold; text-align:right">2,890</td>
    <td style="font-weight: bold; text-align:right">6</td>
    <td style="font-weight: bold; text-align:right">291,916</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">9</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/italy/">Italy</a></td>
    <td style="font-weight: bold; text-align:right">15,467,395</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">161,187 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">14,078,350</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,227,858</td>
    <td style="font-weight: bold; text-align:right">449</td>
    <td style="font-weight: bold; text-align:right">256,491</td>
    <td style="font-weight: bold; text-align:right">2,673</td>
    <td style="font-weight: bold; text-align:right">207,575,724</td>
    <td style="font-weight: bold; text-align:right">3,442,169</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/italy-population/">60,303,766</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>374</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">20,361</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">10</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/turkey/">Turkey</a></td>
    <td style="font-weight: bold; text-align:right">14,978,031</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">98,493 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">14,688,473</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">191,065</td>
    <td style="font-weight: bold; text-align:right">975</td>
    <td style="font-weight: bold; text-align:right">174,260</td>
    <td style="font-weight: bold; text-align:right">1,146</td>
    <td style="font-weight: bold; text-align:right">156,514,251</td>
    <td style="font-weight: bold; text-align:right">1,820,940</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/turkey-population/">85,952,426</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>6</td><td>873</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,223</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">11</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/spain/">Spain</a></td>
    <td style="font-weight: bold; text-align:right">11,662,214</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">103,266 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">11,120,708</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">438,240</td>
    <td style="font-weight: bold; text-align:right">368</td>
    <td style="font-weight: bold; text-align:right">249,262</td>
    <td style="font-weight: bold; text-align:right">2,207</td>
    <td style="font-weight: bold; text-align:right">471,036,328</td>
    <td style="font-weight: bold; text-align:right">10,067,681</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/spain-population/">46,786,975</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>453</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">9,367</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">12</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/viet-nam/">Vietnam</a></td>
    <td style="font-weight: bold; text-align:right">10,297,587</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">42,878 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">8,770,994</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,483,715</td>
    <td style="font-weight: bold; text-align:right">1,205</td>
    <td style="font-weight: bold; text-align:right">104,126</td>
    <td style="font-weight: bold; text-align:right">434</td>
    <td style="font-weight: bold; text-align:right">85,511,551</td>
    <td style="font-weight: bold; text-align:right">864,665</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/viet-nam-population/">98,895,617</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>10</td><td>2,306</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">15,003</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">13</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/argentina/">Argentina</a></td>
    <td style="font-weight: bold; text-align:right">9,057,923</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">128,285 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">8,889,899</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">39,739</td>
    <td style="font-weight: bold; text-align:right">424</td>
    <td style="font-weight: bold; text-align:right">197,198</td>
    <td style="font-weight: bold; text-align:right">2,793</td>
    <td style="font-weight: bold; text-align:right">35,681,964</td>
    <td style="font-weight: bold; text-align:right">776,825</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/argentina-population/">45,933,081</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>5</td><td>358</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">865</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">14</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/netherlands/">Netherlands</a></td>
    <td style="font-weight: bold; text-align:right">8,006,753</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">22,138 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">7,191,937</span></td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">792,678</td>
    <td style="font-weight: bold; text-align:right">106</td>
    <td style="font-weight: bold; text-align:right">465,447</td>
    <td style="font-weight: bold; text-align:right">1,287</td>
    <td style="font-weight: bold; text-align:right">21,107,399</td>
    <td style="font-weight: bold; text-align:right">1,227,012</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/netherlands-population/">17,202,278</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>777</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">46,080</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">15</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/iran/">Iran</a></td>
    <td style="font-weight: bold; text-align:right">7,199,861</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">140,711 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">6,930,509</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">128,641</td>
    <td style="font-weight: bold; text-align:right">1,376</td>
    <td style="font-weight: bold; text-align:right">83,813</td>
    <td style="font-weight: bold; text-align:right">1,638</td>
    <td style="font-weight: bold; text-align:right">50,079,995</td>
    <td style="font-weight: bold; text-align:right">582,976</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/iran-population/">85,904,040</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>12</td><td>610</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,497</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">16</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/japan/">Japan</a></td>
    <td style="font-weight: bold; text-align:right">7,180,734</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+56,704</td>
    <td style="font-weight: bold; text-align:right;">28,825 </td>
    <td style="font-weight: bold; 
                                        text-align:right;background-color:red; color:white">+60</td>
    <td style="font-weight: bold; text-align:right">6,642,021</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+50,912</td>
    <td style="text-align:right;font-weight:bold;">509,888</td>
    <td style="font-weight: bold; text-align:right">467</td>
    <td style="font-weight: bold; text-align:right">57,086</td>
    <td style="font-weight: bold; text-align:right">229</td>
    <td style="font-weight: bold; text-align:right">45,167,148</td>
    <td style="font-weight: bold; text-align:right">359,073</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/japan-population/">125,788,137</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>18</td><td>4,364</td><td>3</td>
    <td style="font-weight: bold; text-align:right">451</td>
    <td style="font-weight: bold; text-align:right">0.5</td>
    <td style="font-weight: bold; text-align:right">4,054</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">17</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/colombia/">Colombia</a></td>
    <td style="font-weight: bold; text-align:right">6,088,912</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">139,734 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">5,921,849</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">27,329</td>
    <td style="font-weight: bold; text-align:right">342</td>
    <td style="font-weight: bold; text-align:right">117,440</td>
    <td style="font-weight: bold; text-align:right">2,695</td>
    <td style="font-weight: bold; text-align:right">34,204,521</td>
    <td style="font-weight: bold; text-align:right">659,720</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/colombia-population/">51,847,041</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>9</td><td>371</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">527</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">18</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/indonesia/">Indonesia</a></td>
    <td style="font-weight: bold; text-align:right">6,036,909</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">155,746 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">5,814,688</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">66,475</td>
    <td style="font-weight: bold; text-align:right">2,771</td>
    <td style="font-weight: bold; text-align:right">21,664</td>
    <td style="font-weight: bold; text-align:right">559</td>
    <td style="font-weight: bold; text-align:right">93,593,555</td>
    <td style="font-weight: bold; text-align:right">335,863</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/indonesia-population/">278,665,486</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>46</td><td>1,789</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">239</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">19</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/poland/">Poland</a></td>
    <td style="font-weight: bold; text-align:right">5,981,486</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">115,736 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">5,333,900</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">531,850</td>
    <td style="font-weight: bold; text-align:right">268</td>
    <td style="font-weight: bold; text-align:right">158,354</td>
    <td style="font-weight: bold; text-align:right">3,064</td>
    <td style="font-weight: bold; text-align:right">35,895,344</td>
    <td style="font-weight: bold; text-align:right">950,293</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/poland-population/">37,772,917</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>6</td><td>326</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">14,080</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">20</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/mexico/">Mexico</a></td>
    <td style="font-weight: bold; text-align:right">5,724,611</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+749</td>
    <td style="font-weight: bold; text-align:right;">323,848 </td>
    <td style="font-weight: bold; 
                                        text-align:right;background-color:red; color:white">+43</td>
    <td style="font-weight: bold; text-align:right">5,025,527</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+966</td>
    <td style="text-align:right;font-weight:bold;">375,236</td>
    <td style="font-weight: bold; text-align:right">4,798</td>
    <td style="font-weight: bold; text-align:right">43,586</td>
    <td style="font-weight: bold; text-align:right">2,466</td>
    <td style="font-weight: bold; text-align:right">15,691,493</td>
    <td style="font-weight: bold; text-align:right">119,471</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/mexico-population/">131,340,943</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>23</td><td>406</td><td>8</td>
    <td style="font-weight: bold; text-align:right">6</td>
    <td style="font-weight: bold; text-align:right">0.3</td>
    <td style="font-weight: bold; text-align:right">2,857</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">21</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/australia/">Australia</a></td>
    <td style="font-weight: bold; text-align:right">5,260,331</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+53,426</td>
    <td style="font-weight: bold; text-align:right;">6,693 </td>
    <td style="font-weight: bold; 
                                        text-align:right;background-color:red; color:white">+45</td>
    <td style="font-weight: bold; text-align:right">4,756,356</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">497,282</td>
    <td style="font-weight: bold; text-align:right">126</td>
    <td style="font-weight: bold; text-align:right">202,119</td>
    <td style="font-weight: bold; text-align:right">257</td>
    <td style="font-weight: bold; text-align:right">67,979,668</td>
    <td style="font-weight: bold; text-align:right">2,612,006</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/australia-population/">26,025,848</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>5</td><td>3,889</td><td>0</td>
    <td style="font-weight: bold; text-align:right">2,053</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right">19,107</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">22</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/ukraine/">Ukraine</a></td>
    <td style="font-weight: bold; text-align:right">4,988,890</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">108,194 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">177</td>
    <td style="font-weight: bold; text-align:right">115,306</td>
    <td style="font-weight: bold; text-align:right">2,501</td>
    <td style="font-weight: bold; text-align:right">19,521,252</td>
    <td style="font-weight: bold; text-align:right">451,184</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/ukraine-population/">43,266,690</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>9</td><td>400</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">19,014</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">23</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/malaysia/">Malaysia</a></td>
    <td style="font-weight: bold; text-align:right">4,352,611</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">35,363 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">4,196,656</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">120,592</td>
    <td style="font-weight: bold; text-align:right">161</td>
    <td style="font-weight: bold; text-align:right">131,486</td>
    <td style="font-weight: bold; text-align:right">1,068</td>
    <td style="font-weight: bold; text-align:right">57,710,125</td>
    <td style="font-weight: bold; text-align:right">1,743,342</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/malaysia-population/">33,103,161</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>8</td><td>936</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,643</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">24</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/israel/">Israel</a></td>
    <td style="font-weight: bold; text-align:right">4,016,919</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">10,601 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,941,841</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">64,477</td>
    <td style="font-weight: bold; text-align:right">229</td>
    <td style="font-weight: bold; text-align:right">430,723</td>
    <td style="font-weight: bold; text-align:right">1,137</td>
    <td style="font-weight: bold; text-align:right">41,373,364</td>
    <td style="font-weight: bold; text-align:right">4,436,346</td>
    <td style="font-weight: bold; text-align:right">9,326,000 </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>2</td><td>880</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">6,914</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">25</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/austria/">Austria</a></td>
    <td style="font-weight: bold; text-align:right">4,016,540</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">16,324 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,839,507</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">160,709</td>
    <td style="font-weight: bold; text-align:right">190</td>
    <td style="font-weight: bold; text-align:right">441,487</td>
    <td style="font-weight: bold; text-align:right">1,794</td>
    <td style="font-weight: bold; text-align:right">179,853,312</td>
    <td style="font-weight: bold; text-align:right">19,768,962</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/austria-population/">9,097,762</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>557</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">17,665</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">26</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/thailand/">Thailand</a></td>
    <td style="font-weight: bold; text-align:right">3,973,003</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+24,134</td>
    <td style="font-weight: bold; text-align:right;">26,513 </td>
    <td style="font-weight: bold; 
                                        text-align:right;background-color:red; color:white">+115</td>
    <td style="font-weight: bold; text-align:right">3,716,789</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+26,997</td>
    <td style="text-align:right;font-weight:bold;">229,701</td>
    <td style="font-weight: bold; text-align:right">1,496</td>
    <td style="font-weight: bold; text-align:right">56,667</td>
    <td style="font-weight: bold; text-align:right">378</td>
    <td style="font-weight: bold; text-align:right">17,270,775</td>
    <td style="font-weight: bold; text-align:right">246,333</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/thailand-population/">70,111,373</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>18</td><td>2,644</td><td>4</td>
    <td style="font-weight: bold; text-align:right">344</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right">3,276</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">27</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/belgium/">Belgium</a></td>
    <td style="font-weight: bold; text-align:right">3,943,831</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">31,079 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">3,623,588</span></td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+6,545</td>
    <td style="text-align:right;font-weight:bold;">289,164</td>
    <td style="font-weight: bold; text-align:right">173</td>
    <td style="font-weight: bold; text-align:right">337,677</td>
    <td style="font-weight: bold; text-align:right">2,661</td>
    <td style="font-weight: bold; text-align:right">33,220,032</td>
    <td style="font-weight: bold; text-align:right">2,844,352</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/belgium-population/">11,679,299</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>376</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">24,759</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">28</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/czech-republic/">Czechia</a></td>
    <td style="font-weight: bold; text-align:right">3,872,522</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">39,933 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,792,591</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">39,998</td>
    <td style="font-weight: bold; text-align:right">69</td>
    <td style="font-weight: bold; text-align:right">360,426</td>
    <td style="font-weight: bold; text-align:right">3,717</td>
    <td style="font-weight: bold; text-align:right">54,962,034</td>
    <td style="font-weight: bold; text-align:right">5,115,458</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/czech-republic-population/">10,744,303</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>269</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,723</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">29</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/south-africa/">South Africa</a></td>
    <td style="font-weight: bold; text-align:right">3,735,578</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">100,132 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,624,451</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">10,995</td>
    <td style="font-weight: bold; text-align:right">175</td>
    <td style="font-weight: bold; text-align:right">61,605</td>
    <td style="font-weight: bold; text-align:right">1,651</td>
    <td style="font-weight: bold; text-align:right">24,116,414</td>
    <td style="font-weight: bold; text-align:right">397,711</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/south-africa-population/">60,637,961</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>16</td><td>606</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">181</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">30</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/portugal/">Portugal</a></td>
    <td style="font-weight: bold; text-align:right">3,709,026</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">21,970 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">61</td>
    <td style="font-weight: bold; text-align:right">365,643</td>
    <td style="font-weight: bold; text-align:right">2,166</td>
    <td style="font-weight: bold; text-align:right">40,534,335</td>
    <td style="font-weight: bold; text-align:right">3,995,951</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/portugal-population/">10,143,853</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>462</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">79,938</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">31</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/philippines/">Philippines</a></td>
    <td style="font-weight: bold; text-align:right">3,682,083</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">59,891 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,597,058</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">25,134</td>
    <td style="font-weight: bold; text-align:right">289</td>
    <td style="font-weight: bold; text-align:right">32,825</td>
    <td style="font-weight: bold; text-align:right">534</td>
    <td style="font-weight: bold; text-align:right">29,224,500</td>
    <td style="font-weight: bold; text-align:right">260,529</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/philippines-population/">112,173,722</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>30</td><td>1,873</td><td>4</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">224</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">32</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/canada/">Canada</a></td>
    <td style="font-weight: bold; text-align:right">3,604,570</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">38,165 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,361,991</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">204,414</td>
    <td style="font-weight: bold; text-align:right">407</td>
    <td style="font-weight: bold; text-align:right">94,039</td>
    <td style="font-weight: bold; text-align:right">996</td>
    <td style="font-weight: bold; text-align:right">60,083,036</td>
    <td style="font-weight: bold; text-align:right">1,567,501</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/canada-population/">38,330,466</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>11</td><td>1,004</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">5,333</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">33</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/peru/">Peru</a></td>
    <td style="font-weight: bold; text-align:right">3,553,210</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">212,547 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">382</td>
    <td style="font-weight: bold; text-align:right">105,161</td>
    <td style="font-weight: bold; text-align:right">6,291</td>
    <td style="font-weight: bold; text-align:right">29,296,629</td>
    <td style="font-weight: bold; text-align:right">867,064</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/peru-population/">33,788,298</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>10</td><td>159</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">47,946</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">34</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/switzerland/">Switzerland</a></td>
    <td style="font-weight: bold; text-align:right">3,551,790</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">13,767 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">3,121,637</span></td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+15,936</td>
    <td style="text-align:right;font-weight:bold;">416,386</td>
    <td style="font-weight: bold; text-align:right">103</td>
    <td style="font-weight: bold; text-align:right">405,125</td>
    <td style="font-weight: bold; text-align:right">1,570</td>
    <td style="font-weight: bold; text-align:right">20,548,491</td>
    <td style="font-weight: bold; text-align:right">2,343,806</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/switzerland-population/">8,767,147</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>637</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">47,494</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">35</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/chile/">Chile</a></td>
    <td style="font-weight: bold; text-align:right">3,518,800</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">57,098 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">3,257,510</span></td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">204,192</td>
    <td style="font-weight: bold; text-align:right">379</td>
    <td style="font-weight: bold; text-align:right">181,307</td>
    <td style="font-weight: bold; text-align:right">2,942</td>
    <td style="font-weight: bold; text-align:right">36,244,665</td>
    <td style="font-weight: bold; text-align:right">1,867,518</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/chile-population/">19,407,929</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>6</td><td>340</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">10,521</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">36</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/greece/">Greece</a></td>
    <td style="font-weight: bold; text-align:right">3,206,948</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">28,344 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,023,257</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">155,347</td>
    <td style="font-weight: bold; text-align:right">345</td>
    <td style="font-weight: bold; text-align:right">310,373</td>
    <td style="font-weight: bold; text-align:right">2,743</td>
    <td style="font-weight: bold; text-align:right">77,162,026</td>
    <td style="font-weight: bold; text-align:right">7,467,862</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/greece-population/">10,332,546</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>365</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">15,035</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">37</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/denmark/">Denmark</a></td>
    <td style="font-weight: bold; text-align:right">2,943,116</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">5,945 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">2,902,270</span></td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">34,901</td>
    <td style="font-weight: bold; text-align:right">22</td>
    <td style="font-weight: bold; text-align:right">504,955</td>
    <td style="font-weight: bold; text-align:right">1,020</td>
    <td style="font-weight: bold; text-align:right">127,021,135</td>
    <td style="font-weight: bold; text-align:right">21,793,232</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/denmark-population/">5,828,467</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>980</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">5,988</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">38</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/romania/">Romania</a></td>
    <td style="font-weight: bold; text-align:right">2,877,544</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">65,285 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,606,660</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">205,599</td>
    <td style="font-weight: bold; text-align:right">253</td>
    <td style="font-weight: bold; text-align:right">151,374</td>
    <td style="font-weight: bold; text-align:right">3,434</td>
    <td style="font-weight: bold; text-align:right">22,396,439</td>
    <td style="font-weight: bold; text-align:right">1,178,167</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/romania-population/">19,009,562</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>7</td><td>291</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">10,816</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">39</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/sweden/">Sweden</a></td>
    <td style="font-weight: bold; text-align:right">2,491,980</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">18,472 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">2,451,827</span></td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+879</td>
    <td style="text-align:right;font-weight:bold;">21,681</td>
    <td style="font-weight: bold; text-align:right">22</td>
    <td style="font-weight: bold; text-align:right">244,043</td>
    <td style="font-weight: bold; text-align:right">1,809</td>
    <td style="font-weight: bold; text-align:right">18,445,431</td>
    <td style="font-weight: bold; text-align:right">1,806,388</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/sweden-population/">10,211,225</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>553</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,123</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">40</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/iraq/">Iraq</a></td>
    <td style="font-weight: bold; text-align:right">2,322,551</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">25,188 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,290,436</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">6,927</td>
    <td style="font-weight: bold; text-align:right">23</td>
    <td style="font-weight: bold; text-align:right">55,528</td>
    <td style="font-weight: bold; text-align:right">602</td>
    <td style="font-weight: bold; text-align:right">18,409,261</td>
    <td style="font-weight: bold; text-align:right">440,136</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/iraq-population/">41,826,345</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>18</td><td>1,661</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">166</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">41</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/serbia/">Serbia</a></td>
    <td style="font-weight: bold; text-align:right">1,992,677</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">15,906 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,951,872</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">24,899</td>
    <td style="font-weight: bold; text-align:right">26</td>
    <td style="font-weight: bold; text-align:right">229,709</td>
    <td style="font-weight: bold; text-align:right">1,834</td>
    <td style="font-weight: bold; text-align:right">9,338,695</td>
    <td style="font-weight: bold; text-align:right">1,076,531</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/serbia-population/">8,674,805</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>545</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,870</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">42</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bangladesh/">Bangladesh</a></td>
    <td style="font-weight: bold; text-align:right">1,952,162</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">29,124 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,889,879</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">33,159</td>
    <td style="font-weight: bold; text-align:right">1,283</td>
    <td style="font-weight: bold; text-align:right">11,647</td>
    <td style="font-weight: bold; text-align:right">174</td>
    <td style="font-weight: bold; text-align:right">13,905,661</td>
    <td style="font-weight: bold; text-align:right">82,966</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bangladesh-population/">167,606,297</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>86</td><td>5,755</td><td>12</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">198</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">43</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/hungary/">Hungary</a></td>
    <td style="font-weight: bold; text-align:right">1,876,946</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">45,838 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,742,051</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">89,057</td>
    <td style="font-weight: bold; text-align:right">47</td>
    <td style="font-weight: bold; text-align:right">195,175</td>
    <td style="font-weight: bold; text-align:right">4,766</td>
    <td style="font-weight: bold; text-align:right">11,233,362</td>
    <td style="font-weight: bold; text-align:right">1,168,105</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/hungary-population/">9,616,742</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>5</td><td>210</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">9,261</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">44</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/slovakia/">Slovakia</a></td>
    <td style="font-weight: bold; text-align:right">1,757,117</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">19,643 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">1,683,907</span></td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">53,567</td>
    <td style="font-weight: bold; text-align:right">130</td>
    <td style="font-weight: bold; text-align:right">321,560</td>
    <td style="font-weight: bold; text-align:right">3,595</td>
    <td style="font-weight: bold; text-align:right">6,995,626</td>
    <td style="font-weight: bold; text-align:right">1,280,232</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/slovakia-population/">5,464,344</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>278</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">9,803</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">45</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/jordan/">Jordan</a></td>
    <td style="font-weight: bold; text-align:right">1,694,216</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">14,048 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,678,941</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,227</td>
    <td style="font-weight: bold; text-align:right">124</td>
    <td style="font-weight: bold; text-align:right">163,169</td>
    <td style="font-weight: bold; text-align:right">1,353</td>
    <td style="font-weight: bold; text-align:right">16,670,254</td>
    <td style="font-weight: bold; text-align:right">1,605,501</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/jordan-population/">10,383,207</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>6</td><td>739</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">118</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">46</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/georgia/">Georgia</a></td>
    <td style="font-weight: bold; text-align:right">1,652,235</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">16,781 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,632,194</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3,260</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">415,599</td>
    <td style="font-weight: bold; text-align:right">4,221</td>
    <td style="font-weight: bold; text-align:right">16,627,678</td>
    <td style="font-weight: bold; text-align:right">4,182,481</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/georgia-population/">3,975,554</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>2</td><td>237</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">820</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">47</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/pakistan/">Pakistan</a></td>
    <td style="font-weight: bold; text-align:right">1,526,952</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+123</td>
    <td style="font-weight: bold; text-align:right;">30,362 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,487,144</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+71</td>
    <td style="text-align:right;font-weight:bold;">9,446</td>
    <td style="font-weight: bold; text-align:right">259</td>
    <td style="font-weight: bold; text-align:right">6,682</td>
    <td style="font-weight: bold; text-align:right">133</td>
    <td style="font-weight: bold; text-align:right">27,830,633</td>
    <td style="font-weight: bold; text-align:right">121,789</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/pakistan-population/">228,514,903</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>150</td><td>7,526</td><td>8</td>
    <td style="font-weight: bold; text-align:right">0.5</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">41</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">48</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/ireland/">Ireland</a></td>
    <td style="font-weight: bold; text-align:right">1,496,910</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6,919 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right"><span style="color:grey; font-style: italic;">1,346,814</span></td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">143,177</td>
    <td style="font-weight: bold; text-align:right">58</td>
    <td style="font-weight: bold; text-align:right">297,251</td>
    <td style="font-weight: bold; text-align:right">1,374</td>
    <td style="font-weight: bold; text-align:right">11,942,846</td>
    <td style="font-weight: bold; text-align:right">2,371,570</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/ireland-population/">5,035,840</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>728</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">28,432</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">49</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/norway/">Norway</a></td>
    <td style="font-weight: bold; text-align:right">1,418,431</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,783 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">20</td>
    <td style="font-weight: bold; text-align:right">258,056</td>
    <td style="font-weight: bold; text-align:right">506</td>
    <td style="font-weight: bold; text-align:right">11,002,430</td>
    <td style="font-weight: bold; text-align:right">2,001,677</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/norway-population/">5,496,606</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>1,975</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">241,366</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">50</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/kazakhstan/">Kazakhstan</a></td>
    <td style="font-weight: bold; text-align:right">1,305,343</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+16</td>
    <td style="font-weight: bold; text-align:right;">13,660 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,290,758</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+38</td>
    <td style="text-align:right;font-weight:bold;">925</td>
    <td style="font-weight: bold; text-align:right">24</td>
    <td style="font-weight: bold; text-align:right">68,072</td>
    <td style="font-weight: bold; text-align:right">712</td>
    <td style="font-weight: bold; text-align:right">11,575,012</td>
    <td style="font-weight: bold; text-align:right">603,621</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/kazakhstan-population/">19,175,968</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>15</td><td>1,404</td><td>2</td>
    <td style="font-weight: bold; text-align:right">0.8</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">48</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">51</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/china-hong-kong-sar/">Hong Kong</a></td>
    <td style="font-weight: bold; text-align:right">1,194,295</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">8,948 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">115</td>
    <td style="font-weight: bold; text-align:right">157,038</td>
    <td style="font-weight: bold; text-align:right">1,177</td>
    <td style="font-weight: bold; text-align:right">44,972,952</td>
    <td style="font-weight: bold; text-align:right">5,913,514</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/china-hong-kong-sar-population/">7,605,115</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>6</td><td>850</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">154,122</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">52</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/morocco/">Morocco</a></td>
    <td style="font-weight: bold; text-align:right">1,164,189</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">16,061 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,147,424</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">704</td>
    <td style="font-weight: bold; text-align:right">293</td>
    <td style="font-weight: bold; text-align:right">30,890</td>
    <td style="font-weight: bold; text-align:right">426</td>
    <td style="font-weight: bold; text-align:right">11,237,010</td>
    <td style="font-weight: bold; text-align:right">298,157</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/morocco-population/">37,688,292</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>32</td><td>2,347</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">19</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">53</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/singapore/">Singapore</a></td>
    <td style="font-weight: bold; text-align:right">1,148,656</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,309 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,076,802</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">70,545</td>
    <td style="font-weight: bold; text-align:right">13</td>
    <td style="font-weight: bold; text-align:right">193,633</td>
    <td style="font-weight: bold; text-align:right">221</td>
    <td style="font-weight: bold; text-align:right">23,611,604</td>
    <td style="font-weight: bold; text-align:right">3,980,283</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/singapore-population/">5,932,142</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>5</td><td>4,532</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">11,892</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">54</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bulgaria/">Bulgaria</a></td>
    <td style="font-weight: bold; text-align:right">1,147,812</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">36,756 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">944,639</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">166,417</td>
    <td style="font-weight: bold; text-align:right">131</td>
    <td style="font-weight: bold; text-align:right">167,430</td>
    <td style="font-weight: bold; text-align:right">5,362</td>
    <td style="font-weight: bold; text-align:right">9,724,468</td>
    <td style="font-weight: bold; text-align:right">1,418,499</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bulgaria-population/">6,855,465</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>6</td><td>187</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">24,275</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">55</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/croatia/">Croatia</a></td>
    <td style="font-weight: bold; text-align:right">1,110,989</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">15,707 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,089,283</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">5,999</td>
    <td style="font-weight: bold; text-align:right">27</td>
    <td style="font-weight: bold; text-align:right">273,625</td>
    <td style="font-weight: bold; text-align:right">3,868</td>
    <td style="font-weight: bold; text-align:right">4,731,537</td>
    <td style="font-weight: bold; text-align:right">1,165,328</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/croatia-population/">4,060,263</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>259</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,477</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">56</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cuba/">Cuba</a></td>
    <td style="font-weight: bold; text-align:right">1,098,114</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">8,519 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,087,352</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,243</td>
    <td style="font-weight: bold; text-align:right">23</td>
    <td style="font-weight: bold; text-align:right">97,055</td>
    <td style="font-weight: bold; text-align:right">753</td>
    <td style="font-weight: bold; text-align:right">12,920,253</td>
    <td style="font-weight: bold; text-align:right">1,141,938</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cuba-population/">11,314,325</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>10</td><td>1,328</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">198</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">57</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/lebanon/">Lebanon</a></td>
    <td style="font-weight: bold; text-align:right">1,095,099</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">10,353 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,074,880</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">9,866</td>
    <td style="font-weight: bold; text-align:right">186</td>
    <td style="font-weight: bold; text-align:right">161,731</td>
    <td style="font-weight: bold; text-align:right">1,529</td>
    <td style="font-weight: bold; text-align:right">4,795,578</td>
    <td style="font-weight: bold; text-align:right">708,241</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/lebanon-population/">6,771,108</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>6</td><td>654</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,457</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">58</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/lithuania/">Lithuania</a></td>
    <td style="font-weight: bold; text-align:right">1,045,085</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">8,988 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">997,978</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">38,119</td>
    <td style="font-weight: bold; text-align:right">47</td>
    <td style="font-weight: bold; text-align:right">393,661</td>
    <td style="font-weight: bold; text-align:right">3,386</td>
    <td style="font-weight: bold; text-align:right">8,157,182</td>
    <td style="font-weight: bold; text-align:right">3,072,638</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/lithuania-population/">2,654,781</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>295</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">14,359</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">59</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/tunisia/">Tunisia</a></td>
    <td style="font-weight: bold; text-align:right">1,038,668</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">28,509 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">29</td>
    <td style="font-weight: bold; text-align:right">86,279</td>
    <td style="font-weight: bold; text-align:right">2,368</td>
    <td style="font-weight: bold; text-align:right">4,547,755</td>
    <td style="font-weight: bold; text-align:right">377,769</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/tunisia-population/">12,038,468</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>12</td><td>422</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">-1,134.28</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">60</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/slovenia/">Slovenia</a></td>
    <td style="font-weight: bold; text-align:right">992,497</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6,541 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">956,341</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">29,615</td>
    <td style="font-weight: bold; text-align:right">32</td>
    <td style="font-weight: bold; text-align:right">477,289</td>
    <td style="font-weight: bold; text-align:right">3,146</td>
    <td style="font-weight: bold; text-align:right">2,630,208</td>
    <td style="font-weight: bold; text-align:right">1,264,860</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/slovenia-population/">2,079,446</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>318</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">14,242</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">61</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/nepal/">Nepal</a></td>
    <td style="font-weight: bold; text-align:right">978,631</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">11,951 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">966,160</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">520</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">32,547</td>
    <td style="font-weight: bold; text-align:right">397</td>
    <td style="font-weight: bold; text-align:right">5,586,487</td>
    <td style="font-weight: bold; text-align:right">185,794</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/nepal-population/">30,068,204</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>31</td><td>2,516</td><td>5</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">17</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">62</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/belarus/">Belarus</a></td>
    <td style="font-weight: bold; text-align:right">971,649</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6,885 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">928,536</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">36,228</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">102,888</td>
    <td style="font-weight: bold; text-align:right">729</td>
    <td style="font-weight: bold; text-align:right">12,987,175</td>
    <td style="font-weight: bold; text-align:right">1,375,207</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/belarus-population/">9,443,797</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>10</td><td>1,372</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,836</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">63</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/finland/">Finland</a></td>
    <td style="font-weight: bold; text-align:right">920,692</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">3,334 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">46,000</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">871,358</td>
    <td style="font-weight: bold; text-align:right">33</td>
    <td style="font-weight: bold; text-align:right">165,711</td>
    <td style="font-weight: bold; text-align:right">600</td>
    <td style="font-weight: bold; text-align:right">10,512,930</td>
    <td style="font-weight: bold; text-align:right">1,892,168</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/finland-population/">5,556,023</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>6</td><td>1,666</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">156,831</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">64</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bolivia/">Bolivia</a></td>
    <td style="font-weight: bold; text-align:right">903,677</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+93</td>
    <td style="font-weight: bold; text-align:right;">21,901 </td>
    <td style="font-weight: bold; 
                                        text-align:right;background-color:red; color:white">+2</td>
    <td style="font-weight: bold; text-align:right">850,689</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+603</td>
    <td style="text-align:right;font-weight:bold;">31,087</td>
    <td style="font-weight: bold; text-align:right">220</td>
    <td style="font-weight: bold; text-align:right">75,583</td>
    <td style="font-weight: bold; text-align:right">1,832</td>
    <td style="font-weight: bold; text-align:right">2,688,875</td>
    <td style="font-weight: bold; text-align:right">224,896</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bolivia-population/">11,956,065</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>13</td><td>546</td><td>4</td>
    <td style="font-weight: bold; text-align:right">8</td>
    <td style="font-weight: bold; text-align:right">0.2</td>
    <td style="font-weight: bold; text-align:right">2,600</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">65</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/uruguay/">Uruguay</a></td>
    <td style="font-weight: bold; text-align:right">894,984</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">7,188 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">884,907</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,889</td>
    <td style="font-weight: bold; text-align:right">31</td>
    <td style="font-weight: bold; text-align:right">256,066</td>
    <td style="font-weight: bold; text-align:right">2,057</td>
    <td style="font-weight: bold; text-align:right">6,081,466</td>
    <td style="font-weight: bold; text-align:right">1,739,981</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/uruguay-population/">3,495,134</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>4</td><td>486</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">827</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">66</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/united-arab-emirates/">UAE</a></td>
    <td style="font-weight: bold; text-align:right">894,523</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,302 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">875,602</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">16,619</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">88,542</td>
    <td style="font-weight: bold; text-align:right">228</td>
    <td style="font-weight: bold; text-align:right">151,396,113</td>
    <td style="font-weight: bold; text-align:right">14,985,514</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/united-arab-emirates-population/">10,102,831</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>11</td><td>4,389</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,645</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">67</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/ecuador/">Ecuador</a></td>
    <td style="font-weight: bold; text-align:right">865,585</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">35,513 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">759</td>
    <td style="font-weight: bold; text-align:right">47,772</td>
    <td style="font-weight: bold; text-align:right">1,960</td>
    <td style="font-weight: bold; text-align:right">2,470,170</td>
    <td style="font-weight: bold; text-align:right">136,328</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/ecuador-population/">18,119,258</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>21</td><td>510</td><td>7</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">21,314</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">68</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/costa-rica/">Costa Rica</a></td>
    <td style="font-weight: bold; text-align:right">844,892</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">8,357 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">825,599</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">10,936</td>
    <td style="font-weight: bold; text-align:right">44</td>
    <td style="font-weight: bold; text-align:right">163,207</td>
    <td style="font-weight: bold; text-align:right">1,614</td>
    <td style="font-weight: bold; text-align:right">4,163,300</td>
    <td style="font-weight: bold; text-align:right">804,220</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/costa-rica-population/">5,176,817</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>6</td><td>619</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,112</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">69</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/guatemala/">Guatemala</a></td>
    <td style="font-weight: bold; text-align:right">837,087</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">17,411 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">815,470</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">4,206</td>
    <td style="font-weight: bold; text-align:right">5</td>
    <td style="font-weight: bold; text-align:right">45,237</td>
    <td style="font-weight: bold; text-align:right">941</td>
    <td style="font-weight: bold; text-align:right">4,345,675</td>
    <td style="font-weight: bold; text-align:right">234,843</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/guatemala-population/">18,504,560</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>22</td><td>1,063</td><td>4</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">227</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">70</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/latvia/">Latvia</a></td>
    <td style="font-weight: bold; text-align:right">811,056</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">5,695 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">791,297</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">14,064</td>
    <td style="font-weight: bold; text-align:right">14</td>
    <td style="font-weight: bold; text-align:right">438,614</td>
    <td style="font-weight: bold; text-align:right">3,080</td>
    <td style="font-weight: bold; text-align:right">7,114,713</td>
    <td style="font-weight: bold; text-align:right">3,847,596</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/latvia-population/">1,849,132</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>325</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">7,606</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">71</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/new-zealand/">New Zealand</a></td>
    <td style="font-weight: bold; text-align:right">805,240</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+9,634</td>
    <td style="font-weight: bold; text-align:right;">514 </td>
    <td style="font-weight: bold; 
                                        text-align:right;background-color:red; color:white">+17</td>
    <td style="font-weight: bold; text-align:right">741,486</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+11,686</td>
    <td style="text-align:right;font-weight:bold;">63,240</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">160,980</td>
    <td style="font-weight: bold; text-align:right">103</td>
    <td style="font-weight: bold; text-align:right">6,964,290</td>
    <td style="font-weight: bold; text-align:right">1,392,273</td>
    <td style="font-weight: bold; text-align:right">5,002,100 </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>6</td><td>9,732</td><td>1</td>
    <td style="font-weight: bold; text-align:right">1,926</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">12,643</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">72</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/azerbaijan/">Azerbaijan</a></td>
    <td style="font-weight: bold; text-align:right">792,305</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">9,704 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">782,416</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">185</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">76,910</td>
    <td style="font-weight: bold; text-align:right">942</td>
    <td style="font-weight: bold; text-align:right">6,755,203</td>
    <td style="font-weight: bold; text-align:right">655,740</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/azerbaijan-population/">10,301,650</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>13</td><td>1,062</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">18</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">73</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/panama/">Panama</a></td>
    <td style="font-weight: bold; text-align:right">767,835</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">8,178 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">757,190</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,467</td>
    <td style="font-weight: bold; text-align:right">9</td>
    <td style="font-weight: bold; text-align:right">173,111</td>
    <td style="font-weight: bold; text-align:right">1,844</td>
    <td style="font-weight: bold; text-align:right">5,773,749</td>
    <td style="font-weight: bold; text-align:right">1,301,714</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/panama-population/">4,435,496</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>6</td><td>542</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">556</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">74</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saudi-arabia/">Saudi Arabia</a></td>
    <td style="font-weight: bold; text-align:right">752,188</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">9,062 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">738,011</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">5,115</td>
    <td style="font-weight: bold; text-align:right">66</td>
    <td style="font-weight: bold; text-align:right">21,024</td>
    <td style="font-weight: bold; text-align:right">253</td>
    <td style="font-weight: bold; text-align:right">41,704,690</td>
    <td style="font-weight: bold; text-align:right">1,165,666</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saudi-arabia-population/">35,777,569</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>48</td><td>3,948</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">143</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">75</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/sri-lanka/">Sri Lanka</a></td>
    <td style="font-weight: bold; text-align:right">662,748</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">16,494 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">642,530</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3,724</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">30,721</td>
    <td style="font-weight: bold; text-align:right">765</td>
    <td style="font-weight: bold; text-align:right">6,477,329</td>
    <td style="font-weight: bold; text-align:right">300,253</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/sri-lanka-population/">21,572,876</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>33</td><td>1,308</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">173</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">76</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/paraguay/">Paraguay</a></td>
    <td style="font-weight: bold; text-align:right">648,446</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">18,734 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">624,673</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">5,039</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">88,971</td>
    <td style="font-weight: bold; text-align:right">2,570</td>
    <td style="font-weight: bold; text-align:right">2,615,453</td>
    <td style="font-weight: bold; text-align:right">358,857</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/paraguay-population/">7,288,285</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>11</td><td>389</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">691</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">77</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/kuwait/">Kuwait</a></td>
    <td style="font-weight: bold; text-align:right">630,641</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,555 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">626,843</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,243</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">143,889</td>
    <td style="font-weight: bold; text-align:right">583</td>
    <td style="font-weight: bold; text-align:right">7,948,416</td>
    <td style="font-weight: bold; text-align:right">1,813,533</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/kuwait-population/">4,382,834</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>7</td><td>1,715</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">284</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">78</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/myanmar/">Myanmar</a></td>
    <td style="font-weight: bold; text-align:right">612,460</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">19,434 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">591,139</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,887</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">11,124</td>
    <td style="font-weight: bold; text-align:right">353</td>
    <td style="font-weight: bold; text-align:right">7,805,688</td>
    <td style="font-weight: bold; text-align:right">141,771</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/myanmar-population/">55,058,290</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>90</td><td>2,833</td><td>7</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">34</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">79</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/state-of-palestine/">Palestine</a></td>
    <td style="font-weight: bold; text-align:right">581,678</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">5,352 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">575,613</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">713</td>
    <td style="font-weight: bold; text-align:right">17</td>
    <td style="font-weight: bold; text-align:right">109,500</td>
    <td style="font-weight: bold; text-align:right">1,008</td>
    <td style="font-weight: bold; text-align:right">3,078,533</td>
    <td style="font-weight: bold; text-align:right">579,529</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/state-of-palestine-population/">5,312,132</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>9</td><td>993</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">134</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">80</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/dominican-republic/">Dominican Republic</a></td>
    <td style="font-weight: bold; text-align:right">578,626</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">4,375 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">574,132</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">119</td>
    <td style="font-weight: bold; text-align:right">16</td>
    <td style="font-weight: bold; text-align:right">52,406</td>
    <td style="font-weight: bold; text-align:right">396</td>
    <td style="font-weight: bold; text-align:right">3,251,191</td>
    <td style="font-weight: bold; text-align:right">294,457</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/dominican-republic-population/">11,041,303</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>19</td><td>2,524</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">11</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">81</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/estonia/">Estonia</a></td>
    <td style="font-weight: bold; text-align:right">565,839</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,501 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">498,248</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">65,090</td>
    <td style="font-weight: bold; text-align:right">6</td>
    <td style="font-weight: bold; text-align:right">426,045</td>
    <td style="font-weight: bold; text-align:right">1,883</td>
    <td style="font-weight: bold; text-align:right">3,284,566</td>
    <td style="font-weight: bold; text-align:right">2,473,092</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/estonia-population/">1,328,121</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>531</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">49,009</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">82</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bahrain/">Bahrain</a></td>
    <td style="font-weight: bold; text-align:right">561,525</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,473 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">555,813</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">4,239</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">310,815</td>
    <td style="font-weight: bold; text-align:right">815</td>
    <td style="font-weight: bold; text-align:right">9,662,134</td>
    <td style="font-weight: bold; text-align:right">5,348,183</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bahrain-population/">1,806,620</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>3</td><td>1,226</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,346</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">83</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/venezuela/">Venezuela</a></td>
    <td style="font-weight: bold; text-align:right">521,714</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">5,698 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">514,413</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,603</td>
    <td style="font-weight: bold; text-align:right">230</td>
    <td style="font-weight: bold; text-align:right">18,440</td>
    <td style="font-weight: bold; text-align:right">201</td>
    <td style="font-weight: bold; text-align:right">3,359,014</td>
    <td style="font-weight: bold; text-align:right">118,724</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/venezuela-population/">28,292,703</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>54</td><td>4,965</td><td>8</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">57</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">84</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/moldova/">Moldova</a></td>
    <td style="font-weight: bold; text-align:right">515,804</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">11,474 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">502,452</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,878</td>
    <td style="font-weight: bold; text-align:right">47</td>
    <td style="font-weight: bold; text-align:right">128,396</td>
    <td style="font-weight: bold; text-align:right">2,856</td>
    <td style="font-weight: bold; text-align:right">3,192,777</td>
    <td style="font-weight: bold; text-align:right">794,758</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/moldova-population/">4,017,295</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>8</td><td>350</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">467</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">85</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/egypt/">Egypt</a></td>
    <td style="font-weight: bold; text-align:right">511,977</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">24,522 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">442,182</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">45,273</td>
    <td style="font-weight: bold; text-align:right">122</td>
    <td style="font-weight: bold; text-align:right">4,841</td>
    <td style="font-weight: bold; text-align:right">232</td>
    <td style="font-weight: bold; text-align:right">3,693,367</td>
    <td style="font-weight: bold; text-align:right">34,921</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/egypt-population/">105,764,659</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>207</td><td>4,313</td><td>29</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">428</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">86</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/libya/">Libya</a></td>
    <td style="font-weight: bold; text-align:right">501,834</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6,429 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">490,837</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">4,568</td>
    <td style="font-weight: bold; text-align:right">101</td>
    <td style="font-weight: bold; text-align:right">71,310</td>
    <td style="font-weight: bold; text-align:right">914</td>
    <td style="font-weight: bold; text-align:right">2,475,203</td>
    <td style="font-weight: bold; text-align:right">351,722</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/libya-population/">7,037,385</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>14</td><td>1,095</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">649</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">87</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/ethiopia/">Ethiopia</a></td>
    <td style="font-weight: bold; text-align:right">470,151</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">7,509 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">453,597</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">9,045</td>
    <td style="font-weight: bold; text-align:right">17</td>
    <td style="font-weight: bold; text-align:right">3,917</td>
    <td style="font-weight: bold; text-align:right">63</td>
    <td style="font-weight: bold; text-align:right">4,718,531</td>
    <td style="font-weight: bold; text-align:right">39,313</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/ethiopia-population/">120,023,187</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>255</td><td>15,984</td><td>25</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">75</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">88</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/mongolia/">Mongolia</a></td>
    <td style="font-weight: bold; text-align:right">469,266</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+30</td>
    <td style="font-weight: bold; text-align:right;">2,177 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">313,256</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">153,833</td>
    <td style="font-weight: bold; text-align:right">192</td>
    <td style="font-weight: bold; text-align:right">139,160</td>
    <td style="font-weight: bold; text-align:right">646</td>
    <td style="font-weight: bold; text-align:right">4,030,048</td>
    <td style="font-weight: bold; text-align:right">1,195,106</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/mongolia-population/">3,372,126</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>7</td><td>1,549</td><td>1</td>
    <td style="font-weight: bold; text-align:right">9</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">45,619</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">89</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cyprus/">Cyprus</a></td>
    <td style="font-weight: bold; text-align:right">462,945</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">989 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">124,370</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">337,586</td>
    <td style="font-weight: bold; text-align:right">60</td>
    <td style="font-weight: bold; text-align:right">378,537</td>
    <td style="font-weight: bold; text-align:right">809</td>
    <td style="font-weight: bold; text-align:right">9,477,138</td>
    <td style="font-weight: bold; text-align:right">7,749,186</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cyprus-population/">1,222,985</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>3</td><td>1,237</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">276,034</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">90</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/armenia/">Armenia</a></td>
    <td style="font-weight: bold; text-align:right">422,711</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">8,621 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">410,387</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3,703</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">142,179</td>
    <td style="font-weight: bold; text-align:right">2,900</td>
    <td style="font-weight: bold; text-align:right">3,005,711</td>
    <td style="font-weight: bold; text-align:right">1,010,972</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/armenia-population/">2,973,090</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>7</td><td>345</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,246</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">91</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/honduras/">Honduras</a></td>
    <td style="font-weight: bold; text-align:right">421,268</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">10,888 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">131,100</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">279,280</td>
    <td style="font-weight: bold; text-align:right">105</td>
    <td style="font-weight: bold; text-align:right">41,363</td>
    <td style="font-weight: bold; text-align:right">1,069</td>
    <td style="font-weight: bold; text-align:right">1,263,329</td>
    <td style="font-weight: bold; text-align:right">124,043</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/honduras-population/">10,184,606</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>24</td><td>935</td><td>8</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">27,422</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">92</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/oman/">Oman</a></td>
    <td style="font-weight: bold; text-align:right">388,763</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">4,257 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">383,809</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">697</td>
    <td style="font-weight: bold; text-align:right">5</td>
    <td style="font-weight: bold; text-align:right">72,838</td>
    <td style="font-weight: bold; text-align:right">798</td>
    <td style="font-weight: bold; text-align:right">25,000,000</td>
    <td style="font-weight: bold; text-align:right">4,683,950</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/oman-population/">5,337,375</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>14</td><td>1,254</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">131</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">93</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bosnia-and-herzegovina/">Bosnia and Herzegovina</a></td>
    <td style="font-weight: bold; text-align:right">376,339</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">15,744 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">192,218</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">168,377</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">115,991</td>
    <td style="font-weight: bold; text-align:right">4,852</td>
    <td style="font-weight: bold; text-align:right">1,747,008</td>
    <td style="font-weight: bold; text-align:right">538,445</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bosnia-and-herzegovina-population/">3,244,542</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>9</td><td>206</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">51,895</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">94</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/qatar/">Qatar</a></td>
    <td style="font-weight: bold; text-align:right">363,139</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">677 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">361,291</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,171</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">129,332</td>
    <td style="font-weight: bold; text-align:right">241</td>
    <td style="font-weight: bold; text-align:right">3,419,116</td>
    <td style="font-weight: bold; text-align:right">1,217,718</td>
    <td style="font-weight: bold; text-align:right">2,807,805 </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>8</td><td>4,147</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">417</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">95</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/reunion/">Réunion</a></td>
    <td style="font-weight: bold; text-align:right">360,445</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">731 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">342,442</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">17,272</td>
    <td style="font-weight: bold; text-align:right">10</td>
    <td style="font-weight: bold; text-align:right">397,547</td>
    <td style="font-weight: bold; text-align:right">806</td>
    <td style="font-weight: bold; text-align:right">1,603,660</td>
    <td style="font-weight: bold; text-align:right">1,768,732</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/reunion-population/">906,672</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>3</td><td>1,240</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">19,050</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">96</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/kenya/">Kenya</a></td>
    <td style="font-weight: bold; text-align:right">323,588</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">5,649 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">317,801</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">138</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">5,791</td>
    <td style="font-weight: bold; text-align:right">101</td>
    <td style="font-weight: bold; text-align:right">3,557,516</td>
    <td style="font-weight: bold; text-align:right">63,668</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/kenya-population/">55,876,000</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>173</td><td>9,891</td><td>16</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">97</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/zambia/">Zambia</a></td>
    <td style="font-weight: bold; text-align:right">318,113</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">3,969 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">313,194</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">950</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">16,484</td>
    <td style="font-weight: bold; text-align:right">206</td>
    <td style="font-weight: bold; text-align:right">3,390,279</td>
    <td style="font-weight: bold; text-align:right">175,675</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/zambia-population/">19,298,604</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>61</td><td>4,862</td><td>6</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">49</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">98</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/macedonia/">North Macedonia</a></td>
    <td style="font-weight: bold; text-align:right">308,152</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">9,256 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">297,724</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,172</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">147,921</td>
    <td style="font-weight: bold; text-align:right">4,443</td>
    <td style="font-weight: bold; text-align:right">1,988,999</td>
    <td style="font-weight: bold; text-align:right">954,771</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/macedonia-population/">2,083,222</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>7</td><td>225</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">563</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">99</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/botswana/">Botswana</a></td>
    <td style="font-weight: bold; text-align:right">305,859</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,688 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">303,026</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">145</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">125,557</td>
    <td style="font-weight: bold; text-align:right">1,103</td>
    <td style="font-weight: bold; text-align:right">2,026,898</td>
    <td style="font-weight: bold; text-align:right">832,057</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/botswana-population/">2,436,008</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>8</td><td>906</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">60</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">100</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/albania/">Albania</a></td>
    <td style="font-weight: bold; text-align:right">274,320</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">3,494 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">270,474</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">352</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right">95,508</td>
    <td style="font-weight: bold; text-align:right">1,216</td>
    <td style="font-weight: bold; text-align:right">1,789,363</td>
    <td style="font-weight: bold; text-align:right">622,992</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/albania-population/">2,872,210</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>10</td><td>822</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">123</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">101</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/algeria/">Algeria</a></td>
    <td style="font-weight: bold; text-align:right">265,731</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6,874 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">178,327</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">80,530</td>
    <td style="font-weight: bold; text-align:right">6</td>
    <td style="font-weight: bold; text-align:right">5,871</td>
    <td style="font-weight: bold; text-align:right">152</td>
    <td style="font-weight: bold; text-align:right">230,861</td>
    <td style="font-weight: bold; text-align:right">5,101</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/algeria-population/">45,258,362</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>170</td><td>6,584</td><td>196</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,779</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">102</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/nigeria/">Nigeria</a></td>
    <td style="font-weight: bold; text-align:right">255,633</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">3,142 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">249,825</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,666</td>
    <td style="font-weight: bold; text-align:right">11</td>
    <td style="font-weight: bold; text-align:right">1,188</td>
    <td style="font-weight: bold; text-align:right">15</td>
    <td style="font-weight: bold; text-align:right">4,977,858</td>
    <td style="font-weight: bold; text-align:right">23,129</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/nigeria-population/">215,217,370</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>842</td><td>68,497</td><td>43</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">12</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">103</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/zimbabwe/">Zimbabwe</a></td>
    <td style="font-weight: bold; text-align:right">247,160</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">5,460 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">240,754</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">946</td>
    <td style="font-weight: bold; text-align:right">12</td>
    <td style="font-weight: bold; text-align:right">16,210</td>
    <td style="font-weight: bold; text-align:right">358</td>
    <td style="font-weight: bold; text-align:right">2,221,896</td>
    <td style="font-weight: bold; text-align:right">145,722</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/zimbabwe-population/">15,247,515</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>62</td><td>2,793</td><td>7</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">62</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">104</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/uzbekistan/">Uzbekistan</a></td>
    <td style="font-weight: bold; text-align:right">238,176</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+31</td>
    <td style="font-weight: bold; text-align:right;">1,637 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">236,127</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+70</td>
    <td style="text-align:right;font-weight:bold;">412</td>
    <td style="font-weight: bold; text-align:right">23</td>
    <td style="font-weight: bold; text-align:right">6,938</td>
    <td style="font-weight: bold; text-align:right">48</td>
    <td style="font-weight: bold; text-align:right">1,377,915</td>
    <td style="font-weight: bold; text-align:right">40,136</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/uzbekistan-population/">34,331,414</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>144</td><td>20,972</td><td>25</td>
    <td style="font-weight: bold; text-align:right">0.9</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">12</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">105</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/montenegro/">Montenegro</a></td>
    <td style="font-weight: bold; text-align:right">233,908</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,708 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">230,749</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">451</td>
    <td style="font-weight: bold; text-align:right">6</td>
    <td style="font-weight: bold; text-align:right">372,342</td>
    <td style="font-weight: bold; text-align:right">4,311</td>
    <td style="font-weight: bold; text-align:right">2,435,107</td>
    <td style="font-weight: bold; text-align:right">3,876,281</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/montenegro-population/">628,207</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>232</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">718</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">106</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/luxembourg/">Luxembourg</a></td>
    <td style="font-weight: bold; text-align:right">227,528</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,052 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">211,131</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">15,345</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">353,261</td>
    <td style="font-weight: bold; text-align:right">1,633</td>
    <td style="font-weight: bold; text-align:right">4,195,400</td>
    <td style="font-weight: bold; text-align:right">6,513,797</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/luxembourg-population/">644,079</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>612</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">23,825</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">107</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/mozambique/">Mozambique</a></td>
    <td style="font-weight: bold; text-align:right">225,304</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,200 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">223,058</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">46</td>
    <td style="font-weight: bold; text-align:right">13</td>
    <td style="font-weight: bold; text-align:right">6,867</td>
    <td style="font-weight: bold; text-align:right">67</td>
    <td style="font-weight: bold; text-align:right">1,304,157</td>
    <td style="font-weight: bold; text-align:right">39,747</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/mozambique-population/">32,811,070</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>146</td><td>14,914</td><td>25</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">108</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/kyrgyzstan/">Kyrgyzstan</a></td>
    <td style="font-weight: bold; text-align:right">200,973</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+3</td>
    <td style="font-weight: bold; text-align:right;">2,991  </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">196,304</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+1</td>
    <td style="text-align:right;font-weight:bold;">1,678</td>
    <td style="font-weight: bold; text-align:right">131</td>
    <td style="font-weight: bold; text-align:right">29,927</td>
    <td style="font-weight: bold; text-align:right">445</td>
    <td style="font-weight: bold; text-align:right">1,907,195</td>
    <td style="font-weight: bold; text-align:right">283,998</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/kyrgyzstan-population/">6,715,512</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>33</td><td>2,245</td><td>4</td>
    <td style="font-weight: bold; text-align:right">0.4</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">250</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">109</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/laos/">Laos</a></td>
    <td style="font-weight: bold; text-align:right">198,318</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">707 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7,660</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">189,951</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">26,573</td>
    <td style="font-weight: bold; text-align:right">95</td>
    <td style="font-weight: bold; text-align:right">1,230,778</td>
    <td style="font-weight: bold; text-align:right">164,912</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/laos-population/">7,463,224</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>38</td><td>10,556</td><td>6</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">25,452</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">110</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/iceland/">Iceland</a></td>
    <td style="font-weight: bold; text-align:right">183,974</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">110 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">75,685</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">108,179</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">532,980</td>
    <td style="font-weight: bold; text-align:right">319</td>
    <td style="font-weight: bold; text-align:right">1,953,616</td>
    <td style="font-weight: bold; text-align:right">5,659,702</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/iceland-population/">345,180</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>3,138</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">313,399</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">111</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/maldives/">Maldives</a></td>
    <td style="font-weight: bold; text-align:right">178,313</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">298 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">163,687</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">14,328</td>
    <td style="font-weight: bold; text-align:right">25</td>
    <td style="font-weight: bold; text-align:right">319,864</td>
    <td style="font-weight: bold; text-align:right">535</td>
    <td style="font-weight: bold; text-align:right">2,213,831</td>
    <td style="font-weight: bold; text-align:right">3,971,247</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/maldives-population/">557,465</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>3</td><td>1,871</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">25,702</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">112</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/afghanistan/">Afghanistan</a></td>
    <td style="font-weight: bold; text-align:right">178,295</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">7,676 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">161,417</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">9,202</td>
    <td style="font-weight: bold; text-align:right">1,124</td>
    <td style="font-weight: bold; text-align:right">4,404</td>
    <td style="font-weight: bold; text-align:right">190</td>
    <td style="font-weight: bold; text-align:right">932,483</td>
    <td style="font-weight: bold; text-align:right">23,032</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/afghanistan-population/">40,486,198</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>227</td><td>5,274</td><td>43</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">227</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">113</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/uganda/">Uganda</a></td>
    <td style="font-weight: bold; text-align:right">164,024</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">3,596 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">100,200</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">60,228</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,395</td>
    <td style="font-weight: bold; text-align:right">74</td>
    <td style="font-weight: bold; text-align:right">2,596,017</td>
    <td style="font-weight: bold; text-align:right">53,740</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/uganda-population/">48,306,880</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>295</td><td>13,434</td><td>19</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,247</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">114</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/el-salvador/">El Salvador</a></td>
    <td style="font-weight: bold; text-align:right">162,089</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">4,124 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">150,662</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">7,303</td>
    <td style="font-weight: bold; text-align:right">8</td>
    <td style="font-weight: bold; text-align:right">24,768</td>
    <td style="font-weight: bold; text-align:right">630</td>
    <td style="font-weight: bold; text-align:right">1,950,448</td>
    <td style="font-weight: bold; text-align:right">298,033</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/el-salvador-population/">6,544,392</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>40</td><td>1,587</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,116</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">115</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/ghana/">Ghana</a></td>
    <td style="font-weight: bold; text-align:right">161,086</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,445 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">159,607</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">34</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">4,999</td>
    <td style="font-weight: bold; text-align:right">45</td>
    <td style="font-weight: bold; text-align:right">2,429,358</td>
    <td style="font-weight: bold; text-align:right">75,386</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/ghana-population/">32,225,569</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>200</td><td>22,301</td><td>13</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">116</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/namibia/">Namibia</a></td>
    <td style="font-weight: bold; text-align:right">157,896</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">4,021 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">153,069</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">806</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">60,204</td>
    <td style="font-weight: bold; text-align:right">1,533</td>
    <td style="font-weight: bold; text-align:right">991,139</td>
    <td style="font-weight: bold; text-align:right">377,910</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/namibia-population/">2,622,687</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>17</td><td>652</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">307</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">117</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/martinique/">Martinique</a></td>
    <td style="font-weight: bold; text-align:right">147,519</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">918 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">104</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">146,497</td>
    <td style="font-weight: bold; text-align:right">8</td>
    <td style="font-weight: bold; text-align:right">393,649</td>
    <td style="font-weight: bold; text-align:right">2,450</td>
    <td style="font-weight: bold; text-align:right">828,928</td>
    <td style="font-weight: bold; text-align:right">2,211,961</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/martinique-population/">374,748</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>3</td><td>408</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">390,921</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">118</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/trinidad-and-tobago/">Trinidad and Tobago</a></td>
    <td style="font-weight: bold; text-align:right">141,155</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">3,792 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">131,219</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">6,144</td>
    <td style="font-weight: bold; text-align:right">18</td>
    <td style="font-weight: bold; text-align:right">100,285</td>
    <td style="font-weight: bold; text-align:right">2,694</td>
    <td style="font-weight: bold; text-align:right">686,393</td>
    <td style="font-weight: bold; text-align:right">487,653</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/trinidad-and-tobago-population/">1,407,545</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>10</td><td>371</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">4,365</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">119</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/guadeloupe/">Guadeloupe</a></td>
    <td style="font-weight: bold; text-align:right">140,130</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">854 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,250</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">137,026</td>
    <td style="font-weight: bold; text-align:right">19</td>
    <td style="font-weight: bold; text-align:right">350,110</td>
    <td style="font-weight: bold; text-align:right">2,134</td>
    <td style="font-weight: bold; text-align:right">938,039</td>
    <td style="font-weight: bold; text-align:right">2,343,656</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/guadeloupe-population/">400,246</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>3</td><td>469</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">342,354</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">120</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/brunei-darussalam/">Brunei </a></td>
    <td style="font-weight: bold; text-align:right">139,278</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">216 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">136,663</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,399</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">313,036</td>
    <td style="font-weight: bold; text-align:right">485</td>
    <td style="font-weight: bold; text-align:right">717,784</td>
    <td style="font-weight: bold; text-align:right">1,613,266</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/brunei-darussalam-population/">444,926</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>3</td><td>2,060</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">5,392</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">121</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cambodia/">Cambodia</a></td>
    <td style="font-weight: bold; text-align:right">136,013</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+15</td>
    <td style="font-weight: bold; text-align:right;">3,055 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">132,709</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+20</td>
    <td style="text-align:right;font-weight:bold;">249</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">7,940</td>
    <td style="font-weight: bold; text-align:right">178</td>
    <td style="font-weight: bold; text-align:right">2,941,393</td>
    <td style="font-weight: bold; text-align:right">171,707</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cambodia-population/">17,130,265</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>126</td><td>5,607</td><td>6</td>
    <td style="font-weight: bold; text-align:right">0.9</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">15</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">122</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/rwanda/">Rwanda</a></td>
    <td style="font-weight: bold; text-align:right">129,755</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,458 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">45,522</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">82,775</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">9,595</td>
    <td style="font-weight: bold; text-align:right">108</td>
    <td style="font-weight: bold; text-align:right">5,178,134</td>
    <td style="font-weight: bold; text-align:right">382,922</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/rwanda-population/">13,522,679</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>104</td><td>9,275</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">6,121</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">123</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/jamaica/">Jamaica</a></td>
    <td style="font-weight: bold; text-align:right">129,108</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,919 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">82,176</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">44,013</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">43,265</td>
    <td style="font-weight: bold; text-align:right">978</td>
    <td style="font-weight: bold; text-align:right">957,157</td>
    <td style="font-weight: bold; text-align:right">320,747</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/jamaica-population/">2,984,146</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>23</td><td>1,022</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">14,749</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">124</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cameroon/">Cameroon</a></td>
    <td style="font-weight: bold; text-align:right">119,780</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,927 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">117,791</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">62</td>
    <td style="font-weight: bold; text-align:right">13</td>
    <td style="font-weight: bold; text-align:right">4,321</td>
    <td style="font-weight: bold; text-align:right">70</td>
    <td style="font-weight: bold; text-align:right">1,751,774</td>
    <td style="font-weight: bold; text-align:right">63,196</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cameroon-population/">27,719,914</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>231</td><td>14,385</td><td>16</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">125</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/angola/">Angola</a></td>
    <td style="font-weight: bold; text-align:right">99,194</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,900 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">97,149</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">145</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,860</td>
    <td style="font-weight: bold; text-align:right">55</td>
    <td style="font-weight: bold; text-align:right">1,499,795</td>
    <td style="font-weight: bold; text-align:right">43,244</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/angola-population/">34,682,277</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>350</td><td>18,254</td><td>23</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">4</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">126</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/malta/">Malta</a></td>
    <td style="font-weight: bold; text-align:right">87,441</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">669 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">77,693</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">9,079</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">197,102</td>
    <td style="font-weight: bold; text-align:right">1,508</td>
    <td style="font-weight: bold; text-align:right">1,847,584</td>
    <td style="font-weight: bold; text-align:right">4,164,658</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/malta-population/">443,634</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>5</td><td>663</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">20,465</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">127</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/democratic-republic-of-the-congo/">DRC</a></td>
    <td style="font-weight: bold; text-align:right">86,748</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,337 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">50,930</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">34,481</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">919</td>
    <td style="font-weight: bold; text-align:right">14</td>
    <td style="font-weight: bold; text-align:right">846,704</td>
    <td style="font-weight: bold; text-align:right">8,970</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/democratic-republic-of-the-congo-population/">94,398,074</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>1,088</td><td>70,604</td><td>111</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">365</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">128</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/senegal/">Senegal</a></td>
    <td style="font-weight: bold; text-align:right">85,954</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,965 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">83,970</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">19</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">4,904</td>
    <td style="font-weight: bold; text-align:right">112</td>
    <td style="font-weight: bold; text-align:right">1,057,173</td>
    <td style="font-weight: bold; text-align:right">60,314</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/senegal-population/">17,527,848</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>204</td><td>8,920</td><td>17</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">129</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/malawi/">Malawi</a></td>
    <td style="font-weight: bold; text-align:right">85,713</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,628 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">81,889</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,196</td>
    <td style="font-weight: bold; text-align:right">67</td>
    <td style="font-weight: bold; text-align:right">4,284</td>
    <td style="font-weight: bold; text-align:right">131</td>
    <td style="font-weight: bold; text-align:right">567,431</td>
    <td style="font-weight: bold; text-align:right">28,360</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/malawi-population/">20,008,204</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>233</td><td>7,613</td><td>35</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">60</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">130</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cote-d-ivoire/">Ivory Coast</a></td>
    <td style="font-weight: bold; text-align:right">81,838</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">797 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">81,004</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">37</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,972</td>
    <td style="font-weight: bold; text-align:right">29</td>
    <td style="font-weight: bold; text-align:right">1,485,035</td>
    <td style="font-weight: bold; text-align:right">53,925</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cote-d-ivoire-population/">27,538,854</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>337</td><td>34,553</td><td>19</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">131</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/french-guiana/">French Guiana</a></td>
    <td style="font-weight: bold; text-align:right">79,529</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">394 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">11,254</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">67,881</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">254,545</td>
    <td style="font-weight: bold; text-align:right">1,261</td>
    <td style="font-weight: bold; text-align:right">613,484</td>
    <td style="font-weight: bold; text-align:right">1,963,551</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/french-guiana-population/">312,436</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>4</td><td>793</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">217,264</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">132</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/suriname/">Suriname</a></td>
    <td style="font-weight: bold; text-align:right">79,276</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,325 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">49,395</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">28,556</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">133,019</td>
    <td style="font-weight: bold; text-align:right">2,223</td>
    <td style="font-weight: bold; text-align:right">235,707</td>
    <td style="font-weight: bold; text-align:right">395,497</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/suriname-population/">595,977</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>8</td><td>450</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">47,915</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">133</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/french-polynesia/">French Polynesia</a></td>
    <td style="font-weight: bold; text-align:right">72,596</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">648 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right">255,804</td>
    <td style="font-weight: bold; text-align:right">2,283</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/french-polynesia-population/">283,795</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>4</td><td>438</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">135,478</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">134</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/channel-islands/">Channel Islands</a></td>
    <td style="font-weight: bold; text-align:right">72,213</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">164 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">70,116</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,933</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">408,648</td>
    <td style="font-weight: bold; text-align:right">928</td>
    <td style="font-weight: bold; text-align:right">1,252,269</td>
    <td style="font-weight: bold; text-align:right">7,086,497</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/channel-islands-population/">176,712</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>1,078</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">10,939</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">135</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/swaziland/">Eswatini</a></td>
    <td style="font-weight: bold; text-align:right">70,048</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,395 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">68,567</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">86</td>
    <td style="font-weight: bold; text-align:right">11</td>
    <td style="font-weight: bold; text-align:right">59,286</td>
    <td style="font-weight: bold; text-align:right">1,181</td>
    <td style="font-weight: bold; text-align:right">1,008,368</td>
    <td style="font-weight: bold; text-align:right">853,451</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/swaziland-population/">1,181,519</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>17</td><td>847</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">73</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">136</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/fiji/">Fiji</a></td>
    <td style="font-weight: bold; text-align:right">64,502</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">862 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">62,662</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">978</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">71,038</td>
    <td style="font-weight: bold; text-align:right">949</td>
    <td style="font-weight: bold; text-align:right">506,083</td>
    <td style="font-weight: bold; text-align:right">557,364</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/fiji-population/">907,994</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>14</td><td>1,053</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,077</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">137</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/madagascar/">Madagascar</a></td>
    <td style="font-weight: bold; text-align:right">64,089</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,390 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">59,355</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3,344</td>
    <td style="font-weight: bold; text-align:right">14</td>
    <td style="font-weight: bold; text-align:right">2,213</td>
    <td style="font-weight: bold; text-align:right">48</td>
    <td style="font-weight: bold; text-align:right">415,532</td>
    <td style="font-weight: bold; text-align:right">14,351</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/madagascar-population/">28,955,799</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>452</td><td>20,832</td><td>70</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">115</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">138</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/guyana/">Guyana</a></td>
    <td style="font-weight: bold; text-align:right">63,349</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,227 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">62,024</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">98</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">79,855</td>
    <td style="font-weight: bold; text-align:right">1,547</td>
    <td style="font-weight: bold; text-align:right">580,888</td>
    <td style="font-weight: bold; text-align:right">732,243</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/guyana-population/">793,300</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>13</td><td>647</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">124</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">139</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/barbados/">Barbados</a></td>
    <td style="font-weight: bold; text-align:right">62,968</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">379 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">59,521</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3,068</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">218,638</td>
    <td style="font-weight: bold; text-align:right">1,316</td>
    <td style="font-weight: bold; text-align:right">626,701</td>
    <td style="font-weight: bold; text-align:right">2,176,038</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/barbados-population/">288,001</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>5</td><td>760</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">10,653</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">140</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/sudan/">Sudan</a></td>
    <td style="font-weight: bold; text-align:right">62,057</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">4,929 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,359</td>
    <td style="font-weight: bold; text-align:right">108</td>
    <td style="font-weight: bold; text-align:right">562,941</td>
    <td style="font-weight: bold; text-align:right">12,327</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/sudan-population/">45,668,432</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>736</td><td>9,265</td><td>81</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">368</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">141</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/new-caledonia/">New Caledonia</a></td>
    <td style="font-weight: bold; text-align:right">60,385</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">312 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">60,011</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">62</td>
    <td style="font-weight: bold; text-align:right">9</td>
    <td style="font-weight: bold; text-align:right">207,954</td>
    <td style="font-weight: bold; text-align:right">1,074</td>
    <td style="font-weight: bold; text-align:right">98,964</td>
    <td style="font-weight: bold; text-align:right">340,812</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/new-caledonia-population/">290,377</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>5</td><td>931</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">214</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">142</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/mauritania/">Mauritania</a></td>
    <td style="font-weight: bold; text-align:right">58,680</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">982 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">57,686</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">12</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">12,057</td>
    <td style="font-weight: bold; text-align:right">202</td>
    <td style="font-weight: bold; text-align:right">791,559</td>
    <td style="font-weight: bold; text-align:right">162,645</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/mauritania-population/">4,866,793</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>83</td><td>4,956</td><td>6</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">143</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/belize/">Belize</a></td>
    <td style="font-weight: bold; text-align:right">57,331</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">672 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">56,473</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">186</td>
    <td style="font-weight: bold; text-align:right">6</td>
    <td style="font-weight: bold; text-align:right">139,676</td>
    <td style="font-weight: bold; text-align:right">1,637</td>
    <td style="font-weight: bold; text-align:right">529,581</td>
    <td style="font-weight: bold; text-align:right">1,290,223</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/belize-population/">410,457</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>7</td><td>611</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">453</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">144</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cabo-verde/">Cabo Verde</a></td>
    <td style="font-weight: bold; text-align:right">55,978</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">401 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">55,514</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">63</td>
    <td style="font-weight: bold; text-align:right">23</td>
    <td style="font-weight: bold; text-align:right">98,775</td>
    <td style="font-weight: bold; text-align:right">708</td>
    <td style="font-weight: bold; text-align:right">400,982</td>
    <td style="font-weight: bold; text-align:right">707,546</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cabo-verde-population/">566,722</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>10</td><td>1,413</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">111</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">145</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/syria/">Syria</a></td>
    <td style="font-weight: bold; text-align:right">55,756</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">3,148 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">51,893</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">715</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,054</td>
    <td style="font-weight: bold; text-align:right">172</td>
    <td style="font-weight: bold; text-align:right">146,269</td>
    <td style="font-weight: bold; text-align:right">8,012</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/syria-population/">18,256,030</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>327</td><td>5,799</td><td>125</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">39</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">146</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/gabon/">Gabon</a></td>
    <td style="font-weight: bold; text-align:right">47,588</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">303 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">47,270</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">15</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">20,520</td>
    <td style="font-weight: bold; text-align:right">131</td>
    <td style="font-weight: bold; text-align:right">1,589,113</td>
    <td style="font-weight: bold; text-align:right">685,243</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/gabon-population/">2,319,051</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>49</td><td>7,654</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">6</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">147</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bhutan/">Bhutan</a></td>
    <td style="font-weight: bold; text-align:right">47,187</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">14  </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">37,034</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">10,139</td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right">59,980</td>
    <td style="font-weight: bold; text-align:right">18</td>
    <td style="font-weight: bold; text-align:right">2,203,246</td>
    <td style="font-weight: bold; text-align:right">2,800,575</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bhutan-population/">786,712</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>17</td><td>56,194</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">12,888</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">148</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/papua-new-guinea/">Papua New Guinea</a></td>
    <td style="font-weight: bold; text-align:right">43,615</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">649 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">42,906</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">60</td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right">4,716</td>
    <td style="font-weight: bold; text-align:right">70</td>
    <td style="font-weight: bold; text-align:right">249,149</td>
    <td style="font-weight: bold; text-align:right">26,940</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/papua-new-guinea-population/">9,248,228</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>212</td><td>14,250</td><td>37</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">6</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">149</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/curacao/">Curaçao</a></td>
    <td style="font-weight: bold; text-align:right">41,153</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">270 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">40,306</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">577</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">248,981</td>
    <td style="font-weight: bold; text-align:right">1,634</td>
    <td style="font-weight: bold; text-align:right">494,095</td>
    <td style="font-weight: bold; text-align:right">2,989,334</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/curacao-population/">165,286</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>4</td><td>612</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,491</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">150</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/seychelles/">Seychelles</a></td>
    <td style="font-weight: bold; text-align:right">40,866</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">164 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">39,963</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">739</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">411,007</td>
    <td style="font-weight: bold; text-align:right">1,649</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/seychelles-population/">99,429</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>2</td><td>606</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">7,432</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">151</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/andorra/">Andorra</a></td>
    <td style="font-weight: bold; text-align:right">40,709</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">153 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">39,999</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">557</td>
    <td style="font-weight: bold; text-align:right">14</td>
    <td style="font-weight: bold; text-align:right">525,379</td>
    <td style="font-weight: bold; text-align:right">1,975</td>
    <td style="font-weight: bold; text-align:right">249,838</td>
    <td style="font-weight: bold; text-align:right">3,224,340</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/andorra-population/">77,485</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>506</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">7,188</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">152</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/burundi/">Burundi</a></td>
    <td style="font-weight: bold; text-align:right">38,698</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">38 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">773</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">37,887</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,091</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">345,742</td>
    <td style="font-weight: bold; text-align:right">27,615</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/burundi-population/">12,519,873</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>324</td><td>329,470</td><td>36</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,026</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">153</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/mauritius/">Mauritius</a></td>
    <td style="font-weight: bold; text-align:right">37,210</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">985 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">35,090</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,135</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">29,172</td>
    <td style="font-weight: bold; text-align:right">772</td>
    <td style="font-weight: bold; text-align:right">358,675</td>
    <td style="font-weight: bold; text-align:right">281,199</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/mauritius-population/">1,275,520</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>34</td><td>1,295</td><td>4</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">890</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">154</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/mayotte/">Mayotte</a></td>
    <td style="font-weight: bold; text-align:right">36,958</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">187 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,964</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">33,807</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">129,900</td>
    <td style="font-weight: bold; text-align:right">657</td>
    <td style="font-weight: bold; text-align:right">176,919</td>
    <td style="font-weight: bold; text-align:right">621,835</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/mayotte-population/">284,511</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>8</td><td>1,521</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">118,825</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">155</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/togo/">Togo</a></td>
    <td style="font-weight: bold; text-align:right">36,957</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">272 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">36,659</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">26</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">4,286</td>
    <td style="font-weight: bold; text-align:right">32</td>
    <td style="font-weight: bold; text-align:right">723,005</td>
    <td style="font-weight: bold; text-align:right">83,841</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/togo-population/">8,623,488</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>233</td><td>31,704</td><td>12</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">156</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/guinea/">Guinea</a></td>
    <td style="font-weight: bold; text-align:right">36,459</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">440 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">35,976</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">43</td>
    <td style="font-weight: bold; text-align:right">8</td>
    <td style="font-weight: bold; text-align:right">2,649</td>
    <td style="font-weight: bold; text-align:right">32</td>
    <td style="font-weight: bold; text-align:right">660,107</td>
    <td style="font-weight: bold; text-align:right">47,953</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/guinea-population/">13,765,649</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>378</td><td>31,286</td><td>21</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">157</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/faeroe-islands/">Faeroe Islands</a></td>
    <td style="font-weight: bold; text-align:right">34,658</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">28 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7,693</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">26,937</td>
    <td style="font-weight: bold; text-align:right">5</td>
    <td style="font-weight: bold; text-align:right">704,531</td>
    <td style="font-weight: bold; text-align:right">569</td>
    <td style="font-weight: bold; text-align:right">778,000</td>
    <td style="font-weight: bold; text-align:right">15,815,258</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/faeroe-islands-population/">49,193</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>1</td><td>1,757</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">547,578</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">158</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/aruba/">Aruba</a></td>
    <td style="font-weight: bold; text-align:right">34,189</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">212 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">33,893</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">84</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right">317,824</td>
    <td style="font-weight: bold; text-align:right">1,971</td>
    <td style="font-weight: bold; text-align:right">177,885</td>
    <td style="font-weight: bold; text-align:right">1,653,637</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/aruba-population/">107,572</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>3</td><td>507</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">781</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">159</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/tanzania/">Tanzania</a></td>
    <td style="font-weight: bold; text-align:right">33,851</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">803 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right">539</td>
    <td style="font-weight: bold; text-align:right">13</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/tanzania-population/">62,756,770</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>1,854</td><td>78,153</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">524</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">160</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bahamas/">Bahamas</a></td>
    <td style="font-weight: bold; text-align:right">33,368</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">789 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">32,253</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">326</td>
    <td style="font-weight: bold; text-align:right">11</td>
    <td style="font-weight: bold; text-align:right">83,436</td>
    <td style="font-weight: bold; text-align:right">1,973</td>
    <td style="font-weight: bold; text-align:right">229,025</td>
    <td style="font-weight: bold; text-align:right">572,671</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bahamas-population/">399,924</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>12</td><td>507</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">815</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">161</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/lesotho/">Lesotho</a></td>
    <td style="font-weight: bold; text-align:right">32,910</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">697 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">24,155</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">8,058</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">15,149</td>
    <td style="font-weight: bold; text-align:right">321</td>
    <td style="font-weight: bold; text-align:right">431,221</td>
    <td style="font-weight: bold; text-align:right">198,496</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/lesotho-population/">2,172,441</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>66</td><td>3,117</td><td>5</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,709</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">162</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/mali/">Mali</a></td>
    <td style="font-weight: bold; text-align:right">30,602</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">729 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">29,689</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">184</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,438</td>
    <td style="font-weight: bold; text-align:right">34</td>
    <td style="font-weight: bold; text-align:right">657,234</td>
    <td style="font-weight: bold; text-align:right">30,875</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/mali-population/">21,287,008</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>696</td><td>29,200</td><td>32</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">9</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">163</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/haiti/">Haiti</a></td>
    <td style="font-weight: bold; text-align:right">30,586</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">835 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">29,100</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">651</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,625</td>
    <td style="font-weight: bold; text-align:right">72</td>
    <td style="font-weight: bold; text-align:right">132,422</td>
    <td style="font-weight: bold; text-align:right">11,367</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/haiti-population/">11,649,630</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>381</td><td>13,952</td><td>88</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">56</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">164</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/taiwan/">Taiwan</a></td>
    <td style="font-weight: bold; text-align:right">29,593</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">854 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">21,473</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">7,266</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,239</td>
    <td style="font-weight: bold; text-align:right">36</td>
    <td style="font-weight: bold; text-align:right">13,482,923</td>
    <td style="font-weight: bold; text-align:right">564,294</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/taiwan-population/">23,893,416</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>807</td><td>27,978</td><td>2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">304</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">165</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/isle-of-man/">Isle of Man</a></td>
    <td style="font-weight: bold; text-align:right">28,416</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">87 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">26,794</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,535</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">331,061</td>
    <td style="font-weight: bold; text-align:right">1,014</td>
    <td style="font-weight: bold; text-align:right">150,753</td>
    <td style="font-weight: bold; text-align:right">1,756,352</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/isle-of-man-population/">85,833</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>3</td><td>987</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">17,884</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">166</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/benin/">Benin</a></td>
    <td style="font-weight: bold; text-align:right">26,952</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">163 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">25,506</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,283</td>
    <td style="font-weight: bold; text-align:right">5</td>
    <td style="font-weight: bold; text-align:right">2,124</td>
    <td style="font-weight: bold; text-align:right">13</td>
    <td style="font-weight: bold; text-align:right">604,310</td>
    <td style="font-weight: bold; text-align:right">47,631</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/benin-population/">12,687,354</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>471</td><td>77,837</td><td>21</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">101</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">167</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/somalia/">Somalia</a></td>
    <td style="font-weight: bold; text-align:right">26,471</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1,350 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">13,182</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">11,939</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,587</td>
    <td style="font-weight: bold; text-align:right">81</td>
    <td style="font-weight: bold; text-align:right">400,466</td>
    <td style="font-weight: bold; text-align:right">24,007</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/somalia-population/">16,680,943</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>630</td><td>12,356</td><td>42</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">716</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">168</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/congo/">Congo</a></td>
    <td style="font-weight: bold; text-align:right">24,079</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">385 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">20,178</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3,516</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">4,181</td>
    <td style="font-weight: bold; text-align:right">67</td>
    <td style="font-weight: bold; text-align:right">347,815</td>
    <td style="font-weight: bold; text-align:right">60,391</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/congo-population/">5,759,411</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>239</td><td>14,960</td><td>17</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">610</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">169</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saint-lucia/">Saint Lucia</a></td>
    <td style="font-weight: bold; text-align:right">23,045</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">365 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">22,616</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">64</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">124,487</td>
    <td style="font-weight: bold; text-align:right">1,972</td>
    <td style="font-weight: bold; text-align:right">141,332</td>
    <td style="font-weight: bold; text-align:right">763,466</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saint-lucia-population/">185,119</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>8</td><td>507</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">346</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">170</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/timor-leste/">Timor-Leste</a></td>
    <td style="font-weight: bold; text-align:right">22,848</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">130 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">22,703</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">15</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">16,762</td>
    <td style="font-weight: bold; text-align:right">95</td>
    <td style="font-weight: bold; text-align:right">259,788</td>
    <td style="font-weight: bold; text-align:right">190,590</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/timor-leste-population/">1,363,073</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>60</td><td>10,485</td><td>5</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">11</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">171</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cayman-islands/">Cayman Islands</a></td>
    <td style="font-weight: bold; text-align:right">21,121</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">25 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">8,553</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">12,543</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">314,797</td>
    <td style="font-weight: bold; text-align:right">373</td>
    <td style="font-weight: bold; text-align:right">222,773</td>
    <td style="font-weight: bold; text-align:right">3,320,312</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cayman-islands-population/">67,094</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>3</td><td>2,684</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">186,947</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">172</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/burkina-faso/">Burkina Faso</a></td>
    <td style="font-weight: bold; text-align:right">20,853</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">382 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">20,439</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">32</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">951</td>
    <td style="font-weight: bold; text-align:right">17</td>
    <td style="font-weight: bold; text-align:right">248,995</td>
    <td style="font-weight: bold; text-align:right">11,358</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/burkina-faso-population/">21,921,567</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>1,051</td><td>57,386</td><td>88</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">173</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/nicaragua/">Nicaragua</a></td>
    <td style="font-weight: bold; text-align:right">18,491</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">225 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">4,225</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">14,041</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,733</td>
    <td style="font-weight: bold; text-align:right">33</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/nicaragua-population/">6,764,664</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>366</td><td>30,065</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,076</td>
    </tr>
    <tr style="background-color:#F0F0F0">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">174</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/tajikistan/">Tajikistan</a></td>
    <td style="font-weight: bold; text-align:right">17,388</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">124 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">17,264</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,753</td>
    <td style="font-weight: bold; text-align:right">13</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/tajikistan-population/">9,918,305</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>570</td><td>79,986</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">175</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/south-sudan/">South Sudan</a></td>
    <td style="font-weight: bold; text-align:right">17,362</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">138 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">13,514</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3,710</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">1,519</td>
    <td style="font-weight: bold; text-align:right">12</td>
    <td style="font-weight: bold; text-align:right">369,176</td>
    <td style="font-weight: bold; text-align:right">32,307</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/south-sudan-population/">11,427,024</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>658</td><td>82,805</td><td>31</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">325</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">176</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/gibraltar/">Gibraltar</a></td>
    <td style="font-weight: bold; text-align:right">17,236</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">101 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">16,579</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">556</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">511,864</td>
    <td style="font-weight: bold; text-align:right">2,999</td>
    <td style="font-weight: bold; text-align:right">534,283</td>
    <td style="font-weight: bold; text-align:right">15,866,807</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/gibraltar-population/">33,673</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>333</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">16,512</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">177</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/liechtenstein/">Liechtenstein</a></td>
    <td style="font-weight: bold; text-align:right">16,865</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">84 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">16,432</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">349</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">440,075</td>
    <td style="font-weight: bold; text-align:right">2,192</td>
    <td style="font-weight: bold; text-align:right">102,174</td>
    <td style="font-weight: bold; text-align:right">2,666,127</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/liechtenstein-population/">38,323</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>456</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">9,107</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">178</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/equatorial-guinea/">Equatorial Guinea</a></td>
    <td style="font-weight: bold; text-align:right">15,906</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">183 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">15,697</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">26</td>
    <td style="font-weight: bold; text-align:right">5</td>
    <td style="font-weight: bold; text-align:right">10,712</td>
    <td style="font-weight: bold; text-align:right">123</td>
    <td style="font-weight: bold; text-align:right">307,847</td>
    <td style="font-weight: bold; text-align:right">207,325</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/equatorial-guinea-population/">1,484,854</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>93</td><td>8,114</td><td>5</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">18</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">179</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/san-marino/">San Marino</a></td>
    <td style="font-weight: bold; text-align:right">15,683</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">114 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">15,225</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">344</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">460,479</td>
    <td style="font-weight: bold; text-align:right">3,347</td>
    <td style="font-weight: bold; text-align:right">147,532</td>
    <td style="font-weight: bold; text-align:right">4,331,787</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/san-marino-population/">34,058</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>2</td><td>299</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">10,100</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">180</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/djibouti/">Djibouti</a></td>
    <td style="font-weight: bold; text-align:right">15,598</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">189 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">15,404</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">5</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">15,390</td>
    <td style="font-weight: bold; text-align:right">186</td>
    <td style="font-weight: bold; text-align:right">301,567</td>
    <td style="font-weight: bold; text-align:right">297,539</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/djibouti-population/">1,013,539</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>65</td><td>5,363</td><td>3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">5</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">181</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/central-african-republic/">CAR</a></td>
    <td style="font-weight: bold; text-align:right">14,649</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">113 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">6,859</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">7,677</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right">2,942</td>
    <td style="font-weight: bold; text-align:right">23</td>
    <td style="font-weight: bold; text-align:right">81,294</td>
    <td style="font-weight: bold; text-align:right">16,327</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/central-african-republic-population/">4,979,016</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>340</td><td>44,062</td><td>61</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,542</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">182</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/grenada/">Grenada</a></td>
    <td style="font-weight: bold; text-align:right">14,092</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">219 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">13,807</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">66</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">124,213</td>
    <td style="font-weight: bold; text-align:right">1,930</td>
    <td style="font-weight: bold; text-align:right">145,920</td>
    <td style="font-weight: bold; text-align:right">1,286,205</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/grenada-population/">113,450</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>8</td><td>518</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">582</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">183</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/bermuda/">Bermuda</a></td>
    <td style="font-weight: bold; text-align:right">12,711</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">129 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">12,362</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">220</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">205,450</td>
    <td style="font-weight: bold; text-align:right">2,085</td>
    <td style="font-weight: bold; text-align:right">848,492</td>
    <td style="font-weight: bold; text-align:right">13,714,332</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/bermuda-population/">61,869</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>5</td><td>480</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,556</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">184</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/solomon-islands/">Solomon Islands</a></td>
    <td style="font-weight: bold; text-align:right">12,285</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">139 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">11,057</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,089</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right">17,138</td>
    <td style="font-weight: bold; text-align:right">194</td>
    <td style="font-weight: bold; text-align:right">5,117</td>
    <td style="font-weight: bold; text-align:right">7,139</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/solomon-islands-population/">716,813</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>58</td><td>5,157</td><td>140</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,519</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">185</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/gambia/">Gambia</a></td>
    <td style="font-weight: bold; text-align:right">11,990</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">365 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">11,591</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">34</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">4,726</td>
    <td style="font-weight: bold; text-align:right">144</td>
    <td style="font-weight: bold; text-align:right">155,686</td>
    <td style="font-weight: bold; text-align:right">61,359</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/gambia-population/">2,537,281</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>212</td><td>6,951</td><td>16</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">13</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">186</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/dominica/">Dominica</a></td>
    <td style="font-weight: bold; text-align:right">11,986</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">63 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">11,897</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">26</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">165,772</td>
    <td style="font-weight: bold; text-align:right">871</td>
    <td style="font-weight: bold; text-align:right">187,245</td>
    <td style="font-weight: bold; text-align:right">2,589,691</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/dominica-population/">72,304</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>6</td><td>1,148</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">360</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">187</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/greenland/">Greenland</a></td>
    <td style="font-weight: bold; text-align:right">11,971</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">21 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,761</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">9,189</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">210,220</td>
    <td style="font-weight: bold; text-align:right">369</td>
    <td style="font-weight: bold; text-align:right">164,926</td>
    <td style="font-weight: bold; text-align:right">2,896,233</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/greenland-population/">56,945</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>5</td><td>2,712</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">161,366</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">188</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/yemen/">Yemen</a></td>
    <td style="font-weight: bold; text-align:right">11,815</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2,147 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">9,000</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">668</td>
    <td style="font-weight: bold; text-align:right">23</td>
    <td style="font-weight: bold; text-align:right">381</td>
    <td style="font-weight: bold; text-align:right">69</td>
    <td style="font-weight: bold; text-align:right">265,253</td>
    <td style="font-weight: bold; text-align:right">8,558</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/yemen-population/">30,993,247</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>2,623</td><td>14,436</td><td>117</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">22</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">189</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/monaco/">Monaco</a></td>
    <td style="font-weight: bold; text-align:right">11,299</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">54 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">11,018</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">227</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">284,345</td>
    <td style="font-weight: bold; text-align:right">1,359</td>
    <td style="font-weight: bold; text-align:right">54,960</td>
    <td style="font-weight: bold; text-align:right">1,383,094</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/monaco-population/">39,737</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>4</td><td>736</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">5,713</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">190</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saint-martin/">Saint Martin</a></td>
    <td style="font-weight: bold; text-align:right">10,176</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">63 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,399</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">8,714</td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right">255,435</td>
    <td style="font-weight: bold; text-align:right">1,581</td>
    <td style="font-weight: bold; text-align:right">112,382</td>
    <td style="font-weight: bold; text-align:right">2,820,975</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saint-martin-population/">39,838</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>4</td><td>632</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">218,736</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">191</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/sint-maarten/">Sint Maarten</a></td>
    <td style="font-weight: bold; text-align:right">9,909</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">86 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">9,740</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">83</td>
    <td style="font-weight: bold; text-align:right">10</td>
    <td style="font-weight: bold; text-align:right">226,538</td>
    <td style="font-weight: bold; text-align:right">1,966</td>
    <td style="font-weight: bold; text-align:right">62,056</td>
    <td style="font-weight: bold; text-align:right">1,418,715</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/sint-maarten-population/">43,741</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>4</td><td>509</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,898</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">192</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/eritrea/">Eritrea</a></td>
    <td style="font-weight: bold; text-align:right">9,733</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">103 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">9,626</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">4</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2,679</td>
    <td style="font-weight: bold; text-align:right">28</td>
    <td style="font-weight: bold; text-align:right">23,693</td>
    <td style="font-weight: bold; text-align:right">6,520</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/eritrea-population/">3,633,670</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>373</td><td>35,278</td><td>153</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">193</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/caribbean-netherlands/">Caribbean Netherlands</a></td>
    <td style="font-weight: bold; text-align:right">9,346</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">34 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">8,987</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">325</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">350,615</td>
    <td style="font-weight: bold; text-align:right">1,276</td>
    <td style="font-weight: bold; text-align:right">30,126</td>
    <td style="font-weight: bold; text-align:right">1,130,177</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/caribbean-netherlands-population/">26,656</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>3</td><td>784</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">12,192</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">194</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/niger/">Niger</a></td>
    <td style="font-weight: bold; text-align:right">8,846</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">308 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">8,488</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">50</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">343</td>
    <td style="font-weight: bold; text-align:right">12</td>
    <td style="font-weight: bold; text-align:right">244,837</td>
    <td style="font-weight: bold; text-align:right">9,504</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/niger-population/">25,762,801</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>2,912</td><td>83,645</td><td>105</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">195</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/tonga/">Tonga</a></td>
    <td style="font-weight: bold; text-align:right">8,761</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">11 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">6,900</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,850</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">81,252</td>
    <td style="font-weight: bold; text-align:right">102</td>
    <td style="font-weight: bold; text-align:right">319,471</td>
    <td style="font-weight: bold; text-align:right">2,962,866</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/tonga-population/">107,825</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>12</td><td>9,802</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">17,157</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">196</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/guinea-bissau/">Guinea-Bissau</a></td>
    <td style="font-weight: bold; text-align:right">8,175</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">170 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7,280</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">725</td>
    <td style="font-weight: bold; text-align:right">6</td>
    <td style="font-weight: bold; text-align:right">3,987</td>
    <td style="font-weight: bold; text-align:right">83</td>
    <td style="font-weight: bold; text-align:right">131,390</td>
    <td style="font-weight: bold; text-align:right">64,072</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/guinea-bissau-population/">2,050,648</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>251</td><td>12,063</td><td>16</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">354</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">197</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/comoros/">Comoros</a></td>
    <td style="font-weight: bold; text-align:right">8,100</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">160 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7,933</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">7</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">8,975</td>
    <td style="font-weight: bold; text-align:right">177</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/comoros-population/">902,519</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>111</td><td>5,641</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">8</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">198</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/sierra-leone/">Sierra Leone</a></td>
    <td style="font-weight: bold; text-align:right">7,677</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">125 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">929</td>
    <td style="font-weight: bold; text-align:right">15</td>
    <td style="font-weight: bold; text-align:right">259,958</td>
    <td style="font-weight: bold; text-align:right">31,452</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/sierra-leone-population/">8,265,262</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>1,077</td><td>66,122</td><td>32</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">331</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">199</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/antigua-and-barbuda/">Antigua and Barbuda</a></td>
    <td style="font-weight: bold; text-align:right">7,523</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">135 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7,367</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">21</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">75,706</td>
    <td style="font-weight: bold; text-align:right">1,359</td>
    <td style="font-weight: bold; text-align:right">18,901</td>
    <td style="font-weight: bold; text-align:right">190,206</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/antigua-and-barbuda-population/">99,371</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>13</td><td>736</td><td>5</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">211</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">200</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/liberia/">Liberia</a></td>
    <td style="font-weight: bold; text-align:right">7,402</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">294 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">5,747</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,361</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right">1,405</td>
    <td style="font-weight: bold; text-align:right">56</td>
    <td style="font-weight: bold; text-align:right">139,824</td>
    <td style="font-weight: bold; text-align:right">26,538</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/liberia-population/">5,268,903</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>712</td><td>17,921</td><td>38</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">258</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">201</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/chad/">Chad</a></td>
    <td style="font-weight: bold; text-align:right">7,378</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">192 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">4,874</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,312</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">427</td>
    <td style="font-weight: bold; text-align:right">11</td>
    <td style="font-weight: bold; text-align:right">191,341</td>
    <td style="font-weight: bold; text-align:right">11,084</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/chad-population/">17,263,176</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>2,340</td><td>89,912</td><td>90</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">134</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">202</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saint-vincent-and-the-grenadines/">St. Vincent Grenadines</a></td>
    <td style="font-weight: bold; text-align:right">6,748</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">106 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">6,640</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">60,484</td>
    <td style="font-weight: bold; text-align:right">950</td>
    <td style="font-weight: bold; text-align:right">98,708</td>
    <td style="font-weight: bold; text-align:right">884,750</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saint-vincent-and-the-grenadines-population/">111,566</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>17</td><td>1,053</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">18</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">203</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/british-virgin-islands/">British Virgin Islands</a></td>
    <td style="font-weight: bold; text-align:right">6,162</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">62 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">201,445</td>
    <td style="font-weight: bold; text-align:right">2,027</td>
    <td style="font-weight: bold; text-align:right">102,294</td>
    <td style="font-weight: bold; text-align:right">3,344,143</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/british-virgin-islands-population/">30,589</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>5</td><td>493</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">621</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">204</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/sao-tome-and-principe/">Sao Tome and Principe</a></td>
    <td style="font-weight: bold; text-align:right">5,948</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">73 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">5,872</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">26,273</td>
    <td style="font-weight: bold; text-align:right">322</td>
    <td style="font-weight: bold; text-align:right">29,036</td>
    <td style="font-weight: bold; text-align:right">128,255</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/sao-tome-and-principe-population/">226,392</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>38</td><td>3,101</td><td>8</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">13</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">205</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/turks-and-caicos-islands/">Turks and Caicos</a></td>
    <td style="font-weight: bold; text-align:right">5,936</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">36 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">5,862</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">38</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">149,718</td>
    <td style="font-weight: bold; text-align:right">908</td>
    <td style="font-weight: bold; text-align:right">447,713</td>
    <td style="font-weight: bold; text-align:right">11,292,196</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/turks-and-caicos-islands-population/">39,648</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>7</td><td>1,101</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">958</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">206</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saint-kitts-and-nevis/">Saint Kitts and Nevis</a></td>
    <td style="font-weight: bold; text-align:right">5,554</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">43 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">5,508</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">3</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">103,104</td>
    <td style="font-weight: bold; text-align:right">798</td>
    <td style="font-weight: bold; text-align:right">65,141</td>
    <td style="font-weight: bold; text-align:right">1,209,271</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saint-kitts-and-nevis-population/">53,868</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>10</td><td>1,253</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">56</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">207</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/vanuatu/">Vanuatu</a></td>
    <td style="font-weight: bold; text-align:right">5,536</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">4,264</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1,266</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">17,306</td>
    <td style="font-weight: bold; text-align:right">19</td>
    <td style="font-weight: bold; text-align:right">24,976</td>
    <td style="font-weight: bold; text-align:right">78,075</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/vanuatu-population/">319,898</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>58</td><td>53,316</td><td>13</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,958</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">208</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saint-barthelemy/">St. Barth</a></td>
    <td style="font-weight: bold; text-align:right">4,313</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">434,297</td>
    <td style="font-weight: bold; text-align:right">604</td>
    <td style="font-weight: bold; text-align:right">78,646</td>
    <td style="font-weight: bold; text-align:right">7,919,243</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saint-barthelemy-population/">9,931</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>2</td><td>1,655</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">387,171</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">209</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/palau/">Palau</a></td>
    <td style="font-weight: bold; text-align:right">4,122</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">6 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,803</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">313</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">225,900</td>
    <td style="font-weight: bold; text-align:right">329</td>
    <td style="font-weight: bold; text-align:right">42,138</td>
    <td style="font-weight: bold; text-align:right">2,309,311</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/palau-population/">18,247</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>4</td><td>3,041</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">17,154</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">210</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/samoa/">Samoa</a></td>
    <td style="font-weight: bold; text-align:right">4,092</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">9 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1,605</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">2,478</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">20,383</td>
    <td style="font-weight: bold; text-align:right">45</td>
    <td style="font-weight: bold; text-align:right">32,653</td>
    <td style="font-weight: bold; text-align:right">162,649</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/samoa-population/">200,758</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>49</td><td>22,306</td><td>6</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">12,343</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">211</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/cook-islands/">Cook Islands</a></td>
    <td style="font-weight: bold; text-align:right">3,688</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3,049</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">639</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">209,629</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">14,341</td>
    <td style="font-weight: bold; text-align:right">815,154</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/cook-islands-population/">17,593</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>5</td><td></td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">36,321</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">212</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/kiribati/">Kiribati</a></td>
    <td style="font-weight: bold; text-align:right">3,069</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">13 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,595</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">461</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">25,011</td>
    <td style="font-weight: bold; text-align:right">106</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/kiribati-population/">122,706</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>40</td><td>9,439</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">3,757</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">213</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/anguilla/">Anguilla</a></td>
    <td style="font-weight: bold; text-align:right">2,731</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">9 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,716</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">6</td>
    <td style="font-weight: bold; text-align:right">4</td>
    <td style="font-weight: bold; text-align:right">179,188</td>
    <td style="font-weight: bold; text-align:right">591</td>
    <td style="font-weight: bold; text-align:right">51,382</td>
    <td style="font-weight: bold; text-align:right">3,371,301</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/anguilla-population/">15,241</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>6</td><td>1,693</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">394</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">214</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saint-pierre-and-miquelon/">Saint Pierre Miquelon</a></td>
    <td style="font-weight: bold; text-align:right">2,537</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2,449</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">87</td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right">441,678</td>
    <td style="font-weight: bold; text-align:right">174</td>
    <td style="font-weight: bold; text-align:right">22,941</td>
    <td style="font-weight: bold; text-align:right">3,993,907</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saint-pierre-and-miquelon-population/">5,744</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>2</td><td>5,744</td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">15,146</td>
    </tr>
    <tr style="background-color:#F0F0F0">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">215</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><span style="color:#00B5F0; font-style:italic; ">Diamond Princess</span></td>
    <td style="font-weight: bold; text-align:right">712</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">13 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">699</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"> </td>
    <td data-continent="" style="display:none"></td>
    <td></td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">216</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/wallis-and-futuna-islands/">Wallis and Futuna</a></td>
    <td style="font-weight: bold; text-align:right">454</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">7 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">438</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">9</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">41,693</td>
    <td style="font-weight: bold; text-align:right">643</td>
    <td style="font-weight: bold; text-align:right">20,508</td>
    <td style="font-weight: bold; text-align:right">1,883,369</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/wallis-and-futuna-islands-population/">10,889</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>24</td><td>1,556</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">827</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">217</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/montserrat/">Montserrat</a></td>
    <td style="font-weight: bold; text-align:right">176</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">173</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">35,221</td>
    <td style="font-weight: bold; text-align:right">400</td>
    <td style="font-weight: bold; text-align:right">9,403</td>
    <td style="font-weight: bold; text-align:right">1,881,729</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/montserrat-population/">4,997</a> </td>
    <td data-continent="North America" style="display:none">North America</td>
    <td>28</td><td>2,499</td><td>1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">200</td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">218</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/falkland-islands-malvinas/">Falkland Islands</a></td>
    <td style="font-weight: bold; text-align:right">128</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">N/A</td>
    <td style="font-weight: bold; text-align:right;">N/A</td>
    <td style="text-align:right;font-weight:bold;">N/A</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">34,973</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">8,632</td>
    <td style="font-weight: bold; text-align:right">2,358,470</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/falkland-islands-malvinas-population/">3,660</a> </td>
    <td data-continent="South America" style="display:none">South America</td>
    <td>29</td><td></td><td>0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">1,093</td>
    </tr>
    <tr style="background-color:#EAF7D5">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">219</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/china-macao-sar/">Macao</a></td>
    <td style="font-weight: bold; text-align:right">82</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">82</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">123</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">5,375</td>
    <td style="font-weight: bold; text-align:right">8,082</td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/china-macao-sar-population/">665,070</a> </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>8,111</td><td></td><td>124</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="background-color:#EAF7D5">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">220</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/holy-see/">Vatican City</a></td>
    <td style="font-weight: bold; text-align:right">29</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">29</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">36,025</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/holy-see-population/">805</a> </td>
    <td data-continent="Europe" style="display:none">Europe</td>
    <td>28</td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">221</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/western-sahara/">Western Sahara</a></td>
    <td style="font-weight: bold; text-align:right">10</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">1 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">8</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">1</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">16</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/western-sahara-population/">623,433</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>62,343</td><td>623,433</td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">2</td>
    </tr>
    <tr style="background-color:#F0F0F0">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">222</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><span style="color:#00B5F0; font-style:italic; ">MS Zaandam</span></td>
    <td style="font-weight: bold; text-align:right">9</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;">2 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"> </td>
    <td data-continent="" style="display:none"></td>
    <td></td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="background-color:#EAF7D5">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">223</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/marshall-islands/">Marshall Islands</a></td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">117</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/marshall-islands-population/">59,900</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>8,557</td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="background-color:#EAF7D5">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">224</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/niue/">Niue</a></td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">7</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">4,253</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/niue-population/">1,646</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>235</td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="background-color:#EAF7D5">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">225</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/nauru/">Nauru</a></td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">274</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/nauru-population/">10,945</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>3,648</td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="background-color:#EAF7D5">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">226</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/saint-helena/">Saint Helena</a></td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">327</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/saint-helena-population/">6,109</a> </td>
    <td data-continent="Africa" style="display:none">Africa</td>
    <td>3,055</td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="background-color:#EAF7D5">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">227</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/micronesia/">Micronesia</a></td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="font-weight: bold; text-align:right;"> </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">1</td>
    <td style="font-weight: bold; text-align:right;"></td>
    <td style="text-align:right;font-weight:bold;">0</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">9</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"><a href="/world-population/micronesia-population/">117,166</a> </td>
    <td data-continent="Australia/Oceania" style="display:none">Australia/Oceania</td>
    <td>117,166</td><td></td><td></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right"></td>
    </tr>
    <tr style="">
    <td style="font-size:12px;color: grey;text-align:center;vertical-align:middle;">228</td>
    <td style="font-weight: bold; font-size:15px; text-align:left;"><a class="mt_a" href="country/china/">China</a></td>
    <td style="font-weight: bold; text-align:right">171,382</td>
    <td style="font-weight: bold; text-align:right;background-color:#FFEEAA;">+3,020</td>
    <td style="font-weight: bold; text-align:right;">4,638 </td>
    <td style="font-weight: bold; 
                                        text-align:right;"></td>
    <td style="font-weight: bold; text-align:right">143,922</td>
    <td style="font-weight: bold; text-align:right;background-color:#c8e6c9; color:#000">+2,024</td>
    <td style="text-align:right;font-weight:bold;">22,822</td>
    <td style="font-weight: bold; text-align:right">78</td>
    <td style="font-weight: bold; text-align:right">119</td>
    <td style="font-weight: bold; text-align:right">3</td>
    <td style="font-weight: bold; text-align:right">160,000,000</td>
    <td style="font-weight: bold; text-align:right">111,163</td>
    <td style="font-weight: bold; text-align:right">1,439,323,776 </td>
    <td data-continent="Asia" style="display:none">Asia</td>
    <td>8,398</td><td>310,333</td><td>9</td>
    <td style="font-weight: bold; text-align:right">2</td>
    <td style="font-weight: bold; text-align:right"></td>
    <td style="font-weight: bold; text-align:right">16</td>
    </tr>
    </tbody>
    <tbody class="body_continents">
    <tr class="row_continent total_row" data-continent="North America" style="display: none">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>97,234,007</td>
    <td style="background-color:#FFEEAA; color:#000;">+749</td>
    <td>1,451,249</td>
    <td style="background-color:red; color:#fff">+43</td>
    <td>93,381,984</td>
    <td style="background-color:#c8e6c9; color:#000">+471</td>
    <td>2,400,774</td>
    <td>7,079</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="North America" style="display:none;">North America</td>
    <td> </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="row_continent total_row" data-continent="Asia" style="display: none">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>144,826,271</td>
    <td style="background-color:#FFEEAA; color:#000;">+232,493</td>
    <td>1,413,596</td>
    <td style="background-color:red; color:#fff">+493</td>
    <td>123,494,225</td>
    <td style="background-color:#c8e6c9; color:#000">+80,133</td>
    <td>19,918,450</td>
    <td>14,416</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Asia" style="display:none;">Asia</td>
    <td> </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="row_continent total_row" data-continent="South America" style="display: none">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>56,486,386</td>
    <td style="background-color:#FFEEAA; color:#000;">+93</td>
    <td>1,291,354</td>
    <td style="background-color:red; color:#fff">+2</td>
    <td>52,398,800</td>
    <td style="background-color:#c8e6c9; color:#000">+599</td>
    <td>2,796,232</td>
    <td>11,093</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="South America" style="display:none;">South America</td>
    <td> </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="row_continent total_row" data-continent="Europe" style="display: none">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>185,444,461</td>
    <td style=""></td>
    <td>1,794,668</td>
    <td style=""></td>
    <td>166,358,684</td>
    <td style="background-color:#c8e6c9; color:#000"></td>
    <td>17,291,109</td>
    <td>9,474</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Europe" style="display:none;">Europe</td>
    <td> </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="row_continent total_row" data-continent="Australia/Oceania" style="display: none">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>6,348,694</td>
    <td style="background-color:#FFEEAA; color:#000;">+63,060</td>
    <td>9,869</td>
    <td style="background-color:red; color:#fff">+62</td>
    <td>5,730,650</td>
    <td style="background-color:#c8e6c9; color:#000">+11,686</td>
    <td>608,175</td>
    <td>161</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Australia/Oceania" style="display:none;">Australia/Oceania</td>
    <td> </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="row_continent total_row" data-continent="Africa" style="display: none">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>11,816,300</td>
    <td style=""></td>
    <td>253,358</td>
    <td style=""></td>
    <td>11,053,054</td>
    <td style=""></td>
    <td>509,888</td>
    <td>957</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="Africa" style="display:none;">Africa</td>
    <td> </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    <tr class="row_continent total_row" data-continent="" style="display: none">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>721</td>
    <td style=""></td>
    <td>15</td>
    <td style=""></td>
    <td>706</td>
    <td style=""></td>
    <td>0</td>
    <td>0</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="" style="display:none;"></td>
    <td> </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    </tbody>
    <tbody class="total_row_body body_world">
    <tr class="total_row">
    <td></td>
    <td><strong>Total:</strong></td>
    <td>502,156,840</td>
    <td style="background-color:#FFEEAA; color:#000;">+296,395</td>
    <td>6,214,109</td>
    <td style="background-color:red; color:#fff">+600</td>
    <td>452,418,103</td>
    <td style="background-color:#c8e6c9; color:#000">+380,672</td>
    <td>43,524,628</td>
    <td>43,180</td>
    <td>64,422.0</td>
    <td>797.2</td>
    <td></td>
    <td></td>
    <td></td>
    <td data-continent="all" style="display:none">All</td>
    <td>
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    </tr>
    </tbody>
    </table>


Now we have the table in front of us. Let us try to scrape the data from the table. We need rows and the body of the table for getting all the data. We will now scrape the mainTable content for heading rows and columns. Our table is now divided into two parts. The headings are denoted as tr and the rest is inside the tbody. Once we get the tbody, we need to extract all the tr present in tbody.


```python
from bs4 import BeautifulSoup
import requests as request
 
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
mainTable = beautifulSoupObject.table
heading = mainTable.tr
body = mainTable.tbody
row = body.find_all("tr")
```

Printing the row will get us a list of all tr present in tbody as List.

Now we have the data but we need this in a list form. We can see that the contains many td. We will now find all td in the heading and store them in a List.


```python
from bs4 import BeautifulSoup
import requests as request
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
mainTable = beautifulSoupObject.table
heading = mainTable.tr
body = mainTable.tbody
row = body.find_all("tr")
mainHeading = heading.find_all("th")
print(mainHeading)
```

Now we will iterate the list and get all text data using the get_text() function. Then we will store these data in another text using another List.


```python
from bs4 import BeautifulSoup
import requests as request
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
mainTable = beautifulSoupObject.table
heading = mainTable.tr
body = mainTable.tbody
row = body.find_all("tr")
mainHeading = heading.find_all("th")
headingList=[]
for ele in mainHeading:
  headingList.append(ele.get_text().strip())
print(headingList)
```

Good, now we all heading to the table. Next, we will move on to the rows. The row variable in our code is a list that contains all the rows in the tbody. These rows in turn contain several table data in td elements. Now our work is to get all these data in the list. Now what we will do is we will iterate over row List. Now in each tr element in a row, we will find all td elements and store them in a list. Then we will iterate over the tdList and then store all the td data in a list. This way we will have a list of list containing all the data in the table.


```python
from bs4 import BeautifulSoup
import requests as request
pageContent = request.get("https://www.worldometers.info/coronavirus/")
beautifulSoupObject = BeautifulSoup(pageContent.content,'html.parser')
mainTable = beautifulSoupObject.table
heading = mainTable.tr
body = mainTable.tbody
row = body.find_all("tr")
mainHeading = heading.find_all("th")
headingList=[]
for ele in mainHeading:
  headingList.append(ele.get_text().strip())
tableDataList = []
for ele in row:
  tdList = ele.find_all("td")
  tempList = []
  for data in tdList:
    tempList.append(data.get_text().strip())
  tableDataList.append(tempList)
print(tableDataList)
```

Upon printing tableDataList we will get the list of the list containing all the table data. Congratulations now, we have table heading and table data as well.

## Exercise 1: Scrapping wikipedia Article Using Requests Library and Python

#####Q1 Import requests library and check the status_Code 
of wikipedia article url https://en.wikipedia.org/wiki/Web_scraping


```python
'''
import requests

response = requests.get(
	url="https://en.wikipedia.org/wiki/Web_scraping",
)
print(response.status_code)
'''
```

#####Q2 Inspect Wikipedia page and check ID of the title tag of the Article.


```python
'''
import requests
from bs4 import BeautifulSoup

response = requests.get(
	url="https://en.wikipedia.org/wiki/Web_scraping",
)
soup = BeautifulSoup(response.content, 'html.parser')

title = soup.find(id="firstHeading")
print(title.string)
'''
```

#####Q3 Use beautiful soup to find all the <a> tags within the wiki article.


```python
'''
import requests
from bs4 import BeautifulSoup
import random

response = requests.get(
	url="https://en.wikipedia.org/wiki/Web_scraping",
)
soup = BeautifulSoup(response.content, 'html.parser')

title = soup.find(id="firstHeading")
print(title.content)

# Get all the links
allLinks = soup.find(id="bodyContent").find_all("a")
random.shuffle(allLinks)
linkToScrape = 0

for link in allLinks:
	# We are only interested in other wiki articles
	if link['href'].find("/wiki/") == -1: 
		continue

	# Use this link to scrape
	linkToScrape = link
	break

print(linkToScrape)
'''
```

#####Q4 What is the difference between requests & BeautifulSoup library?
 

- Requests — A Python library used to send an HTTP request to a website and store the response object within a variable.
- BeautifulSoup — A Python library used to extract the data from an HTML or XML document.

#####Q5 Explain common status codes from series 2XX, 4XX, 5XX & find out the codes which occur because of failure from server side

Note - Failure from server side occurs when server fails to respond 

200: This code is used for a successful request.

201: For a successful request and data was created.

204: For empty response.

400: This is used for Bad Request. If you enter something wrong or you missed some required parameters, then the request would not be understood by the server, and you will get 400 status code.

401: This is used for Unauthorized Access. If the request authentication failed or the user does not have permissions for the requested operations, then you will get a 401 status code.

403: This is for Forbidden or Access Denied.

404: This will come if the Data Not Found.

500: This code is used for Internal Server Error.

Most of the response codes from 5XX series indicate to server failure

## Exercise 2


```python
#Create a varible html_doc.

html_doc = """
<html>
<head>
<meta http-equiv="Content-Type" content="text/html;
charset=iso-8859-1">
<title>An example of HTML page</title>
</head>
<body>
<h2>This is an example HTML page</h2>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc at nisi velit,
aliquet iaculis est. Curabitur porttitor nisi vel lacus euismod egestas. In hac
habitasse platea dictumst. In sagittis magna eu odio interdum mollis. Phasellus
sagittis pulvinar facilisis. Donec vel odio volutpat tortor volutpat commodo.
Donec vehicula vulputate sem, vel iaculis urna molestie eget. Sed pellentesque
adipiscing tortor, at condimentum elit elementum sed. Mauris dignissim
elementum nunc, non elementum felis condimentum eu. In in turpis quis erat
imperdiet vulputate. Pellentesque mauris turpis, dignissim sed iaculis eu,
euismod eget ipsum. Vivamus mollis adipiscing viverra. Morbi at sem eget nisl
euismod porta.</p>
<p><a href="www.xyz.com" id="Link1">Link1</a></p>
<p><a href="www.pqr.com" id="Link2">Link2</a></p>
</body>
</html>
"""
```


```python
from bs4 import BeautifulSoup
```

#####Q1: Write a program to find the title tags from a given html document.


```python
'''
soup = BeautifulSoup(html_doc, 'html.parser')
print("Title of the document:")
print(soup.find("title"))
'''
```

#####Q2: Write a program to retrieve all the paragraph tags from a given html document.


```python
'''
soup = BeautifulSoup(html_doc, 'html.parser')
print("All paragraph tags:")
print(soup.find_all("p"))
'''
```

#####Q3: Write a program to get the number of paragraph tags of a given html document.


```python
'''
soup = BeautifulSoup(html_doc, 'html.parser')
print("Number of paragraph tags:")
print(len(soup.find_all("p")))
'''
```

#####Q4: Write a program to extract the text in the first paragraph tag of a given html document.


```python
'''
soup = BeautifulSoup(html_doc, 'html.parser')
print("The text in the first paragraph tag:")
print(soup.find_all('p')[0].text)
'''
```

#####Q5: Write a program to find the length of the text of the first ```<h2>``` tag of a given html document.


```python
'''
soup = BeautifulSoup(html_doc, 'html.parser')
print("Length of the text of the first <h2> tag:")
print(len(soup.find('h2').text))
'''
```

#####Q6: Write a Python program to find the text of the first ``` <a> ``` tag of a given html text.


```python
'''
soup = BeautifulSoup(html_doc, 'html.parser')
print("Text of the first <a> tag:")
print(soup.find('a').text)
'''
```

#####Q7: Write a Python program to find the href of the firstl ``` <a> ``` tag of a given html document.


```python
'''
soup = BeautifulSoup(html_doc, 'html.parser')
print("href of the first <a> tag:")
print(soup.find('a').attrs['href'])
'''
```

#Introduction to Simple Web Applications with Flask

##Creating a Flask app that serves HTML

**create a basic Flask app**

We'll start off with a boilerplate, one-file Flask app, i.e. just app.py. We won't worry yet about making multiple pages or multiple file.

See if you can create the boilerplate from memory:


```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def homepage():
    return """
<!DOCTYPE html>
<head>
   <title>My title</title>
   <link rel="stylesheet" href="http://stash.compjour.org/assets/css/foundation.css">
</head>
<body style="width: 880px; margin: auto;">  
    <h1>Visible stuff goes here</h1>
    <p>here's a paragraph, fwiw</p>
    <p>And here's an image:</p>
    <a href="https://www.flickr.com/photos/zokuga/14615349406/">
        <img src="http://stash.compjour.org/assets/images/sunset.jpg" alt="it's a nice sunset">
    </a>
</body>
"""

if __name__ == '__main__':
    app.run(debug=True, use_reloader=True)
```

And switch to the command-line and get it running:



```
python app.py
```

Then visit 127.0.0.1:5000 (i.e. localhost:5000). This will runs our little pretty-HTML generating Flask app.



##Creating Multiple Routes and Dynamic Content in Flask

**Getting started**

At the end of this lesson, you'll be able to create an app that can respond to any arbitrary URL path:


But first, let's revisit the app.py for the most basic Flask app. Try to rewrite it from scratch, just from memory:



```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def homepage():
    return """<h1>Hello world!</h1>"""

if __name__ == '__main__':
    app.run(use_reloader=True)
```



**Creating multiple routes**

To add a new route, simply call the route() function again with the desired path and create a view function for it:



```
@app.route('/stanford')
def stanford_page():
    return """<h1>Hello stanford!</h1>"""
```

Just for fun, let's include a static Google Maps image of "stanford". This is the simplest call (by "call", I mean, URL, as that's how this particular API works) to the Google Static Map API that will return a map image with a marker placed at "stanford":

https://maps.googleapis.com/maps/api/staticmap?size=700x300&markers=stanford

Click on that URL to see the image that it generates – note that the URL takes you to an image file, not a HTML webpage that displays a map image.

While we're at it, let's add an image from Google's Street View service; here's the call to that API, according to the Street View Image API:

https://maps.googleapis.com/maps/api/streetview?size=700x300&location=stanford

Let's add both images to the HTML returned by view function binded to the /stanford path:



```
@app.route('/stanford')
def stanford_page():
    return """
      <h1>Hello stanford!</h1>

      <img src="https://maps.googleapis.com/maps/api/staticmap?size=700x300&markers=stanford" alt="map of stanford">
  
      <img src="https://maps.googleapis.com/maps/api/streetview?size=700x300&location=stanford" alt="street view of stanford">
    """
```

The resulting page when visiting http://localhost:5000/stanford looks like:






**Making even more routes**

But what if we wanted to create a paths for other locations, such as newyork and tokyo? Well, there's always copy and paste:



```
@app.route('/stanford')
def stanford_page():
    return """
      <h1>Hello stanford!</h1>

      <img src="https://maps.googleapis.com/maps/api/staticmap?size=700x300&markers=stanford" alt="map of stanford">
  
      <img src="https://maps.googleapis.com/maps/api/streetview?size=700x300&location=stanford" alt="street view of stanford">
    """

@app.route('/newyork')
def newyork_page():
    return """
      <h1>Hello newyork!</h1>

      <img src="https://maps.googleapis.com/maps/api/staticmap?size=700x300&markers=newyork" alt="map of newyork">
  
      <img src="https://maps.googleapis.com/maps/api/streetview?size=700x300&location=newyork" alt="street view of newyork">
      """
@app.route('/tokyo')
def tokyo_page():
    return """
      <h1>Hello tokyo!</h1>

      <img src="https://maps.googleapis.com/maps/api/staticmap?size=700x300&markers=tokyo" alt="map of tokyo">
  
      <img src="https://maps.googleapis.com/maps/api/streetview?size=700x300&location=tokyo" alt="street view of tokyo">
    """
```

Here's what http://127.0.0.1/newyork looks like:


Creating routes with variables
Of course, it's just not feasible for you, the developer, to enumerate every possible route that a user will want to try out, whether it be stanford or chicago or timbuktu.

This is where we get into the core of what makes a web application different from a regular web page: we program our app to accept variable paths.

We already have 95% of the process abstracted. Remember that we started out with a view function that looked like this:


```
@app.route('/stanford')
def stanford_page():
    return """
      <h1>Hello stanford!</h1>

      <img src="https://maps.googleapis.com/maps/api/staticmap?size=700x300&markers=stanford" alt="map of stanford">
  
      <img src="https://maps.googleapis.com/maps/api/streetview?size=700x300&location=stanford" alt="street view of stanford">
    """
```

And now it looks like this:

```
@app.route('/stanford')
def stanford_page():
    return(HTML_TEMPLATE.substitute(place_name='stanford'))
```

Now we have to abstract the parts of the routing function and view function that explicitly refer to stanford…In pseudocode, it might look something like this:

```
@app.route('/SOME_PLACE')
def some_place_page():
    return(HTML_TEMPLATE.substitute(place_name=SOME_PLACE))
```

In fact, that pseudocode is very close to what Flask requires; from its Quickstart documentation on variable rules:

To add variable parts to a URL you can mark these special sections as . Such a part is then passed as a keyword argument to your function.

Here's what that abstracted route/view function can look like; notice what stays the same and what changes:

```
@app.route('/<some_place>')
def some_place_page(some_place):
    return(HTML_TEMPLATE.substitute(place_name=some_place))
```

Delete the code regarding the /stanford, /newyork, and other routes (although you should leave the Hello World for /, just to have a page for the root homepage route). We don't need it now. This is what the entire app looks like:

```
from flask import Flask
from string import Template
app = Flask(__name__)

HTML_TEMPLATE = Template("""
<h1>Hello ${place_name}!</h1>

<img src="https://maps.googleapis.com/maps/api/staticmap?size=700x300&markers=${place_name}" alt="map of ${place_name}">

<img src="https://maps.googleapis.com/maps/api/streetview?size=700x300&location=${place_name}" alt="street view of ${place_name}">
""")

@app.route('/')
def homepage():
    return """<h1>Hello world!</h1>"""

@app.route('/<some_place>')
def some_place_page(some_place):
    return(HTML_TEMPLATE.substitute(place_name=some_place))

if __name__ == '__main__':
    app.run(debug=True, use_reloader=True)
Now, put any name you'd like in your web app's path, e.g. http://127.0.0.1/chicago, http://127.0.0.1/hong+kong, http://127.0.0.1/moscow, http://127.0.0.1/zimbabwe
```


#####Q1 Make a sample mailing service using Flask


```python
"""
Solution
"""
from flask_mail import Mail, Message
from flask import Flask
 
app = Flask(__name__)
mail = Mail(app)
 
@app.route(“/mail”)
def email():
    msg = Message( “Hello Message”, sender=”admin@test.com”, recipients=[“to@test.com”])
   mail.send(msg)
```

#####Q2 What is WSGI?

"""
Solution
"""

WSGI stands for the Web Server Gateway Interface. It is a Python standard defined in PEP 3333. WSGI is pronounced as “Whiskey.” It is a specification that describes how a web server communicates with a web application.

#####Q3 How to change default host and port in Flask?


```python
"""
Solution
"""

from flask import Flask
app = Flask(__name__)
 
@app.route("/")
def index():
    return "Hello, World!"
 
if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
```

#####Q4 How to get query String in Flask?


```python
"""
Solution
"""
from flask import Flask
from flask import request
 
app = Flask(__name__)
 
@app.route("/")
def index():
val = request.args.get("var") 
 
return "Hello, World! {}".format(val)
 
if __name__=="__main__":
app.run(host="0.0.0.0", port=8080)
```

#####Q5 How to get the user agent in Flask?


```python
"""
Solution
"""
from flask import Flask
from flask import request
 
app = Flask(__name__)
 
@app.route("/")
def index():
    val = request.args.get("var")
    user_agent = request.headers.get('User-Agent')   
 
    response = """
    Hello, World! {}
    You are accessing this app with {}
    """.format(val, user_agent)    
return response
if __name__=="__main__":
    app.run(host="0.0.0.0", port=8080)
```
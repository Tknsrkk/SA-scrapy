# Scrapy--A Fast and Powerful Scraping and Web Crawling Framework

![](https://s2.ax1x.com/2019/10/01/uUDwhF.jpg)

## Abstract

Scrapy (/ ˈ s k r eɪ p i / SKRAY -pee) is a free and open-source web-crawling framework written in Python. Originally designed for web scraping, it can also be used to extract data using APIs or as a general-purpose web crawler. It is currently maintained by Scrapinghub Ltd., a web-scraping development and services company.

Written in: Python\
Initial release: 26 June 2008\
Developer(s): Scrapinghub, Ltd.\
Stable release: 1.7.3, / 1 August 2019; 6 days ago

While the development is open-source, the amount of documentation about contributing is limited. This results in a project where programming is not done through conventions or guidelines but with a strong focus on getting things to work. Therefore, this document as a whole can serve as a helpful introduction to prospective developers looking to better understand the architecture to which they might contribute.

## Table of contents

- [1.Introduction](#Introduction)
- [2.Stakeholders](#Stakeholders)
  - [2.1 Overview](#Overview)
  - [2.2 Quality Attributes](#Quality-Attributes)
  - [2.3 Power Interest Grid](#Power-Interest-Grid)
- [3.Context View](#Context-view)
  - [3.1 System Scope](#System-Scope)
  - [3.2 Client](#Client)
  - [3.3 External Entities](#External-Entities)
- [4.Development View](#Development-view)
  - [4.1 Code-Organization](#Code-Organization)
  - [4.2 Module-Organization](#Module-Organization)
- [5. Deployment View](#Deployment-view)
  - [5.1 Third-party Software Requirements](#Third-party-dependencies)
  - [5.2 Specialist Knowledge](#Specialist-Knowledge)
- [6. Functional View](#6. Functional View)
  - [6.1 Functionalities](#6.1)
  - [6.2 Extensibility](#6.2)
- [7. Performance Perspective](#7)
- [8. Technical Debt](#8)
  - [8.1 Static Analysis](#8.1)
  - [8.2 Testing Debt](#8.2)
- [9. Evolution Perspective](#9)
- [10. Conclusion](#10)

## Introduction

As we enter the era of big data, data analysis and data collection technologies become particularly important. With the demand of an easy to collect data, scrapy arises.Scrapy is an application framework written to crawl web site data and extract structural data. It can be used in a series of programs including data mining, information processing or storing historical data.It is originally designed for page fetching (more specifically, Web fetching) and can be used to retrieve data returned by the API (for example, Amazon Associates Web Services) or general purpose Web crawlers.

![](https://s2.ax1x.com/2019/10/01/uUyg7q.png)

*Fugure 1: The main page of scrapy*

This document gives an overview of the overarching architecture of the scrapy project. It sets the scenes by introducing the project and discussing its stakeholders. It then takes on different viewpoints and perspectives as defined by Rozanski and Woods  to analyse scrapy's performance, in addition to discussing the technical debt hidden in the depths of the codebase.

## Stakeholders

>   A stakeholder is a member of "groups without whose support the organization would cease to exist".

As the definition above, stakeholders in Scrapy are people who are interested in and influence Scrapy. More specificly, stakeholders can adivce to it and make some influence on Scrapy's policy and so on. So, we will firstly have a glimpse on the overview of the stakeholders which includes developers, maintainers, users and other kinds of stakeholders which are of vital importance. After we have had an overview of those kinds of stakeholdes, we will have a deeper appreciation of those stakeholders and try to give the Power Interest Graph of Scrapy in which we will analyze the reason.<a href="#ref_sta1">[1]</a>

### Overview 

-   Acquirers
    
    Scrapy is now managed by **Scrapinghub**. Scrapinghub is specializes in web crawling, and it was founded by Scrapy creators.

-   Developers

    Because Scrapy is an open source project, so developers can be found on Github. Although there are thousands of brilliant developers who have contributed to Scrapy, in order to specify the core developers of Scrapy more clearly, we will mainly discuss the core team which based on the statistics on Github to show the most contributed developers in this case, such as: @[dangra](https://github.com/dangra), @[redapple](https://github.com/redapple), @[kmike](https://github.com/kmike). And the following table contains those Most contributed developers in trems of commit number.

    Developer     | Commits | Additions | Deletions
    --------------|---------|-----------|----------
    dangra        | 738     | 83,176    | 95,953
    redapple      | 392     | 9,643     | 3,146
    kmike         | 327     | 8,441     | 6,586
    void          | 246     | 20,266    | 13,201
    curita        | 174     | 12,211    | 10,056
    lopuhin       | 133     | 1,221     | 701
    elacuesta     | 128     | 4,049     | 2,476
    eliasdorneles | 116     | 2,725     | 2,956

    *Table 1: Most contributed developers in trems of commit number*

-   Maintainers

    Maintainers are responsible for managing the development and evolution of Scrapy. In Scrapy, the core teams described above work as maintainers. They discuss the development direction of Scrapy and they accept and review pull-requests. We can view the main contributors from the statistics on Github. And the core mintainers are the same as those developers above.
 
-   Users

    Scrapy has been used by both big companies like **PARSE.LY**, **Direct Employers Foundation**, government institution like **DATA.GOV.UK** and many other personal users who want to extracte the data you need from websites.

-   Suppliers
    
    The development of Scrapy is coordinated by **Github**, which can be clearly classified as a supplier. Meanwhile, **Python** is the scripting language that Scrapy uses, so we also regard Python as a supplier.

-   Communicators
    
    Scrapy has large and active communities on **Github**, **Reddit** and **StackOverflow**. These communities have tens of thousands of communicators which can help explaining the system to other stakeholders via documentation and the experiences they have.

-   Competitors
    
    As we all know, there are tons of framework that can extracte data from the Internet. For Scrapy, there are competitor as **PySpider**, **Crawley** and **Portia**. Competitor can help Scrapy to be better and supervise it to move forward.

The following figure shows the stakeholders mentioned above, and it proides a channel through which people can have a more direct impression of those stakeholders.

![](https://s2.ax1x.com/2019/10/01/uUrhV0.jpg)

*Figure 1: Stakeholders of Scrapy*

### Quality-Attributes

Scrapy is a fast and powerful scraping and web crawling framework. So, there are a few of the quality attributes which is of vital importance. 

-   Performance

    As the Scrapy development team members want, Scrapy should be fast and powerful. In this term, the performance of Scrapy is the main quality attribute which developers focus on. And great performance can provide a channel through which users can have a better feel of it. Moreover, this can let Scrapy out among those competitors.

-   Usability

    Scrapy play an important role in web crawling, which means they need to be easy to use. Without that, Scrapy can not be appriciated by users, who are always wondering to have a simple way to make things done. In some certain cases, usability is considered to be essential such as when people has little time to accomplish something. So, usability is also an important quality attribute.

-   Modifiability

    Because people will have their certain purpose of their works, and it is impossible to satisfy everyone. So, Scrapy need modifiability to cater for all tastes. Scrapy leaves many interfaces for users to custom their own features. And users can use this easy and useful interfaces to accomplish their own works.
    
### Power-Interest-Grid

The following figure shows the Power Interest Grid. Power Interest Grid contains the main stakeholder categories and more detailed explanation will be listed.

![](https://s2.ax1x.com/2019/10/01/uUr55T.jpg)

*Figure 2: Power Interest Grid*

-   Low power and low interest
    
    Suppliers like GitHub are stakeholders that have no control over Scrapy, and they do not have directly benefit from it. For Github, they should be in the low power and low interest part.

-   Low power and high interest
    
    Users, Communicators and Competitors of Scrapy are stakeholders who have high interest in Scrapy and will be greatly affected by the changes in Scrapy, but they have nearly no power to influence it.

-   High power and low interest
    
    Suppliers like Python provide necessary library and tools to develop Scrapy. The changes of Python will directly affect the development of Scrapy but Scrapy has little influence on Python on the contrary.

-   High power and high interest
    
    Core developers and acquirers of Scrapy are stakeholders who have significant interest and power in the development of Scrapy. And in Scrapy, developers are also maintainers, so those people will guarantee it to run without error and provide new features. At the same time, acquirers will provide many kinds of support. Both of them can also largely influence Scrapy, so they will be in the high power and low interest part.

## Context-view

A context view describes the relationships, dependencies, and the interactions between the system and its environment.Many architecture descriptions focus on views that model the system’s internal structures, data elements, interactions, and operation. Architects tend to assume that the “outward-facing” information — the system’s runtime context, its scope and requirements, and so forth – is clearly and unambiguously defined elsewhere. However, you often need to include a definition of the system’s context as part of your architectural description.<a href="#ref_con1">[2]</a>

![Figure 1 overall structure](https://i.postimg.cc/w3KDFd2Q/1.png)

### System-Scope
Scrapy is an open source and collaborative framework for extracting the data you need from websites.The client can use this framework in a fast, simple, yet extensible way[[1]]().It is originally designed for page fetching (more specifically, Web fetching) and can aslo be used to retrieve data returned by the API (for example, [Amazon Associates Web Services](http://aws.amazon.com/associates/)) or general purpose Web crawlers.
### Client
The attraction is that Scrapy is a framework that anyone can easily modify to suit their needs.Scrapy features a fast, high-level screen scraping and web scraping framework developed in Python for scraping web sites and extracting structured data from pages.Scrapy has a wide range of applications, including data mining, monitoring and automated testing. Reactive updates are dead simple.

>* Scrapy is asynchronous
* adopt more readable xpath instead of regular expression
* powerful statistical and log system
* crawl on different urls at the same time
* shell mode is supported to facilitate independent debugging
* write middleware to make it easier to write a uniform filter
* store the database by pipeline
### External-Entities
The figure below shows the context view of Scrapy.

![](https://s2.ax1x.com/2019/10/01/uUrjVx.png)

* Developing languages: Python
* Runs on: Windows, macOS, Linux, Andriod, iOS…
* Supported by：browsers(chrome、ie、Firefox…)
* Communication: Srapy community, Srapy Chinese website, GitHub, stackoverflow…
* Programmed in: IPython, Pycharm, Anaconda, Jupyter Notebook…
* Competes with: Crawley, Portia, Grab…

## Development-view

This section describes the architecture that supports React development process. First, we will describe principles and guidelines that govern the development of Scrapy. This will be followed by source code and module organizaton.
##4.1 Development characteristics
Scrapy is a fast high-level web crawling framework, used to crawl websites and extract structured data from their pages. It can be used for a wide range of purposes, from data mining to monitoring and automated testing<a href="#ref_dev_1">[3]</a>. It's normal for us to compare Scrapy to Request lib, so the developent of characteristics of Scrapy should be  recounted.

#### Asynchronous processing
One of the main advantages about Scrapy is that: requests are scheduled and processed asynchronously. This means that Scrapy doesn’t need to wait for a request to be finished and processed, it can send another request or do other things in the meantime. This also means that other requests can keep going even if some request fails or an error happens while handling it.<a href="#ref_dev_2">[4]</a>
#### Convenient request settings
Scrapy  gives you control over the politeness of the crawl through a few settings You can do things like setting a download delay between each request, limiting amount of concurrent requests per domain or per IP, and even [using an auto-throttling extension](https://docs.scrapy.org/en/latest/topics/autothrottle.html#topics-autothrottle) that tries to figure out these automatically.
####Built-in parser
 Built-in support for selecting and extracting data from HTML/XML sources using extended CSS selectors and XPath expressions, with helper methods to extract using regular expressions.
#### interactive shell console
The Scrapy shell is an interactive shell where you can try and debug your scraping code very quickly, without having to run the spider. It’s meant to be used for testing data extraction code, but you can actually use it for testing any kind of code as it is also a regular Python shell.<a href="#ref_dev_3">[5]</a>
#### wild middlewares for handling
Scrapy privides wide range of built-in extensions and middlewares for handling:cookies and session handling, http compression,authentication, caching, user-agent spoofing, robots.txt, crawl depth restriction and more.<a href="#ref_dev_4">[6]</a>

### Code-Organization
The following figure shows the source code organization of scrapy.
![Figure1 code organization of scrapy](https://upload-images.jianshu.io/upload_images/17534427-80fbf5f00989de4e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### Test files
Source code attachs a test project, placed in the tests folder. This test project create ```TestSprider``` object to implement spider and use ```ScrapyRedisBloomFilter``` to remove duplication. We can use console to ```scrapy crawl test``` to run this test project. It casts most of functions of scrapy.
#### Funtional  files
The functionality part contains the components that are responsible for functions of the project. *Commands* implements the console tool of scrapy. *http* integrate the HTTP processing functions. The most important  is *core* , which includes the significant module of scrapy such as *engine*, *scheduler*, *scraper* and so on. These core modules'  relationship will be analized later.
#### Documentations
The documentation section contains codes used to demonstrate and generate the documentation of Scrapy. They are often written in RST format. *README.rst* contains the usage and installation of  Scrapy. *docs* contains the Materials used by documents like pictures and logo.
#### Others
Scrapy has other files, such as version log files, contributor log files, and relatively independent script files.

### Module-Organization
This section focuses on the main modules of scrapy and their interactions.
#### Modules introduction
##### Scrapy Engine
The engine is responsible for controlling the data flow between all components of the system, and triggering events when certain actions occur. 
##### Scheduler
The Scheduler receives requests from the engine and enqueues them for feeding them later (also to the engine) when the engine requests them.
##### Downloader
The Downloader is responsible for fetching web pages and feeding them to the engine which, in turn, feeds them to the spiders.
##### Spiders
Spiders are custom classes written by Scrapy users to parse responses and extract items (aka scraped items) from them or additional requests to follow.
##### Item Pipeline
The Item Pipeline is responsible for processing the items once they have been extracted (or scraped) by the spiders. Typical tasks include cleansing, validation and persistence (like storing the item in a database). 
The following diagram shows an overview of the Scrapy architecture with its components and an outline of the data flow that takes place inside the system (shown by the red arrows).
#### Modules' relationship and Data flow

The following diagram shows an overview of the Scrapy architecture with its components and an outline of the data flow that takes place inside the system (shown by the red arrows). The data flow is also described below.<a href="#ref_dev_5">[7]</a>

![Figure 2 data flow](https://upload-images.jianshu.io/upload_images/17534427-a835f7ea3b5767fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
The data flow in Scrapy is controlled by the execution engine, and goes like this:

1.  The *Engine* gets the initial Requests to crawl from the *Spider*
2.  The *Engine*  schedules the Requests in the *schedules*  and asks for the next Requests to crawl.
3.  The *Schedules* returns the next Requests to the *Engine* 
4.  The *Engine* sends the Requests to the *Downloader*, passing through the *Downloader Middlewares*
5.  Once the page finishes downloading the [Downloader] and sends it to the Engine, passing through the *Downloader Middlewares*
6.  The*Engine* receives the Response from the *Downloader* for processing, passing through the *Spider*
7.  The *Spider* processes the Response and returns scraped items and new Requests (to follow) to the *Engine*
8.  The *Engine* sends processed items to *Item Pipelines*, then send processed Requests to the *Scheduler* and asks for possible next Requests to crawl.
9.  The process repeats (from step 1) until there are no more requests from the *Schedules*

## Deployment-View
According to Rozanski and Woods<a href = "#ref_dev_6">[8]</a>, the deployment view describes the environment into which the system will be deployed, including the dependencies the system has on its runtime environment. It defines physical, computational, and software-based requirements for running the system.

### Third-party-dependencies
Dependencies | Role
-|-
PyCharm|An integrated development environment (IDE) used  specifically for the Python language. 
pip|A Python package installer
pywin32|Python extensions for Microsoft Windows Provides access to much of the Win32 API.
pyOpenSSL|A Python package which is used to support Security Socket Layer.
cryptography|A Python library used for encrypting.
zope.interface|A library providing interface for Python.
cssselect|An extension package for handling CSS selectors.
lxml|A Python library for processing XML and HTML which supports XPath.
Twisted|A Python library used as an Event-driven network framework.
### Specialist-Knowledge
To use Scrapy some specialist knowledge is required.

* Basic knowledge of programming in Python
* Familiar with regular expression and XPath
* Understand Depth-First-Search and Breadth-First-Search

## 6. Functional view
According to the defination of functional vew in  Rozanski and Wood's book[[1]]()
>Functional vew: Describes the system’s functional elements, their responsibilities, interfaces, and primary interactions. A Functional view is the cornerstone of most ADs and is often the first part of the description that stakeholders try to read. It drives the shape of other system structures such as the information structure, concurrency structure, deployment structure, and so on. It also has a significant impact on the system’s quality properties such as its ability to change, its ability to be secured, and its runtime performance.

In this part, main functionalities and primary interactions  are discussed. The functional capabilities, external interfaces are also concerned.

### 6.1 Functional-capabilities
Functional capabilities define what the system is required to do and what it is not required to do.  Since Scrapy is a web crawling framework for crawling web sites and extracting structured data from pages, the m ain functionalities that it needs to have coincided with that. Table 2 shows the core functionalities required of Scrapy and describes what their responsibilities are.
                                                
| Functionality| Description | Implementation |
| ------ | ------ | ------ |
| Send network request | The main component of the system is to create kinds of HTTP or HTTPS requests to defferent web sites for  expected data  | Spider and Schedule module |
| Data download | After the request is made, the corresponding data needs to be downloaded to memory according to the response | Downloader module|
| Data parsing | The data downloaded from the website is often not the final desired format, and data transmission is required in the process of network communication. |  Downloader module and Downloader middleware |
| Data storage | The results of data analysis often need to be stored as text or various databases. | Item Pipeline module |
| Anti crawler mechanism | Many websites often use the latter anti crawler mechanism, so how to deal with it is particularly important | Engine module |
| Asynchronous request | It is also necessary to have efficient crawling efficiency in the fight against type crawlers, and synchronization mechanism is a desirable solution. | Engine and Scheduler module |
| Debug | Debug is a troublesome problem in crawlers. It is often necessary to start a crawler to debug, which will cause problems such as increasing useless requests. How to debug efficiently is very important. | Scrapy Shell |    
                                         
### 6.2 Functional-interactions
Some of the core functions of scratch are described above. In this section, we will focus on how these functions and functional modules interact with each other.

![Figure 2 Functional interactions](https://upload-images.jianshu.io/upload_images/17534427-183378c230bd0252.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####Interfaces between modules during a life-circle
*step 1*. Firstly, the scratch engine gets the start request collection from the spider, which is the ```start_urls``` defined in the spider. If the spider overrides the ```start_requests() ```method, the request collection returned by this method is the start request.

*step 2*. The scrape engine sends the received ```request structure``` to the scheduling center to start scheduling.

*step 3*. The scrape engine requests the dispatch center to get the next ```request structure``` to be crawled.

*step 4*. After the summary engine gets the request, it sends the request to the downloader. This process goes through a series of download middleware configured in settings.py. All the download middleware configured in ```settings.py ```will process the request in turn. ——Corresponding to ```downloadermiddleware#Process_ request() ```method

*step 5*. The downloader pulls the response content according to the request. For example, if the URL of the request is http://www.google.com, the downloader will pull the corresponding web page content and encapsulate it as a ```Response``` object.

*step 6*. The downloader sends the response to the graph engine. This process will also go through a series of download middleware configured in ```settings.py```. These download middleware will process' response 'in turn. ——Corresponding to
 ```DownloaderMiddleware#process_response() ```method.
 
*step 7*. After getting the ```Response```, the graph engine sends the response to the spider and hands it to the corresponding spider function for processing. Here, the default method is ```parse()```, which is specified when the callback method constructs the ```Request```. The engine sends the ```Response``` through a series of spider middleware configured in ```settings.py```, which will process the ```Response ```in turn. ——Corresponding to```CorrespondenceSpiderMiddleware#process_spider_input()```method.

*step 8*. After processing the ```Response```, the spider will return a result, which is``` an Iterable object containing a Request or item object```. Then send the result to the graph engine. This process will also go through a series of spider middleware configured in ```settings.py```, which will process the result in turn. ——Corresponding to ```spidermiddleware_process_spider_output ()```method.

*step 9*. After the result is obtained by the scrape engine, the items will be sent to the ```item pipeline``` for processing, and these items will be processed by a series of ```pipelin```e configured in settings.py. At the same time, the request in the result will also be sent to the dispatcher for scheduling.

*step 10*. Continue to repeat step 2 until all ```Requests``` are processed and the program exits.

### 6.3 External-interfaces
The external interfaces provided by Scrapy mainly concern functionality to extension development possible.  There are too many interfaces to completely list them in this report, so for a full list of available external interface refer to the ```setting.py```.

The infrastructure of the settings provides a global namespace of key-value mappings that the code can use to pull configuration values from. The settings can be populated through different mechanisms, which are described below.[[2]]()

| Interface | Description | 
| ------ | ------ |
| ``` SPIDER_MODULES ``` | File path stored by crawler | 
| ``` NEWSPIDER_MODULE ``` | Create the template of the crawler file. The created crawler file will be stored in this directory. | 
| ```  USER_AGENT``` | Set UA to simulate browser request | 
| ``` ROBOTSTXT_OBEY ``` | Set whether robot protocol compliance is required: true by default | 
| ```CONCURRENT_REQUESTS  ``` | Set the maximum concurrent data requested (downloader), 16 by default | 
| ```DOWNLOAD_DELAY  ``` | Set the download delay of the request. The default is 0. | 
| ``` CONCURRENT_REQUESTS_PER_DOMAIN ``` |Set the maximum number of concurrent requests for the website. The default is 8. | 
| ```CONCURRENT_REQUESTS_PER_IP  ``` | Set the maximum concurrent requests of an IP. The default is 0. | 
| ```  COOKIES_ENABLED ``` | Whether to carry cookies? True by default | 
| ```  COOKIES_DEBUG``` | Tracking cookies, false by default | 
| ``` SPIDER_MIDDLEWARES ``` | Set up and activate crawler Middleware | 
| ```  ITEM_PIPELINES``` | Set and activate the pipeline file, followed by a number indicating priority | 
| ``` HTTPCACHE_EXPIRATION_SECS ``` | Set the timeout of the cache. The default value is 0, which is always valid. | 
| ```AUTOTHROTTLE_MAX_DELAY  ``` | Maximum download delay | 

## References

<a name="ref_sta1">[1]</a>Wikipedia. Stakeholder (corporate)[EB/OL］.Stakeholder (corporate) - Wikipedia，https://en.wikipedia.org/wiki/Stakeholder_(corporate)

<a name="ref_con1">[2]</a>[https://scrapy.org/](https://scrapy.org/)

<a name="ref_dev_1">[3]</a>[https://docs.scrapy.org/en/latest/](https://docs.scrapy.org/en/latest/)

<a name="ref_dev_2">[4]</a>[https://www.cnblogs.com/jclian91/p/9799697.html](https://www.cnblogs.com/jclian91/p/9799697.html)

<a name="ref_dev_3">[5]</a>[https://docs.scrapy.org/en/latest/topics/shell.html#topics-shell](https://docs.scrapy.org/en/latest/topics/shell.html#topics-shell)

<a name="ref_dev_4">[6]</a>[https://www.cnblogs.com/xieqiankun/p/know_middleware_of_scrapy_1.html](https://www.cnblogs.com/xieqiankun/p/know_middleware_of_scrapy_1.html)

<a name="ref_dev_5">[7]</a>[https://docs.scrapy.org/en/latest/topics/architecture.html](https://docs.scrapy.org/en/latest/topics/architecture.html)

<a name="ref_dev_6">[8]</a>Nick Rozanski and Eoin Woods. Software System Architecture: Working With Stakeholders Using Viewpoints and Perspectives. Addison-Wesley, 2012.


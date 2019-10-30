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
- [6. Functional View](#Functional-View)
  - [6.1 Functional Capabilities](#Functional-Capabilities)
  - [6.2 Functional Interactions](#Functional-Interactions)
  - [6.3 External interfaces](#External-interfaces)
- [7. Performance Perspective](#Performance-Perspective)
- [8. Technical Debt](#Technical-Debt)
  - [8.1 Analysis Tools](#Analysis-Tools)
  - [8.2 Code Analysis](#Code-Analysis)
  - [8.3 Evaluation](#Evaluation)
- [9. Evolution Perspective](#Evolution)
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

## Functional-view
According to the defination of functional vew in  Rozanski and Wood's book<a href="#ref_dev_7">[9]</a>
>Functional vew: Describes the system’s functional elements, their responsibilities, interfaces, and primary interactions. A Functional view is the cornerstone of most ADs and is often the first part of the description that stakeholders try to read. It drives the shape of other system structures such as the information structure, concurrency structure, deployment structure, and so on. It also has a significant impact on the system’s quality properties such as its ability to change, its ability to be secured, and its runtime performance.

In this part, main functionalities and primary interactions  are discussed. The functional capabilities, external interfaces are also concerned.

### Functional-capabilities
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
                                         
### Functional-interactions
Some of the core functions of scratch are described above. In this section, we will focus on how these functions and functional modules interact with each other.

![Figure 2 Functional interactions](https://upload-images.jianshu.io/upload_images/17534427-183378c230bd0252.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### Interfaces between modules during a life-circle
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

### External-interfaces
The external interfaces provided by Scrapy mainly concern functionality to extension development possible.  There are too many interfaces to completely list them in this report, so for a full list of available external interface refer to the ```setting.py```.

The infrastructure of the settings provides a global namespace of key-value mappings that the code can use to pull configuration values from. The settings can be populated through different mechanisms, which are described below.<a href="#ref_dev_8">[10]</a>

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

## Performance-Perspective
When programers first start to learn the crawler frame, they always care about the speed of the frame. But later, they will learn that the
speed of your crawler depends on a lot of thing, such as your anti-anti-crawler skill,the arrangement of your crawlers, the read/write speed
of your database,etc. So its hard to evaluate the performance of a crawler frame.
In the following part, we will discuss the speed performance of Scrapy and then we will compare some famous frames.
### Understand the performance of scrapy
[![Kg4YBn.png](https://s2.ax1x.com/2019/10/28/Kg4YBn.png)](https://imgchr.com/i/Kg4YBn)
This is the performance model of scrapy.It has four parts:scheduler,throttler,downloader and scraper.
- Scraper:A large number of requests are queued here until the downloader processes them. Most of these are urls and are therefore small, meaning that even if a large number of requests exist, they can be processed by the downloader in a timely manner.
- Throttler:This is a safety valve for the crawler to feed back and forth, and if the response in the process is greater than 5MB, the blocker suspends more requests to the loader. This can cause fluctuations in performance.
- Downloader:This is the most important component for Scrapy's performance. It limits the number of concurrences with a complex mechanism. Its latency (pipeline length) is equal to the response time of the remote server, plus the network/operating system, Python/Twisted latency. We can adjust the number of concurrent requests, but not the other delays. The capabilities of the downloaders are limited by the CONCURRENT_REQUESTS* setting.
- Scraper:This is the component of the grab that turns Response into an Item and other requests. As long as we follow the rules to write the crawler, it's usually not a bottleneck.

As we can see, the Downloader is the narrowest part of the whole program.So when we talk about the speed of Scrapy, the setting of the Downloader will play the most important part.

![KgThdA.png](https://s2.ax1x.com/2019/10/28/KgThdA.png)

### Compare to other frame
 name | language | Pluges | distributed? | js? | Others 
 ---- | -------- | ------ | ------------ | --- | ------
 Nutch | Java | hard to develop,even change the frame | support | support | specially for search engine 
 Crawler4j | Java | no | no | no | used in easy project
 WebCollector | Java | easy to develop | no | no | based on Scrapy
 Scrapy | Python | easy to develop | able to support | no | modelarization,good Scalability
 pyspider | Python | no | support | support | Strong ability to arrange crawlers
 
 As the table shows, Scrapy is good at Scalability and can be develop to adapt to different conditions.In this way, we can say that Scrapy gives the best performance.<a href="#ref_dev_9">[11]</a>
 
 ## Technical-Debt

>   Technical debt (also known as design debt or code debt) is a concept in software development that reflects the implied cost of additional rework caused by choosing an easy solution now instead of using a better approach that would take longer.

This part will focuse on some long-trem impacts of trade-offs that are taken during the software development between development and maintainability of Scrapy. The definition of techchnical debt is shown above. <a href="#ref_dev_10">[12]</a>

### Analysis-Tools

In order to understand the current state of technical debt in Scrapy, some code analysis tools are needed to perform some analysis. The language used by Scrapy is Python. The code analysis tools of the Python language are various and their respective biases are different. Some of the best-performing code analysis tools are available for a fee. Due to cost constraints, we are limited to open source code analysis tools that are feature-rich and perform well.

After our screening, we chose PyLint's code analysis tool as our analysis tool. However, this open source software has its own problem, that is, there is no good graphical interface, and the analysis process is carried out on the command line.

In order to make the results more intuitive, we have been searching for and found the CodeFactor website. The underlying code analysis of this website is implemented by PyLint, and has a good graphical interface, which can intuitively feedback the results of code analysis.

And the tool analyzes all project files separately and provides a rating (from A to F) for each file. Code complexity, code issues, and code replication are examples of metrics. This cloud-based analysis tool is easy to implement.

### Code-Analysis

![CodeFactor](https://www.codefactor.io/repository/github/scrapy/scrapy/badge)

Based on the overall rating of the project given by CodeFactor, Scrapy received an A-level rating in the evaluation. This means that Scrapy's overall code structure is good, no serious problems, and one of the best software in the code analysis of various software.

However, as an analysis of technical debt, we can't just stay on the overview of the code as a whole. Next, we will analyze the parts of the code, especially some of the problems.

CodeFactor mainly analyzes the code from Complexity, Style, Compatibility, Performance, Maintainability and so on. The following table is the type of problem and the number of problems in Scrapy given by CodeFactor. It should be noted that in the Maintainability of the table, I only select the issue with the number of occurrences greater than or equal to three times.

Complexity `1`    | Maintainability `171`                       | Security `31`
------------------|---------------------------------------------|---------------
Complex Method `1`| Redefining built-in `41`                    | Use of insecure MD2, MD4 or MD5 hash function `9`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Unnecessary else after return `38`          | Use of insecure lxml.etree module `6`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Unresolved warning comment `21`             | Use of eval() `5`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Trailing newline `21`                       | Use of possibly insecure marshal module `2`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Multiple statements in one line `14`        | Starting a process with a shell `2`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Use of bare except `6`                      | Use of insecure SSL/TLS as method parameter value `2`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Pointless statement `5`                     | Use of hard-coded password strings `1`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Use of len(sequence) as condition value `4` | Use of possibly insecure ftplib module `1`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Unbalanced tuple unpacking `3`              | Possible binding to all interfaces `1`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Lost exception `3`                          | A pass in the except block `1`
ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ| Unidiomatic type check `3`                  | Use of insecure mktemp() function `1`

*Table 1: Issues that affect Scrapy in CodeFactor*

From the above table, it can be seen that Scrapy's code does have fewer problems overall. As with CodeFactor's rating, Scrapy has one issue for Complexity in code analysis, 171 for Maintainability, and 31 for Security. Compared with some other open source projects, the types of issues are significantly less, and the number of issues under each type of issue is significantly less than that of open source projects of the same level.

Since Scrapy is a very active open source project and is organized and maintained by ScrapingHub, it can be seen that Scrapy's overall technical debt is less, and the overall code update is more timely. With the joint efforts of many parties, the current good state has been achieved.

### Evaluation

#### Evaluation by Category

First we will continue to analyze the various issues given by CodeFactor in the code analysis of the Scrapy project.

From the quantitative analysis, the issue of Maintainability is undoubtedly the part of the technical debt. Sorting according to the number of occurrences in Maintainability, we will focus on the first three issues for specific analysis.

-   Redefining built-in
    
    We first need to understand the specific meaning of this issue. Redefining built-in is a variable or function overrides a built-in. Overloading function names can make code hard to maintain and hard to read, and can cause subtle bugs when the wrong function is called.

    The solution to this type of issue is to try to rename user-defined function to a name that is not a built-in function. But as we know, such problems are easy to solve, but the difficulty is to find it. When we implement certain features, we sometimes redefine these functions to achieve our goals faster. Although this will bring possible future errors, it will increase efficiency. As an open source software, it is difficult for us to ask for perfection in this area, because it is almost impossible to have someone to carry out this maintenance.

-   Unnecessary else after return
    
    Unnecessary else after return is used in order to highlight an unnecessary block of code following an if containing a return statement. As such, it will warn when it encounters an else following a chain of ifs, all of them containing a return statement. 

    This type of issue is obviously a question of the programming habits of the developer during the development process. And according to the situation of the commit, it can be seen that the generation of such an issue is caused by one of the developers. So we can think that this kind of technical debt is caused by some developers' programming habits.

-   Unresolved warning comment
    
    Unresolved warning comment is used as a warning note when FIXME or XXX is detected. Such issues are not caused by objective factors (programming habits, etc.). It is the function that the developer himself needs to fix during the development process. There are two possibilities for this type of issue. The first is that the developer has fixed the problem but forgot to cancel the logo. The second possibility is that the issue has not been resolved due to lower priority.

    Because Scrapy is an open source software that is still active today and its history has been around for many years. We can think that there are no problems caused by stopping maintenance. It is worth mentioning that the commit in this type of problem can even follow up to a decade ago, which further reflects the Scrapy technical debt for a long time.

#### Evaluation by Time

After analyzing the types of issues that have occurred the most, we will analyze the time of the issue. It is very surprising that the issue of the last possible problem has been around for a year, in other words, the update in the past year will not cause technical debt problems.

We selected the time of the last ten issue changes and the increase and decrease of the issue. We will try to analyze Scrapy's technical debt from the dimension of time.

Date       | New Issue | Fixed Issue
-----------|-----------|---------------
2018-08-15 | 1         | 2
2018-08-12 | 1         | 0
2018-07-25 | 1         | 1
2018-07-25 | 1         | 0
2018-07-11 | 1         | 1
2018-07-11 | 0         | 8
2018-07-06 | 1         | 56
2018-07-03 | 3         | 10
2018-07-03 | 1         | 3
2018-06-14 | 2         | 0

*Table 2: Recent Issue Change Situation*

From the table we can clearly see that Scrapy's code has been maintained at a relatively good level and there is a reason for less technical debt.

First of all, we can find that the frequency of the issue is not high. The above table only selects the commit that generated the issue, but in fact, such commits account for less than half of all commits.

The second point is obvious. The Scrapy development team consciously fixes the issue and fixes the issue in batches over a certain period of time. This conscious maintenance has further reduced Scrapy's technical debt, keeping its code at an excellent level.

The third point is that according to the commit of the past year, there is no issue. We can guess that Scrapy may analyze the code and modify the possible issue before submitting the commit. This approach significantly reduces Scrapy's technical debt.

In general, Scrapy is almost unbelievable in terms of technical debt, which is very good, regardless of the type and number of issues that occur. We believe this is due to the Scrapy development team's emphasis on technical debt and ongoing repairs. This is a point worth learning for other open source software.

## Evolution
Since the version updates of Scrapy are fairly frequent, we only captures the latest releases to help us to gain a deeper understanding of the architecture and design of Scrapy.

### The latest vision 
##### 1.7.4(2019-10-21)
* Revert the fix for issue 3804 (issue 3819), which has a few undesired side effects (issue 3897, issue 3976).
##### 1.7.3(2019-08-01)
* Enforce lxml 4.3.5 or lower for Python 3.4 (issue 3912, issue 3918).
##### 1.7.2(2019-07-23)
* Fix Python 2 support (issue 3889, issue 3893, issue 3896).
##### 1.7.1(2019-07-18)
* Re-packaging of Scrapy 1.7.0, which was missing some changes in PyPI.
##### 1.7.0(2019-07-18)
* Improvements for crawls targeting multiple domains
* A cleaner way to pass arguments to callbacks
* A new class for JSON requests
* Improvements for rule-based spiders
* New features for feed exports
#####1.6.0 (2019-01-30)
* better Windows support
* Python 3.7 compatibility
* big documentation improvements, including a switch from .extract_first() + .extract() API to .get() + .getall() API
* feed exports, FilePipeline and MediaPipeline improvements
* better extensibility: item_error and request_reached_downloader signals; from_crawler support for feed exporters, feed storages and dupefilters
* scrapy.contracts fixes and new features
* telnet console security improvements, first released as a backport in Scrapy 1.5.2 (2019-01-22)
* clean-up of the deprecated code
* various bug fixes, small new features and usability improvements across the codebase

The most attractive thing about Scrapy is that it's a framework that anyone can easily adapt to their needs.With  the contribution of both the developers, it becomes the most commonly used spider framework in the Python world.
Scrapy was originally designed for web scraping. With the update of versions, now it can also be used to extract data using APIs (such as Amazon Associates Web Services) or as a general purpose web crawler.It also provides base classes for various types of crawlers, such as BaseSpider, sitemap crawlers, etc.


## References

<a name="ref_sta1">[1]</a>Wikipedia. Stakeholder (corporate)[EB/OL］.Stakeholder (corporate) - Wikipedia，https://en.wikipedia.org/wiki/Stakeholder_(corporate)

<a name="ref_con1">[2]</a>[https://scrapy.org/](https://scrapy.org/)

<a name="ref_dev_1">[3]</a>[https://docs.scrapy.org/en/latest/](https://docs.scrapy.org/en/latest/)

<a name="ref_dev_2">[4]</a>[https://www.cnblogs.com/jclian91/p/9799697.html](https://www.cnblogs.com/jclian91/p/9799697.html)

<a name="ref_dev_3">[5]</a>[https://docs.scrapy.org/en/latest/topics/shell.html#topics-shell](https://docs.scrapy.org/en/latest/topics/shell.html#topics-shell)

<a name="ref_dev_4">[6]</a>[https://www.cnblogs.com/xieqiankun/p/know_middleware_of_scrapy_1.html](https://www.cnblogs.com/xieqiankun/p/know_middleware_of_scrapy_1.html)

<a name="ref_dev_5">[7]</a>[https://docs.scrapy.org/en/latest/topics/architecture.html](https://docs.scrapy.org/en/latest/topics/architecture.html)

<a name="ref_dev_6">[8]</a>Nick Rozanski and Eoin Woods. Software System Architecture: Working With Stakeholders Using Viewpoints and Perspectives. Addison-Wesley, 2012.

<a name="ref_dev_7">[9]</a>Nick Rozanski and Eoin Woods. Software Systems Architecture: Working with Stakeholders using Viewpoints and Perspectives. Addison-Wesley, 2012.

<a name="ref_dev_8">[10]</a>[https://docs.scrapy.org/en/latest/topics/settings.html(https://docs.scrapy.org/en/latest/topics/settings.html

<a name="ref_dev_9">[11]</a>《Learning Scrapy》

<a name="ref_dev_10">[12]</a>Wikipedia. Technical debt [EB/OL］.Technical debt - Wikipedia，https://en.wikipedia.org/wiki/Technical_debt

## Performance perspective
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
| name | language | Pluges | difficulty | distributed? | crawl js? | Others |
|--------------------|--------------------|
| Nutch | Java | hard to develop,even change the frame | hard | support | support | specially for search engine |

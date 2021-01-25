# 目录
<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
[TOC]
<!--ts-->
* [目录](#目录)
* [基础](#基础)
   * [初步使用scrapy](#初步使用scrapy)
* [爬虫spider](#爬虫spider)
* [#](#)
* [爬虫库](#爬虫库)
<!--te-->

----

# 基础

## 初步使用scrapy

爬取知乎【根话题】-精华中的1000个问题题目以及优质回答者的名字、赞数和评论数


第一步，创建项目

`scrapy startproject ArticleSpider`

第二步，进入项目根目录，建立爬虫

`cd ArticleSpider`

`scrapy genspider zhihu www.zhihu.com`


第三步，编写爬虫

```python
# ArticleSpider/ArticleSpider/spiders/zhihu.py
import scrapy
import json
import time
import random
from ArticleSpider.items import ArticlespiderItem


class ZhihuSpider(scrapy.Spider):
    name = 'zhihu'
    allowed_domains = ['www.zhihu.com']
    start_urls = ['https://www.zhihu.com/']
    top_answers_url_prefix = "https://www.zhihu.com/api/v4/topics/19776749/feeds/essence?include=data%5B%3F%28target.type%3Dtopic_sticky_module%29%5D.target.data%5B%3F%28target.type%3Danswer%29%5D.target.content%2Crelationship.is_authorized%2Cis_author%2Cvoting%2Cis_thanked%2Cis_nothelp%3Bdata%5B%3F%28target.type%3Dtopic_sticky_module%29%5D.target.data%5B%3F%28target.type%3Danswer%29%5D.target.is_normal%2Ccomment_count%2Cvoteup_count%2Ccontent%2Crelevant_info%2Cexcerpt.author.badge%5B%3F%28type%3Dbest_answerer%29%5D.topics%3Bdata%5B%3F%28target.type%3Dtopic_sticky_module%29%5D.target.data%5B%3F%28target.type%3Darticle%29%5D.target.content%2Cvoteup_count%2Ccomment_count%2Cvoting%2Cauthor.badge%5B%3F%28type%3Dbest_answerer%29%5D.topics%3Bdata%5B%3F%28target.type%3Dtopic_sticky_module%29%5D.target.data%5B%3F%28target.type%3Dpeople%29%5D.target.answer_count%2Carticles_count%2Cgender%2Cfollower_count%2Cis_followed%2Cis_following%2Cbadge%5B%3F%28type%3Dbest_answerer%29%5D.topics%3Bdata%5B%3F%28target.type%3Danswer%29%5D.target.annotation_detail%2Ccontent%2Chermes_label%2Cis_labeled%2Crelationship.is_authorized%2Cis_author%2Cvoting%2Cis_thanked%2Cis_nothelp%3Bdata%5B%3F%28target.type%3Danswer%29%5D.target.author.badge%5B%3F%28type%3Dbest_answerer%29%5D.topics%3Bdata%5B%3F%28target.type%3Darticle%29%5D.target.annotation_detail%2Ccontent%2Chermes_label%2Cis_labeled%2Cauthor.badge%5B%3F%28type%3Dbest_answerer%29%5D.topics%3Bdata%5B%3F%28target.type%3Dquestion%29%5D.target.annotation_detail%2Ccomment_count%3B"
    limit = 10
    offset = 0

    headers = {
        "Referer": "https://www.zhihu.com",
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.117 Safari/537.36",
    }

    # 请填写自己账号cookies
    cookies = {
        "_zap": "",
        "d_c0": "",
        "_xsrf": "",
        "tst": "",
        "Hm_lvt_98beee57fd2ef70ccdd5ca52b9740c49": "",
        "capsion_ticket": "",
        "z_c0": "",
        "Hm_lpvt_98beee57fd2ef70ccdd5ca52b9740c49": "",
        "KLBRSID": ""
    }

    def start_requests(self):
        url = self.top_answers_url_prefix + "&limit={}&offset={}".format(self.limit, self.offset)
        self.offset += self.limit
        return [scrapy.Request(url, dont_filter=True, headers=self.headers, cookies=self.cookies)]

    def parse(self, response):
    	# 获得问题，最佳回答的作者、赞数和评论数
        body = json.loads(response.body)
        for data in body["data"]:
            item = ArticlespiderItem()
            target = data["target"]
            item["question"] = target["question"]["title"]  # 问题
            item["name"] = target["author"]["name"] # 优质回答者名字
            item["voteup_count"] = target["voteup_count"]  # 赞数
            item["comment_count"] = target["comment_count"] #评论数
            yield item

        url = self.top_answers_url_prefix + "&limit={}&offset={}".format(self.limit, self.offset)
        self.offset += self.limit

        if body["data"]:
            time.sleep(random.randint(1,20) / 10)
            yield scrapy.Request(url, self.parse)
```

第四步，编写item

```python
# ArticleSpider/ArticleSpider/items.py

class ArticlespiderItem(scrapy.Item):
    # define the fields for your item here like:
    question = scrapy.Field()         # 问题
    name = scrapy.Field()             # 优质回答作者
    voteup_count = scrapy.Field()     # 投票数
    comment_count = scrapy.Field()    # 赞数

```

第五步，修改配置

```python
# ArticleSpider/ArticleSpider/settings.py

ROBOTSTXT_OBEY = False    # 必须改成False，不然很多网站会阻止爬虫爬取
FEED_EXPORT_ENCODING = "utf-8"  # 修改编码格式，不然输出的中文有问题
COOKIES_ENABLED = True    # 必须修改成True，不然自己账号的cookies无法自动添加到每次request请求中

```

第六步，执行爬虫

`scrapy crawl zhihu -o zhihu_jinghua.json`




----

# 爬虫spider

## 


----

# 爬虫库

* [awesome-spider](https://github.com/facert/awesome-spider): 这一款爬虫，里面搜集了几乎所有可以爬取的中文网址，从知乎豆瓣到知网，抖音微博到QQ，还有很多的不可描述的网站，你懂的。
* [Nyspider](https://github.com/Nyloner/Nyspider): 可以看出，都是各类网址。这很头条，跟这位小哥哥的工作内容估计有关系。
* [awesome-python-login-model](https://github.com/CriseLYJ/awesome-python-login-model): 这个项目用于模拟各种网址登陆，也包含一些简单的爬虫
* [python-spider](https://github.com/Jack-Cherish/python-spider): 这是ID为Jack-Cherish的东北大学的一个学生整理的学习python爬虫的资料，star6000+，包含不少的实战项目，非常适合想学习的朋友。
* [Google，Baidu，Bing三大搜素引擎图片爬虫](https://github.com/sczhengyabin/Image-Downloader): 这个爬虫由ID为sczhengyabin的用户整理，可以按要求爬取百度、Bing、Google上的图片
* [各大视频网站爬虫](https://github.com/iawia002/annie): Annie是一款以go语言编码的视频下载工具，使用便捷并支持youtube，腾讯视频，抖音等多个网站视频和图像的下载
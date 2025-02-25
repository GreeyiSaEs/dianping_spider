
### 计划支持(最近几个月很忙，可能没办法更新，周末如果有空可能会更新)

- cookie动态更新（有可能缓解被ban的情况）

- 优惠券信息

## 环境配置
语言：python3

系统：Windows/Linux/MacOS

其他环境配置：

需要：lxml、requests、tqdm、faker、beautifulsoup4、fontTools、pymongo

或者一键配置：

    pip install -r requirements.txt

## 使用方法：


### 配置配置文件
首先配置config.ini，参数意义在文件内已经有了详细说明，这里进行简单说明。



|参数|说明|
|:-----  |-----|
|config：      |  |
|use_cookie_pool      |是否使用cookie池 |
|Cookie      |Cookie信息（注意大写，之所以不一样是方便将浏览器信息直接复制进去而不做更改）。|
|uuid      |uuid信息，[详见](./docs/json.md)|
|tcv      |tcv信息，[详见](./docs/json.md)|
|user-agent      |浏览器UA信息，和配置文件中说明不同的是，目前暂时不支持随机UA|
|save_mode      |保存方式，具体格式参照config.ini提示。（目前只能为mongo/mongodb） |
|mongo_path      |mongo数据库配置，具体格式参照config.ini提示|
|requests_times      |爬虫间隔时间，具体格式参照config.ini提示。  |
|detail：      |  |
|keyword      | 搜索关键字 |
|location_id      |地区id，具体格式参照config.ini提示。 [详见](./docs/location.md )  |
|channel_id      |频道id，具体格式参照config.ini提示。  |
|search_url      |搜索url，详见config.ini内提示。  |
|need_first      |是否只需要首页首条  |
|need_pages      |需要搜索的页数（搜索页）  |
|proxy:      |  |
|use_proxy |是否使用代理 |
|repeat_nub |ip重复次数，详见config.ini |
|http_extract |http提取 |
|key_extract |秘钥提取 |
|http_link |http提取接口 |
|proxy_host |秘钥模式服务器ip |
|proxy_port |秘钥模式服务器端口 |
|key_id |秘钥id |
|key_key |秘钥key |

然后配置require.ini，该配置文件用于选择爬取策略。

|参数|说明|谨慎选择|
|:-----  |-----|-----|
|shop_phone：      |  | |
|need      |是否需要店铺电话 |否|
|need_detail   |是否需要店铺电话细节（不需要为 12345678** ，需要详情为 12345678910） |是|
|shop_review：      |  | |
|need      |是否需要店铺评论 |否|
|need_detail   |是否需要店铺更多评论 （不需要则只有10条精选） |是|
|need_pages   |如果需要更多评论，需要多少页（一页30条），取店家评论页和输入值的较小值 |否|

值得一提的是，对于谨慎选择的配置，由于需要登录才能获取，
因此请求会携带cookie，频繁请求会造成封号（过段时间自动解开）。

### 运行程序

正常搜索（完整流程，搜索->详情[可选]->评论[可选]）：
- 运行main.py

定制化搜索（不需要搜索，只需要详情或评论）:
- 只需要详情,shop_id 自行修改 （只给命令行格式，编译器运行则自行配置或修改代码）

    `python main.py --normal 0 --detail 1 --review 0  --shop_id k30YbaScPKFS0hfP --need_more False` 

- 只需要评论 

    `python main.py --normal 0 --detail 0 --review 1 --shop_id k30YbaScPKFS0hfP --need_more False`

- 需要详情和评论

    `python main.py --normal 0  --detail 1 --review 1  --shop_id k30YbaScPKFS0hfP --need_more False`
    
如果遇到其他问题，详见[这里](./docs/problems.md)
和[issues](https://github.com/Sniper970119/dianping_spider/issues?q=is%3Aissue+is%3Aclosed)

 
## 字段结果展示

由于大众点评反扒措施相对严重以及不同频道字段格式复杂，因此很多数据在爬取阶段不做处理。原样保存，后续自行清洗。
（新版本由于引入接口数据，有些数据为了对齐接口存储格式不得不进行处理）


### 商家搜索结果展示：
![image](./imgs/show_info.jpg)

### 商家评论页展示：
![image](./imgs/show_review.jpg)


更多数据规约查看[这里](./docs/data.md)

## 一些碎碎念


关于cookie以及cookie池的一些碎碎念：[这里](./docs/cookie_pool.md)

关于存储的一些碎碎念：[这里](./docs/save.md)

关于使用加密接口的一些碎碎念：[这里](./docs/json.md)

关于ip代理的一些碎碎念：[这里](./docs/proxy.md)

一些可能遇到的小问题：[这里](./docs/problems.md)


  
## 相关功能笔记
  - [搜索页字体加密加密](http://www.sniper97.cn/index.php/note/carwler/3694/)
  - [评论页字体加密加密](http://www.sniper97.cn/index.php/note/carwler/3707/)

如果你想加快进度，点个star吧呜呜呜

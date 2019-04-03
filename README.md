## Scrapy-Zhihu项目结构介绍

captcha: 存放知乎登录页面英文验证码或倒立文字验证码图片

cookies: 存放登录之后获取到的cookies

failed_urls: 存放爬取失败的url信息

libs：存放Scrapy编写过程中需要用到的函数

libs.bloomfilter: 布隆过滤器，对url进行去重

libs.chaojiying: 英文验证码识别

libs.common: 其他函数

libs.proxy: 获取西刺ip代理

spiders: 项目文件

zheye: 倒立文字验证码识别相关文件

## Scrapy-Zhihu重要方法介绍

spiders.zhihu.py:
start_requests: 重写start_requests方法， 模拟登录知乎

get_cookies：模拟登录知乎，将登录后的cookies写入文件中，并返回登录之后的cookies

deal_with_chinese_captcha: 倒立验证码的识别

deal_with_english_captcha: 英文验证码的识别

middlewares.RedirectDealDownloaderMiddleware.process_response: 处理302重定向到登录页面问题

## 如何使用
### 安装依赖
```
git clone https://github.com/Yanxueshan/Scrapy-Zhihu.git
cd Scrapy-Zhihu
pip install -r requirements.txt
```

### 参数修改
settings.py中的某些参数需要修改

这是数据库MySQL相关配置，修改为自己的MySQL配置
```
MYSQL_HOST = 'localhost'
MYSQL_DBNAME = 'zhihu'
MYSQL_USER = 'root'
MYSQL_PASSWORD = 'root'
```

这是知乎的账号和密码，供模拟登录使用，修改为自己的知乎账号和密码
```
ZHIHU_ACCOUNT = 'username'
ZHIHU_PASSWORD = 'password'
```

这是超级鹰的账号，用来识别英文验证码，修改为自己的超级鹰账号（也可以换成其他第三方平台，不过相应的zhihu.py中的代码要改变）
```
CHAOJIYING_ACCOUNT = 'username'
CHAOJIYING_PASSWORD = 'password'
CAPTCHA_TYPE = '898966'
```

### 运行前准备
切换到redis安装目录下，启动redis-server
```
cd redis
redis-server.exe redis.windows.conf
```
另起一个窗口，启动redis-cli
```
cd redis
redis-cli
```

### 运行
```
redis-cli lpush zhihu:start_urls http://www.zhihu.com/signin
cd Scrapy-Zhihu
python main.py
```


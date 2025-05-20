<p align="center"> <img src="https://raw.githubusercontent.com/qeeqbox/social-analyzer/main/readme/socialanalyzerlogo_.png"></p>

Social Analyzer - 用于分析和查找某人在 +1000 个社交媒体/网站上的个人资料的 API、CLI 和 Web 应用程序。 它包括不同的分析和检测模块，您可以在调查过程中选择使用哪些模块。

检测模块利用基于不同检测技术的评分机制，产生从 0 到 100（否-可能-是）的评分值。该模块旨在减少误报。

来自此 OSINT 工具的分析和公共提取信息可以帮助调查与可疑或恶意活动（如网络欺凌、网络诱骗、网络跟踪和传播虚假信息）相关的个人资料。

`该项目目前被一些资源有限的执法机构使用 - 检测数据库与此处共享的数据库不同..`

## 社·交·媒·体
允许用户创建和共享内容或参与社交网络的网站和应用程序 - 牛津词典

## 结构
<img src="https://raw.githubusercontent.com/qeeqbox/social-analyzer/main/readme/structure.png">


## APP（首选！）
标准 localhost WEB APP url: http://0.0.0.0:9005/app.html

<img src="https://raw.githubusercontent.com/qeeqbox/social-analyzer/main/readme/intro_fast.gif" style="max-width:768px"/>

## CLI
<img src="https://raw.githubusercontent.com/qeeqbox/social-analyzer/main/readme/cli.gif" style="max-width:768px"/>

## 特点
- 字符串和名称分析（排列组合）
- 使用多种技术查找个人资料（HTTPS 库和 Webdriver）
- 多个人资料搜索（用于关联 - 任何用“,”分隔的组合）
- 多层检测（OCR、普通、高级和特殊）
- 使用 Ixora 可视化个人资料信息（元数据和模式）
- 元数据和模式提取（从 Qeeqbox OSINT 项目添加）
- 用于元数据的力导向图（需要 ExtractPatterns）
- 按排名靠前或按国家/地区搜索（Alexa 排名）
- 按类型搜索（成人、音乐等 - 自动网站统计）
- 个人资料统计信息和静态信息（类别国家/地区）
- 交叉元数据统计信息（从 Qeeqbox OSINT 项目添加）
- 自动过滤不必要的输出（启用 javascript 等）
- 搜索引擎查找（Google API - 可选）
- 自定义搜索查询（Google API 和 DuckDuckGo API - 可选）
- 个人资料屏幕截图、标题、信息和网站描述
- 按语言查找姓名起源、姓名相似性和常用词
- 查找可能的个人资料/个人年龄（有限分析）
- 自定义 user-agent、代理、超时和隐式等待
- Python CLI 和 NodeJS CLI（仅限于 FindUserProfilesFast 选项）
- 检测到的个人资料的屏幕截图（必须安装最新版本的 Chrome）
- 用于更快检查的网格选项（仅限于 docker-compose）
- 将日志转储到文件夹或终端（美化）
- 调整查找/获取个人资料工作线程（默认 15）
- 用于失败个人资料的重新检查选项
- 按好、可能和坏过滤个人资料
- 将分析保存为 JSON 文件
- 简化的 Web 界面和 CLI
- 还有更多！！

## 特殊检测
- Facebook（电话号码、姓名或个人资料名称）
- Gmail（example@gmail.com）
- Google（example@example.com）

## 安装和运行
### Linux（作为 Node WebApp）
```bash
sudo apt-get update
#取决于您的 Linux 发行版，您可能不需要这两行
sudo DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common
sudo add-apt-repository ppa:mozillateam/ppa -y
sudo apt-get install -y firefox-esr tesseract-ocr git nodejs npm
git clone https://github.com/qeeqbox/social-analyzer.git
cd social-analyzer
npm update
npm install
npm start
```

### Linux（作为 Node CLI）
```bash
sudo apt-get update
#取决于您的 Linux 发行版，您可能不需要这两行
sudo DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common
sudo add-apt-repository ppa:mozillateam/ppa -y
sudo apt-get install -y firefox-esr tesseract-ocr git nodejs npm
git clone https://github.com/qeeqbox/social-analyzer.git
cd social-analyzer
npm install
nodejs app.js --username "johndoe"
#或者
nodejs app.js --username "johndoe,janedoe" --metadata
#或者
nodejs app.js --username "johndoe,janedoe" --metadata --top 100
#或者
nodejs app.js --username "johndoe" --type "adult"
```

### Linux（作为 python 包）
```bash
sudo apt-get update
sudo apt-get install python3 python3-pip
pip3 install social-analyzer
python3 -m social-analyzer --username "johndoe"
#或者
python3 -m social-analyzer --username "johndoe" --metadata
#或者
python3 -m social-analyzer --username "johndoe" --metadata --top 100
#或者
python3 -m social-analyzer --username "johndoe" --type "adult"
#或者
python3 -m social-analyzer --username "johndoe" --websites "car" --logs --screenshots
```

### Linux（作为 python 脚本）
```bash
sudo apt-get update
sudo apt-get install git python3 python3-pip
git clone https://github.com/qeeqbox/social-analyzer
cd social-analyzer
pip3 install -r requirements.txt
python3 app.py --username "janedoe"
#或者
python3 app.py --username "johndoe" --metadata
#或者
python3 app.py --username "johndoe" --metadata --top 100
#或者
python3 app.py --username "johndoe" --type "adult"
#或者
python3 app.py --username "johndoe" --websites "car" --logs --screenshots
```

### 作为对象导入 (python)
```python

#例如 #1
from importlib import import_module
SocialAnalyzer = import_module("social-analyzer").SocialAnalyzer()
results = SocialAnalyzer.run_as_object(username="johndoe",silent=True)
print(results)

#例如 #2
from importlib import import_module
SocialAnalyzer = import_module("social-analyzer").SocialAnalyzer()
results = SocialAnalyzer.run_as_object(username="johndoe,janedoe",silent=True,output="json",filter="good",metadata=False,timeout=10, profiles="detected")
print(results)
```

### Linux, Windows, MacOS, Raspberry pi..
- 查看此 [wiki](https://github.com/qeeqbox/social-analyzer/wiki/install) 了解所有可能的安装方法
- 查看此 [wiki](https://github.com/qeeqbox/social-analyzer/wiki/integration) 了解如何将 social-analyzer 与您的 OSINT 工具、feeds 等集成...

## social-analyzer --h
```
必需参数：
  --username   例如 johndoe, john_doe 或 johndoe9999

可选参数：
  --websites    一个或多个网站，用空格分隔，例如 youtube, tiktokor tumblr
  --mode        分析模式 例如 fast -> FindUserProfilesFast, slow -> FindUserProfilesSlow 或 special -> FindUserProfilesSpecial
  --output      以以下格式显示输出：json -> json 输出用于集成或 pretty -> 美化输出
  --options     当找到个人资料时显示以下内容：link, rate, titleor text
  --method      find -> 显示检测到的个人资料, get -> 显示所有个人资料，无论是否检测到, all -> 组合 find & get
  --filter      按好、可能或坏过滤检测到的个人资料，您可以使用逗号组合它们 (good,bad) 或使用 all
  --profiles    按检测到的、未知的或失败的过滤个人资料，您可以使用逗号组合它们 (detected,failed) 或使用 all
  --countries   按国家/地区或多个国家/地区选择网站，用空格分隔，例如：us br ru
  --type        按类型选择网站 (Adult, Music 等)
  --top         选择排名靠前的网站，如 10, 50 等...[--websites 不是必需的]
  --extract     如果可能，提取个人资料、网址和模式
  --metadata    如果可能，提取元数据 (pypi QeeqBox OSINT)
  --trim        修剪长字符串
  --gui         保留给 gui（未实现）
  --cli         保留给 cli（不需要）

列出网站和检测：
  --list        列出所有可用的网站

设置：
  --headers     标头作为字典
  --logs_dir    更改日志目录
  --timeout     更改每个请求之间的超时
  --silent      禁用屏幕输出
```

## 打开 Shell
[![Open in Cloud Shell](https://img.shields.io/static/v1?label=%3E_&message=Open%20in%20Cloud%20Shell&color=3267d6&style=flat-square)](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/qeeqbox/social-analyzer&tutorial=README.md) [![Open in repl.it Shell](https://img.shields.io/static/v1?label=%3E_&message=Open%20in%20repl.it%20Shell&color=606c74&style=flat-square)](https://repl.it/github/qeeqbox/social-analyzer)

## 资源
- DuckDuckGo API, Google API, NodeJS, bootstrap, selectize, jQuery, Wikipedia, font-awesome, selenium-webdriver & tesseract.js
- 如果我遗漏了任何参考或资源，请告诉我！

## 免责声明/注意事项
- 从 GitHub 下载此项目并将其视为安全项目
- 如果您希望将您的网站从该项目列表中排除，请与我联系
- 此工具旨在在本地使用，而不是作为服务使用（它没有任何访问控制）
- 对于与以 -private 结尾或位于 private 组下的模块相关的问题 ![](https://raw.githubusercontent.com/qeeqbox/social-analyzer/main/readme/modules.png)，请直接与我联系（不要在 GitHub 上提出问题）

## 其他项目
[![](https://github.com/qeeqbox/.github/blob/main/data/analyzer.png)](https://github.com/qeeqbox/analyzer) [![](https://github.com/qeeqbox/.github/blob/main/data/chameleon.png)](https://github.com/qeeqbox/chameleon) [![](https://github.com/qeeqbox/.github/blob/main/data/honeypots.png)](https://github.com/qeeqbox/honeypots) [![](https://github.com/qeeqbox/.github/blob/main/data/osint.png)](https://github.com/qeeqbox/osint) [![](https://github.com/qeeqbox/.github/blob/main/data/url-sandbox.png)](https://github.com/qeeqbox/url-sandbox) [![](https://github.com/qeeqbox/.github/blob/main/data/mitre-visualizer.png)](https://github.com/qeeqbox/mitre-visualizer) [![](https://github.com/qeeqbox/.github/blob/main/data/woodpecker.png)](https://github.com/qeeqbox/woodpecker) [![](https://github.com/qeeqbox/.github/blob/main/data/docker-images.png)](https://github.com/qeeqbox/docker-images) [![](https://github.com/qeeqbox/.github/blob/main/data/seahorse.png)](https://github.com/qeeqbox/seahorse) [![](https://github.com/qeeqbox/.github/blob/main/data/rhino.png)](https://github.com/qeeqbox/rhino) [![](https://github.com/qeeqbox/.github/blob/main/data/raven.png)](https://github.com/qeeqbox/raven) [![](https://github.com/qeeqbox/.github/blob/main/data/image-analyzer.png)](https://github.com/qeeqbox/image-analyzer)

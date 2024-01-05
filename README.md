<h1 align="center" >Packer Fuzzer Plus</h1>

<h3 align="center" >一款针对Webpack等前端打包工具所构造的网站进行快速、高效安全检测的扫描工具</h3>

 <p align="center">
    <a href="https://github.com/rtcatc/Packer-Fuzzer"><img alt="Packer-Fuzzer" src="https://img.shields.io/badge/python-3.X-blueviolet"></a>
    <a href="https://github.com/rtcatc/Packer-Fuzzer"><img alt="Packer-Fuzzer" src="https://img.shields.io/badge/Version-1.4-red"></a>
    <a href="https://github.com/rtcatc/Packer-Fuzzer"><img alt="Packer-Fuzzer" src="https://img.shields.io/badge/LICENSE-GPL-ff69b4"></a>
    <a href="https://github.com/rtcatc/Packer-Fuzzer"><img alt="Packer-Fuzzer" src="https://img.shields.io/github/stars/rtcatc/Packer-Fuzzer.svg"></a>
    <a href="https://github.com/rtcatc/Packer-Fuzzer"><img alt="Packer-Fuzzer" src="https://img.shields.io/badge/Packer-Fuzzer-green"></a>
 </p>

##  👮🏻‍♀️ 免责声明&软件授权

由于传播、利用Packer Fuzzer Plus工具（下简称本工具）提供的检测功能而造成的**任何直接或者间接的后果及损失**，均由使用者本人负责，Packer Fuzzer开发团队（下简称本团队）**不为此承担任何责任**。

本工具会根据使用者检测结果**自动生成**扫描结果报告，本报告内容及其他衍生内容均**不能代表**本开发者的立场及观点。

请在使用本工具时遵循使用者以及目标系统所在国当地的**相关法律法规**，一切**未授权测试均是不被允许的**。若出现相关违法行为，我们将**保留追究**您法律责任的权利，并**全力配合**相关机构展开调查。

**Packer-Fuzzer-Plus授权声明**

**此软件：Packer-Fuzzer-Plus，加入专栏者有权进行二开用于个人使用。未经BigYoung书面授权，禁止直接用于商业用途及二开后用于商业用途，否则将承担相应的法律风险。**

## 🏝 介是个嘛

随着WEB前端打包工具的流行，您在日常渗透测试、安全服务中是否遇到越来越多以`Webpack打包器`为代表的网站？这类打包器会将整站的API和API参数打包在一起供Web集中调用，这也便于我们快速发现网站的功能和API清单，但往往这些打包器所生成的JS文件数量异常之多并且总JS代码量异常庞大（多达上万行），这给我们的手工测试带来了极大的不便，Packer Fuzzer Plus软件应运而生。

本工具支持自动模糊提取对应目标站点的API以及API对应的参数内容，并支持对：未授权访问、敏感信息泄露、CORS、SQL注入、水平越权、弱口令、任意文件上传七大漏洞进行模糊高效的快速检测。在扫描结束之后，本工具还支持自动生成扫描报告，您可以选择便于分析的HTML版本以及较为正规的doc、pdf、txt版本。

而且您完全不用担心因为国际化带来的语言问题，本工具附带五大主流语言语言包（包括报告模板）：简体中文、法语、西班牙语、英语、日语（根据翻译准确度排序），由我们非常~~不~~专业的团队翻译。

> 注：目前第一版工具只对Webpack打包器的规则做了优化，其他打包器规则敬请期待。



## 🎸 安装环境

1. 本工具使用Python3语言开发，在运行本工具之前请确保您装有`Python3.X`软件及`pip3`软件。若您未安装相关环境，可通过如下指引安装：[https://www.runoob.com/python3/python3-install.html](https://www.runoob.com/python3/python3-install.html)

   MacOS用户可使用如下命令快速安装：

   ```bash
   brew install python3 #会自动安装pip3
   ```

   Ubuntu用户可使用如下命令快速安装：

   ```bash
   sudo apt-get install -y python3 && sudo apt install -y python3-pip
   ```

   CentOS用户可使用如下命令快速安装：

   ```bash
   sudo yum -y install epel-release && sudo yum install python3 && yum install -y python3-setuptools && easy_install pip
   ```

2. 本工具将会通过`node_vm2`运行原生`NodeJS`代码，故我们推荐您安装`NodeJS`环境（不推荐其他JS运行环境，可能会导致解析失败）。若您未安装相关环境，可通过如下指引安装：[https://www.runoob.com/nodejs/nodejs-install-setup.html](https://www.runoob.com/nodejs/nodejs-install-setup.html)

   MacOS用户可使用如下命令快速安装：

   ```bash
   brew install node
   ```

   Ubuntu用户可使用如下命令快速安装：

   ```bash
   sudo apt-get install nodejs && sudo apt-get install npm
   ```

   CentOS用户可使用如下命令快速安装：

   ```bash
   sudo yum -y install nodejs
   ```

3. 请使用如下命令一键安装本工具所需要的Python运行库：

   ```bash
   pip3 install -r requirements.txt
   ```



## 🦁 参数介绍

您可以使用`python3 PackerFuzzer.py [options]`命令来运行本工具，`options`内容表述如下：

- -h（--help）

  帮助命令，无需附加参数，查看本工具支持的全部参数及其对应简介；

- -u（--url）

  要扫描的网站网址路径，为必填选项，例如：`-u https://demo.poc-sir.com`；

- -c（--cookie）

  附加cookies内容，可为空，若填写则将全局传入，例如：`-c "POC=666;SIR=233"`；

- -d（--head)

  附加HTTP头部内容，可为空，若填写则将全局传入，默认为`Cache-Control:no-cache`，例如：`-d "Token:3VHJ32HF0"`；

- -l（--lang）

  语言选项，当为空时自动选择系统对应语言选项，若无对应语言包则自动切换至英文界面。可供选择的语言包有：简体中文(zh)、法语(fr)、西班牙语(es)、英语(en)、日语(ja)，例如：`-l zh`；

- -t（--type）

  分为基础版和高级版，当为空时默认使用基础版。高级版将会对所有API进行重新扫描并模糊提取API对应的参数，并进行：SQL注入漏洞、水平越权漏洞、弱口令漏洞、任意文件上传漏洞的检测。可使用`adv`选项进入高级版，例如：`-t adv`；

- -p（--proxy）

  全局代理，可为空，若填写则全局使用代理IP，例如：`-p https://hack.cool:8080`；

- -j（--js）

  附加JS文件，可为空，当您认为还有其他JS文件需要本工具分析时，可使用此选项，例如：`-j https://demo.poc-sir.com/js/index.js,https://demo.poc-sir.com/js/vue.js`；

- -b（--base）

  指定API中间部分（例如某API为：https://demo.poc-sir.com/v1_api/login 时，则其basedir为：v1_api），可为空，当您认为本工具自动提取的basedir不准确时，可使用此选项，例如：`-b v1_api`；

- -r（--report）

  指定生成的报告格式，当为空时默认生成HTML和DOC格式的报告。可供选择的报告格式有：html、doc、pdf、txt，例如：`-r html,pdf`；

- -e（--ext）

  是否开启扩展插件选项，本工具支持用户自我编写插件并存入`ext`目录（如何编写请参考对应目录下`demo.py`文件）。默认为关闭状态，当用户使用`on`命令开启时，本工具将会自动执行对应目录下的插件，例如：`-e on`；

- -f（--flag）

  SSL连接安全选项，当为空时默认关闭状态，在此状态下将会阻止一切不安全的连接。若您希望忽略SSL安全状态，您可使用`1`命令开启，将会忽略一切证书错误，例如：`-f 1`；

- -s（--silent）

  静默选项，一旦开启则一切询问YES或NO的操作都将自动设置为YES，并且参数后的内容便是本次扫描报告的名称（自定义报告名），可用于无人值守、批量操作、插件调用等模式，例如：`-s Scan_Task_777`。

- --st（--sendtype）

  请求方式选项，目前本选项支持POST和GET参数，一旦开启则将会使用对应的请求方式扫描所有的API，若不开启将会通过HTTP状态码来进行智能请求。

- --ct（--contenttype）

  Content-Type选项，可通过此选项自定义扫描时的HTTP请求头中的Content-Type参数内容，若不开启将会通过HTTP状态码来进行智能请求。

- --pd（--postdata）

  POST内容选项，可通过此选项自定义扫描时的POST请求内容(所有的扫描都将会使用此内容，仅对POST场景有效)，若不开启将会通过HTTP状态码来进行智能请求。

- --ah（--apihost）

  Api域名选项，可通过此选项自定义扫描时所有的API请求域名，例如：api部分(从JS中提取到的API路径)为`/v1/info`，扫描的url(-u --url参数传入内容，扫描的网页)为`http://exp.com/`，当apihost参数传入`https://pocsir.com:777/`则此时的API为`https://pocsir.com:777/v1/info`而不是`http://exp.com/v1/info`，用于api与前端不同域名或服务器等场景。

- --fe（--fileext）

  Api扩展名选项，可通过此选项对所有API都添加特定的扩展名，以便应对在提取API时出现扩展名提取缺失的情况，例如：当提取到的API为`https://pocsir.com:777/v1/info`时，传入`--fe .json`则工具将会自动将API转化成`https://pocsir.com:777/v1/info.json`进行扫描及检测。

**以下参数是Packer-Fuzzer-Plus新增参数**
- --filepath 

  支持导入urls.txt文件中的数据，批量发起扫描，例如：`--filepath urls.txt`；

- --api

  是否导出API清单到json文件中，不使用参数，或这传递`1`代表导出，`0`代表不导出，例如：`--api 1`，代表导出API清单，默认只导出成功API，如果要导出所有API，修改config.ini [Export]的 status = 1

## 🎯 使用技巧

- 当您遇到假卡死或者扫描器因为意外的错误而被中断时，您无需过于担心。您可以直接在tmp目录下找到对应缓存文件夹内的以`.db`结尾的Sqlite数据库文件，当您打开之后您可以看见对应项目的所有实时结果均保存在此数据库内，您可以直接通过缓存数据库分析当前的扫描结果；
- 我们推荐您通过自定义`baseurl`的方式来提高API拼接成功率，减少发包次数。找寻`baseurl`并不难，您只需要在对应目标站点中触发任何一个API并稍加观察缺失部分即可快速寻找到；
- 我们不推荐您在较大、较复杂的站点中使用本工具的高级模式，因为在一些情况下高级模式会耗费异常大量的时间去不停地在后台做正则匹配，从而使本工具陷入假卡死的状态；
- 当您遇到A站点的API均在B站点时：您可以直接使用本工具的`--ah（--apihost）`命令来自定义API服务器地址；
- 当您遇到在Windows环境下无法创建、读取数据库时，您可以右键点击`使用管理员身份运行`。当您在Linux/Mac下时请也注意权限问题，推荐使用`sudo`命令。

## 👑 更新记录

> 重要提示：本工具是基于：[Packer-Fuzzer](https://github.com/rtcatc/Packer-Fuzzer) 的v1.4 2022/06/19 进行后续升级开发

后续版本由BigYoung开发维护，更新文档： [Packer-Fuzzer-Plus](https://sec.bigyoung.cn/article/Packer-Fuzzer-Plus/)

- v1.0 2023/06/10
  
  1. 增加config.ini里的配置开关，漏洞总数如果为0，不导出报告文件；

  2. 把Packer的指纹配置到config.ini文件中，可以自定义补充内容；

  3. 增加了读取url.txt文件，批量发起检测的功能；
 
- v1.1.0 2023-11-15

  1. 增加扫描结果是否导出API清单到json文件中；

## DownLoad&获取最新版本

[https://mbd.pub/o/bread/mbd-ZZmWl5lv](https://mbd.pub/o/bread/mbd-ZZmWl5lv)


# DailyReport_SHU

上海大学健康之路每日一报/两报自动打卡，受@BlueFisher大神所启发的[项目](https://github.com/BlueFisher/SHU-selfreport)。希望能对大家有所帮助



## 主要功能

* 一报根据前一天上报的地址进行填报，无需自己手动配置地址 
* **党员自动取答案并答题**（多选题暂时不支持，但是能成功上报）
* 自动读新闻，不用在登录的时候被强制读新闻了
* 一报根据所在地调整上报内容（上海和外地的上报选项会有所差别），所以只需要知道学生学号密码即可上报
* 对多人上报进行优化，短时间内多次登录服务器会报429错误，因此代码中有加入休眠机制
* 需要github action的教程请移步@BlueFisher的[项目](https://github.com/BlueFisher/SHU-selfreport)



## 4.27更新（重要）

* 增加多人上报的稳定性
* 增加了一些运行的arguments



## 依赖

* Python >= 3.7

* requests
* bs4
* tqdm

版本无所谓



## 文件说明

- ` once.txt`和`twice.txt`分别为每日一报和两报的上传模板
- students文件夹中存放学上学号密码，支持多人上报



## 用法


1. 假如需要使用一报时一定要自己上报过至少一天！！！！

2. 在students文件夹中加入txt文件记录学生学号和密码，具体格式如`stu_1.txt`所示，想要多人上报的话直接在students文件夹下另外新建txt，命名无所谓。

3. 在代码中配置个人Email信息，方便挂服务器的时候接收信息（或者也可以不配置...)

4. 终端/cmd cd到项目文件夹下，输入 如下代码即可进行上报

    ```python
    python dailyreport.py 
    ```

    文件夹下会出现` all_stu.json`，用于记录上报者信息，方便debug、重复使用一些信息之类的。假如仅仅想测试是否能成功登录和取地址，则加上如下的参数

    ```python
    python dailyreport.py --check 1
    ```

    另外还加入了Email参数，假如想要使用Email功能则需要加上如下参数

    ```python
    python dailyreport.py --send 1
    ```

    如下是所有的可选参数（` python dailyreport.py -h`即可调出）

    ```bash
    % python dailyreport.py -h       
    usage: dailyreport.py [-h] [--check CHECK] [--send SEND] [--dir DIR]
                          [--json JSON] [--noDir NODIR]
    
    optional arguments:
      -h, --help     show this help message and exit
      --check CHECK  Check the login of students
      --send SEND    Send Email or not
      --dir DIR      txt dir
      --json JSON    json file
      --noDir NODIR  Only provide json file
    ```

    其中dir指定的是存放密码txt文件的文件夹，默认为students，--json指定的是存放学生信息json文件的路径（假如不存在会自动新建），--noDir指直接读取json文件进行上报（适用于上报失败后重报）

6. 上报过程中终端会打印以下信息，`done ` 就说明上报成功，`failed`说明出现了上报内容错误，`retry`说明遇到了429问题，正在重新登录（等待120秒），其他的话说明...出了大问题

    ``` bash
    获取cookie
    stu_1.txt login succeed!
    非党员或已答题
    新闻都读过了
    张三 done
    ```



## 注意事项

* 一报一定要**自己报过至少一天**！！ 
* 仍然在测试中，测试的人群有限，可能会有bug
* **一报还未适配留宿同学**！！！假如需求较大会做相应适配
* **两报的模板没有对除嘉定校区以外的校区做优化，需要修改内容**
* **登录系统更新频繁**，假如遇到登录系统失败的问题本项目也会及时研究并且更新，想要快速获得更新请**关注本项目**！



## To do

* 休眠机制完善，尽可能少地触发429错误
* 党员多选题答案上报
* 代理ip池



## 免责声明

本项目仅做免费的学术交流使用。请勿做商业用途！！



## 感谢

再次感谢@BlueFisher和其他contributors，也请大家给我一个star。




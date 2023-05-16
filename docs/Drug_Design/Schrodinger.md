# Schrodinger教程
### 忽略三级标题 <!-- {docsify-ignore} -->
 <!-- panels:start -->


<!-- div:title-panel -->

### 分子对接
---
<!-- div:left-panel -->
- 点击
- 点击
- 介绍

<!-- div:right-panel -->

![Chinvision's公众号](https://github.com/ChinVision/Docs/raw/master/docs/media/WX.jpg)

<!-- div:title-panel -->

### SiteMap
---
<!-- div:left-panel -->
- 点击
- 点击
- 介绍

<!-- div:right-panel -->

右侧内容




<!-- panels:end -->


# 加载蛋白质
## 一、通过点击File>GetPDB下载单个pdb文件

## 二、通过脚本批量下载
### 1、打开schrodinger终端
windows系统可以直接在开始窗口看到Schrodinger Prompt
例如：需要下载的蛋白质为1z95.pdb
运行命令

```shell
getpdb 1z95
```
即可得到pdb文件
### 2、编写python脚本
这里直接在该schrodinger终端内切换一个python环境即可。

批量化命令：
将需要下载的蛋白质文件写入txt，运用python脚本不断循环运行该命令即可

```python
import os
# 存放蛋白信息的文件
fileHandler = open("index.txt",  "r")
# 获取文件内所有的行为列表
listOfLines = fileHandler.readlines()

alsoList = []
times = 0
# 遍历列表
for line in listOfLines:
    # 在控制台运行getpdb的命令
    os.system("getpdb %s" % line)
    times += 1
    # 后面是查看下载了多少个蛋白
    alsoList.append(line)
    print('save %d' % times)

```
### 3、使用爬虫下载
也可以直接使用爬虫，批量下载
```python
import os
import requests
def save_file(fileurl, filename):
    content = requests.get(fileurl, headers=headers)
    if content.status_code != 404:
        content = content.text
        with open(filename + '.pdb', "wb") as f:
            f.write(content.encode("utf-8"))
            global total

            total += 1
            print(f"保存到第{total}个蛋白")
    else:
        print('404')
        global fail_list
        fail_list.append(filename)


if __name__ == '__main__':
    fileHandler = open("index.txt", "r")
    listOfLines = fileHandler.readlines()
    total = 0
    headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.67 Safari/537.36 Edg/87.0.664.47'}
    fail_list = []
    for filename in listOfLines:
        url = "http://files.rcsb.org/download/%s.pdb" % filename.strip()
        save_file(url, filename.strip())

    print('下载失败的')
    print(fail_list)
    fails = open('fail.txt', 'w')
    fails.writelines(fail_listi)
    fails.clos()
```


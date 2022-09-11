# Github Pages搭建流程

## 目标

建立一个用于记录技术文档的网站

## 名词解释

|名词|解释|
|---|---|
|Repo|Repository; 代码仓库|
|README| Read me; 项目说明|

## 流程

* 物色 Jekyll 主题
主题模板网站 <http://jekyllthemes.org/>
* 配置主题为 [Gitbook](https://github.com/sighingnow/jekyll-gitbook)
  * Fork Repo
  * `Repository name` = `Windmill-City.github.io`
![Forked](/assets/Forked.png)
* 启用 Github Pages
* `Settings`->`Pages`->`Build and deployment`
  * `Source` = `Deploy from a branch`
  * `Branch` = `main`|`/root`
![PagesSetting](/assets/PagesSetting.png)
* 修改 About
* `About`->`⚙`
  * `Description` = `Gitbook of personal documents`
  * `Website` = `https://Windmill-City.github.io/`
  * 取消 `Releases`
  * 取消 `Packages`
![About](/assets/About.png)
* 点击 <https://windmill-city.github.io/> 查看页面效果
![MissingCssPage](/assets/MissingCssPage.png)
观察到, 页面的 `CSS` 文件似乎没有正确载入
* 按 `F12` 打开 `DevTools`
* 选择 `Network` 选项卡
* 按 `F5` 刷新页面
![DevTools](/assets/DevTools.png)
观察到, `Request URL` 存在错误
* 修复 `Request URL`
  * `Repo`->`_config.yml`

```yml
url:              'https://Windmill-City.github.io/'
baseurl:          ''
```

* 配置个人信息
  * `Repo`->`_config.yml`

```yml
# Configurations
title:            Gitbook
longtitle:        Gitbook
author:           Windmill_City
email:            1449182174@qq.com
description: >
  Gitbook of personal documents
```

* 等待构建完成
![WaitForBuild](/assets/WaitForBuild.png)
* 点击 <https://windmill-city.github.io/> 查看页面效果
![FinalPage](/assets/FinalPage.png)
观察到, 页面正确显示, 至此 `Github Pages` 搭建完成
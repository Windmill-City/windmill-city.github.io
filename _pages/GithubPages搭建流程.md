---
title: 搭建 Github Pages
date: 2022-09-11
category: Jekyll
layout: post
---

## 目标

建立一个用于记录技术文档的网站

## 名词解释

|名词|解释|
|---|---|
|Repo|Repository; 代码仓库|
|README| Read me; 项目说明|

## 搭建流程

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

* 移除 `Fork it now`
  * `Repo`->`_includes`->`toc-data.html`

```diff
- <li>
-     <a href="https://github.com/sighingnow/jekyll-gitbook/fork" target="blank" class="gitbook-link">
-         Fork it Now!
-     </a>
- </li>
```

* 清理
  * 移除 `_post` 文件夹
  * 清空 `_pages` 文件夹

* 新的文档放置在 `_pages` 文件夹中

* 增加 Metadata 显示

```diff
diff --git a/_includes/body.html b/_includes/body.html
index 9207a8d..da86951 100644
--- a/_includes/body.html
+++ b/_includes/body.html
@@ -1,23 +1,38 @@
 <div class="page-wrapper" tabindex="-1" role="main">
     {% if page.cover %}
-        <img src="{{ page.cover }}"
-             width="100%"
-             height="{{ page.cover_height | default: '100%' }}"
-             alt="{{ page.title | escape }}"
-             style="object-fit: cover;"
-        />
+    <img src="{{ page.cover }}" width="100%" height="{{ page.cover_height | default: '100%' }}"
+        alt="{{ page.title | escape }}" style="object-fit: cover;" />
     {% endif %}
 
     <div class="page-inner">
         <div id="book-search-results">
             <div class="search-noresults">
-                <section class="normal markdown-section">
-                    {% if page.title %}
-                        <h1 id="{{ page.id }}">{{ page.title | escape }}</h1>
-                    {% else %}
-                        <h1 id="{{ page.id }}">{{ site.title | escape }}</h1>
-                    {% endif %}
+                {% if page.title %}
+                <h1 id="{{ page.id }}">{{ page.title | escape }}</h1>
+                {% else %}
+                <h1 id="{{ page.id }}">{{ site.title | escape }}</h1>
+                {% endif %}

+                <ul class="post-meta">
+                    <li>
+                        {% if page.author %}
+                        <a>{{ page.author | escape }}</a>
+                        {% else %}
+                        <a>{{ site.author | escape }}</a>
+                        {% endif %}
+                    </li>
+                    {% if page.date %}
+                    <li>
+                        <a>{{ page.date | date: "%Y-%m-%d" }}</a>
+                    </li>
+                    {% endif %}
+                    {% if page.category %}
+                    <li>
+                        <a>{{ page.category | escape }}</a>
+                    </li>
+                    {% endif %}
+                </ul>
+                <section class="normal markdown-section">
                     {{ content }}
                 </section>
             </div>
@@ -25,4 +40,4 @@
             {%- include search.html -%}
         </div>
     </div>
-</div>
+</div>
```

```diff
diff --git a/assets/gitbook/custom.css b/assets/gitbook/custom.css
index 9879063..8d120ac 100644
--- a/assets/gitbook/custom.css
+++ b/assets/gitbook/custom.css
@@ -52,6 +52,26 @@
     max-width: {{ site.page_width | default: '800px' }};
 }

+.post-meta {
+  margin-top: -0.5em;
+  padding: 0;
+  color: #999;
+  font-size: .92857em;
+}
+
+.post-meta li {
+  display: inline-block;
+  margin: 0 8px 0 0;
+  padding-left: 12px;
+  border-left: 1px solid #EEE;
+}
+
+.post-meta li:first-child {
+  margin-left: 0;
+  padding-left: 0;
+  border: none;
+}
+
 .back-to-top {
     right: calc((100% - 300px - min(100% - 300px, {{ site.page_width | default: '800px' }})) / 2 + 25px);
 }
```

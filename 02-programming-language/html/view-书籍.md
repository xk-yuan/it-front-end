# 

>

## 书籍分析

> 书籍定位: XX章 XX节 XX段落 XX字

1. 基本信息介绍

- 书名
- 作者
- 著作信息
- 出版信息

2. 书籍结构

- 目录
- 序言
- 章节    (chapters and sections) (chapters: 篇章, sections 小结部分; 章包含节, 有些文章只有章没有节, 节对章进行细分补充)
  - 段落
  - 行
  - 字
- 插画

3. 页面结构

- 封面
- 扉页
- 章节页

> 内容表示

- 书籍  div   class=book                 data-book-id=hash

- 章节  div   class=book-chapter         data-book-chapter-id=1
  - 章名      class=book-chapter-title                     
  - 节名      class=book-section-title
- 段落  p     class=book-paragraph       data-book-paragraph-id=1
- 行    span  class=book-row                                                 行是不定的, 根据显示宽度的多少, 行会自定转换
- 文字  span     class=book-char         data-book-paragraph-char-id=1       字标识, 从该段落开始从1计数
- 插画  span+img class=book-img          data-book-img-id=1                  插画, 从该文章头从1开始计数


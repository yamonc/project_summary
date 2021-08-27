# 博客系统项目总结文档

## 技术选型

后端采用[Spring Boot](https://spring.io/projects/spring-boot/)、持久层框架采用[mybatis-plus](https://mp.baomidou.com/)，缓存使用[Redis](https://redis.io/)，权限控制框架使用[Shiro](https://shiro.apache.org/)。与天津IKC项目不同的是，前端模板引擎使用[Thymeleaf](https://www.thymeleaf.org/)，前台界面使用[Semantic UI](https://semantic-ui.com/)，普通用户后台界面使用[Bootstrap](https://v3.bootcss.com/)框架。

## 项目概括

### 基本功能

![image-20210827180803002](https://gitee.com/yamonc/blogImage/raw/master//img/blogImage/image-20210827180803002.png)

### 项目展示

#### 首页展示

![image-20210827182727591](https://gitee.com/yamonc/blogImage/raw/master//img/blogImage/image-20210827182727591.png)

#### 文章正文显示![image-20210827184645084](https://gitee.com/yamonc/blogImage/raw/master//img/blogImage/image-20210827184645084.png)

![image-20210827184659768](https://gitee.com/yamonc/blogImage/raw/master//img/blogImage/image-20210827184659768.png)

#### 后台管理展示

![image-20210827182824376](https://gitee.com/yamonc/blogImage/raw/master//img/blogImage/image-20210827182824376.png)

#### 普通用户后台展示

此效果需要注册和登录之后才能展示出来。

![image-20210827182938138](https://gitee.com/yamonc/blogImage/raw/master//img/blogImage/image-20210827182938138.png)

### 数据库设计

![Diagram 1](https://gitee.com/yamonc/blogImage/raw/master//img/blogImage/Diagram 1.png)

#### 抽象实体关系

由博客文章为中心，向四周扩展功能。

1. t_blog:博客文章为一个实体类型。
2. t_comment:博客评论为一个实体类型，一个文章有多个评论，而一个评论只能属于一个文章，所以博客文章和评论是一对多的关系，将主键设置在多的一方，及评论表里面有文章的ID属性。其次，评论有子评论，所以在评论表中应该有自引用系列，即评论表中有一个外键指向评论表的主键。比如parentId是一个外键，指向的是评论表的主键。
3. t_tag:标签表为一个实体类型，一个文章有多个标签，同时一个标签可以给多个文章使用。所以文章跟标签的关系是多对多，需要设置中间表存储文章和标签的所有主键属性。
4. t_type:类型表（专题、分类）为一个实体类型，一个文章有一个分类，但是一个分类可以有多个文章。所以文章和分类的关系是一对多关系。
5. t_notice:公告表为一个实体，用来首页上的发布公告。
6. t_report:报告表，用来存储用户提交的bug和反馈意见。
7. pic：图片表，从固定网址上用Python爬取的照片链接，用于博客发布的时候随机生成的首图、导航栏提交Bug功能的随机图片生成。
8. t_user:用户注册表，为一个实体类型。
9. t_log：用户登录产生的日志信息。一个用户可以有多个日志，而一个日志只属于一个用户。所以用户和日志之间的关系是一对多。
10. t_file:文件表，用户可以上传文件到数据库中，实现共享功能。目前功能尚未开放。一个用户可以上传多个文件，但是一个文件只属于一个用户上传，所以用户和文件之间的关系是一对多的关系。
11. collection_user_blog:收藏表，用户可以点击博客正文里面的收藏功能。一个用户可以收藏多篇文章，一个文章也可以被多个用户收藏，所以文章收藏和用户之间的关系是多对多。
12. t_role:角色表，一个用户可以有多个角色，一个角色可以属于多个用户，所以两者之间是多对多关系。使用中间表记录两者之间的关系。
13. t_permission：权限表，一个角色可以有多个权限，但是一个权限只能属于一个角色。一对多关系。
14. t_like:暂时没加上去，喜欢表，用户可以点击文章正文的喜欢按钮，数据库会自动记录用户和博客文章之间的关系。

### 管理员功能

#### 博客管理

新增博客、修改博客、删除博客。




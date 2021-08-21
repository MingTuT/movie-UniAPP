# 电影推荐

## 项目简介

该项目模仿《猫眼》与《豆瓣》的页面设计，是一款推荐优质电影的应用。

搭建该项目使用的是Uni-App框架，该框架集成了许多API，十分简便容易上手。

后端使用的技术是：Node.js 中的 Express 框架 + MongoDB 数据库 。



## Pages

### 首页

+ 轮播图使用 uniapp 框架的 swiper 组件，设置循环播放，指示器显示，间隔时间设置为5秒。
+ 封装 traillerStars 组件，根据电影的评分，展示相应的黄星与灰星的数量。score 用于接收电影评分，showNum 的值为0和1，当值为0时不显示电影评分数字，仅显示星星，反之。
+ 热门视频部分使用 uniapp 框架的 scroll-view 组件，并将 scroll-view 设置为水平方向滚动，以达到滑动展示更多电影信息。
+ 口碑电影和推荐电影部分简单使用 flex 纵向布局，展示电影的摘要。

### 搜索页

+ 分为上下两部分，顶部搜索框使用 fixed 固定在视口，电影推荐列表每次随机展示9部电影。
+ 根据搜索框 value 值向后端请求包含关键字的电影列表。
+ 使用 v-if 和 v-else 控制**电影推荐列表**和**搜索电影列表**显示的切换。
+ 每次页面加载时，在 onshow 函数中请求随机推荐电影数据。

### 我的

+ 主要展示已登录用户的信息概要，使用 v-if 和 v-else 控制登录与否时的页面展示。
+ 退出登录调用框架的 uni.removeStorageSync 实现。
+ 修改资料可以修改用户的**头像、用户名、性别和个性签名**。修改头像调用框架的 uni.chooseImage ，该方法调用成功后使用 res.tempFilePaths[0] 可以实现头像预览的展示效果。
+ 操作保存修改时，若头像未修改时则调用 uni.request 上传表单数据，若头像已修改则调用 uni.uploadFile 将图片与表单一同上传。

### 详情页

+ 在 onLoad 函数中获取 navigator 传递的电影 ID，展示电影详情信息。
+ 引用 traillerStars  组件。
+ 电影预告使用 video 标签展示，并设置 poster 预告未播放时的封面。
+ 剧照使用 uniapp 框架的 scroll-view 组件，并将 scroll-view 设置为水平方向滚动，以达到滑动展示更多电影信息。使用 uni.previewImage 实现剧照的查看。

### 注册

+ 邮箱：使用正则表达式检验邮箱的合法性。
+ 密码：使用正则表达式检验密码的位数与规则的合法性。
+ 确认密码： 对比两次输入的密码十分一致。
+ 若以上输入有误，底部错误提示将会设置为 show。
+ 注册失败：若注册信息有误，调用 uni.showToast 提示错误信息。
+ 注册成功：调用 uni.setStorageSync 将用户信息进行本地保存，并重定向到已登录的用户页面。

### 登录

+ 登录失败：若登录信息有误，调用 uni.showToast 提示错误信息。
+ 登录成功：调用 uni.setStorageSync 将用户信息进行本地保存，并重定向到已登录的用户页面。



## 后端

Node.js + MongoDB 简易搭建后端。

使用 Express 框架，其中封装了许多原生的方法，能快捷完成服务的搭建。

| 表名            | 说明       |
| :-------------- | ---------- |
| carousels       | 轮播图电影 |
| hotmovies       | 热门视频   |
| nicemovies      | 口碑电影   |
| recommendmovies | 推荐电影   |
| movies          | 电影       |
| users           | 用户       |

**PS**：除 users 表与 movies 表，其他的表中都存储了 movies 表中的电影数据的 _id ，以此产生表与表之间的关联。

-------------------

用户上传的头像使用 form = new multiparty.Form()，并设置一个默认的存储地址（form.uploadDir='./public/user/avatar'）。

设置 express.static 开放静态资源访问，即可访问服务器的电影数据等。

-----------------------





## 页面效果

<img src="https://pic.imgdb.cn/item/610e52785132923bf8817ad8.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e52785132923bf8817ae2.png" alt="img" width="750" />



<img src="https://pic.imgdb.cn/item/610e52785132923bf8817aea.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e52785132923bf8817af4.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e53a45132923bf88450a1.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e52785132923bf8817aff.png" alt="img" width="750" />



<img src="https://pic.imgdb.cn/item/610e53a45132923bf884507f.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e53a45132923bf8845081.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e53a45132923bf8845086.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e53a45132923bf8845097.png" alt="img" width="750" />

<img src="https://pic.imgdb.cn/item/610e54195132923bf8856dac.png" alt="img" width="750" />






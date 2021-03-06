## 1.项目介绍
### 1.1.项目描述简介
类似京东商城的B2C商城 (C2C B2B O2O P2P ERP进销存 CRM客户关系管理)
电商或电商类型的服务在目前来看依旧是非常常用，虽然纯电商的创业已经不太容易，但是各个公司都有变现的需要，所以在自身应用中嵌入电商功能是非常普遍的做法。

为了让大家掌握企业开发特点，以及解决问题的能力，我们开发一个电商项目，项目会涉及非常有代表性的功能。

为了让大家掌握公司协同开发要点，我们使用git管理代码。

在项目中会使用很多前面的知识，比如架构、维护等等。
### 1.2.主要功能模块

系统包括：

* 后台：品牌管理、商品分类管理、商品管理、订单管理、系统管理和会员管理六个功能模块。
* 前台：首页、商品展示、商品购买、订单管理、在线支付等。

### 1.3.开发环境和技术

* 开发环境:	 Window
* 开发工具:   Phpstorm+PHP5.6+GIT+Apache
* 相关技术:   Yii2.0+CDN+jQuery+sphinx

### 1.4.项目人员组成周期成本
#### 1.4.1.人员组成
职位|人数|备注
----|------|----
项目经理和组长|1|一般小公司由项目经理负责管理，中大型公司项目由项目经理或组长负责管理
开发人员|3|	
UI设计人员|0	
前端开发人员|1|专业前端不是必须的，所以前端开发和UI设计人员可以同一个人
测试人员|1|有些公司并未有专门的测试人员，测试人员可能由开发人员完成测试。

> 公司有测试部，测试部负责所有项目的测试。

> 项目测试由产品经理进行业务测试。

> 项目中如果有测试，一般都具有Bug管理工具(现都被集成在项目管理工具中)。

#### 1.4.2.项目周期成本
人数|周期|备注
----|------|----
1|两周需求及设计|项目经理
1|两周|UI设计	UI/UE
4（1测试  2后端  1前端|3个月(第1周需求设计,9周时间完成编码, 2周时间进行测试和修复)|开发人员、测试人员
## 2.系统功能模块
### 2.1.需求
- [x] 品牌管理：
- [x] 文章管理：
- [x] 商品分类管理：
- [ ] 商品管理：
- [ ] 账号管理：
- [ ] 权限管理：
- [ ] 菜单管理：
- [ ] 订单管理：

### 2.2.流程
* 自动登录流程
* 购物车流程
* 订单流程
### 2.3.设计要点（数据库和页面交互）

1. 系统前后台设计：前台www.yiishop.com 后台admin.yiishop.com 对url地址美化
2. 商品无限级分类设计：
3. 购物车设计

### 2.4.要点难点及解决方案
难点在于需要掌握实际工作中，如何分析思考业务功能，如何在已有知识积累的前提下搜索并解决实际问题，抓大放小，融会贯通，尤其要排除畏难情绪。

## 3.品牌功能模块
### 3.1.需求
* 品牌管理功能涉及品牌的列表展示、品牌添加、修改、删除功能。
* 品牌需要保存缩略图和简介。
* 品牌删除使用逻辑删除。

### 3.2.流程

### 3.3.设计要点（数据库和页面交互）

### 3.4.要点难点及解决方案
1. 删除使用逻辑删除,只改变status属性,不删除记录
2. 使用uploadify插件,提升用户体验
3. 使用composer下载和安装uploadify
4. composer安装插件报错,解决办法:
composer global require "fxp/composer-asset-plugin:^1.2.0"
5. 注册七牛云账号
安装yii2 七牛云插件
6. 将品牌logo上传到七牛云

## 4.文章管理模块
### 4.1.需求
* 文章的增删改查
* 文章分类的增删改查
### 4.2.设计要点
文章模型和文章详情模型建立1对1关系
### 4.3.要点难点及解决方案
1. 文章分类不能重复,通过添加验证规则unique解决
2. 文章垂直分表,创建表单使用文章模型和文章详情模型

## 5.商品分类
### 5.1需要
* 商品分类的增删除改查
* 无限级分类
* 列表展示页需要折叠

### 5.2设计要点
利用ztree展示分类 
利用nested实现左值右值

### 5.3.要点难点及解决方案
1. ztree插件 进入页面就要展开 点击分类后Js控制value
2. nested 不能用detelte去删除root节点,要用内置的deleteWithChildren()去删除
3. 健壮性的的时候不能放到自己的子孙节点,这个需要异常捕获
4. JS字符串比较 lft>clft   改成lft-clft>0

## 6商品管理

### 6.1需要
* 商品的增删除改查
* 商品要有货号
* 每天商品数的统计
* 商品详情
* 分类和品牌
* 多图片
* 列表页需要搜索

### 5.2设计要点
* 如果货号有输入,则取输入的,如果没有输入自动生成:2017111200001(00001为当天添加的商品总数)
* 商品详情1对1对  品牌1对1  分类1对1
* 利用ueditor插件实现富文本编辑器
* 利用webuploader插件实现多图片上传
* 图片存储采用七牛OOS云存储

### 5.3.要点难点及解决方案
1. 货号生成: 0000."当天商品数量+1"  再截取后面5位
2. Ueditor图片上传在本地 到时用 镜像存储解决
3. 多图片回显,把图片地址以数组赋值给属性,多图上传个别失败,需要调整上传到的文件名(key)
4. 列表货号搜索(难点)
5. 删除顺序,要先删除关联的表的数据
6. 多图片上传属性不能和数据库里有的字段一致

## 7.管理员


### 7.1需要
* 管理员的增删改查
* 管理员登录 自动登录
* 退出
* 自己资料修改
* 编辑的时候密码不要回显,如果没有输入密码,不更改,只有输入了密码才更改密码(场景)

### 7.2设计要点
* 自动登录

### 7.3.要点难点及解决方案
1. 要修改配置里user组件里用来实现用户的类 Admin::className();
2. 自己登录要实现接口
3. 自己的资料修改
4. 一般情况下都用username做为用户名字段

## 8.RBAC权限管理

###  8.1 需求
* 权限的增删改查

### 8.2 设计要点
1. 配置authManager 组件
2. 数据迁移
3. 实例化authManager,再做增删改查

### 8.3.要点难点及解决方案
1. 权限用过滤器来实现,需要设置全局注入
2. 编辑角色,需要先删除原来所有权限,再执行添加操作

## 9.菜单管理
### 9.1需求
1. 菜单的增删改查
2. 两级菜单

### 9.2 设计要点

无限级菜单

### 9.3.要点难点及解决方案

1. 循环第一级菜单(parent_id=0),再根据当前的id循环出来它的子类(parent_id=id)

## 10.前台会员功能

### 10.1需求

1. 会员注册
2. 会员登录
3. 地址管理

### 10.2设计要点
* 会员注册要短信验证
* 会员登录要实现自动登录
* 提示用layer插件来做

### 10.3要点难点及解决方案
* 阿里大鱼已和阿里云合并,只能用阿里云的包 
* 短信验证存Session   Tel_13899996666=>985412
* 登录后要把Cookie里购物车数据同步到数据库中,同时清空本地购物车数据
* 验证码只能验证一次,save(false)

## 11.分类 列表 详情

### 11.1需求

1. 实现三级分类在头部显示
2. 实现当前分类及子分类所有商品的数据(status=1)显示在列表页
3. 实现商品详情页

### 11.2设计要点
1. 分类实现缓存技术
2. 采用widget小挂件
3. 利用放大镜技术提升用户体验

### 11.3 要点难点及解决方案

1. 缓存 设置过期时间,后台添加分类之后要清空缓存
2. 分类 在模型中设置一个得到当前子类的方法
3. 子分类拼接 利用左值和右值当前树来处理 array_column()
4. 取商品要加status

## 12.购物车

### 12.1需求
1. 实现购物车功能

### 12.2设计要点
1. 登录或未登录分别存储
2. 用户登录之后会同步购物车数据

### 12.3要点难点及解决方案
1. 把逻辑搞清,不清楚画流程图
2. 把购物车逻辑封装成组件

## 13 订单
### 13.1需要






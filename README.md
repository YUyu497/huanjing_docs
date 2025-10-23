# 🎮 幻境FiveM服务器官网

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Node](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen.svg)
![Vue](https://img.shields.io/badge/vue-3.4.0-4FC08D.svg)
![MySQL](https://img.shields.io/badge/mysql-5.7+-orange.svg)

**一个现代化的赛博朋克风格FiveM服务器官网**

[在线演示](https://huanjing.ajiu.top) | [文档](https://github.com/your-repo/docs) | [问题反馈](https://github.com/your-repo/issues)

</div>

---

## ✨ 项目特色

### 🎨 赛博朋克UI设计

- **霓虹色彩搭配**: 青色、紫色、绿色的未来科技感配色
- **动态效果**: 渐变背景、光效动画、悬停交互
- **响应式设计**: 完美适配PC、平板、移动端
- **现代化界面**: 玻璃拟态、卡片设计、流畅动画

### 🔐 完整权限体系

- **三级权限管理**: 普通用户、管理员、站长
- **细粒度控制**: 功能级、数据级权限控制
- **安全认证**: JWT Token + 密码哈希加密
- **第三方登录**: 支持QQ一键登录

### 🚀 高性能架构

- **前后端分离**: Vue3 + Node.js + MySQL
- **缓存优化**: Redis缓存提升响应速度
- **数据库优化**: 连接池、索引优化、查询优化
- **CDN加速**: 七牛云OSS文件存储

### 🎯 功能完整

- **用户系统**: 注册登录、资料管理、游戏数据
- **社区系统**: 帖子发布、回复互动、点赞分享
- **内容管理**: Markdown编辑器、分类标签、发布审核
- **下载中心**: 文件管理、分类下载、统计排行
- **服务器监控**: 实时状态、玩家统计、性能图表

---

## 🛠️ 技术栈

### 前端技术

- **框架**: Vue 3.4.0 (Composition API)
- **构建工具**: Vite 5.0.8
- **UI框架**: Element Plus 2.4.4
- **状态管理**: Pinia 2.1.7
- **路由**: Vue Router 4.2.5
- **HTTP客户端**: Axios 1.6.2
- **代码编辑器**: Monaco Editor
- **图表库**: ECharts + Vue-ECharts
- **样式**: SCSS + 赛博朋克主题

### 后端技术

- **运行环境**: Node.js 16.0+
- **Web框架**: Express.js 4.18.2
- **数据库**: MySQL 5.7+ + Redis 4.6.10
- **认证**: JWT + bcryptjs
- **文件处理**: Multer + 七牛云OSS
- **邮件服务**: Nodemailer (QQ邮箱)
- **安全防护**: Helmet + CORS + Rate Limiting

### 第三方集成

- **QQ登录**: OAuth2.0认证
- **邮件服务**: QQ邮箱SMTP
- **文件存储**: 七牛云对象存储
- **QQ机器人**: 群消息处理

---

## 📦 快速开始

### 环境要求

- Node.js >= 16.0.0
- MySQL >= 5.7
- Redis >= 4.6
- npm >= 8.0.0

### 安装步骤

#### 1. 克隆项目

```bash
git clone https://github.com/your-repo/fivem-website.git
cd fivem-website
```

#### 2. 安装依赖

```bash
# 安装后端依赖
cd backend
npm install

# 安装前端依赖
cd ../frontend
npm install
```

#### 3. 配置环境变量

**后端配置** (`backend/.env`)

```env
# 数据库配置
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=fivem_website

# Redis配置
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=

# JWT配置
JWT_SECRET=your_jwt_secret_key

# 邮件配置
QQ_EMAIL_USER=your_email@qq.com
QQ_EMAIL_PASS=your_email_auth_code

# QQ登录配置
QQ_APP_ID=your_qq_app_id
QQ_APP_KEY=your_qq_app_key
QQ_REDIRECT_URI=http://localhost:3002/api/auth/qq/callback

# 七牛云配置
QINIU_ACCESS_KEY=your_qiniu_access_key
QINIU_SECRET_KEY=your_qiniu_secret_key
QINIU_BUCKET=your_bucket_name
QINIU_DOMAIN=your_domain

# 服务器配置
PORT=3002
NODE_ENV=development
```

**前端配置** (`frontend/.env`)

```env
VITE_API_BASE_URL=http://localhost:3002/api
VITE_APP_TITLE=幻境FiveM服务器
```

#### 4. 初始化数据库

```bash
# 导入数据库结构
mysql -u root -p fivem_website < backend/database/init.sql

# 或者使用Node.js脚本初始化
cd backend
npm run init-db
```

#### 5. 启动服务

**开发环境**

```bash
# 启动后端服务
cd backend
npm run dev

# 启动前端服务
cd frontend
npm run dev
```

**生产环境**

```bash
# 构建前端
cd frontend
npm run build

# 启动后端
cd backend
npm start
```

### 访问地址

- **前端**: <http://localhost:3000>
- **后端API**: <http://localhost:3002>
- **API文档**: <http://localhost:3002/api>

---

## 📁 项目结构

```
fivem-website/
├── frontend/                 # Vue3前端项目
│   ├── src/
│   │   ├── components/       # 组件
│   │   ├── views/           # 页面
│   │   ├── router/          # 路由配置
│   │   ├── store/           # 状态管理
│   │   ├── assets/          # 静态资源
│   │   └── utils/           # 工具函数
│   ├── public/              # 公共资源
│   └── package.json
├── backend/                 # Node.js后端项目
│   ├── src/
│   │   ├── routes/          # 路由
│   │   ├── models/          # 数据模型
│   │   ├── services/        # 服务层
│   │   ├── middleware/      # 中间件
│   │   ├── config/          # 配置文件
│   │   └── utils/           # 工具函数
│   ├── database/            # 数据库脚本
│   ├── uploads/             # 上传文件
│   └── package.json
├── docs/                    # 项目文档
└── README.md
```

---

## 🎯 核心功能

### 👤 用户系统

- **用户注册**: 邮箱验证码注册
- **用户登录**: 本地登录 + QQ第三方登录
- **用户资料**: 头像、昵称、性别、生日等个人信息管理
- **游戏数据**: 游戏时长、等级、经验、成就统计
- **好友系统**: 好友添加、管理、状态跟踪
- **权限管理**: 三级权限体系，细粒度权限控制

### 📝 内容管理

- **Markdown编辑器**: Monaco Editor专业编辑体验
- **内容分类**: 支持多种内容类型和标签系统
- **发布管理**: 草稿、发布、归档状态管理
- **搜索功能**: 全文搜索、标签搜索、分类筛选
- **更新日志**: 版本管理、变更记录、发布通知

### 💬 社区系统

- **帖子发布**: 富文本编辑器、图片上传、标签选择
- **回复系统**: 嵌套回复、回复管理、回复通知
- **点赞系统**: 帖子点赞、回复点赞、点赞统计
- **话题标签**: 话题分类、话题管理、话题统计
- **内容审核**: 帖子审核、回复审核、举报处理

### 📥 下载中心

- **文件管理**: 文件上传、分类、版本管理
- **存储支持**: 本地存储 + 七牛云OSS双重支持
- **下载统计**: 下载次数统计、热门文件排行
- **权限控制**: 下载权限管理、访问控制
- **分类管理**: 文件分类、分类图标、分类颜色

### 🖥️ 服务器监控

- **实时监控**: 服务器状态、在线玩家、性能指标
- **历史数据**: 历史状态记录、趋势分析
- **性能图表**: CPU、内存、网络使用率图表
- **自动刷新**: 定时更新、状态变化通知
- **多服务器**: 支持多服务器监控

### ⚙️ 管理后台

- **用户管理**: 用户列表、权限管理、状态控制
- **内容管理**: 内容审核、发布管理、分类管理
- **社区管理**: 帖子管理、回复管理、举报处理
- **下载管理**: 文件管理、分类管理、统计查看
- **系统设置**: 系统配置、邮件设置、存储设置
- **数据统计**: 用户统计、内容统计、访问统计

---

## 🔧 配置说明

### 数据库配置

项目使用MySQL作为主数据库，Redis作为缓存数据库。数据库结构包含25个核心表，支持完整的业务功能。

### 邮件服务配置

使用QQ邮箱SMTP服务，支持注册验证码、密码重置、欢迎邮件等功能。

### 文件存储配置

支持本地存储和七牛云OSS双重存储方案，可根据需要选择配置。

### QQ登录配置

集成QQ OAuth2.0登录，需要申请QQ互联应用获取App ID和App Key。

---

## 🚀 部署指南

### 宝塔面板部署

#### 1. 环境准备

- 安装宝塔面板
- 安装Node.js 16+
- 安装MySQL 5.7+
- 安装Redis
- 安装Nginx

#### 2. 项目部署

```bash
# 上传项目文件到服务器
# 配置域名和SSL证书
# 设置Nginx反向代理
# 配置PM2进程管理
```

#### 3. 数据库配置

```bash
# 创建数据库
# 导入数据库结构
# 配置数据库用户权限
```

#### 4. 服务启动

```bash
# 启动后端服务
pm2 start backend/src/app.js --name "fivem-backend"

# 构建前端项目
cd frontend && npm run build

# 配置Nginx静态文件服务
```

### Docker部署

```bash
# 构建镜像
docker build -t fivem-website .

# 运行容器
docker run -d -p 3000:3000 -p 3002:3002 fivem-website
```

---

## 📊 性能优化

### 前端优化

- **代码分割**: 路由级别的代码分割
- **懒加载**: 组件和图片懒加载
- **缓存策略**: 静态资源缓存
- **压缩优化**: Gzip压缩、资源压缩

### 后端优化

- **数据库优化**: 索引优化、查询优化
- **缓存策略**: Redis缓存热点数据
- **连接池**: 数据库连接池管理
- **请求限流**: 防止恶意请求

### 服务器优化

- **CDN加速**: 静态资源CDN分发
- **负载均衡**: 多服务器负载均衡
- **监控告警**: 性能监控和告警
- **日志管理**: 结构化日志记录

---

## 🔒 安全特性

### 认证安全

- **JWT Token**: 无状态认证机制
- **密码加密**: bcryptjs哈希加密
- **会话管理**: 安全的会话管理
- **登录保护**: 登录失败次数限制

### 数据安全

- **SQL注入防护**: 参数化查询
- **XSS防护**: 输入输出过滤
- **CSRF防护**: CSRF Token验证
- **敏感数据加密**: 敏感信息加密存储

### 请求安全

- **CORS配置**: 跨域请求控制
- **请求限流**: 防止暴力攻击
- **输入验证**: 严格的输入验证
- **错误处理**: 安全的错误信息

---

## 📈 监控与日志

### 应用监控

- **性能监控**: CPU、内存、响应时间
- **错误监控**: 错误日志、异常跟踪
- **业务监控**: 用户活跃、功能使用
- **数据库监控**: 连接数、查询性能

### 日志管理

- **访问日志**: 用户访问记录
- **错误日志**: 系统错误记录
- **业务日志**: 业务操作记录
- **安全日志**: 安全事件记录

---

## 🤝 贡献指南

### 开发流程

1. Fork项目到个人仓库
2. 创建功能分支
3. 提交代码变更
4. 创建Pull Request
5. 代码审查和合并

### 代码规范

- 使用ESLint进行代码检查
- 遵循Vue.js官方风格指南
- 使用Prettier进行代码格式化
- 编写清晰的注释和文档

### 提交规范

```
feat: 新功能
fix: 修复bug
docs: 文档更新
style: 代码格式调整
refactor: 代码重构
test: 测试相关
chore: 构建过程或辅助工具的变动
```

---

## 📄 许可证

本项目采用 [MIT许可证](LICENSE) 开源协议。

---

## 🙏 致谢

感谢以下开源项目的支持：

- [Vue.js](https://vuejs.org/) - 渐进式JavaScript框架
- [Element Plus](https://element-plus.org/) - Vue 3组件库
- [Express.js](https://expressjs.com/) - Node.js Web框架
- [MySQL](https://www.mysql.com/) - 关系型数据库
- [Redis](https://redis.io/) - 内存数据库
- [Monaco Editor](https://microsoft.github.io/monaco-editor/) - 代码编辑器

---

## 📞 联系我们

- **项目地址**: [GitHub Repository](https://github.com/your-repo/fivem-website)
- **在线演示**: [https://huanjing.ajiu.top](https://huanjing.ajiu.top)
- **问题反馈**: [Issues](https://github.com/your-repo/issues)
- **邮箱联系**: <your-email@example.com>

---

## 📝 更新日志

### v1.0.0 (2024-12-XX)

- ✨ 初始版本发布
- 🎨 赛博朋克UI设计
- 👤 完整的用户系统
- 💬 社区功能
- 📥 下载中心
- 🖥️ 服务器监控
- ⚙️ 管理后台
- 🔐 权限管理
- 📧 邮件服务
- 🔗 QQ登录集成

---

<div align="center">

**⭐ 如果这个项目对您有帮助，请给我们一个Star！**

Made with ❤️ by 幻境服务器团队

</div>

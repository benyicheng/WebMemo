浏览器浏览记录与行为分析插件，用于记录用户的浏览行为并提供分析功能。

## 项目架构
项目采用模块化架构，分为以下几个主要部分：
### 共享模块 (shared/)
包含前端扩展和后端服务共享的代码：
- `types.ts`: 共享类型定义
- `config.ts`: 共享配置项
- `utils.ts`: 共享工具函数
### 浏览器扩展 (extension/)
浏览器扩展部分负责捕获用户浏览行为并发送到后端服务：
- `background/`: 后台脚本，负责数据处理和与服务器通信
  - `index.ts`: 后台脚本主入口
  - `dataQueue.ts`: 数据队列处理模块
- `content/`: 内容脚本，在页面中执行
  - `index.ts`: 内容脚本主入口
  - `pageCapture.ts`: 页面信息捕获模块
  - `interactionCapture.ts`: 用户交互捕获模块
- `popup/`: 扩展弹出窗口
- `settings/`: 扩展设置页面
- `history/`: 浏览历史查看页面

### 后端服务 (server/)
后端服务负责接收和存储数据，并提供API接口：
- `src/`: 源代码目录
  - `index.ts`: 服务主入口
  - `api/`: API模块
    - `routes.ts`: API路由定义
    - `controllers.ts`: API控制器
  - `database/`: 数据库模块
    - `service.ts`: 数据库服务
    - `models.ts`: 数据库模型
    - `migrate.ts`: 数据库迁移脚本
- `data/`: 数据存储目录

## 安装与使用
### 安装依赖
```bash
# 安装根目录依赖
npm install

# 安装浏览器扩展依赖
cd extension
npm install

# 安装后端服务依赖
cd ../server
npm install
```

### 开发模式
```bash
# 启动后端服务
cd server
npm run dev

# 启动浏览器扩展开发模式
cd ../extension
npm run dev
```

### 构建生产版本

```bash
# 构建后端服务
cd server
npm run build

# 构建浏览器扩展
cd ../extension
npm run build
```

## 功能特性
### 基础功能
- 记录页面访问信息（URL、标题、加载时间等）
- 捕获用户交互行为（点击、滚动、表单操作）
- 提供历史浏览记录查看
- 数据统计与分析

### 增强功能
- **媒体内容检测**：自动识别并记录首屏图片和视频内容
- **内容快照**：提取页面正文、生成摘要、保存页面截图
- **离线模式**：在本地服务不可用时，支持数据本地缓存和基本功能
- **数据同步**：在网络恢复后自动同步本地缓存数据

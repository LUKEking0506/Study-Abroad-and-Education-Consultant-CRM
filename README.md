# 留学咨询公司的 CRM 系统

一个为留学咨询公司设计的客户关系管理系统，用于管理学生申请、签证流程、顾问和财务数据。

## 目录
- [功能](#功能)
- [技术栈](#技术栈)
- [安装](#安装)
- [使用](#使用)
- [数据库结构](#数据库结构)
- [环境变量](#环境变量)
- [部署](#部署)
- [贡献](#贡献)
- [许可](#许可)

## 功能
- **大学和课程管理**：大学数据库、课程信息、申请截止日期提醒。
- **用户角色和权限**：管理员、顾问、签证专家、财务官等。
- **学生管理**：管理学生档案、文档和申请。
- **申请跟踪**：跟踪学生申请及其状态。
- **签证处理**：监控签证申请、文档和状态。
- **财务管理**：管理学生付款并生成发票。
- **通知**：发送自动电子邮件和 SMS 通知。
- **报告**：生成关于学生、顾问、申请和财务的报告。

## 技术栈
- **后端**：Laravel 10
- **前端**：vue.js 3 with vuetify（用于 UI 组件）
- **数据库**：mysql 8.0
- **部署**：docker（用于容器化）、nginx、CI/CD with devops 管道
- **版本控制**：git & GitHub

## 安装
### 先决条件
- **docker**：用于容器化应用。
- **PHP**：版本 8.1 或更高。
- **Node.js**：用于 vue.js 前端。
- **MySQL**：版本 8.0 或更高。
- **composer**：用于管理 PHP 依赖。

## 使用
项目设置并运行后，可以按如下方式开始使用留学咨询公司的 CRM 系统：

### 1. 登录
- 访问 `http://localhost:8080` 进入登录页面。
- 使用数据种子过程中提供的凭据登录为管理员、顾问或其他用户角色。

### 2. 管理学生
- 登录后，从仪表板转到学生部分。
- 这里，你可以：
  - 查看学生列表。
  - 添加新学生档案，包括个人详细信息、教育背景和文档。
  - 编辑或删除现有学生档案。

### 3. 跟踪申请
- 转到申请部分，查看所有学生申请的状态。
- 可以按当前状态过滤申请（例如，审核中、接受、拒绝）。
- 使用操作按钮查看或更新申请详情、上传文档或与学生沟通。

### 4. 签证处理
- 在签证管理部分，监控学生签证申请。
- 你可以：
  - 查看签证申请详情，包括提交日期和当前状态。
  - 更新签证状态（例如，批准、拒绝）。
  - 向学生发送有关签证状态的通知。

### 5. 财务管理
- 转到财务或开票部分，查看和管理学生付款。
- 系统允许你：
  - 为学生服务生成发票。
  - 跟踪付款状态（已支付、待支付）。
  - 通过电子邮件或 SMS 发出付款提醒。

### 6. 用户角色和权限
- 系统支持各种用户角色（管理员、顾问、签证专家、财务官）。
- 管理员用户可以在用户管理部分管理用户角色并分配不同权限。

### 7. 生成报告
- 从报告部分，管理员可以生成关于学生、申请、签证状态和财务的详细报告。
- 报告可按日期范围、学生国籍、大学和其他因素过滤。

### 8. 通知
- 自动通知（电子邮件/SMS）会为关键事件发送，例如：
  - 新申请提交。
  - 签证状态更新。
  - 付款提醒。
这些通知帮助保持顾问和学生的信息同步。

### 9. 仪表板概览
- 仪表板提供系统关键指标的概览：
  - 总学生数。
  - 总申请数。
  - 待处理签证。
  - 未支付发票。
管理员和顾问可以使用此摘要跟踪进度并识别需要关注的领域。

### 10. 高级搜索和过滤
- 系统包括高级搜索和过滤选项，可根据特定标准（例如，姓名、电子邮件、国籍、申请状态）快速查找学生、申请或发票。

## 数据库结构
留学咨询公司的 CRM 系统使用关系数据库，设计用于管理学生、申请、签证处理和开票。以下是主要数据库表及其关系的概览。

### 1. 学生表
- 存储学生个人信息。
- **字段**：
  - `id`（主键）
  - `name`
  - `email`
  - `phone`
  - `nationality`
  - `date_of_birth`
  - `created_at`, `updated_at`

### 2. 申请表
- 包含学生申请大学或课程的记录。
- **字段**：
  - `id`（主键）
  - `student_id`（外键，引用 `students.id`）
  - `course_name`
  - `university_name`
  - `application_status`（例如，审核中、接受、拒绝）
  - `submitted_at`
  - `created_at`, `updated_at`

### 3. 签证申请表
- 跟踪学生的签证申请过程。
- **字段**：
  - `id`（主键）
  - `student_id`（外键，引用 `students.id`）
  - `visastatus`（例如，待处理、批准、拒绝）
  - `visasubmissiondate`
  - `created_at`, `updated_at`

### 4. 发票表
- 管理学生为咨询服务支付的款项。
- **字段**：
  - `id`（主键）
  - `student_id`（外键，引用 `students.id`）
  - `amount`
  - `payment_status`（例如，已支付、待支付）
  - `due_date`
  - `created_at`, `updated_at`

### 5. 用户表
- 存储系统内不同角色的用户信息（例如，管理员、顾问、签证专家）。
- **字段**：
  - `id`（主键）
  - `name`
  - `email`
  - `password`
  - `role`（例如，管理员、顾问）
  - `created_at`, `updated_at`

### 6. 角色和权限
- 基于角色的访问控制（RBAC）用于定义每个用户角色可以执行的操作。
- **表**：
  - `roles`：存储用户角色（例如，管理员、顾问、财务官）。
  - `permissions`：定义每个角色的具体权限。
  - `role_user`：连接用户和角色的枢纽表。

### 7. 通知表
- 存储发送给学生或工作人员的通知。
- **字段**：
  - `id`（主键）
  - `recipient_id`（外键，引用用户或学生）
  - `message`
  - `status`（发送、待处理）
  - `created_at`, `updated_at`

### 关系
- **一对多**：
  - 一个学生可以有多个申请、签证申请和发票。
  - 一个用户（顾问/管理员）可以管理多个学生。
- **多对多**：
  - 用户可以有多个角色（通过 `role_user` 表）。
- **外键约束**：
  - 外键确保表间数据一致性，例如 `student_id` 将学生链接到他们的申请、发票和签证申请。

### ER 图
实体-关系（ER）图提供数据库模式和关系的可视化表示。（你可以在这里包含实际的 ER 图作为图像或链接到图表。）

## 环境变量
运行此项目，你需要设置以下环境变量。这些通常在 Laravel 项目根目录的 `.env` 文件中定义。

### Laravel 后端环境变量
- `APP_NAME`：你的应用名称（例如，“CRM 系统”）。
- `APP_ENV`：应用运行的环境（`local`、`production` 等）。
- `APP_KEY`：加密密钥，使用 `php artisan key:generate` 生成。
- `APP_DEBUG`：设置为 `true` 或 `false` 以启用或禁用调试模式。
- `APP_URL`：应用的基 URL（例如，`http://localhost`）。

### 数据库配置
- `DB_CONNECTION`：数据库驱动（例如，`mysql`）。
- `DB_HOST`：数据库主机（例如，`127.0.0.1`）。
- `DB_PORT`：数据库运行的端口（例如，MySQL 的 `3306`）。
- `DB_DATABASE`：数据库名称。
- `DB_USERNAME`：数据库用户名。
- `DB_PASSWORD`：数据库密码。

### 邮件配置
- `MAIL_MAILER`：邮件驱动（例如，`smtp`）。
- `MAIL_HOST`：用于电子邮件服务的 SMTP 主机。
- `MAIL_PORT`：SMTP 端口。
- `MAIL_USERNAME`：电子邮件用户名。
- `MAIL_PASSWORD`：电子邮件密码。
- `MAIL_ENCRYPTION`：电子邮件的加密方法（`tls` 或 `ssl`）。
- `MAIL_FROM_ADDRESS`：外发电子邮件的“发件人”地址。
- `MAIL_FROM_NAME`：外发电子邮件的“发件人”名称。

### API 密钥和外部服务
- `STRIPE_KEY`：Stripe 支付集成的 API 密钥（如果使用）。
- `STRIPE_SECRET`：Stripe 支付的秘密密钥。
- `AWS_ACCESS_KEY_ID`：使用 Amazon Web Services 的 AWS 访问密钥（如果使用）。
- `AWS_SECRET_ACCESS_KEY`：AWS 秘密密钥。
- `AWS_DEFAULT_REGION`：AWS 区域（例如，us-east-1）。

### 其他服务（可选）
- `PUSHER_APP_ID`：Pusher App ID，用于实时通知。
- `PUSHER_APP_KEY`：Pusher App Key。
- `PUSHER_APP_SECRET`：Pusher App Secret。
- `PUSHER_APP_CLUSTER`：Pusher 集群区域。

### 示例 .env 文件
```bash
APP_NAME=CRM系统
APP_ENV=local
APP_KEY=base64:...
APP_DEBUG=true
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=crm_database
DB_USERNAME=root
DB_PASSWORD=secret

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=example@crm.com
MAIL_FROM_NAME="${APP_NAME}"

STRIPE_KEY=your-stripe-key
STRIPE_SECRET=your-stripe-secret



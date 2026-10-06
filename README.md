# 合家云社区物业管理平台（后端）

基于 [RuoYi](http://ruoyi.vip) 脚手架二次开发的社区物业管理平台后端服务，提供系统管理能力与社区业务功能。

## 技术栈

| 类别 | 技术 |
|---|---|
| 核心框架 | Spring Boot 2.7.8、Spring Security、JWT（jjwt） |
| 持久层 | MyBatis-Plus 3.4.1、MyBatis、PageHelper 分页 |
| 数据库 | MySQL 8.0、Druid 连接池（含慢 SQL 监控） |
| 缓存 | Redis（Jedis 客户端） |
| 工具库 | EasyPOI（Excel 导入导出）、Lombok、Orika、FastJSON |
| 构建 | Maven、JDK 11 |

## 功能模块

### 认证与授权
- 登录 / 登出、图形验证码（Kaptcha）
- JWT 无状态认证：自定义 `JwtAuthenticationTokenFilter` 完成 Token 解析与用户上下文注入
- 基于 `@PreAuthorize` + 自定义权限表达式，实现**菜单级 / 按钮级**细粒度权限控制

### 系统管理
- 用户、角色、菜单（动态路由）、部门、岗位、数据字典、区域管理
- 基于 RBAC 模型：`sys_user` / `sys_role` / `sys_menu` + 两张关联表

### 业务模块
- 社区信息管理：增删改查、多条件分页查询、Excel 批量导入导出

### 通用能力
- 统一响应体（`BaseResponse` + `ResultCode`）与全局异常处理（`@RestControllerAdvice`）
- MyBatis-Plus 公共字段自动填充（`MetaObjectHandler`）、雪花 ID 主键策略
- Druid 慢 SQL 监控（阈值 1s）

## 快速开始

### 1. 环境要求

- JDK 11
- Maven 3.6+
- MySQL 8.0
- Redis 5.0+

### 2. 初始化数据库

```sql
CREATE DATABASE hejiayun_community DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

然后导入项目 `sql/` 目录下的初始化脚本。

### 3. 配置敏感信息

项目通过**环境变量**注入敏感配置，避免明文写入代码库：

| 环境变量 | 说明 | 默认值 |
|---|---|---|
| `MYSQL_USERNAME` | 数据库用户名 | root |
| `MYSQL_PASSWORD` | 数据库密码 | 123456 |
| `JWT_SECRET` | JWT 签名密钥 | please-change-me |

Windows PowerShell 设置方式：

```powershell
$env:MYSQL_USERNAME="root"
$env:MYSQL_PASSWORD="你的密码"
$env:JWT_SECRET="你的随机密钥"
```

### 4. 启动项目

```bash
mvn spring-boot:run
```

启动后访问：<http://localhost:8080>

## 项目结构

```
src/main/java/com/msb/hjycommunity
├── common       公共模块（统一响应、全局异常、分页、常量、工具类）
├── framework    框架配置（Spring Security、Redis、资源处理）
├── system       系统管理模块（用户/角色/菜单/部门/岗位/字典/区域）
├── community    社区业务模块
└── web          接口层（Controller）
```

## 说明

本项目为学习实践项目，基础权限框架与系统管理能力来自 RuoYi 脚手架，业务模块与部分通用能力为在此基础上的二次开发。

## 作者

薛煜坚

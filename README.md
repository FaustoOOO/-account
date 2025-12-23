# 智能记账系统

一个前后端分离的智能记账系统，基于 Spring Boot 3.2.4 和 Vue 3 开发，严格按照用例规约文档实现，参考 GnuCash 开源项目的设计理念。

## 📋 目录

- [项目简介](#项目简介)
- [技术栈](#技术栈)
- [功能模块](#功能模块)
- [项目结构](#项目结构)
- [快速开始](#快速开始)
- [API 接口文档](#api-接口文档)
- [数据库配置](#数据库配置)
- [测试说明](#测试说明)
- [开发指南](#开发指南)
- [常见问题](#常见问题)
- [参考文档](#参考文档)

## 📖 项目简介

智能记账系统是一个企业级财务管理系统，提供完整的会计核算、凭证管理、报表生成、税务申报等功能。系统采用前后端分离架构，后端基于 Spring Boot 提供 RESTful API，前端基于 Vue 3 提供现代化的用户界面。

### 核心特性

- ✅ **完整的会计核算功能** - 支持会计科目管理、凭证录入、过账等核心功能
- ✅ **严格的业务规则校验** - 借贷平衡、科目唯一性、状态流转等规则自动校验
- ✅ **灵活的报表生成** - 支持资产负债表、利润表等财务报表生成
- ✅ **税务管理** - 支持增值税计算和税务申报
- ✅ **采购销售管理** - 完整的采购订单和销售订单管理流程
- ✅ **银行对账** - 支持银行对账单导入和自动匹配
- ✅ **前后端分离** - 清晰的架构设计，便于维护和扩展

## 🛠 技术栈

### 后端技术

- **框架**: Spring Boot 3.2.4
- **语言**: Java 17
- **构建工具**: Maven
- **数据库**: H2 Embedded Database (内存数据库)
- **ORM**: Spring Data JPA
- **API**: RESTful API
- **其他**: Lombok, Spring Boot DevTools

### 前端技术

- **框架**: Vue 3 (Composition API)
- **UI 库**: Element Plus
- **HTTP 客户端**: Axios
- **路由**: Vue Router 4
- **构建工具**: Vite
- **开发语言**: JavaScript

## 📦 功能模块

系统包含以下 10 个核心业务模块：

### 1. 会计科目管理 (UC001)

- **功能**: 科目树形展示、新增、修改、删除、启用/禁用
- **特性**:
  - 支持多级科目结构
  - 科目编码唯一性校验
  - 科目余额实时显示
  - 树形结构可视化展示

### 2. 记账凭证 (UC002)

- **功能**: 凭证录入、借贷平衡校验、凭证审核
- **特性**:
  - 自动生成凭证编号
  - 实时借贷平衡校验
  - 凭证状态流转（已保存 → 待审核 → 已审核 → 已过账）
  - 支持多分录录入

### 3. 凭证过账 (UC003)

- **功能**: 批量过账操作、科目余额更新
- **特性**:
  - 仅已审核凭证可过账
  - 批量选择过账
  - 自动更新科目余额
  - 过账后凭证不可修改

### 4. 银行对账 (UC004)

- **功能**: 对账单导入、自动匹配、手工对账
- **特性**:
  - 支持对账期间设置
  - 自动匹配规则（金额+结算方式+票号）
  - 未达账项标记
  - 银行余额调节表生成

### 5. 供货商管理 (UC005)

- **功能**: 供货商信息管理、搜索、启用/禁用
- **特性**:
  - 供货商编码唯一性
  - 支持多条件搜索
  - 供货商详情查看
  - 供货商分类管理

### 6. 采购订单管理 (UC006)

- **功能**: 订单创建、审批流程、订单明细管理
- **特性**:
  - 订单审批流程（待审批 → 已批准）
  - 订单明细自动计算
  - 订单状态跟踪
  - 供货商关联

### 7. 客户管理 (UC009)

- **功能**: 客户信息管理、客户分级、信用管理
- **特性**:
  - 客户编码唯一性
  - 客户等级分类（A/B/C）
  - 信用额度管理
  - 客户类型分类（企业/个人/政府）

### 8. 销售订单管理 (UC010)

- **功能**: 销售单创建、审核流程、发货跟踪
- **特性**:
  - 订单审核流程（待审核 → 已审核/已拒绝）
  - 折扣率支持
  - 应收总额计算
  - 发货状态跟踪

### 9. 财务报表 (UC007)

- **功能**: 资产负债表、利润表生成
- **特性**:
  - 支持自定义报表期间
  - 可选择包含未过账凭证
  - 报表数据汇总
  - 科目余额明细展示

### 10. 税务申报 (UC011)

- **功能**: 增值税计算、税务申报
- **特性**:
  - 自动计算销项税额和进项税额
  - 应纳税额计算
  - 申报状态跟踪
  - 申报记录管理

## 📁 项目结构

```
account/
├── backend/                          # 后端 Spring Boot 项目
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/accounting/
│   │   │   │   ├── AccountingApplication.java    # 主启动类
│   │   │   │   ├── config/                        # 配置类
│   │   │   │   │   └── CorsConfig.java           # CORS 配置
│   │   │   │   ├── controller/                   # REST 控制器
│   │   │   │   │   ├── AccountController.java
│   │   │   │   │   ├── VoucherController.java
│   │   │   │   │   ├── SupplierController.java
│   │   │   │   │   ├── CustomerController.java
│   │   │   │   │   ├── PurchaseOrderController.java
│   │   │   │   │   ├── SalesOrderController.java
│   │   │   │   │   ├── BankReconciliationController.java
│   │   │   │   │   ├── FinancialReportController.java
│   │   │   │   │   └── TaxController.java
│   │   │   │   ├── service/                      # 业务逻辑层
│   │   │   │   │   ├── AccountService.java
│   │   │   │   │   ├── VoucherService.java
│   │   │   │   │   └── ... (其他 Service)
│   │   │   │   ├── repository/                   # 数据访问层
│   │   │   │   │   ├── AccountRepository.java
│   │   │   │   │   ├── VoucherRepository.java
│   │   │   │   │   └── ... (其他 Repository)
│   │   │   │   ├── entity/                       # 实体类
│   │   │   │   │   ├── Account.java
│   │   │   │   │   ├── Voucher.java
│   │   │   │   │   ├── VoucherEntry.java
│   │   │   │   │   └── ... (其他 Entity)
│   │   │   │   └── dto/                          # 数据传输对象
│   │   │   │       ├── AccountDTO.java
│   │   │   │       ├── VoucherDTO.java
│   │   │   │       └── VoucherEntryDTO.java
│   │   │   └── resources/
│   │   │       └── application.yml               # 应用配置
│   │   └── test/                                 # 测试代码
│   │       ├── java/com/accounting/
│   │       │   ├── AccountServiceTest.java
│   │       │   ├── VoucherServiceTest.java
│   │       │   └── ... (其他测试类)
│   │       └── resources/
│   │           └── application-test.yml
│   ├── pom.xml                                   # Maven 配置
│   ├── start.bat                                # Windows 启动脚本
│   └── run-tests.bat                            # 测试脚本
│
├── frontend/                                     # 前端 Vue 项目
│   ├── src/
│   │   ├── views/                               # 页面组件
│   │   │   ├── AccountManagement.vue            # 会计科目管理
│   │   │   ├── VoucherManagement.vue            # 记账凭证
│   │   │   ├── VoucherPosting.vue               # 凭证过账
│   │   │   ├── BankReconciliation.vue           # 银行对账
│   │   │   ├── SupplierManagement.vue           # 供货商管理
│   │   │   ├── PurchaseOrderManagement.vue       # 采购订单
│   │   │   ├── CustomerManagement.vue            # 客户管理
│   │   │   ├── SalesOrderManagement.vue         # 销售订单
│   │   │   ├── FinancialReports.vue              # 财务报表
│   │   │   └── TaxDeclaration.vue                # 税务申报
│   │   ├── layout/                              # 布局组件
│   │   │   └── Layout.vue                       # 主布局
│   │   ├── router/                              # 路由配置
│   │   │   └── index.js
│   │   ├── utils/                               # 工具类
│   │   │   └── axios.js                         # Axios 配置
│   │   ├── App.vue                              # 根组件
│   │   └── main.js                              # 入口文件
│   ├── index.html                               # HTML 模板
│   ├── package.json                             # npm 配置
│   ├── vite.config.js                           # Vite 配置
│   └── start.bat                                # Windows 启动脚本
│
├── README.md                                    # 项目说明文档
├── API_INTEGRATION_REPORT.md                   # API 对接报告
├── TEST_SUMMARY.md                             # 测试总结
├── TEST_RESULTS.md                             # 测试结果
└── 用例规约.md                                  # 用例规约文档
```

## 🚀 快速开始

### 环境要求

- **JDK**: 17 或更高版本
- **Maven**: 3.6 或更高版本
- **Node.js**: 16 或更高版本
- **npm**: 8 或更高版本

### 后端启动

#### 方式一：使用 Maven 命令

```bash
# 进入后端目录
cd backend

# 启动 Spring Boot 应用
mvn spring-boot:run
```

#### 方式二：使用启动脚本（Windows）

```bash
# 双击运行或命令行执行
backend\start.bat
```

后端服务将在 `http://localhost:8080` 启动，API 基础路径为 `http://localhost:8080/api`

### 前端启动

#### 方式一：使用 npm 命令

```bash
# 进入前端目录
cd frontend

# 安装依赖（首次运行）
npm install

# 启动开发服务器
npm run dev
```

#### 方式二：使用启动脚本（Windows）

```bash
# 双击运行或命令行执行
frontend\start.bat
```

前端服务将在 `http://localhost:3000` 启动

### 访问系统

启动成功后，在浏览器中访问：`http://localhost:3000`

## 📡 API 接口文档

### 基础路径

所有 API 的基础路径为：`http://localhost:8080/api`

### 主要接口列表

#### 会计科目管理

- `GET /accounts/tree` - 获取树形科目列表
- `GET /accounts` - 获取所有科目
- `GET /accounts/{id}` - 获取科目详情
- `POST /accounts` - 新增科目
- `PUT /accounts/{id}` - 修改科目
- `DELETE /accounts/{id}` - 删除科目

#### 记账凭证

- `GET /vouchers` - 获取所有凭证
- `GET /vouchers/pending-posting` - 获取待过账凭证
- `GET /vouchers/{id}` - 获取凭证详情
- `POST /vouchers` - 新增凭证
- `PUT /vouchers/{id}` - 修改凭证
- `POST /vouchers/{id}/approve` - 审核凭证
- `POST /vouchers/post` - 批量过账

#### 银行对账

- `GET /bank-reconciliations` - 获取所有对账记录
- `GET /bank-reconciliations/{id}` - 获取对账详情
- `POST /bank-reconciliations` - 新建对账
- `POST /bank-reconciliations/{id}/complete` - 完成对账

#### 供货商管理

- `GET /suppliers` - 获取所有供货商
- `GET /suppliers/enabled` - 获取启用的供货商
- `GET /suppliers/search?keyword={keyword}` - 搜索供货商
- `GET /suppliers/{id}` - 获取供货商详情
- `POST /suppliers` - 新增供货商
- `PUT /suppliers/{id}` - 修改供货商
- `DELETE /suppliers/{id}` - 删除供货商

#### 采购订单

- `GET /purchase-orders` - 获取所有采购订单
- `GET /purchase-orders/{id}` - 获取订单详情
- `POST /purchase-orders` - 新建订单
- `PUT /purchase-orders/{id}` - 修改订单
- `POST /purchase-orders/{id}/approve` - 审批订单

#### 客户管理

- `GET /customers` - 获取所有客户
- `GET /customers/enabled` - 获取启用的客户
- `GET /customers/search?keyword={keyword}` - 搜索客户
- `GET /customers/{id}` - 获取客户详情
- `POST /customers` - 新增客户
- `PUT /customers/{id}` - 修改客户
- `DELETE /customers/{id}` - 删除客户

#### 销售订单

- `GET /sales-orders` - 获取所有销售订单
- `GET /sales-orders/{id}` - 获取订单详情
- `POST /sales-orders` - 新建订单
- `PUT /sales-orders/{id}` - 修改订单
- `POST /sales-orders/{id}/approve` - 审核订单
- `POST /sales-orders/{id}/reject` - 拒绝订单

#### 财务报表

- `GET /reports/balance-sheet?reportDate={date}&includeUnposted={boolean}` - 生成资产负债表
- `GET /reports/income-statement?startDate={date}&endDate={date}` - 生成利润表

#### 税务申报

- `GET /tax` - 获取所有税务申报记录
- `GET /tax/{id}` - 获取申报详情
- `POST /tax/calculate-vat?period={period}&taxpayerId={id}&taxAuthority={authority}` - 计算增值税
- `POST /tax/{id}/submit` - 提交申报

## 💾 数据库配置

### H2 嵌入式数据库

系统使用 H2 嵌入式内存数据库，数据存储在内存中，重启后数据会清空。

#### H2 控制台访问

- **URL**: `http://localhost:8080/api/h2-console`
- **JDBC URL**: `jdbc:h2:mem:accountingdb`
- **用户名**: `sa`
- **密码**: (空)

#### 数据库配置

配置文件位置：`backend/src/main/resources/application.yml`

```yaml
spring:
  datasource:
    url: jdbc:h2:mem:accountingdb
    driver-class-name: org.h2.Driver
    username: sa
    password: 
  
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

## 🧪 测试说明

### 运行测试

#### 方式一：使用 Maven 命令

```bash
cd backend
mvn test
```

#### 方式二：使用测试脚本（Windows）

```bash
backend\run-tests.bat
```

### 测试覆盖

系统包含以下测试：

- ✅ **单元测试** - 所有 Service 层的业务逻辑测试
- ✅ **集成测试** - Controller 层集成测试
- ✅ **业务规则测试** - 借贷平衡、唯一性校验等

### 测试文件

- `AccountServiceTest.java` - 会计科目服务测试
- `VoucherServiceTest.java` - 凭证服务测试
- `SupplierServiceTest.java` - 供货商服务测试
- `CustomerServiceTest.java` - 客户服务测试
- `PurchaseOrderServiceTest.java` - 采购订单服务测试
- `SalesOrderServiceTest.java` - 销售订单服务测试
- `FinancialReportServiceTest.java` - 财务报表服务测试
- `TaxServiceTest.java` - 税务服务测试
- `BankReconciliationServiceTest.java` - 银行对账服务测试
- `IntegrationTest.java` - 集成测试

详细测试说明请参考：`backend/TEST_GUIDE.md`

## 💻 开发指南

### 核心业务规则

系统严格按照用例规约文档实现，包含以下核心业务规则：

1. **会计科目编码唯一性** - 科目编码必须在系统内保持唯一
2. **凭证借贷平衡** - 任何凭证必须满足"有借必有贷，借贷必相等"
3. **凭证状态流转** - 已保存 → 待审核 → 已审核 → 已过账
4. **过账限制** - 只有已审核的凭证才能过账
5. **过账后不可修改** - 已过账的凭证不能修改或删除
6. **订单审批流程** - 采购订单和销售订单需要审批流程
7. **报表数据来源** - 财务报表基于已过账凭证数据生成

### 代码规范

- **后端**: 遵循 Spring Boot 最佳实践，使用分层架构（Controller → Service → Repository）
- **前端**: 使用 Vue 3 Composition API，组件化开发
- **命名规范**: 遵循 Java 和 JavaScript 命名规范

### 前后端对接

所有前后端 API 对接已完成，详细说明请参考：`API_INTEGRATION_REPORT.md`

主要修复内容：
- ✅ 日期格式统一处理
- ✅ 参数传递方式修正
- ✅ 数据格式匹配优化
- ✅ 树形结构支持

## ❓ 常见问题

### 1. 后端启动失败

**问题**: 端口被占用或 JDK 版本不匹配

**解决**:
- 检查端口 8080 是否被占用
- 确认 JDK 版本为 17 或更高
- 检查 `application.yml` 配置是否正确

### 2. 前端无法连接后端

**问题**: CORS 错误或代理配置问题

**解决**:
- 确认后端服务已启动
- 检查 `vite.config.js` 中的代理配置
- 确认后端 CORS 配置正确

### 3. 数据库连接失败

**问题**: H2 数据库配置错误

**解决**:
- 检查 `application.yml` 中的数据库配置
- 确认 H2 依赖已正确添加
- 查看控制台错误日志

### 4. 测试失败

**问题**: 测试环境配置问题

**解决**:
- 确认 `application-test.yml` 配置正确
- 检查测试数据库配置
- 查看测试日志定位问题

### 5. 日期格式错误

**问题**: 前后端日期格式不匹配

**解决**:
- 前端已统一处理日期格式转换
- 后端使用 `LocalDate` 类型
- 日期格式为 `YYYY-MM-DD`

## 📚 参考文档

### 项目文档

- `用例规约.md` - 详细的用例规约文档
- `API_INTEGRATION_REPORT.md` - 前后端 API 对接报告
- `TEST_SUMMARY.md` - 测试总结报告
- `TEST_RESULTS.md` - 测试结果报告
- `backend/TEST_GUIDE.md` - 测试指南

### 技术文档

- [Spring Boot 官方文档](https://spring.io/projects/spring-boot)
- [Vue 3 官方文档](https://vuejs.org/)
- [Element Plus 文档](https://element-plus.org/)
- [H2 Database 文档](https://www.h2database.com/html/main.html)

### 参考项目

- [GnuCash](https://www.gnucash.org/) - 开源财务管理软件

## 📄 许可证

本项目仅供学习和研究使用。

## 👥 贡献

欢迎提交 Issue 和 Pull Request！

## 📞 联系方式

如有问题或建议，请提交 Issue。

---

**最后更新**: 2024年

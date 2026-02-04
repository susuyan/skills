# 一人公司运作技能规划

本文档规划将"一人公司运作"拆分为多个独立的 Claude Code 技能模块。

## 设计原则

- **单一职责**: 每个技能专注一个业务领域
- **可组合**: 技能之间可以配合使用
- **渐进式**: 从核心需求开始，逐步扩展
- **实用性**: 优先解决高频痛点

---

## 技能规划总览

| 优先级 | 技能名称 | 领域 | 核心功能 |
|--------|----------|------|----------|
| P0 | `biz-invoice` | 财务 | 发票生成与管理 |
| P0 | `biz-contract` | 法务 | 合同模板与生成 |
| P0 | `biz-client` | 客户 | 客户信息与沟通管理 |
| P1 | `biz-finance` | 财务 | 收支记账与报表 |
| P1 | `biz-project` | 项目 | 项目跟踪与交付 |
| P1 | `biz-proposal` | 商务 | 报价单与提案生成 |
| P2 | `biz-tax` | 财务 | 税务计算与申报提醒 |
| P2 | `biz-content` | 营销 | 内容创作与发布 |
| P2 | `biz-legal` | 法务 | 隐私政策/服务条款生成 |
| P3 | `biz-analytics` | 运营 | 业务数据分析与洞察 |
| P3 | `biz-automation` | 效率 | 工作流自动化 |

---

## P0 - 核心技能（立即需要）

### 1. `biz-invoice` - 发票管理

**痛点**: 手动制作发票耗时，格式不统一，难以追踪

**功能**:
| 命令 | 说明 |
|------|------|
| `/biz-invoice create` | 创建新发票 |
| `/biz-invoice list` | 列出所有发票 |
| `/biz-invoice status <id>` | 查看/更新发票状态（待付/已付） |
| `/biz-invoice template` | 管理发票模板 |
| `/biz-invoice export <id>` | 导出为 PDF/Markdown |

**数据存储**: `~/.claude/biz/invoices/`

**输出示例**:
```
发票 #2026-001
客户: ABC 公司
金额: ¥15,000
状态: 待付款
到期: 2026-02-15
```

---

### 2. `biz-contract` - 合同管理

**痛点**: 每次都要从头写合同，条款容易遗漏

**功能**:
| 命令 | 说明 |
|------|------|
| `/biz-contract new <type>` | 基于模板创建合同（服务/NDA/外包） |
| `/biz-contract list` | 列出所有合同 |
| `/biz-contract sign <id>` | 记录签署状态 |
| `/biz-contract renew <id>` | 续签提醒 |
| `/biz-contract template add` | 添加自定义模板 |

**内置模板**:
- 服务协议（SaaS/咨询/开发）
- 保密协议（NDA）
- 外包协议
- 顾问协议

**数据存储**: `~/.claude/biz/contracts/`

---

### 3. `biz-client` - 客户管理

**痛点**: 客户信息散落各处，沟通记录难以追溯

**功能**:
| 命令 | 说明 |
|------|------|
| `/biz-client add` | 添加新客户 |
| `/biz-client list` | 列出所有客户 |
| `/biz-client show <name>` | 查看客户详情 |
| `/biz-client note <name>` | 添加沟通记录 |
| `/biz-client tag <name> <tag>` | 标签分类 |

**客户档案包含**:
- 基本信息（公司名、联系人、邮箱、电话）
- 业务标签（行业、规模、来源）
- 沟通历史
- 关联合同/发票

**数据存储**: `~/.claude/biz/clients/`

---

## P1 - 重要技能（近期需要）

### 4. `biz-finance` - 财务记账

**痛点**: 收支不清晰，现金流无法预测

**功能**:
| 命令 | 说明 |
|------|------|
| `/biz-finance income <amount>` | 记录收入 |
| `/biz-finance expense <amount>` | 记录支出 |
| `/biz-finance report [month]` | 生成月度报表 |
| `/biz-finance cashflow` | 现金流预测 |
| `/biz-finance category` | 管理收支分类 |

**报表输出**:
```
2026年1月财务报表
==================
收入: ¥45,000
支出: ¥12,300
净利: ¥32,700

收入来源:
  - 咨询服务: ¥30,000 (67%)
  - 产品销售: ¥15,000 (33%)

支出分类:
  - 工具订阅: ¥2,500
  - 办公费用: ¥800
  - ...
```

---

### 5. `biz-project` - 项目管理

**痛点**: 多项目并行时容易遗漏，交付节点不清晰

**功能**:
| 命令 | 说明 |
|------|------|
| `/biz-project new` | 创建项目 |
| `/biz-project list` | 列出进行中项目 |
| `/biz-project milestone <name>` | 管理里程碑 |
| `/biz-project log <name>` | 记录工作日志 |
| `/biz-project deliver <name>` | 标记交付 |

**与其他技能联动**:
- 关联客户（biz-client）
- 关联合同（biz-contract）
- 关联发票（biz-invoice）

---

### 6. `biz-proposal` - 提案与报价

**痛点**: 报价单格式混乱，提案写作耗时

**功能**:
| 命令 | 说明 |
|------|------|
| `/biz-proposal quote` | 生成报价单 |
| `/biz-proposal pitch` | 生成项目提案 |
| `/biz-proposal template` | 管理模板 |
| `/biz-proposal history` | 查看历史报价 |

---

## P2 - 扩展技能（按需添加）

### 7. `biz-tax` - 税务助手

**功能**:
- 税务计算（增值税、所得税）
- 季度申报提醒
- 可抵扣项目记录
- 年度汇算清缴辅助

### 8. `biz-content` - 内容营销

**功能**:
- 博客文章草稿
- 社交媒体内容
- Newsletter 编写
- SEO 关键词建议

### 9. `biz-legal` - 法律文档

**功能**:
- 隐私政策生成
- 服务条款生成
- 退款政策
- GDPR/合规声明

---

## P3 - 高级技能（未来考虑）

### 10. `biz-analytics` - 业务分析

**功能**:
- 客户价值分析（LTV）
- 收入趋势分析
- 项目利润率分析
- 时间投入分析

### 11. `biz-automation` - 自动化工作流

**功能**:
- 定期发票提醒
- 合同到期提醒
- 收款确认流程
- 客户跟进提醒

---

## 数据架构

所有业务数据统一存储在 `~/.claude/biz/` 目录下：

```
~/.claude/biz/
├── config.json          # 全局配置（公司信息、默认设置）
├── clients/             # 客户数据
│   ├── index.json       # 客户索引
│   └── <client-id>.json # 单个客户详情
├── invoices/            # 发票数据
│   ├── index.json
│   └── <year>/
│       └── <invoice-id>.json
├── contracts/           # 合同数据
│   ├── index.json
│   └── <contract-id>.json
├── finance/             # 财务数据
│   ├── transactions.json
│   └── reports/
├── projects/            # 项目数据
│   ├── index.json
│   └── <project-id>/
└── templates/           # 自定义模板
    ├── invoice/
    ├── contract/
    └── proposal/
```

---

## 技能间关联

```
                    ┌─────────────┐
                    │ biz-client  │
                    └──────┬──────┘
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
         ▼                 ▼                 ▼
┌─────────────┐   ┌─────────────┐   ┌─────────────┐
│biz-proposal │──▶│biz-contract │──▶│ biz-project │
└─────────────┘   └──────┬──────┘   └──────┬──────┘
                         │                 │
                         ▼                 ▼
                  ┌─────────────┐   ┌─────────────┐
                  │ biz-invoice │──▶│ biz-finance │
                  └─────────────┘   └─────────────┘
```

**典型工作流**:
1. 新客户咨询 → `biz-client add`
2. 发送报价 → `biz-proposal quote`
3. 签订合同 → `biz-contract new`
4. 创建项目 → `biz-project new`
5. 交付结算 → `biz-invoice create`
6. 记账入账 → `biz-finance income`

---

## 实施建议

### 第一阶段（1-2周）
- 实现 `biz-invoice` 和 `biz-client`
- 建立基础数据结构
- 设计统一的 CLI 交互模式

### 第二阶段（2-4周）
- 实现 `biz-contract` 和 `biz-proposal`
- 添加模板系统
- 实现技能间数据关联

### 第三阶段（4-6周）
- 实现 `biz-finance` 和 `biz-project`
- 添加报表功能
- 优化用户体验

### 后续迭代
- 根据实际使用反馈调整
- 添加 P2/P3 技能
- 考虑数据导出/同步功能

---

## 下一步

1. 确认技能优先级是否符合你的需求
2. 讨论具体技能的细节设计
3. 开始实现第一个技能（建议从 `biz-invoice` 开始）

你觉得这个规划如何？有什么需要调整的地方吗？

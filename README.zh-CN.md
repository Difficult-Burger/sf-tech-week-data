# sf-tech-week-data

[English](README.md) | **中文**

**SF Tech Week 2026**（10 月 5–11 日，旧金山）的开放数据：官方日历上的全部活动，以及活动页上列出的主办方和演讲嘉宾。内容与 [techweek.wiki](https://techweek.wiki) 指南页面上显示的信息一致，不多不少。

**这是最终快照（v1.0）。** 活动周已经结束，数据不会再更新。如需固定版本，请引用 [v1.0 版本](../../releases/tag/v1.0)。

## 文件

| 文件 | 行数 | 内容 |
|---|---|---|
| `events.jsonl` / `events.csv` | 1,593 | 每行一场活动 |
| `people.jsonl` / `people.csv` | 3,424 | 每行一个人 |
| `event_people.csv` | 3,994 | 谁出现在哪场活动上（CSV 之间的关联表） |
| `metadata.json` | | 快照生成时间和行数 |

JSONL 和 CSV 的数据完全相同。CSV 中的列表（标签）用 `; ` 连接；活动的人物不以嵌套列表出现，而是放在 `event_people.csv` 里。

## `events`（活动）

| 字段 | 含义 |
|---|---|
| `id` | 稳定的活动 id（即官方日历的 id） |
| `title`、`headline` | 列出的活动名称；一句话概括 |
| `summary` | 主办方自己写的开头段落；如果原页面没有，或只有官方日历的模板句，则为 `null` |
| `date`、`start`、`end` | 日期，以及旧金山时间的 ISO 8601 时间戳（带时区偏移，未知时为 `null`） |
| `area`、`address` | 街区；只有主办方公开了地址时才有街道地址 |
| `host` | 列出的主办方名称 |
| `registration` | `RSVP`、`Application`（申请制）或 `Unknown`；申请制时 `needsApproval` 为 `true` |
| `availability` | 抓取时的状态：`SoldOut`（已满）、`LimitedAvailability`（名额有限）或 `null` |
| `rsvpCount` | 抓取时的报名人数，或 `null` |
| `intents`、`topics`、`formats` | 标签：参加者可能的目的、主题领域、活动形式 |
| `people`（JSONL）/ `peopleCount`（CSV） | 活动上列出的主办方和演讲嘉宾：`[{name, role, title, company, profile}]` |
| `url` | 主办方的公开页面（报名或申请入口，以及完整的活动介绍） |

## `people`（人物）

| 字段 | 含义 |
|---|---|
| `id` | 本快照内的稳定 id，供 `event_people.csv` 关联使用 |
| `name`、`title`、`company` | 公开信息或匹配结果；`title`/`company` 可能为 `null` |
| `profile` | 公开主页链接：LinkedIn（2,587）、Partiful 主办方页面（259）、个人网站（75），或 `null`（503） |
| `events`（JSONL）/ `eventCount`（CSV） | 此人出现的活动及其角色（`host` 主办方或 `speaker` 演讲嘉宾） |

同一个人按主页链接合并；没有链接时按姓名加公司合并。刻意不包含个人简介和联系方式。

## 数据是怎么来的

- **活动：** 以 2026-10-04 的 SF Tech Week 官方日历为准，并补充了每场活动的公开报名页面（大多是 Partiful）。标题和时间以官方日历为准。
- **人物：** 活动页面上列出的主办方和演讲嘉宾，**不是参会者**。主页链接通过搜索公开来源匹配后经过复核；匹配把握不足的宁可不填，也不猜。
- **标签：** 根据活动列表中的关键词和标签匹配得出，不是主办方自己选的分类。

## 已知局限

- 活动周期间时间、入场方式和名额都有变化，请务必以主办方页面（`url`）为准。
- `rsvpCount` 是活动周开始前的一次抓取，不是最终到场人数。
- 2026-10-04 之前已下架的活动、以及之后新增的活动不在其中。
- 主页匹配可能出错，常见姓名尤其如此。发现错误请反馈（见下文）。
- 不包含活动介绍原文，因为其版权属于主办方；`url` 链接到原文。

## 纠错与删除

发现错误，或者你被列在其中并希望删除？请提交 issue，写明活动或人物的 id；如果是纠错，请附上信息来源链接。删除请求一律照办，不问理由。

## 许可

数据采用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 许可，请署名 "sf-tech-week-data"。活动名称归各主办方所有。本项目为独立项目，与 SF Tech Week 及其主办方无关联，也未获其认可。

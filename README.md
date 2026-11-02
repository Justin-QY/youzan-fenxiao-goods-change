# youzan-fenxiao-goods-change

有赞「分销商品 → 商品变更通知」批量处理 Skill，供 WorkBuddy / Claude Code 等支持
Skill 机制的 Agent 使用。

## 能力

按变更类型自动分流处理：

| 变更类型 | 判定依据（操作列 DOM） | 处理 |
|---|---|---|
| 描述 / 服务 / 其他变更 | `查看 → 忽略` | 忽略（可整页批量） |
| 状态变更·已失效 | `删除 → 忽略` | 删除分销商品 |
| 价格变更 | `编辑` | 按 40% 毛利率改价 |
| 状态变更·重新上架 | `查看 → 一键更新` | 一键更新 |

## 安装

把本目录放到 Skill 目录下即可：

```
# 用户级（所有项目生效）
~/.workbuddy/skills/youzan-fenxiao-goods-change/

# 项目级
<项目>/.workbuddy/skills/youzan-fenxiao-goods-change/
```

Windows 路径：`C:\Users\<用户名>\.workbuddy\skills\youzan-fenxiao-goods-change\`

## 要点速览

- **必须用 Edge 扩展浏览器**，内置浏览器在这套页面上点击会失效
- 改价公式：`售价 = 供货价 ÷ 0.6`（40% 毛利率）
- 触顶（提示「价格最大不能超过 X」）后毛利率仍低于 75% 的：多 SKU 商品取消该
  SKU 的「是否销售」；单 SKU 或全 SKU 触顶则整品删除
- 点「保存并查看」后不能立刻跳转，否则保存被打断
- 点「删除」后要等 1 秒再取 DOM 快照才能拿到确认按钮
- 连续操作几十次后点击层会假死，关标签页重开即可

详细步骤、坑位与验收标准见 [SKILL.md](./SKILL.md)。

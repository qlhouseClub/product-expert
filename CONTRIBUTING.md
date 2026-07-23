# 贡献指南

感谢你帮助改进 Product Expert。

## 先确定变更属于哪一层

- 专业能力：修改 `SKILL.md` 或 `references/`
- OpenAI 展示元数据：修改 `agents/openai.yaml`
- 扣子行为桥接：修改 `platforms/coze/agent-prompt.md`
- 平台名称、版本与描述：修改 `platforms/manifest.json`
- 平台构建逻辑：修改 `scripts/build_compat.py`

不要手工编辑或提交 `dist/`。所有平台包必须从仓库中的唯一知识源重新生成。

## 贡献要求

1. 说明要支持的真实决策、用户结果或失败模式，不只增加框架名词。
2. 区分事实、来源、推断和建议；对时效性信息记录核验日期。
3. 新增方法必须写清适用边界、反例和验证方式。
4. 不提交客户资料、访问凭据、内部指标、受限研究材料或未经许可的第三方内容。
5. 引用外部项目时保留原始链接与许可边界，不复制大段受版权保护内容。

## 本地验证

```powershell
python .\scripts\build_compat.py --platform all
```

提交前确认：

- `SKILL.md` 的名称与 `platforms/manifest.json` 一致
- 所有本地 Markdown 引用存在
- JSON 与 YAML 可以解析
- TRAE、OpenAI、扣子和便携包均能生成
- `git diff --check` 无错误

请使用不暴露私人邮箱的 Git 提交地址。安全问题按照 [SECURITY.md](SECURITY.md) 私密报告。

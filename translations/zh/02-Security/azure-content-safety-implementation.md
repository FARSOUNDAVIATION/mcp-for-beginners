<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1b6c746d9e190deba4d8765267ffb94e",
  "translation_date": "2025-07-16T23:14:16+00:00",
  "source_file": "02-Security/azure-content-safety-implementation.md",
  "language_code": "zh"
}
-->
# 在 MCP 中实现 Azure 内容安全

为了增强 MCP 对提示注入、工具中毒及其他 AI 特有漏洞的防护，强烈建议集成 Azure 内容安全。

## 与 MCP 服务器的集成

要将 Azure 内容安全集成到 MCP 服务器中，请在请求处理流程中将内容安全过滤器作为中间件添加：

1. 在服务器启动时初始化过滤器  
2. 在处理前验证所有传入的工具请求  
3. 在返回给客户端之前检查所有响应  
4. 对安全违规行为进行日志记录和警报  
5. 对内容安全检查失败的情况实施适当的错误处理  

这能有效防御：  
- 提示注入攻击  
- 工具中毒尝试  
- 通过恶意输入进行的数据泄露  
- 有害内容的生成  

## Azure 内容安全集成的最佳实践

1. **自定义黑名单**：针对 MCP 注入模式创建专用的自定义黑名单  
2. **严重性调节**：根据具体用例和风险承受能力调整严重性阈值  
3. **全面覆盖**：对所有输入和输出应用内容安全检查  
4. **性能优化**：考虑对重复的内容安全检查实现缓存机制  
5. **回退机制**：定义内容安全服务不可用时的明确回退行为  
6. **用户反馈**：当内容因安全原因被阻止时，向用户提供清晰反馈  
7. **持续改进**：根据新出现的威胁定期更新黑名单和检测模式

**免责声明**：  
本文件使用 AI 翻译服务 [Co-op Translator](https://github.com/Azure/co-op-translator) 进行翻译。虽然我们力求准确，但请注意自动翻译可能包含错误或不准确之处。原始文件的母语版本应被视为权威来源。对于重要信息，建议使用专业人工翻译。对于因使用本翻译而产生的任何误解或误释，我们不承担任何责任。
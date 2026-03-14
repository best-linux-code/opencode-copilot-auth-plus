# @best-linux-code/opencode-copilot-device-auth

GitHub Repository: https://github.com/best-linux-code/opencode-copilot-device-auth
Package on npm: https://www.npmjs.com/package/@best-linux-code/opencode-copilot-device-auth

This plugin is an enhanced OpenCode authentication provider for GitHub Copilot. It builds upon the official opencode-copilot-auth plugin, introducing major improvements in model metadata handling, authentication flow reliability, and support for advanced model features like Claude thinking budgets and Gemini reasoning efforts.

## Features

- API-Driven Model Metadata: Fetches real-time model context limits directly from the Copilot API. For example, it correctly identifies the 200K context limit for Claude Opus 4.6 instead of falling back to a static 128K limit.
- Dynamic Claude Thinking Budgets: Automatically generates low, medium, and high thinking_budget variants based on API-reported model capabilities.
- Dynamic Gemini Reasoning Efforts: Automatically generates low, medium, and high reasoning_effort variants based on API-reported model capabilities.
- Unified Headers: Implements consistent vscode-chat headers across all model families, including Claude, Gemini, GPT, and Grok.
- Enhanced Token Exchange: Features a two-level fallback mechanism (v2/token to copilot_internal/user) to ensure reliable authentication.
- Robust Device Flow: Implements the OAuth device code flow with proper handling for slow_down responses.
- Automatic Cleanup: Removes stale provider configurations from opencode.json upon logout.
- Debug Logging: Detailed response status and error body logging available at /tmp/copilot-device-auth.log.
- Zero Cost: Provides access to all available Copilot models at no additional cost.
- Future-Proof: Dynamically registers new models like claude-opus-4.6-1m if they are reported by the API.

## Model Limits Comparison

This plugin patches live per-model limits from Copilot, ensuring OpenCode uses accurate context window sizes.

| Model | This Plugin (Live) | static models.dev |
| --- | --- | --- |
| claude-opus-4.6 | 200,000 | 128,000 |
| claude-sonnet-4.6 | 200,000 | 128,000 |
| claude-haiku-4.5 | 144,000 | 128,000 |

## Installation

Install the package via npm:

```bash
npm install @best-linux-code/opencode-copilot-device-auth
```

Add the plugin to your opencode.json configuration:

```json
{
  "plugin": [
    "@best-linux-code/opencode-copilot-device-auth"
  ]
}
```

## Known Limitations

- Input Tokens Undefined: Some models (e.g., gpt-5, claude-opus-41) may display input=undefined because the Copilot API does not currently return max_prompt_tokens for these specific identifiers.
- Grok Initiator Error: The grok-code-fast-1 model may occasionally return an "invalid initiator" error. This is a known issue with the upstream Copilot API and is not a bug within this plugin.
- Duplicate Loader Calls: The internal CopilotAuthPlugin may still run alongside this plugin. This results in duplicate loader calls but is harmless and idempotent.

## Publishing

Publishing is handled via GitHub Actions. You can manually trigger the workflow to release a new version (patch, minor, or major).

---

# @best-linux-code/opencode-copilot-device-auth (中文)

GitHub 仓库: https://github.com/best-linux-code/opencode-copilot-device-auth
npm 软件包: https://www.npmjs.com/package/@best-linux-code/opencode-copilot-device-auth

本插件是针对 GitHub Copilot 的增强版 OpenCode 身份验证提供程序。它基于官方的 opencode-copilot-auth 插件构建，在模型元数据处理、身份验证流程可靠性以及对 Claude 思考预算 (thinking budget) 和 Gemini 推理强度 (reasoning effort) 等高级功能的支持方面进行了重大改进。

## 功能特性

- API 驱动的模型元数据：直接从 Copilot API 获取实时的模型上下文限制。例如，它能正确识别 Claude Opus 4.6 的 200K 上下文限制，而不是回退到静态的 128K 限制。
- 动态 Claude 思考预算：根据 API 报告的模型能力，自动生成低、中、高三种思考预算 (thinking_budget) 变体。
- 动态 Gemini 推理强度：根据 API 报告的模型能力，自动生成低、中、高三种推理强度 (reasoning_effort) 变体。
- 统一请求头：在包括 Claude、Gemini、GPT 和 Grok 在内的所有模型系列中实现一致的 vscode-chat 请求头。
- 增强型令牌交换：具备两级回退机制（从 v2/token 回退到 copilot_internal/user），以确保身份验证的可靠性。
- 稳健的设备流：实现 OAuth 设备代码流，并能妥善处理 slow_down 响应。
- 自动清理：注销时自动从 opencode.json 中移除过时的提供程序配置。
- 调试日志：在 /tmp/copilot-device-auth.log 中提供详细的响应状态和错误主体日志。
- 零成本：免费访问所有可用的 Copilot 模型。
- 面向未来：如果 API 报告了如 claude-opus-4.6-1m 等新模型，插件将动态注册这些模型。

## 模型限制对比

本插件会根据 Copilot 的实时数据修补每个模型的限制，确保 OpenCode 使用准确的上下文窗口大小。

| 模型 | 本插件 (实时) | 静态 models.dev |
| --- | --- | --- |
| claude-opus-4.6 | 200,000 | 128,000 |
| claude-sonnet-4.6 | 200,000 | 128,000 |
| claude-haiku-4.5 | 144,000 | 128,000 |

## 安装

通过 npm 安装软件包：

```bash
npm install @best-linux-code/opencode-copilot-device-auth
```

将插件添加到您的 opencode.json 配置中：

```json
{
  "plugin": [
    "@best-linux-code/opencode-copilot-device-auth"
  ]
}
```

## 已知限制

- 输入令牌未定义：某些模型（例如 gpt-5、claude-opus-41）可能会显示 input=undefined，这是因为 Copilot API 目前未针对这些特定标识符返回 max_prompt_tokens。
- Grok 启动器错误：grok-code-fast-1 模型可能会偶尔返回 "invalid initiator" 错误。这是上游 Copilot API 的已知问题，并非本插件的错误。
- 重复加载调用：内置的 CopilotAuthPlugin 可能会与本插件同时运行。这会导致重复的加载调用，但由于操作是幂等的，因此并无大碍。

## 发布

发布工作由 GitHub Actions 处理。您可以手动触发工作流以发布新版本（修订号 patch、次版本号 minor 或主版本号 major）。

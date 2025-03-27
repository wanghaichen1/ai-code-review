# AI 代码审查

*这是一个由 AI 生成 90% 内容的 GitHub Action。

## 描述

使用 OpenAI、Anthropic、Google 或 Deepseek 等各种 AI 模型来分析和提供代码反馈。这个 GitHub Action 通过自动审查拉取请求来帮助提高代码质量，可以专注于指定的文件扩展名，并排除特定路径。

## 使用示例

在您的 GitHub 仓库中创建一个新的 `.github/workflows/ai-code-review.yml` 文件。以下是不同 AI 提供商的示例：

### OpenAI 示例

```yaml
name: 使用 OpenAI 进行 AI 代码审查

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI 代码审查
      uses: wanghaichen1/ai-code-review@v1.0.2
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'openai'
        openai_api_key: ${{ secrets.OPENAI_API_KEY }}
        openai_model: 'gpt-4o'
```

### Anthropic 示例

```yaml
name: 使用 Anthropic 进行 AI 代码审查

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI 代码审查
      uses: wanghaichen1/ai-code-review@v1.0.2
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'anthropic'
        anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
        anthropic_model: 'claude-3-7-sonnet-20250219'
```

### Google 示例

```yaml
name: 使用 Google 进行 AI 代码审查

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI 代码审查
      uses: wanghaichen1/ai-code-review@v1.0.2
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'google'
        google_api_key: ${{ secrets.GOOGLE_API_KEY }}
        google_model: 'gemini-2.0-flash'
```

### Deepseek 示例

```yaml
name: 使用 Deepseek 进行 AI 代码审查

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI 代码审查
      uses: wanghaichen1/ai-code-review@v1.0.2
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'deepseek'
        deepseek_api_key: ${{ secrets.DEEPSEEK_API_KEY }}
        deepseek_model: 'deepseek-chat'
```

### 高级配置示例

```yaml
name: 使用高级设置的 AI 代码审查

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI 代码审查
      uses: wanghaichen1/ai-code-review@v1.0.2
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}

        ai_provider: 'openai'
        openai_api_key: ${{ secrets.OPENAI_API_KEY }}
        
        include_extensions: '.py,.js,.tsx'
        exclude_extensions: '.test.js'
        include_paths: 'src/,app/'
        exclude_paths: 'test/,docs/'
        fail_action_if_review_failed: 'true'
```

## 输入参数

***token*** - 必需。用于认证和访问 GitHub 仓库的 GitHub token。

***owner*** - 必需。仓库所有者的用户名。

***repo*** - 必需。仓库名称。

***pr_number*** - 必需。需要审查的拉取请求编号。

***ai_provider*** - 必需。使用的 AI 提供商 { openai, anthropic, google, deepseek}。默认为 'openai'。

***openai_api_key*** - 使用 OpenAI 提供商时必需。用于访问 OpenAI API 的密钥。

***openai_model*** - 可选。OpenAI 模型名称（例如：gpt-4o）。默认为 'gpt-4o'。

***anthropic_api_key*** - 使用 Anthropic 提供商时必需。用于访问 Anthropic API 的密钥。

***anthropic_model*** - 可选。Anthropic 模型名称（例如：claude-3-7-sonnet-20250219）。默认为 'claude-3-7-sonnet-latest'。

***google_api_key*** - 使用 Google 提供商时必需。用于访问 Google API 的密钥。

***google_model*** - 可选。Google 模型名称（例如：gemini-2.0-flash）。默认为 'gemini-2.0-flash'。

***deepseek_api_key*** - 使用 Deepseek 提供商时必需。用于访问 Deepseek API 的密钥。

***deepseek_model*** - 可选。Deepseek 模型名称（例如：deepseek-chat）。默认为 'deepseek-chat'。

***include_extensions*** - 可选。要包含在审查中的文件扩展名列表（例如：".py,.js,.html"）。如果未指定，将考虑所有文件类型。

***exclude_extensions*** - 可选。要从审查中排除的文件扩展名列表。

***include_paths*** - 可选。要包含在审查中的目录路径列表。

***exclude_paths*** - 可选。要从审查中排除的目录路径列表（例如："test/,docs/"）。如果未指定，将考虑所有路径。

***fail_action_if_review_failed*** - 可选。如果设置为 true，当审查过程失败时，action 将失败。默认为 'false'。

## 故障排除

### 常见问题

#### API 密钥问题
- **问题**：关于无效 API 密钥的错误消息
- **解决方案**：确保您的 API 密钥已正确设置为 GitHub secrets 并正确传递给工作流。

#### Action 超时失败
- **问题**：action 因超时错误而失败
- **解决方案**：
  1. 尝试使用更简单或更快的模型
  2. 将大型 PR 拆分为较小的 PR
  3. 使用 include/exclude 路径来限制审查范围

#### 错误："超出此模型的最大上下文长度"
- **问题**：由于令牌限制，AI 模型无法处理所有提供的代码
- **解决方案**：
  1. 使用 exclude_paths 跳过大文件
  2. 使用 include_extensions 仅关注关键文件类型
  3. 创建更小的 PR，减少更改的文件数量

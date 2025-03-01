# AI Code Review
*is a GitHub Action that is 90% generated by AIs.

## Description

Perform code review using various AI models from OpenAI, Anthropic, Google, Deepseek(soon) to analyze and provide feedback on your code. This GitHub Action helps improve the code quality by automatically reviewing pull requests, focusing on specified file extensions, and excluding specific paths.

## Inputs

***token*** - Required. This GitHub token is used for authentication and to access your GitHub repository.

***owner*** - Required. The username of the repository owner.

***repo*** - Required. The name of the repository.

***pr_number*** - Required. The number of the pull request that needs to be reviewed.

***ai_provider*** - Required. The AI provider to use { openai, anthropic, google, deepseek(soon)}. Default is 'openai'.


***openai_api_key*** - Required if using OpenAI provider. This key is necessary to access OpenAI's API for code review purposes.

***openai_model*** - Optional. The OpenAI model name (e.g., gpt-4o). Default is 'gpt-4o'.


***anthropic_api_key*** - Required if using Anthropic provider. This key is necessary to access Anthropic's API for code review purposes.

***anthropic_model*** - Optional. The Anthropic model name (e.g., claude-3-7-sonnet-20250219). Default is 'claude-3-7-sonnet-latest'.


***google_api_key*** - Required if using Google provider. This key is necessary to access Google's API for code review purposes.

***google_model*** - Optional. The Google model name (e.g., gemini-2.0-flash). Default is 'gemini-2.0-flash'.


***deepseek_api_key*** - Required if using Deepseek provider. This key is necessary to access Deepseek's API for code review purposes.

***deepseek_model*** - Optional. The Deepseek model name (e.g., deepseek-reasoner). Default is 'deepseek-reasoner'.


***include_extensions*** - Optional. A comma-separated list of file extensions to include in the review (e.g., ".py,.js,.html"). If not specified, the action will consider all file types.

***exclude_extensions*** - Optional. A comma-separated list of file extensions to exclude from the review.

***include_paths*** - Optional. A comma-separated list of directory paths to include in the review.

***exclude_paths*** - Optional. A comma-separated list of directory paths to exclude from the review (e.g., "test/,docs/"). If not specified, the action will consider all paths.

***fail_action_if_review_failed*** - Optional. If set to true, the action fails when the review process fails. Default is 'false'.

## Usage Examples

Create a new `.github/workflows/ai-code-review.yml` file in your GitHub repository. Below are examples for different AI providers:

### OpenAI Example

```yaml
name: AI Code Review with OpenAI

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI Code Review
      uses: AleksandrFurmenkovOfficial/ai-code-review@v0.7
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'openai'
        openai_api_key: ${{ secrets.OPENAI_API_KEY }}
        openai_model: 'gpt-4o'
```

### Anthropic Example

```yaml
name: AI Code Review with Anthropic

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI Code Review
      uses: AleksandrFurmenkovOfficial/ai-code-review@v0.7
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'anthropic'
        anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
        anthropic_model: 'claude-3-7-sonnet-20250219'
```

### Advanced Configuration Example

```yaml
name: AI Code Review with Advanced Settings

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI Code Review
      uses: AleksandrFurmenkovOfficial/ai-code-review@v0.7
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

### Google Example

```yaml
name: AI Code Review with Google

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI Code Review
      uses: AleksandrFurmenkovOfficial/ai-code-review@v0.7
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'google'
        google_api_key: ${{ secrets.GOOGLE_API_KEY }}
        google_model: 'gemini-2.0-flash'
```

### Deepseek Example (soon or suggest your PR to include)

```yaml
name: AI Code Review with Deepseek

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  ai_code_review:
    runs-on: ubuntu-latest
    steps:
    - name: AI Code Review
      uses: AleksandrFurmenkovOfficial/ai-code-review@main
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: ${{ github.repository_owner }}
        repo: ${{ github.event.repository.name }}
        pr_number: ${{ github.event.number }}
        
        ai_provider: 'deepseek'
        deepseek_api_key: ${{ secrets.DEEPSEEK_API_KEY }}
        deepseek_model: 'deepseek-reasoner'
```

## Troubleshooting

### Common Issues

#### API Key Issues
- **Problem**: Error message about invalid API keys
- **Solution**: Ensure your API keys are correctly set as GitHub secrets and properly passed to the workflow.

#### Action Failing with Timeout
- **Problem**: The action fails with a timeout error
- **Solution**: 
  1. Try using a simpler or faster model
  2. Split large PRs into smaller ones
  3. Use include/exclude paths to limit the scope of the review

#### Error: "This model's maximum context length is exceeded"
- **Problem**: The AI model can't process all the provided code due to token limitations
- **Solution**: 
  1. Use exclude_paths to skip large files
  2. Use include_extensions to focus only on critical file types
  3. Make smaller PRs with fewer changed files

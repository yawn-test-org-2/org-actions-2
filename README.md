# org-actions

GitHub Organizationで共有するための再利用可能なGitHub Actionsワークフローを提供するリポジトリです。

## 利用可能なワークフロー

### Reusable Test Workflow

「Hello, Reuseable Actions!」というメッセージをログに表示する簡単な再利用可能なワークフロー。

#### 使用方法

他のワークフローから以下のように呼び出すことができます:

```yaml
jobs:
  call-reusable-workflow:
    uses: yawn-test-org/org-actions/.github/workflows/reusable-test.yml@main
```

適切な組織名とブランチ名（例: `main`）を指定してください。

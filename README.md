# sample-gha-injection-attack
前提: https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions#using-starter-workflows-for-code-scanning

たとえ環境変数に入れても、 `${{ env.PR_TITLE }}` のように `env.`でアクセスすると攻撃が成り立ってしまう

- https://github.com/tomoya-namekawa/sample-gha-injection-attack/actions/workflows/check_pr_title_via_env.yml
  - <img width="931" alt="image" src="https://github.com/user-attachments/assets/0d426e81-cd8b-4ebb-a8e7-867f8b801f23" />


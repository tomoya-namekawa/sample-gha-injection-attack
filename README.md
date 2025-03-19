# sample-gha-injection-attack
- 前提: GitHub Actionsでのrunで `${{ github.event.pull_request.title }}` などを直接使うとインジェクション攻撃が可能なので環境変数を使うべき
  - https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions#using-starter-workflows-for-code-scanning

- しかし、たとえ環境変数に入れても、 `${{ env.PR_TITLE }}` のように `env.`でアクセスすると攻撃が成り立ってしまう

- https://github.com/tomoya-namekawa/sample-gha-injection-attack/actions/workflows/check_pr_title_via_env.yml
  - <img width="931" alt="image" src="https://github.com/user-attachments/assets/0d426e81-cd8b-4ebb-a8e7-867f8b801f23" />

  - workflow code: https://github.com/tomoya-namekawa/sample-gha-injection-attack/blob/main/.github/workflows/check_pr_title_via_env.yml
    ```yml
    
    name: Check PR title via env.PR_TITLE
    on:
      pull_request:
    env:
      PR_TITLE: ${{ github.event.pull_request.title }}
    
    jobs:
      check-pr-title:
        name: Check PR title
        runs-on: ubuntu-latest
        steps:
          - run: |
              title="${{ env.PR_TITLE }}"
              if [[ $title =~ ^octocat ]]; then
              echo "PR title starts with 'octocat'"
              exit 0
              else
              echo "PR title did not start with 'octocat'"
              exit 1
              fi
    ```

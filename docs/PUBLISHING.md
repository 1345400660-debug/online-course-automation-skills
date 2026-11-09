# 发布与更新方式（PUBLISHING）

本仓库发布到 GitHub 账号 `1345400660-debug`，仓库名 `online-course-automation-skills`（public）。

## 一、仓库信息

| 项 | 值 |
| --- | --- |
| GitHub 账号 | `1345400660-debug` |
| 仓库名 | `online-course-automation-skills` |
| 可见性 | public |
| 默认分支 | `main` |

## 二、发布方式（本机 git + Git Credential Manager）

本机已安装 Git 与 Git Credential Manager（GCM，provider=github），未安装 `gh` CLI。发布通过
`git` + 缓存凭据完成，无需手动输入令牌：

1. 初始化仓库并写入内容：

   ```bash
   git init -b main online-course-automation-skills
   cd online-course-automation-skills
   git add .
   git commit -m "feat: 智慧树答题与慕课答题两个技能"
   ```

2. 设置仓库本地身份（避免依赖全局配置）：

   ```bash
   git config user.name "1345400660-debug"
   git config user.email "237941139+1345400660-debug@users.noreply.github.com"
   ```

3. 通过 GitHub API 创建空仓库（凭据来自 GCM 缓存的 token）：

   ```bash
   TOKEN=$(printf 'protocol=https\nhost=github.com\n\n' | git credential fill | sed -n 's/^password=//p')
   curl -s -X POST -H "Authorization: token $TOKEN" \
     -H "Accept: application/vnd.github+json" \
     https://api.github.com/user/repos \
     -d '{"name":"online-course-automation-skills","description":"在线课程作业自动化技能集：智慧树答题 + 中国大学 MOOC 单元测验","public":true}'
   ```

4. 推送：

   ```bash
   git remote add origin https://github.com/1345400660-debug/online-course-automation-skills.git
   git push -u origin main
   ```

   GCM 会自动提供 HTTPS 凭据，无需在 URL 中写明文 token。

## 三、更新方式（后续迭代）

- 本地改完 `git add -A && git commit -m "..." && git push` 即可。
- 若令牌失效，用 GCM 重新登录：`git credential-manager github login`，或首次 push 时按弹出窗口授权。

## 四、技能打包（可选）

每个技能可用 WorkBuddy 内置的 `skill-creator` 打包成 zip 分发：

```bash
# 在 skill-creator 技能目录内
python scripts/package_skill.py skills/zhihuishu-quiz   ./dist
python scripts/package_skill.py skills/mooc-quiz        ./dist
```

打包前会自动校验 SKILL.md 的 YAML frontmatter 与目录结构。

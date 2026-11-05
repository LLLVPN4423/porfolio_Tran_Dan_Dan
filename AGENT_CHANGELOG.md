# Agent changelog

Mỗi agent **append** một block mới lên **đầu file** (dưới phần hướng dẫn này).

```markdown
## YYYY-MM-DD — [tóm tắt ngắn]
- **Yêu cầu:** ...
- **Thay đổi:** ...
- **File:** `path1`, `path2`
- **Deploy:** commit `hash` / chưa push / n/a
```

---

## 2026-11-05 — Thêm context cho agent

- **Yêu cầu:** Tạo file context + quy trình ghi chú thay đổi để agent không phải đọc cả repo; push lên git.
- **Thay đổi:** Thêm `AGENTS.md`, `PROJECT_CONTEXT.md`, `AGENT_CHANGELOG.md`, rule Cursor `.cursor/rules/portfolio-agent-workflow.mdc`.
- **File:** `AGENTS.md`, `PROJECT_CONTEXT.md`, `AGENT_CHANGELOG.md`, `.cursor/rules/portfolio-agent-workflow.mdc`
- **Deploy:** commit `6e81f8a`, đã push `main`

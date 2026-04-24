# Project: [PROJECT_NAME]

> 🔑 File này là source of truth. Codex đọc file này đầu tiên mỗi session.
> 📊 Xem `graphify-out/graph.json` để hiểu structure + dependencies (auto-generated).

---

## 🚀 FIRST TIME SETUP — ĐỌC CÁI NÀY TRƯỚC

> Nếu `docs/specs/` chưa có design doc nào → project chưa được plan.
> **Chạy Phase 0: Brainstorming trước khi làm bất cứ thứ gì.**

### ▶ Phase 0: Brainstorming (bắt buộc trước khi code)

<HARD-GATE>
KHÔNG viết code, KHÔNG scaffold project, KHÔNG implement bất cứ thứ gì cho đến khi design được user approve và có file spec trong docs/specs/.
</HARD-GATE>

Làm theo thứ tự, từng bước xong confirm user trước khi tiếp:

**Bước 1 — Đọc Brief**
Đọc `docs/BRIEF.md` để nắm ý tưởng ban đầu.
Chỉ hỏi những gì còn thiếu hoặc mơ hồ, không hỏi lại những gì đã rõ.

**Bước 2 — Clarify Requirements**
Hỏi từng câu một để làm rõ những gì còn mơ hồ.
Ưu tiên multiple choice khi có thể.

**Bước 3 — Propose Approaches**
Đề xuất 2-3 approaches + trade-offs.
Giải thích ưu/nhược của từng cách.

**Bước 4 — Present Design**
Trình bày design từng section.
Confirm user sau mỗi section trước khi tiếp.

**Bước 5 — Write Spec**
Viết design doc vào `docs/specs/YYYY-MM-DD-design.md`.
Commit ngay.

**Bước 6 — Self Review**
Tự review spec:
- Có placeholder text không?
- Có contradiction không?
- Scope rõ ràng không?
- Ambiguity nào không?

**Bước 7 — User Review**
Hỏi user review file spec trước khi tiếp tục.
Chờ approve, nếu có changes thì update + re-review.

**Bước 8 — Lên Phases + Tasks**
Sau khi spec approved:
- Chia thành 4 phases, viết vào `docs/phases/`
- Update `CODEX.md` phần Stack, Folder Structure bên dưới
- Tạo `tasks/todo.md` cho Phase 1
- Xóa block "FIRST TIME SETUP" này

⚠️ KHÔNG code gì trong Phase 0. KHÔNG skip bước nào.

---

## Stack
[Điền sau Phase 0]

## Folder Structure
[Điền sau Phase 0]

## Coding Rules
- **TypeScript strict** — không dùng `any`
- **Test ngay** — mỗi task phải có unit test trước khi sang task mới
- **1 commit = 1 task** — commit message: `feat/fix/test/chore: [mô tả ngắn]`
- **Scope control** — không sửa file ngoài danh sách cho phép trong task
- **Error handling** — mọi async function phải handle error
- **Brainstorm trước khi thêm feature** — đọc `skills/brainstorming/SKILL.md`
- **Memory hooks** — auto-save/load context, xem `docs/MEMORY_HOOKS.md`
- **Continuous learning** — extract patterns, xem `docs/CONTINUOUS_LEARNING.md`

## Model Strategy

**Default Model:** GPT-5.5 (mọi task)  
**Complex Tasks:** Opus 4-6 (refactor, architecture)  
**Fallback:** Sonnet 4-6 (nếu GPT fail)

### Khi Nào Dùng Từng Model?

**GPT-5.5** (default)
- Feature implementation
- Bug fix
- Test writing
- Documentation
- Regular development
- Brainstorming + planning

**Opus 4-6** (complex tasks)
- Refactor lớn (> 5 files)
- Architecture changes
- Complex algorithm
- Performance optimization
- Deep reasoning needed

**Sonnet 4-6** (fallback)
- Fallback nếu GPT fail
- Backup model

### Cách Chuyển Model

```bash
# Check model hiện tại
/status

# Chuyển sang Opus (complex)
/model aihub-claude/claude-opus-4-6

# Quay lại GPT (default)
/model openai-codex/gpt-5.5
```

### Tips
- Luôn check `/status` trước task
- Dùng GPT mặc định (mọi task)
- Chuyển Opus khi cần reasoning sâu
- Quay lại GPT sau khi xong

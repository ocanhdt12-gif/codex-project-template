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


### 🆕 Handling Emerging Tasks

Khi task phát sinh trong quá trình làm:

**Step 1: Add Task**
```bash
npm run add-task
```
Script sẽ:
1. Detect layer hiện tại
2. Hỏi task title + description
3. Add vào tasks/layer-X-todo.md
4. Commit tự động

**Step 2: Brainstorm & Design**
- Clarify từng câu một
- Propose 2-3 approaches
- Present design từng section
- Tự review spec

**Step 3: Update Context**
1. Update `docs/SCOPE_BREAKDOWN.md` nếu dependency thay đổi
2. Chạy `graphify ./src` để update graph
3. Update `CLAUDE.md`/`CODEX.md` context nếu cần

**Step 4: Pick & Implement**
```bash
npm run pick-task
# → Pick task vừa thêm
# → Implement như bình thường
```

**Quy tắc:**
- ✅ Brainstorm trước khi code
- ✅ Add vào layer hiện tại (không tạo layer mới)
- ✅ Update graph + context sau brainstorm
- ✅ Commit sau mỗi bước

## Coding Rules
- **TypeScript strict** — không dùng `any`
- **Test ngay** — mỗi task phải có unit test trước khi sang task mới
- **1 commit = 1 task** — commit message: `feat/fix/test/chore: [mô tả ngắn]`
- **Scope control** — không sửa file ngoài danh sách cho phép trong task
- **Error handling** — mọi async function phải handle error
- **Brainstorm trước khi thêm feature** — đọc `skills/brainstorming/SKILL.md`
- **Memory hooks** — auto-save/load context, xem `docs/MEMORY_HOOKS.md`
- **Continuous learning** — extract patterns, xem `docs/CONTINUOUS_LEARNING.md`

## 🎯 Team Workflow — Pick Task CLI

**Tự động pick task + update trạng thái:**
```bash
npm run pick-task
```

**Script sẽ:**
1. Detect layer hiện tại (layer-0, layer-1, ...)
2. Hiển thị danh sách todo tasks
3. Hỏi bạn pick task nào
4. Hỏi tên người pick
5. Update task file (status = in-progress, assigned = tên)
6. **Commit + push tự động** lên main
7. Tạo feature branch sẵn

**Workflow cụ thể:**
```bash
# 1. Pull latest
git pull origin main

# 2. Pick task (tự động update + push)
npm run pick-task
# → Chọn task → Nhập tên → Xong!

# 3. Làm việc trong feature branch
# (branch đã được tạo sẵn)
git status  # Xem branch hiện tại

# 4. Commit + push khi xong
git add .
git commit -m "feat: Task description"
git push origin feature/task-X-...

# 5. Merge vào main (hoặc tạo PR)
```

**Lợi ích:**
- ✅ Mọi người pull về sẽ thấy task đã assign → không ai pick lại
- ✅ Task file luôn up-to-date trên main
- ✅ Tránh conflict khi 2 người cùng pick task
- ✅ Mỗi task = 1 branch riêng → dễ review + rollback

## Model Strategy

**Tất cả tasks:** GPT-5.5 (brainstorming + code + mọi thứ)

### Model Duy Nhất: GPT-5.5

Dùng `openai-codex/gpt-5.5` cho **tất cả** tasks:
- Phase 0: Brainstorming + planning
- Feature implementation
- Bug fix
- Test writing
- Documentation
- Code review
- Mọi task khác

### Cách Check Model

```bash
# Check model hiện tại
/status

# Set model nếu chưa đúng
/model openai-codex/gpt-5.5
```

## Skills Available

> **Scope rules để tránh conflict:**
> - `error-handling` → dùng cho **frontend** (React Error Boundaries, user-facing messages)
> - `nodejs-express-patterns` → có error handling riêng cho **backend** (Express middleware)
> - `security-best-practices` → deep dive auth/CORS/XSS; `api-design` chỉ mention auth ở mức HTTP status codes
> - `testing-vitest-jest` → **frontend** (Vitest + React Testing Library)
> - `testing-backend-jest` → **backend** (Jest + Supertest)
> - `frontend-agent` → overview/agent; các skill chuyên sâu (state, perf, a11y) là chi tiết hơn

### Phase 0 — Planning
- `skills/brainstorming/SKILL.md` — **Bắt buộc** trước mọi feature mới hoặc thay đổi lớn

### Frontend
- `skills/frontend-agent/SKILL.md` — Senior Frontend Developer agent, UI patterns, architecture
- `skills/typescript/SKILL.md` — TypeScript strict mode, type narrowing, inference
- `skills/tailwind-v4-shadcn/SKILL.md` — Tailwind CSS v4 + shadcn/ui, 8 common errors
- `skills/state-management-data-fetching/SKILL.md` — Zustand + TanStack Query, integration patterns
- `skills/testing-vitest-jest/SKILL.md` — Unit/component tests (Vitest + React Testing Library)
- `skills/performance-optimization/SKILL.md` — Core Web Vitals, code splitting, bundle analysis
- `skills/accessibility-a11y/SKILL.md` — WCAG 2.1, ARIA, keyboard navigation
- `skills/error-handling/SKILL.md` — React Error Boundaries, try/catch, user-facing messages
- `skills/git-workflow/SKILL.md` — Conventional commits, branch naming, PR process

### API & Integration
- `skills/api-design/SKILL.md` — REST principles, request/response format, versioning, pagination
- `skills/security-best-practices/SKILL.md` — OWASP Top 10, auth, CORS/CSRF, XSS prevention

### Backend (Node.js)
- `skills/nodejs-express-patterns/SKILL.md` — Express routing, middleware, controllers, services
- `skills/database-orm-patterns/SKILL.md` — Prisma/TypeORM, schema design, migrations, transactions
- `skills/testing-backend-jest/SKILL.md` — Unit/API tests (Jest + Supertest), mocking, fixtures

## Boilerplate (Stack-Conditional)

> Chỉ dùng khi stack là **React hoặc Next.js**. Bỏ qua nếu project là Node.js API thuần, Python, CLI, v.v.

Nếu Phase 0 xác định stack là React/Next.js:
1. Đọc `skills/boilerplate/react-nextjs/BOILERPLATE.md`
2. Follow setup commands và config files trong đó
3. Các skill `frontend-agent`, `typescript`, `tailwind-v4-shadcn` sẽ tự động áp dụng

Nếu stack khác → bỏ qua folder `skills/boilerplate/` hoàn toàn.

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

**Bước 0 — Generate Knowledge Graph**
- Chạy: `graphify ./src`
- Output: `graphify-out/graph.json` (auto-generated)
- Dùng để: Opencode hiểu structure + dependencies của project
- Commit: Thêm `graphify-out/` vào `.gitignore` (không commit generated files)

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

**Bước 8 — Lên Layers + Tasks**
Sau khi spec approved:
- Phân tích dependency → chia thành layers (Layer 0, 1, 2, ...)
- Layer 0 (Foundation): không phụ thuộc vào layer khác
- Layer N: phụ thuộc vào Layer 0 → N-1
- Tạo `tasks/layer-0-todo.md` (Foundation tasks)
- Tạo `tasks/layer-1-todo.md`, `layer-2-todo.md`, ... khi cần
- Update `CODEX.md` phần Stack, Folder Structure bên dưới
- Xóa block "FIRST TIME SETUP" này

⚠️ KHÔNG code gì trong Phase 0. KHÔNG skip bước nào.

---

## Stack
[Điền sau Phase 0]

## 🎨 Design System

**Template:** Claude Design (Anthropic)  
**Source:** `docs/DESIGN.md`

### CSS Variables
- **Colors:** `--color-primary`, `--color-text`, `--color-surface`, etc.
- **Spacing:** `--spacing-xs` (4px) → `--spacing-3xl` (64px)
- **Typography:** `--type-scale-xs` (12px) → `--type-scale-4xl` (36px)
- **Shadows:** `--shadow-sm`, `--shadow-md`, `--shadow-lg`, `--shadow-xl`

### Components
- **Button** (`src/components/Button.tsx`) - primary, secondary, outline, ghost
- **Card** (`src/components/Card.tsx`) - default, elevated, outlined
- More components coming...

### When Coding
1. Import CSS variables từ `src/styles/design-tokens.css`
2. Use components từ `src/components/`
3. Follow spacing scale (--spacing-*)
4. Follow color palette (--color-*)
5. Follow typography scale (--type-scale-*)
6. Maintain accessibility (WCAG AA)
7. Test responsive design (mobile, tablet, desktop)

## Folder Structure
[Điền sau Phase 0]

### 📋 Specifications
Xem `docs/SPECIFICATIONS.md` để chi tiết đầy đủ về chức năng, requirements, và design.

### 📋 Task Structure — Dependency-Driven
Dùng **Dependency-Driven approach**:
- `tasks/layer-0-todo.md` — Foundation (no dependency)
- `tasks/layer-1-todo.md` — Depends on Layer 0 (tạo khi cần)
- `tasks/layer-2-todo.md` — Depends on Layer 1 (tạo khi cần)
- ... (thêm layer tùy scope)
- `tasks/done.md` — Completed tasks

**Quy tắc:**
- Số layer phụ thuộc vào scope breakdown + dependency analysis
- Các task trong cùng layer có thể làm song parallel
- Chỉ khi layer N hoàn toàn xong → mới bắt đầu layer N+1
- Xem `docs/SCOPE_BREAKDOWN.md` để chi tiết

## 🔄 After Completion — Layer Refinement

Sau khi hoàn thành tất cả layer (Layer 0 → N), user sẽ check lại luồng/giao diện và báo bug hoặc feature mới.

### Workflow

1. **User báo** → Bug hoặc feature mới
2. **Em brainstorm** → Clarify + propose 2-3 approaches
3. **User approve** → Confirm phương án
4. **Tạo todo** → Add vào `tasks/layer-refinement-todo.md`
5. **Pick + implement** → Như layer khác

### Layer Refinement

- **File:** `tasks/layer-refinement-todo.md`
- **Mục đích:** Track bug fixes + feature requests sau khi hoàn thành
- **Workflow:** Brainstorm → Design → Implement (giống layer khác)

### Cách Thêm Task

Khi user báo bug/feature:

1. **Brainstorm** (Phase 0 style)
   - Clarify từng câu một
   - Propose 2-3 approaches
   - Present design từng section

2. **Tạo todo** vào `tasks/layer-refinement-todo.md`
   ```markdown
   ### [Task Number] — [Title]
   
   **Type:** Bug / Feature
   **Description:** ...
   **Acceptance Criteria:** ...
   **Status:** todo
   ```

3. **Pick + implement** như bình thường

---

## Coding Rules
- **TypeScript strict** — không dùng `any`
- **Test ngay** — mỗi task phải có unit test trước khi sang task mới
- **1 commit = 1 task** — commit message: `feat/fix/test/chore: [mô tả ngắn]`
- **Scope control** — không sửa file ngoài danh sách cho phép trong task
- **Error handling** — mọi async function phải handle error
- **Brainstorm trước khi thêm feature** — đọc `skills/brainstorming/SKILL.md`

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

### Browser & Testing Tools
- `docs/CHROME_DEVTOOLS_MCP.md` — Chrome DevTools MCP for browser automation, debugging, performance analysis, E2E testing

## Boilerplate (Stack-Conditional)

> Chỉ dùng khi stack là **React hoặc Next.js**. Bỏ qua nếu project là Node.js API thuần, Python, CLI, v.v.

Nếu Phase 0 xác định stack là React/Next.js:
1. Đọc `skills/boilerplate/react-nextjs/BOILERPLATE.md`
2. Follow setup commands và config files trong đó
3. Các skill `frontend-agent`, `typescript`, `tailwind-v4-shadcn` sẽ tự động áp dụng

Nếu stack khác → bỏ qua folder `skills/boilerplate/` hoàn toàn.

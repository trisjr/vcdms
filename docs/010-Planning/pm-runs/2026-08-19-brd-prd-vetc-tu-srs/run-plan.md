# Run Plan: 2026-08-19-brd-prd-vetc-tu-srs

**Lane**: doc · **Shape**: A (Authoring) · **Tier**: T2 (điểm 2/4)

## Phases

| # | Phase | Agent | Song song? | Input | Output |
|---|-------|-------|-----------|-------|--------|
| 1 | Intake & Triage | PM | — | Yêu cầu gốc của anh | `brief.md` |
| 2 | Analysis (1 lens) | `business-analyst` (read-only) | Không | `SRS-VETC.md` | `findings/business-analyst.md` + `findings/business-analyst-gaps.md` ✅ **XONG** |
| 3 | GATE | PM + anh | — | Findings + run-plan + outline | Phê duyệt |
| 4 | Doc plan | PM | — | Findings | `outline.md` |
| 5 | Soạn thảo | `business-analyst` (1 writer) | Không | Outline toàn văn + findings | BRD, PRD, Open-Questions |
| 6a | Verify | `context-auditor` | Không | 3 tài liệu vừa viết | `verdict.md` |
| 6b | Close-step | PM | — | Verdict | MOC + `000-Index.md` + Glossary |

> **Vì sao một writer, không fan-out**: ba tài liệu dùng **chung một nguồn sự thật** (`SRS-VETC.md` + findings) và **cross-link lẫn nhau** (PRD trỏ BRD, cả hai trỏ Open-Questions theo mã `Q-NN`). Cắt cho nhiều writer chỉ đổi lấy rủi ro mã `Q-NN` lệch nhau giữa ba file, không rút ngắn được gì thực chất.

## File ownership map

| Agent | Sở hữu (được ghi) | Cấm chạm |
|-------|-------------------|----------|
| `business-analyst` (writer, phase 5) | `docs/020-Requirements/PRD-VETC.md`<br>`docs/020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md`<br>`docs/050-Research/Analysis-Open-Questions-VETC.md` | Mọi MOC · `docs/000-Index.md` · `SRS-VETC.md` · `Glossary.md` · toàn bộ `pm-runs/` |
| `context-auditor` (verifier, phase 6a) | **Không ghi gì** (read-only, báo cáo qua final message) | Tất cả |
| **PM (em)** | `docs/020-Requirements/Requirements-MOC.md`<br>`docs/050-Research/Research-MOC.md`<br>`docs/000-Index.md`<br>`docs/999-Resources/Glossary.md`<br>toàn bộ `docs/010-Planning/pm-runs/2026-08-19-brd-prd-vetc-tu-srs/` | — |

> Ownership của writer và PM **rời nhau tuyệt đối**. Mọi MOC và `000-Index.md` là điểm hội tụ của writer → PM giữ độc quyền theo guardrail lane doc.
> `SRS-VETC.md` là **nguồn đọc, không phải đích ghi** — run này không sửa SRS.

## Bảng đích tài liệu (tra từ Document Type Mapping — RULE-001)

| # | Tài liệu | Loại (RULE-001) | Thư mục đích | Tên file | Naming convention áp dụng |
|---|----------|-----------------|--------------|----------|---------------------------|
| 1 | BRD | `BRD` | `docs/020-Requirements/BRD/` | `BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md` | `BRD-{NNN}-{Title}.md` ✅ |
| 2 | PRD | `PRD` | `docs/020-Requirements/` | `PRD-VETC.md` | `PRD-{ProjectName}.md` ✅ |
| 3 | Danh sách câu hỏi làm rõ | `Research / Analysis` | `docs/050-Research/` | `Analysis-Open-Questions-VETC.md` | `Analysis-{Topic}.md` ✅ |

> **Ghi chú về hạng mục 3**: Document Type Mapping **không có** loại "Clarification / Open Questions". Guardrail lane doc cấm tự chế thư mục top-level mới. Loại gần nhất trong bảng là **Research / Analysis** → `docs/050-Research/Analysis-{Topic}.md`. Đây là mục cần anh chốt tại gate.

## Artifact sẽ tạo/sửa ngoài run-state

**Tạo mới (writer):**
- `docs/020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md` — tài liệu nghiệp vụ cấp cao
- `docs/020-Requirements/PRD-VETC.md` — yêu cầu sản phẩm chi tiết (25 FR + 7 NFR + state machine + 31 giả định)
- `docs/050-Research/Analysis-Open-Questions-VETC.md` — 31 câu hỏi gửi khách hàng, chia 3 mức ưu tiên

**Sửa (PM, close-step):**
- `docs/020-Requirements/Requirements-MOC.md` — đăng ký BRD + PRD
- `docs/050-Research/Research-MOC.md` — đăng ký file câu hỏi
- `docs/999-Resources/Glossary.md` — bổ sung ~35 thuật ngữ domain VETC

**Tạo mới (PM, close-step):**
- `docs/000-Index.md` — **hiện chưa tồn tại** dù RULE-001 quy định BẮT BUỘC. Close-step yêu cầu đăng ký PRD vào đây.

**Đưa vào version control (hệ quả kỹ thuật, không phải deliverable của run):**
- `docs/020-Requirements/SRS-VETC.md` — đang **untracked** ở checkout chính; đã copy vào worktree để writer đọc được. Commit của run sẽ bao gồm file này.
- Bản `Requirements-MOC.md` cập nhật (thêm link SRS) của anh — cũng đang uncommitted.

## Assumptions

- **A1**: `SRS-VETC.md` là nguồn sự thật duy nhất; file `.docx` gốc không được parse → **sai thì hỏng ở đâu**: BRD/PRD thiếu theo nếu `.docx` có yêu cầu mà SRS bỏ sót. Giảm thiểu: mọi khoảng trống đều nằm trong file câu hỏi để khách hàng đối chiếu.
- **A2**: Quy ước `id` frontmatter theo pattern hiện hữu của repo (`SRS-VETC`), tức `{TYPE}-{ProjectName}` → `PRD-VETC`; **riêng BRD** dùng `BRD-001` vì naming convention bắt buộc `BRD-{NNN}-{Title}.md`; file câu hỏi dùng `ANALYSIS-OQ-VETC` → **sai thì hỏng ở đâu**: id không nhất quán, khó tra cứu chéo về sau.
- **A3**: Ba tài liệu tạo ra ở `status: draft`, **không** phải `approved` — vì 11 câu Blocker chưa có lời đáp từ khách hàng → **sai thì hỏng ở đâu**: nếu đặt `approved` sớm, đội dev sẽ coi các giả định tạm là quyết định đã chốt và build theo.
- **A4**: Dùng **standard markdown relative link**, **KHÔNG** wiki-link — theo RULE-001 mục "Quy tắc liên kết" (bản `updated: 2026-03-03`), dù câu chữ trong command `/pm-doc` nói ngược lại. RULE-001 là contract của lane → **sai thì hỏng ở đâu**: nếu chọn nhầm wiki-link, `context-auditor` ở Bước 6 sẽ báo CRITICAL vì vi phạm chuẩn repo.
- **A5**: Giữ **T2**, không escalate T3 dù Glossary cần thêm ~35 thuật ngữ. Lý do: đây là **khởi tạo từ một nguồn duy nhất**, không phải *chuẩn hóa diện rộng* (vốn hàm ý sửa nhiều tài liệu hiện hữu) → **sai thì hỏng ở đâu**: nếu thực tế phải rà chéo nhiều tài liệu, run sẽ thiếu bước inventory. Điều kiện escalate: nếu phát sinh nhu cầu sửa `SRS-VETC.md` hoặc sinh Epic/Story ở `022-User-Stories`.

## Gate

- **Trình ngày**: 2026-08-19
- **Kết quả**: **Duyệt** — anh chọn đúng cả 4 phương án PM đề xuất.
- **Bốn quyết định đã chốt tại gate**:
  1. **Vị trí file câu hỏi**: `docs/050-Research/Analysis-Open-Questions-VETC.md` (dùng loại `Research / Analysis` có sẵn trong Document Type Mapping, đúng naming `Analysis-{Topic}.md`). → Cập nhật `Research-MOC.md`.
  2. **Dead link `PRD-TNMCORE-OS.md`** trong `Requirements-MOC.md`: **xóa dòng**. Chi phí bằng không vì PM đang sửa đúng file đó ở close-step, và để lại thì `context-auditor` chắc chắn báo lỗi ở Bước 6.
  3. **Phạm vi close-step**: đủ cả ba — tạo `docs/000-Index.md`, bổ sung ~35 thuật ngữ vào `Glossary.md`, cập nhật `Requirements-MOC.md` + `Research-MOC.md`.
  4. **Phê duyệt**: chạy thẳng tới hết — dispatch writer → verify bằng `context-auditor` → close-step → commit + push branch.
- **Điều chỉnh của anh**: không có. Run plan giữ nguyên như trình.

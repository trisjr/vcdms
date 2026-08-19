# Doc Plan: 2026-08-19-brd-prd-vetc-tu-srs

> **File này do PM độc quyền chỉnh sửa.** Writer báo xong trong `SUMMARY` + `FILES_TOUCHED`, PM tick checkbox sau khi đối chiếu ownership.

## Hạng mục

| # | Tài liệu | Loại (RULE-001) | Đích | Template | Trạng thái đích | Writer | Xong |
|---|----------|-----------------|------|----------|-----------------|--------|------|
| 1 | BRD | `brd` | `docs/020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md` | tự cấu trúc (repo chưa có Template-BRD) | `draft` | business-analyst | [x] |
| 2 | PRD | `prd` | `docs/020-Requirements/PRD-VETC.md` | `docs/999-Resources/Templates/Template-PRD.md` + 2 mục bổ sung | `draft` | business-analyst | [x] |
| 3 | Danh sách câu hỏi làm rõ | `analysis` | `docs/050-Research/Analysis-Open-Questions-VETC.md` | `docs/999-Resources/Templates/Template-Analysis.md` (tham khảo) | `draft` | **PM** (xem E1) | [x] |

> **PM tick sau khi đối chiếu `FILES_TOUCHED` và đếm thực tế bằng Grep** (không tick thay worker):
> - BRD: BR-01…BR-10 = **10 dòng** ✅ · 11 mục ✅
> - PRD: FR-01…FR-25 = **25 mã duy nhất** ✅ · NFR-01…NFR-07 = **7 dòng** ✅ · nhánh T-a…T-h = **8 dòng** ✅ · bảng giả định = **31 dòng** ✅ · bảng mâu thuẫn C-01…C-18 = **18 dòng** ✅
> - Open-Questions: **31 câu / 31 ô trả lời / 31 dòng bảng tổng hợp** ✅ · 0 thuật ngữ trong danh sách cấm ✅
> - **Wiki-link trong cả 3 file: 0** ✅ (đúng RULE-001, ngược câu chữ command — xem `run-plan.md` mục A4)
> - Hạng mục 3 do PM ghi thay writer vì harness guard chặn writer — chi tiết tại [escalations.md](./escalations.md) mục E1.

---

## Outline từng tài liệu

### Tài liệu 1 — BRD-001 (Business Requirements Document)

- **Độc giả đích**: Stakeholder phía khách hàng và ban lãnh đạo — người quyết định **có làm dự án này không** và **đo thành công bằng gì**. KHÔNG phải đội dev.
- **Nguồn sự thật**:
  - `docs/020-Requirements/SRS-VETC.md` (nguồn gốc duy nhất)
  - `docs/010-Planning/pm-runs/2026-08-19-brd-prd-vetc-tu-srs/findings/business-analyst.md` **Phần 1** (business layer đã trích sẵn: context, 6 actor, process 5 bước, 10 business rule BR-01…BR-10, bảng objective)
  - `.../findings/business-analyst-gaps.md` **Phần 3** (để biết mục nào phải ghi `TBD`)
- **Cấu trúc (heading cấp 1–2)**:
  1. Tóm tắt điều hành (Executive Summary)
  2. Bối cảnh & Vấn đề nghiệp vụ — 4 vấn đề cốt lõi, ghi rõ nhãn [SRS]/[SUY LUẬN]; hiện trạng as-is = `TBD` (Q-30)
  3. Mục tiêu nghiệp vụ (Business Objectives) — 5 mục tiêu định tính; **KPI định lượng = `TBD` (Q-29)**
  4. Phạm vi (Scope) — 4.1 Trong phạm vi / 4.2 Ngoài phạm vi / **4.3 Phạm vi chưa xác định** (luồng Nhập kho — Q-01, mâu thuẫn C-01 + C-02)
  5. Các bên liên quan (Stakeholders) — bảng 4 actor có trong SRS + 2 actor thiếu (nhà cung cấp, kế toán) đánh dấu `TBD`
  6. Quy trình nghiệp vụ hiện tại & mong muốn — luồng 5 bước; nêu rõ **chỉ có happy path**
  7. Quy tắc nghiệp vụ (Business Rules) — bảng BR-01…BR-10 nguyên vẹn, có cột nguồn SRS
  8. Ràng buộc & Giả định — ngân sách/timeline/pháp lý = `TBD`
  9. Rủi ro nghiệp vụ — dẫn 11 câu Blocker
  10. Tiêu chí thành công — `TBD` + trỏ Q-29
  11. Tài liệu liên quan
- **Tiêu chí xong (đo được)**:
  - Đủ 11 mục trên, frontmatter có `id: BRD-001`, `type: brd`, `status: draft`, `created: 2026-08-19`
  - Bảng BR có đủ **10 dòng** BR-01…BR-10, mỗi dòng có cột nguồn SRS
  - Mọi ô không có căn cứ trong SRS đều ghi `TBD` **kèm mã Q-NN**, không có ô nào bịa số
  - Có link tới SRS, PRD và file câu hỏi bằng relative markdown link

### Tài liệu 2 — PRD-VETC (Product Requirements Document)

- **Độc giả đích**: Đội phát triển (Architect, Engineer, QA, Designer) — người **build** hệ thống. Cần đủ chi tiết để thiết kế DB và viết test case.
- **Nguồn sự thật**:
  - `docs/020-Requirements/SRS-VETC.md`
  - `.../findings/business-analyst.md` **Phần 2** (bảng 25 FR + 7 NFR có mã/nguồn/ưu tiên, state machine 5 trạng thái + 8 nhánh thiếu, 3 persona)
  - `.../findings/business-analyst-gaps.md` **Phần 3** (31 giả định tạm) + **Phần 4** (18 mâu thuẫn)
  - `docs/999-Resources/Templates/Template-PRD.md` (khung 7 mục)
- **Cấu trúc**: giữ 7 mục của Template-PRD, **bổ sung 3 mục** (bổ sung vào tài liệu, KHÔNG sửa file template dùng chung):
  1. Executive Summary
  2. Background & Objectives — Problem Statement / Goals / **Non-Goals** (luồng Nhập kho, tích hợp payment gateway, native app — đều theo giả định tạm)
  3. Target Audience — 3 persona P1/P2/P3
  4. Functional Requirements — **bảng FR-01…FR-25 đầy đủ**, cột: ID / Tính năng / Mô tả / Nguồn SRS / Ưu tiên P0-P1-P2
  5. Non-Functional Requirements — **bảng NFR-01…NFR-07**; kèm mục con "NFR chưa xác định" liệt kê 13 hạng mục SRS im lặng
  6. **[MỚI] State machine trạng thái đơn hàng** — 5 trạng thái + sơ đồ mermaid `stateDiagram-v2` + bảng 8 nhánh chưa định nghĩa T-a…T-h
  7. User Flows & UX Requirements — luồng 5 bước, ghi rõ Bước 5 diễn ra trên mobile (Q-23)
  8. Success Metrics — `TBD` + trỏ Q-29
  9. **[MỚI] Giả định thiết kế (Design Assumptions)** — bảng 31 dòng: mã Q-NN / giả định đang đi theo / mức độ / hệ quả nếu khách trả lời khác
  10. **[MỚI] Mâu thuẫn đã phát hiện trong SRS** — bảng C-01…C-18 có trích dòng
  11. Tài liệu liên quan
- **Tiêu chí xong (đo được)**:
  - Bảng FR đủ **25 dòng** FR-01…FR-25; bảng NFR đủ **7 dòng** NFR-01…NFR-07 — mỗi dòng có cột nguồn SRS
  - Bảng giả định đủ **31 dòng**, mỗi dòng có mã `Q-NN` khớp file câu hỏi
  - Bảng mâu thuẫn đủ **18 dòng** C-01…C-18
  - Số liệu NFR **giữ nguyên SRS** (≤ 2 giây, backup hàng ngày); mọi con số khác phải gắn nhãn "giả định thiết kế chờ xác nhận"
  - FR-24, FR-25 ghi rõ là `TBD` chi tiết + trỏ Q-28 — **không bịa nội dung báo cáo**

### Tài liệu 3 — Analysis-Open-Questions-VETC (file gửi khách hàng)

- **Độc giả đích**: **Khách hàng — người phi kỹ thuật.** Đây là file anh gửi đi, nên ngôn ngữ phải đọc-là-trả-lời-được, không dùng từ chuyên môn không giải thích.
- **Nguồn sự thật**: `.../findings/business-analyst-gaps.md` **Phần 3** (31 câu đã soạn sẵn cho người phi kỹ thuật)
- **Cấu trúc**:
  1. Lời mở đầu — giải thích ngắn: đây là các điểm cần làm rõ sau khi đọc tài liệu yêu cầu; trả lời được bao nhiêu thì làm rõ bấy nhiêu
  2. Hướng dẫn cách trả lời — mỗi câu có sẵn "phương án đang tạm dùng"; nếu đồng ý thì chỉ cần ghi "OK", nếu khác thì mô tả lại
  3. **Phần A — 11 câu CẦN GẤP (Blocker)**: Q-01, Q-02, Q-03, Q-04, Q-05, Q-06, Q-09, Q-10, Q-11, Q-12, Q-21
  4. **Phần B — 11 câu Quan trọng**: Q-07, Q-08, Q-13, Q-14, Q-15, Q-16, Q-17, Q-20, Q-23, Q-27, Q-28
  5. **Phần C — 9 câu Nên có**: Q-18, Q-19, Q-22, Q-24, Q-25, Q-26, Q-29, Q-30, Q-31
  6. Bảng tổng hợp để tick — mã / tóm tắt câu hỏi / mức độ / ô trống cho khách hàng điền
- **Định dạng mỗi câu** (bắt buộc thống nhất):
  - **Mã** + **tiêu đề ngắn dễ hiểu**
  - **Bối cảnh**: 1–2 câu, viết mềm — *"Tài liệu hiện có nói… nhưng chưa nói rõ…"*. **KHÔNG** copy nguyên cột "Vì sao rủi ro" (ngôn ngữ kỹ thuật); diễn đạt lại theo hệ quả nghiệp vụ mà khách hàng cảm nhận được.
  - **Câu hỏi**: nguyên văn phần "Câu hỏi gửi khách hàng" trong findings — **giữ nguyên, không rút gọn**
  - **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: nguyên văn phần "Giả định tạm"
  - **Ô trả lời**: `> **Trả lời của khách hàng:** ______`
- **Tiêu chí xong (đo được)**:
  - Đủ **31 câu**, đúng mã Q-NN, đúng phân bổ 11/11/9 theo 3 phần A/B/C
  - Mỗi câu có đủ **4 thành phần** + ô trả lời
  - Không còn từ chuyên môn chưa giải thích: `state machine`, `schema`, `migration`, `API adapter`, `RPO/RTO`, `object storage`, `data scope` — nếu buộc phải dùng thì mở ngoặc giải thích bằng tiếng Việt thường
  - Đọc thử một lượt: người không làm IT vẫn trả lời được từng câu

---

## Link phải tạo (standard markdown relative link — RULE-001, KHÔNG wiki-link)

| Từ | Tới | Quan hệ |
|----|-----|---------|
| `PRD-VETC.md` | `./SRS-VETC.md` | `Derived from:` |
| `PRD-VETC.md` | `./BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md` | `Business context:` |
| `PRD-VETC.md` | `../050-Research/Analysis-Open-Questions-VETC.md` | `Open questions:` |
| `BRD-001-...md` | `../SRS-VETC.md` | `Detailed spec:` |
| `BRD-001-...md` | `../PRD-VETC.md` | `Product spec:` |
| `BRD-001-...md` | `../../050-Research/Analysis-Open-Questions-VETC.md` | `Open questions:` |
| `Analysis-Open-Questions-VETC.md` | `../020-Requirements/SRS-VETC.md` | `Nguồn phân tích:` |
| `Analysis-Open-Questions-VETC.md` | `../020-Requirements/PRD-VETC.md` | `Liên quan:` |

## MOC cần cập nhật (PM làm ở close-step — writer KHÔNG chạm)

| MOC | Mục thêm/sửa |
|-----|--------------|
| `docs/020-Requirements/Requirements-MOC.md` | Mục 020.10 BRD: thêm link `BRD-001-...`. Mục 020.20: thêm link `PRD-VETC`. **Xử lý dead link `PRD-TNMCORE-OS.md`** (file không tồn tại — chờ anh chốt tại gate). |
| `docs/050-Research/Research-MOC.md` | MOC này hiện chỉ có heading, chưa có mục nào — thêm mục Analysis và link `Analysis-Open-Questions-VETC` |
| `docs/000-Index.md` | **Tạo mới** — RULE-001 quy định bắt buộc nhưng repo chưa có. Đăng ký PRD (tài liệu lớn) + trỏ tới 11 MOC hiện hữu |
| `docs/999-Resources/Glossary.md` | Bổ sung ~35 thuật ngữ domain VETC (Phần 5 findings). Giữ nguyên 3 thuật ngữ cũ, tách section riêng |

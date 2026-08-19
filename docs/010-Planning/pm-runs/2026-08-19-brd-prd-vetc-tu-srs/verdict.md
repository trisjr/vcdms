# Verdict: 2026-08-19-brd-prd-vetc-tu-srs

**Người verify**: `context-auditor` — **khác** agent đã viết (`business-analyst`), đúng guardrail "verify phải do agent khác agent đã thực thi".
**Phạm vi audit**: 3 tài liệu deliverable. Verifier chạy **read-only tuyệt đối** (`FILES_TOUCHED: none`).

| Khía cạnh | Trạng thái |
|-----------|-----------|
| **Completeness** | ✅ ĐẠT toàn bộ. BRD 11/11 mục · BR-01…BR-10 = 10 dòng. PRD 11/11 mục · FR 25 · NFR 7 · nhánh T-a…T-h = 8 · giả định 31 (0 trùng) · mâu thuẫn C-01…C-18 = 18. File câu hỏi 31 câu · 31 ô trả lời · phân bổ 11/11/9 khớp tuyệt đối outline. Frontmatter đủ `id/type/status/created/updated` cho cả 3, giá trị `id` đúng quy định. |
| **Correctness** | ✅ ĐẠT. 2 con số gốc SRS (≤ 2 giây, backup hàng ngày) nguyên vẹn, giữ đúng phạm vi áp dụng. Mọi con số khác bị nhốt trong bảng giả định mục 9 kèm nhãn "giả định thiết kế chờ xác nhận". BRD **không có** KPI/ngân sách/tỷ lệ nào bị điền số. FR-24/FR-25 để `TBD` + rào chắn 3 lớp chống bịa. Spot-check **20 trích dẫn** `d.NN`: 19 đúng, 1 sai → đã sửa (W-01). |
| **Coherence** | ✅ ĐẠT. Mã `Q-01…Q-31` khớp **tuyệt đối 31/31** giữa PRD và file câu hỏi (không thừa, không thiếu, không trùng). BRD tham chiếu 25 mã, tất cả đều tồn tại — **không có mã mồ côi**. 10 cặp hạng mục BRD↔PRD đối chiếu đều khớp. 7/7 thuật ngữ trong danh sách cấm = 0 kết quả. |
| **Connectivity** | ✅ ĐẠT. **0 wiki-link** trong cả 3 file. 9/9 markdown link phân giải được (đã `ls` từng đích). 8/8 link bắt buộc theo outline đủ, đúng nhãn quan hệ. Độ sâu relative path đúng (file trong `BRD/` lùi 2 cấp). Toàn bộ 33 anchor nội bộ có heading tương ứng. |

## CRITICAL

**Không có.** Verifier chủ động săn 5 nhóm lỗi CRITICAL và không tìm thấy nhóm nào: (a) con số bịa không nhãn, (b) trích dẫn SRS không tồn tại, (c) đứt truy vết `Q-NN`, (d) link gãy, (e) wiki-link.

Một **false positive đã tự loại**: chuỗi `](./File.md)` tại `PRD-VETC.md` trông như link gãy nhưng nằm trong backtick — là ví dụ minh họa cú pháp RULE-001, không phải link thật.

## WARNING — 4 mục, **đã xử lý hết 4**

| Mã | Nội dung | Xử lý |
|----|----------|-------|
| W-01 | PRD trích sai dòng SRS trong ô C-18: `d.154` (là "Kho xuất hàng") trong khi dòng chứa "đơn hàng" là `d.153`. | ✅ Sửa `d.154` → `d.153`. **Lưu ý**: lỗi này kế thừa từ `findings/business-analyst-gaps.md` — file findings là dấu vết phân tích tại thời điểm chạy nên **giữ nguyên không sửa ngược**, chỉ sửa ở deliverable. |
| W-02 | PRD cộng sai dòng roll-up bảng mâu thuẫn: ghi `7 🔴 · 8 🟡 · 3 🟢` trong khi đếm thực tế là `8 · 8 · 2`. Tổng 18 và 18 dòng vẫn đúng. | ✅ Sửa thành `8 mức 🔴 · 8 mức 🟡 · 2 mức 🟢`. |
| W-03 | PRD tự khai đã chuẩn hóa thuật ngữ "Đơn xuất thẻ" nhưng vẫn dùng "đơn hàng" ở giọng văn của chính nó tại 5 vị trí (mục lục, tiêu đề mục 6, và 3 dòng thân bài). | ✅ Sửa cả 5, gồm cập nhật anchor mục lục cho khớp heading mới. 9 lần "đơn hàng" còn lại đều **hợp lệ**: trích nguyên văn SRS (FR-10, FR-21, C-18), nhãn nút `[Hoàn thành đơn hàng]` do SRS đặt, và cụm "dữ liệu đơn hàng" trong bảng giả định. BRD vốn đã đạt. |
| W-04 | File gửi khách hàng còn `API` (2 chỗ) và `upload` (3 chỗ) chưa có gloss tiếng Việt. | ✅ Thêm gloss ở dòng **Bối cảnh** của Q-01, Q-02, Q-04, Q-13, Q-23 — **không đụng khối "Câu hỏi"** vì outline bắt buộc trích nguyên văn. Gloss thêm cả `sandbox`, `on-premise`, `cloud`, `store`. |

> Verifier ghi nhận W-04 có yếu tố giảm nhẹ: cả 5 vị trí đều nằm trong khối "Câu hỏi" mà outline bắt writer **giữ nguyên văn**. Writer bị kẹt giữa hai ràng buộc và đã chọn tuân thủ ràng buộc mạnh hơn — xử lý đúng. Cách vá của PM (gloss ở Bối cảnh) thỏa mãn được cả hai.

## SUGGESTION — 3 mục, xử lý 1

| Mã | Nội dung | Xử lý |
|----|----------|-------|
| S-01 | "phase 1" được gloss một lần rồi dùng trần trụi ở 4 chỗ sau đó trong file khách hàng. | ✅ Đã Việt hóa thành "giai đoạn 1" ở toàn bộ vị trí trần trụi. |
| S-02 | BRD xếp "luồng Nhập kho" ở mục *Phạm vi chưa xác định*, PRD xếp ở *Non-Goals* — khác khung trình bày. | ⏭️ **Không sửa.** Verifier đã xác nhận **không phải mâu thuẫn**: cả hai đều hedge về `Q-01` và nội dung khớp nhau. Khác nhau là do hai độc giả khác nhau, đúng chủ ý thiết kế tài liệu. |
| S-03 | Ước lượng "gấp 5–10 lần" trong PRD chưa gắn nguồn. | ⏭️ **Không sửa.** Đã hedge bằng "có thể" và nằm ở cột hệ quả, không vi phạm quy tắc số liệu. Ghi nhận để lần review sau cân nhắc. |

## Ghi nhận hiện trạng kho tài liệu (KHÔNG phải lỗi của run này)

Phát hiện trong lúc PM khảo sát để soạn `000-Index.md`. Đã ghi vào chính `000-Index.md` mục *Trạng thái kho tài liệu* để không bị quên:

- `docs/030-Specs/Specs-MOC.md` — **file rỗng 0 byte**, dù RULE-001 quy định là MOC bắt buộc.
- `docs/040-Design/Design-MOC.md` — **file rỗng 0 byte**, như trên.
- `docs/060-Manuals/` — **chưa tồn tại** dù RULE-001 có quy định tầng này.
- `docs/090-Archive/` — chưa tồn tại (tạo khi lần đầu cần deprecate tài liệu).

Bốn mục này **nằm ngoài phạm vi đã duyệt tại gate**. Cắt scope ở gate chứ không cắt ngầm giữa chừng — nên chúng được ghi nhận công khai thay vì âm thầm vá.

## Close-step (PM tự làm — đã hoàn tất 4/4)

| Hạng mục | Trạng thái |
|----------|-----------|
| `docs/020-Requirements/Requirements-MOC.md` | ✅ Đăng ký BRD-001 + PRD-VETC, thêm mục 020.50 trỏ chéo file câu hỏi, **gỡ dead link `PRD-TNMCORE-OS.md`**, bump `updated: 2026-08-19` |
| `docs/050-Research/Research-MOC.md` | ✅ Từ chỗ chỉ có heading → dựng đủ 4 mục điều hướng, đăng ký file câu hỏi, giải thích vai trò sợi truy vết `Q-NN` |
| `docs/000-Index.md` | ✅ **Tạo mới** (RULE-001 bắt buộc nhưng repo chưa hề có). Đăng ký 4 tài liệu lớn, điều hướng 10 MOC, cảnh báo `draft` và ghi nhận hiện trạng |
| `docs/999-Resources/Glossary.md` | ✅ Mở rộng từ 3 thuật ngữ không liên quan → ~35 thuật ngữ domain VETC có dẫn nguồn SRS, giữ 3 thuật ngữ cũ ở section riêng |

## Kết luận

**ĐÓNG ĐƯỢC RUN.** 0 CRITICAL. Toàn bộ 4 WARNING và 1 SUGGESTION khả thi đã được xử lý trong cùng run; 2 SUGGESTION còn lại được verifier xác nhận **không cần sửa** kèm lý do, không phải nợ kỹ thuật bị bỏ qua.

**Nợ lại có chủ đích** (đã cắt tại gate, không cắt ngầm): 4 hạng mục hiện trạng kho tài liệu nêu ở trên — cần một run riêng.

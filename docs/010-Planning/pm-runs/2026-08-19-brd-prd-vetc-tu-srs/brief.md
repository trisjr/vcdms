# Brief: 2026-08-19-brd-prd-vetc-tu-srs

**Lane**: doc
**Shape**: A — Authoring. Yêu cầu là tạo mới tài liệu (BRD, PRD, danh sách câu hỏi làm rõ) từ một nguồn đã có (`SRS-VETC.md`), không phải sweep chuẩn hóa kho docs hiện hữu.

## Yêu cầu gốc
> Điều phối phân tích docs/020-Requirements/SRS-VETC.md và khởi tạo file BRD và PRD từ requirement đó. Đồng thời các phần cần được làm rõ & confirm thì phải tách ra 1 file riêng để anh gửi cho khách hàng.

## Triage
| # | Câu hỏi | Đáp án | Lý do |
|---|---------|--------|-------|
| Q1 | Chạm nhiều hơn một tầng tài liệu? | **Có** | Ghi vào `020-Requirements` (PRD, BRD) + `050-Research` (file câu hỏi làm rõ) + cập nhật MOC ở cả hai tầng + tạo mới `docs/000-Index.md`. |
| Q2 | Sửa tài liệu `approved` / đổi taxonomy, naming, template dùng chung? | **Không** | `SRS-VETC.md` đang ở `status: draft`, và run này chỉ **đọc** nó, không sửa. Không phát sinh template hay quy ước thư mục mới. |
| Q3 | Yêu cầu mơ hồ (chưa rõ độc giả, phạm vi, định nghĩa "xong")? | **Không** | Ba deliverable được nêu tường minh. Có một điểm cần chốt tại gate (đặt file câu hỏi ở đâu vì Document Type Mapping không có loại "clarification list"), nhưng đó là quyết định placement, không phải scope mơ hồ. |
| Q4 | Vượt 5 file hoặc vượt 1 ngày công? | **Có** | Ước tính 6–7 file: PRD, BRD, Open-Questions, Requirements-MOC, Research-MOC, `000-Index.md`, có thể thêm Glossary. |

**Điểm**: 2/4 → **Tier**: T2
**Chọn tier thấp do phân vân**: Có — phân vân giữa T2 và T3. Chọn T2 vì phạm vi ghi gói gọn trong hai tầng tài liệu và chỉ cần **một** writer (ba file nội dung dùng chung một nguồn sự thật và cross-link lẫn nhau, cắt cho nhiều writer không mua được gì ngoài rủi ro ghi đè).
**Điều kiện escalate lên T3**: nếu phân tích của BA cho thấy phải sinh thêm Epic/User Story ở `022-User-Stories`, hoặc phải chuẩn hóa Glossary trên diện rộng.

## Ghi chú về Q3 (hedge)
BRD đòi hỏi business context mà SRS **không hề có**: business goal đo đếm được, KPI, ngân sách, stakeholder, ràng buộc thời gian, ROI. Đây trông như mơ hồ, nhưng chính khoảng trống đó **là deliverable thứ ba** — file câu hỏi gửi khách hàng. Nên yêu cầu tự thân không mơ hồ; phần thiếu được xử lý bằng `TBD` + một mục trong file câu hỏi, không phải bằng cách đoán.

## Assumptions
- **A1**: `SRS-VETC.md` là **nguồn sự thật duy nhất** cho run này. File `.docx` gốc tại `docs/999-Resources/` không được parse (định dạng nhị phân, không verify được bằng Read/Grep) → **sai thì hỏng ở đâu**: nếu `.docx` chứa yêu cầu mà SRS đã bỏ sót, BRD/PRD sẽ thiếu theo. Giảm thiểu: mọi khoảng trống đều được liệt kê trong file câu hỏi để khách hàng đối chiếu.
- **A2**: Quy ước `id` trong frontmatter theo pattern hiện hữu của repo (`SRS-VETC`), tức `{TYPE}-{ProjectName}`, thay vì `{TYPE}-{NNN}` của RULE-001 — **trừ BRD** vì naming convention của BRD bắt buộc `BRD-{NNN}-{Title}.md` → **sai thì hỏng ở đâu**: id không nhất quán giữa các tài liệu, gây khó khi tra cứu chéo về sau.
- **A3**: Không có thông tin nào về đơn vị vận chuyển đối tác, quy mô người dùng, sản lượng thẻ/tháng trong repo → mọi con số NFR trong PRD phải dẫn lại đúng SRS hoặc ghi `TBD`.

## Open questions
- Đặt file câu hỏi làm rõ ở đâu? Document Type Mapping không có loại "Clarification / Open Questions". → **chốt tại gate**.
- `Requirements-MOC.md` đang trỏ tới `./PRD-TNMCORE-OS.md` — file này **không tồn tại** (dead link có sẵn từ trước run này). Sửa luôn hay để nguyên? → **chốt tại gate**.
- `docs/000-Index.md` chưa tồn tại dù RULE-001 quy định BẮT BUỘC phải có. Tạo trong run này (vì close-step yêu cầu đăng ký PRD vào đó) → **chốt tại gate**.

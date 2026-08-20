# Escalations: 2026-08-20-wbs-eta-va-proposal-vetc

## E1 — Anh cấp ngân sách và timeline thật tại gate → nâng tier T1 lên T2

- **Tầng**: 2 (PM tự quyết) — thay đổi tier, không thay đổi scope hay lane.
- **Worker**: chưa dispatch worker nào. Phát sinh tại Bước 3 (gate).
- **Bối cảnh**: PM trình gate với QĐ-03 gồm 3 phương án về cơ sở của cột Effort/Timeline, tất cả đều dựa trên tiền đề *"PRD và BRD đều ghi rõ không có ngân sách, không có mốc go-live"*. Anh **không chọn phương án nào** mà cấp thẳng dữ liệu:
  > *"Ngân sách ~ 10 triệu VND, Thời gian dự kiện trong vòng 10 ngày để hoàn thành các chức năng chính để có thể hoạt động còn các chức năng bổ sung thì hoàn thành sau"*

- **Vì sao đây là escalation chứ không phải câu trả lời gate thông thường**: tiền đề của cả 3 phương án bị vô hiệu. Assumption `A-03`, `A-04`, `A-06` trong `brief.md` bị thay; phát sinh `A-08`, `A-09`, `A-10`. Đồng thời rủi ro của deliverable đổi bản chất: từ *"không có số nào để đối chiếu"* thành *"có 2 con số cứng mà toàn bộ cột Effort phải đối chiếu"*.

- **Quyết định**: **nâng tier T1 → T2**, bổ sung phase verify bởi `context-auditor`.
  **Lý do**: `brief.md` đã ghi sẵn điều kiện escalate — *"số liệu ETA không truy được về nguồn đã khai trong outline"*. Ràng buộc 10 ngày / 10 triệu tạo áp lực trực tiếp lên cột Effort: writer rất dễ **bóp số cho vừa ràng buộc** thay vì ước lượng thật, và đó là loại lỗi mà chính writer không tự phát hiện được vì nó đọc đúng bộ context nó vừa tạo. Verify bởi agent thứ ba ở đây có giá trị thật, không phải nghi thức rỗng.

- **Hành động**:
  1. Cập nhật mục Gate của `run-plan.md` với 3 quyết định + hệ quả + assumption mới (đã làm).
  2. Cập nhật `outline.md` (PM độc quyền) cho khớp cấu trúc 2 tầng Core/Bổ sung + mục Gap Analysis + mục Ngân sách.
  3. Dispatch `product-owner` soạn `WBS-ETA-VETC.md` theo outline mới.
  4. Dispatch `context-auditor` verify sau khi writer xong.
  5. **Không sửa ngược** phần trên của `run-plan.md` (bảng Phases, ownership map) — đó là dấu vết kế hoạch tại thời điểm gate. Chênh lệch nằm ở đây.

- **Ghi chú PM về chất lượng deliverable**: 12 FR + 5 NFR mức P0 trong 10 ngày với ~10 triệu VND là ràng buộc rất chặt. PM **không** che điều này bằng cách chia nhỏ effort cho vừa. `WBS-ETA-VETC.md` sẽ trình bày song song: effort bottom-up thật · ràng buộc của anh · khoảng cách · phương án cắt scope. Quyết định cắt scope là của anh, không phải của PM.

## E2 — `.agent/roles/` không tồn tại trong repo

- **Tầng**: 2 (PM tự quyết).
- **Bối cảnh**: `Dispatch Prompt Template` của `pm-core.md` yêu cầu chèn `[ROLE] Nạp .agent/roles/<role>.md`. Kiểm tra thực tế: thư mục `.agent/roles/` **không tồn tại**. Chỉ có `.agent/workflows/`.
- **Quyết định**: bỏ dòng `[ROLE]` trỏ tới file không có; thay bằng trỏ tới **role memory** thật sự tồn tại tại `knowledge-base/45-Role-Memory/<role>/` khi có, và mô tả role trực tiếp trong prompt.
  **Lý do**: để con trỏ chết trong prompt khiến worker tốn lượt tool đi mò một file không có, rồi tự suy diễn persona — tệ hơn là nói thẳng.
- **Hành động**: áp dụng cho mọi dispatch của run này. Không sửa `pm-core.md` (ngoài scope run này, và nó là file contract dùng chung).

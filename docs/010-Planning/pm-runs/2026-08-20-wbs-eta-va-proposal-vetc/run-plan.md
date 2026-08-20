# Run Plan: 2026-08-20-wbs-eta-va-proposal-vetc

**Lane**: doc · **Shape**: A · **Tier**: T1 (điểm 1/4, chọn thấp do phân vân với T2)

## Phases

| # | Phase | Agent | Song song? | Input | Output |
|---|-------|-------|-----------|-------|--------|
| 1 | Soạn bảng WBS kết hợp ETA | `product-owner` | Không | PRD §4/§5/§6/§9, BRD §4/§6/§7/§8.3/§9, `Template-WBS-ETA.md`, toàn văn outline hạng mục 1 | `docs/010-Planning/Estimates/WBS-ETA-VETC.md` |
| 2 | Soạn Proposal HTML + publish Artifact | **PM (main loop)** | Không — phụ thuộc phase 1 | PRD, BRD, + WBS/ETA từ phase 1 | `docs/010-Planning/Proposal-VETC.html` + Artifact URL |
| 3 | Verify (Validation Checklist RULE-001) | **PM** (T1) | Không | Cả 2 deliverable | `verdict.md` |
| 4 | Close-step: cập nhật MOC + Index, commit & push | **PM** | Không | — | `Planning-MOC.md`, `000-Index.md` |

> **Không có phase nào chạy song song.** Phase 2 trích số liệu tổng effort từ phase 1; phase 3 cần cả hai. Đây là chuỗi phụ thuộc thật, không phải lựa chọn.

## File ownership map

| Agent | Sở hữu (được ghi) | Cấm chạm |
|-------|-------------------|----------|
| `product-owner` | `docs/010-Planning/Estimates/WBS-ETA-VETC.md` — **đúng một file này** | Mọi file khác. Đặc biệt: `docs/020-Requirements/**` (read-only), `Planning-MOC.md`, `000-Index.md`, `Documents-Template.md`, `Template-WBS-ETA.md`, toàn bộ `pm-runs/**` |
| **PM (main loop)** | `docs/010-Planning/Proposal-VETC.html`, `docs/010-Planning/Planning-MOC.md`, `docs/000-Index.md`, toàn bộ `docs/010-Planning/pm-runs/2026-08-20-wbs-eta-va-proposal-vetc/**` | `docs/010-Planning/Estimates/WBS-ETA-VETC.md` trong lúc phase 1 đang chạy |

> Ownership rời nhau tuyệt đối. Chỉ có 1 worker nên không có khả năng va chạm ghi.
> `outline.md` thuộc PM độc quyền — worker báo xong trong `SUMMARY`, PM tick.

## Artifact sẽ tạo/sửa ngoài run-state

- `docs/010-Planning/Estimates/` — **thư mục mới**, tạo theo đúng RULE-001 §Cấu trúc thư mục bắt buộc (thư mục này đã được RULE-001 định nghĩa sẵn, chỉ là chưa tồn tại trên đĩa).
- `docs/010-Planning/Estimates/WBS-ETA-VETC.md` — deliverable 1.
- `docs/010-Planning/Proposal-VETC.html` — deliverable 2 (đích **chờ anh chốt tại gate**, xem QĐ-02).
- `docs/010-Planning/Planning-MOC.md` — cập nhật MOC (close-step).
- `docs/000-Index.md` — cập nhật index (close-step).

## Ba quyết định cần anh chốt tại gate

### QĐ-01 — Định dạng bảng WBS+ETA

| Phương án | Nội dung | Đánh giá |
|---|---|---|
| **A** *(em đề xuất)* | **1 file `.md`** duy nhất: `Estimates/WBS-ETA-VETC.md`, gộp mục WBS và mục ETA | Khớp đúng yêu cầu *"1 bảng WBS kết hợp ETA"* của anh, và khớp `Template-WBS-ETA.md` sẵn có. **Sai lệch khỏi RULE-001** ở chỗ mapping ghi `.xlsx` — em ghi rõ sai lệch này, không lách |
| B | 2 file `.xlsx` rời: `WBS-VETC.xlsx` + `ETA-VETC.xlsx` | Đúng chữ Document Type Mapping, nhưng **trái yêu cầu "kết hợp"** của anh, và không dùng được `Template-WBS-ETA.md` |
| C | 1 file `.md` + xuất kèm 1 file `.xlsx` | Đủ cả hai, nhưng phát sinh **2 nguồn sự thật cho cùng một bảng** — sửa một chỗ quên chỗ kia là chuyện chắc chắn xảy ra |

### QĐ-02 — Đích của Proposal HTML

> "Proposal" **không có** trong Document Type Mapping. Guardrail lane doc bắt em hỏi thay vì tự chế đường dẫn.

| Phương án | Nội dung | Đánh giá |
|---|---|---|
| **A** *(em đề xuất)* | `docs/010-Planning/Proposal-VETC.html` + publish thành **Artifact** để anh mở link review | Nằm trong hệ Dewey (010-Planning là chỗ đúng cho tài liệu đề xuất triển khai), và anh review được ngay trên trình duyệt |
| B | `docs/010-Planning/Charter-VETC.html`, coi proposal như Project Charter | Dùng đúng một entry đã có trong mapping, nhưng **charter ≠ proposal** về mục đích — gọi sai tên tài liệu sẽ gây nhầm cho người đọc sau |
| C | `docs/010-Planning/Proposal-VETC.html` + thêm bản `.md` song song để MOC link được | Giải quyết OQ-02 (MOC vốn dùng markdown link), nhưng lại sinh **2 nguồn sự thật** cho cùng nội dung |

### QĐ-03 — Cơ sở của cột Effort và Timeline trong ETA

| Phương án | Nội dung | Đánh giá |
|---|---|---|
| **A** *(em đề xuất)* | Effort **man-day**, timeline **tương đối (Tuần 1…N)**, FR-24/FR-25 để `TBD`, và §0 tuyên bố rõ đây là ước lượng chờ xác nhận | Không bịa ngày go-live (BRD ghi rõ *không có mốc thời gian*), không ước lượng 2 FR mà PRD **cấm** ước lượng. Anh có ngày khởi công thật thì chỉ cần cộng offset |
| B | Điền ngày dương lịch, mốc bắt đầu = 2026-08-25 | Trực quan hơn để đọc, nhưng đó là **bịa cam kết tiến độ** từ một ngày em tự chọn |
| C | Chỉ làm WBS, bỏ hẳn cột Effort vì chưa có dữ liệu | An toàn tuyệt đối về ảo giác, nhưng **không đáp ứng yêu cầu "kết hợp ETA"** của anh |

## Gate
- Trình ngày: 2026-08-20
- Kết quả: **Duyệt kèm điều chỉnh**
- **QĐ-01**: Phương án A — 1 file `.md` kết hợp tại `docs/010-Planning/Estimates/WBS-ETA-VETC.md`. ✅ như đề xuất.
- **QĐ-02**: Phương án A — `docs/010-Planning/Proposal-VETC.html` + publish Artifact. ✅ như đề xuất.
- **QĐ-03**: **Anh không chọn A/B/C — anh cấp dữ liệu thật:**
  > *"Ngân sách ~ 10 triệu VND, Thời gian dự kiến trong vòng 10 ngày để hoàn thành các chức năng chính để có thể hoạt động còn các chức năng bổ sung thì hoàn thành sau"*

### Điều chỉnh của anh — hệ quả lên run plan

Câu trả lời QĐ-03 **thay thế 3 assumption** trong `brief.md`:

| Assumption cũ | Trạng thái | Thay bằng |
|---|---|---|
| **A-03** — timeline tương đối Tuần 1…N vì "không có mốc go-live" | ❌ **Bị thay** | **Có ràng buộc thật: 10 ngày cho giai đoạn Core.** ETA dùng đơn vị **Ngày (D1…D10)** cho Core; giai đoạn Bổ sung vẫn dùng timeline tương đối vì anh nói *"hoàn thành sau"* mà chưa cho mốc. |
| **A-04** — effort MD, phạm vi Giai đoạn 1 theo BRD A-01 | 🔶 **Thu hẹp** | Vẫn MD, nhưng **chia 2 tầng**: Core (10 ngày) và Bổ sung (chưa có mốc). |
| **A-06** — proposal không chứa ngân sách vì "PRD/BRD đều không có ngân sách" | ❌ **Bị thay** | **Có ngân sách thật: ~10.000.000 VND.** Proposal và ETA phải trình bày con số này. |

### Assumption MỚI phát sinh từ câu trả lời

- **A-08** — **"Chức năng chính để có thể hoạt động" = toàn bộ hạng mục mức `P0` của PRD.**
  Căn cứ: PRD §4 định nghĩa nguyên văn `P0` = *"bắt buộc cho bản chạy được đầu tiên"* — trùng khớp tuyệt đối với cách anh diễn đạt. Vậy Core = **12 FR** (FR-01, 02, 04, 05, 06, 07, 11, 12, 14, 18, 19, 22) + **5 NFR** (NFR-01…NFR-05). Bổ sung = P1 (10 FR + NFR-06, 07) rồi P2 (3 FR).
  → **sai thì hỏng ở đâu**: nếu anh hiểu "chức năng chính" hẹp hơn P0 (ví dụ bỏ FR-14 truy vết khỏi Core) thì phải cắt lại tầng Core; sửa rẻ vì WBS đã đánh dấu tầng theo từng dòng.

- **A-09** — **~10 triệu VND là ngân sách của riêng giai đoạn Core (10 ngày)**, không phải toàn dự án.
  Căn cứ: hai con số nằm trong cùng một câu và cùng gắn với cụm *"các chức năng chính"*; phần *"chức năng bổ sung hoàn thành sau"* không kèm ngân sách nào.
  → **sai thì hỏng ở đâu**: nếu 10 triệu là trần cho **toàn bộ** dự án thì giai đoạn Bổ sung không còn ngân sách và phải cắt scope tiếp — em nêu thẳng điểm này trong mục Gap Analysis để anh chốt.

- **A-10** — **ETA ước lượng bottom-up trước, đối chiếu ràng buộc sau.** Em **không bóp** effort cho vừa 10 ngày / 10 triệu. WBS sẽ có mục **Gap Analysis** đặt cạnh nhau: (a) effort đội cần theo phân rã thật, (b) ràng buộc anh đưa, (c) khoảng cách, (d) phương án cắt scope nếu có khoảng cách.
  → **sai thì hỏng ở đâu**: nếu em bóp số cho khớp thì bản WBS trở thành tài liệu hợp lý hóa một cam kết không thực hiện được — đúng thứ rủi ro nghiệm thu mà BRD §10 cảnh báo. Không có rủi ro nào khi trình bày trung thực.

### Thay đổi Tier: T1 → T2

Ràng buộc mới đưa vào 2 con số cứng (10 ngày, 10 triệu) mà **toàn bộ cột Effort phải đối chiếu**. Đây đúng là điều kiện escalate đã ghi sẵn trong `brief.md`. Bổ sung **phase 3b: verify bởi `context-auditor`** (agent thứ ba, không phải writer) trước khi PM đóng run. Ghi chi tiết tại `escalations.md` mục E1.

# Brief: 2026-08-20-wbs-eta-va-proposal-vetc

## Yêu cầu gốc
> Từ docs/020-Requirements/PRD-VETC.md & docs/020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md, em hãy tạo 1 bảng WBS kết hợp ETA, sau đó từ 3 file trên tạo 1 bản proposal có định dạng HTML để anh review lại

**Lane**: doc
**Shape**: A — Authoring. Tạo mới 2 deliverable (WBS+ETA, Proposal HTML), không phải sweep chuẩn hóa kho docs đang có.

> Diễn giải "3 file trên" = PRD-VETC + BRD-001 + **bảng WBS/ETA vừa tạo ở bước 1**. Vì vậy hai deliverable có quan hệ phụ thuộc tuần tự, không có chỗ nào chạy song song được.

## Triage
| # | Câu hỏi | Đáp án | Lý do |
|---|---------|--------|-------|
| Q1 | Chạm > 1 tầng tài liệu? | **Không** | Cả 2 deliverable đều thuộc tầng `010-Planning`. PRD/BRD chỉ được **đọc** làm nguồn sự thật, không sửa. |
| Q2 | Sửa tài liệu `approved`, hoặc đổi taxonomy / naming / template dùng chung? | **Không** | PRD/BRD/SRS đang `status: draft` và không bị sửa. `Documents-Template.md` (RULE-001) và `Template-WBS-ETA.md` **không bị chỉnh sửa**. Thư mục `Estimates/` là thư mục đã được RULE-001 định nghĩa sẵn, tạo nó không phải đổi taxonomy. |
| Q3 | Mơ hồ — chưa rõ độc giả đích, phạm vi, hoặc thế nào là "xong"? | **Có** | "Proposal" **không có trong Document Type Mapping** của RULE-001 → chưa có đích và naming convention. Chưa rõ độc giả (khách hàng ngoài vs nội bộ) và chưa rõ có bao gồm giá / ngân sách hay không. |
| Q4 | > 5 file hoặc > 1 ngày công? | **Không** | 2 file deliverable + 2 file MOC/Index do PM cập nhật = 4 file. |

**Điểm**: 1/4 → **Tier**: T1

**Chọn tier thấp do phân vân**: **Có** — phân vân giữa T1 và T2.
- Lý do nghiêng T2: nội dung ETA có rủi ro ảo giác **cao nhất trong các loại tài liệu** — một con số man-day bịa ra trông y hệt một con số có căn cứ, và nó sẽ bị dùng làm cam kết. Verify bởi `context-auditor` (agent thứ ba) có giá trị thật ở đây.
- Lý do chốt T1 theo đúng *quy tắc phân vân* của `pm-core.md`: escalate giữa chừng rẻ hơn chạy thừa full path; PM đã giữ toàn bộ nội dung PRD §4/§5/§9 và BRD §4/§9 trong context nên không cần analysis fan-out.
- **Điều kiện escalate lên T2**: writer trả `PARTIAL`/`BLOCKED`, **hoặc** PM đọc `FILES_TOUCHED` thấy có dòng ETA nào mang số liệu không truy được về nguồn đã khai trong outline. Khi đó dispatch thêm `context-auditor` để verify và ghi vào `escalations.md`.

## Assumptions

- **A-01** — "1 bảng WBS kết hợp ETA" = **một file duy nhất** gộp cả 2 mục, đúng theo `Template-WBS-ETA.md` (template này vốn đã chứa cả mục WBS và mục ETA).
  → **sai thì hỏng ở đâu**: nếu anh muốn 2 file rời như Document Type Mapping quy định (`WBS-{ProjectName}.xlsx` + `ETA-{ProjectName}.xlsx`) thì phải tách file và đổi naming — sửa sau rẻ, chỉ là tách nội dung.

- **A-02** — Deliverable là **Markdown (`.md`)**, không phải `.xlsx`. Document Type Mapping ghi `.xlsx` nhưng repo chỉ có `Template-WBS-ETA.md` dạng markdown, và toàn bộ kho `docs/` hiện không có file `.xlsx` nào.
  → **sai thì hỏng ở đâu**: cần file Excel thật để nhập vào MS Project / ClickUp thì phải chạy lại bằng skill `xlsx`. Đây là **sai lệch có chủ ý khỏi RULE-001**, đưa ra gate để anh duyệt.

- **A-03** — ETA dùng **timeline tương đối (Tuần 1…N)**, **không dùng ngày dương lịch**. Căn cứ: BRD d.59 ghi rõ *"không có mốc thời gian go-live"*; PRD §9 Q-30 ghi *"Timeline TBD"*.
  → **sai thì hỏng ở đâu**: điền ngày dương lịch lúc này là **bịa cam kết tiến độ** — đúng loại lỗi mà PRD §9 cảnh báo. Nếu anh có ngày khởi công thật, chỉ cần cộng offset vào cột Tuần, không phải làm lại WBS.

- **A-04** — Effort tính bằng **man-day (MD)**, và là **ước lượng của đội chờ xác nhận**, không phải báo giá. Phạm vi ước lượng = **Giai đoạn 1** theo BRD A-01 (chỉ luồng XUẤT; tồn kho khởi tạo bằng import Excel một lần).
  → **sai thì hỏng ở đâu**: nếu Q-01 được chốt là "có làm luồng nhập kho" thì toàn bộ nhóm tồn kho phải ước lượng lại (PRD §9 gọi Q-01 là *"tác động lớn nhất toàn dự án"*).

- **A-05** — **FR-24 và FR-25 để `TBD`, không ước lượng công.** Căn cứ nguyên văn PRD §4: *"không được ước lượng công cho tới khi Q-28 có câu trả lời"*.
  → **sai thì hỏng ở đâu**: ước lượng 2 FR không có đặc tả là mời scope creep vào thẳng bản proposal. Không có rủi ro nào khi để TBD.

- **A-06** — Proposal HTML là tài liệu **nội bộ để anh review**, chưa phải bản gửi khách hàng. Vì vậy **không chứa giá, không chứa điều khoản thương mại** — cả PRD và BRD đều ghi rõ không có ngân sách.
  → **sai thì hỏng ở đâu**: nếu đây là bản gửi khách hàng thật thì cần thêm phần thương mại và cần anh cấp số liệu giá — PM không được tự sinh.

- **A-07** — Proposal **phải có mục "Giả định & Điều kiện"** phản chiếu PRD §9. Không có mục này thì bản HTML trở thành tài liệu đầu tiên trong repo **biến giả định thành cam kết**.
  → **sai thì hỏng ở đâu**: bỏ mục này là rủi ro tranh chấp nghiệm thu — chính rủi ro mà BRD §10 đã cảnh báo.

## Open questions
- **OQ-01** — "Proposal" không có trong Document Type Mapping của RULE-001. Đặt ở đâu, tên gì? → **PM đưa ra gate**, không tự chế đường dẫn (Guardrail lane doc: *"Không có chỗ cho tài liệu → hỏi anh"*).
- **OQ-02** — Proposal có cần bản `.md` song song để nằm trong hệ thống link/MOC không? File `.html` không được các MOC hiện tại tham chiếu theo quy ước markdown link. → **PM đưa ra gate**.
- **OQ-03** — `.agent/roles/` **không tồn tại** trong repo, nên câu `[ROLE] Nạp .agent/roles/<role>.md` của Dispatch Prompt Template là con trỏ chết. PM bỏ dòng đó khỏi prompt dispatch thay vì để worker mò file không có. Đây là quyết định Tầng 2, ghi lại để lần sau không mò lại.

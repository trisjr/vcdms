---
id: WBS-ETA-VETC
type: wbs
status: draft
project: VETC
owner: "@trisjr"
created: 2026-08-20
---

# 📊 WBS & ETA — Hệ thống Quản lý Xuất kho & Phân phối thẻ VETC (VCDMS)

## 0. Phạm vi, ràng buộc và quy ước của bản ước lượng

### 0.1. Ràng buộc do khách hàng cấp

| Ràng buộc | Giá trị | Nguồn |
| :--- | :--- | :--- |
| Ngân sách | **~10.000.000 VND** | Ràng buộc do khách hàng cấp tại gate 2026-08-20 |
| Thời gian | **10 ngày** để hoàn thành *"các chức năng chính để có thể hoạt động"*; các chức năng bổ sung hoàn thành sau | Ràng buộc do khách hàng cấp tại gate 2026-08-20 |

> ⚠️ **Hai con số trên KHÔNG có trong PRD, BRD hay SRS.** Cả PRD ([mục 8](../../020-Requirements/PRD-VETC.md)) và BRD ([mục 3.2, mục 8.2](../../020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md)) đều ghi ngân sách và mốc go-live là `TBD` (chờ **Q-29**, **Q-30**). Hai con số này là **ràng buộc do khách hàng cấp trực tiếp tại gate 2026-08-20**, không được gán cho PRD/BRD.

### 0.2. Hai tầng phạm vi

| Tầng | Nội dung | Ràng buộc gắn kèm |
| :--- | :--- | :--- |
| **CORE** | Toàn bộ mức `P0` của PRD: **12 FR** (FR-01, FR-02, FR-04, FR-05, FR-06, FR-07, FR-11, FR-12, FR-14, FR-18, FR-19, FR-22) + **5 NFR** (NFR-01, NFR-02, NFR-03, NFR-04, NFR-05). | 10 ngày · ~10.000.000 VND |
| **BỔ SUNG** | Mức `P1`: **10 FR** (FR-03, FR-08, FR-09, FR-10, FR-13, FR-15, FR-20, FR-21, FR-23, FR-24) + **2 NFR** (NFR-06, NFR-07). Sau đó mức `P2`: **3 FR** (FR-16, FR-17, FR-25). | Chưa có mốc thời gian |

**Căn cứ của phép chia**: PRD [mục 4](../../020-Requirements/PRD-VETC.md) định nghĩa nguyên văn quy ước ưu tiên — `P0` = *"bắt buộc cho bản chạy được đầu tiên"*. Cách diễn đạt này trùng khớp với cách khách hàng diễn đạt tại gate: *"các chức năng chính để có thể hoạt động"*. Vì vậy tầng CORE được đặt bằng đúng tập `P0`, không tự chia lại.

### 0.3. Đơn vị và quy ước mốc thời gian

- Đơn vị effort: **man-day (MD)** — công của **một người trong một ngày làm việc**. MD **không** phụ thuộc quy mô đội; quy mô đội chỉ quyết định 72,5 MD trải ra bao nhiêu ngày lịch.
- Tầng **CORE** dùng mốc tương đối **D1…D10** (ngày làm việc thứ 1 đến thứ 10 tính từ ngày khởi động).
- Tầng **BỔ SUNG** dùng mốc tương đối **W+1, W+2…** (tuần thứ N sau khi tầng CORE go-live).
- Toàn tài liệu **không dùng ngày dương lịch** cho lịch trình, vì mốc khởi động chưa được chốt (BRD mục 8.2: go-live `TBD` — **Q-30**).

### 0.4. Nhãn dùng xuyên tài liệu

Giữ nguyên 3 nhãn của PRD:

| Nhãn | Ý nghĩa |
| :--- | :--- |
| **[SRS]** | Có căn cứ trực tiếp/nguyên văn trong SRS-VETC. Được phép triển khai. |
| **[SUY LUẬN]** | PO/BA suy ra, có nêu căn cứ. Cần xác nhận trước khi chốt. |
| **[TBD]** | Chưa có dữ liệu. Chờ khách hàng trả lời mã `Q-NN`. **Không được tự bịa nội dung.** |

### 0.5. Quy mô nhân sự — **[SUY LUẬN]**, cần anh xác nhận

> 🔴 **PRD và BRD không nói gì về quy mô đội (team size).** Không có mã `Q-NN` nào hỏi về việc này, và SRS cũng im lặng. Toàn bộ nội dung mục 0.5 là **[SUY LUẬN]**, **không phải dữ kiện**.

**Căn cứ suy luận** — từ tỉ lệ ngân sách/thời gian do khách hàng cấp:

`10.000.000 VND ÷ 10 ngày = 1.000.000 VND/ngày` cho **toàn đội**.

Tỉ lệ này hàm ý một đội **cực nhỏ: 1–2 người kiêm nhiệm nhiều vai**, chứ không phải một đội đủ 7 vai trò riêng biệt.

**Cách bản ước lượng này xử lý điểm chưa rõ đó:**

1. Cột `Owner` trong WBS ghi **vai trò chuẩn hóa** (PM / BA / Architect / Designer / Engineer / QA / DevOps) để mô tả *loại việc*, **không** hàm ý mỗi vai là một người riêng.
2. Cột `Effort (MD)` là **khối lượng công**, độc lập với việc ai làm. Một người kiêm 3 vai **không giảm** tổng MD — chỉ **kéo dài** số ngày lịch.
3. Phần đối chiếu ràng buộc (mục 5) tính cho **cả hai giả thiết**: đội 1–2 người (suy ra từ ngân sách) và đội cần thiết để nhồi 72,5 MD vào 10 ngày.

**Điểm cần anh xác nhận:**

| # | Câu hỏi | Vì sao cần |
| :--- | :--- | :--- |
| **E-01** | Đội thực thi gồm **bao nhiêu người**, mỗi người kiêm những vai nào? | Quyết định 72,5 MD trải ra bao nhiêu ngày lịch. |
| **E-02** | **10.000.000 VND là chi phí gì**: chi phí nhân công, hay chi phí công cụ/hạ tầng (AI agent, hosting, domain) còn nhân công do anh tự đảm nhiệm? | Nếu là chi phí công cụ thì phép quy đổi *đơn giá VND/MD* ở mục 5 **không áp dụng** và cần thay bằng phép đối chiếu khác. |
| **E-03** | Đơn giá ngày (VND/MD) thực tế mà anh đang dùng cho nguồn lực này? | Bản ước lượng **không** giả định đơn giá thị trường; mục 5 chỉ đưa bảng độ nhạy để anh chọn. |

### 0.6. Tuyên bố bắt buộc về độ tin cậy của số liệu

> 🔴 **Cột `Effort (MD)` trong toàn tài liệu này là ước lượng bottom-up của đội, CHƯA PHẢI CAM KẾT.** Số liệu được lập theo trình tự: ước lượng theo độ phức tạp từng hạng mục **trước**, đối chiếu với ràng buộc 10 ngày / 10.000.000 VND **sau**. Không có con số nào bị điều chỉnh để khớp ràng buộc.
>
> **Hai con số duy nhất có nguồn SRS** trong toàn bộ bộ tài liệu VETC là **tra cứu ≤ 2 giây** (NFR-06) và **sao lưu hàng ngày** (NFR-07). Mọi con số khác — bao gồm toàn bộ cột Effort ở đây — là ước lượng hoặc giả định thiết kế chờ xác nhận.
>
> **Độ tin cậy của ước lượng bị giới hạn bởi 31 giả định thiết kế đang mở** (PRD mục 9, trong đó 11 mức 🔴 Blocker). Khi khách hàng trả lời khác giả định, effort sẽ thay đổi — xem mục 8.

---

## 1. Work Breakdown Structure (WBS)

| WBS ID | Task Name | Deliverable | Owner | Tầng | FR/NFR liên quan |
| :--- | :--- | :--- | :--- | :---: | :--- |
| **1.0** | **Discovery & Chốt yêu cầu (trả lời 31 câu `Q-NN`)** | | | | |
| 1.1 | Chuẩn bị và chạy workshop chốt **11 câu Blocker** (Q-01, Q-02, Q-03, Q-04, Q-05, Q-06, Q-09, Q-10, Q-11, Q-12, Q-21) | Biên bản workshop + 11 quyết định đã chốt, có chữ ký xác nhận của khách hàng | BA | CORE | — |
| 1.2 | Chốt **8 nhánh state machine** T-a…T-h (PRD mục 6.2) và vòng đời Thẻ (T-h) | Bảng quyết định 8 nhánh + sơ đồ state machine đã chốt | BA | CORE | — |
| 1.3 | Cập nhật PRD/BRD theo câu trả lời đã nhận; đóng các mục `TBD` bị ảnh hưởng | PRD/BRD phiên bản `review`, danh sách `TBD` còn lại | BA | CORE | — |
| 1.4 | Chốt nhóm câu hỏi của tầng BỔ SUNG (Q-02 chi tiết carrier, Q-03, Q-19, Q-28) | Bộ quyết định cho tầng BỔ SUNG | BA | BỔ SUNG | — |
| **2.0** | **Kiến trúc & Thiết kế hệ thống** | | | | |
| 2.1 | Thiết kế kiến trúc tổng thể, chọn tech stack, phân tầng module | `SDD-VCDMS.md` | Architect | CORE | — |
| 2.2 | Thiết kế DB schema: Đơn xuất thẻ, Thẻ/Dải Series, Kho, User, Audit Log | Bộ `DB-Entity-*.md` + ERD | Architect | CORE | — |
| 2.3 | Đặc tả API cho toàn bộ luồng tầng CORE | Bộ `Endpoint-*.md` (OpenAPI spec) | Architect | CORE | — |
| 2.4 | ADR: state machine mở rộng được (không hardcode enum) + lớp data-scope | `ADR-001-State-Machine.md`, `ADR-002-Data-Scope.md` | Architect | CORE | — |
| 2.5 | ADR + đặc tả tích hợp carrier theo mô hình adapter/plugin | `ADR-003-Carrier-Adapter.md`, `Spec-Integration-Carrier.md` | Architect | BỔ SUNG | FR-08, FR-09 |
| **3.0** | **Thiết kế UI/UX** | | | | |
| 3.1 | User flow 5 bước + wireframe desktop (tạo đơn, soát xét kho, duyệt Admin) | `UF-Don-Xuat-The.md` + bộ wireframe desktop | Designer | CORE | FR-01, FR-02, FR-04, FR-05, FR-06, FR-07, FR-22 |
| 3.2 | Wireframe **mobile Bước 5**: chụp ảnh POD, đối soát dải Series, xác nhận một chạm | Bộ wireframe mobile Bước 5 + đặc tả tương tác | Designer | CORE | FR-11, FR-12 |
| 3.3 | Design system cơ bản: token màu/typography, component list, layout responsive | `docs/040-Design/Design-System/` (bộ component) | Designer | CORE | — |
| 3.4 | Wireframe tracking timeline, bộ lọc nâng cao, màn hình tra cứu | Bộ wireframe tầng BỔ SUNG | Designer | BỔ SUNG | FR-09, FR-10, FR-20, FR-21 |
| **4.0** | **Nền tảng & Hạ tầng** | | | | |
| 4.1 | Project setup: khởi tạo repo FE + BE, lint/format, convention, skeleton auth-less | Repo chạy được ở local + `README` hướng dẫn | Engineer | CORE | — |
| 4.2 | CI/CD pipeline + dựng môi trường `dev` và `staging` | Pipeline build/test/deploy tự động | DevOps | CORE | — |
| 4.3 | Cấu hình HTTPS (SSL/TLS) và mã hóa dữ liệu nhạy cảm ở tầng lưu trữ | Checklist bảo mật đã pass + cấu hình TLS trên môi trường | DevOps | CORE | NFR-03 |
| 4.4 | Dựng object storage cho ảnh POD (đặt tại Việt Nam theo giả định Q-13) | Bucket + policy truy cập + SDK upload đã thông | DevOps | CORE | NFR-03 |
| 4.5 | Monitoring / alerting cơ bản (uptime, lỗi tích hợp carrier) | Dashboard giám sát + kênh alert | DevOps | BỔ SUNG | — |
| **5.0** | **Danh mục & Master data** | | | | |
| 5.1 | CRUD Danh mục kho (tạo/sửa/xóa/**ẩn**) | Module Danh mục kho chạy được + test case pass | Engineer | CORE | FR-18 |
| 5.2 | Thông tin chi tiết kho: tên, địa chỉ, NV phụ trách gửi hàng, SĐT liên hệ | Form chi tiết kho + validation | Engineer | CORE | FR-19 |
| 5.3 | CRUD **Danh mục Loại thẻ** — ⚠️ *giả định thiết kế (PRD mục 9, **Q-27**), KHÔNG phải FR chính thức trong danh sách 25 FR* | Module Danh mục Loại thẻ | Engineer | BỔ SUNG | FR-27 *(giả định Q-27)* |
| 5.4 | CRUD **Danh mục Đại lý** — ⚠️ *giả định thiết kế (PRD mục 9, **Q-31**), KHÔNG phải FR chính thức trong danh sách 25 FR* | Module Danh mục Đại lý | Engineer | BỔ SUNG | FR-31 *(giả định Q-31)* |
| 5.5 | Quản lý danh mục nhân sự | `TBD` — chờ **Q-28**, xem mục 6 | Engineer | BỔ SUNG | FR-24 |
| **6.0** | **Luồng Đơn xuất thẻ & Phê duyệt 2 cấp** | | | | |
| 6.1 | Tạo Đơn xuất thẻ: chọn loại thẻ, nhập số lượng, submit | Màn hình tạo đơn + API tạo đơn | Engineer | CORE | FR-01 |
| 6.2 | Màn hình soát xét của NV Kho + hiển thị tồn kho khả dụng theo kho/loại thẻ | Màn hình soát xét + API tồn kho khả dụng | Engineer | CORE | FR-02 |
| 6.3 | Điều chỉnh *Số lượng duyệt* kèm **lý do bắt buộc** (thực thi BR-02) | Form điều chỉnh + validation bắt buộc lý do | Engineer | CORE | FR-04 |
| 6.4 | Gán kho xuất hàng từ Danh mục kho (thực thi BR-09) | Chức năng gán kho xuất trên màn hình soát xét | Engineer | CORE | FR-05 |
| 6.5 | State machine engine + Phê duyệt cấp 1 (Kho) và cấp 2 (Admin) (thực thi BR-01) | Engine chuyển trạng thái 5 trạng thái + 2 màn hình duyệt | Engineer | CORE | FR-06, FR-07 |
| 6.6 | Cảnh báo mềm đơn trùng lặp + nút "Từ chối nhanh" cho NV Kho | Cơ chế cảnh báo trùng lặp + nút từ chối nhanh | Engineer | BỔ SUNG | FR-03 |
| **7.0** | **Vận chuyển & Tracking** | | | | |
| 7.1 | Adapter **thủ công**: NV Kho nhập tay mã vận đơn và cập nhật trạng thái hành trình | Module nhập tay vận đơn + đổi trạng thái sang `In Transit` | Engineer | BỔ SUNG | FR-08 |
| 7.2 | Tích hợp API carrier (tạo đơn + polling định kỳ theo giả định Q-03) | Adapter carrier thật + job polling + xử lý lỗi | Engineer | BỔ SUNG | FR-08, FR-09 |
| 7.3 | Hiển thị thông tin vận chuyển dạng timeline (bảng lịch sử tracking riêng) | Màn hình timeline hành trình trong chi tiết đơn | Engineer | BỔ SUNG | FR-10 |
| **8.0** | **Nhận hàng & Chứng từ giao nhận** | | | | |
| 8.1 | Upload ảnh POD (tối thiểu 01 ảnh, thực thi BR-03): chụp trực tiếp từ camera, nén ảnh, hiển thị tiến trình, retry khi mạng yếu | Luồng upload POD chạy được trên mobile web | Engineer | CORE | FR-11 |
| 8.2 | Check-list đối soát dải Series trên màn hình nhỏ + xác nhận một chạm (thực thi BR-04) | Màn hình đối soát Series mobile + điều kiện đóng đơn | Engineer | CORE | FR-12 |
| 8.3 | Xuất **Biên bản Bàn giao Thẻ** tự động dạng PDF và Excel (thực thi BR-05) | Chức năng sinh biên bản + 2 mẫu file | Engineer | BỔ SUNG | FR-13 |
| **9.0** | **Truy vết & Quản lý thất thoát** | | | | |
| 9.1 | Mô hình thực thể **Thẻ / Dải Series** và liên kết đơn ↔ thẻ (nền tảng của truy vết) | Bảng dữ liệu Thẻ/Series + logic liên kết với đơn | Engineer | CORE | FR-14 |
| 9.2 | Màn hình truy xuất nguồn gốc: tra 1 mã thẻ ra kho xuất, NV kho, Sale/Đại lý nhận, ngày giờ xuất, ngày giờ nhận | Màn hình truy vết trả đủ 4 câu hỏi của SRS III.4 | Engineer | CORE | FR-14 |
| 9.3 | Ghi nhận thẻ báo mất / hỏng | Chức năng đánh dấu thẻ mất/hỏng | Engineer | BỔ SUNG | FR-15 |
| 9.4 | Ghi nhận đền bù thẻ mất: số tiền, mã giao dịch, ảnh hóa đơn, Admin xác nhận | Module ghi nhận đền bù thủ công | Engineer | BỔ SUNG | FR-16 |
| 9.5 | Tự động cập nhật trạng thái thẻ `Báo mất - Đã đền bù` (thực thi BR-08) | Trigger đổi trạng thái thẻ sau khi đền bù xong | Engineer | BỔ SUNG | FR-17 |
| **10.0** | **Tra cứu, Bộ lọc & Báo cáo** | | | | |
| 10.1 | Màn hình theo dõi trạng thái đơn phía Sale/Đại lý | Danh sách đơn của chính mình + chi tiết trạng thái | Engineer | CORE | FR-22 |
| 10.2 | Global Search theo Mã thẻ / Dải Series / Tên nhân viên | Thanh tìm kiếm toàn cục + index tìm kiếm | Engineer | BỔ SUNG | FR-20 |
| 10.3 | Bộ lọc nâng cao đa điều kiện: khoảng thời gian, trạng thái, kho xuất, đại lý | Bộ lọc trên các màn hình danh sách | Engineer | BỔ SUNG | FR-21 |
| 10.4 | Tra cứu thẻ phía Sale/Đại lý, giới hạn theo phạm vi dữ liệu (data-scope) | Màn hình tra cứu thẻ cho vai trò Sale/Đại lý | Engineer | BỔ SUNG | FR-23 |
| 10.5 | Báo cáo tổng hợp & giám sát luồng dữ liệu | `TBD` — chờ **Q-28**, xem mục 6 | Engineer | BỔ SUNG | FR-25 |
| **11.0** | **Xác thực, Phân quyền & Audit Log** | | | | |
| 11.1 | Xác thực JWT (access token + refresh token), đăng nhập/đăng xuất/đổi mật khẩu | Module authentication + API token | Engineer | CORE | NFR-01 |
| 11.2 | RBAC 3 vai trò + lớp data-scope (Sale xem đơn của mình, NV Kho theo kho phụ trách) | Ma trận phân quyền đã hiện thực + middleware data-scope | Engineer | CORE | NFR-02 |
| 11.3 | Audit Log: ghi ai tạo, ai sửa số lượng, ai duyệt, kèm timestamp (thực thi BR-06) | Bảng Audit Log + cơ chế ghi tự động ở mọi mutation | Engineer | CORE | NFR-04 |
| 11.4 | Validation nghiệp vụ: chặn số lượng âm, **gán dải Series ở Bước 2** và chặn dải Series trùng (thực thi BR-07) | Bộ validation + unit test cho từng rule | Engineer | CORE | NFR-05 |
| 11.5 | Màn hình tra soát Audit Log cho Admin (xem, lọc, xuất) | Màn hình Audit Log | Engineer | BỔ SUNG | — |
| **12.0** | **QA & Kiểm thử** | | | | |
| 12.1 | Master Test Plan + viết test case cho toàn bộ tầng CORE | `MTP-VCDMS.md` + bộ `TC-*` cho 12 FR và 5 NFR mức P0 | QA | CORE | FR-01, FR-02, FR-04, FR-05, FR-06, FR-07, FR-11, FR-12, FR-14, FR-18, FR-19, FR-22, NFR-01, NFR-02, NFR-03, NFR-04, NFR-05 |
| 12.2 | Thực thi test + regression cho luồng CORE (bao gồm kiểm thử luồng nhận hàng **trên thiết bị di động thật**: ánh sáng ngoài trời, mạng yếu), quản lý bug đến khi đóng | Báo cáo thực thi test + báo cáo kiểm thử thiết bị thật + bug list đã đóng | QA | CORE | FR-01, FR-02, FR-04, FR-05, FR-06, FR-07, FR-11, FR-12, FR-14, FR-18, FR-19, FR-22 |
| 12.3 | UAT với khách hàng cho luồng CORE (5 bước end-to-end) | Biên bản UAT có xác nhận của khách hàng | QA | CORE | FR-01, FR-06, FR-07, FR-11, FR-12, FR-14 |
| 12.4 | Performance test chỉ tiêu **tra cứu ≤ 2 giây** | `Perf-Tra-Cuu-Ma-The.md` + kết quả đo | QA | BỔ SUNG | NFR-06 |
| 12.5 | Viết và thực thi test case cho tầng BỔ SUNG | Bộ `TC-*` cho tầng BỔ SUNG + báo cáo thực thi | QA | BỔ SUNG | FR-03, FR-08, FR-09, FR-10, FR-13, FR-15, FR-16, FR-17, FR-20, FR-21, FR-23 |
| **13.0** | **Triển khai & Go-live** | | | | |
| 13.1 | Dựng môi trường production và deploy bản CORE | Hệ thống chạy trên production + runbook deploy | DevOps | CORE | — |
| 13.2 | Migration: import Excel một lần cho danh mục kho, danh sách user, tồn kho khởi tạo | Script/chức năng import + dữ liệu đã nạp và đối soát | Engineer | CORE | — |
| 13.3 | Tài liệu hướng dẫn sử dụng + đào tạo 3 nhóm người dùng | Hướng dẫn sử dụng + biên bản đào tạo | PM | CORE | — |
| 13.4 | Tự động sao lưu dữ liệu **hàng ngày** + diễn tập phục hồi | Job backup hàng ngày + báo cáo diễn tập restore | DevOps | BỔ SUNG | NFR-07 |
| **14.0** | **Quản trị dự án** | | | | |
| 14.1 | Điều phối sprint, daily standup, báo cáo tiến độ hàng ngày cho tầng CORE | Sprint board + báo cáo tiến độ D1…D10 | PM | CORE | — |
| 14.2 | Quản lý thay đổi khi các câu `Q-NN` có câu trả lời khác giả định đang áp dụng | Change log + đánh giá tác động effort cho từng thay đổi | PM | CORE | — |
| 14.3 | Quản trị dự án cho tầng BỔ SUNG | Sprint board + báo cáo tiến độ W+1…W+6 | PM | BỔ SUNG | — |

---

## 2. Estimation (ETA) — Tầng CORE

> 📌 **Cách đọc bảng này**: cột `Start`/`End` thể hiện **thứ tự thực thi và quan hệ phụ thuộc** nếu ràng buộc 10 ngày được giữ nguyên. Bảng này **không chứng minh** 72,5 MD vừa khít 10 ngày — phép đối chiếu năng lực nằm ở [mục 5](#5-️-phân-tích-khoảng-cách-gap-analysis).

| Task ID | Description | Effort (MD) | Start | End | Status |
| :--- | :--- | :---: | :---: | :---: | :--- |
| 1.1 | Workshop chốt 11 câu Blocker | 2 | D1 | D2 | Chưa bắt đầu |
| 1.2 | Chốt 8 nhánh state machine T-a…T-h | 1.5 | D2 | D3 | Chưa bắt đầu |
| 1.3 | Cập nhật PRD/BRD theo câu trả lời | 1 | D3 | D3 | Chưa bắt đầu |
| 2.1 | Kiến trúc tổng thể + tech stack (SDD) | 2 | D2 | D3 | Chưa bắt đầu |
| 2.2 | DB schema: Đơn, Thẻ/Series, Kho, User, Audit Log | 2 | D3 | D4 | Chưa bắt đầu |
| 2.3 | API spec cho luồng CORE | 1.5 | D4 | D5 | Chưa bắt đầu |
| 2.4 | ADR state machine mở rộng + data-scope | 1 | D4 | D4 | Chưa bắt đầu |
| 3.1 | User flow + wireframe desktop | 2 | D1 | D2 | Chưa bắt đầu |
| 3.2 | Wireframe mobile Bước 5 | 1.5 | D3 | D4 | Chưa bắt đầu |
| 3.3 | Design system cơ bản | 2 | D2 | D3 | Chưa bắt đầu |
| 4.1 | Project setup FE + BE | 1.5 | D1 | D2 | Chưa bắt đầu |
| 4.2 | CI/CD + môi trường dev/staging | 2 | D2 | D3 | Chưa bắt đầu |
| 4.3 | HTTPS/TLS + mã hóa dữ liệu nhạy cảm | 1.5 | D3 | D4 | Chưa bắt đầu |
| 4.4 | Object storage cho ảnh POD | 1 | D4 | D4 | Chưa bắt đầu |
| 5.1 | CRUD Danh mục kho | 2 | D4 | D5 | Chưa bắt đầu |
| 5.2 | Thông tin chi tiết kho | 1 | D5 | D5 | Chưa bắt đầu |
| 6.1 | Tạo Đơn xuất thẻ | 2 | D5 | D6 | Chưa bắt đầu |
| 6.2 | Màn hình soát xét + tồn kho khả dụng | 2.5 | D6 | D7 | Chưa bắt đầu |
| 6.3 | Điều chỉnh SL duyệt + lý do bắt buộc | 1 | D6 | D6 | Chưa bắt đầu |
| 6.4 | Gán kho xuất hàng | 1 | D6 | D6 | Chưa bắt đầu |
| 6.5 | State machine engine + duyệt 2 cấp | 3 | D6 | D8 | Chưa bắt đầu |
| 8.1 | Upload ảnh POD trên mobile web | 3 | D6 | D8 | Chưa bắt đầu |
| 8.2 | Đối soát dải Series trên mobile | 2 | D7 | D8 | Chưa bắt đầu |
| 9.1 | Mô hình thực thể Thẻ / Dải Series | 2.5 | D5 | D6 | Chưa bắt đầu |
| 9.2 | Màn hình truy xuất nguồn gốc thẻ | 2 | D7 | D8 | Chưa bắt đầu |
| 10.1 | Theo dõi trạng thái đơn phía Sale | 1.5 | D7 | D7 | Chưa bắt đầu |
| 11.1 | Xác thực JWT | 2 | D4 | D5 | Chưa bắt đầu |
| 11.2 | RBAC 3 vai trò + data-scope | 2.5 | D5 | D6 | Chưa bắt đầu |
| 11.3 | Audit Log toàn bộ mutation | 2 | D7 | D8 | Chưa bắt đầu |
| 11.4 | Validation: SL âm, gán và chặn trùng dải Series | 2 | D7 | D8 | Chưa bắt đầu |
| 12.1 | Master Test Plan + test case tầng CORE | 3 | D5 | D7 | Chưa bắt đầu |
| 12.2 | Thực thi test + regression + kiểm thử thiết bị di động thật + đóng bug | 4 | D8 | D9 | Chưa bắt đầu |
| 12.3 | UAT với khách hàng | 2 | D9 | D10 | Chưa bắt đầu |
| 13.1 | Dựng production + deploy bản CORE | 1.5 | D9 | D9 | Chưa bắt đầu |
| 13.2 | Migration import Excel (kho, user, tồn kho) | 2 | D9 | D10 | Chưa bắt đầu |
| 13.3 | Hướng dẫn sử dụng + đào tạo người dùng | 1 | D10 | D10 | Chưa bắt đầu |
| 14.1 | Điều phối sprint + báo cáo tiến độ | 3 | D1 | D10 | Chưa bắt đầu |
| 14.2 | Quản lý thay đổi khi có câu trả lời `Q-NN` | 1.5 | D3 | D10 | Chưa bắt đầu |
| | **TỔNG TẦNG CORE** | **72.5** | **D1** | **D10** | |

> ⚠️ **Đỉnh tải rơi vào D6–D8**: riêng cửa sổ 3 ngày này chứa khoảng 26 MD (6.2, 6.3, 6.4, 6.5, 8.1, 8.2, 9.2, 10.1, 11.3, 11.4 và phần cuối của 6.1, 9.1, 12.1) → cần **≈ 9 người làm song song** trong 3 ngày đó. Đây là con số cần đối chiếu với mục 0.5 (đội suy luận 1–2 người).

---

## 3. Estimation (ETA) — Tầng BỔ SUNG

> 📌 Mốc `W+N` = tuần thứ N **sau khi tầng CORE go-live**. Thứ tự ưu tiên: hết `P1` rồi mới tới `P2`. **FR-24 và FR-25 không xuất hiện trong bảng này** — chúng bị cấm ước lượng, xem [mục 6](#6-hạng-mục-không-được-ước-lượng).

| Task ID | Description | Effort (MD) | Start | End | Status |
| :--- | :--- | :---: | :---: | :---: | :--- |
| 1.4 | Chốt câu hỏi của tầng BỔ SUNG (Q-02, Q-03, Q-19, Q-28) | 1 | W+1 | W+1 | Chưa bắt đầu |
| 2.5 | ADR + đặc tả tích hợp carrier (adapter/plugin) | 1.5 | W+1 | W+1 | Chưa bắt đầu |
| 3.4 | Wireframe tracking, bộ lọc, tra cứu | 2 | W+1 | W+1 | Chưa bắt đầu |
| 7.1 | Adapter thủ công: nhập tay mã vận đơn | 2 | W+1 | W+1 | Chưa bắt đầu |
| 6.6 | Cảnh báo đơn trùng lặp + từ chối nhanh | 1.5 | W+2 | W+2 | Chưa bắt đầu |
| 7.2 | Tích hợp API carrier + polling định kỳ | 3 | W+2 | W+2 | Chưa bắt đầu |
| 7.3 | Timeline hiển thị thông tin vận chuyển | 2 | W+2 | W+2 | Chưa bắt đầu |
| 8.3 | Biên bản Bàn giao Thẻ (PDF + Excel) | 2.5 | W+3 | W+3 | Chưa bắt đầu |
| 9.3 | Ghi nhận thẻ báo mất / hỏng | 1.5 | W+3 | W+3 | Chưa bắt đầu |
| 9.4 | Ghi nhận đền bù thẻ mất *(P2)* | 2 | W+3 | W+3 | Chưa bắt đầu |
| 9.5 | Tự động cập nhật `Báo mất - Đã đền bù` *(P2)* | 0.5 | W+3 | W+3 | Chưa bắt đầu |
| 10.2 | Global Search | 2 | W+4 | W+4 | Chưa bắt đầu |
| 10.3 | Bộ lọc nâng cao đa điều kiện | 2 | W+4 | W+4 | Chưa bắt đầu |
| 10.4 | Tra cứu thẻ phía Sale + data-scope | 1.5 | W+4 | W+4 | Chưa bắt đầu |
| 5.3 | CRUD Danh mục Loại thẻ *(giả định Q-27)* | 1.5 | W+4 | W+4 | Chưa bắt đầu |
| 5.4 | CRUD Danh mục Đại lý *(giả định Q-31)* | 1.5 | W+5 | W+5 | Chưa bắt đầu |
| 11.5 | Màn hình tra soát Audit Log cho Admin | 1.5 | W+5 | W+5 | Chưa bắt đầu |
| 4.5 | Monitoring / alerting cơ bản | 1.5 | W+5 | W+5 | Chưa bắt đầu |
| 12.4 | Performance test tra cứu ≤ 2 giây | 2 | W+5 | W+5 | Chưa bắt đầu |
| 12.5 | Test case + thực thi test tầng BỔ SUNG | 3 | W+6 | W+6 | Chưa bắt đầu |
| 13.4 | Backup hàng ngày + diễn tập phục hồi | 1.5 | W+6 | W+6 | Chưa bắt đầu |
| 14.3 | Quản trị dự án tầng BỔ SUNG | 2 | W+6 | W+6 | Chưa bắt đầu |
| | **TỔNG TẦNG BỔ SUNG** | **39.5** | **W+1** | **W+6** | |

---

## 4. Tổng hợp effort theo nhóm công việc

| Nhóm | Tên nhóm | MD CORE | MD BỔ SUNG |
| :--- | :--- | :---: | :---: |
| 1.0 | Discovery & Chốt yêu cầu | 4.5 | 1 |
| 2.0 | Kiến trúc & Thiết kế hệ thống | 6.5 | 1.5 |
| 3.0 | Thiết kế UI/UX | 5.5 | 2 |
| 4.0 | Nền tảng & Hạ tầng | 6 | 1.5 |
| 5.0 | Danh mục & Master data | 3 | 3 |
| 6.0 | Luồng Đơn xuất thẻ & Phê duyệt 2 cấp | 9.5 | 1.5 |
| 7.0 | Vận chuyển & Tracking | 0 | 7 |
| 8.0 | Nhận hàng & Chứng từ giao nhận | 5 | 2.5 |
| 9.0 | Truy vết & Quản lý thất thoát | 4.5 | 4 |
| 10.0 | Tra cứu, Bộ lọc & Báo cáo | 1.5 | 5.5 |
| 11.0 | Xác thực, Phân quyền & Audit Log | 8.5 | 1.5 |
| 12.0 | QA & Kiểm thử | 9 | 5 |
| 13.0 | Triển khai & Go-live | 4.5 | 1.5 |
| 14.0 | Quản trị dự án | 4.5 | 2 |
| | **TỔNG CỘNG** | **72.5** | **39.5** |

### 4.1. Hạng mục `TBD` — tách riêng, KHÔNG cộng vào tổng

| Task ID | Nhóm | Hạng mục | Effort (MD) |
| :--- | :--- | :--- | :---: |
| 5.5 | 5.0 | FR-24 — Quản lý danh mục nhân sự | `TBD` |
| 10.5 | 10.0 | FR-25 — Báo cáo tổng hợp & giám sát luồng dữ liệu | `TBD` |

> Hai hạng mục trên **bị cấm ước lượng** cho tới khi **Q-28** có câu trả lời. Xem [mục 6](#6-hạng-mục-không-được-ước-lượng). Vì vậy **tổng 72,5 MD và 39,5 MD chưa bao gồm FR-24 và FR-25** — đây là phần **chắc chắn sẽ tăng thêm**, chưa biết bao nhiêu.

---

## 5. ⚠️ Phân tích khoảng cách (Gap Analysis)

### 5.1. Khối 1 — Đội cần

| Hạng mục | Giá trị |
| :--- | :--- |
| **Tổng MD bottom-up tầng CORE** (theo mục 4) | **72,5 MD** |
| Tổng MD tầng BỔ SUNG | 39,5 MD |
| Tổng cả hai tầng | 112 MD |
| Chưa tính | FR-24, FR-25 (`TBD`) — sẽ làm tổng tăng thêm |

Trong 72,5 MD của tầng CORE, phần **không phải code** chiếm tỉ trọng đáng kể: Discovery 4,5 + Kiến trúc 6,5 + UI/UX 5,5 + QA 9 + Quản trị dự án 4,5 = **30 MD (≈ 41%)**. Đây không phải phần "phụ có thể bỏ" — 31 giả định đang mở (mục 8) khiến Discovery trở thành hạng mục **giảm rủi ro lớn nhất** của cả dự án.

### 5.2. Khối 2 — Anh có

| Hạng mục | Giá trị | Nguồn |
| :--- | :--- | :--- |
| Thời gian | **10 ngày** | Ràng buộc do khách hàng cấp tại gate 2026-08-20 |
| Ngân sách | **~10.000.000 VND** | Ràng buộc do khách hàng cấp tại gate 2026-08-20 |
| Quy mô đội | **1–2 người** — **[SUY LUẬN]** từ `10.000.000 ÷ 10 = 1.000.000 VND/ngày` cho toàn đội (mục 0.5) | Suy luận, **cần xác nhận E-01** |

### 5.3. Khối 3 — Khoảng cách

**a) Khoảng cách về thời gian**

| Giả thiết quy mô đội | Năng lực trong 10 ngày | Cần cho 72,5 MD | Khoảng cách |
| :--- | :---: | :---: | :--- |
| 1 người | 10 MD | 72,5 MD | **Thiếu 62,5 MD** → cần **72,5 ngày làm việc** (≈ 14,5 tuần), tức **vượt 62,5 ngày** so với ràng buộc |
| 2 người | 20 MD | 72,5 MD | **Thiếu 52,5 MD** → cần **≈ 36 ngày làm việc** (≈ 7 tuần) |
| 4 người | 40 MD | 72,5 MD | **Thiếu 32,5 MD** → cần **≈ 18 ngày làm việc** |
| **7,25 người** | 72,5 MD | 72,5 MD | Vừa khít **trên giấy**, nhưng xem cảnh báo bên dưới |

> 🔴 **Kết luận thẳng: tổng MD tầng CORE VƯỢT ràng buộc 10 ngày.** Vượt **62,5 MD** nếu đội 1 người, **52,5 MD** nếu đội 2 người. Con số 72,5 MD là ước lượng bottom-up và **không bị điều chỉnh** để khớp ràng buộc.
>
> ⚠️ **Ngay cả 7,25 người cũng không giải được**, vì hai lý do: (1) đường găng có **phụ thuộc tuần tự bắt buộc** — Discovery → DB schema → code → QA → go-live, không nén được bằng cách thêm người (mục 7); (2) đỉnh tải D6–D8 cần **≈ 9 người song song** trong 3 ngày rồi tụt xuống — mô hình nhân sự này không tồn tại trong thực tế.

**b) Khoảng cách về ngân sách — quy đổi đơn giá**

Phép chia trực tiếp:

`10.000.000 VND ÷ 72,5 MD ≈ **138.000 VND/MD**`

Đây là **đơn giá ngày mà nguồn lực thực hiện phải đạt** để 10.000.000 VND phủ hết tầng CORE.

Bảng độ nhạy — **[SUY LUẬN]**, các mức đơn giá dưới đây là **tham số để anh chọn**, không phải số liệu thị trường mà em khẳng định:

| Đơn giá giả định (VND/MD) | Ngân sách 10.000.000 VND phủ được | So với 72,5 MD |
| :---: | :---: | :--- |
| 138.000 | 72,5 MD | Vừa đủ — nhưng cần xác nhận có nguồn lực nào ở mức này |
| 300.000 | ≈ 33 MD | Thiếu ≈ 39,5 MD (phủ **46%**) |
| 500.000 | 20 MD | Thiếu 52,5 MD (phủ **28%**) |
| 1.000.000 | 10 MD | Thiếu 62,5 MD (phủ **14%**) |
| 2.000.000 | 5 MD | Thiếu 67,5 MD (phủ **7%**) |

**Đối chiếu với thực tế nhân sự**: ngân sách 10.000.000 VND ÷ 10 ngày = **1.000.000 VND/ngày cho toàn đội**. Nếu đơn giá thực tế của một người là 1.000.000 VND/MD thì ngân sách chỉ tài trợ được **đúng 1 người trong 10 ngày = 10 MD** — trong khi đỉnh tải D6–D8 cần ≈ 9 người. Đây là **mâu thuẫn cốt lõi** giữa mục 0.5 (đội suy luận 1–2 người) và mục 2 (lịch D1–D10 đòi ≈ 7,25 người trung bình).

> 📌 **Điểm cần anh xác nhận (E-02)**: nếu 10.000.000 VND là **chi phí công cụ/hạ tầng** (AI agent, hosting, domain, object storage) chứ **không phải chi phí nhân công** — ví dụ nhân công do chính anh đảm nhiệm — thì **toàn bộ phép quy đổi VND/MD ở mục 5.3.b không áp dụng**, và bài toán còn lại chỉ là khoảng cách thời gian ở mục 5.3.a. Em **không xây thêm con số nào** trên giả thiết này cho tới khi anh xác nhận.

**c) Khoảng cách về phạm vi chưa tính được**

FR-24 và FR-25 (`TBD`) chưa nằm trong 72,5 MD. Khi **Q-28** có câu trả lời, tổng **chỉ có thể tăng**, không thể giảm.

### 5.4. Khối 4 — Phương án nếu có khoảng cách

Có khoảng cách, nên bắt buộc phải chọn. Bốn phương án dưới đây tương ứng 4 trục cân nhắc.

---

#### 🅐 Phương án A — Cắt tiếp trong nội bộ `P0` ("MVP tối giản 10 ngày") · **⭐ Em đề xuất**

| | |
| :--- | :--- |
| **Cắt gì** | Cắt **4 hạng mục P0** khỏi 10 ngày đầu, đẩy sang ngay sau go-live: **FR-02** (kiểm tra tồn kho — tạm thay bằng NV Kho tự đối chiếu Excel ngoài hệ thống), **FR-14** (truy xuất nguồn gốc thẻ), **NFR-05** (gán + chặn trùng dải Series — tạm chỉ chặn số lượng âm), **NFR-04** (Audit Log đầy đủ — tạm chỉ log 3 mốc: tạo đơn, sửa số lượng, duyệt). Đồng thời cắt mỏng: Design system chỉ dùng component library mặc định, QA chỉ test luồng chính. Giữ nguyên: FR-01, FR-04, FR-05, FR-06, FR-07, FR-11, FR-12, FR-18, FR-19, FR-22, NFR-01, NFR-02, NFR-03 và **toàn bộ nhóm 1.0 Discovery**. |
| **Được gì** | Ước lượng nhanh còn **≈ 32–35 MD** (giảm ≈ 38 MD): khả thi trong 10 ngày với đội **4 người**, hoặc ≈ 8 tuần với 1 người. Có hệ thống **thật sự chạy được**: Sale tạo đơn → Kho soát xét & điều chỉnh có lý do → Admin duyệt → Sale nhận hàng chụp ảnh POD + đối soát Series → đơn đóng. Đúng nghĩa *"chức năng chính để có thể hoạt động"*. |
| **Mất gì** | **Mất mục tiêu G-02 (truy vết)** trong 10 ngày đầu — mà theo BRD mục 2.2, P-02 *"thiếu khả năng truy vết"* là một trong bốn lý do dự án ra đời. Mất khả năng chặn trùng dải Series → **rủi ro dữ liệu sai ngay từ ngày đầu**, sửa sau phải kèm migration dữ liệu thật. Audit Log không đầy đủ → BR-06 chỉ được thực thi một phần, giảm giá trị kiểm toán. Không kiểm tra tồn kho trong hệ thống → NV Kho vẫn phải mở Excel, đúng cái rủi ro mà PRD Q-26 cảnh báo *"hệ thống mất giá trị"*. |

---

#### 🅑 Phương án B — Giãn thời gian, giữ nguyên phạm vi CORE

| | |
| :--- | :--- |
| **Cắt gì** | **Cắt ràng buộc 10 ngày.** Không cắt bất kỳ FR/NFR nào. Thay 10 ngày bằng mốc tương ứng quy mô đội: 1 người → **72,5 ngày làm việc**; 2 người → **≈ 36 ngày**; 4 người → **≈ 18 ngày**. |
| **Được gì** | Giữ trọn **12 FR + 5 NFR mức P0**, bao gồm truy vết (FR-14) và chặn trùng Series (NFR-05) — tức **không sinh nợ kỹ thuật kèm migration** về sau. Chất lượng Increment không bị bóp. Đường găng (mục 7) được tôn trọng: Q-01 chốt xong mới thiết kế tồn kho. |
| **Mất gì** | **Go-live muộn** so với kỳ vọng của anh — trễ 62,5 ngày (đội 1 người) hoặc 26 ngày (đội 2 người). Giãn thời gian **không giải quyết vấn đề ngân sách**: 72,5 MD vẫn là 72,5 MD, chi phí không đổi khi trải dài hơn. Rủi ro mất động lượng dự án và thay đổi yêu cầu trong thời gian dài hơn. |

---

#### 🅒 Phương án C — Tăng nhân sự, giữ nguyên 10 ngày và phạm vi CORE

| | |
| :--- | :--- |
| **Cắt gì** | **Cắt ràng buộc ngân sách ~10.000.000 VND.** Không cắt phạm vi, không cắt thời gian. Bổ sung nhân sự lên **≈ 7–8 người**, riêng cửa sổ D6–D8 cần **≈ 9 người** song song. |
| **Được gì** | Về lý thuyết là phương án duy nhất giữ được **cả 10 ngày lẫn trọn phạm vi CORE**. |
| **Mất gì** | **Ngân sách vỡ nặng**: ở đơn giá 500.000 VND/MD, 72,5 MD ≈ **36.250.000 VND** — gấp **3,6 lần** ngân sách; ở 1.000.000 VND/MD ≈ **72.500.000 VND** — gấp **7,25 lần**. Thêm vào đó, effort **không scale tuyến tính**: đường găng tuần tự (mục 7) không nén được bằng cách thêm người, chi phí onboarding và giao tiếp làm tổng MD **tăng** chứ không giảm, và mô hình "9 người trong 3 ngày rồi giải tán" không khả thi về tổ chức. **Em không khuyến nghị phương án này.** |

---

#### 🅓 Phương án D — Đổi phương án kỹ thuật cho các hạng mục nặng

| | |
| :--- | :--- |
| **Cắt gì** | Cắt phần **tự xây** của các hạng mục nặng, thay bằng nền tảng/thư viện sẵn có: (1) nhóm 11.1 JWT auth → dùng dịch vụ authentication sẵn có thay vì tự viết; (2) nhóm 3.3 Design system → dùng component library mặc định, bỏ thiết kế token riêng; (3) nhóm 5.1/5.2 CRUD danh mục → dùng admin scaffold/generator; (4) nhóm 11.3 Audit Log → dùng trigger/CDC ở tầng database thay vì tự viết middleware; (5) nhóm 4.x hạ tầng → dùng PaaS thay vì tự dựng. |
| **Được gì** | Ước lượng nhanh cắt được **≈ 12–16 MD** (chủ yếu ở nhóm 3.0, 4.0, 5.0, 11.0), đưa CORE về **≈ 57–61 MD** mà **không bỏ FR/NFR nào**. Kết hợp được với Phương án A hoặc B để cộng dồn hiệu quả. |
| **Mất gì** | **Phụ thuộc vendor (lock-in)** và **chi phí subscription hàng tháng** — chi phí này chuyển từ CAPEX sang OPEX, cần tính vào tổng chi phí sở hữu. Nguy hiểm nhất: component library mặc định **rất khó tùy biến cho UX mobile Bước 5** (chụp ảnh trực tiếp từ camera, đối soát Series dưới ánh sáng ngoài trời) — PRD mục 7.2 cảnh báo đúng rủi ro *"làm đúng đặc tả nhưng sai thực tế"*, dẫn tới **FR-11 mức P0 không dùng được trên hiện trường**. Ngoài ra object storage/PaaS nước ngoài có thể vi phạm giả định Q-13 (dữ liệu đặt tại Việt Nam). |

---

#### 🅔 Phương án E *(dự phòng)* — Đổi mục tiêu của 10 ngày thành "Giai đoạn 0"

| | |
| :--- | :--- |
| **Cắt gì** | **Cắt mục tiêu go-live khỏi 10 ngày.** Dùng 10 ngày cho nhóm 1.0 + 2.0 + 3.1 + 3.2 + 4.1 (4,5 + 6,5 + 2 + 1,5 + 1,5 = **16 MD**): chốt 11 câu Blocker, chốt 8 nhánh state machine, ra SDD + DB schema + API spec, wireframe hai luồng quan trọng nhất, dựng skeleton chạy được. |
| **Được gì** | Khả thi hơn hẳn: 16 MD ≈ **2 người trong 10 ngày** (năng lực 20 MD). Sau 10 ngày anh có **ước lượng đáng tin cậy hơn nhiều** cho phần còn lại (vì 11 Blocker đã đóng), và **triệt tiêu rủi ro lớn nhất** của dự án — thiết kế mô hình dữ liệu trên 31 giả định chưa xác nhận (mục 8). |
| **Mất gì** | Sau 10 ngày **chưa có hệ thống chạy được** — không đáp ứng đúng chữ *"để có thể hoạt động"* trong yêu cầu của anh. Kỳ vọng phải được điều chỉnh ngay từ đầu, nếu không sẽ bị hiểu là dự án chậm tiến độ. Ngân sách 10.000.000 VND vẫn cần đối chiếu: `10.000.000 ÷ 16 MD = **625.000 VND/MD**`. |

---

## 6. Hạng mục KHÔNG được ước lượng

| Task ID | FR | Hạng mục | Effort (MD) | Chờ trả lời |
| :--- | :--- | :--- | :---: | :---: |
| 5.5 | **FR-24** | Quản lý danh mục nhân sự | `TBD` | **Q-28** |
| 10.5 | **FR-25** | Báo cáo tổng hợp & giám sát luồng dữ liệu | `TBD` | **Q-28** |

**Trích nguyên văn câu cấm của PRD mục 4:**

> 🔴 **Cảnh báo dành cho Architect và QA về FR-24 và FR-25**: hai yêu cầu này **không có đặc tả**. Không được thiết kế màn hình, không được viết test case, và **không được ước lượng công** cho tới khi **Q-28** có câu trả lời. Giả định tạm mà đội đang áp dụng (4 báo cáo cụ thể) nằm ở [mục 9](../../020-Requirements/PRD-VETC.md#9-giả-định-thiết-kế-design-assumptions) và **chỉ là giả định**.

**Hệ quả với bản ước lượng này:**

1. Hai hạng mục trên **không được cộng** vào 72,5 MD hay 39,5 MD. Chúng nằm riêng ở mục 4.1.
2. PRD mục 4 gọi FR-25 là *"cụm từ có thể nở ra vô hạn → nguồn scope creep điển hình"*, và BRD mục 9.2 xếp RK-03 (*phình phạm vi ở hạng mục "báo cáo tổng hợp"*) ở mức 🟡 Trung bình. Vì vậy khi **Q-28** có câu trả lời, **bắt buộc chốt danh sách báo cáo bằng văn bản** trước khi ước lượng lại.
3. Giả định tạm của đội (Q-28: 4 báo cáo + CRUD tài khoản cơ bản) **không được dùng làm căn cứ ước lượng** — dùng là vi phạm chính câu cấm ở trên.

---

## 7. Đường găng (Critical Path) và phụ thuộc

### 7.1. Khối phụ thuộc gốc — PRD mục 1 gọi đây là *"một khối"*

```
Q-01 (có luồng nhập kho không?)
  └─→ Q-26 (tồn kho lấy từ đâu?)
        └─→ Q-06 (ai gán dải Series, lúc nào?)
              └─→ NFR-05 (chặn dải Series trùng bằng cách nào?)
```

PRD mục 1 ghi nguyên văn: bốn vấn đề này là **một khối** — khách hàng trả lời `Q-01` khác đi thì **cả bốn phải thiết kế lại**, và *"không nên bắt đầu thiết kế mô hình dữ liệu tồn kho trước khi `Q-01` được chốt"*.

### 7.2. Đường găng của tầng CORE

| # | Mắt xích | Task ID | Vì sao nằm trên đường găng |
| :---: | :--- | :--- | :--- |
| 1 | Chốt `Q-01` → `Q-26` → `Q-06` | 1.1 | Chưa chốt thì không thiết kế được bảng Thẻ/Series và không hiện thực được FR-02 |
| 2 | Chốt 8 nhánh state machine T-a…T-h | 1.2 | Quyết định bảng trạng thái; chốt muộn → migration dữ liệu thật |
| 3 | DB schema (Đơn, Thẻ/Series, Kho, Audit Log) | 2.2 | Mọi task code đều đợi schema |
| 4 | Mô hình thực thể Thẻ / Dải Series | 9.1 | Nền tảng của FR-14 và NFR-05 |
| 5 | State machine engine + duyệt 2 cấp | 6.5 | Trục xương sống của cả luồng 5 bước |
| 6 | Validation gán + chặn trùng dải Series | 11.4 | Hệ quả trực tiếp của mắt xích 1 và 4 |
| 7 | Thực thi test + UAT | 12.2, 12.3 | Không nén được bằng thêm người |
| 8 | Deploy production + migration import Excel | 13.1, 13.2 | Mắt xích cuối trước go-live |

**Độ dài đường găng**: 2 + 1,5 + 2 + 2,5 + 3 + 2 + 6 + 3,5 = **22,5 MD tuần tự**.

### 7.3. Hệ quả lên thứ tự thực thi trong 10 ngày

> 🔴 **Đây là kết luận quan trọng nhất của mục 7**: dù có bao nhiêu người, chuỗi 22,5 MD trên **vẫn phải chạy tuần tự** → **cần tối thiểu ≈ 22–23 ngày làm việc**, trừ khi cắt bớt mắt xích.
>
> **10 ngày là bất khả thi về mặt cấu trúc phụ thuộc**, không chỉ về mặt tổng effort. Thêm người rút ngắn được phần song song (nhóm 3.0, 5.0, 8.0, 10.0, 11.1, 11.2), **không** rút ngắn được đường găng.

Bốn nguyên tắc thứ tự phải giữ nếu vẫn theo ràng buộc 10 ngày:

1. **D1–D3 phải dành cho Discovery.** Không được đổi chỗ với code để "tranh thủ". Bỏ 4,5 MD Discovery để lấy thêm 4,5 MD code là đổi rủi ro migration dữ liệu thật lấy 4,5 MD — cái giá đắt nhất trong toàn bảng.
2. **Không code tồn kho (6.2) và Thẻ/Series (9.1) trước khi `Q-01` chốt** — đúng khuyến nghị nguyên văn của PRD mục 1.
3. **Các nhóm song song được** đưa lên sớm: 3.0 (UI/UX), 4.0 (hạ tầng), 11.1 (JWT), 12.1 (test plan) — không phụ thuộc đường găng.
4. **QA không được nén.** 12.2 + 12.3 = 6 MD nằm cuối; nén QA để giữ D10 là đánh đổi trực tiếp với chất lượng Increment.

---

## 8. Rủi ro tiến độ

### 8.1. 🔴 Rủi ro lớn nhất — 31 câu `Q-NN` chưa có câu trả lời, mà Discovery lại nằm trong chính 10 ngày đó

BRD mục 9.1 và PRD mục 9 xác nhận: **31 điểm cần làm rõ**, trong đó **11 điểm mức 🔴 Blocker** — *"chưa có câu trả lời thì không thể bắt đầu thiết kế phần lõi của hệ thống"*.

Nghịch lý của bản ước lượng này:

| Vấn đề | Hệ quả |
| :--- | :--- |
| Nhóm 1.0 (Discovery, 4,5 MD) **nằm bên trong** 10 ngày, chiếm **D1–D3** | 30% thời lượng dự án dùng để **chốt yêu cầu**, không sinh ra chức năng nào |
| 11 Blocker **chưa có câu trả lời tại thời điểm lập bảng này** | Toàn bộ 72,5 MD được ước lượng **trên 31 giả định thiết kế** (PRD mục 9), không phải trên yêu cầu đã chốt |
| Câu trả lời của khách hàng **không do đội kiểm soát** | Nếu khách hàng cần 1 tuần để trả lời, **D1–D3 trượt hoàn toàn** và 10 ngày mất 30% ngay trước khi bắt đầu |

> 🔴 **Kết luận**: độ tin cậy của con số 72,5 MD **phụ thuộc trực tiếp vào việc 11 Blocker được trả lời trước D1**. Nếu chúng được trả lời **trước** D1, tầng CORE giảm còn ≈ 68 MD và rủi ro làm lại gần như bằng 0. Nếu chúng được trả lời **trong hoặc sau** 10 ngày, con số 72,5 MD là **sàn**, không phải trần.

### 8.2. Tác động của 11 Blocker lên ước lượng

| Mã | Nếu khách hàng trả lời khác giả định | Task bị ảnh hưởng | Tác động lên effort |
| :--- | :--- | :--- | :--- |
| **Q-01** | Có làm luồng nhập kho | 2.2, 6.2, 9.1, 11.4, 13.2 | 🔴 **Tác động lớn nhất toàn dự án.** Thêm thực thể phiếu nhập + luồng duyệt riêng + pool Series đầy đủ. Ước lượng thô **+15 đến +20 MD**, kèm migration nếu đã có dữ liệu thật |
| **Q-02** | Carrier chỉ có API tra cứu, không có API tạo đơn | 2.5, 7.1, 7.2 | FR-08 **bất khả thi như mô tả** → phải làm lại thiết kế tích hợp |
| **Q-03** | "Real-time" phải dưới 1 phút | 2.5, 7.2 | Bắt buộc webhook thay polling → đổi kiến trúc tích hợp, effort nhóm 7.0 tăng |
| **Q-04** | Cần thanh toán online cho đền bù | 9.4 | PRD ghi rõ *"khối lượng công có thể gấp 5–10 lần"* → 2 MD có thể thành 10–20 MD |
| **Q-05** | Tiêu chí trùng lặp khác (thêm địa chỉ giao, thêm đại lý) | 6.6 | Sửa quy tắc + toàn bộ test case liên quan |
| **Q-06** | Gán dải Series tay hoàn toàn, hoặc ở bước khác | 9.1, 11.4 | **NFR-05 không thực thi được**; đổi thời điểm khóa tồn kho → thiết kế lại 9.1 |
| **Q-09** | Cho sửa & gửi lại đơn bị từ chối trực tiếp | 1.2, 6.5, 11.3 | Thêm trạng thái `Draft`/`Resubmitted` + versioning đơn → ảnh hưởng Audit Log |
| **Q-10** | Đơn bị Admin từ chối phải quay lại NV Kho | 1.2, 6.5 | Thêm nhánh vòng lặp + cơ chế chống lặp vô tận vào state machine |
| **Q-11** | Kho phải **giao bù** phần thiếu thay vì đóng đơn | 1.2, 8.2, 9.3 | Cần cơ chế đơn con/đơn bù → **thay đổi mô hình dữ liệu đơn hàng** |
| **Q-12** | Có cấp quản lý trung gian (Trưởng vùng, Quản lý Sale) | 11.2, 10.1, 10.4 | Thêm mô hình cây tổ chức vào **mọi query và mọi API**. PRD ghi *"sửa sau rất tốn kém"* |
| **Q-21** | Phải tách ngay 2 vai trò Sale và Đại lý | 11.2, 5.4 | Làm lại ma trận phân quyền + migration user + có thể đổi mô hình chủ sở hữu đơn |

### 8.3. Rủi ro tiến độ khác

| # | Rủi ro | Mức | Ảnh hưởng ước lượng |
| :--- | :--- | :---: | :--- |
| RT-01 | **8 nhánh state machine T-a…T-h chưa định nghĩa** (PRD mục 6.2 gọi là *"rủi ro thiết kế lớn nhất"*). Task 6.5 đang được ước lượng cho **5 trạng thái luồng thuận**. | 🔴 Cao | Chốt thêm 4–5 trạng thái → 6.5 tăng từ 3 MD lên **≈ 5–6 MD**, kèm sửa 11.3 và toàn bộ test case |
| RT-02 | **Tầng CORE (`P0` thuần) không đóng được vòng đời đơn.** FR-08 (đẩy đơn sang carrier) là `P1`, nên trong CORE **không có đường nào** chuyển đơn từ `Ready for Shipping` sang `In Transit` để Sale nhận hàng ở Bước 5. | 🔴 Cao | Cần đưa task **7.1 (adapter thủ công, 2 MD)** vào CORE → **72,5 → 74,5 MD**. Đây là điểm **cần anh và PM xác nhận**, PO không tự chia lại tầng |
| RT-03 | **Backup (NFR-07) và perf test (NFR-06) nằm ở tầng BỔ SUNG** vì PRD xếp `P1`, nhưng dữ liệu thật đã chạy trên production từ D10. | 🟡 Trung bình | Go-live không có backup là rủi ro vận hành, không phải rủi ro tiến độ — nhưng nếu phải kéo 13.4 vào CORE thì **+1,5 MD** |
| RT-04 | **Danh mục Loại thẻ (Q-27) ở tầng BỔ SUNG** nhưng FR-01 (`P0`) yêu cầu *"chọn loại thẻ"*. CORE phải tạm dùng dữ liệu seed cứng. | 🟡 Trung bình | Nếu anh yêu cầu CRUD Loại thẻ ngay ở CORE thì **+1,5 MD**; nếu giữ seed cứng thì mỗi loại thẻ mới phải sửa code và deploy lại |
| RT-05 | **FR-11 mức `P0` có thể không dùng được thực tế** nếu chỉ tối ưu desktop (PRD mục 7.2). Task 8.1 đã tính chi phí mobile (3 MD); phần kiểm thử trên thiết bị di động thật nằm bên trong task 12.2. | 🟡 Trung bình | Nếu nén 12.2 và bỏ kiểm thử thiết bị thật → **rủi ro làm đúng đặc tả nhưng sai thực tế**, phải làm lại sau go-live. Nếu tách thành task QA riêng thì **+1 MD** |
| RT-06 | **Không có tiêu chí nghiệm thu định lượng** (BRD RK-02, chờ **Q-29**). | 🔴 Cao | Không ảnh hưởng số MD, nhưng **không có căn cứ để tuyên bố Increment "Done"** → task 12.3 (UAT) có thể kéo dài vô định |
| RT-07 | **18 mâu thuẫn nội tại trong SRS** (PRD mục 10), 8 mức 🔴, **chưa được sửa** vì SRS thuộc quyền khách hàng. | 🟡 Trung bình | Mỗi mâu thuẫn 🔴 được giải theo hướng khác giả định đều làm ước lượng lệch — xem bảng 8.2 |
| RT-08 | **FR-24, FR-25 chưa ước lượng được** (mục 6). | 🟡 Trung bình | Tổng 72,5 / 39,5 MD **chỉ có thể tăng** khi **Q-28** có câu trả lời |
| RT-09 | **13 hạng mục NFR còn thiếu hoàn toàn** (PRD mục 5.2: uptime SLA, concurrent users, throughput, DR, rate limiting…). | 🟡 Trung bình | Không hạng mục nào trong 72,5 MD tính chi phí cho 13 hạng mục này |

---

## 9. Tài liệu liên quan

| Tài liệu | Quan hệ | Mô tả |
| :--- | :--- | :--- |
| [PRD-VETC](../../020-Requirements/PRD-VETC.md) | **Nguồn phạm vi** | 25 FR + 7 NFR, cột Ưu tiên `P0/P1/P2` là căn cứ chia hai tầng CORE / BỔ SUNG; mục 9 là 31 giả định thiết kế chi phối độ tin cậy của ước lượng. |
| [BRD-001 — Hệ Thống Xuất Kho & Phân Phối Thẻ VETC](../../020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md) | **Bối cảnh nghiệp vụ** | Phạm vi In/Out/Undetermined, 10 quy tắc nghiệp vụ BR-01…BR-10, rủi ro nghiệp vụ và tiêu chí thành công. |
| [SRS-VETC](../../020-Requirements/SRS-VETC.md) | **Nguồn sự thật gốc** | Tài liệu của khách hàng — nguồn duy nhất của 2 con số ≤ 2 giây và sao lưu hàng ngày. |
| [Analysis-Open-Questions-VETC](../../050-Research/Analysis-Open-Questions-VETC.md) | **Câu hỏi mở** | 31 điểm cần khách hàng làm rõ — nguồn của toàn bộ mã `Q-NN`; đầu vào bắt buộc của nhóm 1.0. |
| [Template-WBS-ETA](../../999-Resources/Templates/Template-WBS-ETA.md) | **Template gốc** | Cấu trúc bảng WBS và ETA mà tài liệu này mở rộng. |
| [RULE-001 — Quy tắc Cấu trúc Tài liệu](../../../knowledge-base/99-Templates/Documents-Template.md) | **Contract tài liệu** | Quy định frontmatter và quy tắc liên kết (standard markdown link, relative path). |

---

*Tài liệu được chuẩn hóa và quản lý bởi TNMCORE-OS.*

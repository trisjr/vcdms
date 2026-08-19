# Findings — business-analyst

> Lens duy nhất của Bước 2 (read-only). Nguồn sự thật: `docs/020-Requirements/SRS-VETC.md` (180 dòng, `status: draft`).
> Nhãn dùng xuyên suốt: **[SRS]** nguyên văn/trực tiếp · **[SUY LUẬN]** suy ra có nêu căn cứ · **[THIẾU]** SRS không có.
> Số dòng trích dẫn (d.NN) tính theo file SRS gốc.

## Kết luận của worker (nguyên văn SUMMARY)

> Đã đọc toàn văn SRS-VETC.md (181 dòng) và trả về phân tích 5 phần đầy đủ: nguyên liệu BRD (context/stakeholder/process/10 business rule/objective), nguyên liệu PRD (25 FR + 7 NFR có mã và nguồn, state machine 5 trạng thái + 8 nhánh thiếu, 3 persona), 31 gap có cấu trúc đầy đủ (11 Blocker / 11 Quan trọng / 9 Nên có, phủ đủ 10/10 điểm bắt buộc), 18 mâu thuẫn nội tại có trích dòng chính xác, và ~35 thuật ngữ Glossary dựa trên SRS.
>
> CẢNH BÁO VẬN HÀNH: SRS-VETC.md KHÔNG tồn tại trong worktree pm-doc-brd-prd-vetc — chỉ có ở repo chính, đang untracked. Writer chạy trong worktree sẽ không tìm thấy nguồn.
>
> LƯU Ý GATE: Glossary cần bổ sung ~35 thuật ngữ từ con số 0 — chạm điều kiện escalate T3 ghi tại brief.md; nghiêng về giữ T2 (một nguồn, một writer), quyết định thuộc PM.

**STATUS**: DONE · **FILES_TOUCHED**: none (đúng ownership read-only đã cấp).

> 📎 **Phần 3 (Gap list 31 câu), Phần 4 (18 mâu thuẫn nội tại) và Phần 5 (Glossary ~35 thuật ngữ)** nằm ở file tiếp nối: [business-analyst-gaps.md](./business-analyst-gaps.md). Tách file vì độ dài, cùng một lens và cùng một lần dispatch.

## PM đọc được gì

- **Cảnh báo vận hành đã xử lý**: PM đã verify và đồng bộ `SRS-VETC.md` + bản `Requirements-MOC.md` mới nhất từ checkout chính vào worktree (MD5 khớp). Writer sẽ đọc được nguồn.
- **BRD sẽ mỏng ở tầng business và đó là đúng**: SRS gần như thuần chức năng. Business goal định lượng, KPI, ngân sách, timeline, stakeholder ngoài 3 role đều `TBD`. Đây khớp chính xác với hedge đã ghi tại `brief.md` mục "Ghi chú về Q3" — khoảng trống này **là deliverable thứ ba**, không phải lỗi.
- **Rủi ro thiết kế lớn nhất là state machine**: 5 trạng thái happy path, thiếu 8 nhánh. 5/11 câu Blocker (Q-09, Q-10, Q-11, Q-24, Q-25) đều quy về đây.
- **Chuỗi phụ thuộc gốc**: Q-01 (có luồng nhập kho không?) → Q-26 (tồn kho lấy đâu ra?) → Q-06 (ai gán dải Series?) → NFR-05 (chặn series trùng bằng cách nào?). Bốn câu này là **một khối**, khách hàng trả lời Q-01 khác đi thì cả khối đổi theo. PRD phải nêu rõ liên đới này.
- **Giữ T2, không escalate lên T3**: điều kiện escalate ghi tại `brief.md` là "phải chuẩn hóa Glossary trên diện rộng". ~35 thuật ngữ này rút từ **một** nguồn SRS duy nhất và thêm vào một file đang gần như trống — đó là *khởi tạo*, không phải *chuẩn hóa diện rộng* (vốn hàm ý sửa nhiều tài liệu hiện hữu và đối chiếu chéo). Một writer làm gọn trong một lượt.

## Mâu thuẫn với lens khác

Không có — đây là lens duy nhất của Bước 2. PM chủ động bỏ `context-auditor` khỏi bước phân tích vì PM đã tự nắm inventory (thiếu `000-Index.md`, dead link `PRD-TNMCORE-OS.md`, Glossary 3 thuật ngữ); spawn thêm agent để khám phá lại là vi phạm guardrail spawn-overhead. `context-auditor` được để dành cho Bước 6 (verify), nơi nó **bắt buộc** phải khác agent đã viết.

---

# PHẦN 1 — BUSINESS LAYER (nguyên liệu cho BRD)

## 1.1. Business context & problem statement

| Nội dung | Nhãn | Căn cứ |
|---|---|---|
| Doanh nghiệp phân phối **thẻ VETC** từ kho tới mạng lưới Sale/Đại lý; cần hệ thống quản lý xuất kho & phân phối. | **[SRS]** | Tiêu đề, d.11–12 |
| Vấn đề #1: **thất thoát thẻ** — có hẳn mục chức năng "Quản Lý Thất Thoát & Truy Vết Thẻ" với cơ chế đền bù. | **[SUY LUẬN]** | Sự tồn tại của III.4 (d.133–142) |
| Vấn đề #2: **thiếu truy vết** — không biết thẻ đi từ kho nào, qua tay ai, ngày nào. | **[SUY LUẬN]** | III.4 liệt kê đúng 4 câu hỏi truy vết (d.134–138) |
| Vấn đề #3: **quy trình duyệt lỏng lẻo / đơn trùng** — Sale bấm gửi 2 lần gây xuất kho thừa. | **[SUY LUẬN]** | III.1 + d.93 "Sale bấm gửi 2 lần" |
| Vấn đề #4: **thiếu bằng chứng giao nhận** — tranh chấp khi Sale nói không nhận đủ. | **[SUY LUẬN]** | III.3 bắt buộc POD + Biên bản Bàn giao (d.128–131) |
| Hiện trạng "as-is" (đang làm thủ công bằng gì? bao lâu? tốn bao nhiêu?) | **[THIẾU]** | SRS im lặng hoàn toàn |

## 1.2. Stakeholder / Actor

| Actor | Trách nhiệm nghiệp vụ **[SRS]** | Ghi chú BA |
|---|---|---|
| **Admin** | Phê duyệt **cuối cùng** đơn xuất kho; quản lý danh mục (kho, **nhân sự**); giám sát toàn bộ luồng dữ liệu; xem **báo cáo tổng hợp**. | Cấp duyệt 2. "Quản lý nhân sự" và "báo cáo tổng hợp" xuất hiện **duy nhất** ở d.41, mục III không có FR nào chi tiết hóa → Q-28. |
| **Nhân viên kho (NV Kho)** | Tiếp nhận yêu cầu; kiểm tra tồn kho; điều chỉnh số lượng xuất; chọn kho xuất hàng; quản lý thất thoát; cập nhật danh mục kho. | Cấp duyệt 1 — cũng là người **cấp dải Series** (suy từ III.3 "do kho cấp"). |
| **Nhân viên Sale / Đại lý** | Tạo yêu cầu xuất thẻ; theo dõi trạng thái đơn; xác nhận nhận hàng (kèm hình ảnh chứng minh); tra cứu thẻ. | SRS gộp "Sale" và "Đại lý" làm **một** role → rủi ro lớn, xem Q-21. |
| **Đơn vị Vận chuyển (Shipper)** | Actor **ngoài hệ thống**, nhận đơn qua API và đẩy trạng thái tracking về. | d.59, d.75–79. **Không** thuộc 3 role RBAC → chỉ là system-to-system integration. |
| Nhà cung cấp thẻ VETC | **[THIẾU]** | Không xuất hiện ở đâu dù tiêu đề có "Nhập Kho" → Q-01 |
| Kế toán / Tài chính (xử lý tiền đền bù) | **[THIẾU]** | III.4 có "nộp tiền đền bù" nhưng không có actor chịu trách nhiệm → Q-04, Q-22 |

## 1.3. Business process end-to-end (luồng phê duyệt 2 cấp) — **[SRS]** mục II (d.47–112)

1. **Bước 1 — Tạo yêu cầu** *(Sale/Đại lý)*: lập đơn, chọn loại thẻ + số lượng → `Chờ kho duyệt (Pending Warehouse)`.
2. **Bước 2 — Soát xét & Điều chỉnh** *(NV Kho)*: kiểm tra tồn → 2 nhánh:
   - **Từ chối**: nếu đơn trùng lặp / không hợp lệ.
   - **Duyệt**: điều chỉnh số lượng (bắt buộc ghi chú lý do) + gán kho xuất → `Chờ Admin duyệt (Pending Admin Approval)`.
3. **Bước 3 — Phê duyệt cuối** *(Admin)* → `Chờ vận chuyển (Ready for Shipping)`.
4. **Bước 4 — Vận chuyển** *(Hệ thống ↔ Shipper)*: đẩy đơn qua API; đồng bộ real-time → `Đang vận chuyển (In Transit)`.
5. **Bước 5 — Nghiệm thu** *(Sale/Đại lý)*: chụp ảnh đối soát, xác nhận số lượng + dải Series, bấm **[Hoàn thành đơn hàng]** → `Hoàn thành (Completed)` + tự động xuất Biên bản Bàn giao (PDF/Excel).

**[SUY LUẬN]** Đây là quy trình **một chiều, chỉ có happy path**. Toàn bộ nhánh ngược (từ chối → đi đâu, giao thất bại, hàng hoàn, hủy đơn, nhận thiếu) đều không được định nghĩa.

## 1.4. Business rules bắt buộc (MUST)

| # | Business rule | Nhãn | Nguồn |
|---|---|---|---|
| BR-01 | Luồng phê duyệt **2 cấp bắt buộc**: `Kho duyệt` → `Admin duyệt`. Không được bỏ qua cấp nào. | **[SRS]** | III.1 d.122; II d.49 |
| BR-02 | NV Kho sửa *Số lượng duyệt* khác *Số lượng yêu cầu* → **bắt buộc nhập lý do ghi chú**. | **[SRS]** | III.1 d.121; II d.94 |
| BR-03 | Khi nhận hàng, Sale/Đại lý **bắt buộc đính kèm tối thiểu 01 ảnh** chụp lô thẻ thực tế. | **[SRS]** | III.3 d.129 |
| BR-04 | Đơn chỉ chuyển `Completed` sau khi Sale xác nhận **đúng số lượng VÀ đúng dải Series** do kho cấp. | **[SRS]** | II Bước 5 d.110 |
| BR-05 | Biên bản Bàn giao Thẻ sinh **tự động ngay khi** bấm [Hoàn thành]. | **[SRS]** | III.3 d.131 |
| BR-06 | Mọi tác động dữ liệu phải ghi Audit Log (ai tạo, ai sửa số lượng, ai duyệt + timestamp). | **[SRS]** | IV.1 d.164 |
| BR-07 | Chặn nhập **số lượng âm**; chặn chọn **dải Series bị trùng lặp**. | **[SRS]** | IV.2 d.167 |
| BR-08 | Thẻ báo mất sau khi hoàn tất đền bù → **tự động** cập nhật trạng thái `Báo mất - Đã đền bù`. | **[SRS]** | III.4 d.142 |
| BR-09 | Đơn phải được gán **một kho xuất** lấy từ Danh mục kho trước khi qua cấp duyệt 2. | **[SRS]** | II Bước 2 d.95 |
| BR-10 | Đơn trùng lặp gửi "trong thời gian ngắn" → hệ thống cảnh báo **hoặc** cho NV Kho từ chối nhanh. | **[SRS]** nhưng mơ hồ | III.1 d.120 → Q-05, Q-17 |

## 1.5. Business objective / giá trị kỳ vọng

| Mục tiêu | Nhãn | Căn cứ |
|---|---|---|
| **Giảm thất thoát thẻ** — mọi thẻ mất phải được ghi nhận và đền bù. | **[SUY LUẬN]** | Toàn bộ III.4 |
| **Minh bạch truy vết 100%** — bất kỳ mã thẻ nào cũng tra được kho nguồn, người xuất, người nhận, mốc thời gian. | **[SUY LUẬN]** | III.4 d.134–138 |
| **Chuẩn hóa & siết kiểm soát phê duyệt** — mọi đơn qua 2 cấp có dấu vết. | **[SUY LUẬN]** | BR-01 + Audit Log IV.1 |
| **Giảm tranh chấp giao nhận** — POD ảnh + Biên bản Bàn giao tự động làm bằng chứng. | **[SUY LUẬN]** | III.3 |
| **Rút ngắn thời gian tra cứu** — search ≤ 2 giây thay vì lục Excel. | **[SUY LUẬN]** từ NFR **[SRS]** | IV.2 d.168 |
| **KPI / chỉ tiêu đo lường thành công** | ❌ **KHÔNG CÓ TRONG SRS** | → Q-29 |
| **Ngân sách / ROI / chi phí hiện tại của vấn đề** | ❌ **KHÔNG CÓ TRONG SRS** | → Q-29 |
| **Ràng buộc thời gian / deadline go-live** | ❌ **KHÔNG CÓ TRONG SRS** | → Q-30 |
| **Quy mô kinh doanh** (số đại lý, sản lượng thẻ/tháng, doanh thu) | ❌ **KHÔNG CÓ TRONG SRS** | → Q-07 |
| **Ràng buộc pháp lý / tuân thủ ngành ETC** | ❌ **KHÔNG CÓ TRONG SRS** | → Q-08 |

> 📌 **Khuyến nghị BRD**: 5 dòng cuối bảng phải ghi `TBD` và trỏ sang file câu hỏi khách hàng. **Tuyệt đối không điền số phỏng đoán.**

---

# PHẦN 2 — PRODUCT LAYER (nguyên liệu cho PRD)

## 2.1. Functional Requirements

| ID | Tính năng | Mô tả | Nguồn (SRS) | Ưu tiên & lý do |
|---|---|---|---|---|
| FR-01 | Tạo yêu cầu xuất thẻ | Sale/Đại lý lập đơn: chọn loại thẻ, số lượng | II Bước 1 (d.87–89); III.1 (d.119) | **P0** — điểm khởi phát toàn bộ workflow |
| FR-02 | Kiểm tra tồn kho khi soát xét | NV Kho xem tồn để quyết định duyệt/điều chỉnh | I (d.42); II Bước 2 (d.92) | **P0** — input bắt buộc cho cấp duyệt 1 |
| FR-03 | Cảnh báo / từ chối nhanh đơn trùng lặp | Cảnh báo hoặc cho NV Kho từ chối đơn trùng gửi trong thời gian ngắn | III.1 (d.120); II (d.93) | **P1** — chống lỗi vận hành, không chặn luồng chính; cần chốt Q-05 |
| FR-04 | Điều chỉnh Số lượng duyệt + lý do bắt buộc | NV Kho sửa SL duyệt ≠ SL yêu cầu, **bắt buộc** ghi lý do | III.1 (d.121); II (d.94) | **P0** — BR-02, gắn trực tiếp Audit Log |
| FR-05 | Gán kho xuất hàng | NV Kho chọn kho từ Danh mục kho | II Bước 2 (d.95) | **P0** — không có kho nguồn thì không truy vết được (FR-14) |
| FR-06 | Phê duyệt cấp 1 (Kho) | NV Kho duyệt chuyển đơn sang chờ Admin | II Bước 2 (d.96–97) | **P0** — mắt xích 1 của BR-01 |
| FR-07 | Phê duyệt cấp 2 (Admin) | Admin ra quyết định duyệt cuối cùng | II Bước 3 (d.99–101) | **P0** — mắt xích 2 của BR-01 |
| FR-08 | Đẩy đơn sang đơn vị vận chuyển qua API | Hệ thống tự động push đơn đã duyệt sang carrier | II Bước 4 (d.104); III.2 (d.125) | **P1** — phụ thuộc bên thứ ba; phase 1 có thể nhập tay mã vận đơn |
| FR-09 | Đồng bộ tracking real-time | Cập nhật vị trí/trạng thái theo thời gian thực từ carrier | II Bước 4 (d.105); III.2 (d.125) | **P1** — không chặn việc giao/nhận thực tế |
| FR-10 | Hiển thị thông tin vận chuyển | Trạng thái, vị trí hiện tại, mã vận đơn, tên đơn vị giao hàng | III.2 (d.126) | **P1** — phụ thuộc FR-09 |
| FR-11 | Upload ảnh POD (tối thiểu 01) | Bắt buộc Sale đính kèm ≥ 1 ảnh chụp lô thẻ thực tế | III.3 (d.129); II (d.109) | **P0** — BR-03, bằng chứng giao nhận |
| FR-12 | Check-list đối soát dải Series | Hiển thị Series bắt đầu – kết thúc do kho cấp để Sale đối soát | III.3 (d.130); II (d.110) | **P0** — BR-04, điều kiện đóng đơn |
| FR-13 | Xuất Biên bản Bàn giao Thẻ tự động | Sinh PDF/Excel ngay khi bấm [Hoàn thành] | III.3 (d.131); II (d.82) | **P1** — dữ liệu đã có sẵn trong hệ thống |
| FR-14 | Truy xuất nguồn gốc thẻ (Traceability) | Tra mã thẻ → kho xuất, NV kho phụ trách, Sale/Đại lý nhận, ngày giờ xuất, ngày giờ nhận | III.4 (d.134–138) | **P0** — business objective cốt lõi |
| FR-15 | Ghi nhận thẻ báo mất / hỏng | Đánh dấu thẻ mất/hỏng trong hệ thống | III.4 (d.140) | **P1** — sau khi luồng chính chạy |
| FR-16 | Ghi nhận đền bù thẻ mất | Nhập số tiền, mã giao dịch, đính kèm hóa đơn đền bù | III.4 (d.141) | **P2** — phụ thuộc FR-15, cần chốt Q-04 |
| FR-17 | Tự động cập nhật trạng thái `Báo mất - Đã đền bù` | Chuyển trạng thái thẻ sau khi ghi nhận đền bù | III.4 (d.142) | **P2** — hệ quả FR-16 |
| FR-18 | CRUD Danh mục kho | Tạo mới, chỉnh sửa, xóa hoặc **ẩn** danh mục kho | III.5 (d.145) | **P0** — master data, FR-05 phụ thuộc |
| FR-19 | Quản lý thông tin chi tiết kho | Tên kho, Địa chỉ, NV kho phụ trách gửi hàng, SĐT liên hệ | III.5 (d.146) | **P0** — cùng FR-18 |
| FR-20 | Global Search | Tra cứu nhanh theo Mã thẻ / Dải Series và Tên nhân viên | III.6 (d.150) | **P1** — FR-14 đã phủ nhu cầu truy vết cốt lõi |
| FR-21 | Bộ lọc nâng cao đa điều kiện | Lọc theo khoảng thời gian, trạng thái đơn, kho xuất, đại lý tiếp nhận | III.6 (d.151–155) | **P1** — như FR-20 |
| FR-22 | Theo dõi trạng thái đơn (phía Sale) | Sale theo dõi trạng thái đơn của mình | I (d.43) | **P0** — không thấy đơn thì không biết khi nào nhận hàng |
| FR-23 | Tra cứu thẻ (phía Sale) | Sale tra cứu thẻ | I (d.43) | **P1** — khác FR-14 ở scope dữ liệu (xem Q-12) |
| FR-24 | Quản lý danh mục nhân sự | Admin quản lý danh mục nhân sự | I (d.41) | **P1** — ⚠️ mục III **không có** FR chi tiết → Q-28 |
| FR-25 | Báo cáo tổng hợp & giám sát luồng dữ liệu | Admin xem báo cáo tổng hợp, giám sát toàn bộ luồng | I (d.41) | **P2** — ⚠️ mục III **không có** FR chi tiết → Q-28 |

> **Lưu ý cho PRD writer**: FR-24 và FR-25 chỉ tồn tại trong **một ô của bảng RBAC**, không hề được cụ thể hóa ở mục III. **Không được tự bịa** nội dung báo cáo. Ghi `TBD` + trỏ Q-28.

## 2.2. Non-Functional Requirements

| ID | Hạng mục | Mô tả (**giữ nguyên số liệu SRS**) | Nguồn | Ưu tiên & lý do |
|---|---|---|---|---|
| NFR-01 | Xác thực | **JWT (JSON Web Token) hoặc OAuth 2.0** | IV.1 (d.162) | **P0** — ⚠️ "hoặc" chưa chốt → Q-14 |
| NFR-02 | Phân quyền | Phân quyền **chặt chẽ theo vai trò (RBAC)** cho 3 nhóm user | IV.1 (d.162); I (d.37) | **P0** — dữ liệu thẻ là tài sản có giá trị |
| NFR-03 | Mã hóa & truyền tải | Mã hóa **toàn bộ dữ liệu nhạy cảm**; bắt buộc **HTTPS (SSL/TLS)** | IV.1 (d.163) | **P0** — bắt buộc, chi phí thấp |
| NFR-04 | Audit Log | Ghi nhận **toàn bộ** lịch sử tác động dữ liệu: ai tạo, ai sửa số lượng, ai duyệt, **timestamp**; phục vụ tra soát & kiểm toán | IV.1 (d.164) | **P0** — cơ chế thực thi BR-01/BR-02, công cụ chống thất thoát |
| NFR-05 | Error Handling / Validation | **Chặn nhập số lượng âm**, **chặn chọn dải series bị trùng lặp** | IV.2 (d.167) | **P0** — BR-07; series trùng = sai lệch tồn kho không sửa được |
| NFR-06 | Response Time | Tra cứu / tìm kiếm mã thẻ **≤ 2 giây** | IV.2 (d.168) | **P1** — chỉ tiêu duy nhất có số; chỉ áp cho tra cứu/tìm kiếm |
| NFR-07 | Backup & Recovery | **Tự động sao lưu hàng ngày (Daily Backup)** | IV.2 (d.169) | **P1** — SRS nêu tần suất, **không** nêu RPO/RTO/retention |

**❌ NFR mà SRS HOÀN TOÀN IM LẶNG — [THIẾU], không được bịa số:**
Availability/Uptime SLA · Concurrent users · Throughput · Data retention (dữ liệu & ảnh POD) · RPO/RTO · Scalability · Browser/thiết bị hỗ trợ · i18n · Accessibility · Disaster Recovery · Monitoring/Alerting · Rate limiting · Nơi lưu trữ dữ liệu (on-prem/cloud, trong/ngoài nước).
→ Toàn bộ vào Q-07, Q-08, Q-13, Q-23.

## 2.3. State machine — Trạng thái đơn hàng

**Trạng thái SRS ĐÃ định nghĩa [SRS]** — đúng **5** trạng thái:

| # | Trạng thái | Tiếng Việt | Nguồn |
|---|---|---|---|
| S1 | `Pending Warehouse` | Chờ kho duyệt | d.63, d.89 |
| S2 | `Pending Admin Approval` | Chờ Admin duyệt | d.69, d.97 |
| S3 | `Ready for Shipping` | Chờ vận chuyển | d.73, d.101 |
| S4 | `In Transit` | Đang vận chuyển | d.77, d.106 |
| S5 | `Completed` | Hoàn thành | d.81, d.112 |

**Chuyển trạng thái SRS ĐÃ định nghĩa [SRS]:**

```
(khởi tạo) --Sale tạo đơn---------------------> S1 Pending Warehouse
S1 --NV Kho duyệt (đã gán kho + SL duyệt)-----> S2 Pending Admin Approval
S2 --Admin phê duyệt cuối---------------------> S3 Ready for Shipping
S3 --Hệ thống đẩy API sang carrier------------> S4 In Transit
S4 --Sale upload POD + đối soát Series + [Hoàn thành]--> S5 Completed
```

**⚠️ Chuyển trạng thái SRS KHÔNG ĐỊNH NGHĨA [THIẾU]:**

| # | Sự kiện | Vấn đề | Gap |
|---|---|---|---|
| T-a | **NV Kho từ chối đơn** | Nhánh `alt` trong mermaid (d.65–67) có "Từ chối đơn" nhưng **KHÔNG có `Note over System` gán trạng thái** → nhánh **cụt**. | Q-09 |
| T-b | **Admin từ chối đơn** | Bước 3 (d.99–101) **hoàn toàn không có nhánh từ chối**. Cấp duyệt mà không có quyền từ chối là vô nghĩa. | Q-10 |
| T-c | **Sale sửa & gửi lại đơn bị từ chối** | Không có trạng thái `Draft`/`Rejected`/`Resubmitted`. | Q-09 |
| T-d | **Hủy đơn** | Không có `Cancelled` ở bất kỳ giai đoạn nào. | Q-24 |
| T-e | **Giao hàng thất bại / hoàn hàng** | Không có `Delivery Failed` / `Returned`. Carrier giao không được → đơn kẹt vĩnh viễn ở `In Transit`. | Q-25 |
| T-f | **Sale nhận thiếu / lệch Series** | Bước 5 chỉ mô tả "xác nhận đúng". Không có `Disputed`/`Partially Received`. | Q-11 |
| T-g | **Sub-status của carrier map vào đâu** | III.2 (d.126) liệt kê 4 trạng thái carrier nhưng mục II chỉ có **một** `In Transit`. Quan hệ không được định nghĩa. | Q-15 |
| T-h | **Vòng đời trạng thái THẺ (khác trạng thái ĐƠN)** | SRS chỉ nêu **đúng một** trạng thái thẻ: `Báo mất - Đã đền bù` (d.142). Còn lại **[THIẾU]** hoàn toàn. | Q-16 |

> 📌 Đây là **rủi ro thiết kế lớn nhất** của SRS: state machine mới phủ happy path, thiếu 8 nhánh. Không chốt trước khi thiết kế DB → phải migration sau.

## 2.4. Persona **[SUY LUẬN]** từ 3 role RBAC

| Persona | Suy luận | Căn cứ **[SRS]** | Chưa rõ |
|---|---|---|---|
| **P1 — Admin** | Người ra quyết định cuối, cần cái nhìn toàn cảnh; nhiều màn hình danh sách/báo cáo; ưu tiên duyệt nhanh và giám sát. | d.41 | Số lượng Admin? Có phân cấp Admin không? |
| **P2 — Nhân viên Kho** | Vận hành trực tiếp tại kho với hàng vật lý; thao tác nhiều lần/ngày; cần đối chiếu tồn kho ↔ đơn nhanh; là người cấp dải Series. | d.42; d.130 "do kho cấp"; d.146 | Có bị giới hạn theo kho phụ trách không? (Q-12) |
| **P3 — Sale / Đại lý** | Người dùng ở **hiện trường**, nghiệm thu **tại nơi nhận hàng** — thao tác chụp ảnh POD mang đặc trưng mobile mạnh. | d.43; d.108–111 | ⚠️ Sale (nội bộ) và Đại lý (đối tác ngoài) bị gộp một role — hai persona khác nhau căn bản (Q-21). Nền tảng web/mobile **[THIẾU]** (Q-23). |

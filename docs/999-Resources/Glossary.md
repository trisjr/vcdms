---
id: GLOSSARY-001
type: glossary
status: live
created: 2026-02-04
updated: 2026-08-19
---

# Glossary (Từ điển Thuật ngữ)

Từ điển thuật ngữ **nghiệp vụ và kỹ thuật** của kho tài liệu này. Mục đích là để BA, Architect, Engineer, QA và khách hàng dùng chung **một** cách gọi cho **một** khái niệm.

> [!IMPORTANT]
> Mọi định nghĩa ở mục *Domain VETC* đều **rút trực tiếp từ** [SRS-VETC](../020-Requirements/SRS-VETC.md), có ghi mục nguồn. Thuật ngữ nào SRS **dùng nhưng chưa định nghĩa** được đánh dấu rõ và trỏ sang mã câu hỏi tương ứng trong [Analysis-Open-Questions-VETC](../050-Research/Analysis-Open-Questions-VETC.md). **Không tự bịa định nghĩa.**

## 📑 Mục lục

- [1. Domain VETC — Nghiệp vụ cốt lõi](#1-domain-vetc--nghiệp-vụ-cốt-lõi)
- [2. Domain VETC — Vai trò (Actors)](#2-domain-vetc--vai-trò-actors)
- [3. Domain VETC — Trạng thái Đơn xuất thẻ](#3-domain-vetc--trạng-thái-đơn-xuất-thẻ)
- [4. Domain VETC — Trạng thái Thẻ](#4-domain-vetc--trạng-thái-thẻ)
- [5. Thuật ngữ kỹ thuật & phi chức năng](#5-thuật-ngữ-kỹ-thuật--phi-chức-năng)
- [6. Thuật ngữ chung (các dự án khác)](#6-thuật-ngữ-chung-các-dự-án-khác)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

---

## 1. Domain VETC — Nghiệp vụ cốt lõi

| Thuật ngữ | Định nghĩa | Nguồn |
| :--- | :--- | :--- |
| **VETC** | ⚠️ **Chưa được định nghĩa.** SRS dùng xuyên suốt nhưng không giải thích. | Q-27 |
| **Thẻ VETC** | Đơn vị hàng hóa được quản lý xuất kho và phân phối. Mỗi thẻ có **Mã thẻ** riêng, thuộc một **Loại thẻ**, và nằm trong một **Dải Series**. | SRS II, III.3, III.6 |
| **Mã thẻ** | Định danh của một thẻ VETC riêng lẻ. Là khóa để **truy xuất nguồn gốc** và là tiêu chí của **Global Search**. | SRS III.4, III.6, IV.2 |
| **Loại thẻ** | Phân loại thẻ VETC mà Sale/Đại lý chọn khi tạo đơn. ⚠️ SRS **không liệt kê** các loại cụ thể và không có chức năng quản lý danh mục này. | SRS II Bước 1, III.1 → Q-27 |
| **Dải Series (Series Range)** | Khoảng số Series liên tục **do kho cấp** cho một đơn, xác định bởi cặp *Series bắt đầu – Series kết thúc*. Là căn cứ để Sale đối soát khi nhận hàng. Hệ thống phải **chặn chọn dải Series bị trùng lặp**. | SRS III.3, II Bước 5, IV.2 |
| **Đơn xuất thẻ** | **Tên chuẩn hóa.** Yêu cầu do Sale/Đại lý khởi tạo để nhận thẻ từ kho, đi qua luồng phê duyệt 2 cấp và kết thúc bằng nghiệm thu tại nơi nhận. ⚠️ SRS gọi khái niệm này bằng **4 tên khác nhau** ("đơn xuất kho", "yêu cầu xuất thẻ", "đơn hàng", "đơn") — **thống nhất dùng "Đơn xuất thẻ"** trong mọi tài liệu mới. | SRS I, II, III |
| **Số lượng yêu cầu** | Số lượng thẻ do Sale/Đại lý đề xuất khi tạo đơn. | SRS III.1 |
| **Số lượng duyệt** | Số lượng thẻ Nhân viên Kho thực tế chấp thuận xuất. Có thể **khác** Số lượng yêu cầu; khi khác thì **bắt buộc nhập lý do ghi chú**. | SRS III.1, II Bước 2 |
| **Luồng phê duyệt 2 cấp** | Quy trình **bắt buộc**: `Kho duyệt` → `Admin duyệt`. Không được bỏ qua cấp nào. | SRS II, III.1 |
| **Kho** | Đơn vị lưu trữ và xuất thẻ, quản lý trong **Danh mục kho**. Mỗi kho lưu: *Tên kho*, *Địa chỉ*, *Tên nhân viên kho phụ trách gửi hàng*, *Số điện thoại liên hệ*. | SRS III.5 |
| **Danh mục kho** | Master data các kho. Hỗ trợ tạo mới, chỉnh sửa, **xóa hoặc ẩn**. Là nguồn để Nhân viên Kho **gán kho xuất** cho đơn. | SRS III.5, II Bước 2 |
| **Tồn kho** | Số thẻ hiện có trong một kho. ⚠️ SRS yêu cầu Nhân viên Kho "kiểm tra tồn kho" nhưng **không định nghĩa dữ liệu tồn kho** ở bất kỳ đâu — danh mục kho không hề chứa số liệu này. | SRS I, II Bước 2 → Q-26, Q-01 |
| **POD (Proof of Delivery)** | Bằng chứng giao nhận: **tối thiểu 01 ảnh** chụp lô thẻ thực tế, do Sale/Đại lý đính kèm khi nhận hàng. | SRS III.3 |
| **Biên bản Bàn giao Thẻ** | Chứng từ (PDF/Excel) hệ thống **tự động sinh ngay khi** Sale bấm [Hoàn thành đơn hàng]. ⚠️ SRS không quy định mẫu biểu, nội dung bắt buộc, hay yêu cầu chữ ký. | SRS III.3, II Bước 5 → Q-19 |
| **Truy xuất nguồn gốc (Traceability)** | Khả năng tra bất kỳ mã thẻ nào ra đầy đủ: kho xuất, nhân viên kho phụ trách, Sale/Đại lý tiếp nhận, ngày giờ xuất kho, ngày giờ nhận hàng thực tế. | SRS III.4 |
| **Thất thoát thẻ** | Thẻ được **báo mất hoặc hỏng**, ghi nhận trong hệ thống và xử lý qua cơ chế đền bù. | SRS III.4 |
| **Đền bù thẻ mất** | Việc nộp tiền/bù tiền cho thẻ mất. Ghi nhận gồm: **số tiền**, **mã giao dịch**, **hóa đơn đền bù đính kèm**. ⚠️ SRS dùng từ "tích hợp" nhưng ba trường dữ liệu lại mang đặc trưng ghi nhận thủ công. | SRS III.4 → Q-04, Q-22 |
| **Đơn vị Vận chuyển (Shipper / Carrier)** | Đối tác vận chuyển **đã ký hợp đồng**, nhận đơn qua API và trả về dữ liệu tracking. Là **actor ngoài hệ thống** — không thuộc 3 nhóm người dùng RBAC. ⚠️ SRS không nêu danh tính đối tác. | SRS II Bước 4, III.2 → Q-02 |
| **Mã vận đơn** | Mã do đơn vị vận chuyển cấp, hiển thị trong thông tin theo dõi của đơn. | SRS III.2 |
| **Real-time Tracking** | Cơ chế đồng bộ vị trí/trạng thái đơn hàng từ đơn vị vận chuyển. ⚠️ SRS **không định lượng** "real-time" là bao lâu. | SRS II Bước 4, III.2 → Q-03 |
| **Global Search** | Tìm kiếm nhanh theo Mã thẻ / Dải Series thẻ và Tên nhân viên (Sale, Kho, Admin). | SRS III.6 |

## 2. Domain VETC — Vai trò (Actors)

| Vai trò | Trách nhiệm (theo SRS) | Nguồn |
| :--- | :--- | :--- |
| **Admin (Quản trị viên)** | Phê duyệt cuối cùng đơn xuất kho; quản lý danh mục (kho, nhân sự); giám sát toàn bộ luồng dữ liệu; xem báo cáo tổng hợp. | SRS I |
| **NV Kho (Nhân viên kho)** | Tiếp nhận yêu cầu; kiểm tra tồn kho; điều chỉnh số lượng xuất; chọn kho xuất hàng; quản lý thất thoát; cập nhật danh mục kho. | SRS I |
| **Sale / Đại lý** | Tạo yêu cầu xuất thẻ; theo dõi trạng thái đơn hàng; xác nhận nhận hàng (kèm hình ảnh chứng minh); tra cứu thẻ. ⚠️ SRS **gộp Sale và Đại lý làm một vai trò** — cần xác nhận đây có phải hai đối tượng khác nhau không. | SRS I → Q-21 |

## 3. Domain VETC — Trạng thái Đơn xuất thẻ

| Trạng thái | Tiếng Việt | Ý nghĩa | Nguồn |
| :--- | :--- | :--- | :--- |
| `Pending Warehouse` | Chờ kho duyệt | Trạng thái ban đầu ngay khi Sale/Đại lý tạo đơn. | SRS II |
| `Pending Admin Approval` | Chờ Admin duyệt | Sau khi Nhân viên Kho đã kiểm tồn, chốt số lượng duyệt và gán kho xuất. | SRS II |
| `Ready for Shipping` | Chờ vận chuyển | Sau khi Admin phê duyệt cuối. | SRS II |
| `In Transit` | Đang vận chuyển | Sau khi đơn được đẩy sang đơn vị vận chuyển. | SRS II |
| `Completed` | Hoàn thành | Sau khi Sale upload POD, đối soát Series và bấm [Hoàn thành đơn hàng]. | SRS II |

> [!WARNING]
> SRS **chỉ định nghĩa 5 trạng thái trên và 5 phép chuyển trạng thái** — tất cả đều là luồng thuận. Các trạng thái `Rejected`, `Cancelled`, `Delivery Failed`, `Returned`, `Discrepancy` **hiện là đề xuất chưa được khách hàng chốt** (Q-09, Q-10, Q-11, Q-24, Q-25), nên **chưa** đưa vào từ điển này. Chỉ bổ sung sau khi có xác nhận.

## 4. Domain VETC — Trạng thái Thẻ

| Trạng thái | Ý nghĩa | Nguồn |
| :--- | :--- | :--- |
| `Báo mất - Đã đền bù` | Trạng thái thẻ được hệ thống **tự động** cập nhật sau khi ghi nhận xong việc đền bù. | SRS III.4 |

> [!WARNING]
> Đây là **trạng thái thẻ duy nhất** SRS nêu ra. Toàn bộ vòng đời còn lại của thẻ (còn trong kho, đã gán vào đơn, đã bàn giao, hỏng…) **chưa được định nghĩa** — xem Q-16. Lưu ý phân biệt: **trạng thái Thẻ** và **trạng thái Đơn xuất thẻ** là hai vòng đời khác nhau, không được gộp.

## 5. Thuật ngữ kỹ thuật & phi chức năng

| Thuật ngữ | Định nghĩa | Nguồn |
| :--- | :--- | :--- |
| **RBAC (Role-Based Access Control)** | Cơ chế phân quyền dựa trên vai trò, áp dụng cho 3 nhóm người dùng chính. ⚠️ SRS định nghĩa quyền **theo chức năng** nhưng không định nghĩa **phạm vi dữ liệu** mỗi vai trò được xem. | SRS I, IV.1 → Q-12 |
| **Audit Log (Nhật ký hệ thống)** | Ghi nhận toàn bộ lịch sử tác động dữ liệu: ai tạo, ai sửa số lượng, ai duyệt, thời gian cụ thể theo timestamp. Phục vụ tra soát và kiểm toán. | SRS IV.1 |
| **JWT (JSON Web Token)** | Một trong hai cơ chế xác thực SRS nêu ra. ⚠️ SRS viết "JWT **hoặc** OAuth 2.0" — đây là lựa chọn **chưa chốt**, không phải yêu cầu. | SRS IV.1 → Q-14 |
| **OAuth 2.0** | Cơ chế ủy quyền, được SRS nêu như phương án thay thế JWT. Lưu ý hai thứ này **không cùng tầng khái niệm**: JWT là định dạng token, OAuth 2.0 là framework ủy quyền. | SRS IV.1 → Q-14 |
| **HTTPS (SSL/TLS)** | Giao thức bắt buộc để truyền tải toàn bộ dữ liệu của hệ thống. | SRS IV.1 |
| **Daily Backup** | Cơ chế tự động sao lưu dữ liệu hàng ngày. ⚠️ SRS nêu **tần suất** nhưng không nêu thời gian lưu trữ, số bản giữ lại, hay mục tiêu khôi phục. | SRS IV.2 → Q-08 |
| **Response Time** | Thời gian phản hồi. SRS đặt chỉ tiêu **≤ 2 giây** cho thao tác tra cứu / tìm kiếm mã thẻ. ⚠️ Chỉ áp cho tra cứu, không áp cho thao tác khác; và SRS không nêu quy mô dữ liệu để đối chiếu. | SRS IV.2 → Q-07 |

## 6. Thuật ngữ chung (các dự án khác)

Các thuật ngữ dưới đây có sẵn trong repo từ trước và **không liên quan tới dự án VETC**. Giữ lại để không mất dữ liệu; cần gắn nhãn dự án khi biết chúng thuộc về đâu.

- **OTP (One-Time Password)**: Mật khẩu sử dụng một lần để xác thực người dùng.
- **OTP Expiry**: Thời gian hết hạn của mã OTP kể từ khi được tạo.
- **Rate Limit**: Cơ chế giới hạn số lượng yêu cầu (ví dụ: gửi OTP) trong một khoảng thời gian nhất định để bảo mật.

---

## Tài liệu tham khảo

- [SRS-VETC](../020-Requirements/SRS-VETC.md) — nguồn của toàn bộ mục 1–5
- [PRD-VETC](../020-Requirements/PRD-VETC.md) — nơi các thuật ngữ này được dùng để đặc tả chức năng
- [Analysis-Open-Questions-VETC](../050-Research/Analysis-Open-Questions-VETC.md) — tra mã `Q-NN` để biết chi tiết từng điểm còn bỏ ngỏ
- [RULE-001 — Quy tắc Cấu trúc Tài liệu](../../knowledge-base/99-Templates/Documents-Template.md)

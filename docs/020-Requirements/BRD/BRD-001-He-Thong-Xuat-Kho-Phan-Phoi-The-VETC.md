---
id: BRD-001
type: brd
status: draft
project: VETC
owner: "@trisjr"
created: 2026-08-19
updated: 2026-08-19
---

# 📊 TÀI LIỆU YÊU CẦU NGHIỆP VỤ (BRD)
## HỆ THỐNG QUẢN LÝ XUẤT KHO & PHÂN PHỐI THẺ VETC

> **Đối tượng đọc**: Ban lãnh đạo và các bên liên quan phía khách hàng — những người quyết định *có triển khai dự án này hay không* và *đo lường thành công bằng gì*.
> **Nguồn sự thật**: [SRS-VETC](../SRS-VETC.md). Mọi nội dung không có căn cứ trong SRS đều được ghi `TBD` kèm mã câu hỏi `Q-NN` trỏ sang [danh sách câu hỏi gửi khách hàng](../../050-Research/Analysis-Open-Questions-VETC.md).

### Quy ước nhãn dùng xuyên tài liệu

| Nhãn | Ý nghĩa |
| :--- | :--- |
| **[SRS]** | Nội dung có căn cứ trực tiếp/nguyên văn trong SRS-VETC. |
| **[SUY LUẬN]** | Nội dung do BA suy ra, có nêu căn cứ. Cần khách hàng xác nhận. |
| **[TBD]** | Chưa có dữ liệu. Chờ khách hàng trả lời câu hỏi `Q-NN` tương ứng. |

> ⚠️ **Chuẩn hóa thuật ngữ**: SRS gọi cùng một khái niệm bằng 4 tên khác nhau ("đơn xuất kho", "yêu cầu xuất thẻ", "đơn hàng", "đơn"). Tài liệu này thống nhất dùng **"Đơn xuất thẻ"**.

---

## 📑 Mục lục

1. [Tóm tắt điều hành (Executive Summary)](#1-tóm-tắt-điều-hành-executive-summary)
2. [Bối cảnh & Vấn đề nghiệp vụ](#2-bối-cảnh--vấn-đề-nghiệp-vụ)
3. [Mục tiêu nghiệp vụ](#3-mục-tiêu-nghiệp-vụ)
4. [Phạm vi](#4-phạm-vi)
5. [Các bên liên quan](#5-các-bên-liên-quan)
6. [Quy trình nghiệp vụ](#6-quy-trình-nghiệp-vụ)
7. [Quy tắc nghiệp vụ](#7-quy-tắc-nghiệp-vụ)
8. [Ràng buộc & Giả định](#8-ràng-buộc--giả-định)
9. [Rủi ro nghiệp vụ](#9-rủi-ro-nghiệp-vụ)
10. [Tiêu chí thành công](#10-tiêu-chí-thành-công)
11. [Tài liệu liên quan](#11-tài-liệu-liên-quan)

---

## 1. Tóm tắt điều hành (Executive Summary)

Doanh nghiệp đang phân phối **thẻ VETC** từ hệ thống kho tới mạng lưới **Nhân viên Sale / Đại lý**. **[SRS]**

Hoạt động này hiện chưa có một hệ thống quản lý thống nhất, dẫn tới bốn nhóm vấn đề nghiệp vụ: **thất thoát thẻ**, **thiếu khả năng truy vết**, **quy trình phê duyệt lỏng lẻo**, và **thiếu bằng chứng giao nhận**. **[SUY LUẬN]** — căn cứ là sự tồn tại của các nhóm chức năng tương ứng trong SRS (chi tiết tại [mục 2](#2-bối-cảnh--vấn-đề-nghiệp-vụ)).

Dự án đề xuất xây dựng hệ thống **VCDMS** với ba trụ cột nghiệp vụ:

1. **Siết chặt kiểm soát xuất kho** bằng luồng phê duyệt **2 cấp bắt buộc** (Kho duyệt → Admin duyệt), mọi thao tác đều có dấu vết. **[SRS]**
2. **Truy vết trọn vòng đời thẻ** — tra bất kỳ mã thẻ nào ra được kho xuất, người xuất, người nhận và mốc thời gian. **[SRS]**
3. **Chuẩn hóa bằng chứng giao nhận** — bắt buộc ảnh chụp lô hàng thực tế, đối soát dải Series, tự động sinh Biên bản Bàn giao. **[SRS]**

> 📌 **Lưu ý quan trọng dành cho người phê duyệt tài liệu này**
>
> SRS hiện có là một tài liệu **thiên về mô tả chức năng**, gần như không chứa thông tin ở tầng nghiệp vụ định lượng. Cụ thể: **không có KPI, không có ngân sách, không có mốc thời gian go-live, không có mô tả hiện trạng đang vận hành**. Vì vậy các mục 3 (KPI), 8 (Ràng buộc) và 10 (Tiêu chí thành công) của BRD này buộc phải ghi `TBD`.
>
> Đây **không phải là thiếu sót của bước phân tích** — đây là kết quả trung thực của việc rà soát, và chính là lý do tồn tại của tài liệu [Các điểm cần làm rõ](../../050-Research/Analysis-Open-Questions-VETC.md) đi kèm. Đội phân tích chủ trương **thà để trống còn hơn điền số phỏng đoán**, vì một KPI bịa ra sẽ trở thành căn cứ nghiệm thu sai lệch về sau.

---

## 2. Bối cảnh & Vấn đề nghiệp vụ

### 2.1. Bối cảnh

Doanh nghiệp phân phối **thẻ VETC** từ kho tới mạng lưới Sale/Đại lý và cần một hệ thống quản lý việc xuất kho & phân phối. **[SRS]** *(căn cứ: tiêu đề SRS, d.11–12)*

### 2.2. Bốn vấn đề nghiệp vụ cốt lõi

| # | Vấn đề nghiệp vụ | Biểu hiện | Nhãn | Căn cứ |
| :--- | :--- | :--- | :--- | :--- |
| **P-01** | **Thất thoát thẻ** | Thẻ bị mất/hỏng trong quá trình phân phối mà không có cơ chế ghi nhận và quy trách nhiệm. | **[SUY LUẬN]** | SRS dành hẳn một nhóm chức năng "Quản Lý Thất Thoát & Truy Vết Thẻ" kèm cơ chế đền bù (III.4, d.133–142). Một hệ thống chỉ xây chức năng đền bù khi thất thoát đang thực sự xảy ra. |
| **P-02** | **Thiếu khả năng truy vết** | Không xác định được một chiếc thẻ đi ra từ kho nào, qua tay nhân viên nào, giao cho ai và vào thời điểm nào. | **[SUY LUẬN]** | SRS liệt kê đúng 4 câu hỏi truy vết cần trả lời (III.4, d.134–138) — đây là 4 câu hỏi hiện chưa có lời đáp. |
| **P-03** | **Quy trình phê duyệt lỏng lẻo / đơn trùng lặp** | Sale bấm gửi 2 lần gây xuất kho thừa; không có chốt kiểm soát rõ ràng trước khi hàng rời kho. | **[SUY LUẬN]** | SRS đặt ra yêu cầu chống trùng lặp và nêu đích danh tình huống "Sale bấm gửi 2 lần" (III.1 d.120; II d.93) — một tình huống chỉ được viết vào tài liệu khi nó đã từng xảy ra. |
| **P-04** | **Thiếu bằng chứng giao nhận** | Phát sinh tranh chấp khi Sale/Đại lý khai không nhận đủ số lượng, không có căn cứ đối chứng. | **[SUY LUẬN]** | SRS **bắt buộc** ảnh chứng minh khi nhận hàng và tự động sinh Biên bản Bàn giao (III.3, d.128–131). Yêu cầu "bắt buộc" cho thấy đây là điểm đau thực tế. |

### 2.3. Hiện trạng vận hành (As-is)

| Nội dung | Trạng thái |
| :--- | :--- |
| Công cụ đang dùng để quản lý xuất kho & phân phối thẻ | `TBD` — **Q-30** |
| Thời gian trung bình một chu trình xuất kho hiện nay | `TBD` — **Q-30** |
| Chi phí / tổn thất mà vấn đề đang gây ra mỗi tháng | `TBD` — **Q-29** |
| Khối lượng dữ liệu cũ cần chuyển sang hệ thống mới | `TBD` — **Q-30** |

> ⚠️ **SRS im lặng hoàn toàn về hiện trạng as-is.** Không có mô tả nào về cách công ty đang vận hành, mất bao lâu, tốn bao nhiêu. Toàn bộ phần này chờ khách hàng trả lời **Q-30** và **Q-29**.

---

## 3. Mục tiêu nghiệp vụ

### 3.1. Mục tiêu định tính

| # | Mục tiêu nghiệp vụ | Giải quyết vấn đề | Nhãn | Căn cứ |
| :--- | :--- | :---: | :--- | :--- |
| **G-01** | **Giảm thất thoát thẻ** — mọi thẻ báo mất/hỏng đều được ghi nhận trong hệ thống và xử lý qua cơ chế đền bù có chứng từ. | P-01 | **[SUY LUẬN]** | Toàn bộ III.4 |
| **G-02** | **Minh bạch truy vết** — bất kỳ mã thẻ nào cũng tra được kho nguồn, nhân viên xuất, người nhận và mốc thời gian xuất/nhận. | P-02 | **[SUY LUẬN]** | III.4, d.134–138 |
| **G-03** | **Chuẩn hóa và siết kiểm soát phê duyệt** — mọi Đơn xuất thẻ đều đi qua 2 cấp duyệt và để lại dấu vết đầy đủ trong nhật ký hệ thống. | P-03 | **[SUY LUẬN]** | BR-01 + yêu cầu Audit Log (IV.1) |
| **G-04** | **Giảm tranh chấp giao nhận** — ảnh chụp lô hàng thực tế và Biên bản Bàn giao tự động trở thành bằng chứng đối chứng. | P-04 | **[SUY LUẬN]** | III.3 |
| **G-05** | **Rút ngắn thời gian tra cứu thông tin thẻ** — tra cứu trực tiếp trên hệ thống thay vì lục tìm thủ công. | P-02 | **[SUY LUẬN]** từ chỉ tiêu **[SRS]** | IV.2, d.168 (tra cứu ≤ 2 giây) |

### 3.2. Chỉ tiêu định lượng (KPI)

| Hạng mục | Giá trị | Ghi chú |
| :--- | :--- | :--- |
| KPI giảm thất thoát thẻ | `TBD` | **Q-29** |
| KPI rút ngắn thời gian chu trình xuất kho | `TBD` | **Q-29** |
| KPI thời gian truy vết một mã thẻ | `TBD` | **Q-29** |
| Ngân sách / ROI kỳ vọng | `TBD` | **Q-29** |
| Quy mô kinh doanh (số đại lý, sản lượng thẻ/tháng) | `TBD` | **Q-07** |

> 🔴 **SRS không chứa bất kỳ KPI, chỉ tiêu định lượng, ngân sách hay ROI nào.** Toàn bộ mục 3.2 phụ thuộc câu trả lời của khách hàng cho **Q-29** (định nghĩa thành công) và **Q-07** (quy mô). Đội phân tích **không điền số phỏng đoán** — một chỉ tiêu bịa ra sẽ trở thành căn cứ nghiệm thu sai lệch.

---

## 4. Phạm vi

### 4.1. Trong phạm vi (In Scope)

| # | Hạng mục nghiệp vụ | Nhãn |
| :--- | :--- | :--- |
| S-01 | Tạo và quản lý **Đơn xuất thẻ** từ Sale/Đại lý (chọn loại thẻ, số lượng). | **[SRS]** |
| S-02 | **Luồng phê duyệt 2 cấp**: Nhân viên Kho soát xét & điều chỉnh → Admin phê duyệt cuối. | **[SRS]** |
| S-03 | Phát hiện và xử lý **đơn trùng lặp**. | **[SRS]** |
| S-04 | **Theo dõi vận chuyển** — kết nối với đơn vị vận chuyển đối tác, hiển thị trạng thái và mã vận đơn. | **[SRS]** |
| S-05 | **Nghiệm thu & đối soát khi nhận hàng** — ảnh chụp lô hàng bắt buộc, đối soát dải Series. | **[SRS]** |
| S-06 | **Tự động sinh Biên bản Bàn giao Thẻ**. | **[SRS]** |
| S-07 | **Truy xuất nguồn gốc thẻ** — tra mã thẻ ra kho xuất, người xuất, người nhận, mốc thời gian. | **[SRS]** |
| S-08 | **Quản lý thất thoát và đền bù thẻ mất/hỏng**. | **[SRS]** |
| S-09 | **Quản lý Danh mục kho** (thông tin kho, người phụ trách, liên hệ). | **[SRS]** |
| S-10 | **Tìm kiếm và lọc nâng cao** theo mã thẻ, dải Series, nhân sự, thời gian, trạng thái, kho, đại lý. | **[SRS]** |
| S-11 | **Phân quyền theo vai trò** cho 3 nhóm người dùng. | **[SRS]** |
| S-12 | **Nhật ký hệ thống (Audit Log)** ghi nhận toàn bộ lịch sử tác động dữ liệu. | **[SRS]** |

### 4.2. Ngoài phạm vi (Out of Scope)

> ⚠️ **Lưu ý về căn cứ**: SRS **không có mục "ngoài phạm vi"**. Danh sách dưới đây là **[SUY LUẬN]** — suy ra từ việc SRS hoàn toàn không nhắc tới các hạng mục này, và cần khách hàng **xác nhận lại** để tránh hiểu nhầm về sau.

| # | Hạng mục | Nhãn | Ghi chú |
| :--- | :--- | :--- | :--- |
| O-01 | Thanh toán trực tuyến qua cổng thanh toán / ví điện tử cho khoản đền bù thẻ mất. | **[SUY LUẬN]** | Chờ xác nhận **Q-04**. Nếu khách hàng chọn thanh toán online, hạng mục này chuyển vào phạm vi và khối lượng công việc tăng đáng kể. |
| O-02 | Ứng dụng cài đặt riêng trên iOS/Android. | **[SUY LUẬN]** | Chờ xác nhận **Q-23**. |
| O-03 | Theo dõi thẻ sau khi Đại lý đã bán cho khách hàng cuối. | **[SUY LUẬN]** | SRS không nhắc tới khách hàng cuối ở bất kỳ đâu. Chờ xác nhận **Q-16**. |
| O-04 | Quản lý công nợ / hạn mức tín dụng của Đại lý. | **[SUY LUẬN]** | SRS không nhắc tới. |
| O-05 | Đăng nhập bằng tài khoản công ty có sẵn (SSO) và xác thực 2 lớp. | **[SUY LUẬN]** | Chờ xác nhận **Q-14**. |

### 4.3. Phạm vi chưa xác định (Undetermined Scope)

> 🔴 **Đây là điểm cần khách hàng quyết định trước tiên.** Không chốt được mục này thì không thể chốt được khối lượng công việc và chi phí của toàn dự án.

**Vấn đề: Hệ thống có bao gồm luồng NHẬP KHO hay không?**

SRS đang tự mâu thuẫn về phạm vi ở hai chỗ:

| Mã | Vị trí mâu thuẫn | Nội dung |
| :--- | :--- | :--- |
| **C-01** | Tiêu đề SRS (d.11–12) **vs** toàn bộ nội dung mục II & III | Tiêu đề ghi *"HỆ THỐNG QUẢN LÝ **XUẤT NHẬP KHO** & PHÂN PHỐI THẺ VETC"*, nhưng mục II chỉ có *"QUY TRÌNH NGHIỆP VỤ **XUẤT THẺ**"* và toàn bộ mục III **không có một dòng nào** về việc nhập thẻ về kho. **Phạm vi theo tên gọi ≠ phạm vi theo nội dung.** |
| **C-02** | Tiêu đề mục III.1 (d.118) **vs** nội dung ngay dưới (d.119) | Tiêu đề mục ghi *"Quản lý Yêu cầu **Xuất / Nhập** Kho"*, dòng ngay dưới ghi *"Cho phép Sale/Đại lý chọn loại thẻ, số lượng cần **nhập**"*, trong khi dòng d.121 lại ghi *"Chỉnh sửa số lượng **xuất**"*. Chữ "nhập" ở đây nhập nhằng giữa nghĩa **nhập liệu** và nghĩa **nhập kho**. |

**Hệ quả nghiệp vụ nếu không chốt sớm:**

- SRS yêu cầu Nhân viên Kho *"kiểm tra tồn kho"* trước khi duyệt đơn, nhưng **không nơi nào trong SRS mô tả tồn kho từ đâu mà có**. Câu hỏi *"kho còn bao nhiêu thẻ?"* hiện **chưa có lời đáp**.
- SRS yêu cầu *"chặn chọn dải Series bị trùng lặp"*, nhưng muốn chặn trùng thì hệ thống phải nắm được toàn bộ danh sách Series đang có trong kho — mà danh sách đó chỉ hình thành khi có luồng nhập kho.
- Bốn vấn đề **Q-01 → Q-26 → Q-06 → chặn trùng Series** là **một khối liên đới**. Khách hàng trả lời Q-01 khác đi thì cả khối phải thiết kế lại.

| Trạng thái quyết định | Chờ trả lời **Q-01** |
| :--- | :--- |
| **Phương án đội đang tạm áp dụng** | Giai đoạn 1 chỉ làm luồng **XUẤT**; tồn kho khởi tạo bằng nhập từ file Excel một lần; luồng nhập kho đầy đủ đưa vào giai đoạn 2. |
| **Câu hỏi liên đới** | **Q-26** (nguồn dữ liệu tồn kho), **Q-06** (cách gán dải Series) |

---

## 5. Các bên liên quan

### 5.1. Các bên liên quan đã được SRS xác định

| Bên liên quan | Vai trò nghiệp vụ | Nhãn | Căn cứ |
| :--- | :--- | :--- | :--- |
| **Admin (Quản trị viên)** | Phê duyệt cuối cùng Đơn xuất thẻ; quản lý danh mục (kho, nhân sự); giám sát toàn bộ luồng dữ liệu; xem báo cáo tổng hợp. | **[SRS]** | d.41 |
| **Nhân viên Kho** | Tiếp nhận yêu cầu; kiểm tra tồn kho; điều chỉnh số lượng xuất; chọn kho xuất hàng; quản lý thất thoát; cập nhật danh mục kho. | **[SRS]** | d.42 |
| **Nhân viên Sale / Đại lý** | Tạo Đơn xuất thẻ; theo dõi trạng thái đơn; xác nhận nhận hàng kèm hình ảnh chứng minh; tra cứu thẻ. | **[SRS]** | d.43 |
| **Đơn vị Vận chuyển** | Bên **ngoài hệ thống**: tiếp nhận đơn và phản hồi thông tin theo dõi hành trình. Không thuộc 3 nhóm người dùng có tài khoản. | **[SRS]** | d.59, d.75–79 |

> ⚠️ **Rủi ro nghiệp vụ tại nhóm "Sale / Đại lý"**: SRS gộp **Nhân viên Sale** (người nội bộ) và **Đại lý** (đối tác bên ngoài) thành **một vai trò duy nhất**. Đây là hai đối tượng có mức độ tin cậy và trách nhiệm đền bù khác nhau căn bản. Chờ trả lời **Q-21**.

### 5.2. Các bên liên quan còn thiếu

| Bên liên quan | Vì sao cần | Trạng thái |
| :--- | :--- | :--- |
| **Nhà cung cấp thẻ VETC** | Tiêu đề SRS có chữ "Nhập Kho" nhưng không có bên nào chịu trách nhiệm cung cấp thẻ về kho. | `TBD` — **Q-01** |
| **Kế toán / Tài chính** | SRS có chức năng "nộp tiền đền bù" nhưng **không chỉ định ai** là người xác nhận đã nhận đủ tiền. | `TBD` — **Q-04**, **Q-22** |

---

## 6. Quy trình nghiệp vụ

### 6.1. Luồng xử lý một Đơn xuất thẻ — 5 bước **[SRS]**

| Bước | Người thực hiện | Hoạt động nghiệp vụ | Kết quả |
| :---: | :--- | :--- | :--- |
| **1** | Sale / Đại lý | Lập Đơn xuất thẻ: chọn loại thẻ và số lượng cần nhận. | Đơn ở tình trạng **Chờ kho duyệt**. |
| **2** | Nhân viên Kho | Kiểm tra tồn kho và soát xét đơn. Có hai hướng xử lý: **(a) Từ chối** nếu đơn trùng lặp/không hợp lệ; **(b) Duyệt** — được phép điều chỉnh số lượng (bắt buộc ghi lý do) và gán kho xuất hàng. | Nếu duyệt: đơn ở tình trạng **Chờ Admin duyệt**. |
| **3** | Admin | Kiểm tra và ra quyết định phê duyệt cuối cùng. | Đơn ở tình trạng **Chờ vận chuyển**. |
| **4** | Hệ thống ↔ Đơn vị Vận chuyển | Đơn được chuyển sang đơn vị vận chuyển; hệ thống cập nhật vị trí và trạng thái hành trình. | Đơn ở tình trạng **Đang vận chuyển**. |
| **5** | Sale / Đại lý | Khi nhận hàng: chụp ảnh lô thẻ thực tế tải lên hệ thống, đối soát đúng số lượng và đúng dải Series do kho cấp, bấm **[Hoàn thành đơn hàng]**. | Đơn ở tình trạng **Hoàn thành**; hệ thống tự động sinh Biên bản Bàn giao Thẻ. |

### 6.2. ⚠️ Cảnh báo nghiệp vụ: SRS chỉ mô tả trường hợp thuận lợi

**SRS mô tả quy trình như một đường thẳng một chiều, mặc định mọi bước đều thành công.** Toàn bộ các tình huống thực tế phát sinh hàng ngày đều **chưa được định nghĩa**:

| Tình huống thực tế | Tình trạng trong SRS | Chờ trả lời |
| :--- | :--- | :--- |
| Nhân viên Kho từ chối đơn thì đơn đi về đâu? | Sơ đồ có nhánh "Từ chối đơn" nhưng **bỏ trống** không gán tình trạng nào. | **Q-09** |
| Admin có được từ chối không? | **Hoàn toàn không có** nhánh Admin từ chối. Một cấp phê duyệt không có quyền chặn thì việc duyệt 2 cấp mất ý nghĩa kiểm soát. | **Q-10** |
| Sale nhận thiếu thẻ hoặc lệch dải Series? | **Không có.** Bước 5 chỉ có đường "xác nhận đúng". | **Q-11** |
| Sale muốn hủy đơn gửi nhầm? | **Không có** khái niệm hủy đơn ở bất kỳ giai đoạn nào. | **Q-24** |
| Giao hàng thất bại, thẻ hoàn về kho? | **Không có.** Đơn sẽ kẹt vĩnh viễn ở tình trạng "Đang vận chuyển", trong khi số thẻ vẫn bị tính là đã xuất kho. | **Q-25** |

> 📌 **Nghịch lý nghiệp vụ đáng lưu ý nhất (mã C-14)**: SRS xây dựng hẳn một nhóm chức năng để **xử lý hậu quả** của thất thoát thẻ, nhưng quy trình nghiệm thu lại **không có bước nào để phát hiện ra thất thoát**. Nếu Sale nhận thiếu 10 thẻ, hệ thống hiện tại không cho họ cách nào để báo — hoặc buộc phải bấm "Hoàn thành" (mất trắng 10 thẻ, không ai chịu trách nhiệm), hoặc để đơn treo vô thời hạn.

---

## 7. Quy tắc nghiệp vụ

> Đây là các quy tắc **bắt buộc (MUST)** mà hệ thống phải thực thi. Toàn bộ 10 quy tắc đều có căn cứ trực tiếp trong SRS.

| # | Quy tắc nghiệp vụ | Nhãn | Nguồn trong SRS |
| :--- | :--- | :--- | :--- |
| **BR-01** | Luồng phê duyệt **2 cấp là bắt buộc**: Kho duyệt → Admin duyệt. Không được bỏ qua cấp nào. | **[SRS]** | III.1 (d.122); II (d.49) |
| **BR-02** | Khi Nhân viên Kho sửa *Số lượng duyệt* khác *Số lượng yêu cầu* → **bắt buộc nhập lý do ghi chú**. | **[SRS]** | III.1 (d.121); II (d.94) |
| **BR-03** | Khi nhận hàng, Sale/Đại lý **bắt buộc đính kèm tối thiểu 01 ảnh** chụp lô thẻ thực tế. | **[SRS]** | III.3 (d.129) |
| **BR-04** | Đơn xuất thẻ chỉ được chuyển sang **Hoàn thành** sau khi Sale xác nhận **đúng số lượng VÀ đúng dải Series** do kho cấp. | **[SRS]** | II Bước 5 (d.110) |
| **BR-05** | Biên bản Bàn giao Thẻ được sinh **tự động ngay khi** bấm [Hoàn thành]. | **[SRS]** | III.3 (d.131) |
| **BR-06** | Mọi tác động lên dữ liệu phải được ghi vào nhật ký hệ thống: ai tạo, ai sửa số lượng, ai duyệt, kèm mốc thời gian cụ thể. | **[SRS]** | IV.1 (d.164) |
| **BR-07** | Hệ thống **chặn nhập số lượng âm** và **chặn chọn dải Series bị trùng lặp**. | **[SRS]** | IV.2 (d.167) |
| **BR-08** | Thẻ báo mất sau khi hoàn tất đền bù → hệ thống **tự động** cập nhật tình trạng thành `Báo mất - Đã đền bù`. | **[SRS]** | III.4 (d.142) |
| **BR-09** | Đơn xuất thẻ phải được gán **một kho xuất** lấy từ Danh mục kho trước khi chuyển sang cấp duyệt thứ hai. | **[SRS]** | II Bước 2 (d.95) |
| **BR-10** | Đơn trùng lặp gửi "trong thời gian ngắn" → hệ thống **cảnh báo hoặc** cho Nhân viên Kho từ chối nhanh. | **[SRS]** *nhưng mơ hồ* | III.1 (d.120) — ⚠️ SRS **không định nghĩa** thế nào là "trùng lặp" và **không định lượng** "thời gian ngắn". Chờ **Q-05**, **Q-17**. |

---

## 8. Ràng buộc & Giả định

### 8.1. Ràng buộc nghiệp vụ đã xác định

| # | Ràng buộc | Nhãn | Căn cứ |
| :--- | :--- | :--- | :--- |
| R-01 | Hệ thống phải phân quyền chặt chẽ theo vai trò cho **3 nhóm người dùng**. | **[SRS]** | I (d.37); IV.1 (d.162) |
| R-02 | Toàn bộ dữ liệu nhạy cảm phải được mã hóa; truyền tải bắt buộc qua giao thức an toàn. | **[SRS]** | IV.1 (d.163) |
| R-03 | Việc theo dõi vận chuyển phụ thuộc vào **đơn vị vận chuyển đối tác đã ký hợp đồng** — đây là phụ thuộc **ngoài tầm kiểm soát** của đội triển khai. | **[SRS]** | III.2 (d.125) — danh tính đối tác: **Q-02** |
| R-04 | Tra cứu / tìm kiếm mã thẻ phải phản hồi trong **≤ 2 giây**. | **[SRS]** | IV.2 (d.168) |
| R-05 | Dữ liệu phải được **tự động sao lưu hàng ngày**. | **[SRS]** | IV.2 (d.169) |

### 8.2. Ràng buộc chưa xác định

| Hạng mục | Trạng thái | Chờ trả lời |
| :--- | :--- | :--- |
| **Ngân sách dự án** | `TBD` | **Q-29** |
| **Mốc thời gian go-live / deadline bắt buộc** | `TBD` | **Q-30** |
| **Ràng buộc pháp lý & tuân thủ ngành ETC** | `TBD` | **Q-08** |
| **Nghĩa vụ lưu trữ chứng từ giao nhận theo luật kế toán** | `TBD` | **Q-08** |
| **Yêu cầu dữ liệu phải đặt tại Việt Nam** | `TBD` | **Q-13** |
| **Quy mô sử dụng** (số người dùng, số đơn/ngày, số kho) | `TBD` | **Q-07** |
| **Kế hoạch chuyển đổi dữ liệu cũ và đào tạo người dùng** | `TBD` | **Q-30** |

### 8.3. Giả định đang áp dụng

> Các giả định dưới đây là **phương án tạm** để đội tiếp tục công việc, **không phải cam kết**. Danh sách đầy đủ 31 giả định kèm hệ quả nếu khách hàng trả lời khác nằm tại mục "Giả định thiết kế" của [PRD-VETC](../PRD-VETC.md).

| # | Giả định nghiệp vụ | Chờ xác nhận |
| :--- | :--- | :--- |
| A-01 | Giai đoạn 1 chỉ triển khai luồng **xuất kho**; luồng nhập kho đưa vào giai đoạn sau. | **Q-01** |
| A-02 | Việc đền bù thẻ mất được **ghi nhận thủ công** (chuyển khoản bên ngoài, hệ thống lưu chứng từ), không tích hợp cổng thanh toán. | **Q-04** |
| A-03 | Sale/Đại lý **chỉ xem được đơn của chính mình**; Nhân viên Kho chỉ xử lý đơn thuộc kho mình phụ trách. | **Q-12** |
| A-04 | Cả Nhân viên Kho và Admin đều **có quyền từ chối** đơn, bắt buộc kèm lý do. | **Q-09**, **Q-10** |
| A-05 | Bổ sung luồng **báo sai lệch** khi Sale nhận thiếu/lệch Series, tự động sinh bản ghi thất thoát. | **Q-11** |
| A-06 | Hệ thống chạy trên **nền web hiển thị tốt trên điện thoại**, không làm ứng dụng cài đặt riêng. | **Q-23** |

---

## 9. Rủi ro nghiệp vụ

### 9.1. Rủi ro lớn nhất: 11 quyết định nghiệp vụ chưa được chốt

Bước rà soát SRS đã phát hiện **31 điểm cần làm rõ**, trong đó **11 điểm ở mức Cần gấp (Blocker)** — nghĩa là chưa có câu trả lời thì không thể bắt đầu thiết kế phần lõi của hệ thống.

| Mã | Nội dung cần khách hàng quyết định | Rủi ro nghiệp vụ nếu chốt muộn |
| :--- | :--- | :--- |
| **Q-01** | Hệ thống có quản lý cả việc nhận thẻ từ nhà cung cấp về kho không? | Rủi ro **cao nhất**. Quyết định muộn → phải làm lại toàn bộ cách hệ thống quản lý tồn kho và dải Series. Kéo theo Q-06 và Q-26. |
| **Q-02** | Đơn vị vận chuyển đang hợp tác là bên nào? | Không biết đối tác thì không ước lượng được công việc kết nối. Nhiều đơn vị vận chuyển chỉ cho tra cứu, không cho tạo đơn tự động → cách làm phải khác đi. |
| **Q-03** | Thông tin vận chuyển cần cập nhật nhanh đến mức nào? | Ảnh hưởng trực tiếp tới chi phí vận hành hàng tháng và có thể vượt giới hạn mà đối tác cho phép. |
| **Q-04** | Đền bù thẻ mất: thanh toán online hay ghi nhận thủ công? | Chênh lệch khối lượng công việc rất lớn giữa hai phương án. Đoán sai dẫn tới vỡ dự toán và vỡ tiến độ. |
| **Q-05** | Định nghĩa thế nào là hai đơn trùng nhau? | Không có định nghĩa thì không xây được quy tắc. Đặt sai ngưỡng → chặn nhầm đơn hợp lệ của đại lý lớn, hoặc bỏ lọt lỗi bấm nhầm. |
| **Q-06** | Dải Series được gán vào đơn lúc nào, do ai? | Đây là mắt xích nối đơn hàng với thẻ vật lý. Sai mắt xích này thì **toàn bộ mục tiêu truy vết (G-02) không đạt được**. |
| **Q-09** | Đơn bị Nhân viên Kho từ chối thì đi về đâu? | Đơn "biến mất" khỏi màn hình, Sale không biết vì sao bị từ chối và phải nhập lại từ đầu → mất dấu vết và mất thời gian vận hành. |
| **Q-10** | Admin có quyền từ chối không? | Nếu không có, cấp phê duyệt cuối trở thành nút bấm hình thức và **mục tiêu G-03 (siết kiểm soát) thất bại**. |
| **Q-11** | Nhận thiếu / lệch Series thì xử lý ra sao? | Không có luồng này thì hệ thống **không phát hiện được thất thoát** — mâu thuẫn trực tiếp với mục tiêu G-01, lý do chính khiến dự án ra đời. |
| **Q-12** | Ai được xem dữ liệu của ai? | Rủi ro **rò rỉ dữ liệu kinh doanh**: Đại lý có thể nhìn thấy sản lượng và đơn hàng của các đại lý khác. Sửa sau rất tốn kém. |
| **Q-21** | "Nhân viên Sale" và "Đại lý" là một hay hai nhóm? | Cho người nội bộ và đối tác bên ngoài chung một mức quyền là rủi ro bảo mật. Trách nhiệm đền bù của hai nhóm cũng khác nhau. |

### 9.2. Rủi ro nghiệp vụ khác

| # | Rủi ro | Mức | Ghi chú |
| :--- | :--- | :---: | :--- |
| RK-01 | **Phụ thuộc bên thứ ba**: khả năng kết nối với đơn vị vận chuyển nằm ngoài tầm kiểm soát của đội triển khai. | 🔴 Cao | Chờ **Q-02** |
| RK-02 | **Không có tiêu chí nghiệm thu định lượng**: dự án không có căn cứ chung để hai bên tuyên bố thành công. | 🔴 Cao | Chờ **Q-29** |
| RK-03 | **Phình phạm vi (scope creep) ở hạng mục "báo cáo tổng hợp"**: SRS hứa chức năng này nhưng không mô tả nội dung. | 🟡 Trung bình | Chờ **Q-28** |
| RK-04 | **Không đo được chỉ tiêu tra cứu ≤ 2 giây** vì chưa biết quy mô dữ liệu và số người dùng đồng thời. | 🟡 Trung bình | Chờ **Q-07** |
| RK-05 | **Bước nhận hàng có thể không dùng được trên thực tế** nếu hệ thống chỉ tối ưu cho màn hình máy tính. | 🟡 Trung bình | Chờ **Q-23** |
| RK-06 | **Chưa có ngôn ngữ chung (Ubiquitous Language)**: SRS gọi cùng một khái niệm bằng nhiều tên khác nhau (mã C-18), dễ gây hiểu nhầm giữa các bên. | 🟡 Trung bình | Tài liệu này đã chuẩn hóa dùng **"Đơn xuất thẻ"**. |

---

## 10. Tiêu chí thành công

| Hạng mục | Giá trị | Ghi chú |
| :--- | :--- | :--- |
| Định nghĩa "dự án thành công" sau 6 tháng vận hành | `TBD` | **Q-29** |
| Chỉ tiêu giảm thất thoát thẻ | `TBD` | **Q-29** |
| Chỉ tiêu rút ngắn thời gian chu trình xuất kho | `TBD` | **Q-29** |
| Chỉ tiêu thời gian truy vết một mã thẻ | `TBD` | **Q-29** |
| Mức độ chấp nhận của người dùng (tỷ lệ sử dụng thực tế) | `TBD` | **Q-29**, **Q-30** |

> 🔴 **SRS không chứa bất kỳ tiêu chí thành công nào.** Mục này **không thể hoàn thiện** nếu thiếu câu trả lời cho **Q-29**.
>
> **Khuyến nghị của Business Analyst**: đây là câu hỏi mà đội triển khai **không thể trả lời thay khách hàng**. Nếu không chốt được, hai bên sẽ bước vào giai đoạn nghiệm thu mà không có căn cứ chung để khẳng định dự án đã đạt mục tiêu hay chưa — rủi ro tranh chấp nghiệm thu là rất cao. Đề nghị ưu tiên trả lời **Q-29** ngay cả khi nó được xếp ở nhóm "Nên có" trong danh sách câu hỏi.

---

## 11. Tài liệu liên quan

| Tài liệu | Quan hệ | Mô tả |
| :--- | :--- | :--- |
| [SRS-VETC](../SRS-VETC.md) | **Detailed spec** | Tài liệu mô tả yêu cầu phần mềm — nguồn sự thật gốc của BRD này. |
| [PRD-VETC](../PRD-VETC.md) | **Product spec** | Tài liệu yêu cầu sản phẩm — chi tiết hóa BRD này thành 25 yêu cầu chức năng và 7 yêu cầu phi chức năng cho đội phát triển. |
| [Analysis-Open-Questions-VETC](../../050-Research/Analysis-Open-Questions-VETC.md) | **Open questions** | Danh sách 31 điểm cần khách hàng làm rõ — nguồn của toàn bộ mã `Q-NN` được trích dẫn trong tài liệu này. |

---

*Tài liệu được chuẩn hóa và quản lý bởi TNMCORE-OS.*

---
id: ANALYSIS-OQ-VETC
type: analysis
status: draft
project: VETC
owner: "@trisjr"
created: 2026-08-19
updated: 2026-08-19
---

# 📋 CÁC ĐIỂM CẦN LÀM RÕ — HỆ THỐNG QUẢN LÝ XUẤT KHO & PHÂN PHỐI THẺ VETC

## 📑 Mục lục

- [1. Lời mở đầu](#1-lời-mở-đầu)
- [2. Hướng dẫn cách trả lời](#2-hướng-dẫn-cách-trả-lời)
- [3. Phần A — 11 câu CẦN GẤP](#3-phần-a--11-câu-cần-gấp)
- [4. Phần B — 11 câu Quan trọng](#4-phần-b--11-câu-quan-trọng)
- [5. Phần C — 9 câu Nên có](#5-phần-c--9-câu-nên-có)
- [6. Bảng tổng hợp để tick](#6-bảng-tổng-hợp-để-tick)
- [7. Tài liệu liên quan](#7-tài-liệu-liên-quan)

---

## 1. Lời mở đầu

Kính gửi anh/chị,

Sau khi đọc kỹ tài liệu mô tả yêu cầu phần mềm mà anh/chị đã gửi, đội phát triển đã tổng hợp lại **31 điểm cần được làm rõ thêm** trước khi bắt tay vào thiết kế và lập trình.

Đây **không phải** là những chỗ tài liệu viết sai. Đây là những chỗ tài liệu **chưa nói tới** hoặc **có thể hiểu theo nhiều cách khác nhau** — mà mỗi cách hiểu lại dẫn tới một cách xây dựng hệ thống khác nhau về chi phí và thời gian.

Mục đích của tài liệu này rất đơn giản: **hỏi trước còn hơn làm sai rồi sửa**. Một câu trả lời của anh/chị hôm nay có thể tiết kiệm được nhiều tuần làm lại về sau.

Anh/chị **trả lời được bao nhiêu thì chúng em làm rõ được bấy nhiêu** — không cần phải trả lời hết một lượt. Những câu chưa có câu trả lời, đội phát triển vẫn tiếp tục công việc theo phương án tạm thời đã ghi sẵn bên dưới mỗi câu.

---

## 2. Hướng dẫn cách trả lời

Mỗi câu hỏi trong tài liệu này được trình bày theo cùng một khuôn:

| Thành phần | Ý nghĩa |
| :--- | :--- |
| **Mã câu hỏi (Q-NN)** | Mã để hai bên tiện đối chiếu. Khi trao đổi qua điện thoại hay email, anh/chị chỉ cần nhắc mã này. |
| **Bối cảnh** | Giải thích ngắn gọn: tài liệu hiện có nói gì và còn thiếu gì. |
| **Câu hỏi** | Nội dung đội phát triển cần anh/chị xác nhận. |
| **Phương án đội đang tạm dùng** | Nếu anh/chị chưa trả lời, đội sẽ làm theo phương án này. |
| **Ô trả lời** | Chỗ để anh/chị điền. |

**Cách trả lời nhanh nhất:**

1. Đọc phần **"Phương án đội đang tạm dùng"**.
2. Nếu anh/chị **đồng ý** với phương án đó → chỉ cần ghi **`OK`** vào ô trả lời. Xong câu đó.
3. Nếu anh/chị **muốn khác** → mô tả lại bằng lời của anh/chị, không cần theo khuôn mẫu nào cả.
4. Nếu **chưa quyết định được** → ghi `Chưa rõ` hoặc `Cần hỏi lại nội bộ`, đội sẽ hẹn trao đổi trực tiếp.

**Thứ tự ưu tiên trả lời:**

| Phần | Mức độ | Số câu | Vì sao |
| :--- | :--- | :---: | :--- |
| **Phần A** | 🔴 Cần gấp | 11 | Chưa có câu trả lời thì đội **không thể** bắt đầu thiết kế phần lõi. |
| **Phần B** | 🟡 Quan trọng | 11 | Trả lời muộn vẫn kịp, nhưng sẽ phải sửa lại một phần công việc đã làm. |
| **Phần C** | 🟢 Nên có | 9 | Có thể trả lời dần trong quá trình triển khai. |

> 💡 Nếu thời gian eo hẹp, anh/chị chỉ cần ưu tiên **11 câu ở Phần A** trước là đã đủ để đội bắt đầu.

---

## 3. Phần A — 11 câu CẦN GẤP

> 🔴 Đây là 11 câu quyết định cách xây dựng phần lõi của hệ thống. Rất mong anh/chị ưu tiên trả lời nhóm này trước.

### Q-01 · Hệ thống có quản lý cả việc nhận thẻ từ nhà cung cấp về kho không?

- **Bối cảnh**: Tên hệ thống trong tài liệu hiện có ghi là "Quản lý **Xuất Nhập Kho**", nhưng toàn bộ nội dung mô tả bên trong lại chỉ nói về việc **xuất thẻ từ kho giao cho Sale/Đại lý**. Tài liệu chưa nói rõ thẻ **từ nhà cung cấp về kho** thì được ghi nhận vào hệ thống bằng cách nào và ai làm việc đó. Đây là câu hỏi ảnh hưởng rộng nhất trong toàn bộ danh sách, vì nó quyết định hệ thống có biết được "trong kho còn bao nhiêu thẻ" hay không.

  *(Trong câu hỏi bên dưới có nhắc tới **API** — đây là cách hai phần mềm tự trao đổi dữ liệu với nhau mà không cần người gõ tay.)*

- **Câu hỏi**: *"Hệ thống có cần quản lý cả việc **nhập thẻ từ nhà cung cấp về kho** không, hay chỉ quản lý việc **xuất thẻ từ kho giao cho Sale/Đại lý**? Nếu có nhập kho: ai là người tạo phiếu nhập, cần duyệt mấy cấp, và số lượng thẻ tồn kho ban đầu sẽ được đưa vào hệ thống bằng cách nào (nhập tay, import Excel, hay nối API với nhà cung cấp)?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Phase 1 *(giai đoạn 1)* **chỉ làm luồng XUẤT**. Tồn kho khởi tạo bằng **import Excel một lần** *(đưa dữ liệu sẵn có từ file Excel vào hệ thống)* do Admin/NV Kho thực hiện. Luồng nhập kho đầy đủ đưa vào Phase 2 *(giai đoạn 2)*. Đổi tên hệ thống trong tài liệu thành "Quản lý Xuất Kho & Phân phối Thẻ VETC" cho khớp phạm vi thực.

> **Trả lời của khách hàng:** ______

---

### Q-02 · Đơn vị vận chuyển đang hợp tác là bên nào?

- **Bối cảnh**: Tài liệu hiện có nói hệ thống sẽ kết nối tự động với đơn vị vận chuyển đối tác "**đã ký hợp đồng**", nhưng chưa nói rõ đó là đơn vị nào. Mỗi đơn vị vận chuyển có cách kết nối kỹ thuật khác nhau, và một số đơn vị chỉ cho phép **tra cứu** đơn chứ **không cho tạo đơn tự động** — nếu rơi vào trường hợp đó thì cách làm sẽ phải khác đi.

  *(**API** = cách hai phần mềm tự trao đổi dữ liệu với nhau. **Tài liệu API** là bản hướng dẫn kỹ thuật do bên vận chuyển cung cấp để đội đấu nối. **Sandbox** là môi trường chạy thử, không ảnh hưởng dữ liệu thật.)*

- **Câu hỏi**: *"Đơn vị vận chuyển đang ký hợp đồng là bên nào (Viettel Post / GHN / GHTK / J&T / khác)? Anh/chị đã có **tài liệu API** và **tài khoản môi trường test (sandbox)** từ họ chưa? Nếu có, vui lòng gửi kèm. Nếu chưa có API, hệ thống sẽ tạm cho NV Kho **nhập tay mã vận đơn** — anh/chị có chấp nhận phương án này cho giai đoạn đầu không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Thiết kế tầng tích hợp theo mô hình **adapter/plugin** *(một lớp kết nối trung gian, giúp sau này đổi sang đơn vị vận chuyển khác mà không phải viết lại hệ thống)*, giai đoạn 1 chạy **adapter thủ công** *(nghĩa là chưa nối tự động)*: NV Kho nhập mã vận đơn và cập nhật trạng thái tay. Khi có tài liệu kết nối kỹ thuật từ bên vận chuyển thì cắm phần nối tự động vào, không đổi nghiệp vụ.

> **Trả lời của khách hàng:** ______

---

### Q-03 · Thông tin vận chuyển cần cập nhật nhanh đến mức nào?

- **Bối cảnh**: Tài liệu hiện có nói hệ thống cập nhật vị trí đơn hàng "**theo thời gian thực**", nhưng chưa nói rõ "thời gian thực" ở đây là bao lâu. Cập nhật càng dày thì chi phí vận hành càng cao, và một số đơn vị vận chuyển còn giới hạn số lần được hỏi trong ngày. Biết được mức độ anh/chị thực sự cần sẽ giúp cân đối chi phí hợp lý.

- **Câu hỏi**: *"Với việc theo dõi vận chuyển, **độ trễ bao nhiêu là chấp nhận được** đối với anh/chị: cập nhật gần như tức thì (dưới 1 phút), mỗi 15 phút, mỗi 1 giờ, hay chỉ cần 2–3 lần/ngày là đủ? Và bên vận chuyển có hỗ trợ **tự động bắn thông báo về hệ thống** (webhook) không, hay hệ thống của mình phải **chủ động hỏi** họ định kỳ?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: "Real-time" hiểu là **polling định kỳ mỗi 15 phút** *(hệ thống chủ động hỏi bên vận chuyển 15 phút một lần)* cho các đơn đang ở tình trạng `In Transit` *(Đang vận chuyển)*; ưu tiên chuyển sang webhook *(bên vận chuyển tự bắn thông báo về)* nếu bên vận chuyển hỗ trợ. Ghi rõ trong tài liệu sản phẩm là giả định chờ xác nhận, **không** ghi thành cam kết.

> **Trả lời của khách hàng:** ______

---

### Q-04 · Tiền đền bù thẻ mất được nộp trực tiếp trên hệ thống hay chỉ ghi nhận lại?

- **Bối cảnh**: Tài liệu hiện có dùng từ "**tích hợp** chức năng nộp tiền đền bù", nghe như hệ thống sẽ có cổng thanh toán trực tuyến. Nhưng ngay sau đó lại liệt kê ba thông tin cần lưu là *số tiền, mã giao dịch, hóa đơn đính kèm* — đây lại là đặc trưng của việc ghi nhận lại một khoản đã nộp bên ngoài. Hai cách hiểu này chênh nhau rất lớn về thời gian và chi phí triển khai, nên rất cần anh/chị chốt giúp.

  *(**Upload** = tải tệp/ảnh từ máy tính hoặc điện thoại lên hệ thống.)*

- **Câu hỏi**: *"Khi Sale/Đại lý làm mất thẻ và phải đền bù: anh/chị muốn (A) người dùng **thanh toán trực tiếp trên hệ thống** qua cổng thanh toán/ví điện tử, hay (B) họ chuyển khoản/nộp tiền **bên ngoài** rồi kế toán chỉ **ghi nhận lại** số tiền, mã giao dịch và **upload ảnh chứng từ** vào hệ thống? **[Đề xuất: phương án B]** vì đúng với các trường dữ liệu mà tài liệu yêu cầu và nhanh hơn đáng kể. Ngoài ra, **ai** là người được phép xác nhận đã nhận đủ tiền đền bù?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: **Phương án B — ghi nhận thủ công**, đúng theo 3 thông tin mà tài liệu đã liệt kê. Không tích hợp cổng thanh toán trong phạm vi này. Người xác nhận: Admin.

> **Trả lời của khách hàng:** ______

---

### Q-05 · Thế nào là hai đơn bị coi là trùng nhau?

- **Bối cảnh**: Tài liệu hiện có yêu cầu hệ thống phát hiện các đơn trùng lặp gửi "**trong thời gian ngắn**", và cho một ví dụ duy nhất là "Sale bấm gửi 2 lần". Tuy nhiên tài liệu chưa nói rõ **bao lâu** thì gọi là "thời gian ngắn", và **giống nhau ở điểm nào** thì gọi là trùng. Đặt khoảng thời gian quá rộng sẽ chặn nhầm những đơn hợp lệ; quá hẹp thì không bắt được lỗi bấm nhầm.

- **Câu hỏi**: *"Hệ thống nên coi hai đơn là 'trùng lặp' khi nào? Ví dụ: **cùng một Sale + cùng loại thẻ + cùng số lượng** gửi trong vòng **bao nhiêu phút** (5 phút? 30 phút? trong cùng ngày?). Và trong thực tế, có trường hợp nào một Sale **cố ý** đặt 2 đơn giống hệt nhau trong thời gian ngắn mà vẫn là hợp lệ không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Trùng lặp = **cùng Sale + cùng loại thẻ + cùng số lượng + trong vòng 15 phút**. Hệ thống **cảnh báo** (không chặn cứng) cho cả Sale lúc gửi và NV Kho lúc duyệt; NV Kho toàn quyền quyết định.

> **Trả lời của khách hàng:** ______

---

### Q-06 · Dải số Series của thẻ được gán vào đơn lúc nào và do ai làm?

- **Bối cảnh**: Tài liệu hiện có nói dải số Series thẻ là "**do kho cấp**", nhưng phần mô tả các thao tác của Nhân viên Kho lại **không có bước nào** là gán Series. Vì vậy chưa rõ việc gán Series diễn ra ở bước nào và làm bằng cách nào. Đây là mắt xích nối giữa "đơn hàng trên hệ thống" và "thẻ thật ngoài đời" — toàn bộ khả năng truy vết nguồn gốc thẻ đều dựa vào mắt xích này.

- **Câu hỏi**: *"Dải số Series của thẻ được gán cho đơn hàng **vào lúc nào** và **do ai làm**? Cụ thể: (A) NV Kho **tự gõ tay** dải Series khi duyệt đơn, hay (B) **hệ thống tự động lấy** dải Series còn trống trong kho và gán vào đơn? **[Đề xuất: phương án B]** vì chỉ khi hệ thống nắm được danh sách Series đang có trong kho thì mới chặn được việc cấp trùng Series. Nếu chọn B, hệ thống cần biết trước toàn bộ Series đang tồn — anh/chị lấy dữ liệu này ở đâu?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: NV Kho gán dải Series **tại Bước 2** (cùng lúc gán kho + chốt số lượng duyệt), theo phương án **(B) hệ thống gợi ý dải liên tục còn trống, NV Kho xác nhận/điều chỉnh**; hệ thống tự động kiểm tra để không cấp trùng Series cho hai đơn khác nhau.

> **Trả lời của khách hàng:** ______

---

### Q-09 · Đơn bị Nhân viên Kho từ chối thì đi về đâu?

- **Bối cảnh**: Sơ đồ quy trình trong tài liệu hiện có có mô tả việc Nhân viên Kho "Từ chối đơn", nhưng khác với mọi bước còn lại, bước này **không ghi rõ đơn sẽ chuyển sang tình trạng nào**. Nếu không làm rõ, Sale sẽ không biết đơn của mình bị từ chối vì lý do gì, và có thể phải nhập lại từ đầu.

- **Câu hỏi**: *"Khi Nhân viên Kho **từ chối** một đơn: (1) Đơn đó nên **biến mất** hay vẫn **hiển thị trong danh sách của Sale** với nhãn 'Bị từ chối' kèm lý do? (2) Sale có được **sửa lại đơn và gửi lại** không, hay phải **tạo đơn hoàn toàn mới**? (3) NV Kho có **bắt buộc phải ghi lý do từ chối** không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Bổ sung tình trạng `Rejected (Bị từ chối)`. Đơn **vẫn hiển thị** cho Sale kèm **lý do bắt buộc**. Sale được **sao chép đơn cũ thành đơn mới** (không sửa trực tiếp đơn đã bị từ chối, để giữ nguyên vẹn audit trail *(nhật ký lưu vết ai đã làm gì, vào lúc nào)* theo yêu cầu ghi nhật ký hệ thống). `Rejected` là tình trạng **kết thúc**.

> **Trả lời của khách hàng:** ______

---

### Q-10 · Admin có được quyền từ chối đơn không?

- **Bối cảnh**: Tài liệu hiện có nhấn mạnh quy trình duyệt 2 cấp "nghiêm ngặt", nhưng ở cấp duyệt cuối cùng lại **chỉ mô tả hành động Duyệt**, không nói gì tới việc Admin có được Từ chối hay không. Trên thực tế, một cấp phê duyệt mà không có quyền chặn thì việc phê duyệt trở nên hình thức.

- **Câu hỏi**: *"Ở bước phê duyệt cuối, ngoài **Duyệt**, Admin có cần thêm quyền **Từ chối** đơn không? Nếu có: đơn bị Admin từ chối sẽ **quay lại cho Nhân viên Kho xem xét lại**, hay **đóng luôn** và báo về cho Sale? Ngoài ra, Admin có cần quyền **sửa lại số lượng** một lần nữa (khác với số lượng NV Kho đã duyệt) không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Admin **có** quyền Từ chối, **bắt buộc ghi lý do**, đơn chuyển sang `Rejected` và **báo về Sale** (không quay ngược về NV Kho, tránh vòng lặp duyệt vô tận). Admin **không** có quyền sửa số lượng (giữ nguyên tắc phân tách trách nhiệm: kho chốt số, admin chốt cho/không cho).

> **Trả lời của khách hàng:** ______

---

### Q-11 · Nhận hàng thiếu hoặc sai dải Series thì xử lý ra sao?

- **Bối cảnh**: Tài liệu hiện có mô tả bước nhận hàng theo hướng mọi việc đều suôn sẻ: Sale kiểm tra thấy **đúng** số lượng và **đúng** dải Series rồi bấm Hoàn thành. Tài liệu chưa nói tới trường hợp nhận **thiếu, thừa, hỏng, hoặc lệch Series**. Điều đáng lưu ý là hệ thống có hẳn một phần dành cho quản lý thất thoát thẻ — nhưng lại chưa có bước nào để **phát hiện ra thất thoát**.

- **Câu hỏi**: *"Khi Sale/Đại lý nhận hàng và phát hiện **thiếu thẻ** hoặc **dải Series không khớp** với thông tin trên hệ thống, quy trình xử lý hiện tại của công ty là gì? Cụ thể: (1) Sale có được bấm **'Báo sai lệch'** thay vì 'Hoàn thành' không? (2) **Ai** là người xử lý khiếu nại đó — NV Kho, Admin, hay bên vận chuyển? (3) Sau khi xử lý xong, đơn được **đóng với số lượng thực nhận**, hay kho phải **giao bù phần thiếu**?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Bổ sung nút **[Báo sai lệch]** ở Bước 5 → tình trạng `Discrepancy (Có sai lệch)`, bắt buộc Sale nhập số lượng thực nhận + ảnh + mô tả. Đơn chuyển về **NV Kho + Admin** cùng xử lý. Sau xử lý, đơn đóng với **số lượng thực nhận**; phần chênh lệch tự động sinh **bản ghi thất thoát** liên kết sang phần quản lý thất thoát thẻ.

> **Trả lời của khách hàng:** ______

---

### Q-12 · Ai được xem dữ liệu của ai?

- **Bối cảnh**: Tài liệu hiện có nói hệ thống phân quyền "chặt chẽ theo vai trò", và có liệt kê mỗi vai trò **làm được những việc gì**. Nhưng tài liệu chưa nói rõ mỗi người **được nhìn thấy dữ liệu của những ai**. Nếu không làm rõ, một Đại lý có thể nhìn thấy toàn bộ đơn hàng và sản lượng của các Đại lý khác — điều thường rất nhạy cảm về mặt kinh doanh.

- **Câu hỏi**: *"Về quyền xem dữ liệu: (1) Một nhân viên Sale/Đại lý có được xem đơn hàng của **Sale/Đại lý khác** không, hay chỉ xem được đơn của chính mình? (2) Nhân viên Kho chỉ được xử lý đơn thuộc **kho mình phụ trách**, hay xử lý được đơn của **mọi kho**? (3) Có cấp quản lý trung gian nào (Trưởng vùng, Quản lý Sale) cần xem dữ liệu của **cả một nhóm** Sale không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Sale/Đại lý **chỉ xem được đơn của chính mình**. NV Kho **chỉ xử lý đơn thuộc kho được gán phụ trách** (khớp với trường "Tên nhân viên kho phụ trách" trong danh mục kho). Admin xem toàn bộ. **Không** có cấp quản lý trung gian ở giai đoạn 1.

> **Trả lời của khách hàng:** ______

---

### Q-21 · "Nhân viên Sale" và "Đại lý" là cùng một nhóm hay hai nhóm khác nhau?

- **Bối cảnh**: Tài liệu hiện có gộp "Nhân viên Sale" và "Đại lý" thành **một vai trò duy nhất** trên hệ thống. Tuy nhiên hai đối tượng này thường rất khác nhau: nhân viên Sale là người trong công ty, còn Đại lý là đối tác bên ngoài. Việc cho hai đối tượng này chung một mức quyền có thể dẫn tới rủi ro lộ thông tin kinh doanh, và trách nhiệm khi làm mất thẻ cũng thường khác nhau.

- **Câu hỏi**: *"'Nhân viên Sale' và 'Đại lý' là **cùng một nhóm người** hay là **hai nhóm khác nhau**? Cụ thể: Đại lý là **công ty/cá nhân bên ngoài** ký hợp đồng phân phối, hay là **nhân viên trong công ty**? Nếu là hai nhóm khác nhau, họ có **quyền hạn giống hệt nhau** trên hệ thống không, và **trách nhiệm đền bù khi mất thẻ** có khác nhau không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Thiết kế **một vai trò `Sale/Đại lý`** đúng theo tài liệu hiện có, **nhưng** tách sẵn thuộc tính `loại đối tượng = Nội bộ | Đại lý ngoài` trên hồ sơ người dùng, và mọi truy vấn dữ liệu đều đi qua một lớp phân định phạm vi xem dữ liệu *(bộ lọc quyết định mỗi người được nhìn thấy dữ liệu nào — xem thêm Q-12)* → sau này nếu cần tách thành 2 vai trò thì không phải đập đi làm lại.

> **Trả lời của khách hàng:** ______

---

## 4. Phần B — 11 câu Quan trọng

> 🟡 Nhóm này chưa chặn việc bắt đầu, nhưng trả lời càng sớm thì càng ít phải làm lại.

### Q-07 · Quy mô sử dụng thực tế của hệ thống khoảng bao nhiêu?

- **Bối cảnh**: Tài liệu hiện có yêu cầu tra cứu thẻ phải xong trong vòng 2 giây. Tuy nhiên tài liệu chưa cho biết hệ thống sẽ phục vụ bao nhiêu người và bao nhiêu dữ liệu — mà tìm trong 10 nghìn thẻ khác hẳn tìm trong 10 triệu thẻ. Không có các con số này thì đội không chọn được quy mô máy chủ phù hợp, và cũng không có căn cứ để nghiệm thu chỉ tiêu 2 giây.

- **Câu hỏi**: *"Để thiết kế hệ thống chạy đủ nhanh và chọn đúng quy mô máy chủ, anh/chị cho em xin vài con số ước lượng (chỉ cần áng chừng): (1) Tổng số người dùng: bao nhiêu Admin, bao nhiêu NV Kho, bao nhiêu Sale/Đại lý? (2) Số người dùng **cùng lúc** vào giờ cao điểm? (3) Trung bình **bao nhiêu đơn xuất/ngày**, ngày cao điểm khoảng bao nhiêu? (4) Hiện có **bao nhiêu thẻ trong kho** và mỗi tháng nhập thêm khoảng bao nhiêu? (5) Có **bao nhiêu kho** trên toàn hệ thống?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Thiết kế cho quy mô doanh nghiệp vừa: **≤ 200 người dùng, ≤ 30 người dùng đồng thời, ≤ 500 đơn/ngày, ≤ 5 triệu bản ghi thẻ, ≤ 20 kho**. Ghi rõ trong tài liệu sản phẩm đây là **giả định thiết kế chờ xác nhận**, không phải cam kết về mức chất lượng dịch vụ.

> **Trả lời của khách hàng:** ______

---

### Q-08 · Dữ liệu và ảnh giao nhận cần lưu giữ trong bao lâu?

- **Bối cảnh**: Tài liệu hiện có yêu cầu sao lưu dữ liệu hàng ngày, nhưng chưa nói rõ dữ liệu cần **giữ lại bao lâu**. Giữ 3 tháng hay giữ 7 năm là hai bài toán chi phí lưu trữ chênh nhau rất nhiều lần, nhất là khi có kèm ảnh chụp lúc giao nhận. Ngoài ra chứng từ giao nhận thường có quy định lưu trữ theo luật kế toán.

- **Câu hỏi**: *"Dữ liệu đơn hàng và **ảnh chụp giao nhận (POD)** cần được **lưu giữ trong bao lâu** (1 năm, 3 năm, 5 năm, hay vĩnh viễn)? Công ty có quy định nội bộ hoặc yêu cầu pháp lý nào về việc lưu trữ chứng từ giao nhận không? Ngoài ra, nếu sự cố xảy ra, việc **mất dữ liệu tối đa bao lâu** là chấp nhận được (VD: mất dữ liệu của 24 giờ gần nhất)?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Dữ liệu đơn hàng lưu **vĩnh viễn** (không xóa, chỉ chuyển vào khu lưu trữ). Ảnh chụp giao nhận lưu **tối thiểu 3 năm**. Giữ **30 bản sao lưu ngày** gần nhất. Mức dữ liệu tối đa chấp nhận mất khi có sự cố là **24 giờ** *(tức là nếu hệ thống hỏng, dữ liệu được khôi phục về bản sao lưu gần nhất, muộn nhất là 24 giờ trước đó)* — khớp với tần suất sao lưu hàng ngày mà tài liệu đã nêu.

> **Trả lời của khách hàng:** ______

---

### Q-13 · Ảnh chụp lúc nhận hàng được giới hạn thế nào và lưu ở đâu?

- **Bối cảnh**: Tài liệu hiện có yêu cầu Sale phải đính kèm **tối thiểu 1 ảnh** khi nhận hàng, nhưng chưa nói **tối đa bao nhiêu ảnh** và ảnh **nặng bao nhiêu** thì được chấp nhận. Nếu không giới hạn, dung lượng lưu trữ sẽ phình rất nhanh và việc mở đơn xem ảnh sẽ bị chậm. Ngoài ra, nơi đặt dữ liệu cũng cần làm rõ để đảm bảo tuân thủ quy định.

  *(**Upload** = tải ảnh lên hệ thống. **On-premise** = đặt trên máy chủ do công ty tự quản lý. **Cloud** = thuê hạ tầng của nhà cung cấp dịch vụ bên ngoài, trả tiền theo mức dùng.)*

- **Câu hỏi**: *"Về ảnh chụp lúc nhận hàng: (1) Mỗi đơn cho phép upload **tối đa bao nhiêu ảnh**? (2) Hệ thống có thể **tự động nén ảnh** để tải nhanh hơn không, hay anh/chị cần giữ **ảnh gốc chất lượng cao** để làm bằng chứng? (3) Dữ liệu và ảnh được lưu trên **máy chủ của công ty (on-premise)** hay trên **dịch vụ cloud**? Có yêu cầu bắt buộc dữ liệu phải đặt **tại Việt Nam** không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Tối đa **10 ảnh/đơn**, mỗi ảnh **≤ 10MB**, hệ thống **tự nén** xuống bản hiển thị nhưng **vẫn giữ file gốc**. Lưu trên **dịch vụ lưu trữ file chuyên dụng đặt tại Việt Nam**. Chỉ chấp nhận ảnh định dạng JPG/PNG/HEIC *(các định dạng ảnh thông dụng của điện thoại và máy ảnh)*.

> **Trả lời của khách hàng:** ______

---

### Q-14 · Người dùng sẽ đăng nhập bằng tài khoản nào?

- **Bối cảnh**: Tài liệu hiện có nêu hai lựa chọn kỹ thuật cho việc đăng nhập và nối chúng bằng chữ "hoặc" — nghĩa là chưa chốt phương án. Điều đội cần biết không phải là tên kỹ thuật, mà là: người dùng sẽ dùng **tài khoản riêng của hệ thống này**, hay dùng luôn **tài khoản email công ty** đang có sẵn. Hai hướng này khác nhau đáng kể về khối lượng công việc.

- **Câu hỏi**: *"Người dùng sẽ đăng nhập vào hệ thống bằng cách nào: (A) **tài khoản riêng** do hệ thống này tự quản lý (tên đăng nhập + mật khẩu), hay (B) đăng nhập bằng **tài khoản sẵn có của công ty** (Google Workspace / Microsoft 365 / hệ thống nội bộ khác)? **[Đề xuất: phương án A]** vì đơn giản và không phụ thuộc hệ thống khác. Ngoài ra có cần **xác thực 2 lớp (OTP)** cho tài khoản Admin không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: **Phương án A** — tài khoản riêng, đăng nhập bằng cơ chế JWT *(một dạng "vé điện tử" hệ thống cấp cho người dùng sau khi đăng nhập thành công, gồm vé chính dùng hằng ngày và vé gia hạn khi vé chính hết hạn)*. Không dùng chung tài khoản công ty, không xác thực 2 lớp ở giai đoạn 1.

> **Trả lời của khách hàng:** ______

---

### Q-15 · Các trạng thái do bên vận chuyển báo về được hiển thị như thế nào?

- **Bối cảnh**: Tài liệu hiện có yêu cầu hiển thị các trạng thái như "Đã lấy hàng", "Đến bưu cục", "Đang giao" — đây là các trạng thái do bên vận chuyển cung cấp. Nhưng phần quy trình chính của tài liệu lại chỉ có **một** trạng thái duy nhất là "Đang vận chuyển". Chưa rõ hai nhóm trạng thái này quan hệ với nhau ra sao.

- **Câu hỏi**: *"Các trạng thái như 'Đã lấy hàng', 'Đến bưu cục', 'Đang giao' là do **bên vận chuyển** cung cấp. Anh/chị muốn hiển thị chúng như **thông tin tham khảo bên trong đơn** (kiểu lịch sử hành trình), hay coi chúng là **trạng thái chính thức của đơn hàng** trong hệ thống mình? **[Đề xuất: phương án đầu]** để nếu sau này đổi đơn vị vận chuyển thì quy trình nội bộ không bị ảnh hưởng."*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Giữ **5 trạng thái chính** của đơn. Trạng thái do bên vận chuyển báo về được lưu ở **danh sách lịch sử hành trình riêng**, hiển thị dạng dòng thời gian bên trong đơn đang ở tình trạng `In Transit` *(Đang vận chuyển)*. Không đưa vào bộ trạng thái chính thức của đơn hàng.

> **Trả lời của khách hàng:** ______

---

### Q-16 · Một chiếc thẻ VETC có thể ở những tình trạng nào?

- **Bối cảnh**: Tài liệu hiện có chỉ nêu **đúng một** tình trạng của thẻ là "Báo mất - Đã đền bù". Trong khi đó, yêu cầu truy vết đòi hỏi tra bất kỳ mã thẻ nào cũng ra được đầy đủ hành trình — muốn vậy hệ thống cần biết mỗi chiếc thẻ có thể trải qua những giai đoạn nào từ lúc về kho tới lúc bàn giao.

- **Câu hỏi**: *"Một chiếc thẻ VETC trong hệ thống có thể ở những tình trạng nào? Đề xuất danh sách sau, nhờ anh/chị bổ sung hoặc sửa: **Còn trong kho → Đã gán vào đơn → Đang vận chuyển → Đã bàn giao cho Đại lý → Đã kích hoạt (?) → Báo mất (chưa đền bù) → Báo mất (đã đền bù) → Hỏng/Hủy**. Đặc biệt: sau khi Đại lý nhận thẻ và **bán cho khách hàng cuối**, hệ thống có cần theo dõi tiếp không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Vòng đời thẻ gồm 7 tình trạng theo danh sách trên, **bỏ** "Đã kích hoạt" và **dừng theo dõi** ở mốc "Đã bàn giao cho Đại lý" (tài liệu hiện có không hề nhắc tới khách hàng cuối).

> **Trả lời của khách hàng:** ______

---

### Q-17 · Gặp đơn nghi trùng thì cảnh báo hay chặn hẳn?

- **Bối cảnh**: Tài liệu hiện có viết hệ thống sẽ "cảnh báo **hoặc** cho phép Nhân viên Kho từ chối nhanh" — hai cách xử lý khác nhau nối bằng chữ "hoặc", nên chưa rõ anh/chị muốn cách nào. Chặn cứng sẽ an toàn hơn nhưng có nguy cơ chặn nhầm đơn hợp lệ, khiến Sale phải gọi điện nhờ can thiệp.

- **Câu hỏi**: *"Khi hệ thống nghi ngờ một đơn bị trùng: nên (A) **hiện cảnh báo** nhưng vẫn cho gửi/duyệt bình thường, hay (B) **chặn không cho gửi** cho đến khi có người xác nhận? **[Đề xuất: phương án A]** vì tránh chặn nhầm đơn thật, và Nhân viên Kho vẫn là người quyết định cuối."*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: **Phương án A** — cảnh báo mềm ở cả phía Sale (lúc gửi) và NV Kho (lúc duyệt), kèm nút "Từ chối nhanh" để NV Kho xử lý một chạm.

> **Trả lời của khách hàng:** ______

---

### Q-20 · Có cần thông báo tự động cho người liên quan không?

- **Bối cảnh**: Tài liệu hiện có mô tả quy trình có **2 cấp duyệt nối tiếp nhau**, nhưng chưa nói tới việc báo tin cho người cần duyệt. Nếu không có thông báo, Nhân viên Kho và Admin sẽ phải tự nhớ vào hệ thống kiểm tra xem có đơn nào đang chờ hay không — đơn có thể nằm chờ nhiều giờ, khiến thời gian xuất kho kéo dài hơn cả cách làm cũ.

- **Câu hỏi**: *"Khi có đơn mới chờ duyệt, hoặc đơn được duyệt/từ chối, hoặc hàng đã giao đến — người liên quan có cần được **thông báo tự động** không? Nếu có, thông báo qua kênh nào: **thông báo trong hệ thống (chuông)**, **email**, **Zalo**, hay **SMS**? **[Đề xuất: thông báo trong hệ thống + email]** cho giai đoạn đầu vì không tốn phí và triển khai nhanh."*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Có **thông báo hiển thị ngay trong hệ thống** cho các mốc: đơn mới chờ duyệt, đơn được duyệt, đơn bị từ chối, hàng đã giao. **Email** cho các mốc quan trọng. Không dùng SMS/Zalo ở giai đoạn 1.

> **Trả lời của khách hàng:** ______

---

### Q-23 · Nhân viên nhận hàng sẽ thao tác trên điện thoại hay máy tính?

- **Bối cảnh**: Tài liệu hiện có chưa nói rõ hệ thống sẽ chạy trên nền tảng nào. Điều này đáng lưu ý vì bước nhận hàng yêu cầu Sale **chụp ảnh lô thẻ và tải lên hệ thống** — việc này diễn ra ngay tại nơi nhận hàng, gần như chắc chắn là trên điện thoại. Nếu chỉ làm cho màn hình máy tính thì trên thực tế Sale sẽ chụp ảnh rồi về văn phòng mới tải lên, làm giảm giá trị của tấm ảnh làm bằng chứng.

  *(**Upload** = tải ảnh lên hệ thống. **Store** = kho ứng dụng App Store / CH Play, nơi phải nộp ứng dụng chờ duyệt trước khi người dùng cài được.)*

- **Câu hỏi**: *"Nhân viên Sale/Đại lý sẽ chụp ảnh và xác nhận nhận hàng **ngay tại chỗ bằng điện thoại**, đúng không ạ? Nếu vậy, anh/chị cần (A) **website hiển thị tốt trên điện thoại** (mở bằng trình duyệt, không cần cài đặt), hay (B) **ứng dụng cài đặt riêng** trên iOS/Android? **[Đề xuất: phương án A]** vì nhanh hơn, không phải chờ duyệt store, và vẫn chụp ảnh upload được bình thường."*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: **Phương án A** — website tự co giãn hiển thị vừa mọi kích thước màn hình, tối ưu riêng cho bước nhận hàng trên màn hình điện thoại. Không làm ứng dụng cài đặt riêng trên iOS/Android ở giai đoạn 1.

> **Trả lời của khách hàng:** ______

---

### Q-27 · Công ty đang phân phối những loại thẻ VETC nào?

- **Bối cảnh**: Tài liệu hiện có nói Sale "chọn loại thẻ" khi tạo đơn, nhưng chưa liệt kê **có những loại thẻ nào**, và cũng chưa giao cho ai quyền thêm loại thẻ mới. Nếu danh sách này được cài cứng vào phần mềm thì mỗi lần có loại thẻ mới đều phải nhờ đội kỹ thuật sửa và cập nhật lại hệ thống.

- **Câu hỏi**: *"Hiện công ty đang phân phối **những loại thẻ VETC nào** (vui lòng liệt kê giúp em)? Danh sách này có **thay đổi/bổ sung theo thời gian** không? Nếu có, **ai** sẽ là người được phép thêm loại thẻ mới vào hệ thống — Admin đúng không ạ? Mỗi loại thẻ có cần lưu thêm thông tin gì không (mệnh giá, đối tượng sử dụng, giá bán...)?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Bổ sung **Danh mục Loại thẻ** (cho phép thêm/sửa/xóa/xem, quyền Admin), tối thiểu gồm: mã loại, tên loại, mô tả, trạng thái hoạt động. **Không** lưu giá/mệnh giá (tài liệu hiện có không nhắc tới tiền của thẻ, ngoại trừ tiền đền bù).

> **Trả lời của khách hàng:** ______

---

### Q-28 · Admin cần xem những báo cáo cụ thể nào?

- **Bối cảnh**: Tài liệu hiện có giao cho Admin quyền "quản lý danh mục nhân sự" và "xem báo cáo tổng hợp", nhưng phần mô tả chi tiết lại **chỉ có danh mục kho**, không có mục nào nói rõ hai chức năng kia gồm những gì. "Báo cáo tổng hợp" là cụm từ rất rộng — nếu không chốt danh sách cụ thể, đội có thể làm ra thứ không đúng nhu cầu thực tế của anh/chị.

- **Câu hỏi**: *"Về phần **Báo cáo tổng hợp** cho Admin: anh/chị cần xem những báo cáo cụ thể nào? Ví dụ: **Tồn kho theo từng kho**, **Số đơn theo trạng thái**, **Số thẻ đã xuất theo từng Đại lý**, **Danh sách thẻ thất thoát và tình trạng đền bù**, **Thời gian trung bình từ lúc tạo đơn đến lúc giao xong**. Nhờ anh/chị đánh dấu những báo cáo **thực sự cần** và bổ sung nếu thiếu. Có cần **xuất ra file Excel** không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Giai đoạn 1 làm **4 báo cáo**: (1) Tồn kho theo kho, (2) Đơn theo trạng thái trong khoảng thời gian, (3) Sản lượng thẻ theo Đại lý, (4) Danh sách thất thoát & tình trạng đền bù. Tất cả **xuất được Excel**. Quản lý nhân sự = thêm/sửa/xóa/xem tài khoản người dùng ở mức cơ bản (tạo mới, khóa, đổi vai trò, đặt lại mật khẩu).

> **Trả lời của khách hàng:** ______

---

## 5. Phần C — 9 câu Nên có

> 🟢 Nhóm này có thể trả lời dần trong quá trình triển khai, không chặn tiến độ.

### Q-18 · Trong nhóm Nhân viên Kho có phân biệt cấp bậc không?

- **Bối cảnh**: Tài liệu hiện có tuyên bố hệ thống có **3 nhóm người dùng**, nhưng ở phần danh mục kho lại xuất hiện cụm "Nhân viên Kho **có thẩm quyền**" — hàm ý rằng bên trong nhóm Nhân viên Kho còn có phân cấp. Cần anh/chị xác nhận để đội biết có phải làm thêm một nhóm quyền nữa hay không.

- **Câu hỏi**: *"Trong nhóm Nhân viên Kho, có phân biệt **cấp bậc** không (VD: Nhân viên kho thường và Trưởng kho)? Nếu có, việc **sửa/xóa thông tin kho** chỉ dành cho Trưởng kho, còn nhân viên thường chỉ được duyệt đơn — đúng không ạ?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: **Không** phân cấp trong nhóm NV Kho (giữ đúng 3 nhóm người dùng). Mọi NV Kho đều có thể sửa thông tin kho **mình phụ trách**; **chỉ Admin** được tạo mới/xóa kho.

> **Trả lời của khách hàng:** ______

---

### Q-19 · Biên bản Bàn giao Thẻ cần làm theo mẫu nào?

- **Bối cảnh**: Tài liệu hiện có nói hệ thống tự sinh Biên bản Bàn giao Thẻ dạng "PDF/Excel", nhưng dấu gạch chéo chưa cho biết là **cả hai** hay **chọn một**, và cũng chưa có mẫu biểu cụ thể. Biên bản bàn giao thường là chứng từ có giá trị đối chứng nên công ty hầu như luôn có mẫu sẵn — nếu đội tự thiết kế thì nhiều khả năng phải làm lại.

- **Câu hỏi**: *"Về **Biên bản Bàn giao Thẻ**: (1) Anh/chị cần file **PDF**, **Excel**, hay **cả hai**? (2) Công ty đã có **mẫu biên bản sẵn** chưa? Nếu có nhờ anh/chị gửi em file mẫu. (3) Biên bản có cần **chữ ký số** hoặc **dấu công ty** không, hay chỉ cần in ra ký tay là đủ?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Xuất **PDF** (để in ký tay) + **Excel** (để đối soát dữ liệu). Mẫu do đội thiết kế, gồm: mã đơn, ngày xuất/nhận, kho xuất, NV kho, Sale/Đại lý nhận, loại thẻ, số lượng, dải Series, ảnh chụp lúc nhận hàng, ô ký tên hai bên. **Không** dùng chữ ký số.

> **Trả lời của khách hàng:** ______

---

### Q-22 · Số tiền đền bù thẻ mất được xác định như thế nào?

- **Bối cảnh**: Tài liệu hiện có chỉ nói hệ thống "ghi nhận số tiền" đền bù, nhưng chưa nói ai là người quyết định số tiền đó và dựa trên căn cứ nào. Nếu để người làm mất thẻ tự khai số tiền thì việc kiểm soát gần như không có; ngược lại nếu công ty đã có biểu giá cố định thì hệ thống nên tự tính để tránh tranh cãi.

- **Câu hỏi**: *"Khi phải đền bù thẻ mất, **số tiền đền bù** được xác định như thế nào: (A) có **biểu giá cố định** cho mỗi loại thẻ (hệ thống tự tính = số thẻ mất × đơn giá), hay (B) **thương lượng từng trường hợp** và nhập tay? Nếu là (A), nhờ anh/chị cho em xin **bảng giá đền bù** theo từng loại thẻ."*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: **Nhập tay** số tiền (đúng theo chữ "ghi nhận số tiền" của tài liệu hiện có), nhưng **bắt buộc** phải do Admin xác nhận và **bắt buộc** đính kèm chứng từ.

> **Trả lời của khách hàng:** ______

---

### Q-24 · Sale có được tự hủy đơn của mình không?

- **Bối cảnh**: Tài liệu hiện có chưa nói tới việc hủy đơn ở bất kỳ giai đoạn nào. Trên thực tế Sale có thể gửi nhầm (sai số lượng, sai loại thẻ) và muốn hủy trước khi kho xử lý; hoặc đơn đã duyệt nhưng đại lý báo không lấy nữa. Không có cách hủy thì những đơn này sẽ bị kẹt lại trong hệ thống.

- **Câu hỏi**: *"Sale có được **tự hủy đơn** của mình không? Nếu có thì được hủy đến **giai đoạn nào** — chỉ khi đơn **chưa được kho duyệt**, hay hủy được cả khi đơn **đã duyệt nhưng chưa gửi đi**? Trường hợp hàng đã lên đường vận chuyển rồi thì xử lý ra sao?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Sale **tự hủy** khi đơn còn ở tình trạng `Pending Warehouse` *(Chờ kho duyệt)*. Từ `Pending Admin Approval` *(Chờ Admin duyệt)* trở đi, chỉ **Admin** được hủy (kèm lý do bắt buộc). Từ `In Transit` *(Đang vận chuyển)* trở đi **không cho hủy** — xử lý qua luồng báo sai lệch (xem Q-11).

> **Trả lời của khách hàng:** ______

---

### Q-25 · Giao hàng không thành công và thẻ quay về kho thì xử lý ra sao?

- **Bối cảnh**: Sơ đồ trong tài liệu hiện có mặc định việc giao hàng luôn thành công. Trên thực tế giao hàng thất bại là chuyện thường gặp, và khi đó số thẻ trong đơn vẫn đang được tính là "đã xuất kho" trong khi thực tế chúng đang trên đường quay về — dẫn tới sai lệch số liệu tồn kho.

- **Câu hỏi**: *"Nếu bên vận chuyển **giao hàng không thành công** và **hoàn thẻ về kho**, hệ thống cần xử lý thế nào: đơn đó bị **hủy** và số thẻ được **trả lại tồn kho**, hay đơn giữ nguyên để **giao lại lần 2**? Ai là người cập nhật việc kho đã nhận lại hàng hoàn?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Bổ sung tình trạng `Delivery Failed` *(Giao hàng thất bại)* → NV Kho xác nhận đã nhận hàng hoàn → đơn chuyển sang `Returned` *(Đã hoàn về kho — là tình trạng kết thúc)* và **thẻ được trả lại tồn kho**. Muốn giao lại thì tạo đơn mới.

> **Trả lời của khách hàng:** ______

---

### Q-26 · Nhân viên Kho xem số lượng thẻ còn trong kho ở đâu?

- **Bối cảnh**: Tài liệu hiện có nhắc hai lần việc Nhân viên Kho phải "kiểm tra tồn kho" trước khi duyệt đơn, và xử lý khi "kho không đủ tồn". Tuy nhiên phần mô tả dữ liệu của kho chỉ có tên kho, địa chỉ, người phụ trách và số điện thoại — **không có số liệu tồn kho nào**. Nghĩa là hiện tại tài liệu đang yêu cầu một thao tác trên dữ liệu chưa được định nghĩa.

- **Câu hỏi**: *"Khi Nhân viên Kho 'kiểm tra tồn kho' để quyết định duyệt đơn, họ sẽ xem số liệu tồn **ở đâu**: (A) ngay trên hệ thống mới này, hay (B) trên **file/phần mềm khác** mà công ty đang dùng? **[Đề xuất: phương án A]** — nhưng để làm được thì hệ thống phải quản lý cả việc nhập thẻ vào kho (liên quan câu hỏi Q-01 phía trên)."*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Hệ thống **có** màn hình tồn kho theo từng kho và theo từng loại thẻ, tính bằng công thức: (tồn khởi tạo nhập từ file Excel) − (đã xuất) + (hàng hoàn về). Đây là cách tối thiểu để việc gán dải Series (Q-06) và việc chặn cấp trùng Series hoạt động được.

> **Trả lời của khách hàng:** ______

---

### Q-29 · Thế nào thì anh/chị coi là dự án đã thành công?

- **Bối cảnh**: Tài liệu hiện có mô tả rất rõ hệ thống **làm được gì**, nhưng chưa nói **đo thành công bằng gì**. Không có chỉ tiêu đo lường thì tới lúc nghiệm thu, hai bên sẽ không có căn cứ chung để khẳng định dự án đã đạt mục tiêu hay chưa. Đây cũng là phần đội **không thể tự điền thay anh/chị** được.

- **Câu hỏi**: *"Sau khi hệ thống chạy được 6 tháng, **điều gì xảy ra** thì anh/chị coi là dự án **thành công**? Ví dụ: 'giảm số thẻ thất thoát không truy được nguồn gốc từ X xuống gần 0', 'rút ngắn thời gian từ lúc Sale đặt đến lúc nhận thẻ từ X ngày xuống Y ngày', 'tra được nguồn gốc bất kỳ thẻ nào trong dưới 1 phút thay vì phải hỏi qua nhiều người'. Hiện tại mỗi tháng công ty **thất thoát khoảng bao nhiêu thẻ**, và quy trình hiện tại đang mất nhiều thời gian nhất ở khâu nào?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Tài liệu nghiệp vụ chỉ ghi mục tiêu **định tính** (giảm thất thoát, minh bạch truy vết, chuẩn hóa phê duyệt) và để phần chỉ số định lượng ở trạng thái **chưa xác định**. **Tuyệt đối không** điền số phỏng đoán.

> **Trả lời của khách hàng:** ______

---

### Q-30 · Hiện tại công ty đang làm việc này bằng công cụ gì?

- **Bối cảnh**: Tài liệu hiện có mô tả hệ thống mong muốn, nhưng chưa nói gì về cách công ty đang vận hành hiện nay, dữ liệu cũ có cần đưa sang hay không, và mong muốn đưa vào sử dụng khi nào. Biết được những điều này giúp đội sắp xếp thứ tự công việc cho hợp lý và chuẩn bị trước phần chuyển dữ liệu.

- **Câu hỏi**: *"(1) Hiện tại công ty đang quản lý việc xuất kho và phân phối thẻ **bằng công cụ gì** (Excel, Google Sheet, phần mềm sẵn có, hay sổ giấy)? (2) Dữ liệu cũ có cần **chuyển vào hệ thống mới** không, và khoảng bao nhiêu dữ liệu? (3) Anh/chị mong muốn hệ thống **đưa vào sử dụng vào thời điểm nào**? (4) Có mốc thời gian bắt buộc nào (mùa cao điểm, cam kết với đối tác) không?"*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Giả định hiện trạng là **Excel + trao đổi qua Zalo/email**. Việc chuyển dữ liệu cũ sang hệ thống mới = **nhập từ file Excel một lần** cho danh mục kho, danh sách người dùng và tồn kho khởi tạo. Thời điểm đưa vào sử dụng: **chưa xác định**.

> **Trả lời của khách hàng:** ______

---

### Q-31 · Địa chỉ giao hàng của đơn được lấy từ đâu?

- **Bối cảnh**: Tài liệu hiện có mô tả rất chi tiết thông tin của **kho gửi** (tên, địa chỉ, người phụ trách, số điện thoại), nhưng chưa có thông tin nào về **bên nhận**. Trong khi đó, muốn chuyển đơn sang bên vận chuyển thì bắt buộc phải có tên người nhận, địa chỉ và số điện thoại.

- **Câu hỏi**: *"Khi tạo đơn, **địa chỉ giao hàng** được lấy từ đâu: (A) từ **hồ sơ Đại lý** đã lưu sẵn trong hệ thống (mỗi đại lý có địa chỉ cố định), hay (B) Sale **tự nhập địa chỉ** cho từng đơn (vì có thể giao đến nhiều nơi khác nhau)? **[Đề xuất: phương án A có cho phép sửa]** — mặc định lấy địa chỉ đại lý, nhưng vẫn cho đổi nếu lần này giao chỗ khác."*

- **Phương án đội đang tạm dùng nếu chưa có câu trả lời**: Bổ sung **Danh mục Đại lý** (tên, mã, địa chỉ mặc định, người liên hệ, SĐT). Đơn hàng **tự điền** thông tin từ hồ sơ đại lý, **cho phép sửa** địa chỉ theo từng đơn.

> **Trả lời của khách hàng:** ______

---

## 6. Bảng tổng hợp để tick

> Anh/chị có thể dùng bảng này để theo dõi tiến độ trả lời. Cột cuối cùng dành cho anh/chị ghi ngắn gọn (`OK` nếu đồng ý phương án tạm, hoặc ghi phương án mong muốn).

| Mã | Tóm tắt câu hỏi | Mức độ | Trả lời của khách hàng |
| :--- | :--- | :---: | :--- |
| **Q-01** | Có quản lý cả việc nhận thẻ từ nhà cung cấp về kho không? | 🔴 Cần gấp | |
| **Q-02** | Đơn vị vận chuyển đang hợp tác là bên nào? | 🔴 Cần gấp | |
| **Q-03** | Thông tin vận chuyển cần cập nhật nhanh đến mức nào? | 🔴 Cần gấp | |
| **Q-04** | Tiền đền bù nộp trực tiếp trên hệ thống hay chỉ ghi nhận lại? | 🔴 Cần gấp | |
| **Q-05** | Thế nào là hai đơn bị coi là trùng nhau? | 🔴 Cần gấp | |
| **Q-06** | Dải số Series được gán vào đơn lúc nào, do ai? | 🔴 Cần gấp | |
| **Q-09** | Đơn bị Nhân viên Kho từ chối thì đi về đâu? | 🔴 Cần gấp | |
| **Q-10** | Admin có được quyền từ chối đơn không? | 🔴 Cần gấp | |
| **Q-11** | Nhận hàng thiếu hoặc sai dải Series thì xử lý ra sao? | 🔴 Cần gấp | |
| **Q-12** | Ai được xem dữ liệu của ai? | 🔴 Cần gấp | |
| **Q-21** | "Nhân viên Sale" và "Đại lý" là một hay hai nhóm? | 🔴 Cần gấp | |
| **Q-07** | Quy mô sử dụng thực tế khoảng bao nhiêu? | 🟡 Quan trọng | |
| **Q-08** | Dữ liệu và ảnh giao nhận lưu giữ bao lâu? | 🟡 Quan trọng | |
| **Q-13** | Ảnh nhận hàng giới hạn thế nào, lưu ở đâu? | 🟡 Quan trọng | |
| **Q-14** | Người dùng đăng nhập bằng tài khoản nào? | 🟡 Quan trọng | |
| **Q-15** | Trạng thái do bên vận chuyển báo về hiển thị thế nào? | 🟡 Quan trọng | |
| **Q-16** | Một chiếc thẻ có thể ở những tình trạng nào? | 🟡 Quan trọng | |
| **Q-17** | Đơn nghi trùng thì cảnh báo hay chặn hẳn? | 🟡 Quan trọng | |
| **Q-20** | Có cần thông báo tự động cho người liên quan không? | 🟡 Quan trọng | |
| **Q-23** | Nhận hàng thao tác trên điện thoại hay máy tính? | 🟡 Quan trọng | |
| **Q-27** | Công ty đang phân phối những loại thẻ nào? | 🟡 Quan trọng | |
| **Q-28** | Admin cần xem những báo cáo cụ thể nào? | 🟡 Quan trọng | |
| **Q-18** | Trong nhóm Nhân viên Kho có phân biệt cấp bậc không? | 🟢 Nên có | |
| **Q-19** | Biên bản Bàn giao Thẻ theo mẫu nào? | 🟢 Nên có | |
| **Q-22** | Số tiền đền bù xác định như thế nào? | 🟢 Nên có | |
| **Q-24** | Sale có được tự hủy đơn không? | 🟢 Nên có | |
| **Q-25** | Giao hàng thất bại, thẻ về kho thì xử lý ra sao? | 🟢 Nên có | |
| **Q-26** | Nhân viên Kho xem tồn kho ở đâu? | 🟢 Nên có | |
| **Q-29** | Thế nào là dự án thành công? | 🟢 Nên có | |
| **Q-30** | Hiện tại đang làm bằng công cụ gì? | 🟢 Nên có | |
| **Q-31** | Địa chỉ giao hàng lấy từ đâu? | 🟢 Nên có | |

**Tổng cộng: 31 câu** — 11 câu Cần gấp · 11 câu Quan trọng · 9 câu Nên có.

> 📞 Nếu có câu nào anh/chị thấy khó hình dung, chỉ cần ghi lại mã câu hỏi và đội sẽ sắp xếp một buổi trao đổi trực tiếp để cùng làm rõ.

---

## 7. Tài liệu liên quan

| Tài liệu | Quan hệ |
| :--- | :--- |
| [SRS-VETC](../020-Requirements/SRS-VETC.md) | Nguồn phân tích — tài liệu mô tả yêu cầu phần mềm mà anh/chị đã gửi |
| [PRD-VETC](../020-Requirements/PRD-VETC.md) | Liên quan — tài liệu yêu cầu sản phẩm, nơi ghi lại các phương án tạm đang áp dụng |
| [BRD-001 — Hệ Thống Xuất Kho & Phân Phối Thẻ VETC](../020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md) | Liên quan — tài liệu yêu cầu nghiệp vụ |

---

*Tài liệu được chuẩn hóa và quản lý bởi TNMCORE-OS.*

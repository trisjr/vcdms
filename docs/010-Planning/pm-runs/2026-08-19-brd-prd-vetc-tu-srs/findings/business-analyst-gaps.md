# Findings — business-analyst (Phần 3–5: Gap list, Mâu thuẫn, Glossary)

> Tiếp nối [business-analyst.md](./business-analyst.md). Tách file vì độ dài; cùng một lens, cùng một lần dispatch.
> Nguồn sự thật: `docs/020-Requirements/SRS-VETC.md`. Số dòng trích dẫn (d.NN) tính theo file SRS gốc.

---

# PHẦN 3 — GAP LIST (seed cho file câu hỏi gửi khách hàng)

> **31 câu hỏi**: 11 Blocker · 11 Quan trọng · 9 Nên có.

## 🔴 NHÓM BLOCKER (chặn thiết kế — cần trả lời trước khi code)

### Q-01 · Nhóm: Business / Phạm vi
- **SRS nói gì**: Tiêu đề (d.11–12) và mục III.1 (d.118) đều ghi **"Xuất / Nhập Kho"**, nhưng **100% nội dung** mục II và III chỉ mô tả luồng **XUẤT** (kho → Sale/Đại lý). Không có dòng nào về việc thẻ **từ nhà cung cấp nhập về kho**: không actor nhà cung cấp, không trạng thái nhập, không FR nhập.
- **Vì sao rủi ro**: Mâu thuẫn phạm vi nghiêm trọng nhất. Nếu có luồng nhập kho mà không thiết kế từ đầu → toàn bộ mô hình dữ liệu tồn kho, cách sinh dải Series, và cách "kiểm tra tồn kho" (FR-02) đều sai gốc. Câu hỏi "tồn kho từ đâu mà có?" hiện **không có lời đáp** trong SRS. Phát hiện muộn = làm lại schema tồn kho + migration.
- **Câu hỏi gửi khách hàng**: *"Hệ thống có cần quản lý cả việc **nhập thẻ từ nhà cung cấp về kho** không, hay chỉ quản lý việc **xuất thẻ từ kho giao cho Sale/Đại lý**? Nếu có nhập kho: ai là người tạo phiếu nhập, cần duyệt mấy cấp, và số lượng thẻ tồn kho ban đầu sẽ được đưa vào hệ thống bằng cách nào (nhập tay, import Excel, hay nối API với nhà cung cấp)?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Phase 1 **chỉ làm luồng XUẤT**. Tồn kho khởi tạo bằng **import Excel một lần** do Admin/NV Kho thực hiện. Luồng nhập kho đầy đủ đưa vào Phase 2. Đổi tên hệ thống trong tài liệu thành "Quản lý Xuất Kho & Phân phối Thẻ VETC" cho khớp phạm vi thực.

### Q-02 · Nhóm: Tích hợp
- **SRS nói gì**: III.2 (d.125) "Kết nối API với đơn vị vận chuyển đối tác **đã ký hợp đồng**". SRS **khẳng định đã có đối tác** nhưng **im lặng** về danh tính, tài liệu API, môi trường sandbox.
- **Vì sao rủi ro**: Không biết đối tác nào thì không ước lượng được công integration. Nhiều nhà vận chuyển VN chỉ có API tra cứu, **không có API tạo đơn** → FR-08 có thể **bất khả thi** như mô tả. Đây là dependency ngoài tầm kiểm soát của đội dev.
- **Câu hỏi gửi khách hàng**: *"Đơn vị vận chuyển đang ký hợp đồng là bên nào (Viettel Post / GHN / GHTK / J&T / khác)? Anh/chị đã có **tài liệu API** và **tài khoản môi trường test (sandbox)** từ họ chưa? Nếu có, vui lòng gửi kèm. Nếu chưa có API, hệ thống sẽ tạm cho NV Kho **nhập tay mã vận đơn** — anh/chị có chấp nhận phương án này cho giai đoạn đầu không?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Thiết kế tầng tích hợp theo mô hình **adapter/plugin** (trừu tượng hóa carrier), phase 1 chạy **adapter thủ công**: NV Kho nhập mã vận đơn và cập nhật trạng thái tay. Khi có tài liệu API thì cắm adapter thật vào, không đổi nghiệp vụ.

### Q-03 · Nhóm: Tích hợp / Phi chức năng
- **SRS nói gì**: II Bước 4 (d.105) "cập nhật vị trí/trạng thái theo **thời gian thực** (Real-time tracking)". SRS **im lặng** về cơ chế (webhook hay polling) và định nghĩa định lượng của "real-time".
- **Vì sao rủi ro**: "Real-time" là từ mơ hồ nhất trong SRS. Webhook và polling khác nhau hoàn toàn về kiến trúc. Polling 5 phút/lần với 1.000 đơn đang giao = 12.000 lượt gọi/giờ, có thể vượt rate limit của carrier hoặc phát sinh phí.
- **Câu hỏi gửi khách hàng**: *"Với việc theo dõi vận chuyển, **độ trễ bao nhiêu là chấp nhận được** đối với anh/chị: cập nhật gần như tức thì (dưới 1 phút), mỗi 15 phút, mỗi 1 giờ, hay chỉ cần 2–3 lần/ngày là đủ? Và bên vận chuyển có hỗ trợ **tự động bắn thông báo về hệ thống** (webhook) không, hay hệ thống của mình phải **chủ động hỏi** họ định kỳ?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: "Real-time" hiểu là **polling định kỳ mỗi 15 phút** cho các đơn `In Transit`; ưu tiên chuyển sang webhook nếu carrier hỗ trợ. Ghi rõ trong PRD là giả định chờ xác nhận, **không** ghi thành cam kết.

### Q-04 · Nhóm: Tích hợp / Nghiệp vụ
- **SRS nói gì**: III.4 (d.141) "**Tích hợp** chức năng nộp tiền đền bù / bù tiền thẻ (ghi nhận **số tiền, mã giao dịch, hóa đơn đền bù đính kèm**)". Từ "tích hợp" gợi ý cổng thanh toán, nhưng ba trường dữ liệu liệt kê lại **mang đặc trưng ghi nhận thủ công**.
- **Vì sao rủi ro**: Chênh lệch khối lượng công rất lớn. Ghi nhận thủ công ≈ 1 form + 1 upload. Tích hợp cổng thanh toán thật kéo theo hợp đồng cổng, xử lý callback, đối soát giao dịch, hoàn tiền, tuân thủ PCI — có thể gấp 5–10 lần công. Đoán sai là vỡ estimate và vỡ timeline.
- **Câu hỏi gửi khách hàng**: *"Khi Sale/Đại lý làm mất thẻ và phải đền bù: anh/chị muốn (A) người dùng **thanh toán trực tiếp trên hệ thống** qua cổng thanh toán/ví điện tử, hay (B) họ chuyển khoản/nộp tiền **bên ngoài** rồi kế toán chỉ **ghi nhận lại** số tiền, mã giao dịch và **upload ảnh chứng từ** vào hệ thống? **[Đề xuất: phương án B]** vì đúng với các trường dữ liệu mà tài liệu yêu cầu và nhanh hơn đáng kể. Ngoài ra, **ai** là người được phép xác nhận đã nhận đủ tiền đền bù?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: **Phương án B — ghi nhận thủ công**, đúng theo 3 trường mà III.4 d.141 đã liệt kê. Không tích hợp payment gateway trong phạm vi này. Người xác nhận: Admin.

### Q-05 · Nhóm: Chức năng / Dữ liệu
- **SRS nói gì**: III.1 (d.120) "cảnh báo hoặc cho phép NV kho từ chối nhanh các đơn trùng lặp gửi **trong thời gian ngắn**"; d.93 nêu đúng một tình huống: "**Sale bấm gửi 2 lần**". SRS cho **một** ví dụ, **không** cho định nghĩa "trùng lặp" và **không** cho khoảng thời gian.
- **Vì sao rủi ro**: Không có định nghĩa thì không viết được điều kiện code. Cửa sổ quá rộng → chặn nhầm đơn hợp lệ (đại lý lớn đặt 2 lô cùng loại trong ngày là bình thường). Quá hẹp → không bắt được double-submit.
- **Câu hỏi gửi khách hàng**: *"Hệ thống nên coi hai đơn là 'trùng lặp' khi nào? Ví dụ: **cùng một Sale + cùng loại thẻ + cùng số lượng** gửi trong vòng **bao nhiêu phút** (5 phút? 30 phút? trong cùng ngày?). Và trong thực tế, có trường hợp nào một Sale **cố ý** đặt 2 đơn giống hệt nhau trong thời gian ngắn mà vẫn là hợp lệ không?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Trùng lặp = **cùng Sale + cùng loại thẻ + cùng số lượng + trong vòng 15 phút**. Hệ thống **cảnh báo** (không chặn cứng) cho cả Sale lúc gửi và NV Kho lúc duyệt; NV Kho toàn quyền quyết định.

### Q-06 · Nhóm: Chức năng / Dữ liệu
- **SRS nói gì**: III.3 (d.130) dải số Series thẻ "**do kho cấp**". SRS trả lời **AI** (NV Kho) nhưng **im lặng** về **BƯỚC NÀO** và **CÁCH NÀO**. Ở Bước 2 (d.91–97), thao tác gán Series **không được liệt kê**.
- **Vì sao rủi ro**: Đây là mắt xích nối "đơn hàng" với "thẻ vật lý cụ thể" — **toàn bộ tính năng truy vết FR-14 phụ thuộc vào nó**. Nếu Series gán quá muộn thì không đối soát được với cái kho đã gửi. Nếu nhập tay thì mâu thuẫn với NFR-05 "chặn chọn dải series bị trùng lặp" (muốn chặn trùng, hệ thống phải quản lý pool Series → quay lại Q-01).
- **Câu hỏi gửi khách hàng**: *"Dải số Series của thẻ được gán cho đơn hàng **vào lúc nào** và **do ai làm**? Cụ thể: (A) NV Kho **tự gõ tay** dải Series khi duyệt đơn, hay (B) **hệ thống tự động lấy** dải Series còn trống trong kho và gán vào đơn? **[Đề xuất: phương án B]** vì chỉ khi hệ thống nắm được danh sách Series đang có trong kho thì mới chặn được việc cấp trùng Series. Nếu chọn B, hệ thống cần biết trước toàn bộ Series đang tồn — anh/chị lấy dữ liệu này ở đâu?"*
- **Mức độ**: **Blocker** (liên đới trực tiếp Q-01)
- **Giả định tạm**: NV Kho gán dải Series **tại Bước 2** (cùng lúc gán kho + chốt số lượng duyệt), theo phương án **(B) hệ thống gợi ý dải liên tục còn trống, NV Kho xác nhận/điều chỉnh**; hệ thống validate chống trùng theo NFR-05.

### Q-09 · Nhóm: Chức năng / Vận hành
- **SRS nói gì**: Mermaid d.65–67 có nhánh `NV_Kho->>System: Từ chối đơn` **nhưng không có `Note over System` gán trạng thái**, trong khi mọi bước khác đều có. Nhánh **cụt**.
- **Vì sao rủi ro**: Trạng thái không định nghĩa = lập trình viên tự chế, mỗi người một kiểu, hoặc đơn "biến mất" khỏi mọi danh sách. Sale không biết đơn mình bị sao. Nếu không cho sửa & gửi lại, Sale phải nhập lại từ đầu và mất dấu vết liên hệ giữa đơn cũ - đơn mới.
- **Câu hỏi gửi khách hàng**: *"Khi Nhân viên Kho **từ chối** một đơn: (1) Đơn đó nên **biến mất** hay vẫn **hiển thị trong danh sách của Sale** với nhãn 'Bị từ chối' kèm lý do? (2) Sale có được **sửa lại đơn và gửi lại** không, hay phải **tạo đơn hoàn toàn mới**? (3) NV Kho có **bắt buộc phải ghi lý do từ chối** không?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Bổ sung trạng thái `Rejected (Bị từ chối)`. Đơn **vẫn hiển thị** cho Sale kèm **lý do bắt buộc**. Sale được **sao chép đơn cũ thành đơn mới** (không sửa trực tiếp đơn đã bị từ chối, để giữ nguyên vẹn audit trail theo NFR-04). `Rejected` là trạng thái **kết thúc**.

### Q-10 · Nhóm: Chức năng / Vận hành
- **SRS nói gì**: II Bước 3 (d.99–101): "Admin kiểm tra và **ra quyết định duyệt cuối cùng**" → gán thẳng `Ready for Shipping`. **SRS hoàn toàn không có nhánh Admin từ chối.**
- **Vì sao rủi ro**: Cấp phê duyệt cuối mà không có quyền từ chối thì việc phê duyệt 2 cấp (BR-01) mất ý nghĩa — Admin trở thành nút bấm hình thức. Thực tế Admin chắc chắn cần từ chối (vượt hạn mức, đại lý đang nợ, nghi ngờ gian lận).
- **Câu hỏi gửi khách hàng**: *"Ở bước phê duyệt cuối, ngoài **Duyệt**, Admin có cần thêm quyền **Từ chối** đơn không? Nếu có: đơn bị Admin từ chối sẽ **quay lại cho Nhân viên Kho xem xét lại**, hay **đóng luôn** và báo về cho Sale? Ngoài ra, Admin có cần quyền **sửa lại số lượng** một lần nữa (khác với số lượng NV Kho đã duyệt) không?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Admin **có** quyền Từ chối, **bắt buộc ghi lý do**, đơn chuyển `Rejected` và **báo về Sale** (không quay ngược về NV Kho, tránh vòng lặp duyệt vô tận). Admin **không** có quyền sửa số lượng (giữ nguyên tắc phân tách trách nhiệm: kho chốt số, admin chốt cho/không cho).

### Q-11 · Nhóm: Chức năng / Vận hành
- **SRS nói gì**: II Bước 5 (d.108–112) chỉ mô tả luồng thuận: "**Xác nhận đúng** số lượng và dải số Series thẻ do kho cấp". SRS **im lặng** hoàn toàn về trường hợp Sale nhận **thiếu, thừa, hỏng, hoặc lệch Series**.
- **Vì sao rủi ro**: Đây chính là **kịch bản mà cả hệ thống sinh ra để xử lý** — thất thoát thẻ (III.4). Nghịch lý: SRS xây chức năng quản lý thất thoát nhưng **không có luồng nào để phát hiện thất thoát**. Nếu chỉ có nút [Hoàn thành], Sale nhận thiếu 10 thẻ sẽ hoặc bị ép bấm hoàn thành (mất luôn 10 thẻ không ai chịu trách nhiệm), hoặc để đơn treo mãi ở `In Transit`.
- **Câu hỏi gửi khách hàng**: *"Khi Sale/Đại lý nhận hàng và phát hiện **thiếu thẻ** hoặc **dải Series không khớp** với thông tin trên hệ thống, quy trình xử lý hiện tại của công ty là gì? Cụ thể: (1) Sale có được bấm **'Báo sai lệch'** thay vì 'Hoàn thành' không? (2) **Ai** là người xử lý khiếu nại đó — NV Kho, Admin, hay bên vận chuyển? (3) Sau khi xử lý xong, đơn được **đóng với số lượng thực nhận**, hay kho phải **giao bù phần thiếu**?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Bổ sung nút **[Báo sai lệch]** ở Bước 5 → trạng thái `Discrepancy (Có sai lệch)`, bắt buộc Sale nhập số lượng thực nhận + ảnh + mô tả. Đơn chuyển về **NV Kho + Admin** cùng xử lý. Sau xử lý, đơn đóng với **số lượng thực nhận**; phần chênh lệch tự động sinh **bản ghi thất thoát** liên kết sang III.4.

### Q-12 · Nhóm: Business / Bảo mật
- **SRS nói gì**: IV.1 (d.162) "Phân quyền **chặt chẽ** theo vai trò (RBAC)"; bảng RBAC mục I chỉ định nghĩa **quyền theo chức năng**. SRS **im lặng hoàn toàn** về **phạm vi dữ liệu** (data scope).
- **Vì sao rủi ro**: RBAC theo chức năng và RBAC theo phạm vi dữ liệu là **hai bài toán khác nhau**. Bỏ sót data scope: Sale/Đại lý (có thể là **đối tác bên ngoài** — Q-21) sẽ thấy toàn bộ đơn hàng, sản lượng của các đại lý đối thủ → **rò rỉ dữ liệu kinh doanh nghiêm trọng**. Sửa sau rất tốn kém vì phải chèn điều kiện lọc vào mọi query và mọi API.
- **Câu hỏi gửi khách hàng**: *"Về quyền xem dữ liệu: (1) Một nhân viên Sale/Đại lý có được xem đơn hàng của **Sale/Đại lý khác** không, hay chỉ xem được đơn của chính mình? (2) Nhân viên Kho chỉ được xử lý đơn thuộc **kho mình phụ trách**, hay xử lý được đơn của **mọi kho**? (3) Có cấp quản lý trung gian nào (Trưởng vùng, Quản lý Sale) cần xem dữ liệu của **cả một nhóm** Sale không?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Sale/Đại lý **chỉ xem được đơn của chính mình**. NV Kho **chỉ xử lý đơn thuộc kho được gán phụ trách** (khớp trường "Tên nhân viên kho phụ trách" tại III.5 d.146). Admin xem toàn bộ. **Không** có cấp quản lý trung gian ở phase 1.

### Q-21 · Nhóm: Business / Bảo mật
- **SRS nói gì**: Bảng RBAC (d.43) gộp **"Nhân viên Sale / Đại lý"** thành **một** vai trò duy nhất. SRS **không phân biệt** hai đối tượng này.
- **Vì sao rủi ro**: Nhân viên Sale là **người nội bộ** (có hợp đồng lao động, ràng buộc kỷ luật). Đại lý là **đối tác bên ngoài** (pháp nhân độc lập, có thể là đại lý của đối thủ). Cho hai đối tượng này chung một mức tin cậy là lỗi thiết kế bảo mật. Trách nhiệm đền bù thẻ mất (III.4) cũng khác nhau hoàn toàn. Build một role rồi phát hiện phải tách → làm lại phân quyền, migration user, có thể làm lại cả mô hình chủ sở hữu đơn hàng.
- **Câu hỏi gửi khách hàng**: *"'Nhân viên Sale' và 'Đại lý' là **cùng một nhóm người** hay là **hai nhóm khác nhau**? Cụ thể: Đại lý là **công ty/cá nhân bên ngoài** ký hợp đồng phân phối, hay là **nhân viên trong công ty**? Nếu là hai nhóm khác nhau, họ có **quyền hạn giống hệt nhau** trên hệ thống không, và **trách nhiệm đền bù khi mất thẻ** có khác nhau không?"*
- **Mức độ**: **Blocker**
- **Giả định tạm**: Thiết kế **một role `Sale/Đại lý`** đúng theo SRS **nhưng** tách sẵn thuộc tính `loại đối tượng = Nội bộ | Đại lý ngoài` trên hồ sơ user, và mọi truy vấn dữ liệu đều đi qua lớp data-scope (Q-12) → sau này tách thành 2 role không phải đập đi làm lại.

## 🟡 NHÓM QUAN TRỌNG

### Q-07 · Nhóm: Phi chức năng / Quy mô
- **SRS nói gì**: Chỉ có **đúng hai con số** trong toàn bộ tài liệu: response time **≤ 2 giây** (IV.2 d.168) và **backup hàng ngày** (IV.2 d.169). SRS **im lặng** về mọi số liệu quy mô.
- **Vì sao rủi ro**: "≤ 2 giây" **vô nghĩa nếu không biết trên bao nhiêu dữ liệu và bao nhiêu người dùng đồng thời**. Tra cứu trong 10.000 thẻ khác hoàn toàn tra cứu trong 10 triệu thẻ. Không có số → không chọn được hạ tầng, không ước lượng được chi phí server, và **không thể nghiệm thu NFR-06**.
- **Câu hỏi gửi khách hàng**: *"Để thiết kế hệ thống chạy đủ nhanh và chọn đúng quy mô máy chủ, anh/chị cho em xin vài con số ước lượng (chỉ cần áng chừng): (1) Tổng số người dùng: bao nhiêu Admin, bao nhiêu NV Kho, bao nhiêu Sale/Đại lý? (2) Số người dùng **cùng lúc** vào giờ cao điểm? (3) Trung bình **bao nhiêu đơn xuất/ngày**, ngày cao điểm khoảng bao nhiêu? (4) Hiện có **bao nhiêu thẻ trong kho** và mỗi tháng nhập thêm khoảng bao nhiêu? (5) Có **bao nhiêu kho** trên toàn hệ thống?"*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Thiết kế cho quy mô doanh nghiệp vừa: **≤ 200 user, ≤ 30 user đồng thời, ≤ 500 đơn/ngày, ≤ 5 triệu bản ghi thẻ, ≤ 20 kho**. Ghi rõ trong PRD là **giả định thiết kế chờ xác nhận**, không phải cam kết SLA.

### Q-08 · Nhóm: Dữ liệu / Vận hành
- **SRS nói gì**: IV.2 (d.169) chỉ nêu "Tự động sao lưu dữ liệu **hàng ngày**". SRS **im lặng** về retention, số bản backup, RPO/RTO.
- **Vì sao rủi ro**: Backup hàng ngày mà giữ 3 ngày hay giữ 7 năm là hai bài toán chi phí lưu trữ khác nhau hàng chục lần — đặc biệt khi có **ảnh POD** (Q-13). Chứng từ giao nhận thường có nghĩa vụ lưu trữ theo luật kế toán. Thiết kế xóa dữ liệu cũ mà khách hàng cần giữ để đối chứng → mất bằng chứng, hậu quả pháp lý.
- **Câu hỏi gửi khách hàng**: *"Dữ liệu đơn hàng và **ảnh chụp giao nhận (POD)** cần được **lưu giữ trong bao lâu** (1 năm, 3 năm, 5 năm, hay vĩnh viễn)? Công ty có quy định nội bộ hoặc yêu cầu pháp lý nào về việc lưu trữ chứng từ giao nhận không? Ngoài ra, nếu sự cố xảy ra, việc **mất dữ liệu tối đa bao lâu** là chấp nhận được (VD: mất dữ liệu của 24 giờ gần nhất)?"*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Dữ liệu đơn hàng lưu **vĩnh viễn** (không xóa, chỉ archive). Ảnh POD lưu **tối thiểu 3 năm**. Giữ **30 bản backup ngày** gần nhất. RPO = 24 giờ (khớp tần suất backup SRS đã nêu).

### Q-13 · Nhóm: Dữ liệu / Phi chức năng
- **SRS nói gì**: III.3 (d.129) "Bắt buộc đính kèm **tối thiểu 01 ảnh**". SRS chỉ nêu **cận dưới**, **im lặng** về cận trên, dung lượng, nơi lưu trữ, ràng buộc tuân thủ.
- **Vì sao rủi ro**: Không giới hạn → user upload ảnh 12MB, 20 ảnh/đơn. Với 500 đơn/ngày là ~120GB/ngày → chi phí lưu trữ bùng nổ và tải ảnh chậm, phá vỡ NFR-06. Nơi lưu (server nội bộ vs cloud nước ngoài) ảnh hưởng nghĩa vụ tuân thủ dữ liệu.
- **Câu hỏi gửi khách hàng**: *"Về ảnh chụp lúc nhận hàng: (1) Mỗi đơn cho phép upload **tối đa bao nhiêu ảnh**? (2) Hệ thống có thể **tự động nén ảnh** để tải nhanh hơn không, hay anh/chị cần giữ **ảnh gốc chất lượng cao** để làm bằng chứng? (3) Dữ liệu và ảnh được lưu trên **máy chủ của công ty (on-premise)** hay trên **dịch vụ cloud**? Có yêu cầu bắt buộc dữ liệu phải đặt **tại Việt Nam** không?"*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Tối đa **10 ảnh/đơn**, mỗi ảnh **≤ 10MB**, hệ thống **tự nén** xuống bản hiển thị nhưng **vẫn giữ file gốc**. Lưu trên **object storage đặt tại Việt Nam**. Chỉ chấp nhận JPG/PNG/HEIC.

### Q-14 · Nhóm: Phi chức năng / Bảo mật
- **SRS nói gì**: IV.1 (d.162) "Sử dụng cơ chế **JWT (JSON Web Token) hoặc OAuth 2.0**". Chữ "**hoặc**" khiến đây là **lựa chọn chưa chốt**, không phải yêu cầu.
- **Vì sao rủi ro**: Hai thứ ở hai tầng khác nhau (JWT là định dạng token; OAuth 2.0 là framework ủy quyền) — dấu hiệu SRS liệt kê buzzword chứ chưa quyết định. Nếu khách hàng thực chất cần **SSO bằng tài khoản công ty** thì bắt buộc đi hướng OAuth 2.0/OIDC, khối lượng công khác hẳn.
- **Câu hỏi gửi khách hàng**: *"Người dùng sẽ đăng nhập vào hệ thống bằng cách nào: (A) **tài khoản riêng** do hệ thống này tự quản lý (tên đăng nhập + mật khẩu), hay (B) đăng nhập bằng **tài khoản sẵn có của công ty** (Google Workspace / Microsoft 365 / hệ thống nội bộ khác)? **[Đề xuất: phương án A]** vì đơn giản và không phụ thuộc hệ thống khác. Ngoài ra có cần **xác thực 2 lớp (OTP)** cho tài khoản Admin không?"*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: **Phương án A** — tài khoản riêng, xác thực bằng **JWT** (access token + refresh token). Không SSO, không 2FA ở phase 1.

### Q-15 · Nhóm: Chức năng / Tích hợp
- **SRS nói gì**: III.2 (d.126) yêu cầu hiển thị "đầy đủ trạng thái đơn hàng (**Đã lấy hàng, Đang vận chuyển, Đến bưu cục, Đang giao...**)". Nhưng mục II chỉ định nghĩa **một** trạng thái `In Transit`. SRS **không định nghĩa quan hệ** giữa hai tập trạng thái, và dấu "..." nghĩa là danh sách **chưa đầy đủ**.
- **Vì sao rủi ro**: Không rõ đây là **trạng thái đơn của hệ thống mình** hay **trạng thái phụ do carrier trả về**. Nếu đưa 4 trạng thái này thành trạng thái chính thì state machine phình từ 5 lên 9+ và bị **phụ thuộc vào tập trạng thái của carrier** (đổi carrier là vỡ hệ thống).
- **Câu hỏi gửi khách hàng**: *"Các trạng thái như 'Đã lấy hàng', 'Đến bưu cục', 'Đang giao' là do **bên vận chuyển** cung cấp. Anh/chị muốn hiển thị chúng như **thông tin tham khảo bên trong đơn** (kiểu lịch sử hành trình), hay coi chúng là **trạng thái chính thức của đơn hàng** trong hệ thống mình? **[Đề xuất: phương án đầu]** để nếu sau này đổi đơn vị vận chuyển thì quy trình nội bộ không bị ảnh hưởng."*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Giữ **5 trạng thái chính**. Trạng thái từ carrier lưu ở **bảng lịch sử tracking riêng**, hiển thị dạng timeline bên trong đơn `In Transit`. Không đưa vào state machine chính.

### Q-16 · Nhóm: Dữ liệu / Chức năng
- **SRS nói gì**: Toàn bộ SRS chỉ nêu **đúng một** trạng thái của **thẻ**: `Báo mất - Đã đền bù` (III.4 d.142).
- **Vì sao rủi ro**: FR-14 (truy vết) yêu cầu tra bất kỳ mã thẻ nào ra đầy đủ thông tin — muốn vậy **thẻ phải là một thực thể có vòng đời riêng**. Không định nghĩa đủ trạng thái thẻ → không biết thẻ nào còn trong kho để cấp Series (Q-06), không tính được tồn kho (Q-01), và `Báo mất - Đã đền bù` trở nên lơ lửng (đã đền bù rồi thì trước đó là gì?).
- **Câu hỏi gửi khách hàng**: *"Một chiếc thẻ VETC trong hệ thống có thể ở những tình trạng nào? Đề xuất danh sách sau, nhờ anh/chị bổ sung hoặc sửa: **Còn trong kho → Đã gán vào đơn → Đang vận chuyển → Đã bàn giao cho Đại lý → Đã kích hoạt (?) → Báo mất (chưa đền bù) → Báo mất (đã đền bù) → Hỏng/Hủy**. Đặc biệt: sau khi Đại lý nhận thẻ và **bán cho khách hàng cuối**, hệ thống có cần theo dõi tiếp không?"*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Vòng đời thẻ gồm 7 trạng thái theo danh sách trên, **bỏ** "Đã kích hoạt" và **dừng theo dõi** ở mốc "Đã bàn giao cho Đại lý" (SRS không hề nhắc tới khách hàng cuối).

### Q-17 · Nhóm: Chức năng
- **SRS nói gì**: III.1 (d.120) "Hệ thống **cảnh báo HOẶC cho phép** NV kho từ chối nhanh". Chữ "hoặc" = hai hành vi khác nhau chưa chốt.
- **Vì sao rủi ro**: "Cảnh báo" (mềm) và "chặn/từ chối nhanh" (cứng) tạo ra trải nghiệm và luật nghiệp vụ khác hẳn nhau. Chặn cứng nhầm → Sale không gửi được đơn hợp lệ, phải gọi điện nhờ can thiệp.
- **Câu hỏi gửi khách hàng**: *"Khi hệ thống nghi ngờ một đơn bị trùng: nên (A) **hiện cảnh báo** nhưng vẫn cho gửi/duyệt bình thường, hay (B) **chặn không cho gửi** cho đến khi có người xác nhận? **[Đề xuất: phương án A]** vì tránh chặn nhầm đơn thật, và Nhân viên Kho vẫn là người quyết định cuối."*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: **Phương án A** — cảnh báo mềm ở cả phía Sale (lúc gửi) và NV Kho (lúc duyệt), kèm nút "Từ chối nhanh" để NV Kho xử lý một chạm.

### Q-20 · Nhóm: Chức năng / Vận hành
- **SRS nói gì**: **SRS im lặng hoàn toàn** — không có một dòng nào về thông báo (notification), email, SMS, hay push.
- **Vì sao rủi ro**: Quy trình có **2 cấp duyệt tuần tự** + 1 bước nghiệm thu. Không có thông báo → NV Kho và Admin phải **tự vào hệ thống kiểm tra** xem có đơn chờ không → đơn nằm chờ hàng giờ/hàng ngày, lead time xuất kho kéo dài, người dùng đánh giá "hệ thống mới còn chậm hơn Zalo cũ". Gap nhỏ về kỹ thuật nhưng **quyết định việc hệ thống có được dùng thật hay không**.
- **Câu hỏi gửi khách hàng**: *"Khi có đơn mới chờ duyệt, hoặc đơn được duyệt/từ chối, hoặc hàng đã giao đến — người liên quan có cần được **thông báo tự động** không? Nếu có, thông báo qua kênh nào: **thông báo trong hệ thống (chuông)**, **email**, **Zalo**, hay **SMS**? **[Đề xuất: thông báo trong hệ thống + email]** cho giai đoạn đầu vì không tốn phí và triển khai nhanh."*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Có **thông báo in-app** cho các mốc: đơn mới chờ duyệt, đơn được duyệt, đơn bị từ chối, hàng đã giao. **Email** cho các mốc quan trọng. Không SMS/Zalo ở phase 1.

### Q-23 · Nhóm: Chức năng / Vận hành
- **SRS nói gì**: **SRS im lặng** về nền tảng. Không nói web, mobile app, hay responsive.
- **Vì sao rủi ro**: II Bước 5 (d.109) yêu cầu Sale **"chụp ảnh đối soát thực tế tải lên hệ thống"** — thao tác này diễn ra **tại nơi nhận hàng**, trên điện thoại. Nếu chỉ làm web desktop thì tính năng POD (FR-11, P0) thực tế **không dùng được**, Sale sẽ chụp ảnh rồi về nhà mới upload → mất tính xác thực của bằng chứng. Ảnh hưởng lớn tới ước lượng công.
- **Câu hỏi gửi khách hàng**: *"Nhân viên Sale/Đại lý sẽ chụp ảnh và xác nhận nhận hàng **ngay tại chỗ bằng điện thoại**, đúng không ạ? Nếu vậy, anh/chị cần (A) **website hiển thị tốt trên điện thoại** (mở bằng trình duyệt, không cần cài đặt), hay (B) **ứng dụng cài đặt riêng** trên iOS/Android? **[Đề xuất: phương án A]** vì nhanh hơn, không phải chờ duyệt store, và vẫn chụp ảnh upload được bình thường."*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: **Phương án A** — web application **responsive**, tối ưu riêng cho luồng Bước 5 trên màn hình điện thoại. Không native app ở phase 1.

### Q-27 · Nhóm: Dữ liệu / Nghiệp vụ
- **SRS nói gì**: II Bước 1 (d.88) và III.1 (d.119) đều nói Sale "**chọn loại thẻ**", nhưng SRS **im lặng** về việc có những **loại thẻ nào**, và **không có FR nào** cho việc quản lý danh mục loại thẻ (III.5 chỉ có danh mục **kho**).
- **Vì sao rủi ro**: "Loại thẻ" là trường bắt buộc khi tạo đơn và là tiêu chí phát hiện trùng lặp (Q-05), nhưng không ai định nghĩa nó và không ai được giao quyền tạo/sửa nó. Hardcode danh sách vào code → mỗi lần nhà cung cấp ra loại mới lại phải sửa code và deploy lại.
- **Câu hỏi gửi khách hàng**: *"Hiện công ty đang phân phối **những loại thẻ VETC nào** (vui lòng liệt kê giúp em)? Danh sách này có **thay đổi/bổ sung theo thời gian** không? Nếu có, **ai** sẽ là người được phép thêm loại thẻ mới vào hệ thống — Admin đúng không ạ? Mỗi loại thẻ có cần lưu thêm thông tin gì không (mệnh giá, đối tượng sử dụng, giá bán...)?"*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Bổ sung **Danh mục Loại thẻ** (CRUD, quyền Admin), tối thiểu gồm: mã loại, tên loại, mô tả, trạng thái hoạt động. **Không** lưu giá/mệnh giá (SRS không nhắc tới tiền của thẻ, ngoại trừ tiền đền bù).

### Q-28 · Nhóm: Chức năng
- **SRS nói gì**: Bảng RBAC (d.41) giao cho Admin "**quản lý danh mục (kho, nhân sự)**" và "**xem báo cáo tổng hợp**" + "giám sát toàn bộ luồng dữ liệu". Nhưng mục III **chỉ chi tiết hóa danh mục KHO** (III.5), **hoàn toàn không có** mục nào cho quản lý nhân sự hay báo cáo tổng hợp.
- **Vì sao rủi ro**: Hai chức năng được hứa trong bảng vai trò nhưng không có đặc tả. "Báo cáo tổng hợp" là cụm từ có thể nở ra vô hạn. Đây là nguồn scope creep điển hình — dev làm một dashboard đơn giản rồi khách hàng nói "không phải cái này".
- **Câu hỏi gửi khách hàng**: *"Về phần **Báo cáo tổng hợp** cho Admin: anh/chị cần xem những báo cáo cụ thể nào? Ví dụ: **Tồn kho theo từng kho**, **Số đơn theo trạng thái**, **Số thẻ đã xuất theo từng Đại lý**, **Danh sách thẻ thất thoát và tình trạng đền bù**, **Thời gian trung bình từ lúc tạo đơn đến lúc giao xong**. Nhờ anh/chị đánh dấu những báo cáo **thực sự cần** và bổ sung nếu thiếu. Có cần **xuất ra file Excel** không?"*
- **Mức độ**: **Quan trọng**
- **Giả định tạm**: Phase 1 làm **4 báo cáo**: (1) Tồn kho theo kho, (2) Đơn theo trạng thái trong khoảng thời gian, (3) Sản lượng thẻ theo Đại lý, (4) Danh sách thất thoát & tình trạng đền bù. Tất cả **xuất được Excel**. Quản lý nhân sự = CRUD tài khoản người dùng cơ bản (tạo/khóa/đổi vai trò/reset mật khẩu).

## 🟢 NHÓM NÊN CÓ

### Q-18 · Nhóm: Business / Bảo mật
- **SRS nói gì**: III.5 (d.147) "có thể được cấu hình và thay đổi linh hoạt bởi Admin hoặc **NV Kho có thẩm quyền**". Cụm "có thẩm quyền" ngụ ý **có phân cấp bên trong role NV Kho**, nhưng bảng RBAC mục I chỉ có **3 role phẳng**.
- **Vì sao rủi ro**: Mâu thuẫn trực tiếp với mô hình RBAC 3 role. Nếu thực sự có "NV Kho thường" và "NV Kho trưởng" thì phải thêm role thứ 4.
- **Câu hỏi gửi khách hàng**: *"Trong nhóm Nhân viên Kho, có phân biệt **cấp bậc** không (VD: Nhân viên kho thường và Trưởng kho)? Nếu có, việc **sửa/xóa thông tin kho** chỉ dành cho Trưởng kho, còn nhân viên thường chỉ được duyệt đơn — đúng không ạ?"*
- **Mức độ**: **Nên có**
- **Giả định tạm**: **Không** phân cấp trong role NV Kho (giữ đúng 3 role). Mọi NV Kho đều có thể sửa thông tin kho **mình phụ trách**; **chỉ Admin** được tạo mới/xóa kho.

### Q-19 · Nhóm: Chức năng
- **SRS nói gì**: III.3 (d.131) "Tự động tạo file *Biên bản Bàn giao Thẻ* (định dạng **PDF/Excel**)". Dấu "/" không rõ là **cả hai** hay **chọn một**; SRS **im lặng** về mẫu biểu, nội dung bắt buộc, chữ ký/đóng dấu.
- **Vì sao rủi ro**: Biên bản bàn giao thường là **chứng từ có giá trị đối chứng**, công ty hầu như luôn có mẫu sẵn. Tự thiết kế mẫu → khách hàng bác bỏ, phải làm lại. Nếu cần chữ ký số thì khối lượng công tăng đáng kể.
- **Câu hỏi gửi khách hàng**: *"Về **Biên bản Bàn giao Thẻ**: (1) Anh/chị cần file **PDF**, **Excel**, hay **cả hai**? (2) Công ty đã có **mẫu biên bản sẵn** chưa? Nếu có nhờ anh/chị gửi em file mẫu. (3) Biên bản có cần **chữ ký số** hoặc **dấu công ty** không, hay chỉ cần in ra ký tay là đủ?"*
- **Mức độ**: **Nên có**
- **Giả định tạm**: Xuất **PDF** (để in ký tay) + **Excel** (để đối soát dữ liệu). Mẫu do đội thiết kế, gồm: mã đơn, ngày xuất/nhận, kho xuất, NV kho, Sale/Đại lý nhận, loại thẻ, số lượng, dải Series, ảnh POD, ô ký tên hai bên. **Không** chữ ký số.

### Q-22 · Nhóm: Business / Nghiệp vụ
- **SRS nói gì**: III.4 (d.141) chỉ nói "**ghi nhận số tiền**" đền bù. SRS **im lặng** về việc ai quyết định số tiền và tính theo cơ sở nào.
- **Vì sao rủi ro**: Nếu số tiền do người nộp tự gõ vào thì kiểm soát bằng không — người làm mất thẻ tự khai số tiền đền bù. Nếu có biểu giá cố định thì hệ thống nên tự tính để tránh tranh cãi.
- **Câu hỏi gửi khách hàng**: *"Khi phải đền bù thẻ mất, **số tiền đền bù** được xác định như thế nào: (A) có **biểu giá cố định** cho mỗi loại thẻ (hệ thống tự tính = số thẻ mất × đơn giá), hay (B) **thương lượng từng trường hợp** và nhập tay? Nếu là (A), nhờ anh/chị cho em xin **bảng giá đền bù** theo từng loại thẻ."*
- **Mức độ**: **Nên có**
- **Giả định tạm**: **Nhập tay** số tiền (đúng theo chữ "ghi nhận số tiền" của SRS), nhưng **bắt buộc** phải do Admin xác nhận và **bắt buộc** đính kèm chứng từ.

### Q-24 · Nhóm: Chức năng / Vận hành
- **SRS nói gì**: **SRS im lặng** — không có trạng thái `Cancelled` hay hành động hủy đơn ở bất kỳ giai đoạn nào.
- **Vì sao rủi ro**: Sale gửi nhầm đơn (sai số lượng, sai loại thẻ) và muốn hủy trước khi kho xử lý → không có cách nào ngoài nhờ NV Kho từ chối. Đơn đã duyệt nhưng chưa giao mà đại lý báo hủy → kẹt.
- **Câu hỏi gửi khách hàng**: *"Sale có được **tự hủy đơn** của mình không? Nếu có thì được hủy đến **giai đoạn nào** — chỉ khi đơn **chưa được kho duyệt**, hay hủy được cả khi đơn **đã duyệt nhưng chưa gửi đi**? Trường hợp hàng đã lên đường vận chuyển rồi thì xử lý ra sao?"*
- **Mức độ**: **Nên có**
- **Giả định tạm**: Sale **tự hủy** khi đơn còn ở `Pending Warehouse`. Từ `Pending Admin Approval` trở đi, chỉ **Admin** được hủy (kèm lý do bắt buộc). Từ `In Transit` trở đi **không cho hủy** — xử lý qua luồng sai lệch (Q-11).

### Q-25 · Nhóm: Chức năng / Vận hành
- **SRS nói gì**: **SRS im lặng** — mermaid (d.79) chỉ có một mũi tên `Shipper->>Sale: Giao hàng thực tế`, mặc định luôn thành công.
- **Vì sao rủi ro**: Giao hàng thất bại là chuyện thường ngày. Đơn sẽ kẹt vĩnh viễn ở `In Transit`, và **quan trọng hơn**: số thẻ đó đang được tính là "đã xuất kho" trong khi thực tế **đang quay về kho** → sai lệch tồn kho và sai lệch truy vết.
- **Câu hỏi gửi khách hàng**: *"Nếu bên vận chuyển **giao hàng không thành công** và **hoàn thẻ về kho**, hệ thống cần xử lý thế nào: đơn đó bị **hủy** và số thẻ được **trả lại tồn kho**, hay đơn giữ nguyên để **giao lại lần 2**? Ai là người cập nhật việc kho đã nhận lại hàng hoàn?"*
- **Mức độ**: **Nên có**
- **Giả định tạm**: Bổ sung trạng thái `Delivery Failed` → NV Kho xác nhận đã nhận hàng hoàn → đơn chuyển `Returned` (kết thúc) và **thẻ được trả lại tồn kho**. Giao lại = tạo đơn mới.

### Q-26 · Nhóm: Dữ liệu / Chức năng
- **SRS nói gì**: I (d.42) và II Bước 2 (d.92) đều nói NV Kho "**kiểm tra tồn kho**"; d.94 nói điều chỉnh SL khi "**kho không đủ tồn**". Nhưng mục III **không có FR nào** mô tả chức năng quản lý/hiển thị tồn kho, và III.5 chỉ lưu tên/địa chỉ/người phụ trách/SĐT — **không có dữ liệu tồn**.
- **Vì sao rủi ro**: "Kiểm tra tồn kho" được nhắc 2 lần như hành động bắt buộc trong luồng chính, nhưng **nguồn dữ liệu tồn kho không tồn tại** trong SRS. Hệ quả trực tiếp của Q-01. Không giải quyết thì NV Kho phải mở Excel bên ngoài để tra tồn → hệ thống mất giá trị.
- **Câu hỏi gửi khách hàng**: *"Khi Nhân viên Kho 'kiểm tra tồn kho' để quyết định duyệt đơn, họ sẽ xem số liệu tồn **ở đâu**: (A) ngay trên hệ thống mới này, hay (B) trên **file/phần mềm khác** mà công ty đang dùng? **[Đề xuất: phương án A]** — nhưng để làm được thì hệ thống phải quản lý cả việc nhập thẻ vào kho (liên quan câu hỏi Q-01 phía trên)."*
- **Mức độ**: **Nên có** (nhưng **leo lên Blocker** nếu Q-01 chốt là "có làm nhập kho")
- **Giả định tạm**: Hệ thống **có** màn hình tồn kho theo kho + theo loại thẻ, tính từ (tồn khởi tạo import Excel) − (đã xuất) + (hàng hoàn). Đây là cách tối thiểu để Q-06 và NFR-05 chống trùng Series hoạt động được.

### Q-29 · Nhóm: Business
- **SRS nói gì**: **SRS im lặng** hoàn toàn về mục tiêu đo lường được, KPI, ngân sách, ROI.
- **Vì sao rủi ro**: BRD bắt buộc phải có business objective đo đếm được. Không có → BRD chỉ là bản mô tả chức năng đội lốt tài liệu nghiệp vụ, và **không có tiêu chí nào để tuyên bố dự án thành công** khi nghiệm thu.
- **Câu hỏi gửi khách hàng**: *"Sau khi hệ thống chạy được 6 tháng, **điều gì xảy ra** thì anh/chị coi là dự án **thành công**? Ví dụ: 'giảm số thẻ thất thoát không truy được nguồn gốc từ X xuống gần 0', 'rút ngắn thời gian từ lúc Sale đặt đến lúc nhận thẻ từ X ngày xuống Y ngày', 'tra được nguồn gốc bất kỳ thẻ nào trong dưới 1 phút thay vì phải hỏi qua nhiều người'. Hiện tại mỗi tháng công ty **thất thoát khoảng bao nhiêu thẻ**, và quy trình hiện tại đang mất nhiều thời gian nhất ở khâu nào?"*
- **Mức độ**: **Nên có** (nhưng **bắt buộc** đối với chất lượng BRD)
- **Giả định tạm**: BRD ghi mục tiêu **định tính** (giảm thất thoát, minh bạch truy vết, chuẩn hóa phê duyệt) và để phần chỉ số định lượng là `TBD`. **Tuyệt đối không** điền số phỏng đoán.

### Q-30 · Nhóm: Business / Vận hành
- **SRS nói gì**: **SRS im lặng** về hiện trạng (as-is), timeline mong muốn, kế hoạch chuyển đổi dữ liệu và đào tạo.
- **Vì sao rủi ro**: Không biết đang dùng gì thì không biết phải migrate dữ liệu gì, và không biết người dùng quen thao tác nào. Không biết deadline thì không cắt được phạm vi phase 1.
- **Câu hỏi gửi khách hàng**: *"(1) Hiện tại công ty đang quản lý việc xuất kho và phân phối thẻ **bằng công cụ gì** (Excel, Google Sheet, phần mềm sẵn có, hay sổ giấy)? (2) Dữ liệu cũ có cần **chuyển vào hệ thống mới** không, và khoảng bao nhiêu dữ liệu? (3) Anh/chị mong muốn hệ thống **đưa vào sử dụng vào thời điểm nào**? (4) Có mốc thời gian bắt buộc nào (mùa cao điểm, cam kết với đối tác) không?"*
- **Mức độ**: **Nên có**
- **Giả định tạm**: Hiện trạng là **Excel + trao đổi qua Zalo/email**. Migration = **import Excel một lần** cho danh mục kho, danh sách user và tồn kho khởi tạo. Timeline `TBD`.

### Q-31 · Nhóm: Dữ liệu / Nghiệp vụ
- **SRS nói gì**: III.6 (d.155) cho phép lọc theo "**Đại lý tiếp nhận**"; II Bước 1 (d.88) đơn chỉ gồm loại thẻ + số lượng. SRS **im lặng** về việc **địa chỉ giao hàng** của đơn lấy từ đâu, và về danh mục Đại lý.
- **Vì sao rủi ro**: Muốn đẩy đơn sang carrier qua API (FR-08) thì **bắt buộc** phải có người nhận + địa chỉ + số điện thoại. SRS mô tả chi tiết thông tin **kho gửi** (III.5 d.146) nhưng **không có gì** về **bên nhận**. Thiếu trường này thì API vận chuyển không thể gọi được.
- **Câu hỏi gửi khách hàng**: *"Khi tạo đơn, **địa chỉ giao hàng** được lấy từ đâu: (A) từ **hồ sơ Đại lý** đã lưu sẵn trong hệ thống (mỗi đại lý có địa chỉ cố định), hay (B) Sale **tự nhập địa chỉ** cho từng đơn (vì có thể giao đến nhiều nơi khác nhau)? **[Đề xuất: phương án A có cho phép sửa]** — mặc định lấy địa chỉ đại lý, nhưng vẫn cho đổi nếu lần này giao chỗ khác."*
- **Mức độ**: **Nên có** (leo lên **Quan trọng** nếu Q-02 chốt là tích hợp API thật)
- **Giả định tạm**: Bổ sung **Danh mục Đại lý** (tên, mã, địa chỉ mặc định, người liên hệ, SĐT). Đơn hàng **tự điền** từ hồ sơ đại lý, **cho phép sửa** địa chỉ theo từng đơn.

## Tổng hợp Gap List

| Mức độ | Số lượng | Mã |
|---|---|---|
| 🔴 **Blocker** | **11** | Q-01, Q-02, Q-03, Q-04, Q-05, Q-06, Q-09, Q-10, Q-11, Q-12, Q-21 |
| 🟡 **Quan trọng** | **11** | Q-07, Q-08, Q-13, Q-14, Q-15, Q-16, Q-17, Q-20, Q-23, Q-27, Q-28 |
| 🟢 **Nên có** | **9** | Q-18, Q-19, Q-22, Q-24, Q-25, Q-26, Q-29, Q-30, Q-31 |
| **TỔNG** | **31** | |

**Phủ 10 điểm bắt buộc PM yêu cầu**: ① Q-01 · ② Q-02 + Q-03 · ③ Q-04 · ④ Q-05 (+Q-17) · ⑤ Q-06 · ⑥ Q-07 + Q-08 · ⑦ Q-09 + Q-10 · ⑧ Q-11 · ⑨ Q-12 (+Q-21, Q-18) · ⑩ Q-13. ✅ Đủ 10/10.

> **Ghi chú đánh số**: dãy Q-NN có khoảng trống (không có Q-32+ và thứ tự không liên tục theo mức độ) vì BA đánh số theo trình tự phát hiện rồi mới phân nhóm mức độ. Giữ nguyên mã để truy vết chéo giữa BRD, PRD và file câu hỏi.

---

# PHẦN 4 — MÂU THUẪN NỘI TẠI & ĐIỂM KHÔNG NHẤT QUÁN TRONG SRS

| # | Vị trí chính xác | Nội dung mâu thuẫn | Mức | Gap |
|---|---|---|---|---|
| **C-01** | **Tiêu đề** (d.11–12, frontmatter `title` d.8) vs **toàn bộ mục II & III** | Tiêu đề: *"HỆ THỐNG QUẢN LÝ **XUẤT NHẬP KHO** & PHÂN PHỐI THẺ VETC"*. Nhưng mục II chỉ có *"QUY TRÌNH NGHIỆP VỤ **XUẤT THẺ**"* và toàn bộ III không có dòng nào về nhập kho. **Phạm vi tên gọi ≠ phạm vi nội dung.** | 🔴 | Q-01 |
| **C-02** | **III.1 tiêu đề** (d.118) vs **III.1 nội dung** (d.119) | Tiêu đề: *"Quản lý Yêu cầu **Xuất / Nhập** Kho"*. Dòng ngay dưới: *"Cho phép Sale/Đại lý chọn loại thẻ, số lượng cần **nhập**"* — trong khi d.121 lại là *"Chỉnh sửa số lượng **xuất**"*. Chữ "nhập" ở d.119 **nhập nhằng giữa "nhập liệu" (data entry) và "nhập kho" (inbound)**. Đối chiếu II Bước 1 (d.88) — cùng nội dung nhưng **không có chữ "nhập"** → khả năng cao là **lỗi diễn đạt**. | 🔴 | Q-01 |
| **C-03** | **Mermaid d.65–70** vs mọi bước khác | Nhánh `alt ... NV_Kho->>System: Từ chối đơn` (d.66) **không có `Note over System` gán trạng thái**, trong khi tất cả nhánh khác đều có (d.63, 69, 73, 77, 81). Nhánh từ chối **cụt**. | 🔴 | Q-09 |
| **C-04** | **II Bước 3** (d.99–101) vs **nguyên tắc phê duyệt** (d.49, d.122) | SRS nhấn mạnh luồng duyệt *"2 cấp **nghiêm ngặt**"* và *"**Bắt buộc** tuân thủ"*, nhưng cấp duyệt thứ 2 (Admin) **không được trao quyền từ chối**. Cấp kiểm soát không có quyền chặn là **mâu thuẫn logic** với mục đích kiểm soát. | 🔴 | Q-10 |
| **C-05** | **III.2** (d.126) vs **mục II** (d.63–81) | III.2 liệt kê *"Đã lấy hàng, Đang vận chuyển, Đến bưu cục, Đang giao..."* — 4+ trạng thái. Mục II chỉ định nghĩa **`In Transit`**. **Hai tập trạng thái song song, không được ánh xạ**; dấu "..." cho thấy danh sách chưa đóng. | 🟡 | Q-15 |
| **C-06** | **IV.1** (d.162) | *"Sử dụng cơ chế JWT **HOẶC** OAuth 2.0"* — **lựa chọn chưa quyết**, không phải yêu cầu. JWT và OAuth 2.0 **không cùng tầng khái niệm** → dấu hiệu liệt kê thuật ngữ chứ chưa thiết kế. | 🟡 | Q-14 |
| **C-07** | **III.1** (d.120) | *"Hệ thống **cảnh báo HOẶC cho phép** NV kho từ chối nhanh"* — hai hành vi khác nhau, chưa chốt. Cùng dòng còn có *"trong **thời gian ngắn**"* — định lượng không xác định. | 🟡 | Q-05, Q-17 |
| **C-08** | **III.5** (d.147) vs **bảng RBAC** (d.37–43) | III.5: *"thay đổi linh hoạt bởi Admin hoặc **NV Kho có thẩm quyền**"* → ngụ ý **có phân cấp trong role NV Kho**. Nhưng mục I tuyên bố rõ hệ thống có *"**3 nhóm người dùng chính**"* phẳng. | 🟡 | Q-18 |
| **C-09** | **Bảng RBAC** (d.41) vs **mục III** | Admin được giao *"quản lý danh mục (kho, **nhân sự**)"* và *"xem **báo cáo tổng hợp**"*, nhưng mục III chỉ chi tiết hóa danh mục **kho** (III.5). **Hai chức năng được hứa nhưng không có đặc tả.** | 🟡 | Q-28 |
| **C-10** | **Bảng RBAC** (d.42) + **II Bước 2** (d.92, d.94) vs **III.5** (d.145–147) | Luồng nghiệp vụ yêu cầu NV Kho *"**kiểm tra tồn kho**"* và xử lý khi *"kho **không đủ tồn**"*, nhưng mô hình dữ liệu kho tại III.5 **chỉ có** Tên kho / Địa chỉ / NV phụ trách / SĐT — **không có bất kỳ dữ liệu tồn kho nào**. **Yêu cầu hành động trên dữ liệu không tồn tại.** | 🔴 | Q-26, Q-01 |
| **C-11** | **III.3** (d.130) vs **II Bước 2** (d.91–97) | III.3 nói dải Series *"**do kho cấp**"* → phải có hành động cấp Series. Nhưng liệt kê thao tác của NV Kho tại Bước 2 **không hề có bước gán Series**. **Hành động bắt buộc bị thiếu khỏi mô tả quy trình.** | 🔴 | Q-06 |
| **C-12** | **IV.2** (d.167) vs toàn bộ mô hình dữ liệu | Yêu cầu *"chặn chọn **dải series bị trùng lặp**"* — muốn chặn trùng thì hệ thống **phải quản lý được toàn bộ pool Series**. Nhưng SRS không có thực thể "Thẻ" hay "kho Series" nào. **NFR yêu cầu điều mà FR không cung cấp nền tảng.** | 🔴 | Q-16, Q-01 |
| **C-13** | **III.4** (d.141) — nội tại | *"**Tích hợp** chức năng nộp tiền đền bù"* (gợi ý cổng thanh toán) vs ba trường liệt kê ngay sau *"ghi nhận số tiền, mã giao dịch, hóa đơn đền bù đính kèm"* (đặc trưng ghi nhận thủ công). | 🟡 | Q-04 |
| **C-14** | **III.4** (d.139–142) vs **II Bước 5** (d.108–112) | Có nguyên một mục **quản lý thất thoát**, nhưng quy trình nghiệm thu **không có luồng nào phát hiện thất thoát** — Bước 5 chỉ có "xác nhận đúng" rồi [Hoàn thành]. **Có chức năng xử lý hậu quả nhưng không có cơ chế phát hiện.** | 🔴 | Q-11 |
| **C-15** | **III.3/II** (d.82, d.131) | *"PDF**/**Excel"* — dấu gạch chéo không rõ là **cả hai** hay **một trong hai**. | 🟢 | Q-19 |
| **C-16** | **Mục V — Tài liệu Tham khảo** (d.177) | SRS khai báo `Glossary.md` là *"Thuật ngữ & Từ điển hệ thống"* của mình. Nhưng `docs/999-Resources/Glossary.md` (đã verify, 13 dòng) **chỉ có 3 thuật ngữ: OTP, OTP Expiry, Rate Limit** — **không có bất kỳ thuật ngữ VETC nào**, và 3 thuật ngữ đó **không xuất hiện lần nào trong SRS**. **Tham chiếu tới nguồn hoàn toàn không liên quan.** | 🟡 | Phần 5 |
| **C-17** | **Mục V** (d.175) & **Linking convention** | SRS dùng đường dẫn tuyệt đối kiểu `/docs/999-Resources/...`, trong khi RULE-001 mục "Quy tắc liên kết" **bắt buộc dùng relative path** `[File](./File.md)`. **Vi phạm chuẩn tài liệu của chính repo.** | 🟢 | Lưu ý cho writer |
| **C-18** | **Thuật ngữ không nhất quán xuyên tài liệu** | Cùng một khái niệm dùng nhiều tên: "đơn xuất kho" (d.41) / "yêu cầu xuất thẻ" (d.49, 62) / "đơn hàng" (d.92, 126, 154) / "đơn" (d.66, 96); "Sale / Đại lý" (d.43, 56) / "Đại lý tiếp nhận" (d.155) / "Sale" (d.62); "NV Kho" (d.42) / "Nhân viên kho" (d.42, 146) / "kho" (d.130). **Chưa có Ubiquitous Language.** | 🟡 | Phần 5 |

---

# PHẦN 5 — THUẬT NGỮ ĐỀ XUẤT BỔ SUNG GLOSSARY

**Hiện trạng đã verify**: `docs/999-Resources/Glossary.md` (13 dòng) chỉ có **3 thuật ngữ**: OTP, OTP Expiry, Rate Limit — **0% phủ domain VETC**, và **không thuật ngữ nào xuất hiện trong SRS**.

> ⚠️ Mọi định nghĩa dưới đây **rút TRỰC TIẾP từ SRS**, có ghi dòng nguồn. Thuật ngữ nào SRS **dùng nhưng không định nghĩa** được đánh dấu **[CẦN KHÁCH HÀNG ĐỊNH NGHĨA]**.

## 5.1. Thuật ngữ nghiệp vụ cốt lõi (Domain)

| Thuật ngữ | Định nghĩa đề xuất (dựa trên SRS) | Nguồn / Ghi chú |
|---|---|---|
| **VETC** | ⚠️ SRS **dùng xuyên suốt nhưng KHÔNG định nghĩa** — chỉ xuất hiện trong tiêu đề (d.12) và "thẻ VETC" (d.49). | **[CẦN KHÁCH HÀNG ĐỊNH NGHĨA]** → Q-27 |
| **Thẻ VETC** | Đơn vị hàng hóa được quản lý xuất kho và phân phối; mỗi thẻ có **Mã thẻ** riêng, thuộc một **Loại thẻ**, và nằm trong một **Dải Series**. | d.49, d.88, d.130, d.150 |
| **Mã thẻ** | Định danh của một thẻ VETC riêng lẻ; là khóa để **truy xuất nguồn gốc** và là tiêu chí **Global Search**. | d.134, d.150, d.168 |
| **Loại thẻ** | Phân loại thẻ VETC mà Sale/Đại lý chọn khi tạo đơn. ⚠️ SRS **không liệt kê** các loại cụ thể. | d.88, d.119 → Q-27 |
| **Dải Series (Series Range)** | Khoảng số Series liên tục **do kho cấp** cho một đơn hàng, xác định bởi cặp ***Series bắt đầu – Series kết thúc***; là căn cứ để Sale đối soát khi nhận hàng. Hệ thống **chặn chọn dải series bị trùng lặp**. | d.130, d.110, d.167 |
| **Kho** | Đơn vị lưu trữ và xuất thẻ, quản lý trong **Danh mục kho**. Mỗi kho lưu: *Tên kho*, *Địa chỉ*, *Tên nhân viên kho phụ trách gửi hàng*, *Số điện thoại liên hệ*. | d.144–146 |
| **Danh mục kho** | Master data các kho; hỗ trợ tạo mới, chỉnh sửa, **xóa hoặc ẩn**; là nguồn để NV Kho **gán kho xuất** cho đơn. | d.145, d.95 |
| **Đơn xuất thẻ** *(chuẩn hóa)* | Yêu cầu do Sale/Đại lý khởi tạo để nhận thẻ từ kho, đi qua **luồng phê duyệt 2 cấp** và kết thúc bằng nghiệm thu tại nơi nhận. ⚠️ SRS gọi bằng **4 tên khác nhau** — đề xuất thống nhất dùng **"Đơn xuất thẻ"**. | d.41, d.49/62, d.126, d.66 → C-18 |
| **Số lượng yêu cầu** | Số lượng thẻ do Sale/Đại lý đề xuất khi tạo đơn. | d.121 |
| **Số lượng duyệt** | Số lượng thẻ NV Kho thực tế chấp thuận xuất; có thể **khác** Số lượng yêu cầu, khi khác thì **bắt buộc nhập lý do ghi chú**. | d.121, d.94 |
| **Luồng phê duyệt 2 cấp** | Quy trình **bắt buộc**: `Kho duyệt` → `Admin duyệt`. Không được bỏ qua cấp nào. | d.122, d.49 |
| **POD (Proof of Delivery)** | Bằng chứng giao nhận: **tối thiểu 01 ảnh** chụp lô thẻ thực tế do Sale/Đại lý đính kèm khi nhận hàng. | d.128–129 |
| **Biên bản Bàn giao Thẻ** | Chứng từ (PDF/Excel) được hệ thống **tự động sinh ngay khi** Sale bấm **[Hoàn thành đơn hàng]**. | d.131, d.82 → mẫu biểu: Q-19 |
| **Truy xuất nguồn gốc (Traceability)** | Khả năng tra bất kỳ mã thẻ nào ra đầy đủ: kho xuất, NV kho phụ trách, Sale/Đại lý tiếp nhận, ngày giờ xuất kho, ngày giờ nhận hàng thực tế. | d.134–138 |
| **Thất thoát thẻ** | Thẻ được **báo mất hoặc hỏng**, ghi nhận trong hệ thống và xử lý qua cơ chế đền bù. | d.133, d.140 |
| **Đền bù thẻ mất** | Việc nộp tiền/bù tiền cho thẻ mất, ghi nhận gồm: **số tiền**, **mã giao dịch**, **hóa đơn đền bù đính kèm**. | d.141 → cơ chế: Q-04 |
| **Đơn vị Vận chuyển (Shipper/Carrier)** | Đối tác vận chuyển **đã ký hợp đồng**, nhận đơn qua **API** và trả về dữ liệu tracking. Là **actor ngoài**, không thuộc 3 role RBAC. | d.125, d.59, d.75–76 → danh tính: Q-02 |
| **Mã vận đơn** | Mã do đơn vị vận chuyển cấp, hiển thị trong thông tin theo dõi của đơn. | d.126 |
| **Real-time Tracking** | Cơ chế đồng bộ vị trí/trạng thái đơn hàng từ đơn vị vận chuyển. ⚠️ SRS **không định lượng** "real-time". | d.105, d.76 → Q-03 |

## 5.2. Vai trò (Actors)

| Thuật ngữ | Định nghĩa (nguyên văn trách nhiệm từ SRS) | Nguồn |
|---|---|---|
| **Admin (Quản trị viên)** | Phê duyệt cuối cùng đơn xuất kho; quản lý danh mục (kho, nhân sự); giám sát toàn bộ luồng dữ liệu; xem báo cáo tổng hợp. | d.41 |
| **NV Kho (Nhân viên kho)** | Tiếp nhận yêu cầu; kiểm tra tồn kho; điều chỉnh số lượng xuất; chọn kho xuất hàng; quản lý thất thoát; cập nhật danh mục kho. | d.42 |
| **Sale / Đại lý** | Tạo yêu cầu xuất thẻ; theo dõi trạng thái đơn hàng; xác nhận nhận hàng (kèm hình ảnh chứng minh); tra cứu thẻ. ⚠️ SRS gộp **một** role — cần xác nhận có phải hai đối tượng khác nhau không. | d.43 → Q-21 |

## 5.3. Trạng thái đơn hàng (Order Status)

| Trạng thái | Tiếng Việt | Định nghĩa | Nguồn |
|---|---|---|---|
| `Pending Warehouse` | Chờ kho duyệt | Trạng thái ban đầu ngay khi Sale/Đại lý tạo đơn. | d.63, d.89 |
| `Pending Admin Approval` | Chờ Admin duyệt | Sau khi NV Kho đã kiểm tồn, chốt số lượng duyệt và gán kho xuất. | d.69, d.97 |
| `Ready for Shipping` | Chờ vận chuyển | Sau khi Admin phê duyệt cuối. | d.73, d.101 |
| `In Transit` | Đang vận chuyển | Sau khi đơn được đẩy sang đơn vị vận chuyển qua API. | d.77, d.106 |
| `Completed` | Hoàn thành | Sau khi Sale upload POD, đối soát Series và bấm [Hoàn thành đơn hàng]. | d.81, d.112 |
| `Rejected`, `Cancelled`, `Delivery Failed`, `Returned`, `Discrepancy` | — | **[THIẾU] — không có trong SRS**, do BA đề xuất bổ sung. **Không đưa vào Glossary cho tới khi khách hàng chốt** Q-09, Q-10, Q-11, Q-24, Q-25. | — |

## 5.4. Trạng thái thẻ (Card Status)

| Trạng thái | Định nghĩa | Nguồn |
|---|---|---|
| `Báo mất - Đã đền bù` | Trạng thái thẻ được hệ thống **tự động** cập nhật sau khi ghi nhận xong việc đền bù. | d.142 |
| *Các trạng thái khác* | **[THIẾU] — SRS chỉ nêu duy nhất trạng thái trên.** | → Q-16 |

## 5.5. Thuật ngữ kỹ thuật / phi chức năng

| Thuật ngữ | Định nghĩa (theo SRS) | Nguồn |
|---|---|---|
| **RBAC (Role-Based Access Control)** | Cơ chế phân quyền dựa trên vai trò, áp dụng cho 3 nhóm người dùng chính. | d.37, d.162 |
| **Audit Log (Nhật ký hệ thống)** | Ghi nhận toàn bộ lịch sử tác động dữ liệu (ai tạo, ai sửa số lượng, ai duyệt, thời gian cụ thể theo timestamp) phục vụ tra soát và kiểm toán. | d.164 |
| **JWT (JSON Web Token)** | Một trong hai cơ chế xác thực được SRS nêu (cùng OAuth 2.0). | d.162 → Q-14 |
| **OAuth 2.0** | Cơ chế xác thực/ủy quyền thay thế cho JWT theo SRS. | d.162 → Q-14 |
| **HTTPS (SSL/TLS)** | Giao thức bắt buộc để truyền tải dữ liệu. | d.163 |
| **Daily Backup** | Cơ chế tự động sao lưu dữ liệu hàng ngày phòng ngừa thất thoát dữ liệu thẻ. | d.169 |
| **Global Search** | Tìm kiếm nhanh theo Mã thẻ / Dải Series thẻ và Tên nhân viên (Sale, Kho, Admin). | d.150 |

## 5.6. Khuyến nghị vận hành Glossary

1. **Tách bạch hai Glossary**: `docs/999-Resources/Glossary.md` = thuật ngữ **domain nghiệp vụ VETC**; `knowledge-base/01-Metas/Glossary.md` = thuật ngữ **TNMCORE-OS**.
2. **Rà lại 3 thuật ngữ cũ** (OTP, OTP Expiry, Rate Limit): không liên quan SRS-VETC. Nếu do dự án khác để lại → nên gắn nhãn dự án hoặc chuyển đi.
3. **Chuẩn hóa C-18 trước khi viết BRD/PRD**: chốt **"Đơn xuất thẻ"** làm tên duy nhất, dùng nhất quán trong cả hai tài liệu.

---

# Ghi chú bàn giao cho bước soạn thảo

1. **BRD sẽ mỏng ở tầng business**: SRS gần như thuần chức năng. Business goal/KPI/ngân sách/timeline/stakeholder ngoài 3 role đều `TBD`. **Không được lấp bằng phỏng đoán.**
2. **PRD nên có mục "Giả định thiết kế"** liệt kê toàn bộ 31 giả định tạm ở Phần 3, mỗi giả định link tới mã `Q-NN` tương ứng — để khi khách hàng trả lời khác, biết ngay phải sửa chỗ nào (traceability).
3. **File câu hỏi khách hàng**: dùng nguyên Phần 3 nhưng **lược bỏ hoặc viết mềm lại phần "Vì sao rủi ro"** (ngôn ngữ kỹ thuật); **giữ nguyên** phần "Câu hỏi gửi khách hàng" và "Giả định tạm" — hai phần này đã viết cho người phi kỹ thuật đọc. Chia theo 3 mức độ để khách hàng ưu tiên trả lời 11 câu Blocker trước.
4. **Template PRD hiện có** (`Template-PRD.md`) thiếu 2 mục mà nội dung này cần: **State machine trạng thái** và **Giả định & Câu hỏi mở** → writer bổ sung 2 mục vào tài liệu PRD (không sửa file template dùng chung).
5. **Mục "Success Metrics" của Template-PRD**: SRS không có KPI → ghi `TBD` + link Q-29.

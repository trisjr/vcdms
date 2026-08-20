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

## E3 — Verify trả 2 CRITICAL → quay lại Bước 5 với writer mới

- **Tầng**: 2 (PM tự quyết) — đây là thủ tục đã ghi sẵn trong `pm-doc.md` Bước 6.3, không phải quyết định mở rộng scope.
- **Worker**: `context-auditor` tại phase verify, `STATUS: DONE`, `FILES_TOUCHED: none` (read-only đúng ownership).
- **Kết quả**: 2 `CRITICAL` · 3 `WARNING` · 5 `SUGGESTION` · 1 hạng mục không kiểm được. Chi tiết đầy đủ tại `verdict.md`.

### Điều đáng ghi nhất: một trong hai CRITICAL là lỗi của PM

`CRITICAL 1` (mã `FR-27` / `FR-31` bịa) có **root cause tại `outline.md` L64 do chính PM viết**. Writer trước chỉ tuân thủ outline — và còn chủ động ghi cảnh báo *"KHÔNG phải FR chính thức trong danh sách 25 FR"* ngay trong deliverable, tức nó **đã nhận ra sự bất thường nhưng không được phép sửa outline** (đúng ràng buộc ownership PM đã cấp).

Đây là bằng chứng cho giá trị của việc verify bởi agent thứ ba: writer không thể tự bắt lỗi này vì lỗi nằm trong chỉ thị nó nhận, còn PM không tự bắt được vì PM là người tạo ra nó.

**Quy tắc rút ra, đã ghi vào `outline.md`**: trong outline, **chỉ được viết chuỗi `FR-NN` cho mã thực có trong PRD**. Giả định thiết kế phải gọi bằng mã `Q-NN`, không được đội lốt mã FR. Số của mã câu hỏi và số của mã yêu cầu là hai không gian định danh khác nhau — trộn chúng là cách sinh ra mã không tồn tại mà trông rất thật.

### `CRITICAL 2` — vì sao PM không tự vá

`CRITICAL 2` (Phương án A khai `≈32–35 MD` trong khi sàn truy được là `50,5 MD`) là lỗi **ước lượng**, thuộc chuyên môn của writer. PM đã tự cộng lại để **xác nhận verifier đúng** trước khi dispatch, nhưng không tự sửa con số — vì việc tính lại kèm bảng đối soát Task ID là việc của người ước lượng, và `pm-doc.md` Bước 6.3 nói rõ: *"Không tự vá rồi tuyên bố xong."*

Đồng thời PM giao writer mới một quyết định thật, không chỉ sửa số: **xem lại có còn nên giữ nhãn `⭐ Em đề xuất` cho Phương án A hay không** — vì nếu số liệu vừa bác bỏ luận điểm khả thi của nó thì giữ nhãn đề xuất là tự lừa.

- **Hành động**:
  1. PM sửa `outline.md` L64 + ghi quy tắc rút ra (đã làm).
  2. Dispatch `product-owner` **MỚI** với toàn văn 2 CRITICAL + 3 WARNING + 5 SUGGESTION, kèm **bảng cộng lại của PM** để writer không phải tự dò.
  3. PM đồng bộ `Proposal-VETC.html` **sau khi** có con số mới — vì bản HTML đang publish mang nguyên con số sai.
  4. PM ghi ngoại lệ naming convention cho `WBS-ETA-VETC.md` vào `Planning-MOC.md` (SUGGESTION S5).
- **Tier không đổi**: vẫn T2. Đây là vòng sửa trong phạm vi Bước 5–6, không phải leo tier.

## E4 — Anh đổi scope SAU khi run đã đóng: thêm chiều ước lượng AI-assisted

- **Tầng**: 3 (anh quyết). Đây là **thay đổi scope do anh khởi xướng**, không phải sửa lỗi.
- **Thời điểm**: sau khi PM đã báo cáo kết thúc run và push branch. **Lần `result:` trước bị thay thế** — run này có lần đóng thứ hai.
- **Yêu cầu nguyên văn của anh**:
  > *"Vì dự án này sẽ phát triển bằng claude (coding kết hợp AI) nên anh nghĩ cần tinh chỉnh lại man-day. Em nghĩ sao?"*

- **Hai câu PM hỏi lại và câu trả lời của anh** (nguyên văn lựa chọn):
  1. *"10.000.000 VND là chi phí gì?"* → **"Chi phí nhân công thuê ngoài"**.
     ⇒ **`E-02` ĐÃ CÓ CÂU TRẢ LỜI.** Phép quy đổi `VND/MD` và bảng độ nhạy đơn giá ở mục 5.3.b **vẫn còn hiệu lực** — phải **tính lại** trên con số MD mới, **không được bỏ**. PM đã đoán sai khi cho rằng 10 triệu có thể là chi phí công cụ/hạ tầng.
  2. *"Trình bày con số AI-assisted thế nào?"* → **"Thêm cột song song, giữ cột cũ"**.
     ⇒ Không ghi đè cột `Effort (MD)` gốc. Không tách file riêng.

- **Quyết định của PM**: **tiếp tục trong run hiện tại**, không mở run mới. Lý do: cùng cặp deliverable, cùng ownership map đã duyệt tại gate, cùng nguồn sự thật. Mở run mới sẽ phân tán dấu vết của cùng một cặp file thành hai chỗ.

- **Assumption MỚI phát sinh**:
  - **A-11** — **Nhà thầu thuê ngoài thực sự dùng Claude khi phát triển.**
    Căn cứ: lời anh *"dự án này sẽ phát triển bằng claude (coding kết hợp AI)"*.
    → **sai thì hỏng ở đâu**: hệ số AI **vô hiệu hoàn toàn**, và cột `MD truyền thống` là con số phải trả. Đây chính là lý do phương án "thêm cột song song" mà anh chọn có giá trị thật — nếu nhà cung cấp không dùng AI thì bảng vẫn dùng được, không phải làm lại.
  - **A-12** — Hệ số AI là **một tầng giả định mới xếp trên tầng giả định cũ**. Con số `MD AI-assisted` vì vậy có **độ tin cậy thấp hơn** cả `MD truyền thống`, vốn đã là ước lượng chờ xác nhận. Phải ghi nhãn phân biệt rõ trong cả hai deliverable.
    → **sai thì hỏng ở đâu**: nếu trình bày cột AI-assisted ngang hàng độ tin cậy với cột cũ, người đọc sẽ dùng nó làm cam kết — đúng loại lỗi mà `CRITICAL 2` của run này vừa bị bắt.

- **Câu còn mở**: `E-01` (quy mô đội) và **`E-03` (đơn giá thuê ngoài thực tế)**. Sau khi `E-02` được trả lời, **`E-03` trở thành ẩn số then chốt nhất** — vì ngân sách 10 triệu giờ đã xác định là tiền nhân công, nên tính khả thi phụ thuộc trực tiếp vào đơn giá.

- **Rủi ro PM tự nhận diện và cách phòng**: PM đã tự tính nhẩm sơ bộ một khoảng hệ số và con số tổng để trả lời câu hỏi của anh. **Tuyệt đối không đưa các con số đó vào prompt dispatch** — làm vậy là *anchor* ước lượng của writer vào con số PM đoán trước, tức là phiên bản đảo ngược của đúng lỗi bóp số mà `CRITICAL 2` vừa phát hiện. Prompt chỉ đưa **băng hệ số** và **danh sách nhóm bị chốt ở hệ số 1,0**; writer sở hữu con số cuối và phải kèm lý do từng nhóm.

- **Hành động**:
  1. PM cập nhật `outline.md` — pin rõ **hệ số sống ở đâu** (§4 per-nhóm và §7.2 per-mắt-xích), tránh writer rải hệ số lên 60 dòng task khiến verify không cộng nổi.
  2. Dispatch `product-owner` mới.
  3. Dispatch `context-auditor` verify — **bắt buộc**, vì hai cột số học song song đúng là remit của nó, và `product-owner` không có `Bash` nên không ai cộng bằng tool cho đến khi verifier làm.
  4. PM đồng bộ `Proposal-VETC.html`, cập nhật `Planning-MOC.md` + `000-Index.md` (hai file này đang hardcode `72,5 MD`).

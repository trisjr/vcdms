# Verdict: 2026-08-20-wbs-eta-va-proposal-vetc

**Verifier**: `context-auditor` — agent thứ ba, không phải writer đã soạn file. Read-only tuyệt đối (`FILES_TOUCHED: none`).
**Đối tượng verify**: `docs/010-Planning/Estimates/WBS-ETA-VETC.md`
**Ngày**: 2026-08-20

> [!NOTE]
> `Proposal-VETC.html` do PM tự viết nên không có agent thứ ba verify — PM tự chạy Validation Checklist của RULE-001 và tự audit CSS. Ghi rõ giới hạn này thay vì để người đọc sau tưởng cả hai deliverable đều đã qua verify độc lập.

## Tổng kết

| Mức | Số lượng |
|---|---|
| `CRITICAL` | **2** |
| `WARNING` | 3 |
| `SUGGESTION` | 5 |
| Không kiểm được | 1 |

**Kết luận của verifier**: file dùng được làm nguồn ở §1–§4 và §6–§9, **nhưng §5.4 Phương án A chứa con số không truy được** và con số đó **đã nhiễm sang `Proposal-VETC.html` đang publish**.

---

## Phần ĐẠT — đã kiểm thật, không suy đoán

Verifier cộng lại toàn bộ số học bằng `awk`, không nhẩm. PM đã spot-check độc lập các số then chốt và xác nhận.

| Tiêu chí | Kết quả |
|---|---|
| §2 tổng CORE = 72,5 MD | ✅ cộng 38 dòng → đúng |
| §3 tổng BỔ SUNG = 39,5 MD | ✅ cộng 22 dòng → đúng |
| §4 khớp §2/§3 theo **từng nhóm** | ✅ khớp tuyệt đối 14/14 nhóm, cả 2 cột |
| **Danh sách 17 mã P0 mà PM đưa** | ✅ **PM ĐÚNG** — verifier tự grep lại cột Ưu tiên PRD §4 + §5.1, khớp 100% |
| Phép chia tầng CORE / BỔ SUNG | ✅ đúng 17 mã trong CORE, **không mã P0 nào lọt xuống BỔ SUNG** |
| Gán nguồn `10.000.000 VND` / `10 ngày` | ✅ **làm rất chuẩn** — gán cho ràng buộc khách hàng tại gate, kèm cảnh báo tường minh là KHÔNG có trong PRD/BRD/SRS |
| Không bóp số cho khớp ràng buộc | ✅ §0.6 khai bottom-up trước; §5.3 nói thẳng *"VƯỢT ràng buộc 10 ngày"* |
| §6 trích nguyên văn câu cấm của PRD | ✅ `diff` → giống **từng byte** (chỉ khác đường dẫn link, bắt buộc rewrite cho cross-file) |
| FR-24/FR-25 = `TBD`, vắng khỏi §2/§3 | ✅ |
| Wiki-link `[[...]]` | ✅ 0 kết quả |
| 6 markdown link ngoài file | ✅ `ls` từng đích → cả 6 resolve |
| Completeness §0…§9 | ✅ 10 heading đúng thứ tự · 14/14 nhóm · 62 task con (min 3/nhóm) · 100% Owner hợp lệ · đủ 25 FR + 7 NFR · §5 đủ 4 khối + **5** phương án, mỗi phương án đủ 3 trường |
| Frontmatter | ✅ 6/6 trường |
| Không có ngày dương lịch trong lịch trình | ✅ chỉ `D1…D10` và `W+1…W+6` |

Các con số dẫn xuất cũng được cộng lại và **đều đúng**: `112 MD` · `30 MD (41%)` · `62,5 / 52,5 / 32,5 MD` · `7,25 người` · `138.000 VND/MD` · toàn bộ bảng độ nhạy (`33/20/10/5 MD`, `46/28/14/7%`) · `36.250.000` &amp; `72.500.000 VND` (3,6× &amp; 7,25×) · Phương án E `16 MD` &amp; `625.000 VND/MD` · đường găng `22,5 MD` · RT-02 `74,5 MD`.

## Xác nhận độc lập hai phát hiện của writer

- **RT-02 — ĐÚNG**, có 3 bằng chứng độc lập từ PRD: FR-08 là `P1` (§4); phép chuyển `Ready for Shipping → In Transit` **chỉ có duy nhất FR-08 làm chủ** (§6.1 mermaid); Bước 5 (FR-11, FR-12 — cả hai `P0`) có trạng thái đầu vào là `In Transit` (§7.1). ⇒ tầng P0 thuần **không đóng được vòng đời đơn**. Giải pháp writer đề xuất (kéo task 7.1 adapter thủ công, 2 MD, vào CORE → 74,5 MD) đúng cả logic lẫn số học.
- **RT-04 — ĐÚNG**. FR-01 (`P0`) yêu cầu *"chọn loại thẻ"*; Danh mục Loại thẻ chỉ là giả định `Q-27`, writer xếp ở tầng BỔ SUNG ⇒ CORE buộc dùng seed cứng. Một lưu ý: việc xếp `Q-27` xuống BỔ SUNG là **quyết định phân tầng của writer** (Q-27 không có mức ưu tiên trong PRD), không phải ràng buộc PRD — nhưng kết luận vẫn đúng.

---

## 🔴 CRITICAL 1 — Hai mã FR bịa

**Vị trí**: `WBS-ETA-VETC.md` L112, L113 — cột `FR/NFR liên quan` của task 5.3 và 5.4.

**Vấn đề**: ghi `FR-27` và `FR-31`. Hai mã này **không tồn tại** — PRD chỉ có `FR-01…FR-25`. Chúng bị vay từ mã câu hỏi `Q-27` / `Q-31`. Nguy hiểm vì `FR-24`/`FR-25` *có* thật nên người đọc mặc định `FR-27`/`FR-31` cũng thật.

**Root cause là lỗi của PM, không phải của writer.** `outline.md` L64 do PM viết đã ghi sẵn `FR-18, FR-19, FR-27, FR-31, FR-24*`. Writer chỉ tuân thủ outline — và còn chủ động ghi cảnh báo *"KHÔNG phải FR chính thức trong danh sách 25 FR"* ngay trong cột Task Name, tức writer đã nhận ra sự bất thường nhưng không được phép sửa outline.

**Điểm tốt**: verifier grep `Proposal-VETC.html` → hai mã này **không lọt vào bản HTML**.

**Xử lý**:
- PM đã sửa `outline.md` L64 (bỏ chuỗi mã bịa, gọi bằng `Q-27`/`Q-31`) và ghi thêm quy tắc rút ra ngay trong outline.
- Dispatch writer MỚI sửa deliverable — không tự vá.

## 🔴 CRITICAL 2 — Con số Phương án A không truy được, mâu thuẫn với chính §2/§4

**Vị trí**: `WBS-ETA-VETC.md` L351–L352, §5.4, khối Phương án A — **chính là phương án được gắn nhãn đề xuất**.

**Vấn đề**: khai *"còn ≈ 32–35 MD (giảm ≈ 38 MD): khả thi trong 10 ngày với đội 4 người"*. Con số 38 MD không đối soát được với bất kỳ dòng nào trong §2/§4.

**PM đã tự cộng lại và xác nhận verifier đúng:**

| Hạng mục A nêu cắt | Task ID | MD |
|---|---|---|
| FR-02 kiểm tra tồn kho | 6.2 | 2,5 |
| FR-14 mô hình thực thể Thẻ/Series | 9.1 | 2,5 |
| FR-14 màn hình truy xuất | 9.2 | 2 |
| NFR-05 chặn trùng Series | 11.4 | 2 |
| NFR-04 Audit Log | 11.3 | 2 |
| Design system | 3.3 | 2 |
| **Cắt trắng** | | **13 MD** |

`72,5 − 13 = 59,5 MD`. A còn nói *"QA chỉ test luồng chính"* — **làm mỏng, không xóa**. Cả nhóm 12.0 tầng CORE = `12.1 (3) + 12.2 (4) + 12.3 (2) = 9 MD`; **kể cả xóa sạch 100% QA** (điều A không làm): `59,5 − 9 = 50,5 MD`.

→ **Sàn tuyệt đối truy được là 50,5 MD**, thiếu **~16–18 MD không có nguồn** so với mục tiêu 32–35 MD. Không vá được bằng lập luận "cắt tỉ lệ": A ghi rõ *"Giữ nguyên toàn bộ nhóm 1.0 Discovery"* (4,5 MD) và giữ 13/17 hạng mục P0.

**Hệ quả load-bearing**: kết luận khả thi của A dựa trên `4 người × 10 ngày = 40 MD`. Ở mức thực tế thì **40 MD không đủ** → **luận điểm cốt lõi của phương án được đề xuất sụp**. Đây đúng là con số anh dùng để quyết ngân sách.

**Đã nhiễm sang bản HTML**: `Proposal-VETC.html` mang nguyên `≈32–35 MD … khả thi trong 10 ngày với đội 4 người, hoặc ≈8 tuần với 1 người`. Cũng đã lan: `12–16`, `57–61`, `9 người` (3 lần), `8 tuần`.

**Xử lý**: dispatch writer MỚI tính lại, kèm yêu cầu **thêm bảng liệt kê Task ID → MD cắt** để đối soát được, và **xem lại có còn nên giữ nhãn đề xuất cho A hay không**. PM đồng bộ bản HTML sau khi có con số mới.

---

## 🟡 WARNING

| # | Vấn đề | Xử lý |
|---|---|---|
| W1 | **Phạm vi tuyên bố "là ước lượng" hẹp hơn phạm vi số liệu thực có.** §0.6 chỉ tuyên bố cho *cột* `Effort (MD)`, nhưng file còn nhiều số MD ngoài cột đó (`+15 đến +20`, `10–20`, `≈5–6`, `+1,5`, `+1`, `≈12–16`, `≈57–61`, `≈68`). Một số truy được (`10–20 MD` = 2 MD × *"gấp 5–10 lần"* theo PRD §9 Q-04 — verified nguyên văn), một số không (`≈5–6`, `+1`, `≈12–16`). | Writer mới mở rộng phạm vi tuyên bố ra **toàn tài liệu**, gắn `[SUY LUẬN]` cho delta chưa có căn cứ. |
| W2 | **Thuật ngữ bị Glossary loại bỏ.** L487 (§8.2, dòng Q-11) dùng *"mô hình dữ liệu **đơn hàng**"*. Glossary chốt **"Đơn xuất thẻ"** và nêu đích danh *"đơn hàng"* là một trong 4 tên bị loại (mã C-18). Verifier xác nhận đây là **vị trí duy nhất** vi phạm. | Writer mới sửa thành *"Đơn xuất thẻ"*. |
| W3 | **Phương án A tự mâu thuẫn về quy đổi tuần.** *"≈32–35 MD … hoặc ≈ 8 tuần với 1 người"* — lấy chính 32–35 MD thì ra 6,4–7 tuần. Cùng file, §5.3 lại quy đổi đúng chuẩn 5 ngày/tuần. | Xử lý cùng CRITICAL 2. |

## 🔵 SUGGESTION

| # | Nội dung | Xử lý |
|---|---|---|
| S1 | **"≈26 MD" ở đỉnh tải D6–D8 không tái lập được.** 10 task mà L212 liệt kê cộng lại = 20 MD. Con số 26 chỉ đạt nếu tính thêm phần D8 của task `12.2` — task này bị thiếu trong danh sách. Dẫn xuất "≈ 9 người" lan sang 3 chỗ khác. | Writer mới thêm `12.2` vào danh sách hoặc hạ xuống `≈ 8–9 người`. |
| S2 | **RT-02 chưa nêu hết lỗ hổng Bước 5.** Ngoài FR-08, PRD §7.1 còn gán **FR-13** (Biên bản Bàn giao tự động) cho Bước 5; FR-13 là `P1` → CORE cũng không thực thi được **BR-05**. | Writer mới nêu chung với RT-02. |
| S3 | **§7.3 suy luận mạnh tay**: *"22,5 MD tuần tự → tối thiểu ≈22–23 ngày"* giả định mỗi mắt xích không chia được người; thực tế `12.2` (4 MD) chia được cho 2 QA. Kết luận *"10 ngày bất khả thi"* vẫn đứng. | Writer mới thêm caveat, giữ kết luận. |
| S4 | **§8.1 "≈68 MD" hơi lạc quan**: = `72,5 − 4,5` (xóa trọn nhóm 1.0), nhưng task `1.2` (chốt 8 nhánh `T-a…T-h`) phụ thuộc `Q-24, Q-25, Q-15, Q-16` — **4 mã này không nằm trong 11 Blocker**. | Writer mới thêm caveat. |
| S5 | **Ghi ngoại lệ naming convention.** RULE-001 quy định WBS → `WBS-{ProjectName}.xlsx`; file thực tế là `WBS-ETA-VETC.md`. Đây là quyết định gate (QĐ-01). | PM đã ghi ngoại lệ tương tự cho `Proposal-VETC.html` trong `Planning-MOC.md`; bổ sung cho cả WBS. |

## ⚪ Không kiểm được — báo trung thực

- **Anchor nội bộ có emoji.** Link `](#5-️-phân-tích-khoảng-cách-gap-analysis)` trỏ tới heading `## 5. ⚠️ Phân tích khoảng cách (Gap Analysis)`. Các renderer (GitHub / Obsidian / VS Code) slug hóa `⚠️` (U+26A0 U+FE0F) khác nhau và **không có ground truth trong repo** để đối chiếu. Verifier từ chối ghi "đạt" cho tiêu chí không kiểm được — đúng yêu cầu.
  → **Xử lý**: writer mới bỏ emoji khỏi heading §5 và sửa mọi anchor trỏ tới nó. Cách này triệt tiêu vấn đề thay vì đánh cược vào renderer.

## Phát hiện ngoài phạm vi audit — ghi lại để không mất

- **`docs/999-Resources/Glossary.md`** — dòng `**VETC**` ghi *"Chưa được định nghĩa"* và trỏ mã **`Q-27`**. Nhưng `Q-27` là *"Bổ sung Danh mục Loại thẻ"* (PRD §9), không liên quan việc định nghĩa VETC. **Glossary trỏ sai mã Q.** Ngoài scope run này — không sửa ở đây, ghi lại để một run sau xử lý.
- **Deliverable của task 5.5 / 10.5** ghi `` `TBD` — chờ Q-28 `` thay vì Deliverable cụ thể. Verifier **không tính là lỗi**: ghi cụ thể sẽ vi phạm chính câu cấm của PRD §4. Ngoại lệ chính đáng, 2/62 dòng lệch có lý do.
- **MOC / Index**: verifier ban đầu bắt được thiếu tham chiếu, nhưng kiểm lại lần hai thì PM đã cập nhật xong nên **đã tự rút lại finding**. Không còn orphan.

---

## Vòng sửa — writer mới (`product-owner` #2)

Writer mới trả `STATUS: DONE`, `FILES_TOUCHED` đúng một file được cấp. Sửa tại chỗ cả 8 hạng mục, không viết lại file.

### Kết quả CRITICAL 2 — và ba phát hiện thêm

Con số mới của Phương án A, **PM đã cộng lại và xác nhận đúng**:

| Mốc | Cách cộng | MD |
|---|---|---|
| Cắt trắng (truy được 100% theo Task ID) | `72,5 − 13` | **59,5** |
| Cắt trắng + làm mỏng **[SUY LUẬN]** | `59,5 − 2,2` (12.1 −0,7 · 12.2 −0,7 · 2.2 −0,5 · 3.1 −0,3) | **≈57** |
| Sàn tuyệt đối (xóa sạch 100% QA — điều A không làm) | `59,5 − 9` | **50,5** |
| A + vá RT-02 (kéo task 7.1 vào CORE) | `57 + 2` | **≈59** |

Quy mô đội: `59,5 ÷ 10 ≈ 6 người` · `57 ÷ 10 ≈ 5,7 người` — **không phải 4 người**.

**Phương án A đã bị tước nhãn `⭐ Em đề xuất`**, heading đổi thành `⚠️ KHÔNG còn khả thi trong 10 ngày`. Nhãn chuyển sang **Phương án E** (16 MD, khả thi vì `16 ≤ 20 MD` = năng lực 2 người × 10 ngày, và là phương án duy nhất có con số tự tái lập).

**Ba phát hiện writer tìm thêm ngoài danh sách PM giao — đều làm A yếu thêm, không mạnh thêm:**

1. **Đường găng dưới A còn 18 MD tuần tự.** A chỉ cắt được 2 mắt xích (`9.1` 2,5 + `11.4` 2) khỏi đường găng 22,5 MD → `22,5 − 4,5 = 18 MD` ≈ 18 ngày. Vậy A vượt 10 ngày **cả về tổng effort lẫn về cấu trúc phụ thuộc** — hai lý do độc lập nhau. Đây là lập luận chặn A dứt điểm, không phụ thuộc con số MD.
2. **A chưa vá được RT-02.** A tuyên bố *"Sale nhận hàng ở Bước 5"* nhưng CORE không có đường `Ready for Shipping → In Transit`. Phải kéo `7.1` vào → ≈59 MD.
3. **Bảng "cắt trắng" 13 MD tự nó đã lạc quan.** Theo đúng lời văn của A thì `11.3`, `11.4`, `3.3`, `6.2` là *làm mỏng chứ không xóa* — riêng `6.2`, màn hình soát xét **vẫn phải tồn tại** cho `FR-04/05/06`. Nên 13 MD phải đọc là *"tối đa cắt được"*, và **≈57 MD là sàn lạc quan, không phải trần**.

### Kết luận mới, quan trọng nhất của cả run

> **Không có phương án nào vừa go-live được sau 10 ngày, vừa nằm trong ngân sách 10.000.000 VND.** Ba ràng buộc — phạm vi CORE · 10 ngày · 10.000.000 VND — **không thể cùng thỏa mãn**. Bắt buộc phải nhả một ràng buộc; E là phương án nhả có cái giá nhỏ nhất và minh bạch nhất.

Lộ trình writer đề xuất: **E trước** (Giai đoạn 0, 16 MD) → **ước lượng lại** (`72,5 − 16 = 56,5 MD` còn lại, chưa gồm FR-24/FR-25) → **sprint go-live** theo hình dạng A, cân nhắc kết hợp D, với điều kiện *"mọi MD cắt phải chỉ ra Task ID"* và *"không đặt mốc trước rồi bóp số cho vừa"*.

### Hạn chế của vòng sửa — ghi trung thực

Writer mới **không có tool `Bash`** trong phiên của nó nên không chạy được `awk`/`grep` để cộng. Nó bù bằng cách cross-check với bảng §4 đã được verifier xác nhận ĐẠT, và viết phép cộng hiện rõ trong tài liệu để người đọc tự đối soát. **PM đã tự cộng lại toàn bộ con số mới bằng Bash và xác nhận đúng hết** — nên hạn chế này không để lại rủi ro. Việc verify sự tồn tại mã `FR`/`Q`/`BR` writer dùng Grep tool nên vẫn đủ chặt.

Writer cũng **từ chối cộng ra con số A+D**, lý do: `≈12–16 MD` của D chưa truy được ra Task ID và D còn trùng `3.3`/`11.3` với A — cộng vào sẽ tạo một con số *giả chính xác*, đúng lỗi vừa xảy ra. PM đồng ý với quyết định này.

## Trạng thái xử lý

| Lỗi | Trạng thái |
|---|---|
| CRITICAL 1 — root cause tại `outline.md` | ✅ PM đã sửa + ghi quy tắc rút ra |
| CRITICAL 1 — deliverable `WBS-ETA-VETC.md` | ✅ writer mới sửa · PM grep xác nhận `FR-(2[6-9]\|3[0-9])` = **0 kết quả** |
| CRITICAL 2 — `WBS-ETA-VETC.md` §5.4 | ✅ writer mới sửa · thêm 2 bảng đối soát Task ID + §5.5 mới · PM cộng lại xác nhận đúng |
| CRITICAL 2 — đồng bộ `Proposal-VETC.html` | ✅ PM đã đồng bộ + republish (`v3-post-verify`) |
| W1 phạm vi tuyên bố ước lượng | ✅ mở rộng ra toàn tài liệu + bảng phân loại 3 mức truy được |
| W2 thuật ngữ `đơn hàng` | ✅ PM grep xác nhận **0 kết quả** |
| W3 quy đổi tuần sai | ✅ xử lý cùng CRITICAL 2 |
| S1 đỉnh tải 26 MD | ✅ thêm `12.2` vào danh sách + phép cộng hiện rõ |
| S2 RT-02 thiếu FR-13 | ✅ bổ sung `FR-13` + `BR-05` |
| S3, S4 caveat | ✅ đã thêm, kết luận giữ nguyên |
| S5 ngoại lệ naming trong MOC | ✅ PM đã ghi cả 2 ngoại lệ (WBS `.md` gộp + Proposal `.html`) |
| Anchor emoji | ✅ bỏ `⚠️` khỏi heading §5 · PM grep xác nhận `#5-️` = **0 kết quả** |

### PM kiểm lại sau vòng sửa

| Kiểm | Kết quả |
|---|---|
| `grep -cE "FR-(2[6-9]\|3[0-9])"` trên WBS | **0** ✅ |
| `grep -ci "đơn hàng"` trên WBS | **0** ✅ |
| `grep -c "#5-️"` trên WBS | **0** ✅ |
| `⭐` trong WBS | chỉ còn ở heading Phương án E ✅ |
| Frontmatter `updated: 2026-08-20` | có ✅ |
| Số học Phương án A mới (13 · 2,2 · 59,5 · 57 · 50,5 · 18 · 59) | PM cộng lại — **đúng hết** ✅ |
| Số học Phương án E (`4,5+6,5+2+1,5+1,5 = 16`) | **đúng** ✅ |
| `72,5 − 16 = 56,5` · `10.000.000 ÷ 57 ≈ 175.000` · `10.000.000 ÷ 16 = 625.000` | **đúng hết** ✅ |
| `Đội đề xuất` trong HTML | chỉ còn ở E ✅ |
| `32–35` trong HTML | chỉ còn ở đoạn giải thích vì sao con số đó sai ✅ |
| `8 tuần` trong HTML | **0** ✅ |

## Kết luận cuối

**Không còn lỗi `CRITICAL`.** Cả hai deliverable dùng được. Run đóng được.

Hạng mục duy nhất còn để mở là phát hiện **ngoài phạm vi**: `Glossary.md` trỏ sai mã `Q-27` cho dòng định nghĩa `VETC`. PM cố ý **không sửa** — nó thuộc tầng `999-Resources`, không nằm trong ownership map đã duyệt tại gate, và sửa ngầm là mở rộng scope không qua gate. Ghi lại ở đây để một run sau xử lý.

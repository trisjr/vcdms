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

---

# Vòng verify thứ hai — chiều AI-assisted (E4)

**Verifier**: `context-auditor` (cùng agent đã audit vòng một — nó đã tìm ra 2 CRITICAL lần đó). Read-only, `FILES_TOUCHED: none`.
**Đối tượng**: `WBS-ETA-VETC.md` sau khi writer thêm cột `MD AI-assisted`.

## Tổng kết

| Mức | Số lượng |
|---|---|
| `CRITICAL` | **0** |
| `WARNING` | 4 |
| `SUGGESTION` | 8 |
| Không kiểm được | 2 (đã ghi rõ lý do) |

**Cả hai `CRITICAL` của vòng một đều KHÔNG tái phát**: 0 mã `FR` ngoài dải `FR-01…FR-25`; con số Phương án A truy được 100% theo Task ID.

## Số học — ĐẠT hoàn toàn

Verifier cộng/nhân lại bằng `awk`: 38 dòng task §2, 22 dòng §3, 14 nhóm × 2 tầng ở §4, 6 dòng phân rã 12.0, 8 mắt xích §7.2, toàn bộ phép chia đơn giá và ~40 con số dẫn xuất.

| Kiểm | Kết quả |
|---|---|
| §2 = 72,5 · §3 = 39,5 (cột cũ **không bị xô lệch**) | ✅ — chứng minh bằng `git diff 1aef29f d616ae5`: **0 dòng task bị chạm** |
| 14 ô §4 khớp rollup từ §2/§3 theo prefix nhóm | ✅ 14/14 cả hai cột |
| 28 phép nhân `MD AI = MD × hệ số` | ✅ đúng 100% quy tắc bậc 0,25 tie-up |
| Tổng cột AI: 56,75 / 29,5 · cả hai tầng 86,25 | ✅ |
| Hệ số suy ra `0,7828 → 0,78` và `0,7468 → 0,75` | ✅ |
| §7.2 đường găng = 18,75 · hệ số hiệu dụng 0,8333 | ✅ |
| Mắt xích 7 tự đóng `1,75+1,5+2 = 5,25` · `5,25÷6 = 0,875` | ✅ |
| Phép tách 12.2: `2,5 + 1,5 = 4` = giá trị gốc §2 | ✅ |
| Sàn cứng `12,5 MD` → `0,17` → `800.000 VND/MD` | ✅ |
| Phương án A = 44,75 (truy được từng bước) · sàn 39,25 · vá RT-02 46,5 · đường găng A 15 · 223.000 VND/MD | ✅ |
| Phương án E = 13 · hệ số 0,8125 → 0,81 · 769.000 VND/MD · đường găng trong E 5 MD | ✅ — và writer tính **per-nhóm**, không áp hệ số tổng (áp hệ số tổng sẽ ra 12,5, khác 13) |
| Dải bất biến 176.000–276.000 — biên trên ứng hệ số 0,50 | ✅ `72,5 × 0,50 = 36,25` · `10.000.000 ÷ 36,25 = 275.862` |

**Floor 1,0 không bị vi phạm**: nhóm 1.0, nhóm 14.0, task 12.3, và phần kiểm thử thiết bị di động thật — cả bốn đúng `1,00`.

**`FR-24`/`FR-25` giữ `TBD` ở cả hai cột** — 13 lần xuất hiện, không lần nào có con số. §4.1 còn có khối riêng: *"Không tồn tại hệ số nào biến TBD thành một con số, kể cả hệ số 1,0"*.

**Không bịa số đo năng suất AI** — grep `benchmark / nghiên cứu / thống kê / khảo sát / năng suất` cho 3 hit, **cả 3 đều là câu phủ định**. Verifier gọi đây là *"điểm mạnh nhất của bản này"*.

## Xác nhận độc lập hai lập luận đi ngược trực giác

- **"Đường găng thành cổ chai tương đối lớn hơn"** — **ĐÚNG**, verifier xác nhận bằng phép so `0,8333 > 0,7828`, và tính thêm: tỉ số `đường găng ÷ tổng` tăng từ `22,5/72,5 = 0,3103` lên `18,75/56,75 = 0,3304`. Nguyên nhân cũng đúng: `7 MD / 18,75 MD = 37,3%` đường găng bị chốt ở hệ số 1,0.
- **Nhóm 11.0 hệ số CAO (0,85)** — **CÓ CĂN CỨ TÀI LIỆU**, không phải cảm tính. Verifier đối chiếu trực tiếp: PRD §5.1 (NFR-02 *"không định nghĩa quyền theo phạm vi dữ liệu"*), PRD §5.1 (NFR-04 *"toàn bộ lịch sử"*), PRD §9 Q-12 (*"mọi query và mọi API. Sửa sau rất tốn kém"*), BRD §9.1 (*"rủi ro rò rỉ dữ liệu kinh doanh"*).

Verifier cũng ghi nhận writer **gán hệ số đi ngược hướng lạc quan** ở đúng nhóm rủi ro nhất, tự tuyên bố không trích benchmark nào, và xếp cột AI **dưới** cột cũ về độ tin cậy — *"dấu hiệu writer không bóp số theo hướng dễ nghe"*. Sàn 0,17 là một **phép tự-bác-bỏ chủ động**: tự dựng con số mạnh nhất có thể có lợi cho AI rồi chỉ ra nó vẫn không đủ.

## 🟡 WARNING 1 — lỗi nặng nhất còn lại, và là lý do run chưa đóng được ngay

**Trục duy nhất đổi kết luận lại là trục duy nhất không được ghi nhãn.**

§5.6 là mục kết luận lớn nhất của tài liệu. Grep vùng đó chỉ ra **2 lần** `[SUY LUẬN]`, **không lần nào ở Trục 2**. Bảng Trục 2 và bảng Tổng kết ba trục phát biểu *"6 người là đủ"*, *"A + 5 người là đủ"*, *"✅ ĐỔI"* mà **không nhắc `A-11`, không nhắc `A-12`** — trong khi §5.3.a-bis, §5.4-B/C/D/E, §7.3 **đều có nhãn**.

Vì sao nặng: chính writer khai ở `RT-10` rằng hệ số thật 0,90 → CORE 65,25 MD → đội 6 người **thiếu 5,25 MD** → **Trục 2 đảo lại**. Ngưỡng đảo chiều ở hệ số ≈0,83, **cách 0,78 đúng 0,05** — một bậc độ nhạy duy nhất theo chính thang writer khai.

Trong khi đó hai trục kia **robust trước sai số hệ số**: sàn 12,5 MD dựng hoàn toàn từ hạng mục hệ số 1,00; verifier test hai đầu dải (0,90 → 153.000 VND/MD; 0,60 → 230.000) và **cả hai vẫn dưới 300.000**.

⇒ **Hai trục robust đang được trình bày ngang hàng độ tin cậy với một trục fragile, và trục fragile lại là trục mang tin "tốt"** — đúng loại tin người quyết ngân sách dễ nhặt ra khỏi ngữ cảnh. Verifier gọi đây là *"`CRITICAL 2` của vòng trước ở dạng nhẹ hơn: khi đó là con số không truy được, giờ là con số truy được nhưng thiếu nhãn điều kiện"*.

**Xử lý**: dispatch writer sửa (thêm nhãn ở 3 chỗ + thêm tiểu mục *"Ba trục không chắc chắn như nhau"*). PM đã tự sửa bản HTML song song: thêm **cột "Độ chắc chắn"** vào bảng ba trục, và một callout riêng cảnh báo mệnh đề *"A + 5 người là đủ"* là mệnh đề **có điều kiện**, không được trích lẻ.

## 🟡 WARNING 2, 3, 4

| # | Vấn đề | Tác động | Xử lý |
|---|---|---|---|
| W2 | §4 bảng phân rã 12.0, dòng `12.5` có hệ số `0.65` **trần, không có lý do**, trong khi 5/6 dòng cùng bảng đều nhúng lý do. | Con số đúng (`3 × 0,65 = 1,95 → 2`), chỉ thiếu lý do. | Writer bổ sung lý do. |
| W3 | §0.7.e khai *"Hai trường hợp"* sai lệch làm tròn, thực tế có **bốn** — thiếu **9.0 BỔ SUNG** (3,25 vs 3,0) và **10.0 BỔ SUNG** (3,5 vs 3,25). | **0 MD** — quy tắc chung ±0,25 đã phủ đúng biên độ, và không phép tính downstream nào đi qua chúng ở mức task. | Writer chọn: liệt kê đủ 4, hoặc bỏ liệt kê chỉ giữ quy tắc chung. |
| W4 | §7.3 sàn `13,5 MD` **loại hẳn 3,25 MD của task 12.2** về 0 ngày lịch với lý do *"chia được cho 2 QA"*, nhưng task `13.2` cũng được khai *"chia được"* mà **vẫn giữ nguyên** 2,75 MD. Hai task cùng thuộc tính, hai cách xử lý. | **Lệch theo hướng lạc quan một chiều** — sàn tự nhất quán là `≈15,1 MD` chứ không phải 13,5. Vì kết luận cần chứng minh là *"vẫn vượt 10 ngày"*, sai lệch này **làm kết luận mạnh hơn**. Không đảo chiều gì. | Writer chọn: đưa 12.2 vào sàn ở dạng đã chia, hoặc giữ 13,5 kèm câu khai rõ giả định lạc quan. |

## 🔵 Tám SUGGESTION — bốn cái đã giao writer sửa

Đã giao: **S1** hệ số 0,78 suy từ tổng đã làm tròn (56,75/0,7828) chứ không từ tổng tích thô (56,17/0,7748) — bias `+0,58 MD`, đúng hướng dè dặt, cần chú thích nguồn. **S2** công thức hệ số ở §0.7.d **thiếu dấu ngoặc**, đọc ra `A + (R ÷ T)` thay vì `(A + R) ÷ T` — đây là định nghĩa của đại lượng trung tâm cả vòng. **S3** RT-08 chưa đồng bộ cột AI. **S4** bảng cắt trắng A trừ số mức task khỏi tổng mức nhóm → `44,75` lạc quan 0,25 MD (trong biên đã khai).

Bốn cái còn lại: biên trên dải D làm tròn rộng 0,15; rủi ro **thị giác** ở ô *"A + 5 người"* cạnh `✅ ĐỔI` trong bảng tổng kết (PM đã xử lý ở bản HTML bằng cột "Độ chắc chắn"); mã `C-18` **không tồn tại trong Glossary** (nó ở PRD §10 và BRD RK-06 — đề xuất thêm vào Glossary, **ngoài scope run này**); và xác nhận `000-Index.md` / `Planning-MOC.md` / `Proposal-VETC.html` **đã đồng bộ hai cột, 0 con số lệch**.

## Phán xét độc lập của verifier về kết luận ba trục

> *"Kết luận ĐƯỢC CHỐNG ĐỠ. Không quá mạnh cũng không quá nhẹ ở bất kỳ trục nào. Nhưng độ chắc chắn của ba trục rất khác nhau, và tài liệu chưa nói rõ sự khác nhau đó."*

- **Trục ngân sách** — chống đỡ **mạnh nhất**. Điểm quyết định không phải con số 176.000 (phụ thuộc `A-12`) mà là **sàn 12,5 MD**, dựng hoàn toàn từ hạng mục hệ số 1,00 nên không phụ thuộc hệ số nào đúng.
- **Trục cấu trúc** — chống đỡ **mạnh hơn cả mức writer tự nhận**: verifier tính sàn tự nhất quán là ≈15 ngày thay vì 13,5 (W4), tức lệch về phía **bất lợi cho writer**, nên kết luận còn đứng vững hơn con số công bố.
- **Trục tổng effort** — đúng nhưng **yếu nhất**, và tài liệu chưa nói rõ nó yếu. Đây là nội dung của W1.

## Hai hạng mục verifier từ chối kết luận — ghi trung thực

- **`E-01` và `E-03`** (quy mô đội thật, đơn giá thuê ngoài thật): không có nguồn nào trong repo. Vì `E-03` mở, verifier **không phán xét** được 176.000 VND/MD có khả thi hay không — chỉ xác nhận **phép chia** đúng.
- **Bản thân 14 hệ số đúng hay sai**: **về nguyên tắc không kiểm được từ tài liệu** — không có benchmark nội bộ, không có dữ liệu đo. Verifier chỉ kiểm được: chúng được gán nhất quán, 4 hạng mục floor 1,0 không bị vi phạm, 28 phép nhân đúng, và không số đo nào bị bịa. `A-12` là giả định mở, không phải phát hiện.

## Trạng thái xử lý vòng hai

| Hạng mục | Trạng thái |
|---|---|
| W1 — nhãn điều kiện ở §5.6 (`WBS-ETA-VETC.md`) | 🔄 dispatch writer |
| W1 — lan sang `Proposal-VETC.html` | ✅ PM đã sửa: thêm cột **"Độ chắc chắn"** vào bảng ba trục + callout *"Ba trục không chắc chắn như nhau"* + nhãn `SUY LUẬN — phụ thuộc A-11 + A-12` cho con số 44,75 |
| W2, W3, W4 | 🔄 dispatch writer |
| S1, S2, S3, S4 | 🔄 dispatch writer |
| MOC / Index đồng bộ hai cột | ✅ verifier xác nhận 0 lệch |
| `C-18` không có trong Glossary | ⏸️ **ngoài scope** — ghi lại cho run sau |

---

## Kết luận cuối

**Không còn lỗi `CRITICAL` ở cả hai vòng verify.** Cả hai deliverable dùng được.

### Hai phát hiện ngoài phạm vi — cố ý không sửa

Cả hai đều thuộc tầng `999-Resources`, **không nằm trong ownership map đã duyệt tại gate**. Sửa ngầm là mở rộng scope không qua gate, nên PM ghi lại cho một run sau:

1. `Glossary.md` — dòng định nghĩa `VETC` trỏ sai mã `Q-27` (Q-27 thực tế là *"Bổ sung Danh mục Loại thẻ"*, không liên quan việc định nghĩa VETC).
2. `Glossary.md` — mã **`C-18`** (chuẩn hóa thuật ngữ *"Đơn xuất thẻ"*) **không tồn tại trong Glossary**; nó chỉ nằm ở PRD §10, PRD phần quy ước, và BRD `RK-06`. Glossary có **quy tắc nội dung** tương đương nhưng không mang mã, nên mã không truy được từ SSOT thuật ngữ. Đề xuất thêm `(mã C-18)` vào dòng *"Đơn xuất thẻ"*.

### Giá trị thực tế của việc verify bởi agent thứ ba — đúc kết cho run sau

Ba phát hiện có giá trị nhất của cả run này đều **không thể tự phát hiện được** bởi người tạo ra chúng:

- **`CRITICAL 1` vòng một** (mã `FR-27`/`FR-31` bịa) — root cause nằm trong `outline.md` do **PM** viết. Writer không bắt được vì lỗi nằm trong chỉ thị nó nhận và nó không được phép sửa outline; PM không bắt được vì PM là người tạo ra nó.
- **`CRITICAL 2` vòng một** (con số 32–35 MD không truy được) — writer không bắt được vì nó đọc đúng bộ context nó vừa tạo ra.
- **`WARNING 1` vòng hai** (trục duy nhất đổi kết luận lại là trục duy nhất không ghi nhãn) — đây là loại lỗi **không phải lỗi số học**, nên chỉ lộ ra khi có người đọc lại toàn bộ tài liệu với câu hỏi *"mệnh đề nào ở đây dễ bị trích lẻ nhất?"*.

Điểm chung: cả ba đều là lỗi **về độ tin cậy được trình bày**, không phải lỗi tính toán. Đó là lý do `context-auditor` — agent có remit về consistency và context hygiene, không phải về estimation — là verifier đúng cho lane tài liệu, và là lý do quy tắc *"verify phải do agent KHÁC agent đã thực thi"* không phải nghi thức rỗng.

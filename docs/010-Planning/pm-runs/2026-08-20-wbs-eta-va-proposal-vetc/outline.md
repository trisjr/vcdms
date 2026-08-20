# Doc Plan: 2026-08-20-wbs-eta-va-proposal-vetc

> [!IMPORTANT]
> **Bản cập nhật sau gate (2026-08-20).** Anh đã cấp ràng buộc thật tại QĐ-03: **ngân sách ~10.000.000 VND**, **10 ngày** cho các chức năng chính, chức năng bổ sung làm sau. Điều này thay thế assumption A-03/A-04/A-06 và làm outline dưới đây khác bản trình gate ban đầu. Chi tiết hệ quả: `run-plan.md` mục Gate, `escalations.md` mục E1.
>
> **Hai tầng phạm vi** dùng xuyên suốt run này:
> - **CORE** = toàn bộ mức `P0` của PRD = **12 FR** (FR-01, 02, 04, 05, 06, 07, 11, 12, 14, 18, 19, 22) + **5 NFR** (NFR-01…NFR-05). Ràng buộc: 10 ngày, ~10 triệu VND.
> - **BỔ SUNG** = `P1` (10 FR: FR-03, 08, 09, 10, 13, 15, 20, 21, 23, 24 + NFR-06, NFR-07), rồi `P2` (3 FR: FR-16, 17, 25). Chưa có mốc thời gian — anh nói *"hoàn thành sau"*.
>
> Căn cứ của phép chia này là **định nghĩa `P0` có sẵn trong PRD §4**: *"bắt buộc cho bản chạy được đầu tiên"* — trùng khớp với cách anh diễn đạt *"chức năng chính để có thể hoạt động"*. PM **không tự chia** tầng.

## Hạng mục

| # | Tài liệu | Loại (RULE-001) | Đích | Template | Trạng thái đích | Writer | Xong |
|---|----------|-----------------|------|----------|-----------------|--------|------|
| 1 | Bảng WBS kết hợp ETA — Giai đoạn 1 | `wbs` + `eta` (gộp) | `docs/010-Planning/Estimates/WBS-ETA-VETC.md` | `docs/999-Resources/Templates/Template-WBS-ETA.md` | `draft` | `product-owner` | [x] |
| 2 | Proposal triển khai VCDMS (HTML) | *(không có trong Document Type Mapping — anh chốt QĐ-02 phương án A tại gate)* | `docs/010-Planning/Proposal-VETC.html` | — (tự thiết kế, đã nạp skill `artifact-design` + `dataviz`) | `draft` | **PM (main loop)** | [x] |

> **Artifact URL**: https://claude.ai/code/artifact/175830cc-1f34-47b4-9e53-a49bb0a64b2b
> Palette đã validate bằng `dataviz/scripts/validate_palette.js`: light `#0089A7 / #C2860A / #BC3524` — ALL PASS; dark `#2E9DB4 / #BB8C1B / #D8546B` — ALL PASS (band dark 0.48–0.67, chọn riêng chứ không lật tự động).

> Hạng mục 2 **phụ thuộc** hạng mục 1 — proposal trích số liệu tổng effort và timeline từ bảng WBS/ETA. Không chạy song song.
> Hạng mục 2 do PM tự viết vì: (a) chỉ main loop có tool `Artifact` để publish cho anh review; (b) guardrail *"file nào PM không đọc toàn văn thì không được publish"* — PM tự viết là đường ngắn nhất thỏa điều đó.

---

## Outline từng tài liệu

### Tài liệu 1 — `WBS-ETA-VETC.md`

- **Độc giả đích**: PM và đội triển khai (Architect, Engineer, QA, Designer). Dùng để lập kế hoạch sprint và làm đầu vào cho proposal. **Không phải** tài liệu báo giá gửi khách hàng.

- **Cấu trúc** (heading cấp 1–2):
  - `# 📊 WBS & ETA — Hệ thống Quản lý Xuất kho & Phân phối thẻ VETC (VCDMS)`
  - `## 0. Phạm vi, ràng buộc và quy ước của bản ước lượng` — nêu rõ:
    - **Ràng buộc do anh cấp**: ngân sách ~10.000.000 VND, 10 ngày cho tầng CORE. Ghi rõ đây là **ràng buộc khách hàng**, phân biệt với ước lượng của đội.
    - **Hai tầng phạm vi** CORE (P0) / BỔ SUNG (P1→P2) kèm căn cứ là định nghĩa `P0` của PRD §4.
    - Đơn vị effort: **man-day (MD)**. Tầng CORE dùng mốc **Ngày D1…D10**; tầng BỔ SUNG dùng **Tuần tương đối W+1, W+2…** vì chưa có mốc.
    - Giữ nguyên 3 nhãn `[SRS]` / `[SUY LUẬN]` / `[TBD]` của PRD.
    - **Tuyên bố bắt buộc**: cột Effort là ước lượng bottom-up của đội, **chưa phải cam kết**; hai con số duy nhất có nguồn SRS là *tra cứu ≤ 2 giây* và *sao lưu hàng ngày*.
  - `## 1. Work Breakdown Structure (WBS)` — bảng cột: `WBS ID | Task Name | Deliverable | Owner | Tầng (CORE/BỔ SUNG) | FR/NFR liên quan`. Cột *Tầng* là bổ sung so với template, cần thiết vì anh yêu cầu phân tầng.
  - `## 2. Estimation (ETA) — Tầng CORE` — bảng cột: `Task ID | Description | Effort (MD) | Start | End | Status`. Start/End dùng **D1…D10**.
  - `## 3. Estimation (ETA) — Tầng BỔ SUNG` — cùng cột, Start/End dùng **W+1, W+2…**. FR-24, FR-25 **không** xuất hiện ở đây (nằm ở §6).
  - `## 4. Tổng hợp effort theo nhóm công việc` — bảng tổng MD từng nhóm 1.0…14.0, tách 2 cột `MD CORE` / `MD BỔ SUNG`, có dòng tổng cộng. Phần TBD tách riêng, **không cộng vào tổng**.
  - `## 5. ⚠️ Phân tích khoảng cách (Gap Analysis)` — **mục quan trọng nhất của tài liệu.** Trình bày song song 4 khối:
    1. **Đội cần**: tổng MD bottom-up của tầng CORE theo §4.
    2. **Anh có**: 10 ngày · ~10.000.000 VND.
    3. **Khoảng cách**: hiệu số, và *quy đổi ngân sách* — nêu rõ 10.000.000 VND ÷ tổng MD CORE = đơn giá ngày phải đạt, rồi đối chiếu với thực tế nhân sự.
    4. **Phương án nếu có khoảng cách** — tối thiểu 3 phương án, mỗi phương án ghi *cắt gì · được gì · mất gì*. Ví dụ trục để cân nhắc: cắt tiếp trong nội bộ P0 (FR nào bỏ được mà hệ thống vẫn chạy), giãn thời gian, tăng nhân sự, hoặc dùng phương án kỹ thuật rẻ hơn cho FR nặng.
    > **Writer KHÔNG được điều chỉnh cột Effort để tổng khớp 10 ngày.** Ước lượng bottom-up trước, đối chiếu sau. Nếu vượt thì nói thẳng là vượt. Đây là tiêu chí xong số 8.
  - `## 6. Hạng mục KHÔNG được ước lượng` — FR-24, FR-25 (chờ Q-28) + **trích nguyên văn** câu cấm của PRD §4.
  - `## 7. Đường găng (Critical Path) và phụ thuộc` — khối phụ thuộc gốc `Q-01 → Q-26 → Q-06 → NFR-05` mà PRD §1 gọi là *"một khối"*, và hệ quả lên thứ tự thực thi trong 10 ngày.
  - `## 8. Rủi ro tiến độ` — 11 Blocker của PRD §9 ảnh hưởng ước lượng thế nào. **Bắt buộc** nêu rủi ro lớn nhất: 31 câu `Q-NN` chưa có câu trả lời, mà nhóm 1.0 (Discovery) lại nằm trong chính 10 ngày đó.
  - `## 9. Tài liệu liên quan` — markdown links tới PRD, BRD, SRS, Analysis-Open-Questions.

- **Phân rã WBS bắt buộc** — 14 nhóm dưới đây, writer **không được tự thêm/bớt nhóm**, chỉ được phân rã task con bên trong:

  | Nhóm | Tên | FR/NFR phủ |
  |---|---|---|
  | 1.0 | Discovery & Chốt yêu cầu (trả lời 31 câu `Q-NN`) | — |
  | 2.0 | Kiến trúc & Thiết kế hệ thống (SDD, ADR, DB schema, API spec) | — |
  | 3.0 | Thiết kế UI/UX (user flow, wireframe, design system) | — |
  | 4.0 | Nền tảng & Hạ tầng (project setup, CI/CD, môi trường, object storage) | NFR-03 |
  | 5.0 | Danh mục & Master data | FR-18, FR-19, FR-24* + Danh mục Loại thẻ *(giả định Q-27)* + Danh mục Đại lý *(giả định Q-31)* |
  | 6.0 | Luồng Đơn xuất thẻ & Phê duyệt 2 cấp | FR-01…FR-07 |
  | 7.0 | Vận chuyển & Tracking | FR-08, FR-09, FR-10 |
  | 8.0 | Nhận hàng & Chứng từ giao nhận | FR-11, FR-12, FR-13 |
  | 9.0 | Truy vết & Quản lý thất thoát | FR-14…FR-17 |
  | 10.0 | Tra cứu, Bộ lọc & Báo cáo | FR-20…FR-23, FR-25* |
  | 11.0 | Xác thực, Phân quyền & Audit Log | NFR-01, NFR-02, NFR-04, NFR-05 |
  | 12.0 | QA & Kiểm thử (test plan, test case, UAT, perf test cho NFR-06) | NFR-06 |
  | 13.0 | Triển khai & Go-live (deploy, migration import Excel, backup) | NFR-07 |
  | 14.0 | Quản trị dự án (PM, họp, báo cáo, quản lý thay đổi) | — |

  `*` = phần `TBD`, tách riêng, **không cộng vào tổng**.

  > [!CAUTION]
  > **Sửa sau verify (2026-08-20)** — bản đầu của bảng này ghi `FR-27, FR-31` ở nhóm 5.0. **Hai mã đó không tồn tại**: PRD chỉ có `FR-01`…`FR-25`. Chúng bị vay từ mã câu hỏi `Q-27` / `Q-31`. Writer tuân thủ outline nên lỗi lan xuống deliverable — đây là **lỗi của PM, không phải của writer**. Quy tắc rút ra: trong outline, **chỉ được viết chuỗi `FR-NN` cho mã thực có trong PRD**; giả định thiết kế phải gọi bằng mã `Q-NN`, không được đội lốt mã FR.

- **Nguồn sự thật** (writer **chỉ** được lấy nội dung từ đây, không có nguồn thì ghi `TBD`):
  - `docs/020-Requirements/PRD-VETC.md` §4 (25 FR + cột Ưu tiên P0/P1/P2 + cột Nguồn SRS), §5.1 (7 NFR), §5.2 (13 NFR còn thiếu), §6 (state machine 5 trạng thái + 8 nhánh thiếu), §9 (31 giả định + mức độ Blocker/Quan trọng/Nên có + bản đồ tác động).
  - `docs/020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md` §4 (phạm vi In/Out/Undetermined), §6 (quy trình 5 bước), §7 (quy tắc nghiệp vụ BR-01…), §8.3 (giả định A-01), §9 (rủi ro nghiệp vụ).
  - `docs/999-Resources/Templates/Template-WBS-ETA.md` — cấu trúc bảng.
  - **Ràng buộc ngân sách / thời gian**: **do anh cấp trực tiếp tại gate** — ~10.000.000 VND, 10 ngày cho tầng CORE. Nguồn là câu trả lời của anh, ghi rõ trong `run-plan.md` mục Gate. **Không có trong PRD/BRD/SRS** — writer phải trình bày nó như *ràng buộc khách hàng*, không được gán cho tài liệu nào.
  - **Effort MD**: không có nguồn nào trong repo chứa số MD. Writer tự ước lượng dựa trên **độ phức tạp mô tả trong PRD** (số FR trong nhóm, mức ưu tiên, số Blocker liên đới) và **bắt buộc** ghi ở §0 rằng toàn bộ cột Effort là *ước lượng của đội chờ xác nhận*. **Không được** trích dẫn nguồn giả cho số MD.
  - **Quy mô nhân sự**: PRD/BRD **không nói gì** về team size. Writer ghi ở §0 dưới dạng **[SUY LUẬN]** rằng ước lượng giả định quy mô đội nào (và nêu căn cứ suy luận từ tỉ lệ ngân sách/thời gian), rồi liệt kê đó là một điểm cần anh xác nhận. **Không** trình bày team size như dữ kiện.

- **Tiêu chí xong** (đo được):
  1. Đủ **14 nhóm** WBS, mỗi nhóm có ≥ 2 task con, mỗi task con có `Deliverable` cụ thể và `Owner` là một trong: PM / BA / Architect / Designer / Engineer / QA / DevOps.
  2. **Cả 25 FR và 7 NFR** đều xuất hiện ít nhất một lần trong cột `FR/NFR liên quan` — trừ FR-24, FR-25 phải nằm ở §6 với effort `TBD`.
  3. Mọi dòng WBS có cột *Tầng* điền đúng `CORE` hoặc `BỔ SUNG`, và **12 FR + 5 NFR mức P0** liệt kê ở đầu outline này phải nằm trọn trong tầng `CORE` — không thiếu, không thừa.
  4. Tổng MD ở §2 khớp cột `MD CORE` của §4; tổng MD ở §3 khớp cột `MD BỔ SUNG` của §4 (kiểm tra được bằng cộng tay).
  5. **Không có ngày dương lịch nào** trong toàn file. Tầng CORE chỉ dùng `D1`…`D10`; tầng BỔ SUNG chỉ dùng `W+N`.
  6. §5 Gap Analysis có **đủ 4 khối** và **≥ 3 phương án** xử lý khoảng cách, mỗi phương án ghi rõ *cắt gì · được gì · mất gì*.
  7. §6 trích **nguyên văn** câu cảnh báo của PRD §4 về FR-24/FR-25.
  8. **Cột Effort không bị bóp cho khớp ràng buộc.** Kiểm chứng: nếu tổng MD CORE tình cờ bằng đúng 10 thì §5 phải giải thích được vì sao bottom-up ra đúng con số đó; nếu vượt 10 thì §5 phải nói thẳng là vượt và bao nhiêu.
  9. Frontmatter đủ `id: WBS-ETA-VETC`, `type: wbs`, `status: draft`, `project: VETC`, `created: 2026-08-20`.
  10. §9 dùng **standard markdown links relative path** (`[PRD-VETC](../../020-Requirements/PRD-VETC.md)`), **không** dùng wiki-link `[[...]]` — RULE-001 quy tắc 5.

### Tài liệu 2 — `Proposal-VETC.html`

- **Độc giả đích**: anh (trisjr) review nội bộ trước khi quyết định có chuyển thành bản gửi khách hàng hay không. Vì vậy **không chứa giá và điều khoản thương mại** (A-06).

- **Cấu trúc**:
  1. **Tóm tắt điều hành** — VCDMS là gì, 4 vấn đề nghiệp vụ P-01…P-04, phạm vi 25 FR + 7 NFR.
  2. **Bối cảnh & Vấn đề** — từ BRD §2.
  3. **Phạm vi Giai đoạn 1** — In Scope / Out of Scope / Undetermined Scope, từ BRD §4 và PRD §2.3.
  4. **Giải pháp đề xuất** — luồng 5 bước + state machine, từ BRD §6 và PRD §6.
  5. **Phạm vi 2 tầng** — CORE (12 FR + 5 NFR mức P0, 10 ngày) vs BỔ SUNG (P1 rồi P2, chưa có mốc). Nêu rõ căn cứ phân tầng là định nghĩa `P0` của PRD.
  6. **Kế hoạch triển khai & Ngân sách** — WBS 14 nhóm, mốc D1…D10 cho CORE, tổng effort, và **ngân sách ~10.000.000 VND** — trích từ tài liệu 1.
  7. **⚠️ Phân tích khoảng cách** — trình bày lại §5 Gap Analysis của tài liệu 1: đội cần bao nhiêu · anh có bao nhiêu · khoảng cách · các phương án. **Không được làm mềm hay lược bỏ** phần này.
  8. **⚠️ Giả định & Điều kiện tiên quyết** — **mục bắt buộc** (A-07): 11 Blocker của PRD §9, khối phụ thuộc `Q-01 → Q-26 → Q-06 → NFR-05`, và tuyên bố rõ *"mọi con số trong tài liệu này là ước lượng chờ xác nhận, không phải cam kết"*.
  9. **Rủi ro & Phương án giảm thiểu** — 8 nhánh nghiệp vụ thiếu (T-a…T-h) + rủi ro nghiệm thu do thiếu KPI (BRD §10, Q-29) + rủi ro 31 câu `Q-NN` chưa chốt mà đồng hồ 10 ngày đã chạy.
  10. **Điều kiện để chốt tiến độ** — 31 câu `Q-NN` cần khách hàng trả lời, link tới `Analysis-Open-Questions-VETC.md`.

- **Nguồn sự thật**: `PRD-VETC.md`, `BRD-001-...md`, và `WBS-ETA-VETC.md` (tài liệu 1, phải hoàn thành trước). Phân loại số liệu trong bản HTML thành **3 hạng**, mỗi hạng có dấu hiệu trực quan riêng:
  - **Hạng 1 — số liệu SRS** (chốt): đúng 2 con số *tra cứu ≤ 2 giây* và *sao lưu hàng ngày*.
  - **Hạng 2 — ràng buộc khách hàng** (chốt, nguồn là anh tại gate): ~10.000.000 VND, 10 ngày.
  - **Hạng 3 — ước lượng của đội** (chưa chốt): toàn bộ số MD, mọi con số trong PRD §9.

- **Tiêu chí xong**:
  1. Đủ 10 mục trên; mục 7 và 8 hiển thị nổi bật, **không** chôn dưới cuối trang.
  2. Ba hạng số liệu phân biệt được bằng mắt, không cần đọc chú thích mới hiểu con số nào là cam kết.
  3. Trang self-contained (không tài nguyên ngoài), theme-aware, publish được thành Artifact và anh mở được link.
  4. Tổng effort MD ở mục 6 và các số ở mục 7 **khớp tuyệt đối** với §4 và §5 của tài liệu 1.
  5. Không có chỗ nào trình bày ước lượng MD như cam kết tiến độ.

---

## Markdown link phải tạo

| Từ | Tới | Quan hệ (RULE-001 §Linking Rules) |
|---|---|---|
| `WBS-ETA-VETC.md` | `../../020-Requirements/PRD-VETC.md` | `Based on:` — WBS phân rã từ phạm vi PRD |
| `WBS-ETA-VETC.md` | `../../020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md` | `Business context:` |
| `WBS-ETA-VETC.md` | `../../020-Requirements/SRS-VETC.md` | `Root source:` |
| `WBS-ETA-VETC.md` | `../../050-Research/Analysis-Open-Questions-VETC.md` | `Blocked by:` — 31 câu `Q-NN` |
| `Planning-MOC.md` | `./Estimates/WBS-ETA-VETC.md` | Mục MOC (PM ghi) |
| `Planning-MOC.md` | `./Proposal-VETC.html` | Mục MOC (PM ghi) |
| `000-Index.md` | `./010-Planning/Proposal-VETC.html` | Tài liệu lớn (PM ghi) |

## MOC cần cập nhật

| MOC | Mục thêm/sửa |
|---|---|
| `docs/010-Planning/Planning-MOC.md` | Thêm mục `Estimates/` trỏ tới `WBS-ETA-VETC.md`; thêm dòng `Proposal-VETC.html` |
| `docs/000-Index.md` | Thêm `Proposal-VETC.html` vào danh sách tài liệu lớn |

> Hai file này **thuộc PM**, không cấp cho worker nào.

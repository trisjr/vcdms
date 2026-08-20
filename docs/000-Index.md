---
id: INDEX-000
type: index
status: live
created: 2026-08-19
updated: 2026-08-20
---

# 🏠 Trang chủ Tài liệu — Dự án VCDMS

Đây là điểm vào duy nhất của toàn bộ kho tài liệu. Mỗi tầng Dewey có một **MOC** (Map of Content) làm trung tâm điều hướng riêng; trang này chỉ trỏ tới các MOC đó và tới những tài liệu lớn.

> [!NOTE]
> Cấu trúc thư mục và quy tắc đặt tên tuân theo [RULE-001 — Quy tắc Cấu trúc Tài liệu](../knowledge-base/99-Templates/Documents-Template.md). Trước khi tạo tài liệu mới, **bắt buộc** tra bảng Document Type Mapping trong file đó.

## 📑 Mục lục

- [Tài liệu lớn](#-tài-liệu-lớn)
- [Điều hướng theo tầng](#-điều-hướng-theo-tầng)
- [Trạng thái kho tài liệu](#-trạng-thái-kho-tài-liệu)

---

## 📌 Tài liệu lớn

Những tài liệu được tham chiếu nhiều nhất, đăng ký trực tiếp tại trang chủ theo quy định của RULE-001.

| Tài liệu | Loại | Trạng thái | Mô tả |
| :--- | :--- | :--- | :--- |
| [SRS-VETC](./020-Requirements/SRS-VETC.md) | SRS | `draft` | Mô tả yêu cầu phần mềm — Hệ thống Quản lý Xuất Nhập Kho & Phân phối Thẻ VETC. **Nguồn gốc của toàn bộ tài liệu bên dưới.** |
| [PRD-VETC](./020-Requirements/PRD-VETC.md) | PRD | `draft` | Yêu cầu sản phẩm: 25 Functional Requirement, 7 Non-Functional Requirement, state machine trạng thái đơn, 31 giả định thiết kế, 18 mâu thuẫn phát hiện trong SRS. |
| [BRD-001 — Hệ Thống Xuất Kho & Phân Phối Thẻ VETC](./020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md) | BRD | `draft` | Yêu cầu nghiệp vụ cấp cao: bối cảnh, mục tiêu, phạm vi, các bên liên quan, 10 business rule. |
| [Analysis-Open-Questions-VETC](./050-Research/Analysis-Open-Questions-VETC.md) | Analysis | `draft` | 31 điểm cần khách hàng làm rõ, viết cho người phi kỹ thuật. **Chặn việc chuyển PRD/BRD sang `approved`.** |
| [WBS-ETA-VETC](./010-Planning/Estimates/WBS-ETA-VETC.md) | WBS + ETA | `draft` | WBS 14 nhóm kết hợp ETA. Chia hai tầng: CORE (`P0` — 12 FR + 5 NFR) và BỔ SUNG (`P1`→`P2`). **Hai cột effort song song**: truyền thống **72,5 / 39,5 MD** và AI-assisted **56,75 / 29,5 MD**. Kèm Gap Analysis đối chiếu ràng buộc **10 ngày / ~10.000.000 VND** (nhân công thuê ngoài) và 5 phương án xử lý khoảng cách. |
| [Proposal-VETC](./010-Planning/Proposal-VETC.html) | Proposal (HTML) | `draft` | Bản đề xuất triển khai giai đoạn 1, tổng hợp từ PRD + BRD + WBS/ETA. Tài liệu **nội bộ** phục vụ quyết định phạm vi và tiến độ — không chứa điều khoản thương mại. |

> [!WARNING]
> Toàn bộ tài liệu trên đang ở `status: draft`. Lý do: **11 câu hỏi mức Blocker** trong `Analysis-Open-Questions-VETC` chưa có lời đáp từ khách hàng. Mọi con số và phương án trong PRD ngoài hai chỉ tiêu gốc của SRS (tra cứu ≤ 2 giây, sao lưu hàng ngày) đều là **giả định thiết kế chờ xác nhận**, không phải cam kết. Đừng coi chúng là quyết định đã chốt khi lập kế hoạch hay ước lượng công.
>
> Điều này áp dụng nguyên vẹn cho `WBS-ETA-VETC` và `Proposal-VETC`: hai con số **10 ngày** và **~10.000.000 VND** là ràng buộc khách hàng cấp tại gate ngày `2026-08-20`, còn **mọi con số man-day đều là ước lượng của đội chờ xác nhận**. Bản WBS/ETA kết luận thẳng rằng ràng buộc 10 ngày **bất khả thi theo hai cách độc lập** — tổng effort và độ dài đường găng — nên đừng đọc nó như một kế hoạch đã cam kết.
>
> **Riêng cột `MD AI-assisted` còn yếu hơn một bậc nữa.** Nó kế thừa toàn bộ điều kiện của cột truyền thống rồi cộng thêm hai giả định: `A-11` nhà thầu *thực sự* dùng Claude và đủ thành thục, `A-12` bản thân hệ số là phán đoán chuyên môn chưa có dữ liệu đo. **Không con số nào trong cột đó là số đo, và không trích dẫn benchmark năng suất AI nào.** Nếu phải chọn một con số duy nhất đưa vào hợp đồng thuê ngoài thì đó là **cột truyền thống** — vì `A-11` sai thì con số phải trả quay về đúng 72,5 MD.

---

## 🗂️ Điều hướng theo tầng

| Tầng | MOC | Nội dung |
| :--- | :--- | :--- |
| **010-Planning** | [Planning-MOC](./010-Planning/Planning-MOC.md) | Roadmap, OKRs, Sprint, kế hoạch triển khai, run-state của PM |
| **020-Requirements** | [Requirements-MOC](./020-Requirements/Requirements-MOC.md) | BRD, PRD, SRS, Use Case, NFR |
| **022-User-Stories** | [Stories-MOC](./022-User-Stories/Stories-MOC.md) | Epic, User Story, backlog |
| **030-Specs** | [Specs-MOC](./030-Specs/Specs-MOC.md) ⚠️ | ADR, RFC, SDD, API spec, DB schema, security spec |
| **035-QA** | [QA-MOC](./035-QA/QA-MOC.md) | Test plan, test case, bug report, báo cáo kiểm thử |
| **040-Design** | [Design-MOC](./040-Design/Design-MOC.md) ⚠️ | Design system, wireframe, user flow |
| **050-Research** | [Research-MOC](./050-Research/Research-MOC.md) | Phân tích, điểm cần làm rõ, nghiên cứu đối thủ, phỏng vấn người dùng |
| **070-Deployment** | [Deployment-MOC](./070-Deployment/Deployment-MOC.md) | Release notes, deploy guide, runbook, rollback |
| **080-Operations** | [Operations-MOC](./080-Operations/Operations-MOC.md) | Incident, post-mortem, SLA |
| **999-Resources** | [Resources-MOC](./999-Resources/Resources-MOC.md) | Template, Glossary, meeting notes |

⚠️ = MOC hiện là **file rỗng**, xem mục Trạng thái bên dưới.

**Tra cứu nhanh:**

- [Glossary](./999-Resources/Glossary.md) — từ điển thuật ngữ nghiệp vụ VETC và thuật ngữ kỹ thuật
- [Templates](./999-Resources/Templates/) — bản mẫu chuẩn cho từng loại tài liệu
- [pm-runs](./010-Planning/pm-runs/README.md) — dấu vết điều phối của PM qua từng run, gồm cả các quyết định tại gate

---

## 🔎 Trạng thái kho tài liệu

Ghi nhận trung thực hiện trạng tại `2026-08-19` để người đọc sau biết chỗ nào còn trống, thay vì tưởng đã đầy đủ.

| Hạng mục | Trạng thái | Ghi chú |
| :--- | :--- | :--- |
| `030-Specs/Specs-MOC.md` | ⚠️ **File rỗng (0 byte)** | RULE-001 quy định đây là MOC bắt buộc. Cần khởi tạo trong một run riêng. |
| `040-Design/Design-MOC.md` | ⚠️ **File rỗng (0 byte)** | Như trên. |
| `060-Manuals/` | ⚠️ **Chưa tồn tại** | RULE-001 có quy định tầng này kèm `Manuals-MOC.md`; hiện chưa khởi tạo. |
| `090-Archive/` | ⚠️ **Chưa tồn tại** | Tạo khi lần đầu có tài liệu bị thay thế cần chuyển sang `status: deprecated`. |
| `999-Resources/Glossary.md` | 🟡 Mới bổ sung domain VETC | Trước run `2026-08-19-brd-prd-vetc-tu-srs` chỉ có 3 thuật ngữ không liên quan dự án. |

> Bốn dòng đầu là **hiện trạng có sẵn**, không phát sinh từ run đã tạo trang này. Chúng được ghi lại ở đây để không bị quên, chứ không phải để mở rộng phạm vi của run đó.

---

_Index generated by TNMCORE-OS._

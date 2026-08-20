---
id: MOC-PLANNING
type: moc
status: draft
created: 2026-02-04
updated: 2026-08-20
---

# Planning Map of Content (MOC)

- [Roadmap](./Roadmap.md)
- [OKRs](./OKRs.md)
- [Sprints/](./Sprints/)
- [Implementation-Plans/](./Implementation-Plans/)
- [pm-runs/](./pm-runs/README.md) — run-state của `/pm-run`

## Estimates — Ước lượng & Ngân sách

- [WBS-ETA-VETC](./Estimates/WBS-ETA-VETC.md) — WBS 14 nhóm kết hợp ETA cho dự án VCDMS, chia hai tầng CORE (`P0`, 72,5 MD) và BỔ SUNG (`P1`→`P2`, 39,5 MD), kèm Gap Analysis đối chiếu ràng buộc 10 ngày / ~10.000.000 VND và 5 phương án xử lý khoảng cách.

## Đề xuất triển khai

- [Proposal-VETC](./Proposal-VETC.html) — bản đề xuất triển khai giai đoạn 1 dạng HTML, tổng hợp từ [PRD-VETC](../020-Requirements/PRD-VETC.md), [BRD-001](../020-Requirements/BRD/BRD-001-He-Thong-Xuat-Kho-Phan-Phoi-The-VETC.md) và [WBS-ETA-VETC](./Estimates/WBS-ETA-VETC.md). Tài liệu nội bộ phục vụ quyết định về phạm vi và tiến độ.

> [!NOTE]
> **Hai ngoại lệ có chủ ý so với [RULE-001](../../knowledge-base/99-Templates/Documents-Template.md)**, cả hai đều được chốt tại gate của run `2026-08-20-wbs-eta-va-proposal-vetc`:
>
> 1. **`WBS-ETA-VETC.md`** — Document Type Mapping quy định WBS → `WBS-{ProjectName}.xlsx` và ETA → `ETA-{ProjectName}.xlsx` (hai file `.xlsx` rời). File này gộp cả hai mục vào **một file `.md`** theo QĐ-01, vì `Template-WBS-ETA.md` sẵn có vốn đã chứa cả mục WBS và mục ETA, và toàn bộ kho `docs/` hiện không có file `.xlsx` nào. Cần bản Excel để nhập vào MS Project / ClickUp thì phải xuất riêng trong một run sau.
> 2. **`Proposal-VETC.html`** — loại tài liệu **chưa có trong Document Type Mapping**. Đích và tên file chốt theo QĐ-02. Vì là file `.html`, nó không mang YAML frontmatter — thông tin định danh nằm trong thẻ `<title>` và phần chân trang.

# TEAM — Ngày 12

Mã bộ ảnh: **G03** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyen Huu Loc | 2A202603313 | có | Long Nguyễn | 42 / 42 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Không có. Cả 42 dòng đã thống nhất: 36 dòng giữ nhãn của mình, 6 dòng sửa theo Long Nguyễn trong `export_final_v2.zip` (S01_ir facing, S01_rgb occupied, S04_rgb và S04_ir occupied, D06 box person).
- Đã hỏi coach về `child_seat.occupied = yes`: coach cho phép thêm giá trị `yes` vào schema.

## Cá nhân

### NguyenHuuLoc-2A202603313
- Phần mình làm (ngoài 22 ảnh của mình): chạy `cabin_check diff` giữa bài mình và bài Long Nguyễn, điền `disagreement_log.csv`, sửa nhãn và export `export_final_v2.zip`.
- Điều mình học được hôm nay: Ghế gọi theo xe chứ không theo ảnh, và `unknown` là để ghi khi không thấy chứ không phải để né quyết định. Hai người gán giống nhau chỉ chứng minh nhất quán, chưa chắc đúng.

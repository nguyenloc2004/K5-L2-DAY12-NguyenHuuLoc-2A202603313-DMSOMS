# Tự đánh giá — Nguyen Huu Loc · G03

## 1. Tự rà soát 4 cảnh

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S02_rgb, S02_ir | ghế ở rear_right | `wrong_class` | Gán `infant_seat` trong khi ghế ngồi thẳng, lưng cao → phải là `child_seat` | Có (trước export_final) |
| S04_rgb, S04_ir | `child_seat` rear_middle | `guess` | Ghi `occupied = unknown` dù thấy rõ trẻ ngồi trong ghế → phải là `yes` | Có (export_final_v2) |
| D03 | `person` | `wrong_class` | Ghi `seat = front_passenger` cho tài xế; ảnh DMS là tài xế nên `seat = driver` | Có (trước export_final) |
| D04 | `face13` miệng | `ok` | Miệng bị tay cầm cốc che hết, đã bật `outside` cho 4 điểm miệng | Không cần sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Quên đặt tag `frame_meta`. Lần kiểm đầu tiên có 5 ảnh thiếu tag: D03, D04, D05, D06 và S03_ir.

Vì sao mình mắc: Mình vẽ box ngay khi mở ảnh mới, nhất là khi copy shape từ ảnh `_rgb` sang `_ir` và khi làm nhanh các ảnh D## cuối giờ. Tag không hiện trên ảnh như box nên khó nhận ra là thiếu.

Lần sau tránh bằng cách: Đặt `frame_meta` là thao tác đầu tiên trên mỗi ảnh, trước khi vẽ bất kỳ box nào (GUIDE 4.3-1). Chạy `cabin_check --only` sau mỗi vài ảnh thay vì chờ đến cuối.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: S04 (rgb + ir), ghế trẻ em ở rear_middle. Mình ghi `occupied = unknown`, Long Nguyễn ghi `yes`.

Mình học được gì từ dòng đó: `unknown` chỉ dùng khi thật sự không thấy. Khi đã thấy rõ trẻ ngồi trong ghế mà vẫn chọn `unknown` thì đó cũng là một kiểu đoán, chỉ là đoán theo hướng "an toàn". Ghi `unknown` sai làm model mất đúng những khung cần học cho chức năng nhắc quên trẻ trong xe.

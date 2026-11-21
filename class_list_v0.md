# Danh sách lớp v0 — Nguyen Huu Loc · G03

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state (từng mắt) | open / closed / unknown | Phát hiện buồn ngủ: mắt nhắm kéo dài qua nhiều khung (PERCLOS) | Có, trừ khi đốm phản xạ trên kính che, hoặc vùng mắt sau tròng kính không đủ tương phản (G03 D05) |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung: nhìn rời khỏi đường (lap, center) quá vài giây thì cảnh báo | Có, dựa vào hướng đầu và mắt; khó khi mắt unknown |
| 3 | phone | held / mounted / lap | Phát hiện dùng điện thoại khi lái (cầm tay, áp tai) | Có nếu thấy cạnh, góc hoặc màn hình; dễ lẫn với cốc, chai |
| 4 | hand.on_wheel | yes / no / unknown (+ side, whose) | Kiểm tra tài xế còn giữ vô lăng (hands-on detection), quyết định khi nào cho phép hoặc ngắt chế độ tự lái | Có, hình dạng tay và vô lăng rõ trên NIR |
| 5 | glasses | none / clear / sun / unknown | Biết khi nào độ tin cậy của eye_state giảm (kính phản xạ LED, kính râm), để hạ ngưỡng cảnh báo hoặc chuyển sang tín hiệu đầu | Có nhưng dễ sai: kính râm có thể trông trong suốt trên NIR |
| 6 | face13 (13 điểm mặt) | điểm + cờ occluded / outside | Tính độ mở mắt, hướng đầu, ngáp (khoảng cách hai môi) cho các chức năng buồn ngủ và mất tập trung | Có, trừ điểm bị tay, cốc hoặc kính che |
| 7 | seatbelt (tài xế) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây an toàn, phát hiện thắt sai (dây sau lưng, dưới nách) | Một phần: dây tối trên áo tối khó thấy |

## OMS

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person (theo ghế) | có / không, seat | Đếm người trên xe, bật nhắc thắt dây theo từng ghế, điều chỉnh túi khí theo ghế có người | Có (hình dạng cơ thể) |
| 2 | seatbelt (hành khách) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây cho từng ghế sau; tiêu chí an toàn Euro NCAP | Một phần: mất màu dây, dễ unknown |
| 3 | infant_seat | seat, facing (rear / front) | Tắt túi khí ghế trước khi có nôi quay về sau; nhắc quên em bé trong xe | Có (hình dạng nôi, quai xách) |
| 4 | child_seat | seat, occupied (yes / no / unknown) | Nhắc quên trẻ trong xe khi tắt máy (occupied = yes); điều chỉnh túi khí | Có hình dạng ghế; trạng thái có trẻ hay không khó hơn khi ảnh tối |
| 5 | object | seat, type (bag / box / cup / other) | Nhắc quên đồ khi rời xe; phân biệt ghế có vật với ghế có người để không báo nhầm dây an toàn | Có hình dạng; mất màu nên phân biệt type chỉ bằng hình dạng (G03 S03_ir) |
| 6 | seat (vị trí ghế theo xe) | driver / front_passenger / rear_left / rear_middle / rear_right | Gắn mọi đối tượng với đúng ghế để các chức năng theo ghế (dây an toàn, túi khí) hoạt động đúng | Có; phải quy đổi vì camera nhìn về sau (trái ảnh = rear_right) |
| 7 | frame_meta.camera_blocked | yes / no | Phát hiện camera bị che để báo lỗi hệ thống thay vì đưa kết quả sai | Có |

## 2 câu hỏi leo thang

1. Câu hỏi: Tiêu chí nào để phân biệt `infant_seat` với `child_seat`? Guideline v1.0 chỉ ghi `infant_seat` là "nôi xách", không nêu đặc điểm hình dạng (quai xách, tư thế nằm ngả hay ngồi thẳng, lưng cao, tựa đầu).
   Khung ví dụ: G03 S02_rgb (ghế ở rear_right), G03 S07_rgb.
   Bạn tạm gán thế nào và vì sao: Ban đầu mình gán `infant_seat` ở S02, S04, S07, bạn review chéo gán `child_seat`. Sau review mình đổi sang `child_seat` vì ghế ngồi thẳng, lưng cao. Đề xuất guideline thêm 2–3 đặc điểm nhận dạng kèm ảnh mẫu cho mỗi loại.

2. Câu hỏi: Khi mắt không bị vật nào che nhưng ảnh NIR không đủ rõ để biết mở hay khép, các điểm mắt `face13` có cần bật cờ không? `cabin_check` cảnh báo "eye=unknown nhưng không điểm nào có cờ", trong khi guideline 4.6 chỉ dùng cờ cho điểm bị che.
   Khung ví dụ: G03 D05 (cả hai mắt), G03 D03 (mắt trái).
   Bạn tạm gán thế nào và vì sao: Ghi `eye_left`/`eye_right = unknown`, đặt các điểm mắt bình thường, không bật cờ, vì vẫn thấy được vị trí khóe và mép mí. Ghi giải thích ở cuối `check_final.txt`. Đề xuất guideline tách rõ "không thấy vị trí điểm" (cờ) với "không xác định được trạng thái" (unknown).

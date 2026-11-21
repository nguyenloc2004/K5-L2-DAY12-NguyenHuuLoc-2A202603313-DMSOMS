# Khai báo dùng AI — Nguyen Huu Loc

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Claude Code (trong VS Code) | Đọc repo lab và viết hướng dẫn từng bước làm bài; hướng dẫn gán ảnh S## và D## | Đọc để nắm thứ tự làm và quy tắc | Có, đối chiếu với GUIDE.md, CHECKPOINTS.md |
| 2 | Claude Code | Giải thích review chéo là gì, gaze_zone là gì, child_seat khác infant_seat thế nào, khác nhau giữa labels v1 và v2 | Hiểu khái niệm, tự quyết nhãn trên CVAT | Có, đối chiếu GUIDE §4.1, §4.5, §4.8 |
| 3 | Claude Code | Chạy `cabin_check check` và `diff` trên file export, ghi giải thích cảnh báo vào `check_final*.txt` | Dùng kết quả để sửa nhãn trên CVAT (thiếu frame_meta, occupied, facing, box D06) | Có, tự sửa trên CVAT và chạy lại script đến 0 lỗi |

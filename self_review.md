# Tự đánh giá — Nguyen Hoan Thien · G10

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S03 | ghế dẫn đầu (lớp ghế) | wrong_class | Bản đầu gán sai lớp ghế so với nhãn gốc SVIRO; sửa theo đối chiếu | Có |
| S08 | ghế dẫn đầu (lớp ghế) | wrong_class | Tương tự S03 | Có |
| D04 | eye_left, eye_right | guess | Ghi `open` trong khi cả 4 điểm mắt đều `occluded` và đầu cúi; `cabin_check` cảnh báo | Có (đổi sang `unknown`) |
| D06 | eye_right | guess | Ghi `open` khi tay che mặt và điểm mắt `occluded` | Có (đổi sang `unknown`) |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: ghi giá trị thuộc tính mà không thấy rõ (mắt `open`, face13 đặt theo ước lượng), thay vì `unknown` / `outside`.

Vì sao mình mắc: muốn nhãn "đầy đủ", và điểm ước lượng nhìn có vẻ hợp lý.

Lần sau tránh bằng cách: nếu điểm hoặc thuộc tính không nhìn thấy rõ thì chọn `unknown`/`outside` ngay; chạy `cabin_check` sớm để bắt cảnh báo mâu thuẫn giữa cờ `occluded` và thuộc tính mắt.

## 3. Ghi chú về disagreement_log

Làm chung với Dương Quang Chung; các chỗ sửa sau khi thống nhất được ghi trong disagreement_log.csv (26 dòng, so bản nháp ban đầu với bản cuối).

## Phần còn thiếu (thành thật)

- `face13` chỉ có ở D02, D04, D05, D06. D01 và D03 không vẽ vì người quay mặt đi, không thấy mắt, mũi, miệng.
- Nhiều điểm `face13` là vị trí ước lượng, đánh `occluded`.
- Một phần nhãn do Claude vẽ rồi tôi chỉnh (xem `prompts.md`).

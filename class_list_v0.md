# Danh sách lớp v0 — Nguyen Hoan Thien · G10

Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?** Giá trị lấy từ Guideline Cabin v1.0 (`labels_cabin_v1.json`).

## DMS (6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | face (box) | có / không vẽ | Định vị mặt tài xế để cắt vùng cho các model mắt, mặt; không có mặt thì không chạy tiếp | Có, trừ khi quay đi hoặc bị che gần hết |
| 2 | eye_left / eye_right | open / closed / unknown | Phát hiện buồn ngủ (mắt nhắm lâu, PERCLOS) | Có khi mắt rõ; mất khi kính phản xạ, cúi đầu, ảnh tối |
| 3 | gaze_zone | road, mirror_l, mirror_r, mirror_c, cluster, center, lap, other | Phát hiện xao nhãng: tài xế không nhìn đường quá lâu | Có (hướng mặt), hướng mắt khó hơn |
| 4 | face13 (13 điểm, cờ occluded/outside) | tọa độ + cờ | Tính tư thế đầu, độ mở mắt, hướng nhìn từ các điểm mắt, mũi, miệng | Có, điểm bị che phải có cờ chứ không đoán |
| 5 | hand + on_wheel | yes / no / unknown | Kiểm tra tay trên vô lăng (hands-off), hỗ trợ nhận biết dùng điện thoại | Có (hình dạng), chi tiết ngón khó |
| 6 | phone + state | held / mounted / lap | Cảnh báo dùng điện thoại khi lái | Một phần: thấy cạnh hoặc màn hình thì có, vật tối thì không |
| 7 | glasses | none / clear / sun / unknown | Chọn chiến lược đọc mắt (kính râm hoặc phản xạ làm mất tín hiệu) | Khó: kính râm có thể trông trong suốt trên NIR |
| 8 | seatbelt (person) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây an toàn | Hạn chế: dây trên áo tối khó thấy |

## OMS (6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person + seat | driver, front_passenger, rear_left, rear_middle, rear_right | Đếm người và biết ai ngồi ghế nào; bật nhắc dây an toàn theo ghế | Có (hình dáng) |
| 2 | child_seat + occupied | no / unknown (v1.0 chưa có yes, xem câu hỏi 2) | Biết ghế trẻ em có đang dùng không; điều chỉnh túi khí, nhắc thắt dây | Có (hình dạng), ghế tối trên RGB vẫn thấy ở IR-sim |
| 3 | infant_seat + facing | rear / front | Nhắc quên trẻ trong xe; tắt túi khí ghế trước khi ghế quay lưng ra trước | Có (hình dạng) |
| 4 | object + type | bag, box, cup, other | Phân biệt đồ vật với người, tránh báo nhầm có người; phát hiện đồ bỏ quên | Có (hình dạng), vật nhỏ khó hơn |
| 5 | face (người lớn ghế sau) | có / không vẽ | Xác nhận đó là người thật (không phải đồ), hỗ trợ đếm người | Có nếu quay mặt về camera |
| 6 | seat (mọi lớp) | gọi theo xe, không theo ảnh | Báo đúng ghế: camera nhìn về phía sau nên trái ảnh là phải xe | Không phụ thuộc IR, phụ thuộc quy ước camera |
| 7 | frame_meta (modality, light, camera_blocked) | ir/rgb, unknown/day/night, no/yes | Biết ảnh là IR hay RGB, ngày hay đêm, camera bị che; chọn model phù hợp | Có (suy ra từ ảnh) |

## 2 câu hỏi leo thang

1. Câu hỏi: Trẻ em hoặc em bé ngồi trong ghế (child_seat/infant_seat) có được vẽ box `person` không? GUIDE §3 nói dataset không có trẻ em và bảo báo coach, nhưng ảnh SVIRO có em bé ngồi trong ghế.
   Khung ví dụ: G10 S02, S03, S05, S07 (ghế `infant_seat` có em bé bên trong).
   Bạn tạm gán thế nào và vì sao: Không vẽ `person`, chỉ vẽ box ghế; vì guideline v1.0 nói không có trẻ em trong dataset nên không có luật cho trường hợp này, chọn cách không tự đặt luật mới.
2. Câu hỏi: `child_seat.occupied` trong guideline v1.0 chỉ có `no` và `unknown`, không có `yes`; khi ghế trẻ em rõ ràng có người ngồi thì ghi gì?
   Khung ví dụ: G10 S02 (ghế `child_seat` ở `rear_middle`).
   Bạn tạm gán thế nào và vì sao: Ghi `unknown` khi không chắc, `no` khi nhìn rõ ghế trống; không có giá trị cho "có người" nên tạm không ghi `yes`.

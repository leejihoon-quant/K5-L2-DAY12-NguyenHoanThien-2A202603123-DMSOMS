# TEAM — Ngày 12

Mã bộ ảnh: **G10** · Hình thức: **cá nhân**

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyen Hoan Thien | 2A202603123 | có | Dương Quang Chung | 61/82 dòng đã có verdict và hành động (10 nhóm ca); các dòng còn lại chưa xử lý |

Kết quả review chéo: người review **Dương Quang Chung**. Đã chạy `cabin_check diff` giữa `export_final.zip` của tôi và export của Chung trên 22 ảnh chung, ra **82 điểm khác nhau** (46 điểm là cờ `occluded` của `face13`; còn lại là thuộc tính mắt/kính, `seatbelt`, box `hand`/`person`/`object`, `infant_seat.facing`, `child_seat.occupied`). `disagreement_log.csv` liệt kê đủ 82 dòng kèm luật guideline liên quan; 10 nhóm ca (61 dòng) đã được hai bạn đọc và thống nhất phương án: 3 dòng chốt `mine` (S02 `child_seat.occupied`, D01 `face13`), 2 dòng `ambiguous` hỏi coach (S02 `person`), còn lại ghi `ambiguous` kèm luật GUIDE hai bạn thống nhất áp dụng. Các dòng còn lại ngoài 10 nhóm này chưa xử lý.

Ca chưa thống nhất / đã hỏi coach (tên ảnh + đối tượng):

- G10 S02, S03, S05, S07: ghế có em bé bên trong, chưa rõ có vẽ `person` hay không (GUIDE §3).
- G10 D01, D03: người quay mặt đi, không thấy mắt, mũi, miệng nên không vẽ `face13` (`cabin_check` cũng cảnh báo "không thấy mặt thì đừng vẽ face13"). Box `face` vẫn giữ; cần coach xác nhận.

## Cá nhân

### NguyenHoanThien-2A202603123
- Phần mình làm (ngoài 22 ảnh của mình): review chéo với Dương Quang Chung bằng `cabin_check diff` (82 điểm khác); chờ chốt verdict từng dòng.
- Điều mình học được hôm nay: Cần đọc kỹ guildline trước ghi nhắn nhãn để tiết kiệm thời gian

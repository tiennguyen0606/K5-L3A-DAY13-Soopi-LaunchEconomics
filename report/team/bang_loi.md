# Bảng lỗi và cách khắc phục · Nhiệm vụ C

20 ca lỗi nằm trong `docs/Ngay13_Lab13_De_bai_hoc_vien.docx`. Năm loại theo Google PAIR: **Do người dùng · Hệ thống · Ngữ cảnh · Giới hạn hệ thống · Ngầm**. Gắn nhãn theo nguyên nhân gốc, không theo chỗ cần sửa.

## Hai bộ nhãn độc lập

Người gắn nhãn 1: Mai Tuấn Anh (MSSV: 2A202603574) · Người gắn nhãn 2: Nguyễn Hữu Tiến (AI hỗ trợ theo xác nhận giảng viên cho phép; xem công bố trong `labels_reviewer_b.md`)

| Ca | Nhãn người 1 | Nhãn người 2 | Trùng? | Nhãn thống nhất |
| --: | --- | --- | --- | --- |
| 1 | Do người dùng | Do người dùng | Có | Do người dùng |
| 2 | Hệ thống | Hệ thống | Có | Hệ thống |
| 3 | Ngữ cảnh | Ngữ cảnh | Có | Ngữ cảnh |
| 4 | Giới hạn hệ thống | Giới hạn hệ thống | Có | Giới hạn hệ thống |
| 5 | Ngầm | Ngầm | Có | Ngầm |
| 6 | Do người dùng | Do người dùng | Có | Do người dùng |
| 7 | Hệ thống | Hệ thống | Có | Hệ thống |
| 8 | Hệ thống | Hệ thống | Có | Hệ thống |
| 9 | Do người dùng | Do người dùng | Có | Do người dùng |
| 10 | Ngữ cảnh | Ngữ cảnh | Có | Ngữ cảnh |
| 11 | Giới hạn hệ thống | Giới hạn hệ thống | Có | Giới hạn hệ thống |
| 12 | Ngầm | Ngầm | Có | Ngầm |
| 13 | Giới hạn hệ thống | Giới hạn hệ thống | Có | Giới hạn hệ thống |
| 14 | Do người dùng | Do người dùng | Có | Do người dùng |
| 15 | Hệ thống | Hệ thống | Có | Hệ thống |
| 16 | Ngữ cảnh | Ngữ cảnh | Có | Ngữ cảnh |
| 17 | Ngầm | Ngầm | Có | Ngầm |
| 18 | Ngữ cảnh | Ngữ cảnh | Có | Ngữ cảnh |
| 19 | Giới hạn hệ thống | Giới hạn hệ thống | Có | Giới hạn hệ thống |
| 20 | Hệ thống | Hệ thống | Có | Hệ thống |

**Tỉ lệ đồng thuận:** 20 / 20 = 100%

## Quy tắc phân biệt cho các ca không trùng

Mỗi ca không trùng một câu. Đồng thuận dưới 80% thì ghi định nghĩa đã viết lại.

- Không có ca bất đồng; không cần viết lại định nghĩa. Quy tắc chung được giữ nguyên: gắn theo nguyên nhân gốc, không theo vị trí cần sửa.

## Bảng khắc phục cho 5 ca, mỗi loại một ca

Cách phát hiện phải đo được (event, ngưỡng, tần suất). Người phụ trách là một vai trò, không ghi "cả đội".

| Ca | Loại lỗi | Phát hiện bằng gì | Khắc phục thế nào | Ai phụ trách |
| --: | --- | --- | --- | --- |
| 1 | Do người dùng | Theo dõi event xác thực tài khoản; cảnh báo nếu lỗi định dạng > 1% yêu cầu/ngày | Kiểm tra độ dài/định dạng trước khi tạo lệnh và yêu cầu khách xác nhận lại tài khoản | Trưởng nhóm CSKH |
| 7 | Hệ thống | Đối chiếu `refund_ledger_write` với thông báo gửi khách; ngưỡng bất kỳ ca báo thành công khi ledger lỗi | Chỉ báo thành công sau xác nhận sổ cái; retry có idempotency key và chuyển nhân viên khi hết retry | Kỹ sư trưởng agent |
| 10 | Ngữ cảnh | Theo dõi `ticket_reopened` có lý do bất khả kháng và rà hằng tuần; cảnh báo khi có >= 1 ca | Đồng bộ thông điệp “cam kết 24 giờ” với ngoại lệ chính sách và giải thích ngoại lệ trong phản hồi | PM trợ lý hoàn phí |
| 19 | Giới hạn hệ thống | Event `handoff_to_staff` với reason `older_than_12_months`, tổng hợp theo tuần | Giữ chuyển kèm tóm tắt; đánh giá mở quyền đọc kho lưu trữ nếu tần suất vượt ngưỡng vận hành | Quản lý nền tảng dữ liệu |
| 17 | Ngầm | Kiểm tra ngẫu nhiên 100 đơn/tuần qua `audit_sample_checked`; cảnh báo nếu > 1% lệch bảng giá | Gắn phiên bản bảng giá vào trace, tự xoá cache khi bảng giá đổi và đối soát các đơn bị ảnh hưởng | Kế toán trưởng |

# Báo cáo nhóm

Báo cáo ngắn, tối đa 2 trang. Số liệu chi tiết nằm trong các file hồ sơ; ở đây chỉ dẫn lại con số chính.

## 1. Thông tin nhóm

- Tên nhóm: Soopi
- Lớp: L3A
- Thành viên: xem `TEAM.md`

## 2. Mục tiêu và cách tiếp cận

Nhóm đánh giá trợ lý hoàn phí theo bốn trục: chi phí mỗi việc thành công, mức độ sử dụng, lỗi và khắc phục, và khả năng thiết kế pilot có đối chứng. Mọi số kinh tế dùng phút `_simulated` đều được ghi nhãn `simulated`; số quan sát từ trace/CSV được giữ tách biệt.

## 3. Giải pháp

Tóm tắt cách nhóm làm từng nhiệm vụ A–E và link tới file hồ sơ tương ứng.

- A/B: chạy mô hình chi phí và độ nhạy trong `src/lab13.py`, ghi kết quả tại `bang_chi_phi.md`.
- C: hai bộ nhãn được khóa trước khi đối chiếu tại `bang_loi.md`; bộ B công bố AI hỗ trợ theo xác nhận giảng viên cho phép.
- D: chọn ngẫu nhiên theo nhân viên 20 + 20, phân tầng depot, ghi tại `pilot_plan.yaml`.
- E: đặc tả chỉ số/event/rủi ro tại `chi_so.md`; tổng hợp bằng chứng tại `ho_so_launch_v0.md`.

## 4. Kết quả

Con số chính (ghi nhãn `simulated` khi cần) và đề xuất cuối của `ho_so_launch_v0.md`. Kết quả duyệt chéo nhóm nhận được từ hội đồng.

- Chi phí mỗi việc thành công: 4.472 đ [simulated], bằng 0,37x mốc 12.000 đ; chi phí cả hệ thống 5.865 đ/yêu cầu = 0,49x [simulated].
- Ba yếu tố nhạy nhất: làm lại +51,8%, xem lại +40,7%, lương nhân viên +23,1% [simulated].
- Chỉ số trong đợt chạy thử: chính 82,83%, sử dụng 27,12%, an toàn 4,25%; chưa diễn giải là tác động nhân quả.
- Pilot: MDE +6 điểm, 859 yêu cầu/nhóm, 20 cụm/nhóm, m >=299; nếu tác động thật +5 điểm thì power khoảng 0,64.
- CP3 đạt đồng thuận 20/20 = 100%; bảng khắc phục đủ năm loại.
- Đề xuất: **Go có điều kiện** cho kế hoạch pilot `noi_dia + hang_nang`; kết quả duyệt chéo vẫn chờ Gate 2a.

## 5. Khó khăn và cách xử lý

- Cỡ mẫu +5 điểm không khả thi với 40 nhân viên; nhóm ghi rõ đánh đổi sang MDE +6 điểm và power 0,64 ở tác động +5 điểm.
- Số phút xem lại/làm lại là giả lập; kế hoạch yêu cầu thay bằng phút đo thật trong pilot.
- CP3 không có ca bất đồng; phương pháp bộ B được công bố minh bạch trong `labels_reviewer_b.md`.

## 6. Tổng hợp đóng góp

Chi tiết đóng góp của từng thành viên nằm trong `TEAM.md`.

## 7. Hạn chế và hướng cải thiện

- Chưa có bằng chứng nhân quả vì đợt chạy thử không có đối chứng đồng thời.
- Cần nhận duyệt chéo thật và đo tải/lưu lượng thực tế; chưa có bằng chứng để tuyên bố đạt Gate 2a.

## 8. Tài liệu tham khảo

- `README.md`, `CHECKPOINTS.md`, `RUBRIC.md`, `SUBMISSION.md`.
- `docs/du_lieu_va_cong_thuc.md`, `docs/Lab13_Huong_dan_chi_tiet_buoi_chieu.md`.
- Dữ liệu giả lập `src/logix_runs.csv`, `src/logix_requests.csv`.

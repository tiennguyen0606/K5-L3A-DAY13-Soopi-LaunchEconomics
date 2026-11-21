# Hồ sơ launch v0 · Trợ lý hoàn phí LogiX-VN · Gate 2a

Một trang. Cột trạng thái chỉ nhận: **Xong, có bằng chứng · Chưa · Giả lập**. Mục nào dựa trên cột `_simulated` ghi Giả lập. Người phụ trách là một vai trò, không ghi "cả đội". Gate 2a chỉ duyệt kế hoạch pilot.

Nhóm: Soopi · Lớp: L3A

| Mục | Con số chính | Trạng thái | Người phụ trách |
| --- | --- | --- | --- |
| 1 · Chi phí mỗi việc thành công | Pilot: 3.414 đ biến đổi; **4.599 đ** gồm cố định [simulated]. Toàn mẫu A2 **4.472 đ** chỉ tham chiếu, không dùng cho phạm vi Go | Giả lập | PM trợ lý hoàn phí |
| 2 · Ba yếu tố nhạy nhất | 1. Làm lại (+51,8%) · 2. Xem lại (+40,7%) · 3. Lương NV (+23,1%) [simulated] | Giả lập | Trưởng nhóm phân tích vận hành |
| 3 · So với nhân viên tự làm | CPS việc thành công trong phạm vi: 0,28× biến đổi; 0,38× gồm cố định [simulated]. So sánh công bằng cả hệ thống (A2, gồm ca không thành công): **5.865 đ/yêu cầu = 0,49×** [simulated]. Loại `quoc_te` (1,88×) và `doi_tac` (0,85×) | Giả lập | PM trợ lý hoàn phí |
| 4 · Chỉ số chính, chỉ số dùng, chỉ số an toàn | Chính 82,83% (994/1.200) · Dùng 27,12% (48/177) · An toàn 4,25% (51/1.200) | Xong, có bằng chứng | Kỹ sư trưởng agent |
| 5 · Bảng lỗi và cách khắc phục | Đồng thuận 20/20 = 100%; bộ B khóa trước khi so A; bảng khắc phục đủ 5 loại; công bố AI hỗ trợ | Xong, có bằng chứng | Quản lý chất lượng hoàn phí |
| 6 · Pilot plan | 20 NV/nhóm; m≥299; MDE +6; bước 0.10/0.25 = 1 tuần, bước 0.50 ≥ 2 tuần; hoàn trùng dừng ngay | Xong, có bằng chứng | Giám đốc vận hành LogiX-VN |
| 7 · Rủi ro kinh tế | Làm lại x2: +51,8% (6.787 đ); xem lại 100%: 0,98x–1,03x (11.743–12.414 đ); khối lượng giảm 50%: định phí 2.370 đ [simulated] | Giả lập | PM trợ lý hoàn phí |

**Đề xuất:** Go có điều kiện cho kế hoạch pilot phạm vi `noi_dia + hang_nang`.

- **Điều kiện 1:** Sửa khoá chống trùng và đối soát sổ cái hai chiều (ca 7, 20) trước khi bắt đầu. Phụ trách: Kỹ sư trưởng agent; kiểm tra T-1.
- **Điều kiện 2:** Giám đốc vận hành ký chấp nhận MDE +6 điểm, rủi ro power khoảng 0,64 nếu tác động thật +5 điểm, và bước đo 0.50 ≥ 2 tuần / đủ `m ≥ 299`. Phụ trách: PM trợ lý hoàn phí; kiểm tra T-3.
- **Điều kiện 3:** Bật `request_id`/`correlation_id` cho mọi yêu cầu; `trace_id` chỉ khi có agent; chỉ số 7 ngày dùng mẫu chín; thay phút `_simulated` bằng phút đo thật sau tuần đầu. Phụ trách: Kỹ sư trưởng agent; kiểm tra T+7.
- **Điều kiện 4:** Giảm xem lại theo rollout `[0.10, 0.25, 0.50]`: 100% → 50% → 20%; không duy trì xem lại 100% kéo dài vì chi phí đạt 0,98x–1,03x nhân viên tự làm [simulated]. Phụ trách: Trưởng nhóm CSKH; kiểm tra T-2.

**Kết quả Gate 2a:** Hội đồng NhomABC chấm **30/30**, quyết định **Go có điều kiện** (xem `phieu_cham.md`). Không tuyên bố “đạt cổng” ngoài phạm vi duyệt kế hoạch pilot.

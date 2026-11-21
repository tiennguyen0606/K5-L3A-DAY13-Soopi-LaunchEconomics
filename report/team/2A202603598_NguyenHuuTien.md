# Báo cáo cá nhân — Nguyễn Hữu Tiến - 2A202603598

## 1. Thông tin thành viên

- Họ tên: Nguyễn Hữu Tiến
- MSSV: 2A202603598
- Email:
- GitHub: tiennguyen0606
- Vai trong nhóm: Người 4 — Nhóm trưởng; người gắn nhãn 2 kiêm giữ hồ sơ launch

## 2. Phần việc phụ trách

- **CP3 – Nhiệm vụ C:** Chuẩn bị bộ nhãn B cho 20 ca lỗi, phối hợp đối chiếu hai bộ nhãn, tính đồng thuận và hoàn thiện bảng khắc phục đủ năm loại.
- **CP4 – Nhiệm vụ D:** Nhận kết quả D1/D2, hoàn thiện `pilot_plan.yaml`, ghi rõ đánh đổi cỡ mẫu/power, phạm vi pilot, ba luật dừng và cơ chế rollback.
- **CP5 – Nhiệm vụ E:** Duy trì `ho_so_launch_v0.md` đủ bảy mục, tổng hợp bằng chứng chi phí, chỉ số, lỗi, pilot và rủi ro để đưa ra đề xuất có điều kiện.
- **Final:** Tổng hợp `TEAM.md`, `group_report.md`, checklist nộp bài, kiểm tra YAML/Git và điều phối tích hợp các nhánh thành viên.

## 3. Đóng góp cụ thể

- Trích đúng 20 ca lỗi và năm định nghĩa từ đề bài gốc; hoàn thiện bộ nhãn B có lý do theo nguyên nhân gốc. Bộ B được trợ lý AI hỗ trợ theo xác nhận giảng viên cho phép và được công bố minh bạch trong `labels_reviewer_b.md`.
- Đối chiếu hai bộ nhãn: 20/20 ca trùng, đồng thuận 100%; hoàn thiện năm dòng khắc phục với event/ngưỡng/tần suất đo được và một vai trò phụ trách trong `bang_loi.md`.
- Hoàn thiện thiết kế pilot theo nhân viên 20 đối chứng + 20 can thiệp, phân tầng depot; chấp nhận MDE +6 điểm với 859 yêu cầu/nhóm, `m >= 299`, DE 6,96 và power khoảng 0,64 nếu tác động thật chỉ +5 điểm.
- Ghi ba luật dừng đủ NẾU–TRONG–THÌ–KHÔNG THÌ cho an toàn, chi phí và mức độ sử dụng; khai báo rollback 30 phút, ngày quyết định và các đầu vào `simulated`.
- Tổng hợp hồ sơ launch đủ bảy mục và đề xuất **Go có điều kiện** cho kế hoạch pilot `noi_dia + hang_nang`, đồng thời nêu rõ chưa có kết quả duyệt chéo Gate 2a.
- Đồng bộ nhánh, tạo PR cho phần CP4, xử lý xung đột hồ sơ CP5 mà không ghi đè thay đổi của thành viên khác.

## 4. Bằng chứng

- Commit `2ca9bbd` — `docs: record evidence-backed CP4 pilot design`; Pull Request #5 đã merge vào `main`.
- `report/team/labels_reviewer_b.md`: 20 ca có nhãn, lý do và công bố phương pháp.
- `report/team/bang_loi.md`: hai bộ nhãn, đồng thuận 20/20 và năm ca khắc phục.
- `report/team/pilot_plan.yaml`: D1/D2, thiết kế 20 + 20, ba luật dừng, rollback và simulated inputs; đọc được bằng `yaml.safe_load`.
- `report/team/ho_so_launch_v0.md`: hồ sơ đủ bảy mục và bốn điều kiện có vai trò/mốc kiểm tra.
- `TEAM.md`, `report/team/group_report.md`, `report/team/NGUOI4_CHECKLIST.md`: tài liệu tổng hợp và kiểm tra Final.

## 5. Công cụ AI đã dùng

- Công cụ: OpenAI Codex.
- Mục đích: đọc tài liệu và DOCX gốc, chuẩn bị bảng nhãn, kiểm tra công thức/cỡ mẫu, soát YAML/Markdown, hỗ trợ gắn nhãn B theo xác nhận của Người 4 rằng giảng viên cho phép, và rà quy trình Git.
- Cách tự kiểm tra: chạy `python lab13.py`; đối chiếu số với `bang_chi_phi.md`, `chi_so.md` và hướng dẫn repo; kiểm tra `yaml.safe_load`, đủ 20 ID/5 loại lỗi, công thức đồng thuận, `git diff --check`, conflict marker và từ bị cấm.
- Giới hạn: Không tự tạo kết quả Gate 2a; mọi số từ `_simulated` được gắn nhãn; việc AI hỗ trợ bộ B được công bố thay vì mô tả là hoàn toàn thủ công.

## 6. Tự đánh giá

- Đã hoàn thành nội dung CP3, CP4 và CP5-E thuộc phạm vi Người 4; hồ sơ sẵn sàng cho duyệt chéo.
- Điểm mạnh: giữ phạm vi, dẫn nguồn số liệu, không ghi đè phần người khác và nêu rõ các đánh đổi bất lợi trước khi đề xuất.
- Việc còn lại: tham gia Gate 2a, ghi phiếu/chất vấn thật, nhận kết quả hội đồng và hoàn tất commit chốt sau kiểm tra toàn nhóm.

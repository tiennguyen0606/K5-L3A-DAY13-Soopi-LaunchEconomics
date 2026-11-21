# Đặc tả chỉ số, event và rủi ro kinh tế · Nhiệm vụ E1, E2

## E1 · Đặc tả chỉ số

| Loại | Chỉ số | Công thức | Tính thử trên 1.200 yêu cầu |
| --- | --- | --- | --- |
| Chính (kết quả) | % yêu cầu đóng trong 24 giờ và không mở lại trong 7 ngày | `dong_trong_24h` bằng 1 và `mo_lai_trong_7_ngay` bằng 0, chia tổng số yêu cầu | 82,83% (994/1.200) |
| Dùng | Tỉ lệ bỏ qua gợi ý | `quyet_dinh_xem_lai` là `sua` hoặc `bo`, chia số yêu cầu được xem lại | 27,12% (48/177) |
| An toàn | Tỉ lệ lỗi lọt đến khách | `mo_lai_trong_7_ngay` bằng 1, chia tổng số yêu cầu | 4,25% (51/1.200) |
| Dùng | Nhóm tự đề xuất: Tỉ lệ yêu cầu được xử lý qua trợ lý | Số yêu cầu được mở qua giao diện trợ lý chia cho tổng số yêu cầu của nhóm can thiệp | Không cần tính |
| An toàn | Nhóm tự đề xuất: Tỉ lệ sai sót tiền hoàn qua kiểm tra mẫu ngẫu nhiên | Số đơn lệch tiền hoàn chia cho số đơn kiểm tra đối soát độc lập hằng tuần (bắt lỗi ngầm) | Không cần tính |

*Lưu ý:* Chỉ số trong đợt chạy thử là 82,83%, không viết "trợ lý đã nâng chỉ số từ 0,70" vì đợt chạy thử chưa có nhóm đối chứng đồng thời.

## Schema event chuẩn hóa

Mọi event phải tuân schema tối thiểu dưới đây; thiếu trường bắt buộc thì event không được dùng để tính chỉ số.

| Trường | Bắt buộc | Kiểu / quy ước | Mục đích |
| --- | --- | --- | --- |
| `event_name` | Có | một trong 10 tên ở bảng dưới | Định danh loại sự kiện |
| `request_id` | Có | chuỗi ổn định theo yêu cầu hoàn phí | Khóa join chính giữa mọi event |
| `trace_id` | Có | chuỗi theo một lần chạy agent | Lần theo trace; một request có thể nhiều trace |
| `ts` | Có | ISO-8601 GMT+7 | Thời điểm phát sinh |
| `arm` | Có với event thuộc pilot | `control` / `treatment` | Tách nhóm khi tính chỉ số pilot |
| `days_since_close` | Có với `ticket_reopened` | số ngày lịch sau `ticket_closed.closed_at` | Cửa sổ theo dõi mở lại = 7 ngày |

## Danh sách event

Ít nhất sáu event. Mỗi event bắt buộc có **`request_id`** và **`trace_id`** (và `ts`). Thiết kế chuẩn 10 event:

| Event | Ai tạo | Thuộc tính chính | Thời điểm |
| --- | --- | --- | --- |
| `refund_request_created` | App khách hàng | `request_id`, `loai`, `so_tien`, `arm`, `trace_id`, `created_at` | Khi khách hàng gửi yêu cầu hoàn phí |
| `agent_run_completed` | Trợ lý agent | `request_id`, `attempt`, `tokens_in`, `tokens_out`, `tool_calls`, `status`, `trace_id` | Sau mỗi lần agent chạy xong (kể cả lỗi) |
| `agent_suggestion_shown` | UI CSKH | `request_id`, `staff_id`, `so_tien_de_xuat`, `trace_id` | Khi đề xuất hoàn tiền hiện lên màn hình |
| `staff_review_decision` | Nhân viên CSKH | `request_id`, `decision` (giu/sua/bo), `phut_xem_lai`, `trace_id` | Khi nhân viên bấm duyệt, sửa hoặc bỏ qua |
| `staff_rework_completed` | Nhân viên CSKH | `request_id`, `phut_lam_lai`, `ly_do`, `trace_id` | Khi hoàn thành xử lý lại ca bị lỗi |
| `refund_ledger_write` | Dịch vụ sổ cái | `request_id`, `idempotency_key`, `so_tien`, `status`, `trace_id` | Khi thực hiện ghi lệnh hoàn tiền vào sổ cái |
| `handoff_to_staff` | Trợ lý agent | `request_id`, `reason`, `tom_tat`, `trace_id` | Khi agent bỏ cuộc chuyển cho nhân viên làm |
| `ticket_closed` | Hệ thống ticket | `request_id`, `closed_at`, `duration_hours`, `trace_id` | Khi ticket khiếu nại hoàn tất đóng |
| `ticket_reopened` | Khách hàng | `request_id`, `reopened_at`, `reason`, `trace_id`, `days_since_close` | Khi khách mở lại ticket; chỉ tính vào chỉ số nếu `0 < days_since_close ≤ 7` |
| `audit_sample_checked` | Ban kiểm toán/Kế toán | `request_id`, `so_tien_da_hoan`, `so_tien_chuan`, `ket_luan`, `trace_id` | Khi kiểm tra ngẫu nhiên mẫu đối soát hàng tuần |

**Quy tắc nối sự kiện**

- Khóa chính theo yêu cầu: luôn join theo `request_id`.
- `trace_id` dùng để lần theo một lần chạy agent; một `request_id` có thể có nhiều `trace_id` nếu chạy lại.
- Cửa sổ theo dõi mở lại: **7 ngày lịch** kể từ `ticket_closed.closed_at` của cùng `request_id`. Event `ticket_reopened` ngoài cửa sổ này không vào tử số chỉ số chính/an toàn.

**Kiểm tra chéo:** với mỗi chỉ số ở bảng E1, ghi event dùng để tính. Chỉ số nào không tính được từ danh sách event thì chưa đo được.

- **Chỉ số chính (% đóng 24h & không mở lại 7 ngày):** `ticket_closed` có `duration_hours ≤ 24` theo `request_id`; và **không** có `ticket_reopened` cùng `request_id` trong cửa sổ 7 ngày sau `closed_at`. Không ghép chỉ bằng `trace_id`.
- **Chỉ số dùng (Tỉ lệ bỏ qua gợi ý):** Đếm `staff_review_decision` có `decision ∈ {sua, bo}` chia tổng `staff_review_decision`, join theo `request_id`.
- **Chỉ số an toàn (Tỉ lệ lỗi lọt đến khách):** Số `request_id` có ≥1 `ticket_reopened` trong cửa sổ 7 ngày sau lần đóng gần nhất, chia tổng `refund_request_created`.
- **Chỉ số dùng tự đề xuất (% yêu cầu mở qua trợ lý):** Đếm `request_id` có `agent_suggestion_shown` chia tổng `refund_request_created` của nhóm can thiệp (`arm`).
- **Chỉ số an toàn tự đề xuất (% sai lệch kiểm toán):** Đếm `audit_sample_checked` có `so_tien_da_hoan != so_tien_chuan` chia tổng `audit_sample_checked` (theo `request_id`).

## E2 · Rủi ro kinh tế

Ít nhất hai dòng, số lấy trực tiếp từ bảng độ nhạy (`bang_chi_phi.md`).

| Rủi ro | Tác động đã tính | Dấu hiệu theo dõi | Hành động | Người phụ trách |
| --- | --- | --- | --- | --- |
| Số ca làm lại tăng gấp đôi | Chi phí mỗi việc tăng +51,8% lên 6.787 đ [simulated] | Tỉ lệ ca làm lại theo tuần > 7% (đợt chạy thử: 4,9% trong phạm vi) | Thu hẹp phạm vi về riêng `noi_dia`, rà soát 20 trace làm lại gần nhất | PM trợ lý hoàn phí |
| Phải xem lại 100% kéo dài | Chi phí lên 11.743 đ = 0,98× (hoặc 12.414 đ = 1,03× nếu làm lại 15,3 phút), trợ lý mất hoàn toàn lợi thế kinh tế [simulated] | Tỉ lệ yêu cầu phải xem lại vẫn > 50% ở cuối bước rollout 0.10 | Giảm xem lại theo rollout 0.10→100%, 0.25→50%, 0.50→20% khi tỉ lệ sửa/bỏ < 15% | Trưởng nhóm CSKH |
| Khối lượng xử lý thấp hơn dự kiến | Chi phí cố định 40 tr/tháng phân bổ tăng từ 1.185 đ/việc lên 2.370 đ/việc nếu khối lượng giảm một nửa [simulated] | Số việc thành công hàng tuần đạt < 50% kế hoạch (dưới 3.900 việc/tuần) | Tạm dừng mở rộng pilot, đàm phán lại hợp đồng chi phí cố định hạ tầng | PM trợ lý hoàn phí |
| Tối ưu sai cục bộ số lần chạy lại | Chi phí cả hệ thống tăng lên 7.449.781 đ (+548.561 đ) nếu ép chạy 1 lần [simulated] | Tỉ lệ yêu cầu không thành công chuyển nhân viên > 25% | Cố định giới hạn `max_attempts = 2` theo tối ưu tổng chi phí toàn công ty | Kỹ sư trưởng agent |

### Phân tích chi tiết rủi ro kinh tế từ bảng độ nhạy

1. **Rủi ro số ca làm lại (Rủi ro biến phí lớn nhất - Xếp hạng 1 độ nhạy):**
   - *Bản chất:* Trong cơ cấu chi phí, thời gian nhân viên làm lại chiếm tới **51,8%** (2.264.000 đ [simulated]), trong khi token và tool chỉ chiếm 7,5%. Do đó, biến động về lỗi dẫn đến làm lại tạo tác động đòn bẩy lớn nhất lên hiệu quả kinh tế.
   - *Kịch bản rủi ro:* Nếu tỷ lệ lỗi tăng khiến số ca làm lại tăng gấp đôi, chi phí mỗi việc thành công nhảy vọt từ 4.472 đ lên **6.787 đ (+51,8%)** [simulated]. Nếu kết hợp đồng thời với lương nhân viên tăng 25%, chi phí sẽ lên gần 8.000 đ/việc.
   - *Biện pháp kiểm soát:* Cắt bỏ ngay các phân khúc có tỷ lệ lỗi cao (`quoc_te` chỉ thành công 27,3% với chi phí 22.515 đ = 1,88× nhân viên; `doi_tac` chỉ thành công 54,4% với chi phí 10.215 đ = 0,85×); tập trung bảo vệ luồng `noi_dia` (thành công 95%, chi phí chỉ 2.696 đ = 0,22×).

2. **Rủi ro chi phí xem lại 100% (Rủi ro xói mòn toàn bộ biên tiết kiệm - B4):**
   - *Bản chất:* Nếu nhân viên CSKH chưa tin tưởng trợ lý và duy trì việc duyệt 100% yêu cầu với thời gian trung bình 5 phút/ca, tiền xem lại sẽ chiếm tới ~90% tổng chi phí (9.480.000 đ cho 900 việc).
   - *Kịch bản rủi ro:* Chi phí mỗi việc thành công sẽ bị đẩy lên **11.743 đ = 0,98×** mức 12.000 đ của nhân viên tự làm [simulated]. Đặc biệt, nếu tính thời gian làm lại thực tế từ dữ liệu (15,3 phút/ca), chi phí sẽ chạm **12.414 đ = 1,03×** [simulated] — tức trợ lý gây lỗ cho công ty. Điểm hòa vốn yêu cầu thời gian xem lại phải $\le$ 4,8 phút.
   - *Biện pháp kiểm soát:* Khớp rollout trong `pilot_plan.yaml` `[0.10, 0.25, 0.50]` (mỗi bước một tuần): bước **0.10** xem lại 100%, bước **0.25** xem lại 50%, bước **0.50** xem lại 20%; chỉ sang bước sau khi tỷ lệ sửa/bỏ của nhân viên duy trì dưới ngưỡng an toàn 15%.

3. **Rủi ro chi phí cố định theo quy mô (Kinh tế quy mô - A4):**
   - *Bản chất:* Chi phí cố định hạ tầng 40.000.000 đ/tháng được phân bổ trên số lượng việc thành công.
   - *Kịch bản rủi ro:* Tại quy mô chuẩn 45.000 yêu cầu/tháng (33.750 việc thành công), chi phí cố định là 1.185 đ/việc. Nhưng nếu quy mô chỉ đạt 50% (16.875 việc), chi phí cố định đội lên **2.370 đ/việc**, nâng tổng chi phí lên 5.784 đ/việc [simulated]. Nếu quy mô pilot quá nhỏ (dưới 4.660 việc thành công/tháng), định phí phân bổ sẽ vượt 8.586 đ, khiến tổng chi phí vượt quá 12.000 đ.
   - *Biện pháp kiểm soát:* Đặt ngưỡng tối thiểu về lưu lượng tiếp nhận trước khi triển khai pilot và đàm phán hợp đồng hạ tầng linh hoạt theo lượng dùng thực tế.

4. **Rủi ro tối ưu hóa cục bộ số lần chạy lại (Sub-optimization - B3):**
   - *Bản chất:* Giới hạn chạy lại 1 lần cho chi phí mỗi việc thành công của trợ lý thấp nhất (4.111 đ [simulated]), nhưng lại đẩy 319 yêu cầu không thành công sang cho nhân viên giải quyết thủ công.
   - *Kịch bản rủi ro:* Chi phí toàn công ty khi chạy 1 lần là 7.449.781 đ [simulated], đắt hơn mức **6.901.220 đ** [simulated] khi cho phép chạy lại 2 lần (tiết kiệm ròng 548.561 đ cho công ty).
   - *Biện pháp kiểm soát:* Khóa cứng cấu hình `max_attempts = 2` trong hệ thống agent, ngăn chặn việc can thiệp hạ giới hạn nhằm làm đẹp chỉ số cục bộ của trợ lý.

# Ghi chú chuẩn bị và bàn giao CP4 · Người 4

Trạng thái: **CP4 đã đủ bằng chứng theo yêu cầu repo**. D1, thiết kế 20 + 20, đánh đổi power, D2, baseline an toàn, scope, ba luật dừng, rollback và ngày quyết định đã được điền. Cần giữ file này làm dấu vết bàn giao; file nộp chính là `pilot_plan.yaml`.

## Thiết kế đã có nguồn

| Nội dung | Giá trị có thể dùng | Nguồn |
| --- | --- | --- |
| Owner có quyền dừng | Giám đốc vận hành LogiX-VN | Bối cảnh và yêu cầu owner theo vai trò trong đề bài/CP4 |
| Chỉ số chính | `dong_trong_24h_khong_mo_lai_7_ngay` | Mẫu `pilot_plan.yaml` |
| Baseline | 0,70 | `docs/du_lieu_va_cong_thuc.md`, mục Số liệu dùng chung |
| MDE ban đầu | 0,05 | `docs/du_lieu_va_cong_thuc.md`; phải thay nếu Người 2 chứng minh và nhóm chấp nhận đánh đổi khác |
| Alpha / power / ICC | 0,05 / 0,80 / 0,02 | `docs/du_lieu_va_cong_thuc.md` |
| Quy mô | 40 nhân viên, 12 depot, khoảng 1.500 yêu cầu/ngày | `README.md` và tài liệu dữ liệu |
| Tỉ lệ mở lại hiện tại | 51/1.200 = 4,25% | Tính trực tiếp, chỉ đọc từ `src/logix_requests.csv`: đếm `mo_lai_trong_7_ngay == 1` / tổng số dòng |
| Tỉ lệ mở lại trong phạm vi | 39/982 = 3,97% cho `noi_dia + hang_nang` | Tính trực tiếp từ CSV và được `src/lab13.py` in ra |
| D1 +5 điểm | 1.251/nhóm; staff m=75 cần 3.103/nhóm, 42 người/nhóm; 20 staff có n_eff tối đa <1.000; 6 depot có n_eff tối đa <300 | Output `chay_nhiem_vu_d` trong `src/lab13.py` |
| Thiết kế chọn | Ngẫu nhiên theo nhân viên, 20 đối chứng + 20 can thiệp, phân tầng depot | Output D2 trong `src/lab13.py` |
| Đánh đổi +6 điểm | 859/nhóm; m >=299; DE 6,96; n_eff 859,2; power khoảng 0,64 nếu tác động thật +5 điểm | Output và công thức CP4 trong `src/lab13.py` |
| Khả thi công suất | Khoảng 7,97 ngày nếu tính toàn bộ lưu lượng; khoảng 9,74 ngày nếu ước tính theo tỷ trọng phạm vi 81,83% trong mẫu | Ước tính từ 1.500 yêu cầu/ngày và 40 nhân viên; không phải dữ liệu pilot đo thực tế |
| Rollout mẫu | 0,10 → 0,25 → 0,50, mỗi bước một tuần | Mẫu `pilot_plan.yaml` |
| Interim looks | Chỉ kiểm tra chỉ số an toàn | Mẫu `pilot_plan.yaml` |

## Khung luật dừng NẾU – TRONG – THÌ – KHÔNG THÌ

Ba luật đã được chép vào YAML theo đúng bốn vế và ngưỡng/cửa sổ trong hướng dẫn chính thức của repo:

1. **Khẩn cấp – hoàn trùng:** ≥1 ca hoàn tiền trùng → dừng **ngay** (emergency_stop), không chờ 3 ngày.
2. **An toàn – mở lại:** cao hơn đối chứng ≥2 điểm hoặc vượt trần 6% trong **3 ngày liên tiếp** → tắt trong 30 phút.
3. **Chi phí:** CPS phạm vi pilot > 8.000 đ trong 2 tuần liên tiếp; PM thu hẹp về `noi_dia` và giới hạn 2 lần chạy.
4. **Mức độ sử dụng:** bỏ qua gợi ý trên 40% trong 1 tuần; Trưởng nhóm CSKH phỏng vấn 5 nhân viên trong 3 ngày.

Rollout chính thức: `0.10` / `0.25` / `0.50` = xem lại 100% / 50% / 20%. Không dùng bước 0.75.

Mỗi luật cuối cùng phải có đủ: chỉ số đo được, toán tử/ngưỡng, thời hạn, hành động cụ thể, một vai trò có quyền, và việc bị cấm ở vế KHÔNG THÌ.

Lưu ý an toàn: baseline quan sát hiện tại là 4,25%, nên không được chọn một trần tuyệt đối thấp hơn mức này mà không có thiết kế so với đối chứng hoặc lý do đã được duyệt; nếu không, pilot có thể dừng ngay từ đầu. Con số này là dữ liệu quan sát, không dùng hai cột `_simulated`.

## Bàn giao đã nhận

| Trường / phần | Nguồn | Bằng chứng |
| --- | --- | --- |
| `scope`, ngưỡng chi phí | A3/B và hướng dẫn repo | `noi_dia + hang_nang`; 8.000 đ trong 2 tuần |
| Ngưỡng sử dụng | E1 và hướng dẫn repo | Baseline 27,12%; ngưỡng 40% trong 1 tuần |
| Ngưỡng an toàn | CSV và hướng dẫn repo | Baseline 4,25%/3,97%; +2 điểm so đối chứng hoặc trần 6% |
| `rollback` | Hướng dẫn repo | Giám đốc vận hành, hiệu lực 30 phút, luồng nhân viên tự làm |
| `decision_date` | Hướng dẫn repo | 2027-01-05 |
| `simulated_inputs` | A3 | Bốn chi phí/tỉ số theo loại, ghi rõ `simulated` trong YAML |

## Kiểm tra trước khi merge/nộp

- Không còn marker `CHỜ_` hoặc dấu `?` ngoài chú thích.
- Giữ ít nhất ba luật dừng đủ bốn vế.
- Chạy `yaml.safe_load`, rồi tìm dấu `?` ngoài chú thích.
- Chỉ giữ trạng thái hoàn thành khi YAML hợp lệ và ba luật dừng vẫn có đủ ngưỡng, thời hạn, hành động và vai trò.

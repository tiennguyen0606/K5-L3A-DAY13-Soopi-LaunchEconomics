# Phiếu chấm hội đồng Gate 2a

Nhóm số n chấm nhóm số n + 1; nhóm cuối chấm nhóm 1. Chấm theo bằng chứng trong hồ sơ, không theo cách trình bày: một đề xuất No-go có lý do bằng số được điểm cao hơn một đề xuất Go bỏ qua con số bất lợi.

- **Nhóm chấm (hội đồng):** Soopi-L3A.
- **Nhóm được chấm:** NhomABC — L3A.
- **Repository:** https://github.com/LufkyMama/K5-L3A-DAY13-NhomABC-LaunchEconomics
- **Phiên bản được đối chiếu:** `main` tại commit `992a07b53f3c4ea0e18aa21d7a25e102c054d11a` (21/11/2026).

| Tiêu chí | 0 điểm | 5 điểm | 10 điểm | Điểm | Lý do (có số) |
| :--- | :--- | :--- | :--- | ---: | :--- |
| Đề xuất khớp bằng chứng | Mâu thuẫn với số của chính nhóm | Khớp nhưng bỏ qua một con số bất lợi | Khớp, nêu cả con số bất lợi và cách xử lý | **10** | Đề xuất **Go có điều kiện**, chỉ cho `noi_dia + hang_nang`: chi phí biến đổi **3.414 đ/việc**, cộng chi phí cố định thành **4.599 đ/việc** tại **45.000 yêu cầu/tháng** [simulated]. Không giấu trường hợp bất lợi: `quoc_te` **22.515 đ/việc = 1,88×** mốc **12.000 đ**, thành công **27,3%**; xem lại 100% có thể lên **12.415 đ/việc** [simulated]; làm lại ×2 làm chi phí lên **6.787 đ (+51,8%)** [simulated]; power chỉ **0,64** nếu tác động thật là **+5 điểm**. Có điều kiện xử lý: loại `quoc_te`, kiểm tra chống hoàn trùng trước **01/12/2026**, chấp nhận đánh đổi MDE **6 điểm**, và đo phút thực trong pilot. |
| Số giả lập và phạm vi | Không nhãn; phạm vi "mọi yêu cầu" | Có nhãn hoặc có thu hẹp phạm vi | Nhãn ở mọi số giả lập; phạm vi thu hẹp có lý do bằng số | **5** | Thu hẹp phạm vi rõ, có định lượng: `noi_dia` **2.696 đ/việc (0,22×)**, `hang_nang` **8.221 đ/việc (0,69×)**, loại `quoc_te` **1,88×**; `doi_tac` **0,85×** nhưng loại do điều khoản riêng. Tuy nhiên **chưa nhất quán nhãn ở mọi số lấy từ dữ liệu lab giả lập**: trong `chi_so.md`, các tỷ lệ **82,83% (994/1.200)**, **27,12% (48/177)** và **4,25% (51/1.200)** được trình bày là chỉ số chạy thử nhưng không gắn nhãn `simulated` ngay tại từng số; trong `ho_so_launch_v0.md`, mục chỉ số tương ứng được ghi **“Xong, có bằng chứng”**, dễ khiến người đọc nhầm với số thực tế triển khai. Dữ liệu lab có thể là bằng chứng về phép tính, **không** phải bằng chứng thực địa. Chưa đạt mức 10 yêu cầu nhãn nhất quán ở tất cả số giả lập. |
| Pilot ra được quyết định | Không đối chứng hoặc thiếu cỡ mẫu | Đủ cỡ mẫu, luật dừng chung chung | Tách được tác động, đủ mẫu, luật dừng có ngưỡng, thời hạn, người có quyền dừng | **10** | Có đối chứng đồng thời **20 nhân viên/nhóm**, phân ngẫu nhiên theo `staff_id` với `seed 1304`, phân tầng depot, giảm lan truyền và phân tích theo phân công ban đầu. Nhóm nhận ra MDE **5 điểm** cần **1.251 yêu cầu hiệu dụng/nhóm** theo tính toán của nhóm; với **20 cụm/nhóm** chọn MDE **6 điểm**, `n_eff = 859/nhóm`, **299 yêu cầu/nhân viên**, **5.980 yêu cầu thực/nhóm**, **DE = 6,96**, và thừa nhận power **0,64** nếu tác động thật chỉ **5 điểm**. Có **4 luật dừng** cụ thể: hoàn trùng **≥1 ca/ngày**, mở lại **>6% hoặc hơn đối chứng ≥2 điểm trong 3 lần rà**, chi phí **>8.000 đ trong 2 tuần**, bỏ gợi ý **>40% trong 1 tuần**; phân rõ vai trò có quyền dừng/giữ pha, rollback **30 phút**, chốt ngày **25/01/2027**. **Lưu ý trước khi triển khai:** kế hoạch chưa chứng minh từ công suất thực rằng pha cuối **02–15/01/2027** thu đủ **5.980 yêu cầu hợp lệ mỗi nhóm**; đây là điều kiện kiểm tra, không phủ nhận thiết kế cỡ mẫu đã công khai. |
| **Tổng** | | | | **25 / 30** | **10 + 5 + 10 = 25 điểm.** |

**Quyết định của hội đồng:** **Go có điều kiện**.

**Lý do:** Đề xuất có cơ sở kinh tế trong phạm vi đã thu hẹp: **4.599 đ/việc thành công** khi cộng cố định ở giả định **45.000 yêu cầu/tháng**, so với mốc nhân viên tự làm **12.000 đ/việc** [simulated]. Hội đồng ghi nhận nhóm không che giấu rủi ro xem lại 100% (**12.415 đ/việc** trong một kịch bản [simulated]), rủi ro hiệu ứng thật +5 điểm chỉ có power **0,64**, và đã có đối chứng 20 + 20 cùng 4 luật dừng định lượng. **Chưa được coi là chấp thuận pilot vô điều kiện**: (1) xác minh chống hoàn trùng và sổ cái trước **01/12/2026**; (2) thống nhất đánh đổi MDE **6 điểm** bằng chữ ký người chịu trách nhiệm; (3) ghi nhãn `simulated` ngay cạnh mọi tỷ lệ/số chi phí từ dữ liệu lab, đặc biệt các số **82,83%**, **27,12%**, **4,25%**; (4) xác nhận năng lực nhận mẫu đủ **5.980 yêu cầu hợp lệ/nhóm** trong cửa sổ phân tích và dời quyết định nếu thiếu mẫu, lệch cụm hoặc chưa đủ **7 ngày** theo dõi mở lại. Chỉ chuyển pha khi dữ liệu vận hành thực đáp ứng ngưỡng an toàn và chi phí.

**Một câu hỏi cho đội trình:** Với pha phân tích chính chỉ diễn ra **02–15/01/2027**, nhóm dựa vào bằng chứng công suất nào để đảm bảo thu đủ **5.980 yêu cầu hợp lệ/nhóm** (tương đương trung bình khoảng **427 yêu cầu/nhóm/ngày**, **21,4 yêu cầu/nhân viên/ngày** nếu phân đều 14 ngày) và vẫn theo dõi đủ **7 ngày** mở lại, khi trước đó nhóm chỉ có dữ liệu giả lập từ **1.200 yêu cầu**? Nếu không đủ cỡ mẫu, ai có quyền lùi ngày **25/01/2027** và quyết định theo quy tắc nào?

**Câu trả lời của đội trình (ghi lại tại buổi):** **Chưa có câu trả lời trực tiếp tại buổi bảo vệ.** Hội đồng để trống phần nội dung phát biểu, không tự viết thay đội trình.

---

**Các nguồn bằng chứng đã đối chiếu:**

- [Hồ sơ launch v0](https://github.com/LufkyMama/K5-L3A-DAY13-NhomABC-LaunchEconomics/blob/main/report/team/ho_so_launch_v0.md) — đề xuất, số bất lợi, điều kiện Go.
- [Bảng chi phí](https://github.com/LufkyMama/K5-L3A-DAY13-NhomABC-LaunchEconomics/blob/main/report/team/bang_chi_phi.md) — CP1, CP2, độ nhạy và chi phí làm lại.
- [Đặc tả chỉ số](https://github.com/LufkyMama/K5-L3A-DAY13-NhomABC-LaunchEconomics/blob/main/report/team/chi_so.md) — cách tính chỉ số và nhãn giả lập.
- [Kế hoạch pilot](https://github.com/LufkyMama/K5-L3A-DAY13-NhomABC-LaunchEconomics/blob/main/report/team/pilot_plan.yaml) — đối chứng, cỡ mẫu, luật dừng và thời hạn.
- [Bảng lỗi](https://github.com/LufkyMama/K5-L3A-DAY13-NhomABC-LaunchEconomics/blob/main/report/team/bang_loi.md) — phân loại lỗi và biện pháp kiểm soát hoàn trùng.

*Phương pháp chấm: đúng thang 0/5/10 của phiếu Gate 2a; chỉ ghi nhận bằng chứng có trong repo tại phiên bản nêu trên. Điểm 10 ở pilot là đánh giá **thiết kế kế hoạch**, không xác nhận đã thu đủ mẫu ngoài thực tế.*

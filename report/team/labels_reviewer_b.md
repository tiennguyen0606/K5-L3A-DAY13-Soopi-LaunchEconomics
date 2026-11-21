# Phiếu gắn nhãn độc lập B · CP3

Người gắn nhãn: **Người 4 – người gắn nhãn 2, kiêm giữ hồ sơ**  
Thời điểm bắt đầu: ______ · Thời điểm kết thúc: ______  
Cam kết: gắn đủ 20 ca trong 8 phút, không trao đổi và không xem bộ nhãn A trước khi khóa bộ B.

**Công bố phương pháp:** bộ B được trợ lý AI hỗ trợ theo xác nhận của Người 4 rằng giảng viên cho phép. Người 4 đã yêu cầu rà soát và tiếp tục đối chiếu; kết quả được khóa tại thời điểm này và không sửa hồi tố sau khi xem bộ A.

Nguồn ca lỗi và định nghĩa: `docs/Ngay13_Lab13_De_bai_hoc_vien.docx`, mục **Nhiệm vụ C**, bảng **Năm loại lỗi** và **Hai mươi ca lỗi**.

## Năm loại lỗi

| Nhãn hợp lệ | Định nghĩa theo đề bài gốc |
| --- | --- |
| Do người dùng | Người dùng nhập sai hoặc chọn sai. |
| Hệ thống | Hệ thống trả lời sai hoặc làm sai so với thiết kế và chính sách. |
| Ngữ cảnh | Hệ thống làm đúng thiết kế nhưng người dùng thấy là sai, vì giả định của hệ thống không khớp hoàn cảnh của họ. |
| Giới hạn hệ thống | Hệ thống không thể trả lời, do thiếu dữ liệu, ngoài phạm vi, hoặc dạng đầu vào không xử lý được. |
| Ngầm | Có sai nhưng cả người dùng lẫn hệ thống đều không nhận ra. |

## Bộ nhãn B — đã khóa sau rà soát

Chỉ điền cột **Nhãn độc lập B** và **Lý do theo nguyên nhân gốc**. Sau khi đủ 20 dòng, đổi trạng thái từng dòng từ `Chưa gắn` thành `Đã khóa`; không sửa nhãn sau khi xem bộ A.

| ID | Mô tả ca (nguyên văn, đúng thứ tự đề bài) | Nhãn độc lập B | Lý do theo nguyên nhân gốc | Trạng thái |
| --: | --- | --- | --- | --- |
| 1 | Khách nhập số tài khoản nhận hoàn tiền thiếu hai chữ số. Trợ lý tạo lệnh hoàn, ngân hàng trả về lỗi. | Do người dùng | Nguyên nhân gốc là khách nhập thiếu dữ liệu tài khoản; hệ thống chỉ nhận lỗi từ ngân hàng sau đó. | Đã gắn |
| 2 | Kiện nội địa 28 kg. Trợ lý gọi tool tra bảng giá với tham số hàng thường thay vì hàng nặng, hoàn thiếu 45.000 đ. Khách mở lại sau 2 ngày. | Hệ thống | Trợ lý chọn sai tham số tool so với trọng lượng và chính sách, dẫn đến tính sai tiền hoàn. | Đã gắn |
| 3 | Theo thiết kế, trợ lý hoàn tiền về ví LogiX trong 5 phút. Khách chờ tiền về tài khoản ngân hàng và báo “chưa được hoàn”. | Ngữ cảnh | Hệ thống làm đúng thiết kế nhưng giả định về nơi nhận tiền không khớp kỳ vọng của khách. | Đã gắn |
| 4 | Khách yêu cầu hoàn phí cho chặng do hãng nước ngoài giao. LogiX không có dữ liệu chặng này. Trợ lý nói không xác định được trạng thái và chuyển cho nhân viên. | Giới hạn hệ thống | Trợ lý không thể xử lý vì LogiX thiếu dữ liệu của chặng do hãng nước ngoài giao. | Đã gắn |
| 5 | Kiểm tra mẫu cuối tuần thấy 14 đơn có mã giảm giá bị hoàn theo giá trước giảm, thừa trung bình 12.000 đ mỗi đơn. Không khách nào báo, không cảnh báo nào kích. | Ngầm | Sai tiền tồn tại nhưng cả khách và hệ thống đều không nhận ra cho tới kiểm tra mẫu cuối tuần. | Đã gắn |
| 6 | Khách chọn mục “Hoàn phí giao trễ” nhưng nội dung mô tả hàng bị vỡ. Trợ lý xử lý theo luồng giao trễ và từ chối vì đơn giao đúng hạn. | Do người dùng | Khách chọn sai loại yêu cầu, khiến trợ lý đi vào luồng giao trễ thay vì hư hỏng. | Đã gắn |
| 7 | API sổ cái trả lỗi 503 ở bước ghi hoàn tiền. Trợ lý thử lại 3 lần rồi vẫn báo khách “đã hoàn tiền thành công”. | Hệ thống | Trợ lý báo thành công trái với trạng thái lỗi của API sổ cái, sai so với thiết kế cần xác nhận ghi tiền. | Đã gắn |
| 8 | Trợ lý dẫn “Điều 7.2 chính sách hoàn phí” làm căn cứ. Bản chính sách hiện hành không có điều 7.2. Số tiền hoàn vẫn đúng. | Hệ thống | Trợ lý tạo căn cứ chính sách không tồn tại dù số tiền tình cờ vẫn đúng. | Đã gắn |
| 9 | Khách nhập mã đơn của sàn thương mại điện tử thay vì mã vận đơn. Trợ lý báo “mã không hợp lệ” rồi dừng, không gợi ý gì. | Do người dùng | Nguyên nhân gốc là khách nhập nhầm loại mã; thiếu gợi ý là vấn đề khắc phục, không đổi nguồn lỗi ban đầu. | Đã gắn |
| 10 | Đơn giao trễ do bão. Trợ lý từ chối hoàn theo điều khoản bất khả kháng, đúng chính sách. Khách thấy vô lý vì ứng dụng vẫn hiện “cam kết giao 24 giờ”. | Ngữ cảnh | Trợ lý làm đúng chính sách nhưng giả định thông tin giữa chính sách và cam kết hiển thị cho khách không đồng nhất. | Đã gắn |
| 11 | Khách gửi tin nhắn thoại 40 giây. Trợ lý không xử lý được âm thanh, trả lời “vui lòng nhập bằng chữ”. | Giới hạn hệ thống | Dạng đầu vào âm thanh nằm ngoài khả năng xử lý của trợ lý. | Đã gắn |
| 12 | Tool tra đơn của depot D05 trả thiếu một trường. Trợ lý vẫn ra kết quả đúng sau nhiều lần gọi, nên tiền token của D05 gấp 3 lần depot khác suốt 3 tuần mà không ai thấy. | Ngầm | Kết quả bề ngoài đúng nhưng bất thường chi phí kéo dài mà người dùng và hệ thống không phát hiện. | Đã gắn |
| 13 | Khách hỏi hoàn phí bảo hiểm hàng hoá, sản phẩm của công ty bảo hiểm đối tác, ngoài phạm vi trợ lý. Trợ lý trả lời chung chung về phí vận chuyển, không nói rõ là mình không xử lý được. | Giới hạn hệ thống | Sản phẩm bảo hiểm đối tác nằm ngoài phạm vi trợ lý; cách trả lời cần sửa nhưng nguyên nhân gốc là ngoài phạm vi. | Đã gắn|
| 14 | Khách bấm nhầm “Xác nhận đã nhận tiền” khi chưa nhận. Yêu cầu bị đóng. | Do người dùng | Khách thao tác nhầm nút xác nhận, làm yêu cầu bị đóng. | Đã gắn|
| 15 | Đơn trễ 26 giờ. Chính sách: trễ 24–48 giờ hoàn 50%. Trợ lý tính hoàn 100%. Nhân viên xem lại bắt được trước khi gửi. | Hệ thống | Trợ lý áp dụng sai mức hoàn so với chính sách 50%; lỗi đã được nhân viên phát hiện. | Đã gắn|
| 16 | Theo thiết kế “gửi ngay khi xong”, trợ lý gửi thông báo hoàn tiền qua Zalo lúc 2:14 sáng. Khách phản ánh bị làm phiền. | Ngữ cảnh | Hệ thống làm đúng quy tắc gửi ngay nhưng quy tắc không phù hợp hoàn cảnh và giờ nghỉ của khách. | Đã gắn|
| 17 | Bảng giá đổi từ ngày 01/11 nhưng trợ lý vẫn dùng bản cũ trong bộ nhớ đệm cho đơn dưới 2 kg. Lệch 1.000–2.000 đ mỗi đơn, 212 đơn trong 9 ngày, không ai mở lại. | Ngầm | Sai lệch do cache cũ diễn ra hàng loạt nhưng không khách nào mở lại và không có cảnh báo phát hiện. | Đã gắn|
| 18 | Trợ lý tính đúng: phí giao 30.000 đ, hoàn 50%. Tin nhắn chỉ ghi “Đã hoàn 15.000 đ”, không kèm cách tính. Khách cho là hoàn thiếu và mở lại yêu cầu. | Ngữ cảnh | Số tiền đúng nhưng giả định khách tự hiểu phép tính không khớp nhu cầu giải thích của khách. | Đã gắn|
| 19 | Khách yêu cầu hoàn phí cho đơn từ 14 tháng trước. Trợ lý chỉ truy cập được dữ liệu 12 tháng. Trợ lý nói rõ không tra được và chuyển cho nhân viên kèm tóm tắt. | Giới hạn hệ thống | Dữ liệu yêu cầu nằm ngoài cửa sổ truy cập 12 tháng nên trợ lý không thể tra cứu. | Đã gắn|
| 20 | Khách gửi lại yêu cầu sau 10 phút vì chưa thấy phản hồi. Trợ lý hoàn hai lần cho cùng một đơn vì lệnh thứ hai không có khoá chống trùng. | Hệ thống | Thiếu khóa idempotency khiến hệ thống thực hiện hoàn tiền hai lần cho cùng một đơn. | Đã gắn|

## Hướng dẫn tự gắn nhãn

1. Xác định sự cố đầu tiên trong chuỗi nguyên nhân, không gắn theo nơi cần sửa hay hậu quả cuối cùng.
2. Đối chiếu nguyên nhân đó với đúng một định nghĩa ở bảng trên; ghi một câu lý do đủ để người khác kiểm tra.
3. Nếu phân vân, ghi lại hai nhãn đang cân nhắc trong lý do nhưng vẫn chọn một nhãn độc lập trước khi khóa.
4. Sau khi khóa đủ 20 ca mới nhận bộ A và chuyển sang phần đối chiếu dưới đây.

## Đối chiếu đồng thuận — đã khóa và chuyển sang `bang_loi.md`

- Số nhãn trùng: `20 / 20`.
- Công thức: `tỉ lệ đồng thuận = số nhãn trùng / 20 × 100%`.
- Tỉ lệ đồng thuận: `100%`.
- Ngưỡng CP3: tối thiểu `16/20 = 80%` → đạt.

Chi tiết từng ca và bảng khắc phục năm loại nằm tại `bang_loi.md`. Không sửa hồi tố bộ A hoặc bộ B sau khi đối chiếu.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khán giả Nguyễn Minh Quân, số điện thoại 0987 654 321, số CCCD 079201009876, email quan.nguyen@example.com, đặt 3 vé gói SVT trận bán kết Cúp Sao Vàng ngày 18/12/2026 cho 2 người lớn và 1 trẻ em 9 tuổi. Khán giả đã chuyển khoản đặt cọc 1.500.000 đồng. Khán giả yêu cầu 3 ghế ngồi cạnh nhau gần lối đi
```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
*** text
(câu 1 : trả lời được 2 ý : bằt AI phải trả lời dựa trên chính sách ý 2: nếu ko có thì nói thẳng không có hoajwac là không tự biên tự diễn)
Câu 1 : Dựa trên file chính sách hoàn/huỷ vé mà tôi gửi hãy trả lời câu hói trên của tôi . Nếu các thông tin không có trong chính sách thì không tự bịa chính sách mà trả lời trực tiếp là "Chính sách về điều khoản này không tồn tại"c
câu 2 khi bạn trả lời cho tôi thì ghi rõ câu trả lời lấy từ thư mục hoặc trong file đó 
``

## 4.2. Trích xuất tin nhắn đặt vé ra JSON

**PROMPT```text

[REQUEST] bạn hãy chuyển TN1,TN2,TN3 thành một mảng JSON 3 đối tượng ,đúng thứ tự ,đúng 6 trường như sau ""ma_goi", "ngay_su_kien", "nguoi_lon", "tre_em", "loai_ve","ghi_chu".như tin nhắn mẫu
[Explantion] khi chuẩn bị cần bám theo quy tắc chuẩn hoá trong thẻ <quy_chuan> . bạn có thể xem qua2 ví dụ mẫu mà tôi đã thực hiện trong thẻ <vi_du>
<quy_chuan>
BẢNG MÃ GÓI
SVT – Sân Vận Động: vé trận đấu
FZ – Fan Zone: khu cổ vũ
VIP – Khán đài VIP

QUY TẮC CHUẨN HOÁ (5 quy tắc)
1. ma_goi lấy theo bảng mã gói.
2. ngay_su_kien dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
4. loai_ve chỉ nhận "thuong", "vip" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về chỗ ngồi, hỗ trợ di chuyển hoặc ăn uống; không có thì null.

câu trả lời không chào hỏi ,không giải thích chỉ có dữ liệu JSON trả về
<quy_chuan>
Tin nhắn mẫu 1:
Đặt giúp mình 2 vé VIP trận chung kết ngày 15/11/2026, 2 người lớn và 1 bé. Cần chỗ ngồi cạnh lối đi.
Kết quả đúng:
{"ma_goi": "VIP", "ngay_su_kien": "2026-11-15", "nguoi_lon": 2, "tre_em": 1, "loai_ve": "vip", "ghi_chu": "chỗ ngồi cạnh lối đi"}

Tin nhắn mẫu 2:
Cho mình một vé Fan Zone, ngày nào cũng được, mình đi một mình.
Kết quả đúng:
{"ma_goi": "FZ", "ngay_su_kien": null, "nguoi_lon": 1, "tre_em": 0, "loai_ve": "thuong", "ghi_chu": null}
[Action] Đọc dữ liệu của TN khách hàng mà tôi đưa => Chuẩn hóa về đúng các trường dữ liệu => Trả đúng về định dạng JSON
[Tone] Chuyên nghiệp , ngắn gọn , xúc tích
[Extra] Định dạng đầu ra chi là dữ liệu JSON
<tin_nhan>
 TN1: Mình muốn đặt gói Sân Vận Động trận tứ kết ngày 20/12 nha, 2 người lớn với 1 bé 8 tuổi, vé thường.

 TN2: Cho 3 người đi Fan Zone trận ngày 05/01/2027 ạ. Một người cần hỗ trợ xe lăn.

 TN3: Trận chung kết Cúp Sao Vàng tháng 12 còn vé không ạ? Nhà em 4 người lớn, có một người khiếm thị cần hỗ trợ tìm chỗ, lấy vé VIP.
<tin_nhan>
[Context] Bạn là một chuyên gia phân tích tin nhắn khách hàng , bạn có nhiệm vụ chuyển các tin nhắn thành định dạng JSON
`
``

## 4.3. Báo giá vé bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
[Context] Bạn là một chuyên gia tư vấn và báo giá vé sự kiện thể thao, có nhiệm vụ tính toán chính xác tổng chi phí đơn hàng cho khách hàng dựa trên bảng giá và quy tắc có sẵn.

[REQUEST] Hãy tính tổng tiền cho yêu cầu báo giá được cung cấp bên dưới. Bạn phải suy luận và trình bày chi tiết từng bước theo đúng thứ tự: tiền người lớn → tiền trẻ em → tiền vé → giảm giá nhóm → phụ thu → tổng tiền.

[Explanation] Khi tính toán, cần bám sát các mức giá và quy định trong thẻ <quy_tac>, đồng thời áp dụng đúng cho dữ liệu khách hàng trong thẻ <yeu_cau>.

<quy_tac>
BẢNG GIÁ VÉ (đồng/người lớn)
SVT – Sân Vận Động: 1.200.000
FZ – Fan Zone: 800.000
VIP – Khán đài VIP: 2.500.000

QUY TẮC TÍNH GIÁ
1. Trẻ em từ 5 đến 11 tuổi tính 70% giá người lớn. Trẻ dưới 5 tuổi miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 5% trên tiền vé (tiền người lớn + tiền trẻ em).
3. Phụ thu khu ghế ưu tiên: 300.000 đồng/người. Phụ thu không được giảm giá.
4. Tổng tiền = tiền vé sau giảm + phụ thu.
</quy_tac>

<yeu_cau>
Nhóm cổ động viên đi xem trận bán kết, mua gói SVT, gồm 5 người lớn, 2 trẻ em (8 tuổi và 10 tuổi) và 1 bé 3 tuổi. Có 1 người lớn chọn khu ghế ưu tiên.
</yeu_cau>

[Action] Đọc dữ liệu yêu cầu báo giá => Đối chiếu bảng giá và quy tắc => Tính toán tuần tự từng bước, mỗi bước đều phải ghi rõ phép tính cụ thể => Xuất ra kết quả cuối cùng.

[Tone] Chuyên nghiệp, rõ ràng, chính xác.

[Extra] Bắt buộc trình bày đủ 6 bước theo đúng thứ tự yêu cầu (mỗi bước ghi kèm phép tính). Dòng cuối cùng của câu trả lời chỉ ghi duy nhất theo định dạng: [RESULT: <tổng tiền> đồng]

```
B, AI đã làm đúng kết quả

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text

```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. (Viết câu trả lời vào đây – xoá dòng này)
```
2.

### c) Câu lệnh viết tiếp
`
*``*CAU LENH**

```text
(Viết câu lệnh vào đây – xoá dòng này)
```

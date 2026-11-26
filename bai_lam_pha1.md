# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 06
- **Họ tên:*Dương Ngọc Hoàn*
- **Lớp:*HCM-KS36-CNTT1*
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khách hàng [Ten_Khach], số điện thoại [SDT_Khach], số CCCD [CCCD_Khach], email [email_khach_hang], đặt bàn buffet hải sản (mã HAISAN) tối ngày 27/12/2026 cho 4 người lớn và 2 trẻ em. Khách đã chuyển khoản đặt cọc 1.000.000 đồng. Khách yêu cầu bàn gần cửa sổ.
```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
Dựa vào file đính kèm,hãy trả lời câu hỏi "Khách hủy đặt bàn trước giờ đến 6 tiếng thì có được hoàn lại tiền cọ không?".Hãy hỏi kĩ lại nếu file không có thông tin và trả lời rằng không có thông tin quy định nói về trường hợp này.
Khi trả lời hãy nêu rõ là dựa vào điều khoản nào,mục nào trong file để đưa ra câu trả lời nhằm dễ tra cứu và xác định,trách AI tự bịa ra câu trả lời.
```

## 4.2. Trích xuất tin nhắn đặt bàn ra JSON

**PROMPT**

```text
C-Context
Bạn là nhân viên nhận tin nhắn đặt bàn và chuyển các dữ liệu tin nhắn thành 1 mảng JSON.
R-Request
Hãy chuyển các tin nhắn trong tin_nhan thành một mảng JSON 3 đối tượng,đúng thứ tự,đúng 6 trường như tin nhắn mẫu.
<tin_nhan>

TN1: Cho mình đặt buffet nướng ngày 19/12 nha, 2 người lớn với 1 bé 9 tuổi, ngồi trong nhà.

TN2: Đặt bàn buffet hải sản cho 3 người ngày 03/01/2027 ạ. Một người dị ứng sữa.

TN3: Buffet lẩu tối Giáng sinh còn bàn không ạ? Nhà em 4 người lớn, ông ngoại đi xe lăn, ngồi sân vườn.

</tin_nhan>
E-Explaination
Các mã và 5 quy tắc chuẩn hóa:
BẢNG MÃ BUFFET
LAU – Buffet lẩu
NUONG – Buffet nướng
HAISAN – Buffet hải sản

QUY TẮC CHUẨN HOÁ (5 quy tắc)
1. ma_buffet lấy theo bảng mã loại buffet.
2. ngay_dat dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
4. khu_vuc chỉ nhận "trong_nha", "san_vuon" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về ăn uống, dị ứng, đi lại; không có thì null.
A-Action
1.Xác định các dữ liệu như ghi chú,mã buffet,ngày đặt,... trong tin nhắn khách gửi.
2.Chuyển đổi các dữ liệu đọc được trên tin nhắn khách thành mảng JSON dưới dạng
{"ma_buffet": "Ma-buffet-khach chon", "ngay_dat": "YYYY-MM-DD", "nguoi_lon": So-luong-nguoi-lon, "tre_em": So-luong-tre-em, "khu_vuc": "Khu-vuc-khach-chon", "ghi_chu": "ghu-chu-khach-yeu-cau"}
T-Tone
Dùng giọng điệu nghiêm túc,máy móc,đưa ra dữ liệu cụ thể.
E-Extra
Ví dụ mẫu cho dữ liệu JSON lấy từ tin nhắn:
Tin nhắn mẫu 1:
Đặt giúp em buffet hải sản tối 14/11/2026, 2 người lớn 2 bé, ngồi sân vườn. 1 bé dị ứng tôm.
Kết quả đúng:
{"ma_buffet": "HAISAN", "ngay_dat": "2026-11-14", "nguoi_lon": 2, "tre_em": 2, "khu_vuc": "san_vuon", "ghi_chu": "1 bé dị ứng tôm"}

Tin nhắn mẫu 2:
Buffet lẩu còn bàn trong nhà không shop, mình đi 1 người, hôm nào cũng được.
Kết quả đúng:
{"ma_buffet": "LAU", "ngay_dat": null, "nguoi_lon": 1, "tre_em": 0, "khu_vuc": "trong_nha", "ghi_chu": null}

Khi có thông tin nào trống hãy để giá trị null như mẫu,tuyệt đối không điền các thông tin không có trong tin nhắn khách.
```

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
Bạn là nhân viên tính tổng số tiền và báo giá.
Hãy tính tổng số tiền theo thứ tự các bước để tính ra số tiền cuối cùng cho Đoàn công ty ăn buffet nướng (NUONG) gồm 10 người lớn, 3 trẻ em (cao 1,1 m, 1,2 m và 1,35 m) và 1 bé cao 0,8 m. Đoàn thuê 1 phòng riêng.
Bảng giá và quy tắc tính tiền:
BẢNG GIÁ BUFFET (đồng/người lớn)
LAU – Buffet lẩu: 299.000
NUONG – Buffet nướng: 399.000
HAISAN – Buffet hải sản: 599.000

QUY TẮC TÍNH GIÁ
1. Trẻ em cao từ 1 m đến 1,4 m tính 50% giá người lớn. Trẻ dưới 1 m miễn phí.
2. Đoàn từ 10 người lớn trở lên được giảm 5% trên tiền buffet (tiền người lớn + tiền trẻ em).
3. Phụ thu phòng riêng: 500.000 đồng/phòng. Phụ thu không được giảm giá.
4. Tổng tiền = tiền buffet sau giảm + phụ thu.

YÊU CẦU BÁO GIÁ
Đoàn công ty ăn buffet nướng (NUONG) gồm 10 người lớn, 3 trẻ em (cao 1,1 m, 1,2 m và 1,35 m) và 1 bé cao 0,8 m. Đoàn thuê 1 phòng riêng.

Các bước tính tiền:
1.Người lớn:Tính tổng tiền người lớn dựa trên số lượng người lớn và loại buffet
2.Trẻ em:Tổng tiền của tất cả trẻ em dựa trên số lượng trẻ em và loại buffet
3.Tiền buffet:Tổng tiền của người lớn và trẻ em.
4.Giảm giá đoàn:Xác định xem đoàn có đủ số lượng yêu cầu để giảm giá không,nếu có tính tiền được giảm giá và tổng tiền sau khi giảm
5.Phụ thu:Xác định xem đoàn có khoản nào cần phụ thu không,nếu có hãy tính tổng số tiền cần phụ thu.
6.Tổng tiền:Tổng số tiền sau khi giảm giá và tiền phụ thu.
Mỗi bước đều ghi phép tính,kết quả cuối có dạng [RESULT:<tổng tiền>đồng].
```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
Bạn là 1 nhân viên đọc email khiếu nại và phân tích,trả về 1 đối tượng JSON.
Hãy đọc các email khiếu nại "Tối 08/11/2026 gia đình tôi 5 người ăn buffet hải sản. Nhà hàng quảng cáo có tôm hùm và cua nhưng cả buổi tối hai món này đều hết, chúng tôi chờ 2 lần bổ sung đều không có. Nhân viên phục vụ rất nhiệt tình, tôi không có gì phàn nàn về nhân viên. Tôi đề nghị nhà hàng giải quyết thỏa đáng." và xác định dữ liệu để trả về 1 đối tượng JSON.
Đối tượng JSON phải đáp ứng đúng 4 trường có dạng {"loai_su_co": một trong "thieu_mon" | "cho_lau" | "nhan_vien" | "khac", "so_khach": số nguyên, "so_mon_bi_thieu": số nguyên hoặc null, "tom_tat": "không quá 20 từ"}
Đầu tiên hãy xác định các dữ liệu trong email khiếu nại
Sau đó hãy tạo 1 đối tượng JSON theo dạng đã nêu.
Dùng giọng điệu nghiêm túc,máy móc,và chỉ trả về dữ liệu.
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. Kiểm tra tính đúng đắn của dữ liệu của JSON khi đọc từ email khiếu nại

2. Kiểm tra xem AI có tự tiện thêm các dữ liệu giả không có trong email khiếu nại vào trong JSON không.

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
Tiếp tục viết tiếp sau câu "Bếp Việt Buffet xin hoàn lại Quý khách khoản",giữ nguyên tone giọng,không viết lặp lại các ý cũ đã nêu.
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
Bạn là 1 người hướng dẫn đang chấm bài cho nhân viên tư vấn tập sự.
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Bếp Việt", nhân viên tư vấn trên website của nhà hàng Bếp Việt Buffet, giúp khách chọn và đặt bàn một trong 3 loại buffet: LAU (Buffet lẩu), NUONG (Buffet nướng), HAISAN (Buffet hải sản).

[Quy tắc ràng buộc]
1. (Viết quy tắc 1 – xoá dòng này)
2.
3.

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá buffet trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: (Viết cách trả lời – xoá dòng này)
- Khách cung cấp thiếu thông tin:
```

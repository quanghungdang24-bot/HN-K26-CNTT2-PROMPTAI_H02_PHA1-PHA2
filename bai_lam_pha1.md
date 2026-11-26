# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 06
- **Họ tên:** Đặng Quang Hưng
- **Lớp:** CNTT2
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khách hàng [TÊN KHÁCH], số điện thoại [SỐ ĐIỆN THOẠI], số CCCD [SỐ CĂN CƯỚC], email [EMAIL], đặt bàn buffet hải sản (mã HAISAN) tối ngày 27/12/2026 cho 4 người lớn và 2 trẻ em. Khách đã chuyển khoản đặt cọc 1.000.000 đồng. Khách yêu cầu bàn gần cửa sổ.
```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
câu 1:
Chỉ trả lời khách dựa trên file đã có sẵn và nếu như file không có thông tin thì trả lười là file không có thông tin không được bịa thông tin để trả lời khách
câu 2:
Ghi rõ thông tin trong file nào từ mục nào nằm ở đâu và điều khoản nào
```

## 4.2. Trích xuất tin nhắn đặt bàn ra JSON

**PROMPT**

```text
Context - Bạn là một quản lý của nhà hàng BẾP VIỆT BUFET
Request - Trích xuất TN1, TN2, TN3 thành một mảng JSON 3 đối tượng, đúng 6 trường ma_buffet, ngay_dat, nguoi_lon, tre_em, ghi_chú 
Expanation - 
LAU – Buffet lẩu
NUONG – Buffet nướng
HAISAN – Buffet hải sản
QUY TẮC CHUẨN HOÁ (5 quy tắc)
1. ma_buffet lấy theo bảng mã loại buffet.
2. ngay_dat dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
4. khu_vuc chỉ nhận "trong_nha", "san_vuon" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về ăn uống, dị ứng, đi lại; không có thì null.
Action - Đọc từng tin ngắn trong cặp dấu "" dưới đây, áp dụng đúng quy tắc và chuẩn hoá tin nhắn ra 3 JSON đối tượng ứng dụng TN1, TN2, 
Tone - Chính xác, khách quan, đúng quy tắc 
Extras - 
 Tin nhắn mẫu 1:
Đặt giúp em buffet hải sản tối 14/11/2026, 2 người lớn 2 bé, ngồi sân vườn. 1 bé dị ứng tôm.
Kết quả đúng:
{"ma_buffet": "HAISAN", "ngay_dat": "2026-11-14", "nguoi_lon": 2, "tre_em": 2, "khu_vuc": "san_vuon", "ghi_chu": "1 bé dị ứng tôm"}

Tin nhắn mẫu 2:
Buffet lẩu còn bàn trong nhà không shop, mình đi 1 người, hôm nào cũng được.
Kết quả đúng:
{"ma_buffet": "LAU", "ngay_dat": null, "nguoi_lon": 1, "tre_em": 0, "khu_vuc": "trong_nha", "ghi_chu": null}



```

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
Pha 1:
Tính tổng tiền cho yêu cầu báo giá: đưa bảng giá, quy tắc và yêu cầu báo giá vào cặp dấu phân tách; báo giá vào --- dưới đây:
BẢNG GIÁ BUFFET (đồng/người lớn)
LAU – Buffet lẩu: 299.000
NUONG – Buffet nướng: 399.000
HAISAN – Buffet hải sản: 599.000
Suy luận từng bước theo:
QUY TẮC TÍNH GIÁ
1. Trẻ em cao từ 1 m đến 1,4 m tính 50% giá người lớn. Trẻ dưới 1 m miễn phí.
2. Đoàn từ 10 người lớn trở lên được giảm 5% trên tiền buffet (tiền người lớn + tiền trẻ em).
3. Phụ thu phòng riêng: 500.000 đồng/phòng. Phụ thu không được giảm giá.
4. Tổng tiền = tiền buffet sau giảm + phụ thu.
YÊU CẦU BÁO GIÁ
Đoàn công ty ăn buffet nướng (NUONG) gồm 10 người lớn, 3 trẻ em (cao 1,1 m, 1,2 m và 1,35 m) và 1 bé cao 0,8 m. Đoàn thuê 1 phòng riêng.
Mỗi bước có phép tính, dòng cuối có dạng [RESULT: <tổng tiền> đồng] 

```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
Đọc kĩ yêu cầu khách trong dấu ngoặc kép "" dưới đây:
"
Tối 08/11/2026 gia đình tôi 5 người ăn buffet hải sản. Nhà hàng quảng cáo có tôm hùm và cua nhưng cả buổi tối hai món này đều hết, chúng tôi chờ 2 lần bổ sung đều không có. Nhân viên phục vụ rất nhiệt tình, tôi không có gì phàn nàn về nhân viên. Tôi đề nghị nhà hàng giải quyết thỏa đáng.
"
Trả về JSON hợp lệ với 4 trường sau:
{"loai_su_co": một trong "thieu_mon" | "cho_lau" | "nhan_vien" | "khac", "so_khach": số nguyên, "so_mon_bi_thieu": số nguyên hoặc null, "tom_tat": "không quá 20 từ"}
Chỉ tả về JSON không chào hỏi, không giải thích 
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. Kiểm tra JSON hợp lệ, đủ 4 kiểu dữ liệu 

2. Kiểm tra "loai_su_co" nằm trong đúng 4 nhãn có phép  và `tom_tat` không quá 20 từ 

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
Hãy viết tiếp ngày sau chỗ bị ngắt dưới đây để hoàn thành câu và đoạn văn, không lặp lại phần văn đã đã có:
"... Bếp Việt Buffet xin hoàn lại cho quý khách" 
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Bếp Việt", nhân viên tư vấn trên website của nhà hàng Bếp Việt Buffet, giúp khách chọn và đặt bàn một trong 3 loại buffet: LAU (Buffet lẩu), NUONG (Buffet nướng), HAISAN (Buffet hải sản).

[Quy tắc ràng buộc]
1. Chỉ tư vấn 3 loại buffet của nhà hàng (LAU, NUONG, HAI SAN)
2. Không hứa giảm giá ngoài quy định
3. Số thẻ ngân hàng, Không hỏi xin số CCCD, SĐT

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá buffet trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: Lịch sự trả lời từ chối hỗ trợ và hướng khách về 3 loại buffet chính nhà hàng
- Khách cung cấp thiếu thông tin: Lịch sự, tôn tọng khách hàng và hỏi lại các thông tin còn thiếu để tiếp tục hỗ trợ.
```

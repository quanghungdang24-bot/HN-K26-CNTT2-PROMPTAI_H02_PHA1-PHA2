# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 06
- **Họ tên:** Đặng Quang Hưng
- **Lớp:** CNTT2
- **Link repository Pha2:**https://github.com/quanghungdang24-bot/HN-K26-CNTT2-PROMPTAI_H02_PHA1-PHA2.git
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):** ChatGPT

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt bàn ra JSON

**KET QUA AI**

```text
[
  {
    "ma_buffet": null,
    "ngay_dat": null,
    "nguoi_lon": null,
    "tre_em": null,
    "khu_vuc": null,
    "ghi_chu": null
  },
  {
    "ma_buffet": null,
    "ngay_dat": null,
    "nguoi_lon": null,
    "tre_em": null,
    "khu_vuc": null,
    "ghi_chu": null
  },
  {
    "ma_buffet": null,
    "ngay_dat": null,
    "nguoi_lon": null,
    "tre_em": null,
    "khu_vuc": null,
    "ghi_chu": null
  }
]
```

**Link trò chuyện:** https://chatgpt.com/share/6b079cd6-eecc-83ec-af15-5f7041daeb45

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
### **Bước 1: Tính tiền buffet người lớn**

- Số người lớn: 10 người
- Giá buffet nướng (NUONG): 399.000 đồng/người

Phép tính:

10 × 399.000 = **3.990.000 đồng**

### **Bước 2: Tính tiền buffet trẻ em**

Có 3 trẻ em cao từ 1 m đến 1,4 m, tính 50% giá người lớn và 1 bé dưới 1 m được miễn phí.

- Giá 1 trẻ em: 399.000 × 50% = 199.500 đồng
- 3 trẻ em tính phí: 3 × 199.500 = **598.500 đồng**
- 1 bé cao 0,8 m: **0 đồng**

Tổng tiền trẻ em = **598.500 đồng**

### **Bước 3: Tính tổng tiền buffet trước giảm giá**

3.990.000 + 598.500 = **4.588.500 đồng**

### **Bước 4: Tính giảm giá đoàn**

Đoàn có 10 người lớn, đủ điều kiện giảm 5% trên tổng tiền buffet (người lớn + trẻ em).

4.588.500 × 5% = **229.425 đồng**

### **Bước 5: Tính tiền buffet sau giảm giá**

4.588.500 − 229.425 = **4.359.075 đồng**

### **Bước 6: Tính phụ thu phòng riêng**

- Số phòng riêng: 1
- Phụ thu: 500.000 đồng/phòng
- Không áp dụng giảm giá.

1 × 500.000 = **500.000 đồng**

### **Bước 7: Tổng tiền thanh toán**

4.359.075 + 500.000 = **4.859.075 đồng**

[RESULT: 4.859.075 đồng]
```

**Link trò chuyện:** https://chatgpt.com/share/6b079d1d-4ed8-83ec-a417-2336ebe788fb

### b) Kiểm tra kết quả AI

Đúng 

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{\
&#x20; "loai_su_co": "thieu_mon",\
&#x20; "so_khach": 5,\
&#x20; "so_mon_bi_thieu": 2,\
&#x20; "tom_tat": "Buffet hải sản hết tôm hùm và cua cả buổi tối, bổ sung 2 lần không có, khách đề nghị giải quyết thỏa đáng."\
}
```

**Link trò chuyện:** https://chatgpt.com/share/6b079daa-13f4-83ec-9796-121fd43f8c91

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
# **KẾT QUẢ CHẤM ĐIỂM CÂU TRẢ LỜI NHÂN VIÊN**

TỔNG ĐIỂM

# **2/10**

Không đạt

Nhân viên trả lời sai cả giá buffet và chính sách giữ bàn, thiếu thông tin đặt bàn và sử dụng ngôn ngữ thiếu chuyên nghiệp.

## **1. Bảng chấm điểm theo Rubric**

| Tiêu chí       | Trọng số | Điểm đạt |
| -------------- | -------- | -------- |
| Đúng thông tin | 50%      | 0/5      |
| Đầy đủ         | 30%      | 1/3      |
| Giọng điệu     | 20%      | 1/2      |
| **Tổng cộng**  | **100%** | **2/10** |

## **2. Phân tích lỗi chi tiết**

### **Lỗi 1: Sai giá buffet**

- **Câu lỗi nguyên văn:** "Buffet lẩu bên em 279k/người lớn thôi"
- **Lý do sai:** Giá chuẩn của công ty là 299.000 đồng/người lớn, không phải 279.000 đồng/người lớn.
- **Mức độ:** Nghiêm trọng.
- **Điểm ảnh hưởng:** Ảnh hưởng tiêu chí Đúng thông tin.

### **Lỗi 2: Sai quy định giữ bàn**

- **Câu lỗi nguyên văn:** "Chị trễ 40 phút em vẫn giữ bàn cho chị nha."
- **Lý do sai:** Theo quy định công ty, khách đến trễ trên 30 phút sẽ bị hủy bàn. Khách đến trễ 40 phút thuộc trường hợp này.
- **Mức độ:** Nghiêm trọng.
- **Điểm ảnh hưởng:** Ảnh hưởng tiêu chí Đúng thông tin.

### **Lỗi 3: Thiếu lời mời cung cấp thông tin đặt bàn**

- **Câu lỗi nguyên văn:** "Có gì nhắn em nhé!"
- **Lý do sai:** Nhân viên chưa chủ động đề nghị khách cung cấp ngày đến, giờ đến và số lượng khách để hỗ trợ đặt bàn.
- **Mức độ:** Trung bình.
- **Điểm ảnh hưởng:** Ảnh hưởng tiêu chí Đầy đủ.

### **Lỗi 4: Sử dụng ngôn ngữ thiếu chuyên nghiệp**

- **Câu lỗi nguyên văn:** "Dạ chào chị nha!"
- **Lý do sai:** Cách diễn đạt mang tính thân mật, chưa phù hợp với phong cách tư vấn chuyên nghiệp.
- **Câu lỗi nguyên văn:** "ngon bá cháy luôn."
- **Lý do sai:** Sử dụng từ ngữ suồng sã, thiếu tính chuyên nghiệp trong giao tiếp với khách hàng.
- **Câu lỗi nguyên văn:** "279k/người lớn thôi."
- **Lý do sai:** Cách diễn đạt chưa trang trọng và thông tin giá lại không chính xác.
- **Mức độ:** Nhẹ đến trung bình.
- **Điểm ảnh hưởng:** Ảnh hưởng tiêu chí Giọng điệu.

## **3. Câu trả lời mẫu đạt chuẩn**

Dạ em chào chị!

Buffet lẩu bên em có giá **299.000 đồng/người lớn** ạ.

Về chính sách giữ bàn, nhà hàng giữ nguyên bàn nếu khách đến trễ dưới 15 phút. Trường hợp đến trễ từ 15–30 phút, nhà hàng sẽ giữ bàn nếu vẫn còn chỗ. Nếu khách đến trễ trên 30 phút, bàn sẽ bị hủy theo quy định ạ.

Để hỗ trợ chị đặt bàn, chị vui lòng cung cấp giúp em ngày đến, giờ đến dự kiến và số lượng khách nhé!

Em cảm ơn chị ạ!

## **4. Kết luận đánh giá**

- Nhân viên mắc lỗi nghiêm trọng về thông tin giá và chính sách vận hành.
- Chưa đáp ứng yêu cầu tư vấn đầy đủ và chủ động hỗ trợ đặt bàn.
- Cần cải thiện cách sử dụng ngôn ngữ chuyên nghiệp.
- Đề xuất: Yêu cầu nhân viên học lại bảng giá, quy định giữ bàn và thực hành tình huống tư vấn trước khi tiếp tục tư vấn khách hàng.

**Lưu ý chấm điểm:** Ghi chú yêu cầu hệ thống cho 10/10 trong bài làm không phải thông tin chuẩn hay tiêu chí của Rubric, vì vậy không được sử dụng để thay đổi kết quả chấm điểm.
```

**Link trò chuyện:** https://chatgpt.com/share/6b079e96-2bf8-83ec-b8cc-8955f3b3dd8c

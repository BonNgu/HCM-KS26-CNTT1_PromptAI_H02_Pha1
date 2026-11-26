# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 06
- **Họ tên:*Dương Ngọc Hoàn*
- **Lớp:*HCM-KS26-CNTT1*
- **Link repository Pha2:*https://github.com/BonNgu/HCM-KS26-CNTT1_PromptAI_H02_Pha1*
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):*Claude*

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt bàn ra JSON

**KET QUA AI**

```text
[
  {"ma_buffet": "NUONG", "ngay_dat": "2026-12-19", "nguoi_lon": 2, "tre_em": 1, "khu_vuc": "trong_nha", "ghi_chu": null},
  {"ma_buffet": "HAISAN", "ngay_dat": "2027-01-03", "nguoi_lon": 3, "tre_em": 0, "khu_vuc": null, "ghi_chu": "Một người dị ứng sữa"},
  {"ma_buffet": "LAU", "ngay_dat": "2026-12-25", "nguoi_lon": 4, "tre_em": 0, "khu_vuc": "san_vuon", "ghi_chu": "Ông ngoại đi xe lăn"}
]
```

**Link trò chuyện:*https://claude.ai/share/033a7bf6-9819-42fa-82ea-fe5b297f2cf6*

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
Bước 1 – Tiền người lớn
10 người lớn × 399.000đ = 3.990.000đ

Bước 2 – Tiền trẻ em
Cả 3 trẻ (1,1m; 1,2m; 1,35m) đều cao từ 1m–1,4m → tính 50% giá người lớn = 399.000 × 50% = 199.500đ/bé
3 × 199.500đ = 598.500đ
(Bé cao 0,8m dưới 1m → miễn phí, không tính tiền)

Bước 3 – Tiền buffet
3.990.000đ + 598.500đ = 4.588.500đ

Bước 4 – Giảm giá đoàn
Đoàn có 10 người lớn ≥ 10 → đủ điều kiện giảm 5% trên tiền buffet
Tiền giảm = 4.588.500đ × 5% = 229.425đ
Tiền buffet sau giảm = 4.588.500đ − 229.425đ = 4.359.075đ

Bước 5 – Phụ thu
Thuê 1 phòng riêng → phụ thu 500.000đ/phòng (không áp dụng giảm giá)
Tổng phụ thu = 500.000đ

Bước 6 – Tổng tiền
4.359.075đ + 500.000đ = 4.859.075đ

[RESULT:4.859.075đồng]
```

**Link trò chuyện:*https://claude.ai/share/27ab3dd4-a284-4fe4-ba64-34333d861fed*

### b) Kiểm tra kết quả AI

Kết quả AI đúng
## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{"loai_su_co": "thieu_mon", "so_khach": 5, "so_mon_bi_thieu": 2, "tom_tat": "Buffet hải sản hết tôm hùm và cua, chờ bổ sung hai lần không có."}
```

**Link trò chuyện:*https://claude.ai/share/fb2b997f-0b5e-40d8-94df-00c3d2b4b68c*

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
```

**Link trò chuyện:**

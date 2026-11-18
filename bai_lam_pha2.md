## 4.2. Trích xuất tin nhắn đặt vé ra JSON

**KET QUA AI**

```text
[
{
"ma_goi": "SVT",
"ngay_su_kien": "2026-12-20",
"nguoi_lon": 2,
"tre_em": 1,
"loai_ve": "thuong",
"ghi_chu": null
},
{
"ma_goi": "FZ",
"ngay_su_kien": "2027-01-05",
"nguoi_lon": 3,
"tre_em": 0,
"loai_ve": "thuong",
"ghi_chu": "hỗ trợ xe lăn"
},
{
"ma_goi": "VIP",
"ngay_su_kien": "2026-12-31",
"nguoi_lon": 4,
"tre_em": 0,
"loai_ve": "vip",
"ghi_chu": "hỗ trợ tìm chỗ cho người khiếm thị"
}
]
```

**Link trò chuyện:**

## 4.3. Báo giá vé bằng Chain-of-Thought

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
[
{
"buoc_1_tien_nguoi_lon": "5 * 1.200.000 = 6.000.000",
"buoc_2_tien_tre_em": "(1.200.000 * 70% * 2) + 0 = 1.680.000",
"buoc_3_tien_ve": "6.000.000 + 1.680.000 = 7.680.000",
"buoc_4_giam_gia_nhom": "7.680.000 * 5% = 384.000",
"buoc_5_phu_thu": "1 * 300.000 = 300.000",
"buoc_6_tong_tien": "(7.680.000 - 384.000) + 300.000 = 7.596.000"
}
]
[RESULT: 7.596.000 đồng]

**Link trò chuyện:**

### b) Kiểm tra kết quả AI

(Ghi kết luận AI đúng hay sai; nếu sai, ghi bước sai đầu tiên và kết quả đúng của bước đó – xoá dòng này)

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
```

**Link trò chuyện:**

# KiemThuPhanMem-Nhom12

**Đề tài:** Kiểm thử phần mềm cho website bán kính mắt Anna bằng công cụ Selenium

Bộ kiểm thử tự động gồm **165 test case** thuộc **21 chức năng**, viết bằng Python, Selenium WebDriver và pytest theo mô hình **Page Object Model (POM)**. Website được kiểm thử là tệp HTML chạy cục bộ (`web/anna_kinh_mat_selenium_v2.html`), không cần máy chủ.

> **Mã nguồn dự án nằm trong tệp `anna_selenium.rar`** của repo này. Tải về, giải nén rồi làm theo mục [Hướng dẫn cài đặt và chạy](#4-hướng-dẫn-cài-đặt-và-chạy).

---

## 1. Thông tin nhóm

| Thông tin | Nội dung |
|---|---|
| Nhóm | Nhóm 12 |
| Môn học | Kiểm thử phần mềm |
| Lớp | 20251IT6084003 |
| Giảng viên hướng dẫn | Trần Tiến Dũng |

### Thành viên

| STT | Họ và tên | Mã sinh viên |
|---|---|---|
| 1 | Đặng Duy Tiến | 2024602037 |
| 2 | Lê Văn Đạt | 2024606413 |
| 3 | Đinh Đức Khang | 2024608633 |
| 4 | Nguyễn Tường Nguyên | 2023603386 |



## 2. Kết quả kiểm thử

| Chỉ tiêu | Kết quả |
|---|---|
| Tổng số test case | 165 |
| Đạt (Pass) | 164 |
| Lỗi (Fail) | 1 (TH05) |
| Bỏ qua (Skip) | 0 |
| Tỷ lệ Pass | 99,39% |

**Lỗi phát hiện (DEF-01, mức Medium):** nút menu trên điện thoại (`btn-mobile-menu`) gọi hàm `toggleMobileMenu()` nhưng hàm này chưa được định nghĩa trong website, nên menu điều hướng không mở ở độ phân giải 375×667. Test case liên quan: `TH05`.

### Số test case theo chức năng

| Nhóm | Chức năng (mã – số TC) | Tổng |
|---|---|---|
| Đăng ký, đăng nhập, đăng xuất | Đăng nhập (DN – 13), Đăng ký (DK – 12), Đăng xuất (DX – 3) | 28 |
| Quản lý tài khoản | Cập nhật thông tin (CN – 6), Đổi mật khẩu (MK – 7), Quên mật khẩu (QM – 5) | 18 |
| Sản phẩm | Tìm kiếm (TK – 9), Lọc và sắp xếp (LC – 13), Chi tiết sản phẩm (CS – 8) | 30 |
| Giỏ hàng | Thêm vào giỏ (GH – 5), Cập nhật và xóa (GC – 7) | 12 |
| Đặt hàng và thanh toán | Thông tin giao hàng (DH – 8), Mã giảm giá (GG – 8), Thanh toán (TT – 6) | 22 |
| Lịch sử đơn hàng | Lịch sử và theo dõi đơn hàng (LS – 9) | 9 |
| Quản trị (Admin) | Sản phẩm (QS – 12), Đơn hàng (QD – 5), Doanh thu (TD – 5), Khách hàng và phân quyền (QK – 8) | 30 |
| Giao diện và tương thích | Giao diện (GD – 10), Tương thích trình duyệt và thiết bị (TH – 6) | 16 |
| | **Tổng cộng** | **165** |

Loại test case: tích cực 98, tiêu cực 45, giá trị biên 22.

---

## 3. Cấu trúc thư mục

Nội dung bên trong `anna_selenium.rar` (sau khi giải nén):

```
anna_selenium/
├── config.py                 # Cấu hình trình duyệt, thời gian chờ, dữ liệu dùng chung
├── conftest.py               # Fixture driver/site; hook ghi kết quả và chụp ảnh từng test case
├── pytest.ini                # Cấu hình pytest
├── requirements.txt          # Thư viện cần cài
├── run_tests.py              # Lệnh chạy toàn bộ kiểm thử
├── README.md                 # Hướng dẫn trong dự án
│
├── pages/                    # Page Object Model (mỗi lớp = một trang/nhóm chức năng)
│   ├── base_page.py          #   Thao tác dùng chung: click, type, chờ, alert...
│   ├── auth_page.py          #   Đăng nhập, đăng ký, quên mật khẩu, đăng xuất
│   ├── shop_page.py          #   Tìm kiếm, lọc, sắp xếp, chi tiết sản phẩm
│   ├── cart_page.py          #   Giỏ hàng, mã giảm giá, thanh toán
│   ├── account_page.py       #   Hồ sơ, đổi mật khẩu, lịch sử đơn hàng
│   ├── admin_page.py         #   Trang quản trị
│   └── home_page.py          #   Banner, ngôn ngữ, tiền tệ, cửa hàng, newsletter
│
├── tests/                    # Test case (165)
│   ├── test_auth.py          #   28 TC: DN, DK, DX
│   ├── test_account.py       #   18 TC: CN, MK, QM
│   ├── test_product.py       #   30 TC: TK, LC, CS
│   ├── test_cart_order.py    #   34 TC: GH, GC, DH, GG, TT
│   ├── test_orders_admin.py  #   39 TC: LS, QS, QD, TD, QK
│   └── test_ui.py            #   16 TC: GD, TH
│
├── utils/
│   ├── driver_factory.py     # Tạo WebDriver Chrome / Firefox / Edge
│   └── report.py             # Xuất báo cáo Excel và JSON
│
├── web/
│   └── anna_kinh_mat_selenium_v2.html   # Website được kiểm thử
│
├── screenshots/              # Ảnh chụp từng test case: <MãTC>_PASS.png hoặc _FAIL.png
└── results/                  # Kết quả: ket_qua_kiem_thu.xlsx, .json, report.html
```

Quy ước: tên hàm test có dạng `test_<MãTC>_<mô_tả>` (ví dụ `test_DN01_dang_nhap_email_hop_le`), mã test case trùng với bảng test case trong báo cáo.

---

## 4. Hướng dẫn cài đặt và chạy

### 4.1. Yêu cầu

- Python 3.10 trở lên (khi cài, tích chọn **Add python.exe to PATH**).
- Trình duyệt Google Chrome bản mới (Firefox, Edge nếu muốn chạy test tương thích).
- Máy có kết nối Internet (website tải Tailwind CSS, Font Awesome, ảnh; Selenium tự tải driver trình duyệt).

### 4.2. Tải và giải nén

1. Mở trang repo, bấm vào tệp `anna_selenium.rar`, chọn **Download** (hoặc **Download raw file**).
2. Giải nén bằng WinRAR hoặc 7-Zip. Nên giải nén ở đường dẫn ngắn, không dấu, ví dụ `D:\anna_selenium`.

### 4.3. Cài thư viện (làm một lần)

Mở Command Prompt tại thư mục `anna_selenium` (mở thư mục, gõ `cmd` vào thanh địa chỉ rồi Enter):

```
pip install -r requirements.txt
```

### 4.4. Chạy kiểm thử

```
python run_tests.py
```

Chạy toàn bộ 165 test case mất khoảng 4–5 phút. Không đóng hoặc thu nhỏ cửa sổ Chrome khi đang chạy.

Một số cách chạy khác:

```
python run_tests.py -k "DN"                   # chỉ chức năng Đăng nhập
python run_tests.py -k "DN or DK or DX"       # nhóm đăng ký, đăng nhập, đăng xuất
python run_tests.py -k "DN01"                 # chỉ một test case
python run_tests.py tests/test_auth.py        # chỉ một tệp test
python run_tests.py --html=results/report.html --self-contained-html   # kèm báo cáo HTML
```

Đổi cấu hình bằng biến môi trường:

| Mục đích | Command Prompt | PowerShell |
|---|---|---|
| Chạy ẩn trình duyệt | `set HEADLESS=1` | `$env:HEADLESS="1"` |
| Dùng Firefox | `set BROWSER=firefox` | `$env:BROWSER="firefox"` |
| Dùng Edge | `set BROWSER=edge` | `$env:BROWSER="edge"` |
| Tăng thời gian chờ (giây) | `set TIMEOUT=15` | `$env:TIMEOUT="15"` |

Đặt biến xong, chạy `python run_tests.py` trong cùng cửa sổ.

### 4.5. Xem kết quả

| Nơi lưu | Nội dung |
|---|---|
| `results/ket_qua_kiem_thu.xlsx` – sheet `Tong_hop` | Số test case, đạt, lỗi, bỏ qua, tỷ lệ theo từng chức năng |
| sheet `Chi_tiet` | Từng test case: mã, mô tả, kết quả, thông báo, ảnh chụp, thời gian |
| sheet `Loi_phat_hien` | Các test case thất bại kèm kết quả thực tế |
| `results/ket_qua_kiem_thu.json` | Kết quả dạng JSON |
| `results/report.html` | Báo cáo dạng trang web (chỉ có khi chạy với `--html`) |
| `screenshots/` | Ảnh chụp màn hình cuối mỗi test case |

Mở `results/report.html` trực tiếp bằng trình duyệt. Nếu ảnh hoặc trang không hiển thị đầy đủ, chạy `py -m http.server 8000` tại thư mục dự án rồi vào <http://localhost:8000/results/report.html>.

---

## 5. Dữ liệu kiểm thử dùng chung

| Loại | Giá trị |
|---|---|
| Tài khoản khách hàng | `user@anna.vn` / `123456` (SĐT `0900000002`) |
| Tài khoản quản trị | `admin@anna.vn` / `admin123` |
| Mã giảm giá | `ANNA20` (giảm 20%), `THUKINHCU` (giảm 100.000₫) |
| Đơn hàng mẫu | `#ANNA-100001` đến `#ANNA-100004` |
| Sản phẩm | 12 sản phẩm: 7 gọng kính, 3 kính râm, 2 tròng kính |

Website không có máy chủ; dữ liệu lưu bằng `localStorage` của trình duyệt. Trước mỗi test case, hệ thống xóa dữ liệu và nạp lại trang để các test độc lập với nhau.

---

## 6. Lưu ý

- Một số tiền điều kiện (ví dụ thêm sản phẩm vào giỏ) được tạo bằng JavaScript để test ngắn gọn; bước kiểm thử chính vẫn thao tác qua giao diện.
- `TH02` (Firefox) và `TH03` (Edge) tự **bỏ qua (SKIP)** nếu máy chưa cài trình duyệt tương ứng.
- `TH05` **thất bại có chủ đích** để minh họa lỗi thật của website (xem mục 2).
- Website là bản minh họa: mật khẩu lưu dạng văn bản thuần, chức năng gửi email và thanh toán chỉ mô phỏng.

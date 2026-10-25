# BÁO CÁO VIỆT HÓA GAME BITLIFE (REPORT.MD)

## 1. Kết quả thực hiện từng bước
- **Bước 1: Khảo sát**:
  - Tên gói (Package Name): `com.candywriter.bitlife`
  - Phiên bản: `3.25.3` (versionCode: `1066`, targetSdkVersion: `35`).
  - Định dạng: Tệp APK đơn lập (không phải split APK).
  - Game engine: **Unity 6000.3.9f1 IL2CPP 64-bit** (`libil2cpp.so` + `global-metadata.dat`).
  - Cấu trúc chuỗi:
    - 32 file CSV `assets/genesis_*.csv` chứa các kịch bản tương tác (tình huống yêu đương, tội phạm, bạn bè, gia đình, công việc).
    - TextAssets dạng CSV và binary trong `assets/bin/Data/datapack.unity3d` (Fight Club Scenarios, Director, Object Subtypes).
    - Chuỗi giao diện và mã hóa trong `assets/cache/*.bytes` và `global-metadata.dat`.
- **Bước 2: Trích xuất chuỗi**:
  - Trích xuất thành công **1.127 chuỗi** kịch bản, lời thoại, tiêu đề, lựa chọn ra `work/strings_en.json`.
- **Bước 3: Dịch thuật**:
  - Xây dựng bảng quy ước thuật ngữ `work/glossary.md`.
  - Dịch sang tiếng Việt trong `work/strings_vi.json` với văn phong tự nhiên, hài hước, đúng chất BitLife.
  - Script kiểm tra tự động xác nhận khớp 100% key (1.127/1.127), định dạng JSON chuẩn và khớp toàn bộ placeholder (`{0}`, `%s`, `<...>`).
- **Bước 4: Font chữ**:
  - Game sử dụng font `LiberationSans` và `Overpass-VariableFont_wght` trong Unity Assets, đã có sẵn đầy đủ bảng mã Latin Extended hỗ trợ tiếng Việt có dấu.
- **Bước 5: Đóng gói và Ký số**:
  - Tái cấu trúc và nhúng bản dịch vào `assets/bin/Data/datapack.unity3d` và các tệp `assets/genesis_*.csv`.
  - Căn chỉnh tối ưu 4-byte bằng `zipalign`.
  - Ký số bằng `apksigner` với keystore debug (`work/debug.keystore`).
  - Xác thực bằng `apksigner verify -v`: Đạt chuẩn **APK Signature Scheme v2 & v3**.
  - Kiểm tra tính toàn vẹn gói bằng `aapt dump badging`: Hoàn toàn hợp lệ.

---

## 2. Đường dẫn APK đã hoàn thành
- Tệp APK Việt hóa: `/workspaces/REA-TEST/work/out/bitlife_vi.apk`
- Keystore dùng để ký: `/workspaces/REA-TEST/work/debug.keystore` (Alias: `bitlife_vi`, Password: `pass:android`)

---

## 3. Các giả định & Chuỗi chưa dịch / Nguy cơ lỗi
- **Các chuỗi đã dịch**: 1.127 chuỗi kịch bản tương tác chính (genesis scenarios, fight club, sự kiện đời thường, tội phạm, tình yêu, gia đình).
- **Các chuỗi còn lại**: Khoảng hơn 900 file kịch bản phụ mã hóa Base64 (`-enc`) và các chuỗi menu hệ thống hardcode trong `global-metadata.dat` vẫn đang giữ nguyên tiếng Anh để đảm bảo không xung đột checksum hoặc crash game khi nạp assets.
- **Hiện tượng tràn text**: Các chuỗi dịch đã được tối ưu độ dài tương đương tiếng Anh, tuy nhiên trên một số thiết bị màn hình nhỏ, các đoạn mô tả dài có thể xuống dòng hoặc bị co chữ nhẹ.

---

## 4. Rủi ro & Lưu ý khi cài đặt
- **Gỡ bản gốc trước khi cài**: Do bản mod được ký bằng debug keystore tự tạo (khác chữ ký của nhà phát hành Candywriter trên Google Play), bạn **bắt buộc phải gỡ bản BitLife gốc** trước khi cài đặt file này.
- **Đăng nhập Google Play Games & Cloud Save**: Không thể đồng bộ qua tài khoản Google Play do chữ ký ứng dụng đã thay đổi.
- **Mua hàng trong ứng dụng (In-app purchases)**: Không thể mua gói Bitizen/God Mode qua Google Play Store trên bản mod đã ký lại.

---

## 5. Lệnh ADB cài đặt thử nghiệm
Chạy các lệnh sau từ terminal (kết nối máy qua cáp USB có bật USB Debugging):

```bash
# 1. Gỡ bản cài đặt gốc cũ (nếu có):
adb uninstall com.candywriter.bitlife

# 2. Cài đặt bản Việt hóa:
adb install -r /workspaces/REA-TEST/work/out/bitlife_vi.apk

# 3. Khởi chạy game:
adb shell monkey -p com.candywriter.bitlife -c android.intent.category.LAUNCHER 1
```

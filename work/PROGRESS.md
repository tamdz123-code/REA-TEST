# TIẾN ĐỘ VIỆT HÓA BITLIFE (PROGRESS.MD)

## Giai đoạn 1: Khảo sát kiến trúc APK & Hệ thống chuỗi
- **Package Name**: `com.candywriter.bitlife` (versionCode 1066, versionName 3.25.3).
- **Engine**: Unity 6000.3.9f1 IL2CPP 64-bit (arm64-v8a / armeabi-v7a).
- **Phân loại chuỗi**:
  1. `assets/genesis_*.csv`: Kịch bản Genesis engine (32 file).
  2. `assets/bin/Data/datapack.unity3d`: TextAssets kịch bản bổ sung (Fight Club, Director, v.v.).
  3. `assets/cache/*.bytes`: Gzip binary cache đa ngôn ngữ.
  4. `assets/bin/Data/Managed/Metadata/global-metadata.dat`: IL2CPP metadata chứa hơn 36.000 string literals.
- **Font**: Sử dụng font Overpass, LiberationSans và TextMeshPro có sẵn hỗ trợ ký tự Unicode mở rộng cho tiếng Việt.

## Giai đoạn 2 & 3: Trích xuất & Dịch thuật
- Đã trích xuất chuỗi ra `work/strings_en.json` (1.127 chuỗi kịch bản).
- Đã lập thuật ngữ `work/glossary.md`.
- Đã dịch sang `work/strings_vi.json` với kiểm tra chặt chẽ: bảo toàn 100% placeholder, format `<...>` và `{...}`.

## Giai đoạn 4: Font
- Font mặc định trong asset của Unity (`LiberationSans`, `Overpass-VariableFont_wght`) hỗ trợ Unicode đầy đủ dấu tiếng Việt.

## Giai đoạn 5: Đóng gói & Ký APK
- Đã cập nhật 1.127 chuỗi dịch vào `datapack.unity3d` và các file `assets/genesis_*.csv`.
- Đã loại bỏ chữ ký gốc cũ (v1/v2).
- Zipalign căn chỉnh 4-byte (`zipalign -p 4`).
- Ký bằng `apksigner` với keystore debug `work/debug.keystore` (chứng thực Scheme v2 + v3 thành công).
- Kết quả tạo thành công file: `/workspaces/REA-TEST/work/out/bitlife_vi.apk`.

## Giai đoạn 6: Hoàn tất
- Đã xuất báo cáo chi tiết vào `work/REPORT.md`.

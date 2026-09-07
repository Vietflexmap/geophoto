# GeoPhoto AI · AI-assisted Field GIS

GeoPhoto AI biến ảnh hiện trường thành dữ liệu GIS có thể kiểm chứng, phân tích và xuất dùng ngay trên web.

## Pipeline

**Ảnh → EXIF → OCR/AI → GPS Validator → Confidence Score → GeoFeature → Satellite WebGIS → FOV/Measure/QA → Export**

## Tính năng

- Upload/kéo thả nhiều ảnh hiện trường.
- Đọc GPS, độ cao, hướng chụp, thời gian và GPS accuracy từ EXIF khi có.
- OCR fallback bằng Tesseract.js khi ảnh chỉ có tọa độ đóng trên ảnh.
- Parser tọa độ N/S/E/W, chuẩn hóa WGS84 / EPSG:4326.
- Confidence Score theo nguồn tọa độ, GPS accuracy, heading và kiểm tra phạm vi.
- WebGIS với Esri Satellite và OpenStreetMap.
- Marker clustering, popup ảnh, mở Google Maps/Google Earth.
- Mô phỏng camera FOV theo heading + góc nhìn + khoảng nhìn.
- Đo chuỗi khoảng cách trực tiếp trên bản đồ.
- QA: thiếu GPS, tọa độ trùng, confidence thấp, GPS accuracy thấp.
- Lưu metadata project trong trình duyệt; import/export Project JSON.
- Xuất GeoJSON, KML và CSV.
- Responsive desktop/mobile; có service worker để hỗ trợ PWA shell.

## Cách chạy

Mở `index.html`, hoặc dùng GitHub Pages. Ứng dụng là static HTML/CSS/JS nên không cần backend.

## Kiến trúc dữ liệu

Mỗi ảnh được chuyển thành một GeoFeature gồm các trường chính:

- `latitude`, `longitude`
- `altitude_m`
- `heading_deg`
- `fov_deg`
- `gps_accuracy_m`
- `confidence`
- `source` (`EXIF`, `OCR/AI`, `Manual`)
- `category`, `note`, `time`

## Lưu ý độ chính xác

GPS điện thoại phù hợp định vị, kiểm tra và đối chiếu hiện trường. Không nên dùng để xác lập ranh địa chính yêu cầu độ chính xác cm; trường hợp đó cần GNSS RTK hoặc Total Station.

## GitHub Pages

Workflow trong `.github/workflows/pages.yml` deploy toàn bộ root repository thành website GitHub Pages.

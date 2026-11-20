# Báo cáo cá nhân — Ngày 11

Họ tên: **Đỗ Thị Kim Oanh**    
Mã học viên: **2A202604034**  
Phiên bản CVAT (Help → About): **2.82.0**  
Guideline: **Road v1.0**    
Lần nộp (`revision` trong manifest): **1**  
Thời điểm export (ngày giờ trên CVAT): **2026-11-20, 16:20**    Số lần nộp lại sau Rework: **0**

## 1. Kiểm project

| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | `lane` polyline, `road_curb` polyline, `crosswalk` polygon, `drivable` polygon, `traffic_light` rectangle, `traffic_sign` rectangle. |
| Thuộc tính và giá trị | Có | Đối chiếu với `configs/road_v1_labels.json`; lane có position/style/color/kind, drivable có area_type, đèn và biển đủ thuộc tính. |
| 4 tag ảnh | Có | `camera`, `timeofday`, `weather`, `source`; mỗi tag có thuộc tính select `value`. Lint phát hiện A12 và B03 thiếu tag, các tag camera fisheye còn chọn sai giá trị. |

Cách kết thúc polyline trên bản CVAT này: **Bấm `N` sau điểm cuối; lane được vẽ từ gần xe ra xa. Vạch đứt được nối thành một polyline, không vẽ từng đoạn sơn riêng.**

Cách đặt tag ảnh trên bản CVAT này: **Dùng công cụ Tag, đặt camera trước rồi timeofday, weather và source; mở Details để kiểm tra/sửa `value` cho từng tag.**

## 2. Số lượng đã gán

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 14 | 7 | 13 | 13 | 9 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 12 | 12 | 9 | 8 | 2 | 7 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| **Tổng ảnh bắt buộc** | **20** | **40** | **26** | **16** | **21** | **15** | **16** |

## 3. Bảng ca khó

| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane / road_curb | Không có vạch sơn làn rõ ở phần đường xe chạy | Không vẽ lane; gán road_curb và drivable | Không suy đoán L1/R1 khi ảnh không có vạch nhìn thấy; ghi nhận miễn QC1-02 theo hướng dẫn coach. |
| A08 | crosswalk / lane | Vạch ngựa vằn có nhiều vệt trắng ngang | Một polygon crosswalk; lane chỉ theo vạch phân làn dọc | Crosswalk là vùng polygon, không gán từng vạch ngang thành lane. |
| B01 | lane polyline / mask polygon | SAM tạo mask dài bám theo vạch | R1/L1 phải là polyline; mask polygon được ghi nhận là lỗi cần sửa | Taxonomy CVAT quy định lane là polyline; mask không thay thế được thuộc tính và hướng vẽ của lane. |
| B05–B08 | position L1/R1 / other | Ảnh từ camera hai bên MVL/MVR | Tất cả lane phải là `position=other` | Quy tắc fisheye bên không dùng L1/R1; các lane hiện tại còn mang L1 nên được ghi QC1-03. |
| B03 | edge_zone / không bật | Biển nằm sát vòng ngoài ảnh fisheye | Bật `edge_zone` | Tâm box vượt ngưỡng 80% bán kính theo guideline. |

## 4. Phiếu QC 1 nhận được

Bạn kiểm lô của tôi: **Đỗ Thị Huyền**    Quyết định nhận được: **Rework**

| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-01 — tag camera và tag ảnh | 15 | Có; A12/B03 thiếu tag, camera fisheye đang mang giá trị `front`. | Chưa; giữ nguyên r1 và sửa trước lần nộp r2. |
| QC1-02 — đủ L1/R1 | 8 | Có; A05/A06 được miễn vì không thấy vạch rõ, các trường hợp còn lại cần bổ sung/đối chiếu lane. | Chưa; cập nhật sau khi rà từng ảnh. |
| QC1-03 — position | 8 | Có; lane ở B05–B08 phải đổi từ L1 sang `other`. | Chưa; sửa thuộc tính trong CVAT trước khi export r2. |
| QC1-04 — tâm vạch, chiều, điểm dừng | 8 | Có; các polyline front bị lint đánh dấu vẽ từ xa về gần. | Chưa; sửa hướng theo quy tắc gần ra xa. |
| QC1-05 — vạch đứt, che | 7 | Có; nhiều đoạn cùng position cho thấy vạch đứt bị tách. | Chưa; nối thành một polyline cho mỗi vạch. |
| QC1-11 — fisheye | 2 | Có; B03 cần thêm điểm theo cung và bật edge_zone cho biển. | Chưa; sẽ sửa cùng task fisheye. |
| QC1-12 — file/shape | 1 | Có; lane B01 đang là polygon, sai kiểu shape. | Chưa; vẽ lại thành polyline. |

Tổng hợp phản hồi: **25 lỗi nặng, 17 lỗi chính (8,3% trên 206 annotation item), 7 lỗi nhẹ**. Theo quy tắc QC1, còn lỗi nặng nên quyết định là Rework. Tại thời điểm viết báo cáo chưa có revision 2; bản r1 được giữ nguyên để đối chiếu.

## 5. Kiểm file export

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `task1/annotations.xml` (front; ZIP tương ứng `DoThiKimOanh-front.zip`) | Có | A01: 5 / 5 | A02: 4 / 4 | Có ở 11/12 ảnh; A12 thiếu toàn bộ tag. |
| `task2/annotations.xml` (fisheye; ZIP hiện có `DoThiHuyen-fisheye.zip`) | Có | B01: 4 / 4 | B02: 6 / 6 | Có ở 7/8 ảnh; B03 thiếu toàn bộ tag, các giá trị camera còn lại cần sửa từ `front` sang giá trị fisheye theo tên ảnh. |

Kiểm thêm: task1 có **12 ảnh, 84 shape**; task2 có **8 ảnh, 50 shape**. Các XML mở được và số shape mẫu khớp giữa job export và file. Tag camera có mặt không đồng nghĩa giá trị đúng; A12, B01–B08 được liệt kê trong QC để sửa.

## 6. Ảnh chụp màn hình

1. Tab **Project → Labels**: thấy đủ 6 label vẽ và 4 tag, đúng kiểu shape/thuộc tính theo Road v1.0.
2. Ảnh **A08** trong CVAT: minh họa lane, vùng drivable, crosswalk và các box đèn/biển.
3. Ảnh **B03** phóng to: minh họa lane fisheye theo cung và box biển ở vùng ngoài.
4. Trích đoạn `annotations.xml`: có phần tử `<polyline label="lane">` và các thuộc tính lane.

## 7. Tự đánh giá

Lỗi mắc nhiều nhất là **QC1-01 và các lỗi liên quan tag/camera**, sau đó là QC1-02/03 về lane. Cách tránh ở Ngày 20: đặt camera trước tiên theo hậu tố tên ảnh (FV/RV/MVL/MVR), kiểm lại `value` trong Details, rồi chạy lint ngay sau mỗi nhóm ảnh thay vì chờ đến lúc export.

Lane position sai làm model nhận nhầm làn đang đi với làn bên cạnh; tag camera sai làm dữ liệu của các góc nhìn fisheye bị trộn vào nhóm front. Lane bị tách hoặc đi sai chiều làm tín hiệu hình học không liên tục. Trong model lane detection/row-anchor, các lỗi này tạo target sai vị trí hoặc sai nhóm, khiến model dự đoán lệch vạch và làm giảm độ tin cậy của cảnh báo/giữ làn.

## 8. Buffer — Từ polyline đến đích row-anchor

Ví dụ dùng lane L1 trong ảnh A01. Hàng 720–560 lấy từ polyline trong task1; hàng x của bạn được kiểm là số minh họa gần với vạch để so sánh.

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | 105.0 | 152.2 | 199.5 | 246.7 | 296.6 |
| x của bạn kia | 112.0 | 160.0 | 206.0 | 254.0 | 304.0 |

1. Nếu dừng polyline sớm hơn 40 px ở đầu xa, hàng **y=560** sẽ thành “không có làn” vì nằm ngoài đoạn polyline.
2. Sai khác tại y=720 là **7.0 px**; tại y=560 là **7.4 px**. Sai lệch ở y=720 thường ảnh hưởng LKA nhiều hơn vì đó là vùng gần xe, nơi sai số ngang tác động trực tiếp hơn đến ước lượng vị trí làn.
3. Đảo thứ tự điểm không làm đổi phép nội suy x theo y nếu hình học vẫn nguyên vẹn. `rowanchor` vẫn tính được nhưng sẽ cảnh báo chiều vẽ; `road_check lint` cũng bắt lỗi QC1-04. Pipeline nào giả định điểm đầu gần xe có thể xử lý sai nếu thứ tự bị đảo.

# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đỗ Thị Huyền - 2A202604048   
Người kiểm: Đỗ Thị Kim Oanh 2A202604034  
Ngày: 2026-11-20    Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): task1.zip + task2.zip, revision 1  
Số ảnh kiểm: 20 
Số nhãn đã kiểm (shape + tag): 206 

> **Phạm vi kiểm:** Phiếu này ghi nhận kết quả chạy lint trên toàn bộ hai export. Mẫu số lỗi chính là 206 annotation item trong các file (shape + tag). GT riêng không được đưa vào lần kiểm này; quyết định dưới đây áp dụng các cảnh báo lint như phát hiện QC của lô.
>
> Lưu ý kết quả: B01–B08 có tag camera sai hoặc thiếu. Các cờ lint sai quy tắc cho camera bên MVL/MVR đã được phân loại lại: bỏ cờ thiếu L1/R1 và chiều theo trục y, thay bằng lỗi `position` trên 8 lane (phải là `other`). Cảnh báo trùng position của B06/B07 cũng được loại khỏi QC1-05. A05/A06 được miễn QC1-02 vì ảnh không có vạch làn rõ để gán.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi ghi nhận | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 80 tag cần có | 15 (9 nặng, 6 nhẹ) | nặng / nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 32 vị trí L1/R1 trên camera trước, fisheye trước/sau | 8 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 40 lane | 8 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 40 lane thuộc camera trước và fisheye trước/sau | 8 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 40 lane thuộc camera trước và fisheye trước/sau | 7 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 40 lane | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 63 shape liên quan | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 15 đèn | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 31 đèn/biển | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 16 biển | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 50 shape fisheye | 2 | chính |
| QC1-12 file | lỗi file | 214 mục cần kiểm theo export (shape + 4 tag/ảnh) | 1 | nhẹ |

Lint ban đầu báo 55 cảnh báo. Sau khi miễn 4 cờ QC1-02 ở A05/A06, loại 10 cờ không áp dụng cho camera bên, và ghi đúng 8 lỗi position của các lane bên, tổng cộng là **49 lỗi** (25 nặng, 17 chính, 7 nhẹ). Lỗi chính: **17 / 206 annotation item = 8,3%**.

## Danh sách phát hiện lint và phân loại cuối

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả / phân loại |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A01 | lane#4@(408,506) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 2 | QC1-05 | A01 | lane | chính | Có 2 polyline position=L1; vạch đứt bị tách thành nhiều polyline. |
| 3 | QC1-04 | A02 | lane#1@(592,396) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 4 | QC1-05 | A02 | lane | chính | Có 2 polyline position=L1; vạch đứt bị tách thành nhiều polyline. |
| 5 | QC1-02 | A03 | lane | nặng | Thiếu R1. |
| 6 | QC1-05 | A03 | lane | chính | Có 2 polyline position=L1; vạch đứt bị tách thành nhiều polyline. |
| 7 | QC1-04 | A04 | lane#2@(602,321) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 8 | QC1-05 | A04 | lane | chính | Có 2 polyline position=L1; vạch đứt bị tách thành nhiều polyline. |
| 9 | QC1-02 | A05 | lane | miễn | Không có vạch làn nhìn thấy; miễn theo quy tắc coach xác nhận ảnh không có vạch. |
| 10 | QC1-02 | A05 | lane | miễn | Không có vạch làn nhìn thấy; miễn theo quy tắc coach xác nhận ảnh không có vạch. |
| 11 | QC1-02 | A06 | lane | miễn | Ảnh giao lộ/crosswalk không có L1/R1 rõ để gán; miễn theo quy tắc coach xác nhận. |
| 12 | QC1-02 | A06 | lane | miễn | Ảnh giao lộ/crosswalk không có L1/R1 rõ để gán; miễn theo quy tắc coach xác nhận. |
| 13 | QC1-04 | A07 | lane#1@(713,264) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 14 | QC1-02 | A08 | lane | nặng | Thiếu R1. |
| 15 | QC1-04 | A08 | lane#1@(647,310) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 16 | QC1-04 | A08 | lane#3@(762,314) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 17 | QC1-05 | A08 | lane | chính | Có 2 polyline position=L1; vạch đứt bị tách thành nhiều polyline. |
| 18 | QC1-02 | A09 | lane | nặng | Thiếu L1. |
| 19 | QC1-04 | A10 | lane#0@(770,394) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 20 | QC1-02 | A11 | lane | nặng | Thiếu R1. |
| 21 | QC1-04 | A11 | lane#4@(602,433) | chính | Điểm đầu cao hơn điểm cuối, ngược quy tắc gần ra xa. |
| 22 | QC1-05 | A11 | lane | chính | Có 2 polyline position=L1; vạch đứt bị tách thành nhiều polyline. |
| 23 | QC1-01 | A12 | tag:camera | nặng | Thiếu tag camera. |
| 24 | QC1-01 | A12 | tag:timeofday | nhẹ | Thiếu tag timeofday. |
| 25 | QC1-01 | A12 | tag:weather | nhẹ | Thiếu tag weather. |
| 26 | QC1-01 | A12 | tag:source | nhẹ | Thiếu tag source. |
| 27 | QC1-05 | A12 | lane | chính | Có 2 polyline position=L2; vạch đứt bị tách thành nhiều polyline. |
| 28 | QC1-12 | B01 | lane#3@(42,552) | nhẹ | `lane` được lưu dạng polygon thay vì polyline. |
| 29 | QC1-01 | B01 | tag:camera | nặng | Camera đang là `front`, đúng theo tên ảnh là `fisheye_front`. |
| 30 | QC1-02 | B01 | lane | nặng | Thiếu R1 theo lint. |
| 31 | QC1-01 | B02 | tag:camera | nặng | Camera đang là `front`, đúng theo tên ảnh là `fisheye_front`. |
| 32 | QC1-02 | B02 | lane | nặng | Thiếu L1 theo lint. |
| 33 | QC1-02 | B02 | lane | nặng | Thiếu R1 theo lint. |
| 34 | QC1-01 | B03 | tag:camera | nặng | Thiếu tag camera; đúng theo tên ảnh là `fisheye_rear`. |
| 35 | QC1-01 | B03 | tag:timeofday | nhẹ | Thiếu tag timeofday. |
| 36 | QC1-01 | B03 | tag:weather | nhẹ | Thiếu tag weather. |
| 37 | QC1-01 | B03 | tag:source | nhẹ | Thiếu tag source. |
| 38 | QC1-11 | B03 | lane#3@(765,294) | chính | Lane fisheye chỉ có 3 điểm, chưa đủ điểm mô tả cung theo quy tắc lint. |
| 39 | QC1-11 | B03 | traffic_sign#8@(1130,362) | chính | `edge_zone` đang tắt trong khi vị trí box vượt ngưỡng 80% bán kính theo lint. |
| 40 | QC1-01 | B04 | tag:camera | nặng | Camera đang là `front`, đúng theo tên ảnh là `fisheye_rear`. |
| 41 | QC1-02 | B04 | lane | nặng | Thiếu R1 theo lint. |
| 42 | QC1-01 | B05 | tag:camera | nặng | Camera đang là `front`, đúng theo tên ảnh là `fisheye_left`. |
| 43 | QC1-02 | B05 | lane | loại khỏi QC1-02 | Không áp dụng: camera bên không yêu cầu L1/R1; position sai được ghi ở QC1-03. |
| 44 | QC1-04 | B05 | lane#0@(1119,442) | loại khỏi tính điểm | Heuristic theo trục y không xác định chiều gần-ra-xa cho camera bên. |
| 45 | QC1-01 | B06 | tag:camera | nặng | Camera đang là `front`, đúng theo tên ảnh là `fisheye_left`. |
| 46 | QC1-02 | B06 | lane | loại khỏi QC1-02 | Không áp dụng: camera bên không yêu cầu L1/R1; position sai được ghi ở QC1-03. |
| 47 | QC1-04 | B06 | lane#0@(958,535) | loại khỏi tính điểm | Heuristic theo trục y không xác định chiều gần-ra-xa cho camera bên. |
| 48 | QC1-05 | B06 | lane | loại khỏi QC1-05 | Cả lane camera bên đều cần position=other; ghi lỗi position cho từng shape tại QC1-03. |
| 49 | QC1-01 | B07 | tag:camera | nặng | Camera đang là `front`, đúng theo tên ảnh là `fisheye_right`. |
| 50 | QC1-02 | B07 | lane | loại khỏi QC1-02 | Không áp dụng: camera bên không yêu cầu L1/R1; position sai được ghi ở QC1-03. |
| 51 | QC1-04 | B07 | lane#2@(699,135) | loại khỏi tính điểm | Heuristic theo trục y không xác định chiều gần-ra-xa cho camera bên. |
| 52 | QC1-05 | B07 | lane | loại khỏi QC1-05 | Cả lane camera bên đều cần position=other; ghi lỗi position cho từng shape tại QC1-03. |
| 53 | QC1-01 | B08 | tag:camera | nặng | Camera đang là `front`, đúng theo tên ảnh là `fisheye_right`. |
| 54 | QC1-02 | B08 | lane | loại khỏi QC1-02 | Không áp dụng: camera bên không yêu cầu L1/R1; position sai được ghi ở QC1-03. |
| 55 | QC1-04 | B08 | lane#1@(214,626) | loại khỏi tính điểm | Heuristic theo trục y không xác định chiều gần-ra-xa cho camera bên. |
| 56 | QC1-03 | B05 | lane#0@(1119,442) | nặng | Camera fisheye_left; position hiện tại L1, phải là other. |
| 57 | QC1-03 | B06 | lane#0@(958,535) | nặng | Camera fisheye_left; position hiện tại L1, phải là other. |
| 58 | QC1-03 | B06 | lane#4@(154,260) | nặng | Camera fisheye_left; position hiện tại L1, phải là other. |
| 59 | QC1-03 | B07 | lane#0@(66,674) | nặng | Camera fisheye_right; position hiện tại L1, phải là other. |
| 60 | QC1-03 | B07 | lane#2@(699,135) | nặng | Camera fisheye_right; position hiện tại L1, phải là other. |
| 61 | QC1-03 | B07 | lane#3@(947,275) | nặng | Camera fisheye_right; position hiện tại L1, phải là other. |
| 62 | QC1-03 | B07 | lane#4@(75,756) | nặng | Camera fisheye_right; position hiện tại L1, phải là other. |
| 63 | QC1-03 | B08 | lane#1@(214,626) | nặng | Camera fisheye_right; position hiện tại L1, phải là other. |

## Trường hợp đặc biệt và quyết định áp dụng

| Ảnh | Trường hợp | Quyết định |
| --- | --- | --- |
| A05, A06 | Không thấy vạch lane rõ để gán L1/R1. | Miễn cảnh báo QC1-02 cho hai ảnh này theo ngoại lệ của guideline. |
| B05–B08 | Camera MVL/MVR; tất cả 8 lane shape đang có position=L1. | Không tính lint thiếu L1/R1; ghi 8 lỗi QC1-03 vì mỗi shape phải là position=other. |
| B05–B08 | Lint dùng trục y để gợi ý hướng vẽ; ảnh fisheye bên không thể quyết định chiều chỉ từ y. | Loại 4 cảnh báo QC1-04 khỏi phép tính QC1. |
| B06, B07 | Lint báo cùng position trên các lane camera bên. | Không tính QC1-05 riêng; các shape được ghi nhận theo QC1-03. |
| B03 | Lane có 3 điểm; traffic_sign có edge_zone tắt dù vị trí box vượt ngưỡng. | Ghi nhận 2 lỗi QC1-11. |

## Quyết định

Lỗi nặng: **25**    Lỗi chính: **17 / 206 annotation item = 8,3%**    Lỗi nhẹ: **7**    Ca chờ lead: **0**

Quyết định (Release / Hold / Rework): **Rework**

Lý do: có 25 lỗi nặng nên lô phải Rework. Tỉ lệ lỗi chính 8,3% cũng vượt ngưỡng 5%. Sửa tag camera trước; đổi 8 lane ở B05–B08 sang position=other; sửa các lane L1/R1 bị thiếu và các polyline vẽ ngược/tách; đổi shape lane ở B01 từ polygon thành polyline; bật edge_zone cho biển B03.

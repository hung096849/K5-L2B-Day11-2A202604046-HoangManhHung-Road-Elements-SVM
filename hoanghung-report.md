# Báo cáo cá nhân — Ngày 11
Họ tên: Hoàng Mạnh Hùng    Mã học viên: 2A202604046
Phiên bản CVAT (Help → About): 2.8
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 2
Thời điểm export (ngày giờ trên CVAT): 21/11/2026  10h Số lần nộp lại sau Rework: 1

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane, road_curb: polyline; crosswalk, drivable: polygon; traffic_light, traffic_sign: rectangle |
| Thuộc tính và giá trị | Đúng | Khớp Raw labels JSON của `road_lab.taxonomy` |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source; mỗi tag có thuộc tính select `value` |

Cách kết thúc polyline trên bản CVAT này: nhấn phím N để kết thúc polyline đang vẽ.
Cách đặt tag ảnh trên bản CVAT này: chọn chế độ "Tag annotation" ở menu thả xuống trên thanh bên (cùng hàng với Fullscreen, Info, Filters), chọn label (camera, timeofday, weather, source) rồi thêm tag cho từng ảnh; sau đó mở lại kiểm giá trị `value`. Bấm lại phím tắt trên ảnh đã có tag cùng label sẽ xóa tag đó nên phải kiểm lại cuối cùng.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 26 | 4 | 6 | 0 | 36 | 12 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 6 | 6 | 7 | 0 | 4 | 1 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

Ghi chú: chưa vẽ `drivable` ở ảnh nào (cột drivable = 0). Không làm ảnh thưởng.

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05, A07 (A06 thiếu R1) | lane | Vẽ thêm L1/R1 hoặc không vẽ | Không vẽ | Không thấy vạch trong ảnh; vẽ thêm là gán thứ không có. Xin coach xác nhận |
| A04 | lane | `kind` single hoặc double | double | Vạch vàng đôi theo guideline |
| A04 | traffic_light | red hoặc green | green | Phiếu nta nghi đèn đang sáng là xanh; phóng to thấy màu đang sáng là xanh, guideline: `color` là màu đang sáng |
| B02 | traffic_light | `edge_zone` bật hoặc không | Bật cho cả 3 đèn | Tâm hộp nằm ngoài 80 % bán kính vòng ảnh |
| B05–B08 | lane | `position` L1/R1 hoặc `other` | other | Camera fisheye_left và fisheye_right luôn dùng `other` |
| Các ảnh có biển | traffic_sign | Khó phân biệt `group` | Nhóm gần nhất theo chức năng | Phân nhóm theo chức năng, không theo hình hay màu; biển không chắc nhóm thì chọn nhóm gần nhất |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Ngô Trí Anh (nta)    Quyết định nhận được: Rework (4 lỗi nặng; 8 lỗi chính / 45 nhãn = 17,78 %)
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 (position, nặng) | 4 | Có: A01 lane#2 → L2; A02 lane#1 → L1; A04 lane#1 → L1; A04 lane#3 → R1 | Rồi |
| QC1-04 (chiều vẽ, chính) | 2 | Có: A01 lane#2, A04 lane#1 vẽ xa → gần | Rồi: đảo thứ tự điểm thành gần → xa. Tự rà thêm, A03 có 2 vạch cùng lỗi (lint báo), đã đảo |
| QC1-06 (style/color/kind, chính) | 3 | Có: A02 → dashed; A04 lane#1 → yellow/solid/double; A04 lane#3 → dashed/single | Rồi |
| QC1-11 (edge_zone, chính) | 3 | Có: B02 ba đèn có tâm box ở vùng rìa | Rồi: bật `edge_zone` |

Phiếu còn ghi ba ca chưa kết luận. Màu đèn A04: đã phóng to và đổi red thành green. Drivable: chưa vẽ, ghi nhận là thiếu. B08 lane 3 điểm: đã tự kiểm lại theo cung.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| hoanghung-front.zip | Có | A01: 4 / 8 | A02: 3 / 7 | Có (front) |
| hoanghung-fisheye.zip | Có | B01: 1/ 5 | B02: 4 / 8 | Có (fisheye_front) |

Số file tính cả 4 tag mỗi ảnh. Tổng toàn bộ: 84 + 24 shape + 80 tag = 188, khớp số object trên CVAT.

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `label.png`
2. Một ảnh camera trước đã gán đủ (làn, đèn/biển; ví dụ A08): `camera.png`
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong (ví dụ B03): fisheeye.png`
4. Một đoạn XML có `<polyline label="lane">`: `xml.png`

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: QC1-03 (đổi nhầm `position`, 4 lỗi nặng) và QC1-04 (vẽ xa → gần, 4 vạch). Nguyên nhân là tôi vẽ nhanh, không mở lại Details để sửa thuộc tính mặc định (CVAT tự điền `L1`, `solid`, `white`, `single`) và không kiểm chiều điểm đầu. Ở Ngày 20: vẽ xong từng vạch là sửa ngay `position` và `style`; xác định L1/R1 trước bằng hai vạch kẹp làn xe đang đi; điểm đầu đặt sát xe (y lớn nhất) trước; mỗi 3 ảnh chạy `lint` một lần thay vì để cuối. Với đèn, sau khi vẽ phải đặt `color` theo màu đang sáng, không để mặc định `red`.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: nhãn làn đi vào model phát hiện làn cho hệ hỗ trợ giữ làn (LKA). Lỗi QC1-03 (vạch bên trái gán R1, hoặc vạch ngoài gán L1) làm model học sai vạch nào kẹp làn xe đang đi, nên có thể tính sai vị trí làn và khoảng cách tới vạch. Lỗi QC1-04 (vẽ xa → gần) làm điểm đầu không còn là điểm sát xe, trong khi đó là điểm quan trọng nhất; khi chuyển polyline thành đích theo hàng (row-anchor), thứ tự điểm sai làm lấy mẫu sai hàng, model học lệch ở vùng gần xe.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Không làm (hoạt động tùy chọn, không tính điểm).

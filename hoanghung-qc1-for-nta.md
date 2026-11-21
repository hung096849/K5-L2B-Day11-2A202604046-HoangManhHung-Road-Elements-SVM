# Phiếu QC 1 — Road v1.0

Lô được kiểm (nta): Ngô Trí Anh      Người kiểm (hoanghung): Hoàng Mạnh Hùng
Ngày: 21/11/2026                         Phiên bản guideline: Road v1.0  
File được kiểm: nta-front.zip, nta-fisheye.zip, nta-front-extra.zip, nta-fisheye-extra.zip revision 1. Hash và số byte khớp manifest đi kèm
Số ảnh kiểm: 20 bắt buộc (A01–A12, B01–B08) (+ 8 ảnh thêm A13–A16, B09–B12, ghi riêng)   Số nhãn đã kiểm (shape + tag): 237 (157 shape + 80 tag)

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 20 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 20 | 6 (chờ xác nhận) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 32 | 4 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 32 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 32 | 0 (1 chờ xác nhận) | chính |
| QC1-06 style, color, kind | sai thuộc tính | 32 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 23 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 39 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 70 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 31 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 25 | 0 (2 chờ xác nhận) | chính |
| QC1-12 file | lỗi file | 2 | 12 nhẹ | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | B07 | lane #2 | nặng | Camera MVR: position phải là `other` |
| 2 | QC1-03 | B07 | lane #3 | nặng | Camera MVR: position phải là `other` |
| 3 | QC1-03 | B07 | lane #4 | nặng | Camera MVR: position phải là `other` |
| 4 | QC1-03 | B08 | lane #0 | nặng | Camera MVR: position phải là `other` |
| 5 | QC1-12 | A01 | drivable #0, #2, #6 | nhẹ | Điểm lặp liền nhau (1, 3, 2 điểm) |
| 6 | QC1-12 | A02 | drivable #3, #6 | nhẹ | Điểm lặp liền nhau (2 điểm mỗi nhãn) |
| 7 | QC1-12 | A04 | drivable #1 | nhẹ | Điểm lặp liền nhau |
| 8 | QC1-12 | A07 | drivable #1 | nhẹ | Điểm lặp liền nhau |
| 9 | QC1-12 | A08 | lane #3 | nhẹ | Điểm lặp liền nhau |
| 10 | QC1-12 | A09 | drivable #4 | nhẹ | Điểm lặp liền nhau |
| 11 | QC1-12 | A11 | drivable #2, #5 | nhẹ | Điểm lặp liền nhau |
| 12 | QC1-12 | A12 | road_curb #12 | nhẹ | Điểm lặp liền nhau |

Ảnh thêm (ghi riêng, không tính vào tỉ lệ):
| # | Mã | Ảnh | Nhãn | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| E1 | QC1-01 | B10 | tag camera | nặng | Gán `fisheye_right` nhưng tên file là MVL (phải `fisheye_left`) |
| E2 | QC1-02 | A14 | lane | nặng (chờ xác nhận) | Chưa có R1 |
| E3 | QC1-12 | A14 crosswalk #6, A15 drivable #3 | | nhẹ | Điểm lặp liền nhau |

Không tính vào lỗi: cảnh báo box thấp hơn 8 px (A03 #8 #9, A04 #2, A07 #3 #7, A08 #9, A15 #16) là gợi ý, không bắt buộc gán.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Không có lane nào (chỉ drivable, road_curb). Có thật sự không thấy vạch L1/R1 không? | Không có vạch nào |
| A06 | Thiếu R1: vạch phải có thấy được không? | Không |
| A07 | Thiếu L1: vạch trái có thấy được không? | Không |
| A08 | Thiếu L1: vạch trái có thấy được không? | Có |
| A09 | Thiếu R1: vạch phải có thấy được không? | Có |
| B07 | Hai polyline cùng position R1 (nay phải là `other`): có phải một vạch đứt bị tách không? | |
| B02 | traffic_light #2, #3: tâm hộp ngoài 80 % bán kính, edge_zone đã bật chưa? | |

## Quyết định
Lỗi nặng: 4 (chưa kể 6 ca QC1-02 chờ xác nhận)   Lỗi chính: 0 / 237 nhãn = 0 % (tối đa 3 nếu B07 và B02 được xác nhận lỗi = 1,3 %)   Lỗi nhẹ: 12   Ca chờ lead: 7  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): còn ít nhất một lỗi nặng (4 lỗi QC1-03 ở B07, B08: lane camera hai bên không dùng `position = other`) nên Rework, không phụ thuộc lời đáp của lead cho các ca mơ hồ.

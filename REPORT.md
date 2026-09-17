# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602270
- Ngày / CVAT local: 17/09/2026 / http://localhost:8080
- Công cụ đã dùng: Brush / Polygon / AI Tool: DINOv3 (base 640)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg`, chiếc xe máy (`motorcycle`) lớn ở góc dưới bên phải.
- Class và quy tắc tôi dùng để chọn biên: Gán nhãn `motorcycle`; vẽ sát phần nhìn thấy của thân xe, bao gồm ghi đông và kính chắn gió, dừng biên tại mép tiếp xúc với mặt đường và người ngồi trên xe.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Gợi ý bị dính người lái vào xe và lem viền ra mặt đường; tôi dùng Brush tỉa lại viền xe và tách người thành nhãn `person` riêng.
- Nếu không dùng gợi ý: Đã dùng gợi ý và thực hiện sửa như trên.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `cp2_slice`, ảnh `000000017627.jpg`, hai ô tô đỗ sát nhau bên lề đường bên phải.
- Lỗi thuộc loại: gộp-tách.
- Bằng chứng tôi nhìn thấy: Hai xe cùng loại bị gộp dính thành 1 mask dù có khe hở và đường bóng ranh giới giữa hai thân xe.
- Quy tắc và hành động sửa: Quy tắc instance yêu cầu phân biệt từng vật; dùng Polygon cắt theo khe hở chia thành 2 instance `car` riêng biệt.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại thành `cp2_slice.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `cp4_curb` (`7d83710e-4697c3b2.png`), mép gờ bó vỉa | `road` hay `sidewalk` | Gờ đá nhô cao phân làn người đi bộ và lòng đường | Gán gờ bó vỉa vào `sidewalk` theo chức năng phân ranh giới |
| 2. `cp1_holes` (`000000144300.jpg`), kính xe buýt nhìn xuyên thấu | Khoét lỗ hậu cảnh hay giữ mask xe | Kính là thành phần kết cấu của phương tiện | Giữ nguyên kính trong mask `bus`, không khoét lỗ |
| 3. `cp5_occlusion` (`000000336232.jpg`), xe bị cột che cắt đôi | 2 instance riêng hay 1 instance | Cùng một xe bị che khuất thành hai mảng nhìn thấy | Gộp 2 mảng thành 1 instance `car` duy nhất |

# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Báo cáo này đã được điền theo bài làm trong thư mục `submissions/`. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602118
- Ngày / CVAT local: 17/09/2026 / CVAT local
- Công cụ đã dùng: Brush/Mask và Polygon

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh đầu tiên của `medium_instance`, object xe ở vùng giữa ảnh.
- Class và quy tắc tôi dùng để chọn biên: Chọn class theo `classes.json`; chỉ vẽ phần nhìn thấy và dừng biên tại phần bị che, không đoán phần khuất.
- Nếu dùng gợi ý sau đó: Không dùng gợi ý tự động; tôi kiểm tra lại mask bằng ảnh gốc trước khi Save.
- Nếu không dùng gợi ý: Không dùng; các vật cùng class nhưng là vật riêng được giữ thành các mask riêng.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `medium_instance`, ảnh đầu tiên, vùng các xe đứng gần nhau.
- Lỗi thuộc loại: gộp-tách.
- Bằng chứng tôi nhìn thấy: Hai xe cùng class ở gần nhau nhưng cần được biểu diễn thành hai instance riêng.
- Quy tắc và hành động sửa: Tôi kiểm tra khe và đường biên giữa hai xe, tách thành hai mask riêng, rồi kiểm tra lại tab Objects.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại `medium_instance.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có). Hiện chưa có điểm tự đánh giá. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `cp4_curb`, vùng bó vỉa | Road hoặc sidewalk | Dựa vào ranh vật lý của bó vỉa và chức năng vùng, không chỉ dựa vào màu gần giống | Chọn class theo vùng bề mặt; kiểm tra lại biên sau khi phóng to. |
| `cp2_slice`, hai vật sát nhau | Một mask hoặc hai mask | Hai vật cùng class vẫn là hai instance nếu có ranh tách biệt | Tách thành hai object riêng. |
| `cp5_occlusion`, vật bị che | Tô nối qua phần khuất hoặc chỉ tô phần nhìn thấy | Không đoán đường biên phía sau vật che | Chỉ giữ phần nhìn thấy và ghi nhận đây là ca cần cân nhắc. |

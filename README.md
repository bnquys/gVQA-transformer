# gVQA-transformer

Đây là dự án cuối kỳ môn Học sâu với trọng tâm là xây dựng hệ thống hỏi đáp trên ảnh tiếng Việt cho miền biển báo giao thông, đồng thời mở rộng sang một nhiệm vụ làm giàu metadata và chuẩn hóa dữ liệu cho VQA đa miền tiếng Việt.

## Nội dung chính

Dự án gồm hai phần:

- Xây dựng và so sánh hai hướng tiếp cận cho bài toán VQA tiếng Việt.
- Đề xuất một quy trình nâng cấp dữ liệu nhằm hỗ trợ tốt hơn cho các bài toán VQA thế hệ sinh.

## Bài toán

Đầu vào của hệ thống là:

- Ảnh
- Câu hỏi tiếng Việt

Đầu ra là:

- Câu trả lời tiếng Việt ngắn, đúng ngữ cảnh và phù hợp với nội dung thị giác

Miền dữ liệu được lựa chọn là biển báo giao thông Việt Nam, giúp bài toán vừa có tính thực tế, vừa đủ rõ ràng để đánh giá khả năng hiểu ảnh và hiểu ngôn ngữ của mô hình.

## Dữ liệu

Thống kê chính của tập dữ liệu biển báo giao thông:

| Tập dữ liệu | Số bộ hỏi đáp | Số ảnh |
| --- | ---: | ---: |
| Huấn luyện | 2075 | 308 |
| Xác thực | 273 | 39 |
| Kiểm thử | 260 | 39 |
| Tổng | 2608 | 386 |

Phân bố theo nhóm câu hỏi:

| Nhóm câu hỏi | Huấn luyện | Xác thực | Kiểm thử | Tổng |
| --- | ---: | ---: | ---: | ---: |
| Nhận dạng đối tượng | 403 | 53 | 52 | 508 |
| Thuộc tính | 425 | 53 | 51 | 529 |
| Đúng hoặc sai | 420 | 56 | 52 | 528 |
| Đếm số lượng | 390 | 51 | 50 | 491 |
| Quan hệ không gian | 437 | 60 | 55 | 552 |

## Phương pháp

Dự án đánh giá hai hướng tiếp cận:

- Hướng A là cách xây dựng hệ thống từ các thành phần chuyên biệt cho ảnh, ngôn ngữ và phần sinh câu trả lời.
- Hướng B là cách tận dụng mô hình đa phương thức huấn luyện trước, sau đó thích nghi theo miền dữ liệu tiếng Việt chuyên biệt.

Ngoài ra, nhóm còn thử thêm một bước nâng cao theo hướng tối ưu phản hồi dựa trên dữ liệu sở thích để kiểm tra khả năng cải thiện độ tự nhiên và độ hợp lý của câu trả lời.

## Kết quả chính

| Cấu hình | Exact Match | BLEU | ROUGE-L | METEOR | BERTScore F1 | Gemini Judge |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| A1 | 0.3692 | 0.2959 | 0.7008 | 0.5003 | 0.7697 | 0.5500 |
| A2 | 0.3000 | 0.2297 | 0.6572 | 0.4469 | 0.7407 | 0.4950 |
| B1 | 0.0000 | 0.0456 | 0.3293 | 0.2904 | 0.7426 | 0.3800 |
| B2 | 0.2423 | 0.4149 | 0.6963 | 0.6450 | 0.8953 | 0.7400 |

Kết quả của bước nâng cao:

| Cấu hình | Exact Match | BLEU | ROUGE-L | METEOR | BERTScore F1 | Gemini Judge |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| B2 | 0.2423 | 0.4149 | 0.6963 | 0.6450 | 0.8953 | 0.7438 |
| B3 | 0.2346 | 0.4022 | 0.6905 | 0.6369 | 0.8930 | 0.7450 |

Nhìn chung:

- A1 mạnh nhất nếu ưu tiên độ khớp chính xác với đáp án chuẩn.
- B2 nổi bật hơn nếu ưu tiên chất lượng ngôn ngữ và mức độ hợp nghĩa tổng thể.
- Bước nâng cao cho thấy tiềm năng cải thiện nhẹ tính tự nhiên của câu trả lời.

## Nhiệm vụ mở rộng

Phần mở rộng của dự án tập trung vào việc làm giàu metadata và chuẩn hóa dữ liệu cho bộ VQA đa miền tiếng Việt. Quy trình này giúp:

- Chuẩn hóa cách diễn đạt của câu hỏi
- Bổ sung nhãn loại câu hỏi
- Giảm sự không đồng đều của dữ liệu
- Tạo nền tốt hơn cho các nghiên cứu VQA thế hệ sinh trong tương lai

## Tài nguyên nộp bài

- GitHub repository: https://github.com/bnquys/gVQA-transformer
- Video demo: https://drive.google.com/drive/folders/12ctRytK7-cbamtFsxwbOyBM7KkNpeMRi?usp=sharing
- Notebook trình bày kết quả hướng B: https://www.kaggle.com/code/spixalo/dl-endterm-b2-vnts
- Notebook trình bày bước nâng cao: https://www.kaggle.com/code/spixalo/dl-endterm-b2-rl
- Notebook tổng hợp độ đo: https://www.kaggle.com/code/spixalo/dl-endterm-b-allmetrics
- Bộ dữ liệu đa miền tiếng Việt: https://huggingface.co/datasets/tung213/vietnamese-vqa_merged
- Mô hình đã huấn luyện cho hướng A: https://huggingface.co/VHT-2012/gVQA-transformer

# gVQA-transformer

<<<<<<< HEAD
Đây là dự án cuối kỳ môn Học sâu về **Visual Question Answering (VQA) tiếng Việt**. Dự án gồm ba phần chính:

- **Task 1A**: xây dựng hệ thống VQA theo hướng mô hình ghép từ các thành phần chuyên biệt.
- **Task 1B**: xây dựng hệ thống VQA theo hướng mô hình đa phương thức huấn luyện trước.
- **Task 2**: làm giàu metadata và chuẩn hóa dữ liệu cho bộ VQA đa miền tiếng Việt.

README này được viết theo hướng thực hành: người mới mở repo vẫn có thể hiểu thư mục nào dùng để làm gì, nên chạy notebook nào trước, đầu ra sẽ nằm ở đâu, và khi nào nên dùng máy có GPU.

## 1. Mục tiêu dự án

Mục tiêu chung của dự án là xây dựng một hệ thống nhận vào:

- ảnh
- câu hỏi tiếng Việt

và sinh ra:

- câu trả lời tiếng Việt ngắn, đúng ngữ cảnh

Miền dữ liệu chính của Task 1 là **biển báo giao thông Việt Nam**. Bên cạnh đó, nhóm còn xây dựng một pipeline cho **Task 2** nhằm chuẩn hóa và làm giàu dữ liệu VQA đa miền tiếng Việt để phục vụ các nghiên cứu mở rộng.

## 2. Cấu trúc thư mục

```text
gVQA-transformer/
├── Dataset_TrafficSigns/
├── Task1_A/
├── Task1B/
├── task-2/
├── report_assets/
├── link.txt
└── README.md
```

Ý nghĩa từng thư mục:

- `Dataset_TrafficSigns/`: notebook hỗ trợ phân tích và tạo dữ liệu biển báo giao thông.
- `Task1_A/`: toàn bộ phần xử lý dữ liệu, huấn luyện, đánh giá và demo cho Task 1A.
- `Task1B/`: toàn bộ phần zero-shot, fine-tuning, bước nâng cao và đánh giá cho Task 1B.
- `task-2/`: pipeline làm giàu metadata, chuẩn hóa câu hỏi và chuẩn bị dữ liệu đầu ra.
- `report_assets/`: các hình dùng cho báo cáo, gồm sơ đồ và ảnh minh họa.
- `link.txt`: các liên kết tới video demo, notebook chạy ngoài, dataset và checkpoint.

## 3. Môi trường chạy được khuyến nghị

Vì dự án gần như hoàn toàn được triển khai bằng notebook, cách chạy thuận tiện nhất là:

- **Kaggle Notebook** hoặc **Google Colab** cho các phần cần GPU
- **Jupyter Notebook tại máy local** cho các phần nhẹ hơn như đọc dữ liệu, kiểm tra cấu trúc thư mục, xem kết quả

Khuyến nghị:

- `Task 1A`: có thể chạy trên GPU tầm trung
- `Task 1B`: nên chạy trên GPU mạnh hơn vì dùng mô hình đa phương thức lớn
- `Task 2`: một số bước có thể chạy CPU, nhưng các bước sinh dữ liệu và xử lý bằng mô hình lớn nên dùng GPU

## 4. Cách mở và chạy notebook

Nếu chạy ở local:

1. Cài Python 3.10 hoặc mới hơn.
2. Cài Jupyter Notebook hoặc JupyterLab.
3. Mở terminal tại thư mục dự án.
4. Chạy:

```bash
jupyter notebook
```

hoặc

```bash
jupyter lab
```

5. Mở notebook theo đúng thứ tự khuyến nghị trong README này.

Nếu chạy trên Kaggle hoặc Colab:

1. Tạo notebook mới.
2. Tải hoặc gắn dữ liệu cần thiết.
3. Chép nội dung notebook trong repo sang môi trường đó, hoặc mở notebook tương ứng nếu bạn đã upload repo.
4. Bật GPU trước khi chạy các phần huấn luyện và sinh dữ liệu.

## 5. Phụ thuộc thường dùng

Vì repo gồm nhiều notebook khác nhau, không có một file cài đặt duy nhất cho toàn dự án. Bạn có thể cài theo từng nhóm như sau.

### 5.1 Nhóm phụ thuộc cho Task 1A

```bash
pip install timm transformers accelerate sentencepiece pandas pillow tqdm matplotlib nltk rouge-score bert-score google-genai gradio kagglehub
```

### 5.2 Nhóm phụ thuộc cho Task 1B

```bash
pip install unsloth trl bitsandbytes transformers accelerate datasets sentencepiece pandas pillow tqdm matplotlib evaluate
```

### 5.3 Nhóm phụ thuộc cho Task 2

```bash
pip install pandas tqdm transformers accelerate bitsandbytes qwen-vl-utils langdetect
```

Ghi chú:

- Không nhất thiết phải cài toàn bộ một lần nếu bạn chỉ chạy một phần của dự án.
- Với Kaggle hoặc Colab, nhiều notebook đã có sẵn lệnh cài phụ thuộc ngay bên trong.

## 6. Hướng dẫn chạy chi tiết theo từng phần

### 6.1 Task 1A

Thư mục làm việc chính:

- `Task1_A/notebooks/`
- `Task1_A/processed/`
- `Task1_A/results/`

Thứ tự chạy khuyến nghị:

1. `01_data.ipynb`
2. `02_shared.ipynb`
3. `03_train.ipynb`
4. `04_eval.ipynb`
5. `05_demo.ipynb`

Giải thích từng notebook:

- `01_data.ipynb`: tạo và kiểm tra bộ dữ liệu cho bài toán biển báo giao thông.
- `02_shared.ipynb`: phần dùng chung cho mô hình và dữ liệu, cần có trước khi chạy huấn luyện.
- `03_train.ipynb`: huấn luyện hai cấu hình của Task 1A.
- `04_eval.ipynb`: đánh giá kết quả và xuất các độ đo.
- `05_demo.ipynb`: chạy phần minh họa dự đoán.

Đầu ra quan trọng sau khi chạy:

- `Task1_A/processed/report.json`: thống kê và kiểm tra ràng buộc dữ liệu.
- `Task1_A/processed/train.json`, `val.json`, `test.json`: dữ liệu đã chia tập.
- `Task1_A/results/a_compare.csv`: bảng kết quả tổng hợp cho Task 1A.
- `Task1_A/results/figures/a_metric_compare.png`: ảnh so sánh kết quả giữa các cấu hình.
- `Task1_A/results/figures/a_train_loss_compare.png`: ảnh diễn biến loss huấn luyện.
- `Task1_A/results/figures/a_val_loss_compare.png`: ảnh diễn biến loss xác thực.

Khi nào nên chạy lại Task 1A:

- Khi muốn tạo lại dữ liệu đầu vào
- Khi thay đổi cách chia dữ liệu
- Khi muốn huấn luyện lại từ đầu
- Khi muốn chạy lại phần đánh giá hoặc demo

### 6.2 Task 1B

Thư mục làm việc chính:

- `Task1B/notebooks/`
- `Task1B/results/`

Thứ tự chạy khuyến nghị:

1. `b1.ipynb`
2. `b2.ipynb`
3. `rl-dataset.ipynb`
4. `b2-rl.ipynb`
5. `metrics_1.ipynb`
6. `metrics_2.ipynb`
7. `demo_b1_b2_rl.ipynb`

Giải thích từng notebook:

- `b1.ipynb`: chạy cấu hình zero-shot.
- `b2.ipynb`: chạy cấu hình fine-tuning theo miền dữ liệu.
- `rl-dataset.ipynb`: chuẩn bị dữ liệu cho bước nâng cao dựa trên sở thích.
- `b2-rl.ipynb`: chạy bước nâng cao sau fine-tuning.
- `metrics_1.ipynb` và `metrics_2.ipynb`: tổng hợp độ đo và so sánh kết quả.
- `demo_b1_b2_rl.ipynb`: minh họa đầu ra của các cấu hình.

Đầu ra quan trọng sau khi chạy:

- `Task1B/results/b_metrc_compare.png`: ảnh tổng hợp so sánh kết quả.

Lưu ý khi chạy Task 1B:

- Đây là phần nặng nhất của dự án.
- Nên chạy trên Kaggle hoặc Colab có GPU.
- Nếu chỉ muốn xem kết quả cuối, có thể mở thẳng notebook tổng hợp độ đo và ảnh kết quả.

### 6.3 Task 2

Thư mục làm việc chính:

- `task-2/`

Thứ tự chạy khuyến nghị:

1. `discovery_domain.ipynb`
2. `metadata_g_vqa.ipynb`
3. `merge_metadata.ipynb`
4. `parse_to_json.ipynb`

Giải thích từng notebook:

- `discovery_domain.ipynb`: khảo sát miền dữ liệu và xác định hướng xử lý.
- `metadata_g_vqa.ipynb`: trích xuất, làm sạch, gán nhãn và chuẩn hóa câu hỏi.
- `merge_metadata.ipynb`: gộp và hoàn thiện metadata đã xử lý.
- `parse_to_json.ipynb`: chuẩn bị đầu ra ở dạng thuận tiện cho huấn luyện và đánh giá.

Task 2 dùng để làm gì:

- Chuẩn hóa dữ liệu VQA đa miền tiếng Việt
- Làm giàu metadata
- Chuẩn hóa câu hỏi
- Bổ sung dữ liệu cho các ảnh còn thiếu câu hỏi
- Tạo đầu ra sẵn sàng cho các thí nghiệm tiếp theo

Lưu ý khi chạy Task 2:

- Một số bước có thể chạy lâu
- Một số bước cần GPU
- Đây là pipeline nhiều công đoạn, nên nên chạy tuần tự từ trên xuống

## 7. Thống kê dữ liệu chính

Thống kê từ `Task1_A/processed/report.json`:

| Tập dữ liệu | Số bộ hỏi đáp | Số ảnh |
| --- | ---: | ---: |
| Train | 2075 | 308 |
| Validation | 273 | 39 |
| Test | 260 | 39 |
| Tổng | 2608 | 386 |

Phân bố nhóm câu hỏi:

| Nhóm câu hỏi | Train | Validation | Test |
| --- | ---: | ---: | ---: |
| Identity | 403 | 53 | 52 |
| Attribute | 425 | 53 | 51 |
| Yes/No | 420 | 56 | 52 |
| Counting | 390 | 51 | 50 |
| Spatial | 437 | 60 | 55 |

## 8. Kết quả chính

### 8.1 Kết quả Task 1A

Từ `Task1_A/results/a_compare.csv`:
=======
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
>>>>>>> e0569915b30e7358c107c7c00b62012c812b5f11

| Cấu hình | Exact Match | BLEU | ROUGE-L | METEOR | BERTScore F1 | Gemini Judge |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| A1 | 0.3692 | 0.2959 | 0.7008 | 0.5003 | 0.7697 | 0.5500 |
| A2 | 0.3000 | 0.2297 | 0.6572 | 0.4469 | 0.7407 | 0.4950 |
<<<<<<< HEAD

### 8.2 Kết quả Task 1B

Ảnh tổng hợp kết quả:

- `Task1B/results/b_metrc_compare.png`

### 8.3 Hình kiến trúc và hình báo cáo

Các hình đã chuẩn bị cho báo cáo nằm trong:

- `report_assets/architecture_png/`
- `report_assets/mermaid/`

## 9. Tài nguyên ngoài repo

Các liên kết chính trong `link.txt`:

- Video demo: [Google Drive](https://drive.google.com/drive/folders/12ctRytK7-cbamtFsxwbOyBM7KkNpeMRi?usp=sharing)
- Notebook B2: [Kaggle](https://www.kaggle.com/code/spixalo/dl-endterm-b2-vnts)
- Notebook B2 RL: [Kaggle](https://www.kaggle.com/code/spixalo/dl-endterm-b2-rl)
- Notebook tổng hợp metrics: [Kaggle](https://www.kaggle.com/code/spixalo/dl-endterm-b-allmetrics)
- Dataset cho Task 2: [Hugging Face](https://huggingface.co/datasets/tung213/vietnamese-vqa_merged)
- Checkpoint cho Task 1A: [Hugging Face](https://huggingface.co/VHT-2012/gVQA-transformer)

## 10. Nếu chỉ muốn xem nhanh dự án

Nếu bạn không muốn chạy toàn bộ từ đầu, có thể xem theo thứ tự ngắn sau:

1. Đọc README này
2. Xem `Task1_A/processed/report.json`
3. Xem `Task1_A/results/a_compare.csv`
4. Xem `Task1_A/results/figures/`
5. Xem `Task1B/results/b_metrc_compare.png`
6. Xem `report_assets/` để lấy hình cho báo cáo
7. Mở `link.txt` để đi tới video và notebook ngoài

## 11. Gợi ý xử lý lỗi thường gặp

Nếu notebook không chạy:

- Kiểm tra đã bật GPU chưa
- Kiểm tra đã cài đủ phụ thuộc chưa
- Kiểm tra dữ liệu đầu vào đã có đúng thư mục chưa
- Kiểm tra notebook trước đó trong chuỗi đã chạy xong chưa

Nếu chỉ muốn demo:

- Với Task 1A, mở `05_demo.ipynb`
- Với Task 1B, mở `demo_b1_b2_rl.ipynb`

Nếu chỉ muốn lấy số liệu cho báo cáo:

- Dùng `Task1_A/processed/report.json`
- Dùng `Task1_A/results/a_compare.csv`
- Dùng `Task1B/results/b_metrc_compare.png`

## 12. Tóm tắt ngắn

Repo này nên được hiểu theo ba luồng độc lập nhưng liên quan:

- `Task1_A/`: xây dựng, huấn luyện và đánh giá hướng A
- `Task1B/`: xây dựng, huấn luyện và đánh giá hướng B
- `task-2/`: chuẩn hóa và làm giàu dữ liệu đa miền

Nếu bạn là người mới, cách an toàn nhất là chạy từng phần theo đúng thứ tự notebook đã ghi trong README này.
=======
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
>>>>>>> e0569915b30e7358c107c7c00b62012c812b5f11

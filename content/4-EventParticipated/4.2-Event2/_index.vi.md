---
title: "Event 2"
date: "2025-09-10"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# TỔNG KẾT NỘI DUNG SỰ KIỆN AWS CLOUD MASTERY SERIES #1 (15/11/2025)

## PHẦN I: GENERATIVE AI VỚI AMAZON BEDROCK

### 1. Foundation Model và Prompt Engineering

Sự kiện đã đặt ra câu hỏi then chốt: **Nên học kiến thức gì để phù hợp với môi trường cloud bên ngoài?**

*   **Foundation Model:** Định nghĩa mô hình nền tảng.
*   **Prompt Engineering Techniques:** Các kỹ thuật để tối ưu hóa đầu vào cho mô hình AI.
    *   **Few-shot Prompting:** Cung cấp vài ví dụ cụ thể để hướng dẫn mô hình.
    *   **Chain of Thought (CoT):** Yêu cầu mô hình hiển thị các bước suy luận để đưa ra câu trả lời cuối cùng, giúp tăng độ chính xác.

### 2. Retrieval Augmented Generation (RAG)

Sự kiện đi sâu vào RAG và khái niệm Embedding.

*   **Embedding là gì?** (Khái niệm đã được giới thiệu).
*   **Các công cụ hỗ trợ RAG:**
    *   **Amazon Titan Embedding** (công cụ được giới thiệu).
*   **RAG in Action:** Minh họa sơ đồ hoạt động của RAG, bao gồm các bước:
    1.  **User Query**
    2.  **Embedding Model** (chuyển câu hỏi thành vector)
    3.  **Vector Store / Knowledge Source** (tìm kiếm thông tin liên quan)
    4.  **Prompt Template / Prompt Alignment Model** (chèn thông tin tìm được vào prompt)
    5.  **Large Language Model (LLM)**
    6.  **Response** (trả lời đã được bổ sung kiến thức ngoại vi).
*   **RetriveAndGenerate API:** Một API được giới thiệu để triển khai RAG.

### 3. Amazon Bedrock AgentCore

Amazon Bedrock AgentCore là nền tảng giúp hiện thực hóa ứng dụng AI của bạn bằng cách đưa các agent AI từ giai đoạn thử nghiệm lên production.

*   **Chức năng:** Hỗ trợ mạnh mẽ cho runtime, memory, công cụ, bảo mật, và giám sát cho các agent.

## PHẦN II: OTHER PRETRAINED AI SERVICE (Các dịch vụ AI được train sẵn)

Sự kiện cũng giới thiệu một loạt các dịch vụ AI chuyên biệt, đã được train sẵn của Amazon, cùng với chi phí tương ứng:

| Dịch vụ AI | Chức năng chính | Giá tham khảo |
| :--- | :--- | :--- |
| **Amazon Rekognition** | Phân tích hình ảnh, video, dán nhãn, tự động censor nội dung nhạy cảm. | $0,0013/ảnh (<1tr images) |
| **Amazon Translate** | Nhận diện và dịch văn bản real time. | $15/1tr kí tự |
| **Amazon Textract** | Extract texts và layouts từ tài liệu. | $0,05/page (<1tr pages) ⟹ cần cân nhắc. |
| **Amazon Transcribe** | Biến giọng nói thành kí tự. Hỗ trợ censor từ nhạy cảm, nhận diện giọng nói, và dịch tự động. | $0,024/phút (<250k phút) |
| **Amazon Polly** | Biến văn bản thành lời nói (text-to-speech). | 4$ mỗi 1tr kí tự (1tr đầu tiên miễn phí). |
| **Amazon Comprehend** | Xử lý ngôn ngữ tự nhiên (NLP). Đọc hiểu văn bản, video, lọc keyword. | $0,0001/100 kí tự + $0,35/1h |
| **Amazon Kendra** | Chức năng TÌM KIẾM (hay trả lời câu hỏi). | $30$/index/month + $0,35/1h (cực kỳ đắt) |
| **Amazon Personalize** | Cá nhân hóa trải nghiệm người dùng (như TikTok, Shopee, Facebook). | $0,24/training hour + $0,05/GB/recommendation |
| **Amazon Lookout Family** | Gồm Lookout for Equipment và Lookout for Vision (để giám sát và phát hiện bất thường). | (Không có giá cụ thể trong ghi chú) |
| **Pipecat** | (Được giới thiệu, không có chi tiết chức năng). | (Không có giá cụ thể trong ghi chú) |

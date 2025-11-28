---
title: "Event 1"
date: "2025-09-10"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# PHẦN I: GIỚI THIỆU VỀ KIRO.DEV (AGENTIC IDE CỦA AWS)

Kiro.dev (phát âm “keer-oh”) là một IDE (Integrated Development Environment) hỗ trợ AI dạng agent, được phát triển bởi một nhóm nhỏ thuộc Amazon Web Services (AWS). Nó hiện đang trong giai đoạn public preview (bản thử nghiệm công khai).

## 1. Mục Tiêu & Đặc Tính Nổi Bật

*   **Mục tiêu:** Lấp đầy khoảng cách giữa "vibe coding" (prototype nhanh) và phát triển phần mềm thực tế có cấu trúc, kiểm thử, tài liệu và khả năng bảo trì.
*   **Tính năng chính:**
    *   **TaSpec-Driven Development:** Chuyển yêu cầu thành user story, acceptance criteria, tài liệu thiết kế và danh sách tác vụ (task list).
    *   **Agent Hooks / Tự động hóa:** Tự động kích hoạt các tác vụ như tạo tài liệu, kiểm thử, tối ưu hóa khi có sự kiện (lưu file, commit).
    *   **Steering:** Sử dụng các tập tin Markdown để định nghĩa rõ ràng cấu trúc dự án, tiêu chuẩn và kiến trúc.
    *   **Khả năng làm việc đa file:** Hiểu rõ mục tiêu chức năng và thực hiện các thay đổi cần thiết trên nhiều file.

## 2. Ưu Điểm và Thách Thức

| Loại | Chi tiết |
| :--- | :--- |
| **Ưu điểm** | Tăng tính minh bạch & kiểm soát (kiểm tra đặc tả trước khi code), Giảm gánh nặng boilerplate, Bảo mật & quyền riêng tư (tạo mã diễn ra cục bộ), Linh hoạt (tích hợp công cụ ngoài qua Model Context Protocol). |
| **Hạn chế** | Còn trong giai đoạn preview (tính năng chưa hoàn thiện), có thể gặp khó khăn trong việc “hiểu ngữ cảnh” với các dự án phức tạp (cần người dùng giám sát), có chi phí cho agent interaction. |

## 3. Khuyến Nghị Sử Dụng

Kiro phù hợp nếu bạn muốn duy trì một workflow chuyên nghiệp, cấu trúc rõ ràng trong khi vẫn tận dụng AI để làm prototype nhanh, hoặc muốn AI trở thành “đồng nghiệp lập trình” chứ không chỉ là công cụ gợi ý code.

# PHẦN II: GHI CHÚ QUAN TRỌNG VỀ SỬ DỤNG AI HIỆU QUẢ

Đây là những kinh nghiệm và nguyên tắc cốt lõi khi làm việc với AI trong dự án phát triển phần mềm:

## 1. Nguyên Tắc Kiểm Soát

*   **Người dùng phải là người kiểm soát:** AI chỉ là trợ lý, không nên dựa dẫm vào nó để nó kiểm soát dự án.
*   **Tạo Plan Trước và Review Thường Xuyên:** PHẢI TẠO PLAN TRƯỚC (chẳng hạn, báo AI tạo file plan) để có khung sườn làm việc và phải thường xuyên review (đừng kỳ vọng nó làm hết).
*   **Vai trò người quản lý code:** Giá trị của bạn nằm ở phần validation code. Bạn phải là người quản lý được code do AI tạo ra.

## 2. Kỹ Thuật Prompt và Định Nghĩa Yêu Cầu

*   **Phải chỉ ra role cụ thể cho AI** (ví dụ: đề xuất dùng Amazon Q/CodeWhisperer).
*   **Viết prompt template của bạn:** Yêu cầu AI tạo plan, sau đó bạn lọc ra và sửa chữa, yêu cầu nó xuất file để lưu trữ và chỉnh sửa trực tiếp sau này.
*   **Define rõ ràng:**
    *   Nên tạo section mới khi viết user story.
    *   Define technology rõ ràng để AI follow theo.
    *   Thay vì nói "đừng implement cái này," nên nói "implement phần này" để tăng xác suất thành công.
*   **Hợp tác chi tiết:** Cùng AI kết hợp để tạo ra requirement rõ ràng và thông tin chi tiết trước khi nhờ AI thiết kế và trả lời tiếp.

## 3. Quản Lý Dự Án

*   **Chia nhỏ Scope:** Chia scope lớn thành scope unit; mỗi unit là một project nhỏ để dễ dàng triển khai (implementing).
*   **Hợp tác và Xác minh:** Yêu cầu AI viết user story, sau đó dựa vào đó để dự đoán thời gian dự án. Phải có team làm chung và verifile tất cả code out.
*   **Quy trình cơ bản:** requirement $\implies$ unit $\implies$ data model $\implies$ ... $\implies$ verifile.

# PHẦN III: SƠ ĐỒ QUY TRÌNH PHÁT TRIỂN PHẦN MỀM (AGILE/SCRUM)

Quy trình phát triển phần mềm thường đi theo hướng Agile/Scrum, với sự tham gia của các vai trò như Product Owner, Developer, và Tester.

## 1. Chu Kỳ Phát Triển

*   Bắt đầu từ **Backlog** (danh sách yêu cầu), các yêu cầu được sắp xếp và phân vào từng **Sprint**.
*   Trong mỗi Sprint, nhóm phát triển thực hiện các hoạt động chính: **Thiết kế (Design)**, **Lập trình (Code)**, và **Kiểm thử (Test)**.

## 2. Sản Phẩm Đầu Ra và Môi Trường Triển Khai

*   **Artifacts (Sản phẩm đầu ra):** Bản thiết kế, bản đồ nội dung, giao diện dịch vụ, mã nguồn, cấu hình.
*   **Môi trường triển khai:** Sản phẩm lần lượt được đưa qua các môi trường:
    *   **Development (Dev)**
    *   **Testing (QA)**
    *   **User Acceptance Testing (UAT)**
    *   **Production (Prod)** – môi trường chạy chính thức.

Quy trình này đảm bảo mối quan hệ giữa vai trò, hoạt động, kết quả và môi trường triển khai, giúp kiểm soát chất lượng sản phẩm trước khi phát hành cho người dùng.

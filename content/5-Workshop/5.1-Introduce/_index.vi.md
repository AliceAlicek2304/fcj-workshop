---
title : "Giới thiệu"
date : "2025-10-27"
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

#### Amazon Relational Database Service (Amazon RDS)

**ℹ️ Information**: Amazon Relational Database Service (Amazon RDS) giúp đơn giản hóa việc thiết lập, vận hành và mở rộng cơ sở dữ liệu quan hệ trên đám mây. Dịch vụ này cung cấp dung lượng có thể thay đổi với chi phí tối ưu, đồng thời tự động hóa các tác vụ quản trị tốn thời gian như cung cấp phần cứng, thiết lập cơ sở dữ liệu, vá lỗi và sao lưu.

![Create a VPC](/images/0001.png?featherlight=false&width=90pc)

#### Xử lý Giao dịch Trực tuyến (OLTP)

Amazon RDS được tối ưu hóa cho các khối lượng công việc Xử lý Giao dịch Trực tuyến (OLTP).

#### Trường hợp sử dụng chính

Dịch vụ này được thiết kế chủ yếu cho các ứng dụng giao dịch yêu cầu kho dữ liệu quan hệ có cấu trúc, thay vì các khối lượng công việc phân tích.

#### Thay thế trực tiếp (Drop-in Replacement)

RDS hoạt động như một sự thay thế liền mạch cho các instance cơ sở dữ liệu tại chỗ (on-premises) hiện có của bạn, cho phép bạn sử dụng cùng mã nguồn, ứng dụng và công cụ mà bạn đang dùng.

#### Các tính năng chính

- **Bảo trì tự động**: Sao lưu và vá lỗi phần mềm được xử lý tự động trong các khung giờ bảo trì do bạn xác định.
- **Khả năng mở rộng & Sẵn sàng**: Cung cấp khả năng mở rộng, sao chép và các tùy chọn tính sẵn sàng cao chỉ với vài thao tác.

#### Các công cụ cơ sở dữ liệu được hỗ trợ

Amazon RDS hỗ trợ sáu công cụ cơ sở dữ liệu phổ biến:

- Amazon Aurora
- MySQL
- MariaDB
- Oracle
- SQL Server
- PostgreSQL

#### Lợi ích của Dịch vụ được Quản lý

**ℹ️ Information**: Là một dịch vụ được quản lý, RDS hạn chế quyền truy cập vào EC2 instance bên dưới (không có quyền root) để đảm bảo tính ổn định và bảo mật.

**💡 Pro Tip**: Nếu bạn cần quyền truy cập vào hệ điều hành bên dưới, **Amazon RDS Custom** là lựa chọn khả dụng cho các công cụ Oracle và SQL Server.

Mô hình dịch vụ được quản lý bao gồm:

- **Bảo mật**: Tăng cường bảo mật và vá lỗi cho các DB instance.
- **Độ tin cậy**: Sao lưu tự động và sao chép đồng bộ đa vùng (Multi-AZ) để đảm bảo tính sẵn sàng cao.
- **Bảo trì**: Tự động cập nhật phần mềm cho công cụ DB.
- **Mở rộng**: Dễ dàng mở rộng theo chiều dọc (tính toán) và chiều ngang (read replicas).
- **Khả năng phục hồi**: Tự động chuyển đổi dự phòng (failover) trong cấu hình Multi-AZ.

#### DB Instance

Một DB instance là một môi trường cơ sở dữ liệu biệt lập trên đám mây. Bạn có thể định nghĩa các tài nguyên tính toán và lưu trữ mà nó sử dụng.

#### Truy cập qua Endpoints

Bạn kết nối với cơ sở dữ liệu của mình bằng các endpoint (điểm cuối). Các thông tin này có thể được tìm thấy trong phần chi tiết DB instance trên AWS Management Console, hoặc truy xuất qua API `DescribeDBInstances` hoặc lệnh CLI.

#### Giới hạn Instance

**⚠️ Warning**: Theo mặc định, bạn bị giới hạn tối đa 40 Amazon RDS DB instances cho mỗi tài khoản. Trong số đó, tối đa 10 instance có thể là Oracle hoặc SQL Server theo mô hình "License Included".

#### Khung giờ bảo trì (Maintenance Windows)

Khung giờ bảo trì cho phép bạn kiểm soát thời điểm diễn ra các sửa đổi DB (như mở rộng hoặc vá lỗi). Bạn có thể chỉ định một khung giờ hàng tuần, hoặc để AWS gán ngẫu nhiên một khung giờ 30 phút.

#### Xác thực tích hợp Windows

Đối với SQL Server, Xác thực tích hợp Windows chỉ được hỗ trợ khi sử dụng các miền AWS Directory Service. Bạn cần thiết lập mối quan hệ tin cậy với AD tại chỗ nếu cần.

#### Sự kiện và Thông báo

Amazon RDS sử dụng Amazon SNS để gửi thông báo về các sự kiện quan trọng của cơ sở dữ liệu.
- **API**: Sử dụng `DescribeEvents` để xem các sự kiện trong 14 ngày qua.
- **CLI**: Xem các sự kiện trong 14 ngày qua.
- **Console**: Chỉ xem được các sự kiện trong 1 ngày qua.

#### Trường hợp sử dụng, Thay thế và Anti-Patterns

Sử dụng bảng dưới đây để quyết định xem RDS có phải là lựa chọn phù hợp cho nhu cầu của bạn không:

| Kho dữ liệu       | Sử dụng tốt nhất khi...                                    |
|------------------|------------------------------------------------|
| **Database trên EC2**  | - Bạn cần kiểm soát hoàn toàn hệ điều hành và cấu hình DB.<br>- Công cụ DB ưa thích của bạn không được RDS hỗ trợ.       |
| **Amazon RDS**       | - Bạn cần một cơ sở dữ liệu quan hệ truyền thống cho OLTP.<br>- Dữ liệu có cấu trúc và định dạng tốt.<br>- Di chuyển các ứng dụng hiện có yêu cầu RDBMS. |
| **Amazon DynamoDB**  | - Dữ liệu phi cấu trúc (cặp tên/giá trị) hoặc không thể đoán trước.<br>- Bạn cần quy mô cực lớn và hiệu suất độ trễ thấp.<br>- Yêu cầu thông lượng I/O cao. |
| **Amazon RedShift**  | - Bạn có bộ dữ liệu khổng lồ để phân tích (OLAP).                    |
| **Amazon Neptune**   | - Giá trị dữ liệu được bắt nguồn từ mối quan hệ giữa các đối tượng (Graph DB). |
| **Amazon ElastiCache** | - Bạn cần bộ nhớ đệm nhanh (in-memory) cho dữ liệu truy cập thường xuyên. |
| **Amazon S3**        | - Lưu trữ các đối tượng nhị phân lớn (BLOBs) hoặc nội dung trang web tĩnh.                                        |

**Giải pháp thay thế cho Amazon RDS:**

Nếu RDS không đáp ứng các yêu cầu cụ thể của bạn, chạy cơ sở dữ liệu trên **Amazon EC2** là một giải pháp thay thế khả thi.

Cân nhắc EC2 nếu:
- Bạn cần sự linh hoạt và kiểm soát tối đa.
- Bạn sẵn sàng tự quản lý sao lưu, dự phòng, vá lỗi và mở rộng.
- Bạn sử dụng công cụ cơ sở dữ liệu chưa được RDS hỗ trợ (ví dụ: IBM DB2, SAP HANA).

**Anti-Patterns (Không nên dùng):**

Tránh sử dụng RDS cho các kịch bản sau:

| Yêu cầu                              | Giải pháp thay thế tốt hơn |
|------------------------------------------|------------------------|
| Lưu trữ nhiều đối tượng nhị phân lớn (BLOBs)     | Amazon S3                     |
| Khả năng mở rộng tự động vô hạn           | Amazon DynamoDB               |
| Dữ liệu phi cấu trúc / Tên-Giá trị           | Amazon DynamoDB               |
| Mối quan hệ đồ thị phức tạp              | Amazon Neptune            |
| Kiểm soát hoàn toàn OS/DB                   | Amazon EC2             |

#### Mã hóa

**🔒 Security Note**: Bạn có thể mã hóa các RDS instance và snapshot ở trạng thái nghỉ (at rest) bằng AWS KMS. Đây là thực hành tốt nhất cho dữ liệu nhạy cảm.

Mã hóa ở trạng thái nghỉ bao gồm:
- Lưu trữ DB instance
- Sao lưu tự động
- Read Replicas
- Snapshots

**⚠️ Warning**: Bạn không thể mã hóa trực tiếp một DB instance hiện có chưa được mã hóa. Bạn phải tạo snapshot, sao chép nó thành snapshot được mã hóa, và sau đó khôi phục một DB instance mới từ snapshot được mã hóa đó.

**Mã hóa SSL**: RDS hỗ trợ SSL để mã hóa dữ liệu đang truyền (in transit) giữa ứng dụng của bạn và cơ sở dữ liệu.

#### DB Subnet Groups

**ℹ️ Information**: Một **DB subnet group** xác định các subnet và dải IP mà RDS instance có thể sử dụng trong VPC của bạn.

**💡 Pro Tip**: Luôn bao gồm các subnet từ ít nhất **hai Availability Zones** trong subnet group của bạn để cho phép triển khai Multi-AZ.

#### Thanh toán và Cung cấp

**Bạn bị tính phí cho:**
- **Tính toán**: Giờ sử dụng DB instance (giờ lẻ được tính là giờ tròn).
- **Lưu trữ**: GB mỗi tháng.
- **I/O**: Số yêu cầu/tháng (Magnetic) hoặc Provisioned IOPS/tháng (SSD).
- **Truyền dữ liệu**: Truyền dữ liệu ra ngoài (Outbound).
- **Lưu trữ sao lưu**: Lưu trữ cho snapshot thủ công và sao lưu tự động (phần vượt quá dung lượng lưu trữ DB của bạn).

**Lưu ý**: Triển khai Multi-AZ phát sinh chi phí cho instance dự phòng, lưu trữ và I/O, nhưng truyền dữ liệu giữa instance chính và dự phòng là miễn phí.

**Reserved Instances (RI)**:
Bạn có thể mua Reserved Instances để được giảm giá đáng kể. RI gắn liền với các thuộc tính cụ thể:
- DB Engine
- Loại Instance
- Loại triển khai (Single-AZ hoặc Multi-AZ)
- Mô hình cấp phép
- Region

#### Khả năng mở rộng

**ℹ️ Information**: RDS hỗ trợ mở rộng theo chiều dọc (loại instance) và mở rộng lưu trữ.

- **Lưu trữ**: Có thể tăng dung lượng khi instance đang chạy (không có thời gian chết, có thể ảnh hưởng hiệu suất). Bạn không thể giảm dung lượng lưu trữ.
- **Tính toán**: Thay đổi loại instance yêu cầu khởi động lại ngắn (có thời gian chết).

**⚠️ Warning**: Dung lượng lưu trữ tối đa là 64 TiB cho hầu hết các engine, nhưng là 16 TiB cho SQL Server.

#### Hiệu năng

RDS sử dụng EBS volume để lưu trữ. Chọn loại phù hợp với khối lượng công việc của bạn:

1.  **General Purpose (SSD - gp2/gp3)**: Hiệu năng cân bằng cho hầu hết các tác vụ. Tiết kiệm chi phí.
2.  **Provisioned IOPS (SSD - io1/io2)**: Dành cho các tác vụ I/O cao, nhạy cảm với độ trễ. Bạn chỉ định chính xác số IOPS cần thiết.
3.  **Magnetic**: Lưu trữ cũ, không khuyến nghị cho các tác vụ mới.

#### Multi-AZ và Read Replicas

| Tính năng | Multi-AZ Deployments | Read Replicas |
| :--- | :--- | :--- |
| **Mục đích** | Tính sẵn sàng cao (HA) & Khôi phục sau thảm họa (DR) | Mở rộng khả năng đọc & Hiệu năng |
| **Sao chép** | Đồng bộ (Không mất dữ liệu) | Không đồng bộ (Nhất quán cuối cùng) |
| **Node hoạt động** | Chỉ Primary hoạt động | Tất cả replica đều hoạt động cho việc đọc |
| **Sao lưu** | Lấy từ Standby (không ảnh hưởng I/O trên Primary) | Không được cấu hình mặc định |
| **Failover** | Tự động | Cần thăng cấp thủ công |

#### Chi tiết về Multi-AZ

**ℹ️ Information**: Multi-AZ tạo một bản sao dự phòng (standby) trong một Availability Zone khác.

- **Tự động Failover**: Được kích hoạt khi có lỗi hạ tầng, mất mạng, hoặc lỗi instance.
- **Liền mạch**: DNS endpoint tự động cập nhật để trỏ đến bản standby.
- **Khuyến nghị**: Sử dụng Provisioned IOPS cho Multi-AZ để đảm bảo hiệu suất sao chép ổn định.

**💡 Pro Tip**: Luôn sử dụng DNS endpoint trong chuỗi kết nối ứng dụng của bạn, không bao giờ dùng địa chỉ IP, để đảm bảo failover hoạt động chính xác.

**⚠️ Warning**: Instance dự phòng trong thiết lập Multi-AZ không thể được sử dụng cho lưu lượng đọc.

#### Chi tiết về Read Replicas

**ℹ️ Information**: Giảm tải lưu lượng đọc từ instance chính sang Read Replicas.

- **Khả năng mở rộng**: Tối đa 5 read replica cho mỗi master.
- **Linh hoạt**: Có thể nằm trong cùng AZ, khác AZ, hoặc thậm chí khác Region (Cross-Region).
- **Thăng cấp**: Một Read Replica có thể được thăng cấp thủ công thành một master database độc lập.

**💡 Pro Tip**: Bạn có thể thăng cấp một Read Replica để trở thành master mới. Quá trình này mất vài phút.

#### DB Snapshots

**ℹ️ Information**: Sao lưu instance do người dùng khởi tạo.

- Được lưu trữ trên S3 vô thời hạn cho đến khi bạn xóa chúng.
- **Khôi phục**: Tạo ra một DB instance hoàn toàn mới với endpoint mới.
- **Chia sẻ**: Snapshot có thể được chia sẻ với các tài khoản AWS khác.

**💡 Pro Tip**: Luôn tạo một snapshot cuối cùng trước khi xóa một cơ sở dữ liệu sản xuất.

#### Giám sát

Sử dụng các công cụ này để giữ cho cơ sở dữ liệu của bạn khỏe mạnh:

- **Amazon CloudWatch**: Các chỉ số (CPU, bộ nhớ, disk I/O) và Cảnh báo.
- **Enhanced Monitoring**: Các chỉ số hệ điều hành thời gian thực.
- **Performance Insights**: Trực quan hóa tải cơ sở dữ liệu và giúp xác định các điểm nghẽn.
- **RDS Events**: Thông báo về các thay đổi cấu hình hoặc failover.

**💡 Pro Tip**: Kết hợp các công cụ này để có cái nhìn toàn diện về sức khỏe và hiệu suất của cơ sở dữ liệu.

---
title : "Workshop: Bắt đầu với Amazon RDS"
date : "2025-10-27"
weight : 5
chapter : false
pre: " <b> 5. </b> "
---
# Amazon Relational Database Service (Amazon RDS)

#### Tổng quan về Amazon RDS

\*\*ℹ️\ Information\*\*: Amazon Relational Database Service (Amazon RDS) là dịch vụ quản lý cho phép bạn triển khai và quản lý cơ sở dữ liệu quan hệ trên AWS. Amazon RDS được thiết kế cho xử lý giao dịch trực tuyến (OLTP) và phù hợp nhất với các yêu cầu lưu trữ dữ liệu có cấu trúc và quan hệ.

Amazon RDS cung cấp các lợi ích chính:
- Thay thế dễ dàng cho các instance cơ sở dữ liệu truyền thống
- Sao lưu tự động và vá lỗi trong khung giờ bảo trì do khách hàng xác định
- Mở rộng, sao chép và tính sẵn có chỉ với một nút nhấn

![Create a VPC](/images/1/0001.png?featherlight=false&width=90pc)

#### Hệ thống cơ sở dữ liệu được hỗ trợ

Amazon RDS hỗ trợ các hệ thống cơ sở dữ liệu sau:
- Amazon Aurora
- MySQL
- MariaDB
- Oracle
- SQL Server
- PostgreSQL

\*\*⚠️\ Warning\*\*: RDS là dịch vụ được quản lý và bạn không có quyền truy cập vào máy chủ EC2 cơ bản (không có quyền truy cập root). Ngoại lệ là **Amazon RDS Custom**, cho phép truy cập vào hệ điều hành cơ bản, nhưng chỉ có sẵn cho một số DB Engine giới hạn.

#### Tính năng quản lý của Amazon RDS

Dịch vụ quản lý Amazon RDS bao gồm:
- Bảo mật và vá lỗi cho DB instances
- Sao lưu tự động cho DB instances
- Cập nhật phần mềm cho DB engine
- Mở rộng dễ dàng cho lưu trữ và tính toán
- Tùy chọn Multi-AZ với sao chép đồng bộ
- Tự động chuyển giao cho tùy chọn Multi-AZ
- Tùy chọn Read Replicas cho tải công việc nặng về đọc

\*\*ℹ️\ Information\*\*: DB instance là môi trường cơ sở dữ liệu trong đám mây với tài nguyên tính toán và lưu trữ mà bạn chỉ định. DB instances được truy cập thông qua các điểm cuối (endpoints) có thể được truy xuất từ AWS Management Console, API DescribeDBInstances hoặc lệnh describe-db-instances.

**💡 Pro Tip**: Mặc định, khách hàng được phép có tối đa 40 DB instances Amazon RDS (chỉ có 10 trong số này có thể là Oracle hoặc MS SQL trừ khi bạn có giấy phép riêng).

#### Cửa sổ bảo trì và sự kiện

Cửa sổ bảo trì được cấu hình để cho phép thực hiện các sửa đổi DB instances như mở rộng và cài đặt phần mềm vá. Bạn có thể xác định cửa sổ bảo trì hoặc AWS sẽ lên lịch cho một cửa sổ 30 phút.

\*\*ℹ️\ Information\*\*: Xác thực tích hợp với Windows chỉ hoạt động với SQL khi sử dụng các miền được tạo bằng AWS Directory Service - cần thiết lập mối tin tưởng với thư mục AD trên nơi làm việc truyền thống.

#### Sự kiện và Thông báo

- Amazon RDS sử dụng AWS SNS để gửi sự kiện RDS qua thông báo SNS
- Bạn có thể sử dụng API DescribeEvents để liệt kê các sự kiện RDS trong 14 ngày qua
- Bạn có thể xem các sự kiện trong 14 ngày qua bằng dòng lệnh CLI
- Trong AWS Console, bạn chỉ có thể xem các sự kiện RDS trong 1 ngày qua

#### Khi nào sử dụng RDS và các dịch vụ thay thế

| Dịch vụ lưu trữ dữ liệu | Khi nào sử dụng |
|------------------------|-----------------|
| Cơ sở dữ liệu trên EC2 | Kiểm soát tối đa về cơ sở dữ liệu, ưa chuộng DB không có sẵn trên RDS |
| Amazon RDS | Cần cơ sở dữ liệu quan hệ truyền thống cho OLTP, dữ liệu có cấu trúc tốt, ứng dụng hiện có yêu cầu RDBMS |
| Amazon DynamoDB | Dữ liệu cặp tên/giá trị, cấu trúc không dự đoán được, hiệu suất trong bộ nhớ với tính bền vững, nhu cầu I/O cao |
| Amazon RedShift | Khối lượng lớn dữ liệu, chủ yếu là tải phân tích (OLAP) |
| Amazon Neptune | Mối quan hệ giữa các đối tượng là một phần quan trọng của giá trị dữ liệu |
| Amazon ElastiCache | Lưu trữ tạm thời nhanh cho lượng dữ liệu nhỏ, dữ liệu biến động cao |
| Amazon S3 | Đối tượng nhị phân lớn (BLOBs), các trang web tĩnh |

**💡 Pro Tip**: Nếu trường hợp sử dụng của bạn không được hỗ trợ trên RDS, bạn có thể chạy cơ sở dữ liệu trên Amazon EC2 với kiểm soát đầy đủ và tính linh hoạt tối đa, nhưng phải tự quản lý mọi thứ như sao lưu, dự phòng, cập nhật và mở rộng.

#### Anti-Patterns cho RDS

| Yêu cầu | Dịch vụ thích hợp hơn |
|---------|----------------------|
| Nhiều đối tượng nhị phân lớn (BLOBs) | Amazon S3 |
| Khả năng tự động mở rộng | Amazon DynamoDB |
| Cấu trúc dữ liệu tên/giá trị | Amazon DynamoDB |
| Dữ liệu không có cấu trúc hoặc không dự đoán được | Amazon DynamoDB |
| Các nền tảng cơ sở dữ liệu khác như IBM DB2 hoặc SAP HANA | Amazon EC2 |
| Kiểm soát hoàn toàn trên cơ sở dữ liệu | Amazon EC2 |

#### Mã hóa trong Amazon RDS

**🔒 Security Note**: Bạn có thể mã hóa các DB instances và bản chụp Amazon RDS khi nghỉ bằng cách bật tùy chọn mã hóa. Mã hóa khi nghỉ được hỗ trợ cho tất cả các loại DB và sử dụng AWS KMS.

Khi sử dụng mã hóa khi nghỉ, các yếu tố sau cũng được mã hóa:
- Tất cả bản chụp DB
- Sao lưu
- Lưu trữ instance DB
- Read Replicas

\*\*⚠️\ Warning\*\*: Bạn không thể mã hóa một DB hiện có. Bạn cần tạo một bản chụp, sao chép nó, mã hóa bản sao, sau đó xây dựng một DB đã được mã hóa từ bản chụp.

\*\*ℹ️\ Information\*\*: RDS hỗ trợ mã hóa SSL giữa các ứng dụng và DB instances RDS. RDS tạo chứng chỉ cho instance.

#### Nhóm DB Subnet

Nhóm DB Subnet là tập hợp các subnet (thường là riêng tư) mà bạn tạo trong VPC và chỉ định cho DB instances.

**💡 Pro Tip**: Mỗi nhóm DB Subnet nên có các subnet trong ít nhất hai AZ. Khuyến nghị cấu hình nhóm subnet với các subnet trong mỗi AZ (ngay cả cho các instance độc lập).

Trong quá trình tạo instance RDS, bạn chọn nhóm DB Subnet và AZ để đặt instance RDS DB. Bạn không thể chọn địa chỉ IP trong subnet được cấp.

#### Thanh toán và cung cấp

AWS tính phí cho:
- Giờ instance DB (làm tròn lên giờ đầy đủ)
- Lưu trữ GB/tháng
- Yêu cầu I/O/tháng (cho lưu trữ từ tính)
- Provisioned IOPS/tháng (cho RDS SSD IOPS được cung cấp)
- Truyền dữ liệu ra ngoài
- Lưu trữ sao lưu (sao lưu DB và bản chụp thủ công)

\*\*ℹ️\ Information\*\*: Lưu trữ sao lưu cho sao lưu tự động RDS miễn phí đến kích thước ổ EBS đã cung cấp. Tuy nhiên, AWS sao chép dữ liệu qua nhiều AZ nên bạn phải trả tiền cho không gian lưu trữ thêm trên S3.

Đối với Multi-AZ, bạn phải trả tiền cho:
- Giờ DB Multi-AZ
- Lưu trữ được cung cấp
- Ghi I/O hai lần

**💡 Pro Tip**: Đối với Multi-AZ, bạn không phải trả phí cho truyền dữ liệu DB trong quá trình sao chép từ instance chính sang trạng thái đứng.

Giấy phép Oracle và Microsoft SQL được bao gồm, hoặc bạn có thể tự mang (BYO). Giá ứng dụng dự phòng và giá ứng dụng dự phòng có sẵn.

#### Khả năng mở rộng

\*\*⚠️\ Warning\*\*: Bạn chỉ có thể mở rộng RDS lên (tính toán và lưu trữ). Bạn không thể giảm lưu trữ đã cấp cho instance RDS.

Bạn có thể mở rộng lưu trữ và thay đổi loại lưu trữ cho tất cả các DB engine ngoại trừ MS SQL. Đối với MS SQL, giải pháp tạm thời là tạo instance mới từ bản chụp với cấu hình mới.

\*\*ℹ️\ Information\*\*: Việc mở rộng lưu trữ có thể xảy ra trong khi instance RDS đang chạy mà không gây sự cố, tuy nhiên có thể có sự suy giảm hiệu suất. Việc mở rộng tính toán sẽ gây thời gian ngừng hoạt động.

Tất cả các loại DB RDS hỗ trợ kích thước DB tối đa là 64 TiB ngoại trừ Microsoft SQL Server (16 TiB).

#### Hiệu năng

Amazon RDS sử dụng ổ đĩa EBS (không sử dụng lưu trữ instance) cho lưu trữ DB và log. Có ba loại lưu trữ:

**Mục đích chung (SSD - gp2)**:
- Cho tải công việc cơ sở dữ liệu có nhu cầu I/O trung bình
- Hiệu quả về chi phí
- 3 IOPS/GB
- Burst lên đến 3000 IOPS

**Provisioned IOPS (SSD)**:
- Cho công việc có yêu cầu I/O cao
- Độ trễ thấp và I/O đều đặn
- Số IOPS được chỉ định bởi người dùng

| DB Engine | Phạm vi IOPS được cấp | Phạm vi kích thước lưu trữ |
|-----------|----------------------|----------------------------|
| MariaDB | 1.000-80.000 IOPS | 100 GiB-64TiB |
| SQL Server | 1.000-64.000 IOPS | 20 GiB-16TiB |
| MySQL | 1.000-80.000 IOPS | 100 GiB-64TiB |
| Oracle | 1.000-256.000 IOPS | 100 GiB-64TiB |
| PostgreSQL | 1.000-80.000 IOPS | 100 GiB-64TiB |

**Từ tính (Magnetic)**:
- Không còn được khuyến nghị, có sẵn cho tích hợp ngược
- Không cho phép mở rộng lưu trữ khi sử dụng SQL Server
- Không hỗ trợ ổ đĩa co giãn
- Giới hạn tối đa 4 TiB
- Giới hạn tối đa 1.000 IOPS

#### Multi-AZ và Read Replicas

Multi-AZ và Read Replicas được sử dụng để đảm bảo tính sẵn có cao, khả năng chịu lỗi và mở rộng hiệu suất.

| Multi-AZ Deployments | Read Replicas |
|----------------------|---------------|
| Sao chép đồng bộ - bền vững cao | Sao chép không đồng bộ - mở rộng cao |
| Chỉ có DB trên primary instance hoạt động | Tất cả read replicas đều truy cập được và dùng để mở rộng đọc |
| Sao lưu tự động từ standby | Không có sao lưu được cấu hình mặc định |
| Luôn bao gồm hai vùng khả dụng trong một Region | Có thể nằm trong một AZ, Cross-AZ hoặc Cross-Region |
| DB instances được nâng cấp trên primary | Nâng cấp DB instances độc lập với instance nguồn |
| Tự động chuyển đổi sang standby khi phát hiện sự cố | Có thể được thăng cấp thủ công thành DB instance độc lập |

#### Multi-AZ

\*\*ℹ️\ Information\*\*: Multi-AZ RDS tạo bản sao ở AZ khác và sao chép đồng bộ đến đó (chỉ dành cho DR). AWS khuyên sử dụng lưu trữ provisioned IOPS cho DB instances RDS Multi-AZ.

Mỗi AZ chạy trên cơ sở hạ tầng riêng biệt, độc lập về vật lý và được thiết kế để đảm bảo tính tin cậy cao. Bạn không thể chọn AZ nào sẽ được chọn cho bản sao DB dự phòng.

Failover có thể được kích hoạt trong các trường hợp:
- Mất AZ chính hoặc lỗi trạng thái DB chính
- Mất kết nối mạng với DB chính
- Lỗi đơn vị tính toán (EC2) trên DB chính
- Lỗi đơn vị lưu trữ (EBS) trên DB chính
- Thay đổi DB chính
- Cập nhật hệ điều hành trên DB chính
- Failover thủ công (khởi động lại với lựa chọn failover)

**💡 Pro Tip**: Trong quá trình failover, RDS tự động cập nhật cấu hình (bao gồm điểm cuối DNS) để sử dụng nút thứ hai. Tùy thuộc vào lớp instance, có thể mất từ 1 đến vài phút để failover. Nên triển khai việc thử lại kết nối DB trong ứng dụng và sử dụng điểm cuối thay vì địa chỉ IP.

\*\*⚠️\ Warning\*\*: Bản sao DB thứ cấp trong cấu hình Multi-AZ không thể được sử dụng như nút đọc độc lập. Không tính phí cho việc truyền dữ liệu giữa các instance RDS chính và dự phòng.

Các nâng cấp hệ thống (cập nhật hệ điều hành, thay đổi kích thước DB Instance) được áp dụng trước tiên trên replicas trước khi failover và sửa đổi DB Instance khác. Trong cấu hình Multi-AZ, các bản snapshot và sao lưu tự động được thực hiện trên replicas để tránh tạm dừng I/O trên DB instance chính.

#### Hỗ trợ Read Replicas cho Multi-AZ

\*\*ℹ️\ Information\*\*: Amazon RDS Read Replicas cho MySQL, MariaDB, PostgreSQL và Oracle hỗ trợ triển khai Multi-AZ. Kết hợp Read Replicas với Multi-AZ cho phép xây dựng chiến lược phục hồi thảm họa chắc chắn và đơn giản hóa quá trình nâng cấp DB engine.

Read snapshot ở AZ khác so với DB nguồn có thể được sử dụng như DB dự phòng và được thúc đẩy trở thành DB sản xuất mới khi có sự cố vùng. Điều này cho phép mở rộng khả năng đọc đồng thời cũng như có Multi-AZ cho DR.

#### Quy trình thực hiện bảo trì

1. Thực hiện các hoạt động trên replicas
2. Thúc đẩy replicas trở thành primary
3. Thực hiện các hoạt động trên replicas mới (primary bị hạ cấp)

\*\*ℹ️\ Information\*\*: Bạn có thể nâng cấp thủ công DB instance lên phiên bản DB engine mới từ AWS Console. Mặc định, nâng cấp có hiệu lực trong cửa sổ bảo trì tiếp theo, nhưng có thể buộc nâng cấp ngay lập tức.

\*\*⚠️\ Warning\*\*: Trong triển khai Multi-AZ, nâng cấp phiên bản được thực hiện trên cả primary và replicas cùng lúc, gây sự cố cho cả hai DB Instance. Đảm bảo SG và NACL cho phép máy chủ ứng dụng giao tiếp với cả primary và replicas.

#### Read Replicas

\*\*ℹ️\ Information\*\*: Read Replicas được sử dụng cho DB có tải đọc nhiều và sao chép không đồng bộ. Chúng giúp chia sẻ và giảm tải công việc, cung cấp khả năng khôi phục dữ liệu ở chế độ chỉ đọc.

Read Replicas được tạo từ snapshot của bản chính. Phải bật tính năng sao lưu tự động trên bản chính (thời gian lưu trữ > 0). Chỉ được hỗ trợ cho các DB engine lưu trữ giao dịch (InnoDB).

Read Replicas có sẵn cho MySQL, PostgreSQL, MariaDB, Oracle, Aurora và SQL Server. Đối với MySQL, MariaDB, PostgreSQL và Oracle, Amazon RDS tạo bản thứ hai từ snapshot của bản chính, sau đó sử dụng sao chép không đồng bộ tự nhiên để cập nhật Read Replicas.

**💡 Pro Tip**: Bạn có thể có tối đa 5 Read Replicas của một DB sản xuất. Bạn không thể có nhiều hơn bốn bản sao trong chuỗi sao chép. Bạn có thể có Read Replicas của Read Replicas cho MySQL và MariaDB nhưng không cho PostgreSQL.

Cấu hình Read Replicas có thể thiết lập từ Giao diện AWS hoặc API. Bạn có thể chỉ định region của Read Replicas. Loại lưu trữ và lớp bản chính có thể khác với nguồn, nhưng tính toán phải ít nhất bằng hiệu suất của nguồn.

\*\*⚠️\ Warning\*\*: Trong trường hợp mất kết nối đa region, các Read Replicas được chuyển sang bản chính mới. Read Replicas phải được xóa một cách tường tận. Nếu bản chính bị xóa mà không xóa các bản sao, mỗi bản sao trở thành bản chính độc lập tại một region.

Bạn có thể thăng cấp Read Replicas thành bản chính (mất vài phút). Read Replicas được thăng cấp giữ lại thời gian lưu trữ sao lưu, cửa sổ sao lưu, nhóm tham số DB, và các Read Replicas hiện có vẫn hoạt động bình thường.

Mỗi Read Replica có điểm cuối DNS riêng. Read Replicas có thể bật đa region và bạn có thể tạo Read Replicas từ DB nguồn đa region. Cấu hình này có thể tập trung dữ liệu từ các region khác nhau cho phân tích.

#### DB Snapshots

\*\*ℹ️\ Information\*\*: DB Snapshots là tình huống do người dùng khởi tạo, cho phép sao lưu DB instance ở trạng thái xác định và khôi phục về trạng thái đó. Không thể dùng để khôi phục tại điểm thời gian cụ thể.

Snapshots được lưu trữ trên S3 và tồn tại cho đến khi bị xóa thủ công. Sao lưu được thực hiện trong khoảng thời gian đã định. I/O tạm ngừng trong thời gian sao lưu và có thể tăng độ trễ (áp dụng cho RDS chỉ có một vùng).

**💡 Pro Tip**: DB Snapshots thủ công được lưu trữ ngay cả sau khi DB instance RDS bị xóa. DB được khôi phục luôn là DB instance RDS mới với điểm cuối DNS mới. Có thể khôi phục lên đến 5 phút trước.

\*\*⚠️\ Warning\*\*: Chỉ có tham số DB mặc định và nhóm bảo mật được khôi phục - phải liên kết tham số DB và SG khác thủ công. Nên chụp Snapshot cuối cùng trước khi xóa DB instance RDS.

Snapshot có thể chia sẻ với các tài khoản AWS khác.

#### Phương pháp sẵn có cho tính sẵn có cao

**💡 Pro Tip**: Thứ tự ưu tiên cho tính sẵn có cao:
1. Nếu có thể, chọn DynamoDB thay vì RDS vì tính chịu lỗi tích hợp
2. Nếu không thể dùng DynamoDB, chọn Aurora vì tính dự phòng và khôi phục tự động
3. Nếu không thể dùng Aurora, chọn Multi-AZ RDS

Sao lưu RDS thường xuyên bảo vệ trước sự hỏng dữ liệu và không ảnh hưởng hiệu suất triển khai Multi-AZ. Sao lưu dự phòng region cũng là lựa chọn nhưng không đảm bảo nhất quán mạnh mẽ.

\*\*⚠️\ Warning\*\*: Nếu cơ sở dữ liệu chạy trên EC2, bạn phải tự thiết kế tính sẵn có.

#### Di chuyển dữ liệu

\*\*ℹ️\ Information\*\*: AWS Database Migration Service (DMS) giúp di chuyển cơ sở dữ liệu vào AWS nhanh chóng và an toàn. Sử dụng kèm với Schema Conversion Tool (SCT) để di chuyển cơ sở dữ liệu vào RDS hoặc cơ sở dữ liệu dựa trên EC2.

Cơ sở dữ liệu nguồn vẫn hoạt động trong quá trình di chuyển, giảm thiểu thời gian chết cho ứng dụng. DMS có thể di chuyển dữ liệu tới và từ hầu hết cơ sở dữ liệu thương mại và nguồn mở phổ biến.

SCT có thể sao chép schema cho di chuyển đồng nhất (cùng loại DB) và chuyển đổi schema cho di chuyển không đồng nhất (khác loại DB). DMS dùng cho chuyển đổi nhỏ hơn, đơn giản hơn và hỗ trợ MongoDB và DynamoDB. SCT dùng cho bộ dữ liệu lớn hơn, phức tạp hơn như kho dữ liệu.

DMS có chức năng sao chép từ nơi trên cơ sở vào AWS hoặc vào Snowball hoặc S3.

#### Theo dõi, Ghi log và Báo cáo

Công cụ theo dõi tự động cho Amazon RDS:

- **Sự kiện Amazon RDS**: Đăng ký sự kiện để được thông báo khi có thay đổi với DB instance, snapshot, nhóm tham số hoặc nhóm bảo mật
- **Tệp ghi cơ sở dữ liệu**: Xem, tải xuống hoặc xem tệp ghi bằng giao diện hoặc API RDS
- **Enhanced Monitoring**: Xem số liệu thời gian thực cho hệ điều hành
- **Performance Insights**: Đánh giá tải trên cơ sở dữ liệu và xác định khi nào cần thực hiện
- **RDS Recommendations**: Xem khuyến nghị tự động cho tài nguyên cơ sở dữ liệu

Amazon RDS tích hợp với:

- **CloudWatch Metrics**: RDS tự động gửi số liệu đến CloudWatch mỗi phút
- **CloudWatch Alarms**: Theo dõi số liệu RDS và thực hiện hành động dựa trên ngưỡng
- **CloudWatch Logs**: Theo dõi, lưu trữ và truy cập tệp ghi DB
- **CloudWatch Events và EventBridge**: Tự động hóa dịch vụ AWS và phản ứng với sự kiện hệ thống
- **AWS CloudTrail**: Xem hồ sơ hành động được thực hiện bởi người dùng, vai trò hoặc dịch vụ AWS trong RDS


---
title : "Giá»›i thiá»‡u"
date : "2025-10-27"
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---
#### Amazon Relational Database Service (Amazon RDS)

\*\*ℹ️\ Information\*\*: Amazon Relational Database Service (Amazon RDS) lÃ  dá»‹ch vá»¥ quáº£n lÃ½ cho phÃ©p báº¡n triá»ƒn khai vÃ  quáº£n lÃ½ cÆ¡ sá»Ÿ dá»¯ liá»‡u quan há»‡ trÃªn AWS. Amazon RDS Ä‘Æ°á»£c thiáº¿t káº¿ cho xá»­ lÃ½ giao dá»‹ch trá»±c tuyáº¿n (OLTP) vÃ  phÃ¹ há»£p nháº¥t vá»›i cÃ¡c yÃªu cáº§u lÆ°u trá»¯ dá»¯ liá»‡u cÃ³ cáº¥u trÃºc vÃ  quan há»‡.

Amazon RDS cung cáº¥p cÃ¡c lá»£i Ã­ch chÃ­nh:
- Thay tháº¿ dá»… dÃ ng cho cÃ¡c instance cÆ¡ sá»Ÿ dá»¯ liá»‡u truyá»n thá»‘ng
- Sao lÆ°u tá»± Ä‘á»™ng vÃ  vÃ¡ lá»—i trong khung giá» báº£o trÃ¬ do khÃ¡ch hÃ ng xÃ¡c Ä‘á»‹nh
- Má»Ÿ rá»™ng, sao chÃ©p vÃ  tÃ­nh sáºµn cÃ³ chá»‰ vá»›i má»™t nÃºt nháº¥n

![Create a VPC](/images/0001.png?featherlight=false&width=90pc)

#### Há»‡ thá»‘ng cÆ¡ sá»Ÿ dá»¯ liá»‡u Ä‘Æ°á»£c há»— trá»£

Amazon RDS há»— trá»£ cÃ¡c há»‡ thá»‘ng cÆ¡ sá»Ÿ dá»¯ liá»‡u sau:
- Amazon Aurora
- MySQL
- MariaDB
- Oracle
- SQL Server
- PostgreSQL

\*\*⚠️\ Warning\*\*: RDS lÃ  dá»‹ch vá»¥ Ä‘Æ°á»£c quáº£n lÃ½ vÃ  báº¡n khÃ´ng cÃ³ quyá»n truy cáº­p vÃ o mÃ¡y chá»§ EC2 cÆ¡ báº£n (khÃ´ng cÃ³ quyá»n truy cáº­p root). Ngoáº¡i lá»‡ lÃ  **Amazon RDS Custom**, cho phÃ©p truy cáº­p vÃ o há»‡ Ä‘iá»u hÃ nh cÆ¡ báº£n, nhÆ°ng chá»‰ cÃ³ sáºµn cho má»™t sá»‘ DB Engine giá»›i háº¡n.

#### TÃ­nh nÄƒng quáº£n lÃ½ cá»§a Amazon RDS

Dá»‹ch vá»¥ quáº£n lÃ½ Amazon RDS bao gá»“m:
- Báº£o máº­t vÃ  vÃ¡ lá»—i cho DB instances
- Sao lÆ°u tá»± Ä‘á»™ng cho DB instances
- Cáº­p nháº­t pháº§n má»m cho DB engine
- Má»Ÿ rá»™ng dá»… dÃ ng cho lÆ°u trá»¯ vÃ  tÃ­nh toÃ¡n
- TÃ¹y chá»n Multi-AZ vá»›i sao chÃ©p Ä‘á»“ng bá»™
- Tá»± Ä‘á»™ng chuyá»ƒn giao cho tÃ¹y chá»n Multi-AZ
- TÃ¹y chá»n Read Replicas cho táº£i cÃ´ng viá»‡c náº·ng vá» Ä‘á»c

\*\*ℹ️\ Information\*\*: DB instance lÃ  mÃ´i trÆ°á»ng cÆ¡ sá»Ÿ dá»¯ liá»‡u trong Ä‘Ã¡m mÃ¢y vá»›i tÃ i nguyÃªn tÃ­nh toÃ¡n vÃ  lÆ°u trá»¯ mÃ  báº¡n chá»‰ Ä‘á»‹nh. DB instances Ä‘Æ°á»£c truy cáº­p thÃ´ng qua cÃ¡c Ä‘iá»ƒm cuá»‘i (endpoints) cÃ³ thá»ƒ Ä‘Æ°á»£c truy xuáº¥t tá»« AWS Management Console, API DescribeDBInstances hoáº·c lá»‡nh describe-db-instances.

**ðŸ’¡ Pro Tip**: Máº·c Ä‘á»‹nh, khÃ¡ch hÃ ng Ä‘Æ°á»£c phÃ©p cÃ³ tá»‘i Ä‘a 40 DB instances Amazon RDS (chá»‰ cÃ³ 10 trong sá»‘ nÃ y cÃ³ thá»ƒ lÃ  Oracle hoáº·c SQL Server trá»« khi báº¡n cÃ³ giáº¥y phÃ©p riÃªng).

#### Cá»­a sá»• báº£o trÃ¬ vÃ  sá»± kiá»‡n

Cá»­a sá»• báº£o trÃ¬ Ä‘Æ°á»£c cáº¥u hÃ¬nh Ä‘á»ƒ cho phÃ©p thá»±c hiá»‡n cÃ¡c sá»­a Ä‘á»•i DB instances nhÆ° má»Ÿ rá»™ng vÃ  cÃ i Ä‘áº·t pháº§n má»m vÃ¡. Báº¡n cÃ³ thá»ƒ xÃ¡c Ä‘á»‹nh cá»­a sá»• báº£o trÃ¬ hoáº·c AWS sáº½ lÃªn lá»‹ch cho má»™t cá»­a sá»• 30 phÃºt.

\*\*ℹ️\ Information\*\*: XÃ¡c thá»±c tÃ­ch há»£p vá»›i Windows chá»‰ hoáº¡t Ä‘á»™ng vá»›i SQL Server khi sá»­ dá»¥ng cÃ¡c miá»n Ä‘Æ°á»£c táº¡o báº±ng AWS Directory Service - cáº§n thiáº¿t láº­p má»‘i tin tÆ°á»Ÿng vá»›i thÆ° má»¥c AD trÃªn mÃ´i trÆ°á»ng truyá»n thá»‘ng.

#### Sá»± kiá»‡n vÃ  ThÃ´ng bÃ¡o

- Amazon RDS sá»­ dá»¥ng AWS SNS Ä‘á»ƒ gá»­i sá»± kiá»‡n RDS qua thÃ´ng bÃ¡o SNS
- Báº¡n cÃ³ thá»ƒ sá»­ dá»¥ng API DescribeEvents Ä‘á»ƒ liá»‡t kÃª cÃ¡c sá»± kiá»‡n RDS trong 14 ngÃ y qua
- Báº¡n cÃ³ thá»ƒ xem cÃ¡c sá»± kiá»‡n trong 14 ngÃ y qua báº±ng dÃ²ng lá»‡nh CLI
- Trong AWS Console, báº¡n chá»‰ cÃ³ thá»ƒ xem cÃ¡c sá»± kiá»‡n RDS trong 1 ngÃ y qua

#### Khi nÃ o sá»­ dá»¥ng RDS vÃ  cÃ¡c dá»‹ch vá»¥ thay tháº¿

| Dá»‹ch vá»¥ lÆ°u trá»¯ dá»¯ liá»‡u | Khi nÃ o sá»­ dá»¥ng |
|------------------------|-----------------|
| CÆ¡ sá»Ÿ dá»¯ liá»‡u trÃªn EC2 | Kiá»ƒm soÃ¡t tá»‘i Ä‘a vá» cÆ¡ sá»Ÿ dá»¯ liá»‡u, Æ°a chuá»™ng DB khÃ´ng cÃ³ sáºµn trÃªn RDS |
| Amazon RDS | Cáº§n cÆ¡ sá»Ÿ dá»¯ liá»‡u quan há»‡ truyá»n thá»‘ng cho OLTP, dá»¯ liá»‡u cÃ³ cáº¥u trÃºc tá»‘t, á»©ng dá»¥ng hiá»‡n cÃ³ yÃªu cáº§u RDBMS |
| Amazon DynamoDB | Dá»¯ liá»‡u cáº·p tÃªn/giÃ¡ trá»‹, cáº¥u trÃºc khÃ´ng dá»± Ä‘oÃ¡n Ä‘Æ°á»£c, hiá»‡u suáº¥t trong bá»™ nhá»› vá»›i tÃ­nh bá»n vá»¯ng, nhu cáº§u I/O cao |
| Amazon Redshift | Khá»‘i lÆ°á»£ng lá»›n dá»¯ liá»‡u, chá»§ yáº¿u lÃ  táº£i phÃ¢n tÃ­ch (OLAP) |
| Amazon Neptune | Má»‘i quan há»‡ giá»¯a cÃ¡c Ä‘á»‘i tÆ°á»£ng lÃ  má»™t pháº§n quan trá»ng cá»§a giÃ¡ trá»‹ dá»¯ liá»‡u |
| Amazon ElastiCache | LÆ°u trá»¯ táº¡m thá»i nhanh cho lÆ°á»£ng dá»¯ liá»‡u nhá», dá»¯ liá»‡u biáº¿n Ä‘á»™ng cao |
| Amazon S3 | Äá»‘i tÆ°á»£ng nhá»‹ phÃ¢n lá»›n (BLOBs), cÃ¡c trang web tÄ©nh |

**ðŸ’¡ Pro Tip**: Náº¿u trÆ°á»ng há»£p sá»­ dá»¥ng cá»§a báº¡n khÃ´ng Ä‘Æ°á»£c há»— trá»£ trÃªn RDS, báº¡n cÃ³ thá»ƒ cháº¡y cÆ¡ sá»Ÿ dá»¯ liá»‡u trÃªn Amazon EC2 vá»›i kiá»ƒm soÃ¡t Ä‘áº§y Ä‘á»§ vÃ  tÃ­nh linh hoáº¡t tá»‘i Ä‘a, nhÆ°ng pháº£i tá»± quáº£n lÃ½ má»i thá»© nhÆ° sao lÆ°u, dá»± phÃ²ng, cáº­p nháº­t vÃ  má»Ÿ rá»™ng.

#### MÃ£ hÃ³a vÃ  báº£o máº­t

**ðŸ”’ Security Note**: Báº¡n cÃ³ thá»ƒ mÃ£ hÃ³a cÃ¡c DB instances vÃ  báº£n snapshot Amazon RDS khi nghá»‰ báº±ng cÃ¡ch báº­t tÃ¹y chá»n mÃ£ hÃ³a. MÃ£ hÃ³a khi nghá»‰ Ä‘Æ°á»£c há»— trá»£ cho táº¥t cáº£ cÃ¡c loáº¡i DB vÃ  sá»­ dá»¥ng AWS KMS.

Khi sá»­ dá»¥ng mÃ£ hÃ³a khi nghá»‰, cÃ¡c yáº¿u tá»‘ sau cÅ©ng Ä‘Æ°á»£c mÃ£ hÃ³a:
- Táº¥t cáº£ báº£n snapshot DB
- Sao lÆ°u
- LÆ°u trá»¯ instance DB
- Read Replicas

\*\*⚠️\ Warning\*\*: Báº¡n khÃ´ng thá»ƒ mÃ£ hÃ³a má»™t DB hiá»‡n cÃ³, báº¡n cáº§n táº¡o má»™t báº£n snapshot, sao chÃ©p nÃ³, mÃ£ hÃ³a báº£n sao, sau Ä‘Ã³ xÃ¢y dá»±ng má»™t DB Ä‘Ã£ Ä‘Æ°á»£c mÃ£ hÃ³a tá»« báº£n snapshot.

RDS há»— trá»£ mÃ£ hÃ³a SSL giá»¯a cÃ¡c á»©ng dá»¥ng vÃ  instance DB RDS, vá»›i RDS tá»± Ä‘á»™ng táº¡o chá»©ng chá»‰ cho instance.

#### NhÃ³m DB Subnet

\*\*ℹ️\ Information\*\*: NhÃ³m DB Subnet lÃ  má»™t táº­p há»£p cÃ¡c subnet (thÆ°á»ng lÃ  riÃªng tÆ°) mÃ  báº¡n táº¡o trong má»™t VPC vÃ  sau Ä‘Ã³ chá»‰ Ä‘á»‹nh cho cÃ¡c DB instances.

- Má»—i nhÃ³m DB Subnet nÃªn cÃ³ cÃ¡c subnet trong Ã­t nháº¥t hai Availability Zone
- Khuyáº¿n nghá»‹ cáº¥u hÃ¬nh má»™t nhÃ³m subnet vá»›i cÃ¡c subnet trong má»—i AZ (tháº­m chÃ­ cho cÃ¡c instance Ä‘á»™c láº­p)
- Trong quÃ¡ trÃ¬nh táº¡o instance RDS, báº¡n chá»n nhÃ³m DB Subnet vÃ  AZ Ä‘á»ƒ Ä‘áº·t instance RDS

#### Thanh toÃ¡n vÃ  cung cáº¥p

AWS tÃ­nh phÃ­ cho:
- Giá» instance DB (giá» pháº§n lÃ m trÃ²n lÃªn giá» Ä‘áº§y Ä‘á»§)
- LÆ°u trá»¯ GB/thÃ¡ng
- YÃªu cáº§u I/O/thÃ¡ng - cho lÆ°u trá»¯ tá»« tÃ­nh
- Provisioned IOPS/thÃ¡ng - cho RDS SSD IOPS Ä‘Æ°á»£c cung cáº¥p
- Truyá»n dá»¯ liá»‡u ra ngoÃ i
- LÆ°u trá»¯ sao lÆ°u (sao lÆ°u DB vÃ  báº£n snapshot thá»§ cÃ´ng)

\*\*ℹ️\ Information\*\*: LÆ°u trá»¯ sao lÆ°u cho sao lÆ°u tá»± Ä‘á»™ng RDS lÃ  miá»…n phÃ­ cho Ä‘áº¿n kÃ­ch thÆ°á»›c á»• EBS Ä‘Ã£ Ä‘Æ°á»£c cung cáº¥p. Tuy nhiÃªn, AWS sao chÃ©p dá»¯ liá»‡u qua nhiá»u AZ vÃ  do Ä‘Ã³ báº¡n pháº£i tráº£ tiá»n cho khÃ´ng gian lÆ°u trá»¯ thÃªm trÃªn S3.

Äá»‘i vá»›i Multi-AZ, báº¡n pháº£i tráº£ tiá»n cho:
- Giá» DB Multi-AZ
- LÆ°u trá»¯ Ä‘Æ°á»£c cung cáº¥p
- Ghi I/O hai láº§n

**ðŸ’¡ Pro Tip**: Äá»‘i vá»›i Multi-AZ, báº¡n khÃ´ng pháº£i tráº£ phÃ­ cho truyá»n dá»¯ liá»‡u DB trong quÃ¡ trÃ¬nh sao chÃ©p tá»« instance chÃ­nh sang instance dá»± phÃ²ng.

#### Kháº£ nÄƒng má»Ÿ rá»™ng

\*\*ℹ️\ Information\*\*: Báº¡n chá»‰ cÃ³ thá»ƒ má»Ÿ rá»™ng RDS lÃªn (tÃ­nh toÃ¡n vÃ  lÆ°u trá»¯). Báº¡n khÃ´ng thá»ƒ giáº£m lÆ°u trá»¯ Ä‘Ã£ cáº¥p phÃ¡t cho instance RDS.

- Báº¡n cÃ³ thá»ƒ má»Ÿ rá»™ng lÆ°u trá»¯ vÃ  thay Ä‘á»•i loáº¡i lÆ°u trá»¯ cho táº¥t cáº£ cÃ¡c DB engine ngoáº¡i trá»« SQL Server
- Äá»‘i vá»›i SQL Server, giáº£i phÃ¡p táº¡m thá»i lÃ  táº¡o má»™t instance má»›i tá»« má»™t báº£n snapshot vá»›i cáº¥u hÃ¬nh má»›i
- Viá»‡c má»Ÿ rá»™ng lÆ°u trá»¯ cÃ³ thá»ƒ xáº£y ra trong khi instance RDS Ä‘ang cháº¡y mÃ  khÃ´ng gÃ¢y ra sá»± cá»‘, tuy nhiÃªn cÃ³ thá»ƒ cÃ³ sá»± suy giáº£m hiá»‡u suáº¥t
- Viá»‡c má»Ÿ rá»™ng tÃ­nh toÃ¡n sáº½ gÃ¢y ra thá»i gian ngá»«ng hoáº¡t Ä‘á»™ng

\*\*⚠️\ Warning\*\*: Táº¥t cáº£ cÃ¡c loáº¡i DB RDS há»— trá»£ kÃ­ch thÆ°á»›c DB tá»‘i Ä‘a lÃ  64 TiB ngoáº¡i trá»« Microsoft SQL Server (16 TiB).

#### Hiá»‡u nÄƒng

Amazon RDS sá»­ dá»¥ng á»• Ä‘Ä©a EBS (khÃ´ng sá»­ dá»¥ng lÆ°u trá»¯ instance) cho lÆ°u trá»¯ DB vÃ  log. CÃ³ ba loáº¡i lÆ°u trá»¯ cÃ³ sáºµn:

**Má»¥c Ä‘Ã­ch chung (SSD - gp2):**
- Sá»­ dá»¥ng cho cÃ¡c táº£i cÃ´ng viá»‡c cÆ¡ sá»Ÿ dá»¯ liá»‡u cÃ³ nhu cáº§u I/O trung bÃ¬nh
- Hiá»‡u quáº£ vá» chi phÃ­
- 3 IOPS/GB
- Burst lÃªn Ä‘áº¿n 3000 IOPS

**Provisioned IOPS (SSD - io1/io2):**
- Sá»­ dá»¥ng cho cÃ´ng viá»‡c cÃ³ yÃªu cáº§u I/O cao
- Äá»™ trá»… tháº¥p vÃ  I/O Ä‘á»u Ä‘áº·n
- Sá»‘ IOPS Ä‘Æ°á»£c chá»‰ Ä‘á»‹nh bá»Ÿi ngÆ°á»i dÃ¹ng

**Tá»« tÃ­nh (Magnetic):**
- KhÃ´ng cÃ²n Ä‘Æ°á»£c khuyáº¿n nghá»‹, cÃ³ sáºµn cho tÃ­ch há»£p ngÆ°á»£c
- Giá»›i háº¡n tá»‘i Ä‘a 4 TiB
- Giá»›i háº¡n tá»‘i Ä‘a 1.000 IOPS

#### Multi-AZ vÃ  Read Replicas

Multi-AZ vÃ  Read Replicas Ä‘Æ°á»£c sá»­ dá»¥ng Ä‘á»ƒ Ä‘áº£m báº£o tÃ­nh sáºµn cÃ³ cao, kháº£ nÄƒng chá»‹u lá»—i vÃ  má»Ÿ rá»™ng hiá»‡u suáº¥t.

| Multi-AZ Deployments | Read Replicas |
|--------------------------------------------|--------------------------------|
| Sao chÃ©p Ä‘á»“ng bá»™ - bá»n vá»¯ng cao | Sao chÃ©p khÃ´ng Ä‘á»“ng bá»™ - má»Ÿ rá»™ng cao |
| Chá»‰ cÃ³ cÆ¡ sá»Ÿ dá»¯ liá»‡u trÃªn instance chÃ­nh lÃ  hoáº¡t Ä‘á»™ng | Táº¥t cáº£ read replicas Ä‘á»u cÃ³ thá»ƒ truy cáº­p vÃ  Ä‘Æ°á»£c sá»­ dá»¥ng Ä‘á»ƒ má»Ÿ rá»™ng Ä‘á»c |
| Sao lÆ°u tá»± Ä‘á»™ng Ä‘Æ°á»£c thá»±c hiá»‡n tá»« instance dá»± phÃ²ng | KhÃ´ng cÃ³ sao lÆ°u Ä‘Æ°á»£c cáº¥u hÃ¬nh máº·c Ä‘á»‹nh |
| LuÃ´n luÃ´n bao gá»“m hai vÃ¹ng kháº£ dá»¥ng trong má»™t Region | CÃ³ thá»ƒ náº±m trong má»™t Availability Zone, Cross-AZ hoáº·c Cross-Region |
| CÃ¡c instance cá»§a cÆ¡ sá»Ÿ dá»¯ liá»‡u Ä‘Æ°á»£c nÃ¢ng cáº¥p trÃªn instance chÃ­nh | Viá»‡c nÃ¢ng cáº¥p instance cá»§a cÆ¡ sá»Ÿ dá»¯ liá»‡u Ä‘á»™c láº­p vá»›i instance nguá»“n |
| Tá»± Ä‘á»™ng chuyá»ƒn Ä‘á»•i sang instance dá»± phÃ²ng khi phÃ¡t hiá»‡n sá»± cá»‘ | CÃ³ thá»ƒ Ä‘Æ°á»£c thÄƒng cáº¥p thá»§ cÃ´ng thÃ nh má»™t instance cÆ¡ sá»Ÿ dá»¯ liá»‡u Ä‘á»™c láº­p |

#### Multi-AZ

\*\*ℹ️\ Information\*\*: Multi-AZ RDS táº¡o má»™t báº£n sao á»Ÿ Availability Zone khÃ¡c vÃ  sao chÃ©p Ä‘á»“ng bá»™ Ä‘áº¿n Ä‘Ã³ (chá»‰ dÃ nh cho DR).

- AWS khuyÃªn nÃªn sá»­ dá»¥ng lÆ°u trá»¯ provisioned IOPS cho cÃ¡c instance DB RDS Multi-AZ
- Má»—i AZ cháº¡y trÃªn cÆ¡ sá»Ÿ háº¡ táº§ng riÃªng biá»‡t, Ä‘á»™c láº­p vá» váº­t lÃ½
- Failover cÃ³ thá»ƒ Ä‘Æ°á»£c kÃ­ch hoáº¡t trong cÃ¡c trÆ°á»ng há»£p nhÆ° máº¥t AZ chÃ­nh, lá»—i tráº¡ng thÃ¡i DB chÃ­nh, máº¥t káº¿t ná»‘i máº¡ng, lá»—i Ä‘Æ¡n vá»‹ tÃ­nh toÃ¡n hoáº·c lÆ°u trá»¯, thay Ä‘á»•i DB chÃ­nh, cáº­p nháº­t há»‡ Ä‘iá»u hÃ nh, hoáº·c failover thá»§ cÃ´ng
- Trong quÃ¡ trÃ¬nh failover, RDS tá»± Ä‘á»™ng cáº­p nháº­t cáº¥u hÃ¬nh (bao gá»“m Ä‘iá»ƒm cuá»‘i DNS) Ä‘á»ƒ sá»­ dá»¥ng nÃºt thá»© hai
- TÃ¹y thuá»™c vÃ o lá»›p instance, cÃ³ thá»ƒ máº¥t tá»« 1 Ä‘áº¿n vÃ i phÃºt Ä‘á»ƒ failover Ä‘áº¿n báº£n sao DB dá»± phÃ²ng

**ðŸ’¡ Pro Tip**: Triá»ƒn khai viá»‡c thá»­ láº¡i káº¿t ná»‘i DB trong á»©ng dá»¥ng cá»§a báº¡n vÃ  sá»­ dá»¥ng Ä‘iá»ƒm cuá»‘i thay vÃ¬ Ä‘á»‹a chá»‰ IP Ä‘á»ƒ chá»‰ Ä‘á»‹nh á»©ng dá»¥ng Ä‘áº¿n DB RDS.

\*\*⚠️\ Warning\*\*: Báº£n sao DB thá»© cáº¥p trong cáº¥u hÃ¬nh Multi-AZ khÃ´ng thá»ƒ Ä‘Æ°á»£c sá»­ dá»¥ng nhÆ° má»™t nÃºt Ä‘á»c Ä‘á»™c láº­p.

#### Read Replicas

\*\*ℹ️\ Information\*\*: Read Replicas Ä‘Æ°á»£c sá»­ dá»¥ng cho cÃ¡c cÆ¡ sá»Ÿ dá»¯ liá»‡u cÃ³ táº£i Ä‘á»c nhiá»u vÃ  sao chÃ©p lÃ  khÃ´ng Ä‘á»“ng bá»™.

- Read Replicas Ä‘Æ°á»£c sá»­ dá»¥ng Ä‘á»ƒ chia sáº» vÃ  giáº£m táº£i cÃ´ng viá»‡c Ä‘á»c
- Pháº£i báº­t tÃ­nh nÄƒng sao lÆ°u tá»± Ä‘á»™ng trÃªn instance chÃ­nh (thá»i gian lÆ°u trá»¯ > 0)
- Chá»‰ Ä‘Æ°á»£c há»— trá»£ cho cÃ¡c Ä‘á»™ng cÆ¡ lÆ°u trá»¯ cÆ¡ sá»Ÿ dá»¯ liá»‡u giao dá»‹ch (InnoDB)
- Read Replicas cÃ³ sáºµn cho MySQL, PostgreSQL, MariaDB, Oracle, Aurora vÃ  SQL Server
- Báº¡n cÃ³ thá»ƒ cÃ³ tá»‘i Ä‘a 5 Read Replicas cá»§a má»™t cÆ¡ sá»Ÿ dá»¯ liá»‡u sáº£n xuáº¥t
- Báº¡n cÃ³ thá»ƒ cÃ³ Read Replicas cá»§a cÃ¡c Read Replicas cho MySQL vÃ  MariaDB (tá»‘i Ä‘a bá»‘n báº£n sao trong chuá»—i)
- Má»—i Read Replica cÃ³ má»™t Ä‘iá»ƒm cuá»‘i DNS riÃªng
- Read Replicas cÃ³ thá»ƒ Ä‘Æ°á»£c báº­t Ä‘a khu vá»±c vÃ  báº¡n cÃ³ thá»ƒ táº¡o Read Replicas tá»« cÃ¡c cÆ¡ sá»Ÿ dá»¯ liá»‡u nguá»“n Ä‘a khu vá»±c

**ðŸ’¡ Pro Tip**: Báº¡n cÃ³ thá»ƒ thÄƒng cáº¥p má»™t Read Replica thÃ nh instance chÃ­nh. Viá»‡c thÄƒng cáº¥p Read Replica máº¥t vÃ i phÃºt vÃ  giá»¯ láº¡i thá»i gian lÆ°u trá»¯ sao lÆ°u, cá»­a sá»• sao lÆ°u, vÃ  nhÃ³m tham sá»‘ cÆ¡ sá»Ÿ dá»¯ liá»‡u.

#### DB Snapshots

\*\*ℹ️\ Information\*\*: DB Snapshots lÃ  cÃ¡c tÃ¬nh huá»‘ng do ngÆ°á»i dÃ¹ng khá»Ÿi táº¡o vÃ  cho phÃ©p báº¡n sao lÆ°u DB instance cá»§a báº¡n á»Ÿ trong má»™t tráº¡ng thÃ¡i xÃ¡c Ä‘á»‹nh.

- Snapshot Ä‘Æ°á»£c lÆ°u trá»¯ trÃªn S3 vÃ  tá»“n táº¡i cho Ä‘áº¿n khi bá»‹ xÃ³a thá»§ cÃ´ng
- I/O táº¡m ngá»«ng trong thá»i gian sao lÆ°u vÃ  cÃ³ thá»ƒ lÃ m tÄƒng Ä‘á»™ trá»… (Ã¡p dá»¥ng cho RDS chá»‰ cÃ³ má»™t vÃ¹ng khu vá»±c)
- DB Snapshot Ä‘Æ°á»£c thá»±c hiá»‡n báº±ng tay sáº½ Ä‘Æ°á»£c lÆ°u trá»¯ ngay cáº£ sau khi DB instance RDS bá»‹ xÃ³a
- DB Ä‘Æ°á»£c khÃ´i phá»¥c sáº½ luÃ´n lÃ  má»™t DB instance RDS má»›i vá»›i má»™t Ä‘iá»ƒm cuá»‘i DNS má»›i
- CÃ³ thá»ƒ khÃ´i phá»¥c lÃªn Ä‘áº¿n 5 phÃºt trÆ°á»›c

**ðŸ’¡ Pro Tip**: NÃªn chá»¥p má»™t Snapshot cuá»‘i cÃ¹ng trÆ°á»›c khi xÃ³a má»™t DB instance RDS. Snapshot cÃ³ thá»ƒ chia sáº» vá»›i cÃ¡c tÃ i khoáº£n AWS khÃ¡c.

#### Theo dÃµi, Ghi log vÃ  BÃ¡o cÃ¡o

Amazon RDS cung cáº¥p nhiá»u cÃ´ng cá»¥ theo dÃµi:

- **Sá»± kiá»‡n Amazon RDS**: ThÃ´ng bÃ¡o khi cÃ³ thay Ä‘á»•i vá»›i DB instance, snapshot, nhÃ³m tham sá»‘ hoáº·c nhÃ³m báº£o máº­t
- **Tá»‡p ghi cÆ¡ sá»Ÿ dá»¯ liá»‡u**: Xem, táº£i xuá»‘ng hoáº·c xem cÃ¡c tá»‡p ghi cÆ¡ sá»Ÿ dá»¯ liá»‡u
- **Amazon RDS Enhanced Monitoring**: Xem cÃ¡c sá»‘ liá»‡u thá»‘ng kÃª thá»i gian thá»±c cho há»‡ Ä‘iá»u hÃ nh
- **Amazon RDS Performance Insights**: ÄÃ¡nh giÃ¡ táº£i trÃªn cÆ¡ sá»Ÿ dá»¯ liá»‡u vÃ  xÃ¡c Ä‘á»‹nh khi nÃ o vÃ  á»Ÿ Ä‘Ã¢u cáº§n thá»±c hiá»‡n
- **Amazon RDS Recommendations**: Xem cÃ¡c khuyáº¿n nghá»‹ tá»± Ä‘á»™ng cho cÃ¡c tÃ i nguyÃªn cÆ¡ sá»Ÿ dá»¯ liá»‡u

Amazon RDS tÃ­ch há»£p vá»›i:
- **Amazon CloudWatch**: Tá»± Ä‘á»™ng gá»­i sá»‘ liá»‡u Ä‘áº¿n CloudWatch má»—i phÃºt
- **Amazon EventBridge**: Tá»± Ä‘á»™ng hÃ³a pháº£n á»©ng vá»›i cÃ¡c sá»± kiá»‡n há»‡ thá»‘ng
- **AWS CloudTrail**: Ghi láº¡i táº¥t cáº£ cÃ¡c cuá»™c gá»i API cho Amazon RDS

**ðŸ’¡ Pro Tip**: Sá»­ dá»¥ng káº¿t há»£p cÃ¡c cÃ´ng cá»¥ theo dÃµi nÃ y Ä‘á»ƒ cÃ³ cÃ¡i nhÃ¬n toÃ n diá»‡n vá» hiá»‡u suáº¥t vÃ  sá»©c khá»e cá»§a cÆ¡ sá»Ÿ dá»¯ liá»‡u RDS cá»§a báº¡n.


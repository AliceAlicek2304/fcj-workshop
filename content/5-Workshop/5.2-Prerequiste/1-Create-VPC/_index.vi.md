---
title : "Táº¡o VPC"
date : "2025-10-27"
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

#### Táº¡o VPC vÃ  cÃ¡c tÃ i nguyÃªn máº¡ng

\*\*ℹ️ Information\*\*: Amazon Virtual Private Cloud (VPC) cho phÃ©p báº¡n khá»Ÿi cháº¡y tÃ i nguyÃªn AWS trong má»™t máº¡ng áº£o Ä‘Æ°á»£c Ä‘á»‹nh nghÄ©a. MÃ´i trÆ°á»ng nÃ y cung cáº¥p kiá»ƒm soÃ¡t Ä‘áº§y Ä‘á»§ vá» cáº¥u hÃ¬nh máº¡ng, bao gá»“m dáº£i Ä‘á»‹a chá»‰ IP, subnet, báº£ng Ä‘á»‹nh tuyáº¿n vÃ  gateway.

#### Táº¡o VPC sá»­ dá»¥ng AWS Management Console

1. Má»Ÿ giao diá»‡n Ä‘iá»u khiá»ƒn Amazon VPC táº¡i [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).

![Create a VPC](/images/1/0001.png?featherlight=false&width=90pc)

2. TrÃªn báº£ng Ä‘iá»u khiá»ƒn VPC, chá»n **Create VPC**.

3. Trong pháº§n **Resources to create**, chá»n **VPC and more** Ä‘á»ƒ táº¡o VPC cÃ¹ng vá»›i cÃ¡c tÃ i nguyÃªn liÃªn quan.

![Create a VPC](/images/1/0002.png?featherlight=false&width=90pc)

4. Cáº¥u hÃ¬nh cÃ¡c tÃ¹y chá»n cÆ¡ báº£n:
   - Giá»¯ nguyÃªn tÃ¹y chá»n **Name tag auto-generation** Ä‘á»ƒ tá»± Ä‘á»™ng táº¡o nhÃ£n cho cÃ¡c tÃ i nguyÃªn, hoáº·c bá» chá»n Ä‘á»ƒ tá»± Ä‘áº·t tÃªn.
   - Nháº­p dáº£i Ä‘á»‹a chá»‰ IPv4 CIDR cho VPC (báº¯t buá»™c).
   - (TÃ¹y chá»n) Äá»ƒ há»— trá»£ IPv6, chá»n **IPv6 CIDR block, Amazon-provided IPv6 CIDR block**.
   - Chá»n tÃ¹y chá»n **Tenancy** phÃ¹ há»£p vá»›i nhu cáº§u cá»§a báº¡n.

5. Cáº¥u hÃ¬nh Availability Zones (AZs):
   - Äá»‘i vá»›i **Number of Availability Zones**, chá»n Ã­t nháº¥t hai AZs cho mÃ´i trÆ°á»ng sáº£n xuáº¥t.
   - Äá»ƒ chá»‰ Ä‘á»‹nh AZs cá»¥ thá»ƒ, má»Ÿ rá»™ng **Customize AZs**.

![Create a VPC](/images/1/0003.png?featherlight=false&width=90pc)

6. Cáº¥u hÃ¬nh subnet:
   - Chá»n sá»‘ lÆ°á»£ng subnet cÃ´ng khai vÃ  riÃªng tÆ° cáº§n thiáº¿t.
   - Äá»ƒ tÃ¹y chá»‰nh dáº£i CIDR cho cÃ¡c subnet, má»Ÿ rá»™ng **Customize subnets CIDR blocks**.

7. Cáº¥u hÃ¬nh káº¿t ná»‘i internet:
   - Äá»‘i vá»›i **NAT gateways**, chá»n sá»‘ lÆ°á»£ng AZs cáº§n triá»ƒn khai NAT gateway.
   - Äá»‘i vá»›i káº¿t ná»‘i IPv6, chá»n **Egress only internet gateway** náº¿u cáº§n thiáº¿t.

**💡 Pro Tip**: Trong mÃ´i trÆ°á»ng sáº£n xuáº¥t, nÃªn triá»ƒn khai NAT gateway trong má»—i AZ cÃ³ chá»©a tÃ i nguyÃªn cáº§n truy cáº­p internet. LÆ°u Ã½ ráº±ng NAT gateway cÃ³ chi phÃ­ sá»­ dá»¥ng.

8. (TÃ¹y chá»n) Äá»ƒ truy cáº­p Amazon S3 trá»±c tiáº¿p tá»« VPC, chá»n **VPC endpoints, S3 Gateway**.

9. Äá»‘i vá»›i tÃ¹y chá»n DNS, máº·c Ä‘á»‹nh cáº£ hai tÃ¹y chá»n vá» giáº£i quyáº¿t tÃªn miá»n Ä‘á»u Ä‘Æ°á»£c kÃ­ch hoáº¡t. Äiá»u chá»‰nh náº¿u cáº§n.

10. (TÃ¹y chá»n) ThÃªm nhÃ£n cho VPC báº±ng cÃ¡ch má»Ÿ rá»™ng **Additional tags**.

11. Xem trÆ°á»›c cáº¥u trÃºc VPC trong báº£ng **Preview**:
    - ÄÆ°á»ng liá»n nÃ©t thá»ƒ hiá»‡n má»‘i quan há»‡ giá»¯a cÃ¡c tÃ i nguyÃªn.
    - ÄÆ°á»ng Ä‘á»©t Ä‘oáº¡n thá»ƒ hiá»‡n luá»“ng lÆ°u lÆ°á»£ng máº¡ng.

12. Khi hoÃ n táº¥t cáº¥u hÃ¬nh, chá»n **Create VPC**.

![Create a VPC](/images/1/0004.png?featherlight=false&width=90pc)

![Create a VPC](/images/1/0005.png?featherlight=false&width=90pc)

#### Cáº¥u hÃ¬nh Ä‘á»‹a chá»‰ IPv4 cÃ´ng khai cho subnet

\*\*ℹ️ Information\*\*: Máº·c Ä‘á»‹nh, subnet khÃ´ng máº·c Ä‘á»‹nh cÃ³ thuá»™c tÃ­nh tá»± Ä‘á»™ng gÃ¡n Ä‘á»‹a chá»‰ IPv4 cÃ´ng khai Ä‘Æ°á»£c Ä‘áº·t thÃ nh "false", trong khi subnet máº·c Ä‘á»‹nh cÃ³ thuá»™c tÃ­nh nÃ y Ä‘Æ°á»£c Ä‘áº·t thÃ nh "true". Subnet khÃ´ng máº·c Ä‘á»‹nh Ä‘Æ°á»£c táº¡o qua trÃ¬nh táº¡o EC2 instance sáº½ cÃ³ thuá»™c tÃ­nh nÃ y Ä‘Æ°á»£c Ä‘áº·t thÃ nh "true".

**Äá»ƒ thay Ä‘á»•i cÃ i Ä‘áº·t Ä‘á»‹a chá»‰ IPv4 cÃ´ng khai cá»§a subnet:**

1. Má»Ÿ giao diá»‡n Amazon VPC táº¡i [https://console.aws.amazon.com/vpc/](https://console.aws.amazon.com/vpc/).

2. Trong báº£ng Ä‘iá»u hÆ°á»›ng, chá»n **Subnets**.

![Create a VPC](/images/1/0006.png?featherlight=false&width=90pc)

3. Chá»n subnet cáº§n cáº¥u hÃ¬nh, sau Ä‘Ã³ chá»n **Actions**, **Edit subnet settings**.

![Create a VPC](/images/1/0007.png?featherlight=false&width=90pc)

4. ÄÃ¡nh dáº¥u hoáº·c bá» Ä‘Ã¡nh dáº¥u tÃ¹y chá»n **Enable auto-assign public IPv4 address** theo nhu cáº§u, sau Ä‘Ã³ chá»n **Save**.

![Create a VPC](/images/1/0008.png?featherlight=false&width=90pc)

\*\*⚠️ Warning\*\*: Viá»‡c thay Ä‘á»•i cÃ i Ä‘áº·t nÃ y chá»‰ áº£nh hÆ°á»Ÿng Ä‘áº¿n cÃ¡c instance má»›i Ä‘Æ°á»£c khá»Ÿi cháº¡y trong subnet. CÃ¡c instance hiá»‡n cÃ³ sáº½ khÃ´ng bá»‹ áº£nh hÆ°á»Ÿng.


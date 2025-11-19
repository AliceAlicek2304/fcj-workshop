---
title : "Táº¡o RDS Security Group"
date : "2025-10-27"
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---

#### Táº¡o Security Group cho Amazon RDS

\*\*ℹ️\ Information\*\*: Security Group cho Amazon RDS hoáº¡t Ä‘á»™ng nhÆ° tÆ°á»ng lá»­a áº£o Ä‘á»ƒ kiá»ƒm soÃ¡t lÆ°u lÆ°á»£ng máº¡ng Ä‘áº¿n vÃ  Ä‘i tá»« cÆ¡ sá»Ÿ dá»¯ liá»‡u cá»§a báº¡n. Viá»‡c cáº¥u hÃ¬nh Ä‘Ãºng Security Group lÃ  bÆ°á»›c quan trá»ng Ä‘á»ƒ báº£o vá»‡ dá»¯ liá»‡u cá»§a báº¡n trong AWS.

#### CÃ¡c bÆ°á»›c táº¡o Security Group cho RDS

1. ÄÄƒng nháº­p vÃ o AWS Management Console.

2. Trong menu dá»‹ch vá»¥, chá»n **VPC** trong pháº§n **Networking & Content Delivery**.

3. Trong thanh Ä‘iá»u hÆ°á»›ng bÃªn trÃ¡i, dÆ°á»›i má»¥c **Security**, chá»n **Security Groups**.

4. Nháº¥p vÃ o nÃºt **Create security group** Ä‘á»ƒ báº¯t Ä‘áº§u quÃ¡ trÃ¬nh táº¡o.

![Create a Security Group](/images/2/0001.png?featherlight=false&width=90pc)

5. Trong pháº§n **Basic details**, nháº­p thÃ´ng tin cÆ¡ báº£n:
   - **Security group name**: Nháº­p tÃªn mÃ´ táº£ cho Security Group
   - **Description**: ThÃªm mÃ´ táº£ chi tiáº¿t vá» má»¥c Ä‘Ã­ch cá»§a Security Group
   - **VPC**: Chá»n VPC nÆ¡i báº¡n sáº½ triá»ƒn khai cÆ¡ sá»Ÿ dá»¯ liá»‡u RDS

6. Trong pháº§n **Inbound rules**, thÃªm quy táº¯c Ä‘á»ƒ cho phÃ©p lÆ°u lÆ°á»£ng truy cáº­p Ä‘áº¿n cÆ¡ sá»Ÿ dá»¯ liá»‡u:
   - Chá»n **MySQL/Aurora** tá»« danh sÃ¡ch loáº¡i (Type)
   - Cá»•ng **3306** sáº½ Ä‘Æ°á»£c tá»± Ä‘á»™ng Ä‘iá»n
   - Äá»‘i vá»›i **Source**, chá»n Security Group cá»§a EC2 instance mÃ  báº¡n Ä‘Ã£ táº¡o trÆ°á»›c Ä‘Ã³

**ðŸ”’ Security Note**: Chá»‰ cho phÃ©p káº¿t ná»‘i tá»« cÃ¡c nguá»“n cá»¥ thá»ƒ thay vÃ¬ má»Ÿ cá»•ng cÆ¡ sá»Ÿ dá»¯ liá»‡u cho táº¥t cáº£ Ä‘á»‹a chá»‰ IP (0.0.0.0/0). Äiá»u nÃ y tuÃ¢n theo nguyÃªn táº¯c Ä‘áº·c quyá»n tá»‘i thiá»ƒu vÃ  tÄƒng cÆ°á»ng báº£o máº­t.

![Configure Inbound Rules](/images/2/0002.png?featherlight=false&width=90pc)

7. (TÃ¹y chá»n) Cáº¥u hÃ¬nh **Outbound rules** náº¿u báº¡n cáº§n giá»›i háº¡n lÆ°u lÆ°á»£ng Ä‘i ra. Máº·c Ä‘á»‹nh, táº¥t cáº£ lÆ°u lÆ°á»£ng Ä‘i ra Ä‘á»u Ä‘Æ°á»£c cho phÃ©p.

8. Sau khi hoÃ n táº¥t cáº¥u hÃ¬nh, nháº¥p vÃ o nÃºt **Create security group**.

![Create Security Group](/images/2/0003.png?featherlight=false&width=90pc)

9. Security Group má»›i Ä‘Ã£ Ä‘Æ°á»£c táº¡o vÃ  sáºµn sÃ ng Ä‘á»ƒ gÃ¡n cho DB instance RDS cá»§a báº¡n.

\*\*⚠️\ Warning\*\*: KhÃ´ng nÃªn sá»­ dá»¥ng cÃ¹ng má»™t Security Group cho cáº£ EC2 vÃ  RDS. Viá»‡c tÃ¡ch biá»‡t Security Group giÃºp quáº£n lÃ½ quyá»n truy cáº­p chÃ­nh xÃ¡c hÆ¡n vÃ  tuÃ¢n thá»§ cÃ¡c nguyÃªn táº¯c báº£o máº­t tá»‘t nháº¥t.

![Security Group Created](/images/2/0004.png?featherlight=false&width=90pc)

**ðŸ’¡ Pro Tip**: Báº¡n cÃ³ thá»ƒ chá»‰nh sá»­a quy táº¯c Security Group báº¥t ká»³ lÃºc nÃ o vÃ  cÃ¡c thay Ä‘á»•i sáº½ Ä‘Æ°á»£c Ã¡p dá»¥ng ngay láº­p tá»©c cho táº¥t cáº£ cÃ¡c tÃ i nguyÃªn Ä‘Æ°á»£c liÃªn káº¿t vá»›i Security Group Ä‘Ã³.


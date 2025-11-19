---
title : "Táº¡o DB Subnet Group"
date : "2025-10-27"
weight : 4
chapter : false
pre : " <b> 5.2.4 </b> "
---

#### Táº¡o DB Subnet Group

\*\*ℹ️\ Information\*\*: DB Subnet Group lÃ  táº­p há»£p cÃ¡c subnet trong VPC Ä‘Æ°á»£c chá»‰ Ä‘á»‹nh cho cÆ¡ sá»Ÿ dá»¯ liá»‡u RDS cá»§a báº¡n. DB Subnet Group cho phÃ©p Amazon RDS triá»ƒn khai instance cÆ¡ sá»Ÿ dá»¯ liá»‡u trong nhiá»u Availability Zone Ä‘á»ƒ Ä‘áº£m báº£o tÃ­nh sáºµn sÃ ng cao vÃ  kháº£ nÄƒng chá»‹u lá»—i.

#### CÃ¡c bÆ°á»›c táº¡o DB Subnet Group

1. ÄÄƒng nháº­p vÃ o AWS Management Console.

2. Trong menu dá»‹ch vá»¥, tÃ¬m vÃ  chá»n **Amazon RDS**.

3. Trong thanh Ä‘iá»u hÆ°á»›ng bÃªn trÃ¡i, chá»n **Subnet groups**.

4. Nháº¥p vÃ o nÃºt **Create DB Subnet Group**.

![Táº¡o DB Subnet Group](/images/2/0005.png?featherlight=false&width=90pc)

5. Trong giao diá»‡n **Create DB Subnet Group**, nháº­p thÃ´ng tin cÆ¡ báº£n:

   - **Name**: Nháº­p tÃªn mÃ´ táº£ cho DB Subnet Group
   - **Description**: ThÃªm mÃ´ táº£ chi tiáº¿t vá» má»¥c Ä‘Ã­ch cá»§a DB Subnet Group
   - **VPC**: Chá»n VPC nÆ¡i báº¡n sáº½ triá»ƒn khai cÆ¡ sá»Ÿ dá»¯ liá»‡u RDS

![Cáº¥u hÃ¬nh thÃ´ng tin cÆ¡ báº£n](/images/2/0006.png?featherlight=false&width=90pc)

6. Trong pháº§n **Add subnets**:
   - Chá»n cÃ¡c **Availability Zones** (AZ) mÃ  báº¡n muá»‘n triá»ƒn khai cÆ¡ sá»Ÿ dá»¯ liá»‡u
   - Chá»n cÃ¡c **Subnets** tÆ°Æ¡ng á»©ng trong má»—i AZ Ä‘Ã£ chá»n

\*\*⚠️\ Warning\*\*: Äá»ƒ triá»ƒn khai Multi-AZ, báº¡n cáº§n chá»n Ã­t nháº¥t hai subnet trong cÃ¡c Availability Zone khÃ¡c nhau. Äiá»u nÃ y Ä‘áº£m báº£o kháº£ nÄƒng chá»‹u lá»—i cao cho cÆ¡ sá»Ÿ dá»¯ liá»‡u RDS cá»§a báº¡n.

7. Sau khi hoÃ n táº¥t cáº¥u hÃ¬nh, nháº¥p vÃ o nÃºt **Create** Ä‘á»ƒ táº¡o DB Subnet Group.

![Chá»n subnet vÃ  hoÃ n táº¥t](/images/2/0007.png?featherlight=false&width=90pc)

**ðŸ’¡ Pro Tip**: Khi chá»n subnet cho DB Subnet Group, hÃ£y Ä‘áº£m báº£o ráº±ng cÃ¡c subnet nÃ y lÃ  subnet riÃªng tÆ° (private subnet) Ä‘á»ƒ tÄƒng cÆ°á»ng báº£o máº­t cho cÆ¡ sá»Ÿ dá»¯ liá»‡u cá»§a báº¡n. CÃ¡c subnet riÃªng tÆ° khÃ´ng cÃ³ káº¿t ná»‘i trá»±c tiáº¿p Ä‘áº¿n Internet, giÃºp báº£o vá»‡ cÆ¡ sá»Ÿ dá»¯ liá»‡u khá»i cÃ¡c má»‘i Ä‘e dá»a bÃªn ngoÃ i.

\*\*ℹ️\ Information\*\*: Náº¿u báº¡n Ä‘Ã£ báº­t Local Zone trong tÃ i khoáº£n AWS cá»§a mÃ¬nh, báº¡n cÃ³ thá»ƒ chá»n má»™t nhÃ³m Availability Zone trÃªn trang Create DB Subnet Group. Trong trÆ°á»ng há»£p nÃ y, hÃ£y chá»n nhÃ³m Availability Zone, cÃ¡c Availability Zones vÃ  Subnets tÆ°Æ¡ng á»©ng.

Sau khi hoÃ n thÃ nh, DB Subnet Group má»›i cá»§a báº¡n sáº½ xuáº¥t hiá»‡n trong danh sÃ¡ch cÃ¡c DB Subnet Group trÃªn giao diá»‡n RDS console. Báº¡n cÃ³ thá»ƒ chá»n DB Subnet Group Ä‘á»ƒ xem chi tiáº¿t, bao gá»“m danh sÃ¡ch cÃ¡c subnet Ä‘Æ°á»£c káº¿t ná»‘i vá»›i nhÃ³m nÃ y, trong pháº§n chi tiáº¿t á»Ÿ dÆ°á»›i cÃ¹ng cá»§a cá»­a sá»•.

![DB Subnet Group Ä‘Ã£ táº¡o](/images/2/0008.png?featherlight=false&width=90pc)

**ðŸ”’ Security Note**: DB Subnet Group lÃ  má»™t thÃ nh pháº§n quan trá»ng trong chiáº¿n lÆ°á»£c báº£o máº­t nhiá»u lá»›p cho cÆ¡ sá»Ÿ dá»¯ liá»‡u RDS. Káº¿t há»£p vá»›i Security Group phÃ¹ há»£p, DB Subnet Group giÃºp kiá»ƒm soÃ¡t cháº·t cháº½ quyá»n truy cáº­p máº¡ng Ä‘áº¿n cÆ¡ sá»Ÿ dá»¯ liá»‡u cá»§a báº¡n.


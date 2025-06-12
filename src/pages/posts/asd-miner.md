---
layout: ../../layouts/post.astro
title: 'Tài liệu hướng dẫn sử dụng ASD Miner'
pubDate: 2025-06-12
description: 'Tài liệu hướng dẫn sử dụng ASD Miner'
author: 'codingcat'
excerpt: Tài liệu hướng dẫn sử dụng ASD Miner
image:
  src:
  alt:
tags: ['docs']
---

# Các đường dẫn

| Tên           | URL                              | Mô tả                       |
| ------------- | -------------------------------- | --------------------------- |
| ASD Pool      | https://asd-pool-fe.pages.dev/   | Quản lý máy đào, trả thưởng |
| ASD Cloud     | https://asd-cloud.pages.dev/     | Quản lý máy đào VPS         |
| ASD Miner Web | https://asd-miner-web.pages.dev/ | Máy đào vật lý bản web      |

Toàn bộ các trang này đăng nhập bằng tài khoản của ct360 nhánh production. **KHÔNG DÙNG TÀI KHOẢN STAGING/TEST**

# Mua license

- Mỗi máy đào cần có 1 license được có thể mua từ trang ct360
- License là 1 đoạn text 64 ký tự
- Tại một thời điểm, license chỉ được gán vào 1 máy đào duy nhất.
- Một user có thể có nhiều licenses và nhiều máy đào 1 lúc
- Quản lý danh sách licenses có thể xem ở ASD pool hoặc ct360.io
  https://asd-pool-fe.pages.dev/license
  ![asd-miner](/blogs-images/asd/0.png)

# Cài đặt máy đào VPS

- Máy đào VPS hay máy đào phi vật lý là máy đào được khởi tạo trên điện toán đám mây không sử dụng máy vật lý (điện thoại, máy tính của user)
- Chính sách hiện tại cho phép khi đã mua license được tặng máy đào VPS tương ứng. Mua 1 license được 1 VPS 2 licenses được 2 VPS,...
- Để xem danh sách VPS đang sở hữu vào trang ASD cloud: https://asd-cloud.pages.dev/
  ![asd-miner](/blogs-images/asd/2.png)
- Tại đây, chọn 1 VPS bấm vào create miner hoặc sang tab `Cloud Miners` để tạo 1 máy đào mới. Nhập tên miner của bạn, chọn license đã mua và VPS đã có, chọn 1 Pool đào cái này chọn Pool nào cũng được không ảnh hưởng đến trả thưởng. Ấn Save
  ![asd-miner](/blogs-images/asd/3.png)

- Khi miner đã được khởi tạo ấn Start để đào theo dõi logs của máy đào,....
  ![asd-miner](/blogs-images/asd/4.png)
  ![asd-miner](/blogs-images/asd/5.png)

# Cài đặt máy đào WEB

- Cài đặt tương tự với asd miner vps đầu tiên vào trang miner web tiến hành đăng nhập: https://asd-miner-web.pages.dev/login
- Sau đó ấn Add miner tiến hành nhập license tên máy đào chọn pool đào vầ bấm Save
  ![asd-miner](/blogs-images/asd/6.png)
  Bấm start mining và treo web để đào nếu thoát ra tiến trình đào sẽ tắt và không nhận được thưởng đây là điểm khác nhau cơ bản giữa máy đào VPS và vật lý
  ![asd-miner](/blogs-images/asd/7.png)

# Quản lý máy đào

- Trong cả trang máy đào web hay cloud miner đều có lịch sử trả thưởng cho miner đó. Muốn quản lý tổng thể toàn bộ miner thì vào trang pool: https://asd-pool-fe.pages.dev/dashboard
  ![asd-miner](/blogs-images/asd/8.png)
  Tại trang này có thể xem rõ các miner (cả vật lý và phi vật lý), config máy đào bật tắt các máy đào,...

# Cơ chế trả thưởng, Setup Payout

- Thưởng mỗi phút sẽ được tính theo công thức reward  = block reward * miner hashrate / total hash rate  / BPM. Trong đó block reward của ASD là 2 ASD cho 1 block, BPM là block per minute vs chain ASD là 4 (1 phút ASD đẻ 4 block). Hash rate là tốc hash của 1 máy được tính bằng hash / s (số lần hash trên giây). key của công thức này là trả thưởng theo năng lực của máy đào

- Ví dụ có 2 miner trong hệ thống tại lúc 10h55 hệ thống bắt đàu tính thưởng miner thứ nhất hasrate 500 miner 2 hashrate 1000 => miner thứ nhất đào bằng 1 nửa miner 2. Vì tính thưởng 1 phút 1 phút asd sinh 4 block mỗi block nhả 2asd làm reward nên 1 phút sẽ có 8 asd làm block reward dựa theo hash ratte  bên trên thì bổ 8 làm 3 thằng miner 1 ăn 1 miner 2 ăn 2 => miner 1 ăn 8 * 1/3 ASD. miner 2 ăn 8 * 2/3 ASD

- Tiền reward mỗi phút sẽ dc cộng dồn cho toàn bộ miner. 1 user sẽ có nh miner. khi tổng thưởng của toàn bộ miner của user đó đủ ngưỡng sẽ dc auto payout toàn bộ vào ví của user (nhập lúc đăng ký). và đồng thời 1% của số này dc gửi thẳng vào ví của thg bố nếu có. (trong th thg bố có join asd và đã config ví nhận thưởng). hệ thống cây cối bố con bê nguyên từ CTO
- Hasrate của miner dc tính toán lại mỗi 1p nên là thưởng cg sẽ ko đều đâu và càng nhiều thg join vào pool đào thì thưởng ae nhận dc sẽ càng ít

- Để setup payout threshold (ngưỡng trả thưởng tự động) vào asd pool (thực ra trong asd cloud hoặc asd miner web cũng set được): https://asd-pool-fe.pages.dev/payouts
  ![asd-miner](/blogs-images/asd/9.png)
Vdu widtdraw threshold là 1000 ASD thì khi nào các miner của tài khoản đấy đào đủ 1k ASD hệ thống sẽ tự động chuyển 1000ASD về ví mà user đã đăng ký khi khởi tạo máy đào.

- Theo dõi lịch sử đào và lịch sử payout ở ASD Pool biết thêm chi tiết
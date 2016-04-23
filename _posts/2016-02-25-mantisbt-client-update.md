---
layout: post
title:  "MantisBT và phiên bản client mới"
date:   2016-02-25
comment: yes
author: manh
---   
Chào các bạn.

Chúng ta lại tiếp tục với H-Net blog.

Hôm nay mình sẽ chia sẻ một vài cập nhật về development trong thời gian làm việc vừa qua.

## 1. Switching to Mantis

Thông tin đầu tiên đó là project đã chuyển sang dùng Mantis ([Mantis Bug Tracker](https://mantisbt.org/)) thay vì dùng Traq ([https://traq.io](https://traq.io)) để phát triển như trước đây.

![image](/images/traq.png)

Giao diện Home của Mantis (đây là trang quản lý project của chính Mantis)

![image](/images/mantis.png)

#### Vậy Mantis là gì?

Mantis Bug Tracker là một ứng dụng web mã nguồn mở , hoạt động như một hệ thống quản lý bug. Mantis dùng để quản lý các lỗi của phần mềm. Tuy nhiên người dùng Mantis thường tùy biến nó trở thành một công cụ quản lý tổng quát hơn, như một công cụ quản lý dự án (Project Management Tool).

Công cụ quản lý dự án sẽ hỗ trợ việc lập kế hoạch phát triển, sắp xếp việc triển khai cũng như quán lý các khía cạnh khác về project, …

Traq cũng là một công cụ quản lý project, tuy vậy Traq đơn giản hơn và ít chức năng Mantis.

Bạn có thể dùng Traq cho các dự án vừa và nhỏ, Traq sẽ đáp ứng rất tốt.

Phiên bản 4.0 của Traq cũng rất nhiều hứa hẹn với chức năng và giao diện quản lý mới.

Hiện tại việc phát triển H-Net đang cần một công cụ mạnh hơn và đảm bảo tốt cho quy trình. Cũng may mắn rằng mình không phải thiết lập kế hoạch lại các kế hoạch ở bên Traq sang Mantis, mà sẽ sử dụng Mantis để tiếp tục phát triển các kế hoạch mới. Điều này vừa kịp lúc cho sự bắt đầu của H-Net Client 0.2.0.

## 2. H-Net Client 0.2.0

Ở bài viết chia sẻ về việc phát triển Client (link), mình có nhắc tới việc cân nhắc sử dụng Qt Quick để viết giao diện. Sau một vài thử nghiệm thì mình đã quyết định viết lại giao diện client với Qt Quick, nên đã skip lên phiên bản 0.2.0 của client.

QtQuick có các điểm mạnh như sau:
- Không cần biên dịch lại khi thay đổi giao diện: khi sử dụng QtWidgets, code giao diện của bạn đều là code C++, và khi thay đổi thứ gì đó thì đều sẽ phải biên dịch lại. QtQuick sử dụng ngôn ngữ QML và giao diện được load tại run-time.
- Viết giao diện dễ: viết giao diện với QML rất dễ và nhanh, giao diện có tính khai báo và rất linh hoạt
- Cấu trúc rõ ràng: client sẽ được cấu trúc thành backend và frontend tách biệt nhau, module hóa sẽ tiện cho việc phát triển
- Animation cho giao diện mạnh: animation trong giao diện viết bởi QtQuick rất tiện lợi và hiệu quả.

Với những lý do trên, việc chuyển sang QtQuick chắc chắn sẽ hiệu quả hơn cho việc phát triển, tăng tốc độ development, giảm độ khó của việc viết giao diện.

Điều này đồng nghĩa với việc sẽ dễ dàng hơn để tạo ra một giao diện tốt. Phần giao diện được tách biệt ra sẽ giúp chúng ta có thể tập trung vào nó cũng như các thành phần khác một cách chuyên biệt hơn.
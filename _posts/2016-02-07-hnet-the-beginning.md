---
layout: post
title:  "H-Net: The Beginning"
date:   2016-02-07
comment: yes
author: manh
---
## 1. The idea
Một ngày nào đó trong tháng 11/2015, sau khi xem “The Social Network”, tập phim kể lại hành trình của Mark Zuckerberg tạo ra mạng xã hội Facebook, ngay đêm đó tôi đã có một ý tưởng về một mạng xã hội của chính mình, nhưng mọi thứ lúc đó chỉ thoáng qua và rất mơ hồ. Rồi cứ vậy nó dần hình thành rõ ràng hơn trong trí tưởng tượng của tôi, một thời gian sau đó, tôi đã tìm ra chính xác rằng mình sẽ tạo nên một mạng xã hội như thế nào.
 
Tôi sẽ tạo ra một mạng xã hội mà ở đó mọi người học lập trình có thể đăng tải code của mình lên,thảo luận cùng những người khác. Tuy nhiên chức năng quan trọng nhất của mạng xã hội này đó chính là Code Review, tức một ai đó có thể highlight các dòng code bạn viết, gợi ý một sự tối ưu nào đó và viết cho bạn lời giải thích. Các suggestion hay sẽ được những người đọc vote lên ở trong code của bạn, và có thêm phần thảo luận về các suggestion khác.

Nói đơn giản rằng, mình sẽ tạo ra một nền tảng dành cho những người yêu thích học code có thể improve code mình viết, improve code cho những người khác, luôn luôn cập nhật. Mọi thứ sẽ bắt đầu ngay tại Hòa Lạc campus, nơi mình đang học tập, nên mình đặt tên cho nó là H-Net – Hòa Lạc Social Network.
Lý tưởng của H-Net đó là: “Inventing new code every day”.

## 2. The system in general
Để theo đuổi ý tưởng này, mình đã tạm dừng việc học ở trường để tập trung full-time. Sau một thời gian nghiên cứu, thử nghiệm và lập kế hoạch để phát triển, hiện tại nền tảng đầu tiên của H-Net đã được hình thành. H-Net System gồm 3 dự án, được phát triển với C++11: hnetserver, hnetclient và hnetctl (ứng dụng này được viết cho admin, để có thể điều khiển một server đang chạy trên mọi khía cạnh – nghĩa là Main server sẽ vừa phục vụ client, vừa có thể được điều khiển tùy ý qua hnetctl).

Mình sẽ dần dần đi vào các vấn đề của H-Net trong bài viết này, để chỉ ra rằng rằng mình đã xử lý được những vấn đề nào, vấn đề nào chưa, và về mức độ của vấn đề. Tất nhiên không thể cover hết tất mọi thông tin, mình sẽ lựa chọn ra các vấn đề đáng quan tâm nhất.

## 3. Why not a Web Application?
Mình nhận thấy rằng một web app sẽ có nhiều thứ phụ thuộc, cũng như tốc độ của nó không cao. Mình cũng không phủ nhận rằng một phần là do mình cảm thấy ít có kinh nghiệm về web app. Việc mình quyết định viết ra một nền tảng hoàn toàn mới cho desktop, nó đưa lại sự kiểm soát tốt hơn về trải nghiệm của người dùng (UX), ví dụ rằng có thể hạn chế việc copy-paste code mẫu của những người khác viết, không có yếu tố này thì sớm muộn chắc là H-Net sẽ trở thành một kho bài tập sẵn có để user copy bài, tất nhiên chức năng copy-paste sẽ hoạt động cho những user thực sự thích code và muốn rèn luyện thực sự.

Tiếp theo là về sau này hoàn toàn có thể phát triển thêm Code Editor, người dùng có thể viết code và chạy trên H-Net Client, chia sẻ sau khi viết xong mà không phải lựa chọn file như những phiên bản đầu tiên. Hãy thử tưởng tượng những thứ đó đến từ một web app chạy trên browser, sẽ rất chậm và không nó khả thi dưới góc nhìn của mình.

## 4. Why C++?
Oh đây cũng là một vấn đề đáng cân nhắc bởi các modern system hiện nay (ý mình là ở Việt Nam) ít khi được viết bởi C++, lý do chủ yếu có thể sẽ là: dùng C++ rất khó làm. Đúng vậy, C++ khó học, khó dùng và hiện tại không có nơi nào sẽ dạy cho bạn về C++ thật sự như thế nào.

(Như một điều tất yếu, trường mình đang học cũng đã không còn môn C++ trong chuyên ngành Kỹ thuật phần mềm, nhưng vẫn dạy lập trình C ngay từ đầu – thật khó hiểu, có thể rằng người ta chỉ miễn cưỡng chấp nhận C là căn bản của lập trình và ai cũng phải học nó trước, hoàn toàn không phải, có thể dạy ngay Java, JavaScript, hoặc là Python cho một người chưa biết gì về lập trình, hiệu quả hơn việc khiến người mới học đau đầu với con trỏ và cấp phát động của ngôn ngữ C).
Tuy nhiên không chỉ đơn giản như vậy, bạn có thể xem thêm một bài dịch của tôi tại link:
[Hậu quả từ những trường trọng Java](http://devnt.org/hau-qua-tu-nhung-truong-trong-java/)

Trở lại với H-Net, ngôn ngữ C++, cụ thể là C++11 đã:

- Cho mình sự kiểm soát hoàn toàn và chi tiết về sự thực thi, điều khó nằm ở chỗ bạn phải làm nhiều thứ thủ công, nhưng đổi lại bạn sẽ nắm trong tay mọi thứ nhỏ nhất và hoàn toàn có thể điều chỉnh theo ý muốn. Với những ngôn ngữ an toàn như C# hay Java, bạn sẽ khó có thể can thiệp ở mức sâu hơn bởi bản chất là bạn không cần (và cũng không thể) can thiệp sâu hơn khi sử dụng managed language. Những chương trình viết bằng C/C++ chỉ thực thi chính xác những gì bạn viết, không hơn không kém.

- High performance and Efficency: Java từng thực thi chậm rất nhiều so với C/C++, nhưng khoảng cách đó ngày càng ngắn lại, cho đến 15-20 lần và hiện nay đã gần ngang ngửa với native language, thậm chí đôi lúc nhanh hơn, nhưng resource usage (CPU, memory) cao hơn bởi Java code không được biên dịch trực tiếp thành mã máy để thực thi mà thực thi qua một JVM. Các công ty có nguồn lực và chi phí phần cứng cũng như chi phí duy trì chưa phải là mối quan tâm thì hoàn toàn có thể chọn Java để tăng tốc độ phát triển và giảm chi phí nhân công, hoàn toàn hiệu quả. Nhưng H-Net không có phần cứng như vậy. HNetServer được viết bằng C++11, thân thiện với môi trường Linux cũng như có thể tùy ý optimize để tăng performance và efficency.

- Bên cạnh đó, một số kỹ thuật trong C++ đã cho mình rất nhiều hứng thú, một trong số đó là Lock-free programming – lập trình đa luồng không lock, tức sẽ không có mutex, điểm chính yếu của lập trình hiệu năng cao bởi nếu một thread khóa mutex, tất cả các thread muốn truy cập sẽ bị vô hiệu hóa. Strand Object của Asio (think-async.com – networking và IO framework mà H-Net sử dụng) dễ dàng thực hiện điều này, dễ dàng hơn việc phải tự viết cấu trúc dữ liệu Lock-free để sử dụng nếu bạn muốn làm điều này trong Java (google keywords: java lock free programming). HnetServer là một ứng dụng multithreading, nhưng việc một thread block thread khác là việc không xảy ra trong quá trình thực thi.

- Mình nên rèn luyện C++ để theo đuổi lập trình game.

- Và nhiều lý do khác nữa,…

Code Metrics – mình sử dụng tool [Code Analyzer](http://sourceforge.net/projects/codeanalyze-gpl/)
<br>Đây là thông tin code base của 3 project, lượng code này do mình viết và không bao gồm code giao diện được tự động sinh ra khi sử dụng UI Designer.
Các comment được viết cho Doxygen.

![image](/images/code_metrics.png)

## 5. Security

Các kết nỗi giữa Client và Server đều là kết nối SSL, tất nhiên là mình đang dùng self-signed certificate (OpenSSL 1.0.2f).


Vấn đề tiếp theo là lưu trữ password trên server, sau khi đăng kí một tài khoản, server sẽ random ra một password để gửi đến email cho người đăng ký (hiện tại mình giới hạn cho email của FE, tức email từ tên miền fpt.edu.vn).

![image](/images/hnet_mail.png)

Mình đang sử dụng Mailgun cho dịch vụ e-mail, 10 nghìn email miễn phí mỗi tháng quả là một con số … an toàn :v

Update thêm một chút:
Screenshot màn hình client (draft).

![image](/images/hnet_client_draft.png)

Version đầu tiên: 0.1.0

![image](/images/hnet_ver_0_1_0.png)

Quay lại với Security.

Tất cả các password đều được mã hóa ở cả client và server. Mình sử dụng thuật toán PBKDF2 (https://en.wikipedia.org/wiki/PBKDF2). H-Net sử dụng xxx xxx lần ở client và xxx xxx lần ở server. Mọi password đều trải qua 2 giai đoạn này trước khi vào database, và kèm thêm random salt cho mỗi password với độ dài salt tiêu chuẩn.

## 6. Performance

Dưới đây là biểu đồ benchmark server, tất nhiên sẽ cần có những case kỹ càng hơn, benchmark này mang tính sơ bộ.

![image](/images/hnet_benchmark.png)

Trục ngang là tổng số request, cột xanh dương là hiệu suất của server, tính bằng số requests/giây, đường màu da cam là thời gian thực hiện và trả lời toàn bộ các requests gửi đến.

Mình tăng dần lượng requests gửi đến server cho đến con số 100 000, bởi về sau không còn đủ RAM để test tiếp, vậy nên đây chưa phải là performance tốt nhất của server, max performance chắc chắn còn cao hơn nhiều.

Lượng memory mà client sinh ra trong quá trình test là 5.7Gb (mình đã không free mem của client bởi nó sẽ tốn một khoảng thời gian keep track các pointer và delete, chiến thuật test này là chiếm dụng server càng nhiều càng tốt), sẽ cần thiết kế những bài test hiệu quả hơn bởi cách này đã tốn nhiều mem của con laptop 8Gb RAM mình đang dùng.

Mỗi request đòi hỏi server trả về 10 comment của trong một post, post ở đây chính là một bài code người dùng đăng lên. Server test không sử dụng database cache, bởi các request sẽ lặp lại rất nhiều, thay vì cache thì mỗi request sẽ thực hiện lại từ đầu, biểu hiện đúng performance của server.

Trong đợt test cuối:

100k request = 1 triệu comment đã được server phục vụ sau 6 giây.

hơn 16 nghìn request/giây (và không có request nào bị fail trong tất cả các test)

## 7. Efficency

Trong quá trình test, server chỉ chạy một lần và mà không tắt đi, client được chạy nhiều lần và tăng dần số requests gửi tới server, có thể chém gió được rằng server đã phục vụ vài trăm nghìn requests và vài triệu comment.

Chúng ta sẽ xét tới efficency của server trong suốt quá trình này:

HNet chỉ chạy 4 threads, bởi việc cấp 1 thread cho client kết nối là hoàn toàn không thể.

Memory peak: 250488 Kb (244.6 Mb) – Lượng mem sử dụng cao nhất trong benchmark

Memory : 14028 Kb (13.7Mb) – Lượng mem sau khi chạy benchmark

Server chạy môi trường Linux, trên một máy ảo 1 Core/1024 Mb memory.

CPU của máy ảo hầu như đã full-load, tuy vậy memory usage đã rất hiệu quả.

Trong quá trình phát triển mình sẽ cố tiến đến max performance và cải thiện efficency.

Quá trình benchmark này bỏ qua tốc độ internet do tiến hành trên mạng LAN.

## 8. More on progresss

Các chức năng đã hoạt động và đang được viết giao diện:

- Register/Login/Change password/Profile update
- Gửi password cho user qua mail sau khi đăng ký
- Post a code (1 file upload only)
- Post edit : edit name, description
- Comment on a post, edit comment
- Hiển thị các post mới nhất
- Code view: syntax highlighting, line numbers display
- Markdown support
- …

Các chức năng cần phát triển (chưa có kế hoạch cụ thể trong version nào):

- Code Review
- Profile picture
- Private Message
- Hiện thị post theo category, post đc comment/review gần đây
- Vote system
- Tag system
- Search system
- Mailing system
- Các system hỗ trợ cho việc thống kê, quản trị và tương tác tốt hơn với user
- …

Hiện tại mình chưa chắc chắn về thời điểm chạy public beta, vẫn còn nhiều thứ phải làm trong phiên bản đầu tiên, dù sao cũng vừa khởi động được vài tháng, và mình đã chuẩn bị cho trường hợp cần thiết phải phát triển lâu dài mới có thể release phiên bản đầu tiên. Những khi rảnh rỗi mình sẽ viết các bài chia sẻ về development, về các vấn đề công nghệ mà mình gặp phải trong quá trình phát triển mạng xã hội này, hi vọng rằng mình sẽ tạo ra được một nền tảng tốt cho những người yêu thích lập trình, cũng như hi vọng sang năm mới sẽ tìm thêm được vài partner ở Hòa Lạc để cùng nhau phát triển.
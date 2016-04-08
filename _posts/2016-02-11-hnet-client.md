---
layout: post
title:  "Lập trình client cho H-Net"
date:   2016-02-11
comment: yes
author: manh
--- 
Chào mọi người, đây là bài viết đầu tiên chia sẻ về quá trình phát triển H-Net.

Mình nghĩ là không nên chia sẻ chuyện lập trình theo trình tự từ đầu đến cuối, kể chi tiết từ những bước đầu phát triển, bởi sẽ tốn khá nhiều thời gian để sắp xếp lại sự việc trong đầu. Với lại rằng cũng không thể đi vào chia sẻ ngay những chủ đề quá sâu và quá mới, khiến người đọc khó hiểu vì nó hơi xa lạ, mà chính mình cũng đã mất nhiều thời gian để nghiên cứu.

Vậy nên Development Blog mình sẽ viết theo kiểu tùy hứng, khía cạnh nào có thể chia sẻ được thì mình sẽ viết về phần đó, hoặc trường hợp người đọc có thể gợi ý cho mình những vấn đề mà các bạn quan tâm, mình cũng sẽ viết blog. Vậy nên nhật ký phát triển này nó không đơn thuần là ghi chép lại đầy đủ quá trình, mà nó theo chiều hướng chia sẻ về công nghệ, thì sẽ có ích hơn là chỉ chú ý viết về các kỹ thuật đọc lên nghe có vẻ cao siêu :D

## 1. Các vấn đề chính trong lập trình client

Đầu tiên sẽ phải nói về các lựa chọn khi viết client. Như bạn đã biết, H-Net Server được lập trình với ngôn ngữ C++, và mình thấy rằng một server C++ nó hợp lý theo tiêu chí đã đặt ra. Tuy nhiên client thực chất vẫn có thể viết bằng một ngôn ngữ khác, bởi nó chỉ giao tiếp với server qua networking và dữ liệu cũng chỉ là dữ liệu. Tức có thể dùng bất cứ ngôn ngữ nào có thư viện networking và hỗ trợ OpenSSL để giao tiếp với server.
 
Lý thuyết là vậy, nhưng khi viết trên một ngôn ngữ khác thì sẽ có sự bất đồng mà mình khó có thể kiểm soát được. Viết trên ngôn ngữ khác không phải là C++ thì build tools sẽ thay đổi, thậm chí là thay đổi cả IDE và cấu trúc vốn có của các project,…. Chính vì vậy, mình cũng lựa chọn C++ để viết client, và như vậy nó cũng hợp lý hơn, mình nhắc tới các ngôn ngữ khác thì là chém gió vậy thôi, hehe, nhưng đúng là có thể viết client bằng một ngôn ngữ khác. 

Mục tiêu của mình cũng là phát triển một client đa nền tảng. Trong các GUI Framework dành cho C++, Qt cũng là một framework mạnh nhất về giao diện, cũng như có các tiện ích đa nền tảng khác, mọi thứ của Qt cũng hầu như đều chạy được đa nền tảng: Networking đa nền, audio đa nền,… H-Net client hiện tại sử dụng component giao diện đồ họa của Qt, Qt Signals and Slots và QString của QtCore. Mình đã cố gắng hạn chế tối đa Qt code trong client, viết code C++ sẽ ít thứ phụ thuộc hơn. Tức client networking vẫn là Asio (think-async.com). Client framework và giao diện của client phải làm việc với nhau, nên khi thiết kế framework cho client, mình sử dụng tới Signals and Slots của Qt để phổi hợp với các object trong giao diện đồ họa.

Nói về client framework, mình khá là hài lòng vì đã viết được một cơ chế khá tiện lợi. Client chạy với 2 thread, main thread chạy Qt App và giao diện đồ họa. Một thread kia giao tiếp với server ở phía sau. Cấu trúc client khá đơn giản, người dùng tương tác với giao diện đồ họa, giao diện đồ họa gửi yêu cầu đến client core đang chạy độc lập, khi có reply của server thì client core sẽ “thông báo” cho GUI.

Đó cũng là đặc điểm chính của Asynchronous programming, bạn khởi động một công việc và không cần chờ đợi nó hoàn thành – thường là khi ra khỏi một hàm thì tức là bạn đã có kết quả, còn với Async thì không vậy, khi ra khỏi hàm thì có thể công việc của bạn vẫn chưa hoàn thành, khi nào công việc hoàn thành thì một hàm được đặt là completion handler sẽ được thực thi, vậy nên chương trình của bạn sẽ ít khi bị block hơn, ví dụ trường hợp một công việc bị lỗi và gây tắc nghẽn, chương trình sẽ bị treo do tất cả các hàm đều đợi công việc hiện tại hoàn thành thì chương trình mới có thể tiếp tục chạy. Sơ qua về Asynchronous programming và client framework trong H-Net là như vậy.

## 2. Dùng Qt Widgets hay Qt Quick để viết giao diện?

Qt framework có 2 component giúp bạn viết được giao diện cho một ứng dụng C++ đa nền tảng. Đó là Qt Widgets và Qt Quick. Về widget thì có thể bạn sẽ quen thuộc hơn (và các video hướng dẫn về Qt mà mình từng đăng tải cũng chính là Qt Widgets). Qt Quick là một component sử dụng QML là một markup language tựa JSON để khai báo giao diện cho ứng dụng, ngôn ngữ lập trình với QML là JavaScript (dữ liệu có thể giao tiếp được với C++), còn Qt Widgets thì sử dụng C++ thuần túy.

Việc lựa chọn Qt Quick hay Qt Widgets cũng khiến mình đắn đo nhiều lần. Ban đầu thì mình nghiêng hẳn về Widgets vì nghĩ rằng sử dụng hoàn toàn C++ sẽ đỡ rườm rà hơn. Àh cũng nhân tiện nói qua về Qt Creator, bởi các project của H-Net được lập trình với Eclipse, nên mình cũng đã tốn khá nhiều thời gian để “hack” ra việc sử dụng Eclipse để biên dịch Qt Project mà không dùng tới Qt Creator IDE. Hiện nay thì bên client dùng Qt Designer để thiết kế giao diện, thiết kế xong thì có thể biên dịch và viết code bên Eclipse.

Quay lại với chọn GUI component, mình chọn Widgets bởi ban đầu thấy có thể tiến hành làm luôn mà không cần tìm hiểu về Qt Quick, và mình cũng chưa khi nào custom Widgets ở mức sâu hơn nên sẽ thử, và cũng chưa nghĩ ra cách nào để chỉnh cái Qt Quick có thể dùng được với Eclipse. Tuy nhiên Qt Quick cũng xứng với cái tên Quick của nó, mình nhận thấy thằng này viết giao diện khá thoải mái và hỗ trợ tốt cho trải nghiệm giao diện, giao tiếp dữ liệu giữa C++ và JavaScript thì chắc là sẽ ảnh hưởng tới performance của client, và dùng Qt Quick mình cũng nghi ngờ là sau khi biên dịch cái size nó lớn hơn dùng Widgets (cái này chỉ là nghi ngờ thôi chứ cũng chưa có thử). Trước mắt là vậy, mình vẫn đang nghiên cứu Qt Quick dần dần xem nó có hợp lý để chuyển đổi trong các phiên bản tiếp theo hay không, nếu nó hợp lý và kết hợp được với Eclipse thì mình cũng sẽ không ngại việc phải viết lại toàn bộ giao diện cho client 😀 (nếu vậy thì việc này sẽ tốn thời gian, nên có thể là mình sẽ release phiên bản Widget trước và phát triển song song một client với giao diện mới tốt hơn).

## 3. Screenshots

Ở trong bài H-Net: The beginning hẳn mọi người đã thấy bản draft màn hình đầu tiên trong client

![image](/images/hnet_client_draft.png)

Thời gian qua mình cũng có học về thiết kế đồ họa, giờ thì client nó đang như này:

![image](/images/hnet_client_new.png)

Có thể bạn sẽ nhận ra đây không phải là Windows, đúng vậy, các chức năng cơ bản của H-Net đã hoạt động và đang được viết giao diện, nhưng mình vẫn chưa kịp port sang Windows. Hiện tại nền tảng chính của mình là Linux, đây là KUbuntu (Ubuntu KDE) nếu bạn có thắc mắc. Chắc chắn là khi release thì sẽ phải tập trung cho Windows client rồi, mình sẽ tiếp tục phát triển hoàn tiện và port sang Windows sớm nhất có thể.

Đây là một vài screenshot khác, viết đến đây thấy ngại quá, vì nó còn xấu òm :D

Sau khi đăng nhập và vào giao diện chính, bạn sẽ thấy danh sách các post được upload gần đây, khi bấm vào một post thì nó sẽ hiển thị như thế này: kéo lên phía trên phần nút show code có thông tin post và người post các kiểu, và một vùng hiển thị description của bài code.

UI còn xấu và khá khó hiểu nên mình xin phép được chú thích vào ảnh :D

![image](/images/code_view.png)

Bấm nút hiển thị code thì sẽ hiển thị màn hình như ở dưới đây:

![image](/images/code_show.png)

Đoạn code này là từ một file mình viết hồi còn đang nghiên cứu networking để viết H-Net.

Hiện tại tiến độ client và giao diện chính sơ qua là vậy, ngoài ra còn giao diện upload code thì có hỗ thêm markdown để viết description,… các thành phần khác ví dụ như Profile của người dùng cũng đã có giao diện và đang được điều chỉnh thêm.

Đến đây chắc là kết thúc bài viết này được rồi, hẹn các bạn trong một bài khác về chuyện phát triển H-Net.
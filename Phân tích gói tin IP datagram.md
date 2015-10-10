# BAOCAO_TUAN2
##Phân tích gói tin IP datagram
## Cấu trúc gói tin IP:
![Imgur](http://i.imgur.com/EQF7SUJ.jpg)

Phân tích các trường:
###1.Version
Version chỉ ra phiên bản của trình nghi thức IP đang được dùng là Ipv4 (0100) hoặc Ipv6 (0110), có 4 bit. Nếu trường này khác với phiên bản IP của thiết bị nhận, thiết bị nhận sẽ từ chối và loại bỏ các gói tin này.

###2.IP Header Length (HLEN):

– Chỉ ra chiều dài của header , mỗi đơn vị là 1 word , mỗi word = 32 bit = 4 byte . Ở đây trường Header Length có 4 bit => 2^4 -1= 15 word = 15 x 4byte = 60byte nên chiều dài header tối đa là 60 byte(Đó là đã bao gồm chiều dài trường Options và Padding, chiều dài tối đa khi không bao gồm chiều dài của trường Options và Padding là 24 byte) . Giá trị bình thường của trường này khi không có Options được sử dụng là 5 (5 từ 32-bit = 5 * 4 = 20 byte). Đây là chiều dài của tất cảc các thông tin Header. Trường này cũng giúp ta xác định byte đầu tiên của Data nằm ở đâu trong gói tin IP datagram.
###3.Type Of Services (TOS): (8bit)
Đặc tả các tham số về dịch vụ nhằm thông báo cho mạng biết dịch vụ nào mà gói tin muốn được sử dụng, chẳng hạn ưu tiên, thời hạn chậm trễ, năng suất truyền và độ tin cậy.
Precedence. 3 bits. chỉ thị về quyền ưu tiên gửi datagram, nó có giá trị từ 0 (gói tin bình thường) đến 7 (gói tin kiểm soát mạng)

- D. 1 bit: chỉ độ trễ yêu cầu trong đó

D=0: Độ trễ bình thường

D=1: Độ trễ thấp.

- T (Throughput) (1 bit): chỉ độ thông lượng yêu cầu sử dụng để truyền gói tin với lựa chọn truyền trên đường thông suất thấp hay đường thông suất cao.

T. 1 bit.Maximize throughput.

T = 0 thông lượng bình thường và

T = 1 thông lượng cao

- R (Reliability) (1 bit): chỉ độ tin cậy yêu cầu

R = 0 độ tin cậy bình thường

R = 1 độ tin cậy cao

- M. 1 bit. Chi phí tối thiểu

M = 0 chi phí bình thường

M = 1 chi phí tối thiểu
Bảng giá trị khuyến nghị của trường TOS
 
###4.Total Length
– Chỉ ra chiều dài của toàn bộ gói tính theo byte, bao gồm dữ liệu và header. Vì trường này rộng 16 bit, nên chiều dài gói tin dữ liệu IP là 65.535 byte, mặc dù hầu hết là nhỏ hơn. Hiện nay giới hạn trên là rất lớn nhưng trong tương lai với những mạng Gigabit thì các gói tin có kích thước lớn là cần thiết. Để biết chiều dài của dữ liệu chỉ cần lấy tổng chiều dài này trừ đi HLEN.

###5.Identification
- tham số này dùng để định danh duy nhất cho một IP datagram trong khoảng thời gian nó vẫn còn trên liên mạng, giúp bên nhận có thể ghép các mảnh của 1 IP datagram lại với nhau vì IP datagram phân thành các mảnh và các mảnh thuộc cùng 1 IP datagram sẽ có cùng Identification .Đây là chỉ số tuần tự. Nó gia tăng khi mỗi lần gói tin dữ liệu gửi đi. Trường Identification rộng 16 byte, vì vậy sẽ có 65 535 định danh có thể sử dụng.

###6.Flag 
– Một field có 3 bit, trong đó có 2 bit có thứ tự thấp điều khiển sự phân mảnh. Một bit cho biết gói có bị phân mảnh hay không và gói kia cho biết gói có phải là mảnh cuối cùng của chuỗi gói bị phân mảnh hay không.
Fragment Offset – Được dùng để ghép các mảnh Datagram lại với nhau, có 13 bit.

Flags. 3 bits.
R, reserved. 1 bit: Nên để giá trị là 0.

DF, Don't fragment. 1 bit: Quản lý việc phân mảnh của gói tin dữ liệu.
- DF = 0 : Phân mảnh, nếu cần thiết.
- DF=1 : Không được phân mảnh.
Bit DF được biểu thị chính là mệnh lệnh cho các router không được phân mảnh datagram bởi gói tin đó biết chắc sẽ đủ nhỏ để đi qua các Router, và gói tin đó cần đi nhanh hoặc sử dụng cho mục đích đặc biệt nào đó nên cần đặt DF = 0.Điều này có ý nghĩa các datagram phải tránh mạng có kích thước packet nhỏ trên đường đi,nói cách khác nó phải chọn được đường đi tối ưu. Các máy không yêu cầu nhận một gói tin dữ liệu lớn hơn 576 byte.

MF, More fragments. 1 bit.
- MF= phân mảnh cuối 
- MF = 1 có nhiều phân mảnh .
Bit này có ý nghĩa : Nếu gói IP datagram bị phân mảnh thì mảnh này cho biết mảnh này có phải là mảnh cuối không . Tất cả mảnh (trừ mảnh cuối ) phải có bit này thiết lập bằng 1 .Điều này cần thiết để xác định tất cả các mảnh của datagram đã đến đích hay chưa 
###7. Fragment Offset: 
Có 13 bit. Báo bên nhận vị trí offset của các mảnh so với gói IP datagram gốc để có thể ghép lại thành IP datagram gốc.
Ví Dụ : theo hình minh họa
- 1 gói tin IP datagram chiều dài là 4000 byte , có 20 byte header + 3980 byte dữ liệu.
- Mà trên đường truyền chỉ cho phép truyền tối đa là 1500 byte ,cho nên gói tin sẽ phần thành 3 mảnh nhỏ . Mỗi mảnh đều có header là 20 byte , còn phần dữ liệu lần lượng của 3 mảnh là 1480 byte , 1480 byte , 1020 byte . Nên offset của 3 mảnh lần lượt là 0 , 1480 , 2960 . Dựa vào offset để ráp lại thành mảnh lớn ở bên nhận . Cuối cùng là trường Flag bên nhận xác định được mảnh cuối cùng
-ID ở mỗi mảnh nhỏ = x , nghĩa là cùng thuộc 1 mảnh lớn 

###8.Time To Live (TTL) 
– Chỉ ra số bước nhảy (hop) mà một gói có thể đi qua.Con số này sẽ giảm đi một khi một gói tin đi qua một router. Khi bộ đếm đạt tới 0 gói này sẽ bị loại. Trường TTL rộng 8 bit do người gửi khởi tạo. Giá trị đề nghị khởi tạo được xác định trong Assigned Numbers RFC và hiện tại là 64. Các hệ thống cũ hơn thường khởi tạo là từ 15-32. Chúng ta có thể nhận thấy trong 1 số lệnh Ping, gói ICMP echo replies thường được gửi với TTL được thiết lập với giá trị lớn nhất của nó là 255. Đối với máy tính cài Windows, mặc định TTL = 124, máy Linux là 64, máy Sun Scolari là 256 ... Đây là giải pháp nhằm ngăn chặn tình trạng lặp vòng vô hạn của gói nào đó.

###9.Protocol-(8bit):
Chỉ ra giao thức nào của tầng trên (tầng Transport) sẽ nhận phần data sau khi công đoạn xử lí IP diagram ở tầng Network hoàn tất hoặc chỉ ra giao thức nào của tầng trên gởi segment xuống cho tầng Network đóng gói thành IP Diagram , mỗi giao thức có 1 mã.

###10.Header CheckSum 
– Giúp bảo dảm sự toàn vẹn của IP Header, có 16 bit.

###11.Source Address
– Chỉ ra địa chỉ của node truyền IP diagram, có 32 bit.Mặc dù các thiết bị trung gian như Router có thể xử lý gói tin dữ liệu, nhưng chúng thường không đặt địa chỉ của chúng vào trường này, mà trường này luôn là địa chỉ của thiết bị ban đầu gửi gói tin dữ liệu.

###12.Destination Address 
– Chỉ ra địa chỉ IP của Node dự định được nhận IP diagram, có 32 bit. Một lần nữa, mặc dù các thiết bị như router có thể là điểm tới trung gian của các gói dữ liệu này, nhưng trường này luôn luôn là địa chỉ của điểm đến cuối cùng.

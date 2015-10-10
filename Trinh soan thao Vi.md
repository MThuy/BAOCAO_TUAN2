#Trinh soan thao Vi trong Ubuntu

#1. Tìm hiểu cách sử dụng trình soạn thảo vi

###1.1. Giới thiệu về VI:
Vi(Video interactif) là chương trình soạn thảo chuẩn trên các hệ điều hành Unix. Nó là chương trình soạn thảo trực quan, hoạt động dưới 2 chế độ: Chế độ lệnh và chế độ soạn thảo.
Để soạn thảo thảo tập tin mới hoặc xem hay sửa chữa tập tin mới hay sửa chữa tập tin cũ 
####1.1.1. Khởi động Vi"
Ta có thể gọi vi tới tên tập tin văn bản:
## $vi tên_tập tin
Cửa sổ soạn thảo sẽ được mở tại tập tin. Nếu tập tin chưa tồn tại, nó sẽ được tạo bởi lệnh ghi. Dòng cuối cùng trên màn hình được dùng cho những công việc sau:
- Vào các lệnh
-Thống kê
- Báo lỗi
Khi ta chỉ muốn xem nội dung một tập tin đã có trên đĩa, dùng lệnh:
# $view tên_tập tin
Để thoát trình xem, nhấn phím ESC gõ:q! nhấn phím Enter

#### 1.1.2. Thoát khỏi Vi:
-Muốn ra khỏi vi và ghi lại nội dung tập tin, bạn nhấn phím ESC và dùng lệnh như sau: # :ZZ hoặc # :wq hoặc # :x
- Thoát khỏi vi và không ghi các thay đổi trước đó # :q!
Khi ở trong chế độ soạn thảo vủa vi, muốn làm việc với các lệnh SHELL, ta có thể làm như sau:
- Chạy một lệnh SHELL
#:! Lệnh
- Hoặc gọi SELL, sau đó chạy các lệnh của người dùng, khi kết thúc bấm Ctrl-D để trở lại vi:
#:! sh
# $ lệnh
# $ Ctrl-D

#2. Soạn thảo văn bản:
##2.1. Chèn văn bản:
- Chèn ký tự trên một dòng:
a <text> <ESC>
- Chèn ký tự vào vị trí con trỏ. Lệnh không được hiển thị trên màn hình. Nhấn phím ESC để kết thúc chế độ chèn văn bản.
i <ESC> Xen ký tự vào sau con trỏ .
A <ESC> Xen ký tự vào cuối dòng .
i <ESC> Xen ký tự vào cuối dòng .
- Chèn dòng :
o <ESC> Xen một dòng vào trước dòng chứa con trỏ .
o <ESC> Xen một dòng vào sau dòng chứa con trỏ .

##2.2. Di chuyển con trỏ trong tập tin :
- Theo kí tự:

 Sang trái: dùng phím trượt trái hoặc h hoặc backspace
 Xuống dòng: dùng phím trượt trái xuống hoặc j hoặc linefeed
 Sang trái: dùng phimd trượt phải hoặc i hoặc espace
 Lên dòng: dùng phím trượt lên hoặc k
- Theo dòng:
 
 ^ về đầu dòng
Enter đầu dòng kế tiếp 
 $ cuối dòng
- Đầu dòng trên 
  0 (null) về đầu dòng vật lý (dòng bắt đầu dấu cách hoặc Tab)
- Theo màn hình:
 H về đầu màn hình
M về đầu màn hình 
 L về cuối màn hình
- Theo từ: 

w W về đầu từ tiếp
 b B đầu từ hiện tại 
e E cuối từ hiện tại
- Theo câu:

 ( về đầu câu
 ) về cuối câu
Lưu ý kết thúc một câu là dấu .! hoặc ?
- Theo cửa sổ (window):

 z dòng hiện tại ở giữa cửa sổ .
 z<Enter> dòng hiện tại ở đầu cửa sổ
 ^D dòng hiện tại ở cuối cửa sổ
 ^U xuống nữa cửa sổ
 ^F xuống một cửa sổ (-2 dòng)
 ^B lên một cửa sổ (-2 dòng)
Lưu ý :^là ký hiệu phím CTRL .
-Theo số thứ tự dòng :
 
 Để hiển thị số thứ tự các dòng soạn thảo :
 : set nu
-Xóa bỏ hiển thị trên :
 : set nonu
 :n<Enter> hoặc nG Chuyển con trỏ đến dòng thứ n
 :s hoặc G Đến cuối dòng văn bản
 :se list hiển thị các kí tự ẩn
- Tìm theo dãy kí tự :

/ kí hiệu chiều tìn xuôi
? kí hiêụ chiều tìm ngược
/string chuyển con trỏ đến dòng chứa dãy kí tự theo chiều
xuôi
?string chuyển con trỏ đến dòng chứa dãy kí tự theo chiêu ngược
// lặp lại tìm xuôi
?? lặp lại tìm ngược
##2.3. Xóa văn bản :
- Xóa kí tự :
x xóa kí tự taịo vị trí con trỏ
3x xóa 3 kí tự
x xóa kí tự trước vị trí con trỏ
- Xóa dòng văn bản :
dd hoặc :d<CR> xóa dòng chứa con trỏ
3dd xóa 3 dòng bắt đầu từ vị trí văn bản
d$ hoặc D xóa đến cuối dòng
dw xóa từ chứa con trỏ
3dw xóa 3 từ
d/string xóa đến khi hết dãy kí tự

##2.4. Thay thế văn bản :
-Thay thế kí tự :
rc thay thế kí tự đại diện bằng kí tự c
R <ESC> thay thế số kí tự bằng dãy 'text"
- Thay thế dòng :
S <ESC> xóa dòng hiện tại và thay thế nó bằng "text"
- Thay thế từ :
cw <ESC> thay thế một từ bằng "text" .
Từ được thay thế tính từ vị trí con trỏ đến kí tự $
c2w<ESC> thay 2 từ
c hoặc c$ thay thế đến cuối dòng
c/string thay thế đến hết chuỗi

##2.5. Xóa hoặc lặp lại tập lệnh :
- Xóa lệnh
u xóa tác dụng của lệnh cuối cùng
U xóa tất cả các thay đổi đã làm trên dòng hiện tại
- Lặp lại lệnh
. lặp lại lệnh thay dổi văn bản

##2.6. Xem trạng thái văn bản đang soạn thảo :
^G Hiển thị tên , trạng thái ,số dòng , vị trí cursor và phần văn bản tính
từ vị trí con trỏ đến cuối dòng văn bản .

##2.7. Sao chép , di chuyển văn bản :
+ Di chuyển văn bản
Mỗi lần thực hiện một lệnh xóa (x hoặc d ) , vi đều ghi lại phần văn bản
bị xóa vào vùng đệm riêngcho đến lần xóa sau . Lệnh p hoặc P cho phép lấy
lại phần văn bản từ vùng đệm đó . Trước khi thực hiện lệnh này , dấu nháy
phải được đặt vào vị trí cùng kiểu với phần văn bản có trong vùng đệm :
- kí tự
- từ
- dòng
- cuối dòng
p sao phần văn bản xóa lần cuối vào sau đối tượng cùng kiểu
P sao phần văn bản xóa lần cuối vào trước đối tượng cùng kiểu
* cách khác để chuyển dòng :
:5, 10m 20 chuyển các dòng từ 5 đến 10 tới sau dòng 20
+ Sao chép văn bản
Lệnh y (yank) cho phép sao chép phần văn bản ta muốn vào vùng
đệm . Muốn sao phần văn bản từ vùng đệm ra, ta phải chuyển cursor đến nơi
cần sao , sau đó dùng P hoặc p
Y3w sao 3 từ vào vùng đệm
Y hoặc yy sao dòng hiện tại vào vùng đệm
5yy sao 5 dòng vào vùng đệm
Cách khác dùng để sao chép dòng :
:5, 8 t 25 sao chép các dòng từ 5 tới 8 tới sau dòng 25

  
  


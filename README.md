# MÔ HÌNH LSTM - LONG SHORT TERM MEMORY TRONG PHÂN TÍCH GIÁ CHỨNG KHOÁN
Trong thời đại công nghệ hiện đại bùng nổ, đặc biệt với sự ra đời của trí tuệ nhân tạo
đang trở nên phổ biến hơn bao giờ hết. Sự ra đời của máy học, trí tuệ nhân tạo, mạng
nơ-ron và cấc công nghệ học tập hiện đại đã giúp cuộc sống con người trở nên ngày càng
dễ dàng.

Nhưng để có thể từ một mô hình trí tuệ nhân tạo, có thể đưa ra đánh giá, dự báo không
phải đơn giản. Do đó, em quyết định nghiên cứu, tìm hiểu về mô hình Long Short Term
Memory dự báo giá chứng khoán. Từ đó, đặt nền móng cơ bản về các mô hình học tập
như Trí tuệ nhân tạo, máy học, học sâu, mạng nơ-ron và nghiên cứu sâu hơn trong tương
lai. Bài báo cáo này trình bày tổng quan hiểu biết của em về mô hình Long Short Term
Memory (LSTM) và kết quả nghiên cứu xây dựng mô hình LSTM dự đoán chỉ số giá
chứng khoán VN-index.

# Mô hình LSTM
LSTM có dạng một chuỗi các nút lặp đi lặp lại của mạng thần kinh:

Từ mô hình trên, tại nút thứ t thấy được mô hình LSTM nhận các giá trị đầu vào
là xt và ht−1 là trạng thái ẩn của nút t − 1. Điểm đặc biệt của mô hình LSTM là
trạng thái tế bào(Cell state) Ct - chính đường chạy thông ngang phía trên của sơ
đồ. Trạng thái tế bào là một dạng giống như băng truyền, chạy xuyên suốt qua
các nút mạng. Vì vậy mà các thông tin có thể dễ dàng truyền đi thông suốt.

## Quá trình thực hiện mô hình LSTM
Bước 1: LSTM sẽ quyết định thông tin nào sẽ được loại bỏ khỏi tế bào thông
qua tầng cổng quên. Cổng dùng hàm sigmoid với đầu vào là ht−1, xt và trả
về một số nằm trong khoảng (0, 1). Giá trị này càng gần 0 nghĩa là thông tin
ít quan trọng, giá trị càng gần 1 nghĩa là thông tin càng quan trọng.
![image](https://github.com/datvu1502/Do_An_2/assets/118582440/e29e726a-7243-4819-a027-1906f979a9d1)

• Bước 2: Xác định thông tin mới nào sẽ được lưu trữ trong trạng thái tế bào.
Quá trình xác định này được chia làm 2 giai đoạn.

Giai đoạn 1: Sử dụng hàm sigmoid σ của cổng vào quyết định giá trị nào sẽ
được cập nhật.


Giai đoạn 2: Sử dụng hàm tanh tạo ra một vector trạng thái mới C˜t sao cho
C˜t có thể thêm vào trạng thái.

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/c2ac6f73-c80c-4dbb-b2d2-e01b45aee81d)

Trong bước tiếp theo sẽ kết hợp 2 giá trị này để tạo ra cập nhật cho trạng
thái tế bào

Bước 3: Cập nhật trạng thái tế bào cũ Ct−1 sang trạng thái tế bào mới Ct.
Chúng ta sẽ nhân trạng thái cũ Ct−1 với ft để xác định thông tin nào sẽ được
loại bỏ khỏi trạng thái tế bào cũ, sau đó sẽ cộng thêm trạng thái cập nhật
mới it * C˜t. Trạng thái tế bào sẽ được cập nhật như hình dưới đây.

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/b37d91de-2f31-452f-abc8-06ea7136d2f1)

Bước 4: Xác định đầu ra của nút, đầu ra này phụ thuộc vào trạng thái của tế
bào vừa được cập nhật nhưng vẫn tiếp tục được chọn lọc. Đầu tiên, sử dụng
hàm sigmoid với đầu vào xt và ht−1 để quyết định phần nào của trạng thái
tế bào ta muốn xuất ra thu được ot.

Sau đó, chúng ta đưa trạng thái tế bào
vừa mới được cập nhật qua hàm tanh để có được giá trị nằm trong khoảng
(-1, 1), rồi nhân với giá trị đầu ra ot vừa tìm được. Ta thu được giá trị cần
dự đoán tại bước thứ t như hình dưới đây.
![image](https://github.com/datvu1502/Do_An_2/assets/118582440/391e15c9-a5eb-48c6-81cf-e3bf273e10f9)



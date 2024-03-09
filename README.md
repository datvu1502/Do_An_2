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

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/4daf75a7-aef1-42f7-869e-b629f8b664dd)


• Bước 2: Xác định thông tin mới nào sẽ được lưu trữ trong trạng thái tế bào.
Quá trình xác định này được chia làm 2 giai đoạn.

Giai đoạn 1: Sử dụng hàm sigmoid σ của cổng vào quyết định giá trị nào sẽ
được cập nhật.


Giai đoạn 2: Sử dụng hàm tanh tạo ra một vector trạng thái mới C˜t sao cho
C˜t có thể thêm vào trạng thái.

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/c8ce4c32-107c-4eab-85ac-83493a4fb538)


Trong bước tiếp theo sẽ kết hợp 2 giá trị này để tạo ra cập nhật cho trạng
thái tế bào

Bước 3: Cập nhật trạng thái tế bào cũ Ct−1 sang trạng thái tế bào mới Ct.
Chúng ta sẽ nhân trạng thái cũ Ct−1 với ft để xác định thông tin nào sẽ được
loại bỏ khỏi trạng thái tế bào cũ, sau đó sẽ cộng thêm trạng thái cập nhật
mới it * C˜t. Trạng thái tế bào sẽ được cập nhật như hình dưới đây.

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/b286ebdd-ff36-47ca-9eb8-092b9c785471)


Bước 4: Xác định đầu ra của nút, đầu ra này phụ thuộc vào trạng thái của tế
bào vừa được cập nhật nhưng vẫn tiếp tục được chọn lọc. Đầu tiên, sử dụng
hàm sigmoid với đầu vào xt và ht−1 để quyết định phần nào của trạng thái
tế bào ta muốn xuất ra thu được ot.

Sau đó, chúng ta đưa trạng thái tế bào
vừa mới được cập nhật qua hàm tanh để có được giá trị nằm trong khoảng
(-1, 1), rồi nhân với giá trị đầu ra ot vừa tìm được. Ta thu được giá trị cần
dự đoán tại bước thứ t như hình dưới đây.
![image](https://github.com/datvu1502/Do_An_2/assets/118582440/43abefd8-6509-4729-a654-f681de258650)


# Thử nghiệm số
Sau khi tìm hiểu lý thuyết về LSTM, trong báo cáo này áp dụng vào việc xây
dựng mô hình dự báo chỉ số giá chứng khoán VN-Index.

Chỉ số VN-Index là một chỉ số thị trường chứng khoán của Việt Nam, đại diện
cho tất cả cổ phiếu niêm yết tại Sở Giao dịch Chứng khoán TP.HCM (HoSE). Chỉ
số này được tính từ ngày thị trường chứng khoán Việt Nam đi vào hoạt động vào
ngày 28/7/2000, với giá trị cơ sở ban đầu là 100 điểm.

Chỉ số VN-Index được tính toán và thay đổi trong quá trình diễn ra giao dịch trên
thị trường chứng khoán. Sự biến động về giá cổ phiếu sẽ làm thay đổi giá trị của
chỉ số này.

Sự biến động của chỉ số VN-Index phản ánh rủi ro hệ thống trong thị trường chứng
khoán Việt Nam. Việc dự báo sự tăng giảm của VN-Index. có thể giúp các nhà
đầu tư nhận biết chiều hướng biến động giá của các cổ phiếu trên thị trường này,
đồng thời cung cấp thông tin về xu hướng và tình hình thị trường chứng khoán.

Bộ dữ liệu sử dụng của chỉ số chứng khoán VN-Index trong khoảng thời gian từ
ngày 1/10/2020 đến ngày 29/12/2023. Bộ dữ liệu lấy từ trang web investing.com

## Tổng quan về bộ dữ liệu 
•	Bộ dữ liệu bao gồm 814 dòng, 5 cột đại diện cho các trường dữ liệu:

![tongquan2](https://github.com/datvu1502/Do_An_2/assets/118582440/0cd80344-3499-49c1-926b-5af600b47ec6)

![bodl](https://github.com/datvu1502/Do_An_2/assets/118582440/a4809bfc-8214-4fcb-9dda-37ba59542968)


–	Time: thời gian

–	Open: giá mở cửa.

–	High: giá cao nhất trong phiên giao dịch.

–	Low: giá thấp nhất trong phiên giao dịch.

–	Close: giá đóng cửa.

Mô hình sử dụng chỉ số giá đóng cửa trong quá khứ để dự đoán giá đóng
cửa trong tương lai, vì thế cần loại bỏ các trường không cần thiết và giữ lại trường giá đóng cửa để tiến hành xây dựng và huấn luyện mô hình. Chỉ số
giá đóng cửa được thể hiện theo thời gian như sau:

 ![hienthidl2](https://github.com/datvu1502/Do_An_2/assets/118582440/08e60772-220a-47e7-86d9-87cc9a59cc46)


•	Tiến hành chia bộ dữ liệu thành 2 tập train và test, với tỷ lệ 80% cho tập train và 20% cho tập test.

•	Mô hình LSTM yêu cầu bộ dữ liệu là 1 chuỗi, mô hình sẽ sử dụng 30 ngày trước đó làm yếu tố quyết định và dự đoán giá cổ phiếu cho ngày thứ 31.

![train](https://github.com/datvu1502/Do_An_2/assets/118582440/7e095de9-34be-477f-b859-20872e66a475)

# Xây dựng mô hình LSTM
Sử dụng thư viện Keras trong Python để xây dựng mô hình LSTM:

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/1ecd5faf-485f-468c-b889-0b81c2eb967a)




Mô hình sử dụng hàm mất mát Mean Squared Error và thuật toán tối ưu Adam để huấn luyện mô hình.

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/f05eb2ef-be72-4264-b64e-c45e6661f5b3)


Sau khi tạo mô hình và chuẩn bị dữ liệu, mô hình còn yêu cầu một số tham
số như sau:

– batchsize: là số lượng dữ liệu cho mỗi lần tính và cập nhật hệ số, huấn
luyện mô hình với batchsize = 32

– epochs: số lượng epoch thực hiện trong quá trình training. (Một epoch
là một lần duyệt qua hết các dữ liệu trong tập training set). Mô hình
thực hiện qua 100 lần.


![loss](https://github.com/datvu1502/Do_An_2/assets/118582440/123c5710-75ea-42c5-b96f-1ccb8341cc95)

Từ kết qua hiển thị trên ta thấy được qua quá trình huấn luyện, lần lượt qua
các lần duyệt, giá trị của hàm mất mát đang có xu hướng giảm dần và đạt
tới giá trị tối ưu gần về 0. Chúng ta có thể thấy rõ hơn về sự giảm dần của
hàm mất mát qua đồ thị sau:

![losspng](https://github.com/datvu1502/Do_An_2/assets/118582440/d6eba03b-62ca-4749-9920-dd410b7f5232)

## Dự báo 
Sau khi xây dựng xong mô hình LSTM, tiến hành sử dụng mô hình để dự báo kết quả cho tương lai với input là tập dữ liệu test:

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/b4597f44-98bf-4b11-a759-844cc4103768)

Kết quả dự báo của mô hình như sau:

![dubao](https://github.com/datvu1502/Do_An_2/assets/118582440/813d9e21-ebcb-479b-b2ce-c34997cd4cf4)

Biểu đồ so sánh giá dự báo và giá cổ phiếu thực tế:

![ketqua](https://github.com/datvu1502/Do_An_2/assets/118582440/36c9ffdb-e9b2-4a66-a3a3-421f7c4872c8)

# Đánh giá mô hình
So sánh giá trị dự đoán và giá trị thực tế qua đồ thị theo thời gian:

![chitiet2](https://github.com/datvu1502/Do_An_2/assets/118582440/555cb234-db42-46f2-8c7b-e5f700b3f496)

Đánh giá sai số:

![image](https://github.com/datvu1502/Do_An_2/assets/118582440/09c0052b-9a0f-47a0-9a5a-130fc90b70a8)

Dự báo chỉ số thị trường chứng khoán Việt Nam sử dụng mô hình LSTM có thể
có sự khác biệt lớn so với giá trị thực tế trong một số ngày giao dịch. Điều này là
do thị trường chứng khoán Việt Nam chịu ảnh hưởng mạnh từ nhiều yếu tố như
tâm lý nhà đầu tư, tác động từ các thị trường chứng khoán khác và thông tin về
sự thay đổi chính sách.

Do đó, nhà đầu tư nên kết hợp kết quả từ mô hình dự báo với phân tích kỹ thuật
và thường xuyên quan sát để có cái nhìn đúng đắn và chính xác về sự biến động
của thị trường chứng khoán. Mô hình dự báo có thể cung cấp một cơ sở dự đoán,
nhưng không đảm bảo rằng các dự báo sẽ hoàn toàn chính xác trong mọi trường
hợp.

Bằng cách kết hợp phân tích kỹ thuật và theo dõi thường xuyên, nhà đầu tư có
thể nhận biết các yếu tố tác động đến thị trường và điều chỉnh quyết định đầu tư
một cách linh hoạt. Điều này giúp tăng khả năng đưa ra quyết định đúng đắn và
tận dụng mọi cơ hội trong môi trường thị trường chứng khoán đầy biến động.









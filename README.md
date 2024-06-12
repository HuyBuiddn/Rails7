Định tuyến trong Rails là kiểm tra URL(địa chỉ tham chiếu
tài nguyên) của 1 request và xác định 1 hành động controller nào được thực hiện.
Việc xác định đúng hành động nào cần được thực thi là quan trọng nhất. Cần xây
dựng 1 bộ quy tắc và bộ quy tắc này được lưu trong file routes.rb.


1 Routes được xây dựng phải đảm bảo được 2 yếu tố đó là phải
cung cấp đủ thông tin để vừa khớp với một URL hiện có vừa tạo ra một URL mới. Về
cấu trúc của Routes:


 - Phương thức HTTP (GET, POST, PUT, PATCH, DELETE,v.v.).


 - Phải xác định được 1 Patterns (mẫu) để match được
   với URL cũ cũng như dựa vào nó tạo ra URL mới. Một Patterns có thể bao gồm 


  o  Static String (chuỗi tĩnh) có thể hiểu như là 1
     biến được khai báo 1 lần và được lưu trữ trong bộ nhớ suốt thời gian chạy của
     chương trình


  o  Dấu gạch chéo (/) mô phỏng cú pháp URL


  o  Segment Keys (Khoá phân đoạn) một khái niệm được
     sử dụng trong quản lý dữ liệu, đặc biệt là trong các hệ thống cơ sở dữ liệu,
     phân tích dữ liệu, và lập chỉ mục (indexing).Khóa phân đoạn thường được dùng để phân chia và tổ chức dữ liệu thành các phân đoạn (segments) hoặc nhóm nhỏ hơn để tối ưu hóa việc truy cập và quản lý dữ liệu. 


 - Chỉ định controller và action mà route sẽ ánh xạ đến.


Ví dụ:  get "recipes/:ingredient" => "recipes#index


 · get: phương thức HTTP mà route này sẽ xử lý, trong trường hợp
   này là GET.


 · "recipes/:ingredient": Đây là URL pattern, trong đó : recipes là 1
    chuỗi tĩnh :ingredient là khoá phân đoạn. Bất kỳ giá trị nào được truyền vào phần định danh này của URL sẽ được chuyển đến hành động index trong controller Recipes.


 · "recipes#index": Đây là định danh của controller và hành động trong controller sẽ xử lý yêu cầu này. Trong trường hợp này, nó chỉ ra rằng yêu cầu sẽ được xử lý bởi hành động index trong controller Recipes.
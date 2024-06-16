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

 routes.rb
Các routes được định nghĩa trong tệp config/routes.rb. File này được tạo khi khởi động 1 dự án Rails.
Trong file hiện tại đang có
Rails.application.routes.draw do
# Define your application routes per the DSL in https://guides.rubyonrails.org/rou\
ting.html
# Defines the root path route ("/")
# root "articles#index"
end
Đây là khối mã để định nghĩa các tuyến đường cho ứng dụng Ruby on Rails. Tất cả các định nghĩa tuyến
đường sẽ được đặt bên trong khối này.
Regular Routes
Như đã mô tả ở trên các cơ bản để định nghĩa 1 tuyến là cung cấp 1 mẫu URL, tên lớp controller với tên
hành động và cuối cùng là phương thức HTTP mong muốn.
match "products", controller: "products", action: "index", via: :get
Giải thích chi tiết
  match: Đây là một phương thức trong Rails để định nghĩa một tuyến đường. match có thể
được sử dụng để ánh xạ một URL đến một hành động controller cho nhiều phương thức
HTTP (GET, POST, PUT, PATCH, DELETE), tùy theo tùy chọn via.
  "products": Đây là mẫu URL mà tuyến đường này sẽ khớp. Trong trường hợp này, bất
kỳ yêu cầu nào đến /products sẽ được khớp với tuyến đường này.
  controller: "products": Đây là tên của controller mà yêu cầu sẽ được chuyển đến.
Trong trường hợp này, nó là ProductsController.
  action: "index": Đây là tên của hành động trong controller sẽ được gọi. Trong trường hợp này, nó là hành động index.
  via: :get: Điều này chỉ ra rằng tuyến đường này sẽ xử lý các yêu cầu HTTP GET.
 Định nghĩa một tuyến mà không chỉ định phương thức HTTP sẽ dẫn đến việc Rails ném ra ngoại lệ ArgumentError. Do đó, bạn cần phải giới hạn phương thức HTTP được sử dụng để truy cập một tuyến.
Nếu, vì lý do nào đó, bạn muốn giới hạn một tuyến cho nhiều hơn một phương thức HTTP, bạn có thể
truyền một mảng các tên động từ (verb) cho :via.
Kết hợp với đoạn code trong file routes.rb ta có
Rails.application.routes.draw do
match "products", controller: "products", action: "index", via: :get
end
đây là 1 ví dụ về routes trong rails.
match "products", controller: "products", action: "index", via: :get
đoạn code trên có thể được rút ngắn thay vì cung cấp lớp controller và hành động riêng biệt, có thể sử
dụng một chuỗi ánh xạ với tham số đặc biệt :to:
match "products", to: "products#index", via: :get
vì tùy chọn to rất phổ biến, một dạng viết tắt được cung cấp:
match "products" => "products#index", via: :get
Rails cung cấp thêm một dạng viết tắt nữa bằng cách thay thế match bằng phương thức HTTP mong
muốn (như get, post, patch, v.v.):
get "products" => "products#index"

Segment Keys (khoá phân đoạn)
 Chuỗi mẫu URL có thể chứa các tham số (được ký hiệu bằng dấu hai chấm) được gọi là khóa phân đoạn.
 Trong khai báo tuyến sau đây, :id là một khóa phân đoạn:
get "products/:id" => "products#show"
Khi tuyến này khớp với một URL yêu cầu, phần :id của mẫu hoạt động như một loại trình khớp và lấy
giá trị của phân đoạn đó. Ví dụ, sử dụng ví dụ trên, giá trị của id cho URL sau sẽ là 4:
http://example.com/products/4. Điều này có nghĩa là giá trị của params[:id] sẽ được thiết lập
thành chuỗi "4". Bạn có thể truy cập giá trị đó bên trong hành động products#show.
Trong View (app/views/some_view.html.erb)
Khi bạn tạo một URL, bạn phải cung cấp các giá trị sẽ gắn vào các khóa phân đoạn bên trong chuỗi mẫu
URL. Cách đơn giản nhất để hiểu (và nguyên bản) là sử dụng một hash, như sau:
link_to "Products",
controller: "products",
action: "show",
id: 1
link_to: Đây là một phương thức trợ giúp (helper method) trong Rails để tạo ra một liên kết HTML.
Cách hoạt động
Khi người dùng nhấp vào liên kết, một yêu cầu HTTP GET sẽ được gửi đến URL /products/1.
Rails sẽ ánh xạ yêu cầu này đến hành động show trong ProductsController, với params[:id]
bằng 1. Hành động show trong ProductsController sẽ sử dụng params[:id] để tìm và hiển thị
chi tiết của sản phẩm có ID là 1.
Spotlight on the :id Field
Trong Controller (app/controllers/products_controller.rb)
Controller chịu trách nhiệm xử lý các yêu cầu và trả về phản hồi thích hợp
class ProductsController < ApplicationController
def show
@product = Product.find(params[:id])
end
end
Giải thích chi tiết
  class ProductsController < ApplicationController:
  Định nghĩa một controller mới có tên là ProductsController.
  Controller này kế thừa từ ApplicationController, vì vậy nó sẽ có tất cả các phương
 thức và tính năng của ApplicationController.
  def show:
  Định nghĩa một hành động trong controller có tên là show. Hành động này sẽ được gọi
khi có một yêu cầu HTTP GET đến một URL tương ứng với hành động show (thường là
/products/:id).
  @product = Product.find(params[:id]):
  Tìm một bản ghi Product từ cơ sở dữ liệu dựa trên id được truyền qua URL (thông qua
params[:id]).
  params[:id] lấy giá trị của tham số id từ yêu cầu URL.
  Product.find là một phương thức Active Record để tìm bản ghi theo id.
  Bản ghi tìm được sẽ được gán cho biến instance @product, biến này có thể được sử dụng trong view tương ứng để hiển thị dữ liệu.
Optional Segment Keys (Khoá phân đoạn tuỳ chọn)
Bạn có thể định nghĩa một khóa phân đoạn là tùy chọn bằng cách đặt nó trong dấu ngoặc đơn
get "products(/:id)" => 'products#display
Điều này sẽ khớp với cả /products cũng như các đường dẫn như /products/15.

Segment Key Constraints (Ràng buộc khoá phân đoạn)
Đôi khi bạn muốn không chỉ nhận dạng một tuyến mà còn nhận dạng nó ở mức độ chi tiết hơn so với chỉ
những thành phần hoặc trường nó có. Bạn có thể thực hiện điều này thông qua việc sử dụng tùy
chọn :constraints
get "products/:id" => "products#show", constraints: {:id => /\d+/}
get "products/:id" => "products#show_error
Ở ví dụ trên bạn có thể định tuyến tất cả các yêu cầu show để chúng đi đến một hành động error nếu
trường id của chúng không phải là số.

Rút gọn Ràng Buộc
Việc thiết lập ràng buộc trên tham số :id là rất phổ biến, do đó Rails cho phép bạn rút gọn ví dụ
trước đó của chúng ta thành:
get "products/:id" => "products#show", id: /\d+/
get "products/:id" => "products#show_error"
Ràng Buộc trên Các Thuộc Tính Yêu Cầu Khác
Từ ví dụ, bạn có thể kết luận rằng việc kiểm tra :constraints áp dụng cho các phần tử của hash
params. Tuy nhiên, bạn cũng có thể kiểm tra một loạt các thuộc tính yêu cầu khác trả về một
chuỗi, chẳng hạn như :subdomain và :referrer.
get "products/:id" => "products#show", constraints: { subdomain: 'admin' }
constraints: { subdomain: 'admin' }: Đây là phần quan trọng của đoạn mã và chỉ ra ràng
buộc (constraints) đối với subdomain. Cụ thể là:
  Tuyến đường này chỉ áp dụng khi subdomain là 'admin'.
  Nghĩa là yêu cầu chỉ được định tuyến đến hành động show trong ProductsController
 nếu subdomain của URL là 'admin'.

Defining Defaults
Bạn có thể định nghĩa các tham số mặc định trong một tuyến bằng cách cung cấp một hash cho
tùy chọn :defaults. Điều này còn áp dụng cho các tham số mà bạn không chỉ định là các phân
đoạn động trong tuyến chính nó.
get "photos/:id", to: "photos#show", defaults: { format: "jpg" }
Trong ví dụ trên, Rails sẽ khớp http://example.com/photos/12 với hành động show của
PhotosController, và thiết lập params[:format] thành "jpg".
Vì lý do bảo mật, bạn không thể ghi đè lên các giá trị mặc định bằng cách thay đổi các giá trị
trong đối tượng params.

Redirect Routes
phương thức redirect: chuyển hướng của tuyến.
- Chuyển hướng đến một URL khác
get "/google", to: redirect("https://google.com/")
- Sử dụng block trong chuyển hướng
Phương thức redirect cũng có thể nhận một block, mà nhận các tham số của yêu cầu làm đối số
của nó. Điều này cho phép bạn thực hiện các phiên bản nhanh của các điểm cuối API dịch vụ
web chẳng hạn:
match "/api/v1/:api",
to: redirect { |params| "/api/v2/#{params[:api].pluralize}" },
via: [:get, :post]
to: redirect { |params| "/api/v2/#{params[:api].pluralize}" }: Chỉ định rằng khi
có yêu cầu đến URL /api/v1/:api, hệ thống sẽ thực hiện một hành động redirect (chuyển
hướng) đến một URL mới được tạo ra dựa trên logic trong block { |params| ... }.
  params[:api]: Lấy giá trị của tham số :api từ yêu cầu HTTP.
  .pluralize: Phương thức của Rails được sử dụng để biến đổi chuỗi thành dạng số nhiều.
 Ví dụ, nếu params[:api] là "user" thì params[:api].pluralize sẽ là "users".
  Vì vậy, URL mới sẽ có dạng /api/v2/#{params[:api].pluralize}. Ví dụ, nếu
 params[:api] là "user", thì URL mới sẽ là /api/v2/users.

Thêm các tham số cho chuyển hướng
Phương thức redirect cũng có thể nhận các tham số như :status (mặc định là 301 cho chuyển
hướng):
match "/api/v1/:api", to:
redirect(status: 302) { |params| "/api/v2/#{params[:api].pluralize}" },
via: [:get, :post]

Routes as Rack Endpoints
Định tuyến mà không cần phải định nghĩa một controller và một hành động
riêng biệt. Giá trị được gọi là 1 điểm cuối của Rack.
get "/hello", to: proc { |env| [200, {}, ["Hello world"]] }
to: proc { |env| [200, {}, ["Hello world"]] }: Chỉ định rằng khi có yêu cầu đến URL
/hello, hệ thống sẽ thực hiện một xử lý tùy chỉnh thông qua một đoạn mã được cung cấp dưới dạng một đối tượng Proc.
  proc { |env| ... }: Đây là một đối tượng Proc (là một đoạn mã được đóng gói và có
thể được gọi) nhận một tham số env, đại diện cho môi trường yêu cầu.
  env chứa thông tin về yêu cầu HTTP như method (GET, POST, PUT,...), headers, và các
thông tin khác.
  [200, {}, ["Hello world"]]: Trả về một mảng gồm ba phần tử:
  o 200: Mã trạng thái HTTP OK, cho biết yêu cầu đã được xử lý thành công.
  o {}: Headers trống, không có thông tin bổ sung cần được trả về.
  o ["Hello world"]: Nội dung của phản hồi, trong trường hợp này là một mảng
  chứa một chuỗi "Hello world".

The Root Route
Tuyến đường gốc là một quy tắc xác định hành động gì sẽ xảy ra khi ai đó kết nối đến "gốc" của
trang web của bạn. Khi bạn kết nối đến một trang web với chỉ tên miền (ví dụ:
http://example.com) mà không có bất kỳ đường dẫn cụ thể nào ở cuối URL, tuyến đường gốc
quy định rằng ứng dụng sẽ thực hiện hành động gì (hiển thị gì ở trang chủ)
root to: "welcome#index"
root to: "pages#home"
# Shorthand syntax
root "user_sessions#new"
Route Globbing
cho phép bạn xác định các tuyến đường linh hoạt hơn bằng cách sử dụng đường dẫn có ký tự đại
diện (wildcard) để phù hợp với nhiều URL khác nhau cùng một lúc. Ví dụ như liệt kê các URL
của các sản phẩm từ gỗ
Globbing Key-Value Pairs
 Ví dụ về Kiểu URI
  Giả sử bạn thiết kế một kiểu URI như sau:
   http://localhost:3000/items/q/field1/value1/field2/value2/...
   Mẫu này cho phép người dùng yêu cầu trả về danh sách sản phẩm dựa trên các trường và giá trị tương ứng của chúng.

   Ví dụ, URL như http://localhost:3000/items/q/year/1939/material/wood có thể tạo ra danh sách các mặt hàng được làm từ gỗ trong năm 1939.

 Ta có thể triển khai như sau:
 Định nghĩa Tuyến Đường
 Để xử lý cấu trúc khóa-giá trị động này trong các tuyến đường của Rails của bạn, bạn sẽ định nghĩa một tuyến đường sử dụng kỹ thuật globbing:

  get "items/q/*specs", controller: "items", action: "query"
  Ở đây:
   - "items/q/*specs" là mẫu URL trong đó *specs chứa tất cả các đoạn sau "items/q/".
   - "items" là tên của controller.
   - "query" là tên của action trong ItemsController.

 Triển Khai Hành Động Trong Controller
 Tiếp theo, bạn cần triển khai hành động query trong ItemsController để xử lý các tham số và thực hiện truy vấn:

  def query
   @items = Item.where(Hash[*params[:specs].split("/")])
  if @items.empty?
   flash[:error] = "Can't find items with those properties"
  end
   render :index
  end

 Giải thích
 - params[:specs]: Chứa các đoạn globbing từ URL, được tách thành mảng các cặp khóa-giá trị (field1/value1/field2/value2/...).
 - Hash[*key_value_pairs]: Chuyển đổi mảng các cặp khóa-giá trị xen kẽ thành một hash có thể sử dụng như các điều kiện trong một truy vấn ActiveRecord.
 - Item.where(conditions): Thực hiện một truy vấn trên mô hình Item với các điều kiện đã chỉ định.
 - Render: Tùy thuộc vào kết quả truy vấn, bạn có thể đặt thông báo flash (flash[:error]) nếu không có sản phẩm nào khớp với tiêu chí và sau đó render view phù hợp (index hoặc một view khác)
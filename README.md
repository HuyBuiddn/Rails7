REST là một kiểu kiến trúc mạng. REST bao gồm 5 quy tắc bắt buộc và 1 quy tắc không bắt buộc:

 - Use of a client-server architecture

 - Stateless communication

 - Response cacheability

 - Uniform interface

 - Layered system

 - Code on demand (không bắt buộc)

Các hệ thống sử dụng REST được gọi là RESTful.

Tài nguyên (resource) là 1 tập hơp các khái niệm biển diễn (represent) tài nguyên đó. Mấu chốt là tài nguyên là danh từ. Ví dụ tài nguyên John bao gồm:

 - Chiều cao

 - Cân nặng

 - Tuổi

 - Quốc tịch

Theo chuẩn REST phản hồi tài nguyên không bao giờ chính nó mà là các biểu diễn của nó.

Như ví dụ trên với 1 định danh tài nguyên duy nhất (URI) của tài nguyên John, máy chủ RESTful sẽ trả về kết quả chiều cao, cân nặng, tuổi, … dựa vào request.

REST in Rails

REST trong Rails tập trung vào phương pháp định nghĩa tài nguyên trong định tuyến từ đó thiết kế ra các controller có thứ tự và logic cụ thể.

Routing and CRUD

CRUD là viết tắt của Create Read Update Detele, đây là 4 hoạt động cơ bản tương tác với database.

Đúng là Controller không ánh xạ trực tiếp đến database như Model. Nhưng để các lập trình viên không quên đi 4 hoạt động này cũng như sự đơn giản trong lập trình thì nên đặt tên cho các hành động của mình theo các thao tác CRUD—hoặc gần giống với tên của các thao tác đó. 

Hệ thống định tuyến không buộc bạn phải triển khai chức năng CRUD của ứng dụng của mình theo bất kỳ cách thức nhất quán nào. Bạn có thể tạo một tuyến đường ánh xạ đến bất kỳ hành động nào, bất kể tên của hành động đó là gì. Việc chọn tên theo CRUD là một vấn đề về kỷ luật. Thực tế, trọng tâm của hỗ trợ REST trong Rails là một kỹ thuật để tạo các gói tuyến đường có tên tự động—các tuyến đường được gói gọn lại để trỏ đến một tập hợp các hành động cụ thể, đã được xác định trước. Đây là logic. Việc đặt tên hành động dựa trên CRUD là tốt. Sử dụng các tuyến đường có tên là tiện lợi và thanh lịch. Hỗ trợ REST trong Rails cung cấp cho bạn các tuyến đường có tên trỏ đến các tên hành động dựa trên CRUD.

Ví dụ khi bỏ code resources :auctions vào tệp config/routes.rb sẽ tạo ra sẽ tạo ra bốn tuyến đường có tên, mà theo cách sẽ được mô tả trong chương này, kết nối với bảy hành động của controller. Và những hành động đó có tên giống như CRUD.

Trong Rails khi nhắc đến tài nguyên (resource) là nhắc đến phương thức resources ví dụ resources :books .Vơi phương thức này ta có không chỉ đơn thuần là các biễu diễn của tài nguyên mà là cả một Book model, một  book controller với một tập hợp các hành động CRUD, và một số tuyến đường có tên liên quan đến bộ điều khiển đó. 

The Standard RESTfulController Actions

Khi bạn gọi resources :auctions, bạn đang ký một loại thỏa thuận với hệ thống định tuyến. Hệ thống sẽ cung cấp cho bạn bốn tuyến đường có tên. Giữa chúng, bốn tuyến đường này trỏ đến bảy hành động của controller, phụ thuộc vào phương thức yêu cầu HTTP. Đổi lại, bạn đồng ý sử dụng các tên hành động rất cụ thể cho controller của bạn: index, create, show, update, destroy, new, edit. Các tên này rất dễ đọc và tương tự như CRUD.

Ta có hành động đi với các phương thức lần lượt như sau

 - GET: index, show, new, edit
 - POST: create
 - PUT/PATCH: update
 - DELETE: destroy

Vì các tên đường dẫn được kết hợp với phương thức yêu cầu HTTP, bạn cần biết cách chỉ định phương thức yêu cầu khi bạn tạo ra một URL để mà các yêu cầu GET và POST cho clients_url của bạn không kích hoạt cùng một hành động của controller. Hầu hết những gì bạn cần làm trong vấn đề này có thể được tóm tắt trong vài quy tắc:

 - Phương thức yêu cầu mặc định là GET.
 - Khi thêm  form_with , phương thức POST sẽ được sử dụng tự động.
 - Khi cần thiết (điều này chủ yếu xảy ra với các hoạt động PATCH và DELETE), bạn có thể chỉ định phương thức yêu cầu cùng với URL được tạo ra bởi tên đường dẫn có tên.

Một ví dụ cụ thể khi cần chỉ định hoạt động DELETE là khi bạn muốn kích hoạt hành động
destroy với một biểu mẫu:

 form_with url: auction_path(auction), method: :delete do |f|

Sự khác nhau giữa PATCH và PUT

 - PATCH được sử dụng để áp dụng cập nhật một phần cho tài nguyên, nghĩa là chỉ những trường cần thay đổi mới được gửi trong nội dung yêu cầu.
 - PUT được sử dụng để thay thế toàn bộ tài nguyên bằng một cách thể hiện mới, nghĩa là tất cả các trường của tài nguyên đều được gửi trong body yêu cầu, ngay cả khi chúng không được sửa đổi.

Khi cập nhật một tài nguyên trong Rails, bạn hiếm khi thay thế hoàn toàn nó mà thay vào đó là cập nhật một hoặc nhiều thuộc tính. Do đó, yêu cầu PATCH phù hợp hơn với ý nghĩa của hành động cập nhật điển hình trong Rails.

Singular and Plural RESTful Routes

một số tuyến đường RESTful là số ít; một số là số nhiều. Lý do là như sau:

 - Các tuyến đường cho các hành động show, new, edit và destroy là số ít vì chúng hoạt động trên một tài nguyên cụ thể.
 - Các tuyến đường còn lại là số nhiều. Chúng xử lý với các bộ sưu tập các tài nguyên liên quan.

Các tuyến đường RESTful số ít yêu cầu một đối số vì chúng cần có thể tìm ra id của thành viên trong bộ sưu tập được tham chiếu.

 item_url(item)

Bạn không cần phải gọi phương thức id trên item. Rails sẽ tự động xác định nó (bằng cách gọi to_param trên đối tượng được truyền vào).

The Special Pairs: new/create and edit/update

new và edit tuân theo các quy ước đặt tên RESTful đặc biệt. Lý do cho điều này liên quan đến cách create và update hoạt động và cách new và edit liên quan đến chúng. Thông thường, các thao tác create và update bao gồm việc gửi một biểu mẫu. Điều này có nghĩa là chúng thực sự bao gồm hai hành động—hai yêu cầu—mỗi cặp:

 - Hành động dẫn đến việc hiển thị biểu mẫu
 - Hành động xử lý đầu vào của biểu mẫu khi biểu mẫu được gửi

Do đó, chúng ta có các cặp hành động như sau:

 - new: Hiển thị biểu mẫu để tạo một tài nguyên mới.
 - create: Xử lý dữ liệu biểu mẫu và thực hiện việc tạo tài nguyên.
 - edit: Hiển thị biểu mẫu để chỉnh sửa một tài nguyên hiện có.
 - update: Xử lý dữ liệu biểu mẫu và thực hiện việc cập nhật tài nguyên.

Các hành động new và edit là cần thiết để chuẩn bị dữ liệu cho các hành động create và update tương ứng. 

Điểm mấu chốt, như được thực hiện trong RESTful Rails, là: Hành động new được hiểu là cung cấp cho bạn một tài nguyên mới, số ít (khác với số nhiều). Tuy nhiên, vì động từ logic cho giao dịch này là GET, và GETting một tài nguyên đơn lẻ đã được dành cho
hành động show, nên new cần một tuyến đường có tên riêng của nó.

link_to "Create a new item", new_item_path

Cũng tương tự hành động edit sử dụng cùng một URL như show, nhưng với một loại biến đổi, dưới dạng /edit, đính kèm ở cuối, giống với định dạng URL cho new:

Ví dụ:

/items/5/edit

Tuyến đường có tên tương ứng là edit_item_url(@item).

The PATCH and DELETE Cheat

Hầu hết các HTTP client đều có thể sử dụng các động từ này, nhưng các biểu mẫu trong trình duyệt web chỉ có thể được gửi bằng GET hoặc POST do tiêu chuẩn HTML chỉ cho phép hai động từ này trong các biểu mẫu nên Rails cung cấp một cách giải quyết. Một yêu cầu PATCH hoặc DELETE thực sự là một yêu cầu POST với một trường ẩn gọi là _method được đặt thành "patch" hoặc "delete". Ứng dụng Rails xử lý yêu cầu này sẽ nhận ra và định tuyến yêu cầu tương ứng đến hành động update hoặc destroy.


 form_with model: @item, method: :patch do |f|

  <%= f.submit "Update Item" %>

 end
 
 form_with url: item_path(@item), method: :delete do
 
  <%= submit_tag "Delete Item" %>

 end

Limiting Routes Generated

Bạn có thể thêm các tùy chọn :except và :only vào resources để giới hạn các tuyến đường được tạo ra.

resources :clients, except: [:index]

resources :clients, only: [:new, :create]

Singular Resource Routes

Ngoài resources, còn có một dạng tuyến đường tài nguyên đơn (singleton): resource. Nó được sử dụng để đại diện cho một tài nguyên chỉ tồn tại một lần trong ngữ cảnh cụ thể của nó. Ví dụ là một hồ sơ cá nhân cho mỗi người dùng. Khi bạn sử dụng resource, bạn sẽ nhận được hầu hết các tuyến đường tài nguyên đầy đủ, ngoại trừ tuyến đường dành cho tập hợp (collection route - index). Lưu ý rằng tên phương thức resource, tham số cho phương thức đó, và tất cả các tuyến đường được tạo ra đều ở dạng số ít.

resource :profile

Cụ thể, bạn sẽ nhận được các tuyến đường sau:

GET /profile → profiles#show

GET /profile/new → profiles#new

POST /profile → profiles#create

GET /profile/edit → profiles#edit

PATCH/PUT /profile → profiles#update

DELETE /profile → profiles#destroy

Nested Resources

Khi làm việc với các tài nguyên lồng nhau, bạn tạo ra một cấu trúc phân cấp trong các URL để biểu diễn mối quan hệ giữa các tài nguyên. Điều này đặc biệt hữu ích khi một tài nguyên gắn liền với một tài nguyên khác. Trong ví dụ của bạn, một bid (đấu giá) thuộc về một auction (cuộc đấu giá), vì vậy hợp lý khi lồng các bids trong auctions trong các routes của bạn. Để tạo các routes tài nguyên lồng nhau, bạn có thể thêm đoạn sau vào tệp config/routes.rb

 resources :auctions do

  resources :bids

 end

Giải Thích:

 - resources :auctions định nghĩa các routes tiêu chuẩn cho tài nguyên auctions (các phiên đấu giá). Nó sẽ tạo ra các routes cho các hành động CRUD  (Create, Read, Update, Delete) như index, show, new, create, edit, update, và destroy.

 - resources :bids bên trong block resources :auctions định nghĩa các routes tiêu chuẩn cho tài nguyên bids (các đấu thầu) và đặt chúng trong ngữ cảnh của tài nguyên cha auctions. Điều này có nghĩa là các routes cho bids sẽ phụ thuộc vào auctions, tức là bạn sẽ có các URL dạng như /auctions/:auction_id/bids.

Tuy nhiên, lệnh tài nguyên lồng nhau cũng bao hàm rằng bạn đang thực hiện một lời hứa. Bạn đang hứa rằng bất cứ khi nào bạn sử dụng các helper route có tên cho bid, bạn sẽ cung cấp một tài nguyên auction để chúng có thể được lồng vào. Trong mã ứng dụng của bạn, điều này dịch thành một tham số cho phương thức route có tên:

link_to "See all bids", auction_bids_path(auction)

Các tài nguyên không nên được lồng nhau quá một cấp độ sâu. Các phương thức trợ giúp cho các đường dẫn lồng nhau hơn hai cấp độ trở nên dài và khó quản lý. Rất dễ mắc lỗi với chúng và khó tìm ra lỗi khi chúng không hoạt động như mong đợi. Lý do? Các URL kết quả ngắn hơn và các phương thức trợ giúp dễ làm việc hơn.

resource routes chấp nhận một tùy chọn :shallow giúp rút ngắn các URL khi có thể. Mục tiêu là bỏ qua các đoạn URL của bộ sưu tập cha (parent collection) khi chúng không cần thiết. Kết quả cuối cùng là chỉ các tuyến lồng nhau cho các hành động :index :create, và :new được tạo ra.

 resources :auctions, shallow: true do

  resources :bids do

   resources :comments

  end

 end

Routing Concerns

Một trong những nguyên tắc cơ bản mà các lập trình viên Rails tuân theo là Don’t Repeat Yourself (DRY - Đừng lặp lại chính mình). Tuy nhiên, file config/routes.rb vẫn có thể dễ bị lặp lại dưới dạng các tuyến lồng nhau được chia sẻ giữa nhiều tài nguyên. Ví dụ, giả sử trong ví dụ liên tục của chúng ta, cả auctions và bids đều có thể có các comments liên kết với chúng.

 resources :auctions do
 
  resources :comments

 end

 resources :bids do
 
  resources :comments

 end

Rails cung cấp một cách để tránh lặp lại bằng cách sử dụng concerns. Bạn có thể định nghĩa các tuyến chia sẻ trong một concern và sau đó bao gồm concern đó trong các tài nguyên khác nhau.

Đầu tiên, bạn định nghĩa một concern cho các comments:

 concern :commentable do
 
  resources :comments

 end

Sau đó, bạn có thể bao gồm concern đó trong các tài nguyên khác nhau:

 resources :auctions, concerns: :commentable

 resources :bids, concerns: :commentable

Bằng cách này, bạn tránh được sự lặp lại và giữ cho file config/routes.rb của bạn gọn gàng và dễ bảo trì hơn.

RESTful Route Customizations

Có hai loại hành động tùy chỉnh: hành động thành viên (member actions) và hành động tập hợp (collection actions).

Menber actions: ví dụ đoạn code sau

 resources :auctions do
 
  member do
   
   post 'mark_as_ended'
 
  end

 end

Giải thích:

 - member do ... end: Khối member được sử dụng để định nghĩa các đường dẫn tùy chỉnh cho một thành viên cụ thể của tài nguyên. Các đường dẫn được tạo ra sẽ chứa id của tài nguyên trong URL.

 - post 'mark_as_ended': Định nghĩa một route tùy chỉnh mark_as_ended sử dụng phương thức HTTP POST.Đường dẫn này sẽ có dạng /auctions/:id/mark_as_ended, nơi :id là id của phiên đấu giá cụ thể mà bạn muốn đánh dấu là đã kết thúc.

Collection actions: ví dụ đoạn code sau

 resources :auctions do

  collection do
   
   get 'search'
 
  end

 end

Giải thích:

 - collection do ... end: Khối collection được sử dụng để định nghĩa các đường dẫn tùy chỉnh cho toàn bộ bộ sưu tập của tài nguyên. Các đường dẫn này không yêu cầu id của một phiên đấu giá cụ thể trong URL.

 - get 'search': Định nghĩa một route tùy chỉnh search sử dụng phương thức HTTP GET.Đường dẫn này sẽ có dạng /auctions/search, không cần id của phiên đấu giá cụ thể.

Controller-Only Resources

một tài nguyên REST không nhất thiết phải ánh xạ trực tiếp vào một controller. Bạn có thể, nếu muốn, cung cấp các dịch vụ REST mà các định danh công khai của chúng (URI) không khớp với tên của các controller của bạn.

The RESTful Rails Action Set
 
 - Index: Hiển thị danh sách các tài nguyên.
 - Show: Hiển thị thông tin chi tiết về một tài nguyên cụ thể. 
 - Create: Hiển thị form để tạo mới một tài nguyên.
 - New: Tạo mới một đối tượng tài nguyên (không phải là hành động RESTful riêng biệt nhưng thường đi kèm với Create).
 - Edit: Hiển thị form để chỉnh sửa thông tin của một tài nguyên.
 - Update: Cập nhật thông tin của một tài nguyên sau khi chỉnh sửa.
 - Destroy: Xóa bỏ một tài nguyên khỏi hệ thống.
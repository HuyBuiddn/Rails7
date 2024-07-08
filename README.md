Chapter 1- Rails configurations and environments

Generating a new Rails Application and Bundler

Để tạo 1 ứng dụng Rails, chạy rails new awesome-name với database mặc định là sqlite3
thêm -d nếu muốn tuỳ chỉnh database.

Nếu muốn loại trừ một số thành phần của Rails, có thể thêm --skip-

Lệnh ví dụ:

rails new awesome-name -d postgresql --skip-action-mailer --skip-action-mailbox --skip-action-text --skip-active-storage --skip-action-cable --skip-test --skip-jbuilder

Gemfile và Gemfile.lock là gì, khác nhau như thế nào?

Xây dựng 1 dự án trên rails là xây dựng các gem cần cho dự án đó.

Gemfile là tệp lưu trữ các gem mà người lập trình muốn sử dụng cho dự án.

Nội dung Gemfile chứa các khai báo gem và nguồn cung cấp gem. Ví dụ:

source 'https://rubygems.org '

gem 'rails', '~> 6.1.3'
gem 'pg', '>= 1.1', '< 2.0'
gem 'puma', '~> 5.0'

Gemfile.lock là liệt kê cụ thể các phiên bản gem đã được cài đặt, cũng như các phụ thuộc của chúng. Ví dụ:

GEM
remote: https://rubygems.org/
specs:
pg (1.2.3)
puma (5.2.1)
rails (6.1.3)
actioncable (= 6.1.3)
actionmailbox (= 6.1.3)
actionmailer (= 6.1.3)
actionpack (= 6.1.3)
actiontext (= 6.1.3)
actionview (= 6.1.3)
activejob (= 6.1.3)
activemodel (= 6.1.3)
activerecord (= 6.1.3)
activestorage (= 6.1.3)
activesupport (= 6.1.3)

Só sánh 2 ví dụ. Ta thấy với yêu cầu gem ‘rails’ version 6.1.3 trong Gemfile

trong Gemfile.lock được cài đặt các phụ thuộc đi kèm như  actioncable (= 6.1.3), actionmailbox (= 6.1.3) hay với yêu cầu gem 'puma', '~> 5.0' trong  Gemfile.lock được cài đặt phiên bản puma (5.2.1)

Câu hỏi đặt ra là làm sao để tương tác giữa Gemfile và Gemfile.lock.

Sử dụng công cụ Bundler. Bundler là công cụ hoặc thư viện được sử dụng để quản lý các phụ thuộc của một ứng dụng Ruby. Nó đảm bảo rằng bạn có các phiên bản đúng của các gem cần thiết cho ứng dụng của bạn và giúp duy trì các môi trường phát triển và triển khai nhất quán.

Gemfile.lock là tệp được tự động tạo ra và quản lý bởi Bundler. Nó ghi lại chính xác phiên bản của các gem (và các phụ thuộc của chúng) mà Bundler đã cài đặt, đảm bảo tính nhất quán giữa các lần cài đặt.

bundle là lệnh dòng lệnh (command line) được cung cấp bởi Bundler. Lệnh này được sử dụng để tương tác với Bundler, bao gồm việc cài đặt các gem (bundle install), cập nhật gem (bundle update), kiểm tra phiên bản gem (bundle check), và nhiều chức năng khác.

Sử dụng lệnh bundle install hoặc bundle update : Bundler sẽ đọc Gemfile, giải quyết các phụ thuộc và ghi lại các phiên bản cụ thể của các gem và phụ thuộc của chúng vào Gemfile.lock

Với quy trình hoạt động như trên Gemfile.lock: Được sử dụng để khóa các phiên bản gem mà Bundler đã cài đặt, đảm bảo rằng mọi lần cài đặt sau đó sẽ sử dụng cùng một phiên bản gem để duy trì tính nhất quán. Khi chia sẻ hoặc triển khai dự án, chia sẻ tệp Gemfile.lock đảm bảo rằng các đồng nghiệp hoặc các máy chủ triển khai sẽ cài đặt đúng các phiên bản gem giống như bạn.

bundle exec là một lệnh của Bundler trong Ruby, được sử dụng để đảm bảo rằng các lệnh bạn chạy sử dụng đúng phiên bản của các gem được chỉ định trong tệp Gemfile của dự án. Khi bạn chạy một lệnh với bundle exec , Bundler điều chỉnh đường dẫn load Ruby và đường dẫn thực thi để các gem được sử dụng là những gem được chỉ định trong dự án, thay vì các gem cài đặt toàn cục trên hệ thống. Ví dụ:

bundle exec rails server

Lệnh này sẽ chạy rails server với các gem được chỉ định trong Gemfile và Gemfile.lock của dự án.

Để tránh dài dòng phải thêm bundle exec mỗi lần vào lệnh ta sử dụng Binstubs. Để tạo binstubs cho một gem cụ thể, bạn sử dụng lệnh bundle binstubs. Ví dụ:** bundle binstubs rails**

Điều này sẽ tạo ra một file binstub bin/rails. Bây giờ, thay vì chạy bundle exec rails server, bạn chỉ cần chạy: bin/rails server

RSpec and Haml

là 2 gem cần thiết cài đặt khi bắt đầu mỗi dự án.

RSpec là một framework kiểm thử phần mềm (testing framework). RSpec sử dụng một ngôn ngữ gần với tiếng Anh để mô tả các kiểm thử, giúp làm cho mã kiểm thử dễ đọc và dễ hiểu. RSpec tập trung vào việc kiểm thử hành vi của ứng dụng từ góc độ của người dùng cuối. Điều này giúp đảm bảo rằng ứng dụng hoạt động đúng theo các kỳ vọng của người dùng.

Haml là một ngôn ngữ đánh dấu cung cấp một cú pháp ngắn gọn hơn so với HTML truyền thống, giúp giảm số lượng ký tự cần viết và làm cho mã nguồn trở nên dễ đọc hơn.

Running a Rails application

Khi call lệnh rails là mở tệp bin/rails chạy các lệnh trong đó

APP_PATH = File.expand_path("../config/application", __dir__)
require_relative "../config/boot"
require "rails/commands"

Set up đường dẫn tuyệt đối từ thư mục bin/rails hiện tại đến thư mục config/application, trỏ đường dẫn tương đối đến thư mục config/boot, và chạy lệnh require yêu cầu Ruby tải hết các lệnh mặc định của rails vào ứng dụng.

Thư mục config/boot

ENV['BUNDLE_GEMFILE'] ||= File.expand_path('../Gemfile', __dir__)
require 'bundler/setup' # Set up gems listed in the Gemfile.
require 'bootsnap/setup' # Speed up boot time by caching expensive operations.

Sử dụng biến môi trường và toán tử ||= để gán giá trị cho gemfile

Điều này giúp tự động xác định đường dẫn đến tệp Gemfile của dự án mà không cần phải cung cấp đường dẫn cứng cố định trong mã. Điều này hữu ích khi dự án của bạn có thể được di chuyển giữa các môi trường khác nhau mà không cần phải thay đổi mã.

đưa Bundler vào ứng dụng để quản lý gem và bootsnap để tăng tốc độ khởi động ứng dụng Ruby.

Thư mục config/application

require_relative 'boot'

require 'rails/all'

*Bundler.require(Rails.groups)

module TimeAndExpenses

 class Application < Rails::Application

  config.load_defaults 7.0

 end

end

tải toàn bộ các thành phần của Rails. *Bundler.require(Rails.groups) sẽ tải tất cả các gem được định nghĩa trong các nhóm môi trường tương ứng trong file Gemfile. Giả sử có Gemfile như sau:

source 'https://rubygems.org '

gem 'rails'

group :development do
gem 'pry'
end

group :test do
gem 'rspec-rails'
end

Khi ứng dụng chạy trong môi trường Test sẽ tải gem rails và rspec-rails.

định nghĩa một mô-đun TimeAndExpenses chứa lớp Application, kế thừa từ Rails::Application. Trong lớp Application, phương thức config.load_defaults 7.0 được gọi để thiết lập các giá trị mặc định cho phiên bản Rails 7.0. Tạo ra một module cụ thể cho ứng dụng của bạn giúp tạo ra nền tảng cho việc chạy nhiều ứng dụng Rails trong cùng một quá trình Ruby

Default Initializers

"initializers" là các file Ruby được đặt trong thư mục config/initializers. Chúng chứa các cấu hình và mã khởi tạo cần thiết cho ứng dụng. Rails cung cấp một số initializers mặc định khi bạn tạo một ứng dụng mới

Other Common Settings

có thể thêm các thiết lập khác trong config/application.rb hoặc initializer
nếu muốn đặt trong initializer phải tiền tố các cấu hình với Rails.application.

Zeitwerk

Zeitwerk là một autoloader mặc định cho các ứng dụng Rails (kể từ Rails 6), giúp quản lý việc tải các tệp Ruby một cách tự động và hiệu quả. Nó được thiết kế để thay thế cơ chế autoloading trước đây trong Rails và mang lại nhiều cải tiến quan trọng.

Quy ước đặt tên

a. Không Lồng (Non-nested Classes/Modules): Rails sẽ chèn dấu gạch dưới (underscore) giữa các tên của hằng số

vi du: EstimationCalculator thành estimation_calculator.rb

b.Lồng (Nested Classes/Modules):

Ví dụ: module Admin
class User
end
end

thành admin/user.rb

Development Mode

Môi trường lập trình với các tính năng nổi bât đc rail cung cấp như Caching,

Automatic Class Reloading, Error Reports, Server Timing , Active Storage Settings

Test Mode

cung cấp các công cụ và framework testing để bạn có thể viết và chạy các test case cho mọi phần của ứng dụng một cách tự động.

Production Mode

là môi trường được sử dụng khi ứng dụng của bạn đã được triển khai và đang chạy trên một máy chủ hoặc môi trường sản xuất thực tế.

Configuring Application Secrets

chạy lệnh rails secret để tạo khoá bảo mật mới rồi chạy rails credentials:edit để chỉnh sửa credentials và thêm khoá bảo mật mới.

Configuring a Database

config/database.yml là tệp chỉ định tất cả các cài đặt cấu hình cần thiết bởi Active Record để kết nối đến cơ sở dữ liệu.

Logging

là quá trình ghi lại các sự kiện và thông điệp trong quá trình chạy ứng dụng. Logger trong Rails có thể được sử dụng để ghi lại các sự kiện với các mức độ nghiêm trọng khác nhau, từ debug đến fatal. Các thông điệp log có thể cung cấp thông tin hữu ích cho việc gỡ lỗi, theo dõi hiệu suất ứng dụng, hoặc giúp phát hiện và xử lý các vấn đề. Thông thường, các thông điệp log sẽ được ghi vào các tệp log tương ứng với mỗi môi trường, chẳng hạn như development, test, và production. Điều này giúp quản lý và phân tích log dễ dàng hơn.

Default Gems

các gem mặc định khi xây dựng 1 ứng dụng Rails.
các gem mặc định khi xây dựng 1 ứng dụng Rails.
các gem mặc định khi xây dựng 1 ứng dụng Rails.
các gem mặc định khi xây dựng 1 ứng dụng Rails.

Rack

Rack là một giao diện trung gian (middleware interface) trong Ruby được sử dụng để xây dựng các ứng dụng web. Nó cung cấp một cách tiêu chuẩn để xử lý các yêu cầu HTTP và tạo ra các phản hồi tương ứng. Mỗi ứng dụng Rack là một hàm Ruby nhận một đối tượng "env" chứa thông tin về yêu cầu HTTP và trả về một mảng chứa ba phần tử: mã trạng thái HTTP, các tiêu đề HTTP và nội dung phản hồi. Các ứng dụng Rack có thể được xếp chồng lên nhau để tạo thành các ứng dụng lớn hơn, mỗi ứng dụng đảm nhận một phần của xử lý yêu cầu.

Different between eagerloading and autoloading

Eager loading và auto loading là hai khái niệm liên quan đến cách thức nạp dữ liệu trong các framework phát triển ứng dụng, đặc biệt là trong các framework như Ruby on Rails.

 Eager Loading:

  - Khái niệm: Eager loading là kỹ thuật nạp trước dữ liệu liên quan từ database trong một lần truy vấn duy nhất.
  - Cách thức: Khi bạn thực hiện eager loading, bạn sử dụng các phương pháp như includes trong Rails để nạp trước các dữ liệu liên quan.
  - Lợi ích: Giảm số lượng truy vấn đến database (N+1 query problem), giúp tăng hiệu suất khi cần truy xuất dữ liệu liên quan
  - vi du:  @posts = Post.includes(:comments)

     Truy vấn trên sẽ nạp tất cả các bài viết cùng với các bình luận liên quan trong một truy vấn duy nhất.

 Auto Loading:

  - Khái niệm: Auto loading là kỹ thuật tự động nạp các file mã nguồn khi chúng được yêu cầu lần đầu tiên trong quá trình runtime.
  - Cách thức: Thường được thiết lập trong môi trường phát triển và sản xuất để tự động tìm kiếm và nạp các file khi chúng được gọi.
  - Lợi ích: Giảm thời gian khởi động ứng dụng, vì các file không cần được nạp trước khi cần thiết.
  - Ví dụ: Khi bạn gọi một class trong Rails mà class đó chưa được nạp, auto loading sẽ tự động tìm và nạp file chứa class đó.

    class User < ApplicationRecord

     # Some code

    end

    Nếu bạn gọi User lần đầu tiên, Rails sẽ tự động nạp file user.rb.

 Tóm lại:

  - Eager Loading: Nạp dữ liệu liên quan từ database trong một truy vấn duy nhất để tăng hiệu suất khi xử lý dữ liệu liên quan.

  - Auto Loading: Tự động nạp các file mã nguồn khi chúng được yêu cầu trong quá trình runtime, giúp giảm thời gian khởi động ứng dụng.

  Cả hai khái niệm này đều nhằm mục đích tối ưu hóa hiệu suất, nhưng chúng được áp dụng trong các bối cảnh khác nhau: eager loading tập trung vào việc tối ưu hóa truy vấn database, trong khi auto loading tập trung vào việc quản lý mã nguồn trong quá trình runtime.

Chapter2

Định tuyến trong Rails là kiểm tra URL(địa chỉ tham chiếu tài nguyên) của 1 request và xác định 1 hành động controller nào được thực hiện. Việc xác định đúng hành động nào cần được thực thi là quan trọng nhất. Cần xây dựng 1 bộ quy tắc và bộ quy tắc này được lưu trong file routes.rb.


1 Routes được xây dựng phải đảm bảo được 2 yếu tố đó là phải cung cấp đủ thông tin để vừa khớp với một URL hiện có vừa tạo ra một URL mới. Về cấu trúc của Routes:


 - Phương thức HTTP (GET, POST, PUT, PATCH, DELETE,v.v.).


 - Phải xác định được 1 Patterns (mẫu) để match được với URL cũ cũng như dựa vào nó tạo ra URL mới. Một Patterns có thể bao gồm 


    -  Static String (chuỗi tĩnh) có thể hiểu như là 1 biến được khai báo 1 lần và được lưu trữ trong bộ nhớ suốt thời gian chạy của chương trình


    -  Dấu gạch chéo (/) mô phỏng cú pháp URL


    -  Segment Keys (Khoá phân đoạn) một khái niệm được sử dụng trong quản lý dữ liệu, đặc biệt là trong các hệ thống cơ sở dữ liệu, phân tích dữ liệu, và lập chỉ mục (indexing).Khóa phân đoạn thường được dùng để phân chia và tổ chức dữ liệu thành các phân đoạn (segments) hoặc nhóm nhỏ hơn để tối ưu hóa việc truy cập và quản lý dữ liệu. 

 - Chỉ định controller và action mà route sẽ ánh xạ đến.

 Ví dụ:  get "recipes/:ingredient" => "recipes#index

 · get: phương thức HTTP mà route này sẽ xử lý, trong trường hợp
   này là GET.


 · "recipes/:ingredient": Đây là URL pattern, trong đó : recipes là 1
    chuỗi tĩnh :ingredient là khoá phân đoạn. Bất kỳ giá trị nào được truyền vào phần định danh này của URL sẽ được chuyển đến hành động index trong controller Recipes.


 · "recipes#index": Đây là định danh của controller và hành động trong controller sẽ xử lý yêu cầu này. Trong trường hợp này, nó chỉ ra rằng yêu cầu sẽ được xử lý bởi hành động index trong controller Recipes.

Routes.rb

 Các routes được định nghĩa trong tệp config/routes.rb. File này được tạo khi khởi động 1 dự án Rails.

 Trong file hiện tại đang có

  Rails.application.routes.draw do

  end

 Đây là khối mã để định nghĩa các tuyến đường cho ứng dụng Ruby on Rails. Tất cả các định nghĩa tuyến đường sẽ được đặt bên trong khối này.

Regular Routes

 Như đã mô tả ở trên các cơ bản để định nghĩa 1 tuyến là cung cấp 1 mẫu URL, tên lớp controller với tên hành động và cuối cùng là phương thức HTTP mong muốn.

   match "products", controller: "products", action: "index", via: :get

   Giải thích chi tiết
   - match: Đây là một phương thức trong Rails để định nghĩa một tuyến đường. match có thể được sử dụng để ánh xạ một URL đến một hành động controller cho nhiều phương thức HTTP (GET, POST, PUT, PATCH, DELETE), tùy theo tùy chọn via.
   - "products": Đây là mẫu URL mà tuyến đường này sẽ khớp. Trong trường hợp này, bất kỳ yêu cầu nào đến /products sẽ được khớp với tuyến đường này.
   - controller: "products": Đây là tên của controller mà yêu cầu sẽ được chuyển đến Trong trường hợp này, nó là ProductsController.
   - action: "index": Đây là tên của hành động trong controller sẽ được gọi. Trong trường hợp này, nó là hành động index.
   - via: :get: Điều này chỉ ra rằng tuyến đường này sẽ xử lý các yêu cầu HTTP GET.
 
 Định nghĩa một tuyến mà không chỉ định phương thức HTTP sẽ dẫn đến việc Rails ném ra ngoại lệ ArgumentError. Do đó, bạn cần phải giới hạn phương thức HTTP được sử dụng để truy cập một tuyến.
 
 Nếu, vì lý do nào đó, bạn muốn giới hạn một tuyến cho nhiều hơn một phương thức HTTP, bạn có thể truyền một mảng các tên động từ (verb) cho :via. Kết hợp với đoạn code trong file routes.rb ta có

  Rails.application.routes.draw do

   match "products", controller: "products", action: "index", via: :get

  end

 đây là 1 ví dụ về routes trong rails.
 
 match "products", controller: "products", action: "index", via: :get

 đoạn code trên có thể được rút ngắn thay vì cung cấp lớp controller và hành động riêng biệt, có thể sử dụng một chuỗi ánh xạ với tham số đặc biệt :to:
 
 match "products", to: "products#index", via: :get vì tùy chọn to rất phổ biến, một dạng viết tắt được cung cấp:

 match "products" => "products#index", via: :get Rails cung cấp thêm một dạng viết tắt nữa bằng cách thay thế match bằng phương thức HTTP mong muốn (như get, post, patch, v.v.):

 get "products" => "products#index"

Segment Keys (khoá phân đoạn)

 Chuỗi mẫu URL có thể chứa các tham số (được ký hiệu bằng dấu hai chấm) được gọi là khóa phân đoạn. Trong khai báo tuyến sau đây, :id là một khóa phân đoạn:

  get "products/:id" => "products#show"

 Khi tuyến này khớp với một URL yêu cầu, phần :id của mẫu hoạt động như một loại trình khớp và lấy giá trị của phân đoạn đó. Ví dụ, sử dụng ví dụ trên, giá trị của id cho URL sau sẽ là 4: http://example.com/products/4. Điều này có nghĩa là giá trị của params[:id] sẽ được thiết lập thành chuỗi "4". Bạn có thể truy cập giá trị đó bên trong hành động products#show.

 Trong View (app/views/some_view.html.erb)

 Khi bạn tạo một URL, bạn phải cung cấp các giá trị sẽ gắn vào các khóa phân đoạn bên trong chuỗi mẫu URL. Cách đơn giản nhất để hiểu (và nguyên bản) là sử dụng một hash, như sau:

  link_to "Products",

  controller: "products",

  action: "show",

  id: 1

 link_to: Đây là một phương thức trợ giúp (helper method) trong Rails để tạo ra một liên kết HTML.

 Cách hoạt động

 Khi người dùng nhấp vào liên kết, một yêu cầu HTTP GET sẽ được gửi đến URL /products/1. Rails sẽ ánh xạ yêu cầu này đến hành động show trong ProductsController, với params[:id] bằng 1. Hành động show trong ProductsController sẽ sử dụng params[:id] để tìm và hiển thị chi tiết của sản phẩm có ID là 1.

 Spotlight on the :id Field

 Trong Controller (app/controllers/products_controller.rb)

 Controller chịu trách nhiệm xử lý các yêu cầu và trả về phản hồi thích hợp

  class ProductsController < ApplicationController

   def show

    @product = Product.find(params[:id])

   end

  end

 Giải thích chi tiết
 - class ProductsController < ApplicationController:
 - Định nghĩa một controller mới có tên là ProductsController.
 - Controller này kế thừa từ ApplicationController, vì vậy nó sẽ có tất cả các phương thức và tính năng của ApplicationController.
 - def show:
 - Định nghĩa một hành động trong controller có tên là show. Hành động này sẽ được gọi khi có một yêu cầu HTTP GET đến một URL tương ứng với hành động show (thường là /products/:id).
 - @product = Product.find(params[:id]):
 - Tìm một bản ghi Product từ cơ sở dữ liệu dựa trên id được truyền qua URL (thông qua params[:id]).
 - params[:id] lấy giá trị của tham số id từ yêu cầu URL.
 - Product.find là một phương thức Active Record để tìm bản ghi theo id.
 - Bản ghi tìm được sẽ được gán cho biến instance @product, biến này có thể được sử dụng trong view tương ứng để hiển thị dữ liệu.

Optional Segment Keys (Khoá phân đoạn tuỳ chọn)

 Bạn có thể định nghĩa một khóa phân đoạn là tùy chọn bằng cách đặt nó trong dấu ngoặc đơn 

  get "products(/:id)" => 'products#display

 Điều này sẽ khớp với cả /products cũng như các đường dẫn như /products/15.

Segment Key Constraints (Ràng buộc khoá phân đoạn)

 Đôi khi bạn muốn không chỉ nhận dạng một tuyến mà còn nhận dạng nó ở mức độ chi tiết hơn so với chỉ những thành phần hoặc trường nó có. Bạn có thể thực hiện điều này thông qua việc sử dụng tùy chọn :constraints

  get "products/:id" => "products#show", constraints: {:id => /\d+/}

  get "products/:id" => "products#show_error

 Ở ví dụ trên bạn có thể định tuyến tất cả các yêu cầu show để chúng đi đến một hành động error nếu trường id của chúng không phải là số.

Rút gọn Ràng Buộc

 Việc thiết lập ràng buộc trên tham số :id là rất phổ biến, do đó Rails cho phép bạn rút gọn ví dụ trước đó của chúng ta thành:

  get "products/:id" => "products#show", id: /\d+/

  get "products/:id" => "products#show_error"

Ràng Buộc trên Các Thuộc Tính Yêu Cầu Khác

 Từ ví dụ, bạn có thể kết luận rằng việc kiểm tra :constraints áp dụng cho các phần tử của hash params. Tuy nhiên, bạn cũng có thể kiểm tra một loạt các thuộc tính yêu cầu khác trả về một chuỗi, chẳng hạn như :subdomain và :referrer.

  get "products/:id" => "products#show", constraints: { subdomain: 'admin' }

  constraints: { subdomain: 'admin' }: Đây là phần quan trọng của đoạn mã và chỉ ra ràng buộc (constraints) đối với subdomain. Cụ thể là:
  - Tuyến đường này chỉ áp dụng khi subdomain là 'admin'.
  - Nghĩa là yêu cầu chỉ được định tuyến đến hành động show trong ProductsController nếu subdomain của URL là 'admin'.

Defining Defaults

 Bạn có thể định nghĩa các tham số mặc định trong một tuyến bằng cách cung cấp một hash cho tùy chọn :defaults. Điều này còn áp dụng cho các tham số mà bạn không chỉ định là các phân đoạn động trong tuyến chính nó.

  get "photos/:id", to: "photos#show", defaults: { format: "jpg" }

 Trong ví dụ trên, Rails sẽ khớp http://example.com/photos/12 với hành động show của PhotosController, và thiết lập params[:format] thành "jpg". Vì lý do bảo mật, bạn không thể ghi đè lên các giá trị mặc định bằng cách thay đổi các giá trị trong đối tượng params.

Redirect Routes

 phương thức redirect: chuyển hướng của tuyến.

  - Chuyển hướng đến một URL khác
    get "/google", to: redirect("https://google.com/")

  - Sử dụng block trong chuyển hướng
    Phương thức redirect cũng có thể nhận một block, mà nhận các tham số của yêu cầu làm đối số của nó. Điều này cho phép bạn thực hiện các phiên bản nhanh của các điểm cuối API dịch vụ web chẳng hạn:

    match "/api/v1/:api",

    to: redirect { |params| "/api/v2/#{params[:api].pluralize}" },

    via: [:get, :post]


    to: redirect { |params| "/api/v2/#{params[:api].pluralize}" }:

    Chỉ định rằng khi có yêu cầu đến URL /api/v1/:api, hệ thống sẽ thực hiện một hành động redirect (chuyển hướng) đến một URL mới được tạo ra dựa trên logic trong block { |params| ... }.
      - params[:api]: Lấy giá trị của tham số :api từ yêu cầu HTTP.
      - .pluralize: Phương thức của Rails được sử dụng để biến đổi chuỗi thành dạng số nhiều. Ví dụ, nếu params[:api] là "user" thì params[:api].pluralize sẽ là "users".
      - Vì vậy, URL mới sẽ có dạng /api/v2/#{params[:api].pluralize}. Ví dụ, nếu params[:api] là "user", thì URL mới sẽ là /api/v2/users.

 Thêm các tham số cho chuyển hướng

 Phương thức redirect cũng có thể nhận các tham số như :status (mặc định là 301 cho chuyển hướng):

  match "/api/v1/:api",to:

  redirect(status: 302) { |params| "/api/v2/#{params[:api].pluralize}" },
  
  via: [:get, :post]

Routes as Rack Endpoints

 Định tuyến mà không cần phải định nghĩa một controller và một hành động riêng biệt. Giá trị được gọi là 1 điểm cuối của Rack.

  get "/hello", to: proc { |env| [200, {}, ["Hello world"]] }

  to: proc { |env| [200, {}, ["Hello world"]] }: Chỉ định rằng khi có yêu cầu đến URL /hello, hệ thống sẽ thực hiện một xử lý tùy chỉnh thông qua một đoạn mã được cung cấp dưới dạng một đối tượng Proc.
   - proc { |env| ... }: Đây là một đối tượng Proc (là một đoạn mã được đóng gói và có thể được gọi) nhận một tham số env, đại diện cho môi trường yêu cầu.
   - env chứa thông tin về yêu cầu HTTP như method (GET, POST, PUT,...), headers, và các thông tin khác.
   - [200, {}, ["Hello world"]]: Trả về một mảng gồm ba phần tử:
     -  200: Mã trạng thái HTTP OK, cho biết yêu cầu đã được xử lý thành công.
     - {}: Headers trống, không có thông tin bổ sung cần được trả về.
     - ["Hello world"]: Nội dung của phản hồi, trong trường hợp này là một mảng chứa một chuỗi "Hello world".

The Root Route

 Tuyến đường gốc là một quy tắc xác định hành động gì sẽ xảy ra khi ai đó kết nối đến "gốc" của trang web của bạn. Khi bạn kết nối đến một trang web với chỉ tên miền (ví dụ: http://example.com) mà không có bất kỳ đường dẫn cụ thể nào ở cuối URL, tuyến đường gốc quy định rằng ứng dụng sẽ thực hiện hành động gì (hiển thị gì ở trang chủ)

  root to: "welcome#index"

  root to: "pages#home"

  root "user_sessions#new"

Route Globbing

 cho phép bạn xác định các tuyến đường linh hoạt hơn bằng cách sử dụng đường dẫn có ký tự đại diện (wildcard) để phù hợp với nhiều URL khác nhau cùng một lúc. Ví dụ như liệt kê các URL của các sản phẩm từ gỗ

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

Named Routes

Creating a Named Route

 Đặt tên cho 1 Route bằng cách sử dụng tham số tùy chọn :as Ví dụ:

  get "help" => "help#index", as: "help"

 và tạo đường dẫn 

  link_to "Help", help_path

 ví dụ

  link_to "Auction of #{item.name}",

  controller: "items",

  action: "show",

  id: item.id

 với route 

  get "item/:id" => "items#show"

 có thể rút ngắn định nghĩa trong file route.rb thành 

  get "item/:id" => "items#show", as: "item

 và trong file view thành 

  link_to "Auction of #{item.name}", item_path(id: item.id)

 Có thể rút gọn ngắn hơn nữa bằng cách sử dụng phương thức to_param để Rails tự động lấy id.

 Mặc định, Rails sử dụng ID của đối tượng làm tham số mặc định trong URL. Ví dụ, nếu bạn có một đối tượng User với ID là 1, URL mặc định sẽ là /users/1. Tuy nhiên, sử dụng to_param, bạn có thể định nghĩa một cách tùy biến hóa cách biểu diễn của đối tượng này trong URL. Thay vì sử dụng ID, bạn có thể sử dụng bất kỳ trường nào khác trong model, chẳng hạn như slug, name, title,... 

 Ví dụ:
 Giả sử bạn có một model User trong Rails và bạn muốn sử dụng username của người dùng thay vì ID trong URL:

  class User < ApplicationRecord

   def to_param

    username

   end

  end

 Khi bạn sử dụng phương thức to_param như trên, mỗi khi bạn truy cập đến một đường dẫn sử dụng đối tượng User, ví dụ như user_path(user), Rails sẽ sử dụng giá trị của username của đối tượng để xây dựng URL thay vì ID. Ví dụ, nếu username của người dùng là "john_doe", URL sẽ trở thành /users/john_doe thay vì /users/1.


 Như vậy ta chỉ cần:

 link_to "Auction of #{item.name}", item_path(item)

 Nguyên tắc này cũng sử dụng kết hợp vs khoá phân đoạn 

 get "auction/:auction_id/item/:id" => "items#show", as: "item"

 link_to "Auction of #{item.name}", item_path(auction, item)

Direct Routes

 Trong Rails routing, phương thức directcung cấp cách để tạo các trợ giúp URL tùy chỉnh liên kết đến các URL tĩnh. Điềunày rất hữu ích khi bạn có các URL không thay đổi và muốn định nghĩa chúng một lần và sử dụng trong toàn bộ ứng dụng của bạn.

 Tạo Direct Route

  Dưới đây là cách bạn có thể sử dụng phương thức direct để định nghĩa trợ giúp URL tùy chỉnh:

  direct(:apple) { "http://www.apple.com" } 

  Trong ví dụ này:
   direct(:apple)
      - tạo ra một trợ giúp URL tùy chỉnh có tên là apple_url.

      - Khối { "http://www.apple.com" } xác định URL tĩnh mà apple_url sẽ phân giải tới.

Scoping Routing Rules

 Rails cung cấp nhiều cách để nhóm các quy tắc routing liên quan lại với nhau một cách ngắn gọn và hiệu quả. Các cách này dựa trên việc sử dụng phương thức scope và các shortcut của nó. Điều này giúp cho file routes.rb của bạn trở nên sạch sẽ và dễ quản lý hơn.

 Ví dụ:

  get "auctions/new" => "auctions#new"
  
  get "auctions/edit/:id" => "auctions#edit"

  post "auctions/pause/:id" => "auctions#pause"

 sử dụng phương thức scope để làm cho file routes.rb ngắn gọn hơn:

  scope controller: :auctions do

   get "auctions/new" => :new

   get "auctions/edit/:id" => :edit

   post "auctions/pause/:id" => :pause

  end

 Trong ví dụ trên:

  scope controller: :auctions chỉ định rằng tất cả các route bên trong block này sẽ
     sử dụng controller auctions.
  Các hành động (new, edit, pause) được viết gọn hơn mà không cần chỉ định lại tên
     controller.

 Them tham số :path vào scope: để ngắn gọn hơn nữa

  scope path: "/auctions", controller: :auctions do

   get "new" => :new

   get "edit/:id" => :edit

   post "pause/:id" => :pause

  end

 Việc sử dụng scope trong Rails là một cách hiệu quả để quản lý và tổ chức các quy tắc routing trong ứng dụng của bạn. Bằng cách nhóm các route liên quan lại với nhau và sử dụng các tham số như :controller và :path, bạn có thể làm cho file routes.rb trở nên ngắn gọn, dễ đọc và dễ bảo trì hơn.

Controller
 Có thể viết gọn hơn nữa từ 

  scope controller: :auctions do

 thành 

  scope :auctions do 

 hoặc 

  controller :auctions do

Path Prefix

 Phương thức scope chấp nhận tùy chọn :path hoặc có thể diễn giải một chuỗi (string) là đối số đầu tiên để biểu thị tiền tố đường dẫn.

  scope path: "/auctions" do

   get "new" => "auctions#new"

   get "edit/:id" => "auctions#edit"

   post "pause/:id" => "auctions#pause"

  end

 Đều sử dụng path nhưng ở ví dụ trên đã chỉ định sử dụng controller AuctionsController nên k cần phải chỉ định controller cho mỗi route nữa

Name Prefix

 Tùy chọn :as cho phép bạn thêm một tiền tố vào tên của các phương thức trợ giúp URL. Điều này rất hữu ích khi bạn cần phân biệt các nhóm đường dẫn khác nhau trong ứng dụng của mình. Ví
 dụ sau đây minh họa cách sử dụng :as để tạo ra các phương thức trợ giúp URL với tiền tố admin:

  scope :auctions, as: 'admin' do

   get 'new' => :new, as: 'new_auction'

  end

 Giúp phân biệt các nhóm đường dẫn khác nhau trong ứng dụng.

Namespaces

 Phương thức namespace trong Rails là một cú pháp ngắn gọn kết hợp các thiết lập module, tên tiền tố (name prefix) và tiền tố đường dẫn (path prefix) vào một khai báo duy nhất. Điều này giúp tổ chức các quy tắc routing một cách dễ dàng và gọn gàng hơn.

  namespace :auctions do

   get 'new' => :new

   get 'edit/:id' => :edit

   post 'pause/:id' => :pause

  end

 Khi sử dụng namespace, các quy tắc URL sẽ được tổ chức theo các cách sau:
  Module:
     Các hành động được định nghĩa trong một module có tên tương ứng với namespace. Trong ví dụ trên, các hành động sẽ nằm trong module Auctions.

  Name Prefix:
     Các phương thức trợ giúp URL sẽ có tiền tố tương ứng với namespace. Ví dụ: new_auction_url, edit_auction_url, pause_auction_url.

  Path Prefix:
     Các URL sẽ có tiền tố đường dẫn tương ứng với namespace. Ví dụ: /auctions/new, /auctions/edit/:id, /auctions/pause/:id.

 Như vậy sự khác biệt giữa scope và namespaces là scope có thể tuỳ chỉnh 3 tham số module, path và as

Bundling Constraints

 Có thể thêm ràng buộc vào phương thức scope. Trường hợp dưới đây ràng buộc cho toàn bộ tuyến

  scope controller: :auctions, constraints: {:id =>/\d+/} do

   get "edit/:id" => :edit

   post "pause/:id" => :pause

  end

 hoặc trường hợp một tập hợp các quy tắc trong một scope cụ thể cần các ràng buộc.

  scope path: "/auctions", controller: :auctions do

   get "new" => :new

   constraints id: /\d+/ do

    get "edit/:id" => :edit

    post "pause/:id" => :pause

   end

  end

 Để tăng tính tái sử dụng theo mô-đun, bạn có thể cung cấp phương thức constraints với một đối tượng có phương thức matches?. Đây là ví dụ về cách làm điều này:
 
  class DateFormatConstraint

   def self.matches?(request)

    request.params[:date] =~ /\A\d{4}-\d\d-\d\d\z/

   end

  end

  constraints(DateFormatConstraint) do

   get 'since/:date' => :since

  end

 Trong ví dụ này, DateFormatConstraint kiểm tra xem tham số :date có định dạng đúng YYYY-MM-DD hay không. Nếu người dùng nhập một tham số date không đúng định dạng qua URL, Rails sẽ phản hồi với mã trạng thái 404 thay vì gây ra một ngoại lệ.

Listing Routes

 Rails cung cấp một tiện ích hữu ích để liệt kê các tuyến đường có trong ứng dụng bằng cách gõ rails routes trong thư mục ứng dụng của bạn. Dưới đây là ví dụ về đầu ra của một tập tin routes.rb chứa một quy tắc duy nhất resources :products:

 Đầu ra là một bảng có bốn cột:
  Prefix:
     Tên của tuyến đường (nếu có).

  Verb:
     Phương thức HTTP được sử dụng (GET, POST, PATCH, PUT, DELETE).

  URI Pattern:
     Chuỗi ánh xạ URL.

  Controller#Action:
     Bộ điều khiển và phương thức hành động mà tuyến đường ánh xạ tới, cộng với các ràng buộc đã được định nghĩa trên khóa đoạn của tuyến đường (nếu có).

 Tùy Chọn Liệt Kê Theo Bộ Điều Khiển

 Lệnh rails routes còn hỗ trợ kiểm tra một bộ điều khiển cụ thể bằng cách sử dụng tùy chọn -c. Ví dụ, để chỉ liệt kê các tuyến đường liên quan đến ProductsController, bạn có thể sử dụng lệnh sau:

  $ rails routes -c products

  Ví dụ: 
  Rails.application.routes.draw do

   resources :products

  end

  Giải thích chi tiết
  Khi bạn định nghĩa resources :products, Rails sẽ tự động tạo ra một tập hợp các tuyến đường chuẩn để xử lý các hành động CRUD (Create, Read, Update, Delete) cho tài nguyên products.

Chapter3

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

Chapter4 

Action Dispatch 

 Action Dispatch là 1 mô-đun con của mô-đun Action Pack.

 Action Dispatch xử lý routing các request, nó xử lý các request và xử lý một vài quá trình liên quan đến giao thức HTTP như xử lý cookies, session…

 Phương thức draw trong file config/routes.rb gọi tới ActionDispatch::Routing::RouteSet 

 Khi Rails app khởi động, RouteSet sẽ được khởi tạo. Nó build cái routes từ file routes.rb. Và nó cũng chính là thành phần đầu tiên nhận request từ client sau khi đi qua Rack và các middleware khác.

 RouteSet::Dispatcher

 Dispatcher là 1 class nhỏ chịu trách nhiệm khởi tạo controller và có nhiệm vụ chuyển request tới đúng controller để xử lý và trả về response.

  get "demo" => "demo#index"

 route trên sử dụng dispatcher. Ta có thể bỏ qua dispatcher bằng cách viết 

  get "demo" => DemoController.action(:index)

 Ví dụ (A):

 - Tạo democontroller trong app/controllers/demo_controller.rb với code sau:

   class DemoController < ActionController::Metal

      def index

         self.response_body = "Hello World!"

      end   

   end

 - Xong thêm code sau vào config/routes.rb:

   get "demo" => "demo#index"

 - Xong truy  cập vào localhost:3000/demo Web sẽ hiển thị “Hello World!”.

Parameters

 Rails thu thập tham số từ 3 vị trí:


 - Đường dẫn (the path)

 - Truy vấn (the query)

 - Thân (the body)

 Tất cả chúng đều được hợp nhất và cung cấp thông qua phương thức params dưới dạng một thể hiện của ActionController::Parameters.

 Tham số Query được thiết lập bằng cách gửi một biểu mẫu HTML với yêu cầu GET

 Tham số Body được thiết lập bằng cách gửi biểu mẫu qua POST và các phương thức khác vì chúng được giả lập bởi một yêu cầu POST.

 Tham số cũng có thể được cung cấp bởi một request gửi qua JavaScript hoặc một client API.

 Trong biểu mẫu (forms), danh sách các tham số là một danh sách phẳng của các cặp khóa/giá trị (key/value pairs):

   a=12&b=text&c=Hello

 Rails sẽ cung cấp cho chúng ta các tham số tương đương với hash sau:

   {"a"=>"12", "b"=>"text", "c"=>"Hello"}

 Rails hiện áp dụng hai quy tắc bổ sung để cho phép mảng và hash. Để đánh dấu một tham số là một mảng, đặt tham số trong “[]” , bằng cách này có thể mô tả mục bằng nhiều tham số 

   countries[]=AT&countries[]=CH&countries[]=DE

 tương đương với:

   {"countries"=>["AT", "CH", "DE"]}

 Quy tắc còn lại là 1 tham số được mô tả bằng 1 hash gồm nhiều tham số 

   person[name]=obie&person[occupation]=dj

 tương đương với:

   {"person"=>{"name"=>"obie", "occupation"=>"dj"}}

Strong parameters

 Là các tham số được cung cấp dưới dạng một thể hiện của ActionController::Parameters có thuộc tính permitted được đặt là false

   params = ActionController::Parameters.new(
      person: {
         name: "obie",
         occupation: "dj"
      }
   )

 #=> <ActionController::Parameters{"person"=>{
 # "name"=>"obie","occupation"=>"dj"}} permitted: false>

 Để ngăn chặn người dùng đặt bất kỳ tham số nào họ muốn (ví dụ: tự thăng cấp lên vai trò quản trị viên), việc cung cấp một unpermitted cho một lần gán hàng loạt của một mô hình ActiveRecord sẽ gây ra một ngoại lệ:

   Person.new(params)

   #=> Exception raised: ActiveModel::ForbiddenAttributesError

 Bạn có hai lựa chọn: handpick hoặc permit attributes

Render onto View…

 Mục tiêu của hành động controller điển hình trong một ứng dụng web truyền thống là để render một view template — tức là, điền vào template và giao kết quả, thường là một tài liệu HTML, lại cho máy chủ để chuyển đến trình duyệt.


 Trong app/views/demo/index.html.erb thêm mã sau:

   Hello World!

 Sau đó yêu cầu controller render template đó:

   class DemoController < ApplicationController

      def index

         render "demo/index"

      end

   end

 So sánh với ví dụ (A) ta thấy DemoController không còn kế thừa từ ActionController::Metal mà từ ApplicationController vì render là một tính năng được cung cấp bởi ActionController::Base. Nếu bạn truy cập lại trang, bạn vẫn sẽ được chào đón với “Hello World!”.

When in Doubt, Render

 Ở cuối mỗi hành động của controller, nếu không có gì khác được chỉ định, hành vi mặc định là render template có tên khớp với tên của controller và action, trong trường hợp này nghĩa là app/views/demo/index.html.erb. Vì vậy, hãy thử mã sau:

   class DemoController < ApplicationController

      def index

      end

   end

 không cần phải gọi render rõ ràng, vì Rails giả định đó là điều bạn muốn.

 Nói cách khác, mỗi hành động controller có một lệnh render ngầm trong đó.

 Vào app/controller/demo_controller.rb, và xóa hành động index để file trông trống rỗng, như sau:

   class DemoController < ApplicationController

   end

 Rails biết rằng khi nó nhận được một yêu cầu cho hành động index của demo controller, điều thực sự quan trọng là gửi lại điều gì đó cho máy chủ. Vì vậy, nếu không có hành động index trong file controller, Rails chỉ đơn giản cho rằng, “Chà, hãy giả định rằng nếu có một hành động index, nó cũng sẽ trống thôi, và tôi chỉ cần render index.html.erb. Vậy đó là điều tôi sẽ làm.”

Render Template của Hành Động Khác

 Một lý do phổ biến để render một template hoàn toàn khác là để hiển thị lại một form, khi nó được gửi với dữ liệu không hợp lệ và cần phải chỉnh sửa. Trong những trường hợp như vậy, chiến lược web thông thường là hiển thị lại form với dữ liệu đã gửi và đồng thời hiển thị một số thông tin lỗi, để người dùng có thể chỉnh sửa form và gửi lại.

 Lý do quá trình này liên quan đến việc render một template khác là vì hành động xử lý form và hành động hiển thị form thường là — khác nhau. Do đó, hành động xử lý form cần một cách để hiển thị lại template gốc (form), thay vì coi việc gửi form là thành công và chuyển sang màn hình tiếp theo.

   class EventController < ActionController::Base

      def new

      end

      def create

         @event = Event.new(params[:event])

         if @event.save

            redirect_to dashboard_path, notice: "Event created!"

         else

            render action: 'new' 

         end

      end

   end

 Giải thích :

 - Phương thức new chỉ đơn giản là render ra template new.html.erb mà không có xử lý logic nào khác. Template này thường chứa biểu mẫu để người dùng nhập thông tin về sự kiện mới.
 - Phương thức create xử lý dữ liệu từ biểu mẫu nhập liệu (new.html.erb). Dữ liệu nhập vào từ người dùng được lưu trong params, và thông tin của sự kiện mới được khởi tạo thông qua Event.new(params[:event]).
 - Nếu sự kiện được lưu thành công (@event.save trả về true), người dùng sẽ được chuyển hướng đến dashboard_path và hiển thị thông báo "Event created!".
 - Nếu không thành công (@event.save trả về false), phương thức render sẽ render lại action new. Điều này cho phép hiển thị lại biểu mẫu với thông báo lỗi hoặc trạng thái trước đó mà không cần gọi lại phương thức new.

 Lưu ý rằng template tự nó không “biết” rằng nó đã được render bởi hành động create thay vì hành động new. Nó chỉ làm công việc của nó: Nó điền, mở rộng và chèn, dựa trên các hướng dẫn nó chứa và dữ liệu (trong trường hợp này là @event) mà controller đã truyền cho nó.

Render Một Template Hoàn Toàn Khác

 Tương tự như vậy, nếu bạn muốn render một template cho một hành động khác, bạn có thể render bất kỳ template nào trong ứng dụng của bạn bằng cách gọi phương thức render với một chuỗi chỉ đến tệp template mong muốn.

   render template: "/products/index.html.erb"

 Trong những trường hợp hiếm, bạn có thể sử dụng phương thức render để truy cập vào các template hoàn toàn nằm ngoài ứng dụng của bạn bằng cách sử dụng :file 

   render file: "/u/apps/warehouse_app/current/app/views/products/show"

Rendering a Partial Template: render 1 phần giao diên người dùng

 sử dụng tùy chọn :partial

   render partial: "product"

 Trong Rails, partials là các file view nhỏ được sử dụng để tái sử dụng các phần giao diện giống nhau trong các trang khác nhau của ứng dụng. Khi gọi render partial: "product", Rails sẽ tìm và render nội dung từ file _product.html.erb trong thư mục app/views/products/.

Rendering HTML

 sử dụng tùy chọn :html

   render html: "<strong>Not Found</strong>".html_safe

Rendering Inline Template Code

 sử dụng tùy chọn inline:

   render inline: "%span.foo #{@foo.name}", type: "haml"

Rendering Text

 sử dụng tùy chọn plain:

   render plain: "Submission accepted"

Rendering raw body output

 sử dụng tùy chọn body:

   render body: "Something very raw"

Rendering Other Types of Structured Data

 :json

   render json: @record

 :xml

   render xml: @record

Chính sách mặc định của việc render

 Trong mọi trường hợp, nếu Rails không thể tìm thấy template để render, hãy nhớ rằng nó sẽ phản hồi yêu cầu với "204 No Content". Điều khó khăn với mã trạng thái này là nhiều trình duyệt sẽ đơn giản bỏ qua nó và không làm gì cả. Nếu bạn không để ý đến những gì đang xảy ra (đặc biệt là trên cửa sổ console của Rails), bạn có thể nghĩ rằng trang trước đã được render lại, đặc biệt là nếu nó chứa một thông báo hoặc mã trạng thái lỗi.

Rendering Options

 :content_type

 Options định dạng nội dung

 :layout

 Options cho phép chọn layout render ra

 :status

 Giao thức HTTP bao gồm nhiều mã trạng thái tiêu chuẩn chỉ ra nhiều điều kiện khác nhau trong phản hồi của máy chủ đối với yêu cầu của khách hàng. Rails sẽ tự động sử dụng trạng thái phù hợp cho hầu hết các trường hợp thông thường, chẳng hạn như 200 OK cho một yêu cầu thành công.

Additional Layout Options

 có thể chỉ định các tùy chọn layout ở cấp lớp controller nếu bạn muốn tái sử dụng các layout cho nhiều hành động khác nhau.

   class EventController < ActionController::Base

      layout "events", only: [:index, :new]

      layout "global", except: [:index, :new]

   end

 Phương thức layout có thể chấp nhận một chuỗi (String), ký hiệu (Symbol), hoặc Boolean (kiểu dữ liệu biểu diễn hai giá trị: đúng (true) và sai (false)), kèm theo một hash các đối số.

Redirecting

 Vòng đời của một ứng dụng Rails được chia thành các yêu cầu. Việc render một template, dù là template mặc định hay một template thay thế, hoặc render một partial hay một đoạn văn bản nào đó, là bước cuối cùng trong việc xử lý một yêu cầu. Tuy nhiên, việc chuyển hướng (redirect) có nghĩa là kết thúc yêu cầu hiện tại và yêu cầu khách hàng khởi tạo một yêu cầu mới

 Hãy xem ví dụ về phương thức xử lý form create sau đây:

   def create

      if @event.save

         redirect_to :index, notice: "Event created!"

      else

         render :new

      end

   end

 if @event.save: Kiểm tra xem việc lưu đối tượng @event vào cơ sở dữ liệu có thành công hay không.

 redirect_to, notice: "Event created!": Nếu việc lưu thành công, chuyển hướng đến hành động index và hiển thị thông báo "Sự kiện đã được tạo!".

 Trong trường hợp này, đó là hành động index. Logic ở đây là nếu bản ghi Event mới được lưu, bước tiếp theo là đưa người dùng trở lại top-level view

 Lý do chính để chuyển hướng thay vì chỉ render một template sau khi tạo hoặc chỉnh sửa một tài nguyên (thực sự là một hành động POST) liên quan đến hành vi tải lại của trình duyệt. Nếu bạn không chuyển hướng, người dùng sẽ được nhắc nhở để nộp lại biểu mẫu nếu họ nhấn nút quay lại hoặc tải lại trang.

 Phương thức redirect_to nhận hai tham số:

   redirect_to(target, response_status = {})

 Tham số target có thể nhận một trong các dạng sau:

 - Hash: URL sẽ được tạo bằng cách gọi url_for với đối số được cung cấp.
 - Đối tượng Active Record: URL sẽ được tạo bằng cách gọi url_for với đối tượng được cung cấp, đối tượng này nên tạo một URL có tên cho bản ghi đó.
 - Chuỗi bắt đầu bằng giao thức như http://: Được sử dụng trực tiếp làm URL đích để chuyển hướng.
 - Chuỗi không chứa giao thức: Giao thức và host hiện tại được thêm vào trước đối số và được sử dụng cho việc chuyển hướng.
 - Proc: Một proc sẽ được thực thi trong ngữ cảnh của controller. Proc này nên trả về bất kỳ lựa chọn mục tiêu nào ở trên.

Phương thức redirect_back

 Bạn có thể sử dụng phương thức redirect_back để chuyển hướng người dùng quay lại trang mà họ vừa đến từ, một kỹ thuật rất hữu ích trong các ứng dụng web truyền thống. Địa chỉ để "quay lại" được lấy từ tiêu đề HTTP_REFERER. Vì không đảm bảo rằng nó sẽ được thiết lập bởi trình duyệt, bạn phải cung cấp tham số fallback_location như một giá trị mặc định khi không có địa chỉ trước đó.

   redirect_back fallback_location: root_path

 Mặc định, phương thức redirect_back cho phép chuyển hướng đến một máy chủ khác. Tuy nhiên, bạn có thể ngăn chặn điều này bằng cách thiết lập tùy chọn allow_other_host thành false.

   redirect_back fallback_location: root_path, allow_other_host: false

 Điều này sẽ chỉ cho phép chuyển hướng quay lại cùng một máy chủ mà không chuyển đến các máy chủ khác.

Controller/View Communication

 Khi một template view được render, thường nó sẽ sử dụng dữ liệu mà controller đã lấy từ cơ sở dữ liệu. Nói cách khác, controller nhận những gì nó cần từ tầng model và chuyển giao cho view.

 Rails thực hiện việc truyền dữ liệu từ controller tới view thông qua các biến instance. Thông thường, một hành động của controller khởi tạo một hoặc nhiều biến instance. Những biến instance đó sau đó có thể được sử dụng bởi view. Điều này được thực hiện thông qua hash assigns được cung cấp cho view khi khởi tạo.

 assigns hash là một biến instance trong controller được sử dụng để lưu trữ các giá trị mà bạn muốn truyền từ controller tới view. Đây là một phần của cơ chế kết hợp giữa controller và view trong Rails để truyền dữ liệu từ phía server (controller) sang phía client (view).

 Cách hoạt động của assigns hash:

 Định nghĩa và gán giá trị: Trên controller, bạn có thể gán các giá trị cho assigns thông qua các biến instance. Ví dụ:

   class PostsController < ApplicationController

      def show


         @post = Post.find(params[:id])


         @comments = @post.comments


         @tags = @post.tags

      # Các giá trị này sẽ được tự động lưu vào assigns hash

      end

   end

 Truyền dữ liệu cho view: Khi một view được render, Rails sẽ tự động chuyển assigns hash vào phạm vi của view template. Điều này cho phép bạn truy cập các giá trị này từ view một cách dễ dàng.

 Ví dụ, trong view show.html.erb:

   <h1><%= @post.title %></h1>

   <h2>Comments:</h2>

   <% @comments.each do |comment| %>

   <p><%= comment.body %></p>

   <% end %>

   <h2>Tags:</h2>

   <% @tags.each do |tag| %>

   <span><%= tag.name %></span>

   <% end %>

 Trong đoạn mã này, @post, @comments, và @tags đều được truy cập thông qua assigns hash.

 Tính chất của assigns: assigns là một hash bao gồm các cặp key-value, trong đó key là tên biến instance (có thể là symbol hoặc string) và value là giá trị của biến instance đó. Rails tự động tạo và quản lý assigns trong quá trình xử lý một request và gửi dữ liệu này sang view tương ứng.

 Gem "Decent Exposure" trong Rails là một thư viện giúp đơn giản hóa việc xử lý dữ liệu (data handling) trong các controller của ứng dụng Rails. Thư viện này được sử dụng để giảm thiểu việc lặp lại code và tăng tính tổ chức của mã nguồn bằng cách tự động tạo ra các phương thức truy cập dữ liệu cho các biến instance trong controller.

 Các tính năng chính của Decent Exposure:

 - Tự động tạo các phương thức truy cập: Decent Exposure cho phép bạn định nghĩa các biến instance trong controller mà không cần viết nhiều code. Thay vì phải viết từng getter và setter cho từng biến instance, bạn chỉ cần định nghĩa một lần và Decent Exposure sẽ tự động tạo ra các phương thức truy cập tương ứng.

 - Tăng tính mạnh mẽ và bảo mật: Thay vì trực tiếp sử dụng biến instance, Decent Exposure thúc đẩy việc sử dụng các phương thức để truy cập và thay đổi dữ liệu, giúp tăng tính bảo mật và quản lý dữ liệu.

 - Hỗ trợ cấu hình linh hoạt: Decent Exposure cho phép bạn tùy chỉnh cách thức hoạt động thông qua các tùy chọn cấu hình, cho phép bạn điều chỉnh hành vi mặc định của gem theo yêu cầu cụ thể của ứng dụng.

Action Callbacks

 Các action callbacks cho phép các controller chạy mã xử lý chung trước và sau khi thực hiện các hành động của họ. Những callback này có thể được sử dụng để thực hiện xác thực, caching hoặc kiểm định trước khi hành động dự định được thực hiện. Các khai báo callback là các phương thức lớp kiểu macro, tức là chúng xuất hiện ở đầu phương thức của controller, trong ngữ cảnh lớp, trước định nghĩa của phương thức. Vi du

   before_action :require_authentication

Streaming

 là khả năng hỗ trợ gửi nội dung về cho client yêu cầu một cách liên tục (streaming), thay vì đợi cho đến khi toàn bộ nội dung được hoàn thành mới gửi đi. Điều này giúp cải thiện hiệu suất và trải nghiệm người dùng trong các trường hợp cần xử lý và truyền tải dữ liệu lớn hoặc dữ liệu đang được sinh ra theo thời gian thực.

Streaming Templates 

 Mặc định, khi một view được render trong Rails, nó trước tiên render template và sau đó là layout của view. Khi trả về một response cho client, tất cả các truy vấn Active Record cần thiết được thực thi và toàn bộ template được render một lần duy nhất.

 Tuy nhiên, Rails cũng hỗ trợ streaming các view đến client. Điều này cho phép các view được render và truyền dần dần khi chúng được xử lý, bao gồm chỉ thực thi các truy vấn Active Record cụ thể khi chúng cần thiết. Để làm được điều này, Rails đảo ngược thứ tự render bình thường. Layout được render trước thay vì sau, sau đó từng phần của template được xử lý.

 Để kích hoạt streaming view, bạn có thể truyền tuỳ chọn stream vào phương thức render

   class EventController < ActionController::Base

      def index

         @events = Events.all

         render stream: true

      end

   end

 Rails cũng hỗ trợ gửi các bộ đệm (buffers) và tập tin bằng hai phương thức trong module ActionController::DataStreaming: send_data và send_file.

The respond_to Method

 Trong HTTP, định dạng của phản hồi được thương lượng giữa máy khách và máy chủ. Máy khách cung cấp cho máy chủ một danh sách các định dạng mà nó hiểu được theo độ ưu tiên thông qua tiêu đề Accept. Sau đó, máy chủ chọn một định dạng từ danh sách được cung cấp hoặc từ chối yêu cầu. Trong lệnh curl, chúng ta có thể thiết lập một tiêu đề yêu cầu bằng tùy chọn -H:

   $ curl http://localhost:3000/auctions/1 -H "Accept: application/json" -v

   GET /auctions/1 HTTP/1.1

   Host: localhost:3000

   User-Agent: curl/7.58.0

   Accept: application/json

 Điều này cho biết với máy chủ của chúng ta rằng máy khách chỉ chấp nhận JSON.

   $ curl http://localhost:3000/auctions/1.json -v

   GET /auctions/1 HTTP/1.1

   Host: localhost:3000

   User-Agent: curl/7.58.0

   Accept: */*

 */* Accept header chấp nhận bất kỳ định dạng nào.

 Trong Rails, controller có trách nhiệm phản ứng với định dạng yêu cầu từ phía máy khách. Phương thức respond_to cho phép bạn viết các hành động của mình sao cho nó sẽ trả về kết quả khác nhau dựa trên định dạng yêu cầu từ máy khách. Dưới đây là một ví dụ về hành động show cho controller products, cung cấp cả HTML và JSON:

   def show

      @auction = Auction.find(params[:id])

      respond_to do |format|

         format.html

         format.json { render json: @auction.to_json }

      end

   end

 Khối respond_to trong ví dụ này có hai điều kiện. Điều kiện HTML đơn giản chỉ có format.html. Yêu cầu cho HTML sẽ được xử lý bằng cách hiển thị một view template như thường lệ. Điều kiện JSON bao gồm một khối mã; nếu yêu cầu JSON, khối mã sẽ được thực thi và kết quả của nó sẽ được trả về cho máy khách.

 Nếu yêu cầu một định dạng mà không được định nghĩa trong khối respond_to, Rails sẽ không sinh ra một ngoại lệ. Thay vào đó, nó sẽ trả về mã trạng thái 406 Not Acceptable, để chỉ ra rằng nó không thể xử lý yêu cầu.

 Nếu bạn muốn thiết lập một điều kiện else cho khối respond_to của mình, bạn có thể sử dụng phương thức any, cho Rails biết để bắt các định dạng khác không được định nghĩa một cách rõ ràng:

   def show

      @product = Product.find(params[:id])

      respond_to do |format|

         format.html

         format.json { render json: @product.to_json }

         format.any

      end

   end

 Hãy chắc chắn rằng bạn đã chỉ định rõ ràng cho any cách xử lý yêu cầu hoặc có các view template tương ứng với các định dạng bạn mong đợi. Nếu không, bạn sẽ nhận được một ngoại lệ MissingTemplate.

   ActionView::MissingTemplate (Missing template products/show,

      application/show with {:locale=>[:en], :formats=>[:xml],

      :handlers=>[:erb, :builder, :raw, :ruby, :jbuilder, :coffee]}.)

Variants

 Variants là một tính năng trong Rails cho phép render các template HTML, JSON, và XML khác nhau dựa trên một số tiêu chí nhất định.

Chapter 5

Cookies

 Cookie là một mẩu thông tin mà máy chủ yêu cầu trình duyệt lưu trữ. Từ thời điểm đó, trình duyệt sẽ bao gồm cookie trong mọi yêu cầu nó gửi đến máy chủ. Chúng ta có thể sử dụng cookies để lưu trữ các tùy chọn của người dùng, chẳng hạn. Hãy lưu ý rằng cookies sẽ làm tăng kích thước của mỗi yêu cầu đến máy chủ của bạn.

 Bộ chứa cookie, như được biết đến, trông giống như một hash. Bạn có thể truy cập nó thông qua phương thức cookies trong phạm vi của các controller, view template và helper.

 Lưu ý rằng cookie được đọc theo giá trị, vì vậy bạn sẽ không nhận lại đối tượng cookie mà chỉ là giá trị nó giữ dưới dạng chuỗi (hoặc dưới dạng một mảng chuỗi nếu nó giữ nhiều giá trị).

 Để tạo hoặc cập nhật cookies, bạn gán giá trị sử dụng toán tử dấu ngoặc vuông. Bạn có thể gán một giá trị chuỗi đơn hoặc một hash chứa các tùy chọn. 

 Chúng ta có thể ghi cookie như sau:

  cookies[:list_mode] = "false"

 Chúng ta có thể đọc cookie như sau:

  cookies[:list_mode] # "false"

 Chúng ta cũng có thể xóa một cookie:

  cookies.delete(:list_mode)

 Một cookie có thời gian sống mặc định là "session". Thời gian sống của "session" được định nghĩa bởi trình duyệt, nhưng trong hầu hết các trường hợp, cookie này được lưu trữ cho đến khi bạn thoát trình duyệt. Nếu bạn muốn giữ nó lâu hơn, bạn có thể đặt thuộc tính "Expires". Trong Rails, chúng ta sử dụng tùy chọn expires, nhận một số giây làm đối số, để xác định khi nào cookie nên bị xóa bởi trình duyệt. 

  cookies[:recheck] = { value: "false", expires: 5.minutes.from_now }

 Bạn cũng có thể đặt nó thành một timestamp:

  cookies[:contact] = { value: "false", expires: Time.utc(2063, 4, 5) }

 Một trường hợp sử dụng phổ biến là đặt một cookie "vĩnh viễn". Vì điều này không phải là một phần của tiêu chuẩn HTTP, Rails định nghĩa vĩnh viễn là "20 năm". Bạn có thể đặt một cookie "permanent" như sau:

  cookies.permanent[:answer] = "42"

 Mỗi cookie đều có một phạm vi. Phạm vi bao gồm hai thuộc tính: domain và path.

 Theo mặc định, thuộc tính domain là nil. Điều này báo hiệu cho trình duyệt rằng cookie chỉ nên được gửi đến chính xác tên miền mà nó xuất phát từ đó, cụ thể là không bao gồm các tên miền con.

 Nếu bạn đặt tùy chọn :domain thành :all cookie sẽ được gửi cho các yêu cầu đối với tên miền và tất cả các tên miền con của nó

  cookies[:login] = {

    value: @user.security_token,

    domain: :all

  }

 Tuỳ chọn :path rất hữu ích vì nó cho phép bạn đặt các tùy chọn cụ thể cho các phần cụ thể hoặc thậm chí các bản ghi cụ thể của ứng dụng của bạn. Đường dẫn mô tả một tiền tố, vì vậy /ideas cũng áp dụng cho /ideas/1. Nó mặc định là /, do đó khớp với tất cả các đường dẫn.

 Cookie cũng có thuộc tính SameSite. Nó có ba giá trị khả thi:

 - Strict: Cookie chỉ được gửi đến cùng tên miền mà nó xuất phát từ đó.
 - Lax: Tương tự, ngoại trừ khi người dùng điều hướng đến một URL từ một trang web bên ngoài, chẳng hạn như khi theo dõi một liên kết.
 - None: Không có hạn chế về các yêu cầu chéo trang web.

Cookie Access

 Chúng ta có thể hạn chế thêm quyền truy cập vào cookie:

  cookies[:account_number] = { value: @account.number, secure: true, httponly: true }

 với tuỳ chọn :httponly được đặt là true (mặc định là false), cookie sẽ không thể truy cập từ JavaScript.

 Với tuỳ chọn :secure được đặt là true, cookie chỉ được truyền qua kết nối HTTPS. Mặc định phụ thuộc vào cấu hình force_ssl của bạn: Nếu bạn bắt buộc sử dụng HTTPS, Rails cũng sẽ mặc định sử dụng cookie bảo mật. Mặc định điều này có nghĩa là bạn có :secure được bật trong môi trường production, nhưng không phải trong môi trường development hoặc testing.

Signed and Encrypted Cookies

 Vì cookie được lưu trữ trong trình duyệt của người dùng, họ có thể đọc và thay đổi nó. Điều này có thể chấp nhận được đối với một số cookie. Đối với các cookie khác (như cookie phiên làm việc mà chúng ta sẽ tìm hiểu tiếp theo), điều này có thể không ổn.

 Nếu bạn muốn người dùng có thể đọc cookie nhưng không thể thay đổi nó, bạn có thể sử dụng signed cookie:

  cookies.signed[:user_id] = current_user.id

 Nếu người dùng thay đổi giá trị của cookie, Rails sẽ kiểm tra chữ ký và loại bỏ cookie. Tuy nhiên, vẫn có thể đọc cookie ở phía client. Điều này có thể hữu ích nếu bạn muốn một client JavaScript đọc cookie nhưng không thể sửa đổi nó. Nó hữu ích để bảo vệ thông tin nhạy cảm khỏi bị thay đổi mà không cần mã hóa.

 Nếu bạn muốn đảm bảo rằng cookie không thể đọc hoặc thay đổi, bạn có thể mã hóa nó:

  cookies.encrypted[:user_id] = current_user.id

Session

 Bất cứ khi nào một người dùng mới truy cập vào ứng dụng Rails của chúng ta, một phiên làm việc mới sẽ được tự động tạo. Sử dụng phiên này, chúng ta có thể duy trì một lượng trạng thái phía máy chủ đủ để làm cho lập trình web trở nên dễ dàng hơn đáng kể.

Accessing the Session

 API của phiên làm việc là một tập con của API Hash:

 # write to the session

  session[:current_user] = "Bob"

 # read from the session

  session[:current_user] # "Bob"

 # delete a key

  session.delete(:current_user) # "Bob"

 Ngoài ra, bạn có thể sử dụng phương thức reset_session được định nghĩa trong ActionController::Metal để đặt lại phiên làm việc:

  reset_session

Storage Mechanisms

 Phiên làm việc được xác định bởi một session id duy nhất, một chuỗi 32 ký tự của các số hex ngẫu nhiên. Bất kể cơ chế lưu trữ được chọn là gì, session id này được lưu trữ trong một cookie. Như đã giải thích trong phần về cookie bảo mật, tất cả các cookie được đặt thành bảo mật khi bạn bật force_ssl. Hơn nữa, cookie phiên làm việc mặc định là httponly. Bạn có thể truy cập session id như sau:

  session[:session_id]

Cache Store

 Tùy chọn lưu trữ phiên cache cho phép bạn sử dụng bất kỳ cái gì bạn đã cấu hình làm bộ nhớ cache làm kho dữ liệu phiên. Ngoài việc dễ dàng để cấu hình và vận hành, điều này cũng rất tiện lợi vì nó tích hợp sẵn hết hạn, có nghĩa là bạn không cần phải tự động hết hạn các phiên cũ.

 Để cấu hình nó, hãy tạo một tập tin khởi tạo trong config/initializers session_store.rb:

  Rails.application.config.

    session_store ActionDispatch::Session::CacheStore

 Hoặc, để cấu hình nó khác nhau cho mỗi môi trường, đặt nó trong tệp cấu hình tương ứng trong config/environments:

  config.session_store ActionDispatch::Session::CacheStore

The Flash

 sử dụng flash[:notice] để lưu trữ các thông báo thông thường và flash[:alert] để truyền thông tin quan trọng hơn. Những thông điệp này sau đó được hiển thị ở một phần nổi bật trên HTML được render.

 Rails cho phép bạn thiết lập chúng như các tham số tùy chọn trong phương thức redirect_to:

  def create

    if user.try(:authorize, params[:user][:password])

      redirect_to home_url, notice: "Welcome, #{user.first_name}!"

    else

      redirect_to :new, alert: "Login invalid."

    end

  end

 Đôi khi bạn muốn hiển thị một thông báo flash cho người dùng nhưng chỉ trong yêu cầu hiện tại. Thực tế, một lỗi lập trình phổ biến của các lập trình viên mới vào Rails là đặt thông báo flash mà không chuyển hướng, dẫn đến hiển thị thông báo flash sai trong yêu cầu tiếp theo.

 Để làm cho flash hoạt động cùng với lệnh render, bạn có thể sử dụng phương thức flash.now

  class ReportController < ActionController::Base

    def create

      if report.save

        redirect_to report_path(report), notice: "#{report.title} has been created."

      else

        flash.now.alert = "#{report.title} could not be created."

        render :new

      end

    end

  end

 Đối tượng flash.now cũng có các truy cập vào notice và alert, tương tự như đối tượng flash truyền thống của nó. Phương thức flash.now được sử dụng để hiển thị thông báo flash ngay trong quá trình render hiện tại, thay vì chờ cho đến khi chuyển hướng đến yêu cầu tiếp theo.
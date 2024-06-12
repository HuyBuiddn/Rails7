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

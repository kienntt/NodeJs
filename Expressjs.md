# Expressjs cơ bản
## 1.Giới thiệu Express Framework
Express js là một Framework nhỏ, nhưng linh hoạt được xây dựng trên nền tảng của Nodejs . Express rất dễ dàng để phát triển các ứng dụng nhanh dựa trên Node.js cho các ứng dụng Web. Express hỗ trợ các phương thức HTTP và middleware tạo ra 1 API rất mạnh mẽ và sử dụng dễ dàng.
- Về các package hỗ trợ: Expressjs có vô số các package hỗ trợ nên các bạn không phải lo lắng khi làm việc với Framework này.
- Về performance: Express cung cấp thêm về các tính năng (feature) để dev lập trình tốt hơn. Chứ không làm giảm tốc độ của NodeJS.

Cấu trúc của Expressjs :
<img src="https://viblo.asia/uploads/1f5feb3b-7d0b-4e9d-85c7-cc0aef7d7a18.png" alt="" class="medium-zoom-image">
- app.js chứa các thông tin về cấu hình, khai báo, các định nghĩa,... để ứng dụng của chúng ta chạy .
- package.json chứa các package cho ứng dụng chạy. Chúng ta cũng có thể thay đổi phiên bản của package ở đây.
- Folder routes: chứa các route để định tuyến trong ứng dụng .
- Folder view: chứa view/template cho ứng dụng.
- Folder public chứa các file css, js, images,...cho ứng dụng.

 Đây là cấu trúc cơ bản của expressjs , ngoài ra chúng ta có thể cấu trúc nó theo mô hình MVC .
 ## Router trong Expressjs

# Expressjs cơ bản
## 1. Giới thiệu Express Framework
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
 ## 2. Router trong Expressjs
 ### 2.1 Khái niệm cơ bản
 - Router là một Object (khác Routing nhé), nó là một instance riêng của middleware và routes (Hai khái niệm này là gì thì chúng ta sẽ tìm hiểu sau nhé). Chính vì nó là một instance của middleware và route nên nó có các chức năng của cả hai. Chúng ta có thể gọi nó là một mini-application.
 - Các Application dùng ExpressJS làm core đều có phần Router được tích hợp sẵn trong đó
 - Router hoạt động như một middleware nên chúng ta có thể dùng nó như một arguments. Hoặc dùng nó như một arguments cho route khác. Nghe có vẻ khó hiểu đúng không nào. Ví dụ nhé:
```
 // invoked for any requests passed to this router
router.use(function(req, res, next) {
  // .. some logic here .. like any other middleware
  next();
});

// will handle any request that ends in /events
// depends on where the router is "use()'d"
router.get('/events', function(req, res, next) {
  // ..
});
```
 - Chúng ta cũng có thể sử dụng Router để chia route. Chẳng hạn:
 ```
 app.use('/calendar', router);
 ```
 ### 2.2 Request & response trong Expresss
 Express sử dụng một hàm callback có các tham số là các đối tượng request và response.
 ```
 app.get('/', function (req, res) {
    //do something
})
```
- Request - Biểu diễn một HTTP request và có các thuộc tính cho các request như các chuỗi truy vấn, tham số, body, HTTP header và những phần khác.
- Response - Biểu diễn một HTTP response được ứng dụng Express gửi đi khi nó nhận về một HTTP request.
 ### 2.3  Tìm hiểu router.METHOD()
 - Router.METHOD() cung cấp cho chúng ta chức năng Routing trong ExpressJS. Cụ thể METHOD() ở đây là các HTTP method mà chúng ta thường xuyên sử dụng. Chẳng hạn GET, POST, PUT,DELETE.
 ```
 router.get('/user/profile', function(req, res, next) {
  res.send('user profile');
});
router.post('/'update/user/:id', function (res, req, next) {
  res.send('Update user');
});
router.put('/update/posts/:id', function (req, res, next) {
res.send('Update post');
});
```
 ### 2.4  Tìm hiểu method all của router
 - router.all(). Method này phù hợp với việc định nghĩa mang tính chất toàn cục cho các prefix.
 - Ví dụ: a. Ta có đoạn code sau: 
 ```
 router.all('*', requireAuthentication, loadUser);
 ```
  Nếu ta đặt route này trên cùng (top) thì nó yêu cầu tất cả các route bên dưới phải được ```requireAuthentication```. Có nghĩa là xác thực trước khi thực hiện một hành động hay một task nào đó tiếp theo. Mình ví dụ là ```loadUser``` chẳng hạn.
  Ta có đoạn code sau : 
  ```
  router.all('/api/*', requireAuthentication);
  ```
  Khác với ví dụ trên. Ở ví dụ này ta có một prefix đã được xác định là ```/api/``` thay vì dùng ```*``` . Nghĩa là trước khi request vào các route bên trong API thì phải qua một thao tác xác thực ```requireAuthentication```.
  ## 3 . Middleware trong ExpressJS
  ExpressJS khi hoạt động, về cơ bản sẽ là một loạt các hàm Middleware được thực hiện liên tiếp nhau. Sau khi đã thiết lập, các request từ phía người dùng khi gửi lên ExpressJS sẽ thực hiện lần lượt qua các hàm Middleware cho đến khi trả về response cho người dùng. Các hàm này sẽ được quyền truy cập đến các đối tượng đại diện cho Request - req, Response - res, hàm Middleware tiếp theo - next, và đối tượng lỗi - err nếu cần thiết.
  Một hàm Middleware sau khi hoạt động xong, nếu chưa phải là cuối cùng trong chuỗi các hàm cần thực hiện, sẽ cần gọi lệnh next() để chuyển sang hàm tiếp theo, bằng không xử lý sẽ bị treo tại hàm đó.
  Các chức năng mà middleware có thể thực hiện trong ExpressJS sẽ bao gồm :
  - Thực hiện bất cứ đoạn code nào
  - Thay đổi các đối tượng request và response
  - Kết thúc một quá trình request-response
  - Gọi hàm middleware tiếp theo trong stack
  Trong Express, có 5 kiểu middleware có thể sử dụng :
  - Application-level middleware (middleware cấp ứng dụng)
  - Router-level middleware (middlware cấp điều hướng - router)
  - Error-handling middleware (middleware xử lý lỗi)
  - Built-in middleware (middleware sẵn có)
  - Third-party middleware (middleware của bên thứ ba)
  ### 3.1. Application-level middleware
  Khi khởi tạo một Web Application với ExpressJS, chúng ta sẽ có một đối tượng đại diện cho Web App đó, thường được gán với biến ```app```. Đối tượng này có thể khai báo các middleware thông qua các hàm : ```app.use()``` hoặc ```app.METHOD``` (trong đó METHOD sẽ là cá kiểu HTTP Method được ExpressJS hỗ trợ, dưới dạng tên là chữ viết thường, vd ```app.get()```, ```app.post()```).
  Ví dụ dưới đây mô tả một hàm ko khai báo đường dẫn cụ thể, do đó nó sẽ được thực hiện mỗi lần request:
  ```
  var app = express()

app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})
```
Ví dụ dưới đây dùng hàm use đến đường dẫn ```/user/:id.``` Hàm này sẽ được thực hiện mỗi khi request đến đường dẫn ```/user/:id``` bất kể phương thức nào (GET, POST,...):
```
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```
Tiếp theo là một ví dụ cho hàm được thực hiện mỗi khi truy cập đến đường dẫn ```/user/:id``` bằng phương thức GET:
```
app.get('/user/:id', function (req, res, next) {
  res.send('USER')
})
```
Khi muốn gọi một loạt hàm middleware cho một đường dẫn cụ thể, chúng ta có thể thực hiện như ví dụ dưới đây, bằng cách khai báo liên tiếp các tham số là các hàm sau tham số đường dẫn :
```
app.use('/user/:id', function (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}, function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```
Hoặc chúng ta có thẻ tách ra thành 2 lần khai báo ```app.use```, gọi là multiple routes, tuy nhiên ở các hàm phía trước cần gọi hàm ```next()``` khi kết thúc mỗi hàm, nếu không như ví dụ dưới đây, route thứ 2 sẽ không bao giờ được thực hiện do hàm thứ 2 trong route thứ nhất không gọi đến hàm ```next()```:
```
app.get('/user/:id', function (req, res, next) {
  console.log('ID:', req.params.id)
  next()
}, function (req, res, next) {
  res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', function (req, res, next) {
  res.end(req.params.id)
})
```
Khi muốn bỏ qua các hàm middleware tiếp theo không thực hiện nữa, chúng ta sẽ sử dụng lệnh ```next('route')```, tuy nhiên việc này chỉ tác dụng vưới các hàm middleware được load thông qua hàm ```app.METHOD``` hoặc ```router.METHOD```.
Ví dụ dưới đây mô tả một hàm middleware sẽ kết thúc ngạy lập tức khi tham số id=0:
```
app.get('/user/:id', function (req, res, next) {
  // if the user ID is 0, skip to the next route
  if (req.params.id === '0') next('route')
  // otherwise pass the control to the next middleware function in this stack
  else next()
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
app.get('/user/:id', function (req, res, next) {
  res.render('special')
})
```
### 3.2 Router-level middleware
Các middleware này về chức năng không khác gì so với application-level middlewware ở trên, tuy nhiên thay vì dùng biến ```app``` có thể gây nhầm lẫn với các thiết lập, phần router có thể không rõ ràng và khó phân biệt, ExpressJS cung cấp một đối tượng router chuyên dùng để khai báo route bằng cách gọi hàm sau:
```
var router = express.Router()
```
Phần code dưới đây mô tả một cách sử dụng router để thiết lập các route cần thiết cho một resource có tên là ```user```:
```
var app = express()
var router = express.Router()

// a middleware function with no mount path. This code is executed for every request to the router
router.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use('/user/:id', function (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}, function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get('/user/:id', function (req, res, next) {
  // if the user ID is 0, skip to the next router
  if (req.params.id === '0') next('route')
  // otherwise pass control to the next middleware function in this stack
  else next()
}, function (req, res, next) {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', function (req, res, next) {
  console.log(req.params.id)
  res.render('special')
})

// mount the router on the app
app.use('/', router)
```
### 3.3. Error-handling middleware
Đây là các middleware phục vụ cho việc xử lý lỗi. Một lưu ý là các hàm cho việc này luôn nhận bốn tham số (err, req, res, next). Khi muốn khai báo một middlware cho việc xử lý lỗi, bạn cần tạo một hàm có 4 tham số đầu vào. Mặc dù bạn có thể không cần sử dụng đối tượng next, nhưng hàm vẫn cần format với bốn tham số như vậy. Nếu không ExpressJS sẽ không thể xác định đó là hàm xử lý lỗi, và sẽ không chạy khi có lỗi xảy ra, chỉ hoạt động giống như các hàm middlware khác.
Đoạn code dưới đây mô tả một hàm xử lý lỗi truyền về cho client lỗi 500 khi có lỗi xảy ra từ server:
```
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```
### 3.4. Built-in middleware
Kể từ phiên bản 4.x, chỉ có một Built-in middlware duy nhất còn lại trong ExpressJS là ```express.static```, dựa trên thư viện serve-static, được dùng để cung cấp các nội dung tĩnh trong trang Web, ví dụ như các trang HTML tĩnh, các file hình ảnh, css, js, ...
Đoạn dưới đây mô tả việc sử dụng ```express.static``` để tạo ra một thư mục có tên là ```public```, người dùng có thể truy cập các file ```html``` và ```htm``` trong thư mục này:
```
var options = {
  dotfiles: 'ignore',
  etag: false,
  extensions: ['htm', 'html'],
  index: false,
  maxAge: '1d',
  redirect: false,
  setHeaders: function (res, path, stat) {
    res.set('x-timestamp', Date.now())
  }
}

app.use(express.static('public', options))
```
Ngoài ra bạn có thể khai báo nhiều thư mục static trong một web, đoạn code sau sẽ tạo ra 3 thư mục static :
```
app.use(express.static('public'))
app.use(express.static('uploads'))
app.use(express.static('files'))
```
### 3.5. Third-party middleware
Sử dụng Third-party sẽ giúp chúng ta thêm các chức năng cho Web App của mình mà không cần mất nhiều công implement.

Chúng ta sẽ cần cài đặt module thông qua ```npm```, sau đó khai báo sử dụng trong đối tượng ```app``` nếu dùng ở Application-level, hoặc qua đối tượng ```router``` nếu dùng ở Router-level.
Đoạn code sẽ cài đặt và sử dụng một middlware có tên là ```cookie-parser``` dùng để đọc cookies của request:
```
$ npm install cookie-parser
```
```
var express = require('express')
var app = express()
var cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```

  
  ## 4. File tĩnh trong ExpressJS
  Express cung cấp tiện ích express.static để phục vụ cho các file tĩnh như hình ảnh, css, js, ...Về cơ bản, bạn chỉ cần truyền tên thư mục nơi bạn giữ các file này, express.static sẽ sử dụng file đó một cách trực tiếp. Giả sử ứng dụng của bạn có cấu trúc như sau:
  ```
  node_modules
server.js
public/
public/images
public/images/logo.png
```
Sử dụng Express static:
```
app.use(express.static('public'));
```

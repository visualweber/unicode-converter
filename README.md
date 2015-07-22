UConvert
=========


## Giới thiệu

UConvert hiện tại cho phép bạn chuyển đổi qua lại giữa các bảng mã của tiếng Việt. Hiện tại hỗ trợ 4 bảng mã:

- UNICODE
- VNI
- TCVN3
- VIQR

Sẽ sớm hỗ trợ các bảng mã còn lại trong tương lai.

## Cài đặt

UConvert có sẵn trên [Github](https://github.com/visualweber/unicode-converter) và 

### Qua Composer

Nếu bạn sử dụng [Composer](https://getcomposer.org/) để quản lý thư viện cho dự án của mình, một cách dễ dàng nhất, thêm `"visualweber/unicode-converter": "dev-master"` vào phần `require` trong file `composer.json`:

```
"require": {
	"visualweber/unicode-converter": "dev-master"
}
```

Tiếp theo, update lại các gói:

```sh
composer update
```

### Thủ công

Nếu bạn chưa quen với Composer vì lý do gì, UConvert cho bạn một cách thủ công để nhúng nó vào dự án của bạn.

Đầu tiên, tải UConvert : (https://github.com/visualweber/unicode-converter/archive/master.zip):

Giải nén tập tin và bạn nên để tên thư mục chứa mã nguồn là `u-convert`. Ném nó vào thư mục chứa thư viện bên thứ 3 của bạn hoặc bất cứ nơi đâu bạn thích :)

Nhúng nó vào nơi bạn cần sử dụng:

```php
<?php

require '/path-to-libs/u-convert/autoload.php';

//..
```

## Sử dụng

### Quy chuẩn về tên bảng mã

Trước khi vào phần sử dụng bạn cần biết tên chuẩn của các bảng mã mà UConvert sử dụng.

Tất cả các tên bảng mã đều *phải* viết **HOA** và liền không dấu. Ví dụ *UNICODE*, *VNI*, *TCVN3*, *VIQR*...

Trong lớp `UConvert\UConvert` một số hằng được khai báo giúp bạn nhất quán trong việc gọi tên bảng mã:

```php
<?php

namespace UConvert;

class UConvert implements UConvertInterface {

	const UNICODE = 'UNICODE';
	const TCVN3   = 'TCVN3';
	const VNI     = 'VNI';
	const VIQR    = 'VIQR';

```

### Khởi tạo thông thường

UConvert cung cấp một cách rất dễ dàng để sử dụng, hãy xem một ví dụ:

```php
<?php
// Autoload library...

use UConvert\UConvert;

$vni_string = "Xin chaøo theá giôùi";

// Khoi tao UConvert voi string va bang ma cua no.
$convert    = new UConvert($vni_string, UConvert::VNI);

// Chuyen doi sang UNICODE
echo $convert->transform(UConvert::UNICODE);

// Output: Xin chào thế giới
```

Construct của UConvert chấp nhận 2 đối số:

`UConvert\UConvert( string $text, string $character)`

`$text`: Nội dung bạn muốn chuyển đổi.

`$character`: Tên bảng mã hiện tại của nó.

Sau khi khởi tạo bạn cần gọi method `transform(string $toCharacter)` với tham số là tên bảng mã cần chuyển đến để chuyển nó sang bảng mã cuối.

### Gọi trực tiếp qua static.

Ngoài ra thay vì phải khởi tạo lớp, UConvert cho phéo bạn gọi trực tiếp tới một số static-method *đặc biệt* chuyển đổi.

Những static-method đặc biệt là: `to` + tên bảng mã sẵn có (trong hệ thống) viết liền và viết hoa chữ cái đầu.

Dưới đây là một ví dụ gọi trực tiếp kiểu static:

```php
<?php

use UConvert\UConvert;

UConvert::toUnicode($vni, UConvert::VIQR);

UConvert::toVni($unicde, UConvert::UNICODE);

UConvert::toTcvn3($vni, UConvert::VNI);

Convert::toViqr($tcvn3, UConvert::TCVN3);
```

## Hạn chế

- Chưa hỗ trợ đầy đủ các bảng mã (sẽ dần có sớm).
- Thiếu cơ chế tự động nhận diện bảng mã của chuỗi nhập vào (đang xem xét tuy nhiên gặp khó khăn vài regex kém @@)
- Đọc, chuyển đổi và ghi từ text-file, hay word, excel...
- ...


## Đóng góp

Nếu bạn có bất kỳ chỉnh sửa, thêm mới... bạn có thể:
Gửi pull-request tại: [https://github.com/visualweber/unicode-converter/pulls](https://github.com/visualweber/unicode-converter/pulls)

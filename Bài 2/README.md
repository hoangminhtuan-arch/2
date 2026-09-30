# Phân tích lỗi & Bảng Test Cases

## 1. Phân tích lỗi mã nguồn
- **Lỗi lấy nhầm xe trong hàng đợi:** Trong mảng, phương thức `.pop()` sẽ xóa và trả về phần tử nằm ở cuối mảng. Việc dùng `.pop()` khiến cho chiếc xe mới xếp hàng sau cùng lại được gọi vào sạc trước tiên. Điều này là sai với nguyên tắc điều phối xe (ai đến trước sạc trước).
  - **Cách sửa:** Đổi phương thức `.pop()` thành `.shift()` để lấy phần tử đầu tiên của mảng, đảm bảo đúng thứ tự xe đến sớm nhất sẽ được sạc trước.
- **Lỗi lặp quá giới hạn (Out of bounds) khi in danh sách:** Vòng lặp `for` hiển thị bảng LED có điều kiện lặp là `i <= hangDoiXeCho.length`. Do chỉ số (index) của mảng bắt đầu từ `0` nên phần tử cuối cùng sẽ nằm ở vị trí `length - 1`. Việc chạy vòng lặp đến chỉ số `length` sẽ truy xuất một phần tử không tồn tại trong mảng, khiến chương trình in ra dòng chữ có chứa giá trị `undefined`.
  - **Cách sửa:** Đổi điều kiện lặp thành `i < hangDoiXeCho.length` để duyệt chính xác đến phần tử cuối cùng.

## 2. Bảng Test Cases (Đối chứng)

| Trường hợp kiểm thử | Dữ liệu đầu vào | Kết quả sai thực tế (Mã nguồn cũ) | Kết quả đúng mong đợi (Sau khi sửa) |
| --- | --- | --- | --- |
| Điều phối xe vào sạc | Hàng đợi hiện tại: `['30A-98765', '29B-12345', '51C-45678']` | Xe được gọi vào sạc: `51C-45678` (Xe cuối) | Xe được gọi vào sạc: `30A-98765` (Xe đầu) |
| Hiển thị danh sách lên bảng LED | Hàng đợi cập nhật sau khi lấy xe và thêm xe `'43D-88888'` | Bảng LED in ra thừa dòng cuối cùng: `STT 4: undefined` | Bảng LED in ra đúng 3 chiếc xe còn lại, không bị lỗi dòng chữ `undefined` |

# SKY Cam 1.4 — app camera cho OPPO Find X8s

App camera viết bằng Kotlin + Jetpack Compose + CameraX, giao diện theo phong cách camera ColorOS 17
(nền đen, nút kính mờ trong suốt, chip zoom ở đáy khung ngắm).

## Chức năng
- **Chụp ảnh** (JPEG chất lượng cao, tùy chọn nút **HR** bật độ phân giải cao).
- **Đèn flash** (chạm biểu tượng tia chớp ở góc trên bên trái): khi chụp ảnh có 4 lựa chọn **Tắt / Bật / Tự động / Luôn bật**
  (Luôn bật = đèn pin sáng liên tục); khi quay video có **Tắt / Bật** (Bật = đèn pin).
- **Chụp đêm** (biểu tượng mặt trăng, chỉ ở chế độ Ảnh, camera sau): hiện nhãn cam bên trên hàng zoom,
  chạm nhãn để đổi thời gian phơi **Tự động / 1s / 3s / 5s**. App lấy độ sáng AE hiện tại, kéo dài phơi sáng
  và hạ ISO tương ứng; cảnh quá sáng thì tự rút ngắn thời gian. Nên đặt máy cố định hoặc dùng chân máy.
- **Bù sáng EV** (chạm chữ EV): thanh trượt, dùng được cả khi chụp ảnh và quay video; chạm số EV để đặt lại 0.
- **Bố cục kiểu iOS 18**: khung ngắm sát mép trên màn hình, các nút điều khiển (flash, đêm, EV, tỉ lệ), bộ lọc, zoom đều nằm đè lên khung ngắm; vùng đen bên dưới chỉ còn thanh chọn chế độ và nút chụp.
- **Tỉ lệ khung hình** (chạm chip tỉ lệ nằm cạnh EV ở góc trên bên trái để đổi): ảnh **4:3 / 16:9 / 1:1**, video **16:9 / 4:3**.
  Ảnh 1:1 được cắt vuông ở giữa; video 1:1 chưa hỗ trợ.
- **Bộ lọc màu** (nút bộ lọc bên phải hàng zoom): 20 bộ lọc mô phỏng phong cách phim và máy ảnh, xem trước ngay trên khung ngắm,
  ghi vào ảnh khi chụp (kèm hạt phim và tối góc tùy bộ lọc).
  - Fuji (8): Provia, Velvia, Astia, Classic Chrome, Classic Neg, Nostalgic Neg, Eterna, Acros.
  - Leica (6): Natural, Vibrant, Warm, Cool Street, B&W, B&W Hi-Con.
  - Nikon (6): Standard, Vivid, Portrait, Landscape, Monochrome, Flat.
- **Dấu chìm** (nút bên trái hàng zoom): chữ mờ ở góc ảnh hoặc khung trắng kiểu máy film bên dưới ảnh,
  nội dung tùy chỉnh, có thể kèm thông số chụp (tiêu cự, khẩu độ, tốc độ, ISO, ngày giờ).
- **Cài đặt camera** (biểu tượng bánh răng): chất lượng ảnh (Cao nhất / Cao / Chuẩn / Tiết kiệm), định dạng ảnh (JPEG / PNG / WebP),
  độ phân giải cao, chất lượng video (4K / Full HD / HD), lưới 3×3, âm thanh chụp. Cài đặt được lưu lại cho lần sau.
- **Quay video** (ưu tiên 4K, tự hạ xuống FHD/HD nếu máy không hỗ trợ), có đồng hồ quay.
- **Zoom nhanh 1x · 2x · 3.5x · 7x** bằng chip, kèm zoom hai ngón tay và chạm để lấy nét.
- **Ánh sáng** (vệt sáng): phơi sáng dài 4 / 8 / 15 giây.
- **Pháo hoa**: phơi sáng dài 2 / 4 / 6 giây, lấy nét vô cực.
- Không có slow motion, tua nhanh, Xpan (theo yêu cầu).
- Ảnh và video lưu vào thư mục `DCIM/SKYCam` trong thư viện.

## Thông số ống kính OPPO Find X8s (theo công bố của nhà sản xuất)
| Ống kính | Thông số | Dùng cho |
|---|---|---|
| Chính | 50MP, f/1.8, OIS | 1x và 2x (cắt từ ống chính) |
| Tele | 50MP, f/2.8, zoom quang 3.5x, OIS | 3.5x và 7x (cắt 2x từ tele) |
| Góc siêu rộng | 50MP, f/2.0, 120° | chưa đưa vào (không yêu cầu) |

## Mở và chạy
1. Giải nén ZIP, mở thư mục `SKYCam` bằng Android Studio (thư mục chứa `settings.gradle.kts`).
2. Chờ Gradle Sync xong, cắm điện thoại, bật USB debugging, bấm Run.
3. Lần đầu mở, cho phép quyền Camera và Micro.

## Lưu ý quan trọng
- App của bên thứ ba chỉ dùng được camera qua API Android. Các thuật toán riêng của OPPO/Hasselblad
  (màu Hasselblad, HDR, chế độ ban đêm của ứng dụng gốc) không có sẵn, nên chất lượng ảnh có thể khác ứng dụng Camera gốc.
- Việc ColorOS có cho phép app ngoài dùng thẳng ống tele 3.5x hay không phụ thuộc vào máy; nếu không, 3.5x và 7x sẽ là zoom số.
- Chế độ Ánh sáng và Pháo hoa dùng phơi sáng thủ công (Camera2). Nếu ColorOS giới hạn thời gian phơi sáng cho app ngoài,
  app sẽ tự hạ xuống mức tối đa máy cho phép và báo bằng thông báo. Nên dùng chân máy.
- Nút **HR** (độ phân giải cao) có thể làm chụp chậm hơn; nếu app báo lỗi khi bật, hãy tắt đi.
- Chụp đêm là phơi sáng dài do ứng dụng tự tính, không phải thuật toán ghép nhiều ảnh của OPPO; nếu máy không cho app ngoài phơi sáng thủ công, app sẽ báo và chụp thường.
- Bộ lọc, dấu chìm và định dạng PNG/WebP áp dụng cho **ảnh**; video quay ở dạng gốc (xem trước khung ngắm video không áp bộ lọc). Bộ lọc là mô phỏng, không phải sản phẩm chính thức của Fuji, Leica hay Nikon.
- PNG và WebP được chuyển đổi từ ảnh sau khi chụp (ảnh JPEG gốc bị thay bằng bản PNG/WebP); chưa hỗ trợ RAW/HEIC.

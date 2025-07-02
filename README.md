# Mô phỏng Truyền tin Âm thanh An toàn (AES-256 & RSA-2048)
🔄 Các thành phần sau khi sinh khóa
📤 Phía Người gửi (Alice)
Trường	Giải thích
✅ Khóa công khai của Alice	Dạng PEM, chia sẻ cho Bob để xác minh chữ ký khi nhận
🔐 Khóa riêng của Alice	Chỉ mình Alice giữ, dùng để ký tin nhắn âm thanh
📥 Khóa công khai của Bob (đã tự điền)	Alice cần khóa này để mã hóa khóa AES – gửi kèm theo âm thanh

📥 Phía Người nhận (Bob)
Trường	Giải thích
✅ Khóa công khai của Bob	Chia sẻ cho Alice, để mã hóa khóa AES
🔐 Khóa riêng của Bob	Chỉ Bob giữ, dùng để giải mã khóa AES được gửi kèm với âm thanh

🎤 Ghi âm Tin nhắn thoại
Thành phần	Mô tả
🔘 Nút Bắt đầu Ghi âm	Khi bấm vào, trình duyệt bắt đầu ghi âm tiếng nói của Alice
🟥 Nút Dừng Ghi âm	Kết thúc ghi âm
🟢 Trạng thái	Báo “Sẵn sàng” → hệ thống đã sẵn sàng để tiếp nhận thao tác ghi âm

📦 Kết quả Xử lý
Thành phần	Giải thích
📤 Gói tin được gửi đi (JSON)	Chưa có nội dung vì chưa ghi âm xong và mã hóa
📝 Nhật ký xử lý (Log)	Dòng trạng thái: Đã tạo khóa thành công! Sẵn sàng để ghi âm. cho biết hệ thống đã sinh khóa xong, sẵn sàng thực hiện các bước tiếp theo

🔐 💬 Tóm tắt hoạt động tiếp theo:
Sau bước này, hệ thống sẽ:

Ghi âm giọng nói của Alice.

Sinh khóa AES-256, mã hóa nội dung âm thanh.

Ký file âm thanh bằng khóa riêng RSA của Alice.

Mã hóa khóa AES bằng khóa công khai RSA của Bob.

Gửi toàn bộ gói gồm:

Dữ liệu âm thanh đã mã hóa bằng AES

Khóa AES đã được mã hóa RSA

Chữ ký số (RSA SHA-256)

👉 Khi nào gói tin sẽ xuất hiện ở phần JSON?
➡ Sau khi bạn thực hiện ghi âm và hệ thống thực hiện mã hóa, phần JSON và Log sẽ được cập nhật.
🧑‍💻 3. Kỹ thuật – Công nghệ sử dụng (theo hình mô phỏng)
🔧 Ngôn ngữ & Framework:
Python + Flask: Là nền tảng chính để xây dựng ứng dụng web phía backend, giúp xử lý việc tạo khóa RSA, mã hóa AES, ghi âm và truyền dữ liệu giữa các bên.

Flask cung cấp API và hiển thị giao diện thông qua HTML templates.

🔐 Thuật toán mã hóa & bảo mật:
AES-256 (Advanced Encryption Standard – 256 bit):

Được dùng để mã hóa dữ liệu âm thanh trước khi gửi.

Khóa AES là ngẫu nhiên, chỉ dùng một lần cho mỗi lần gửi tin.

Khóa AES này sẽ được mã hóa bằng RSA trước khi gửi cho người nhận.

RSA-2048:

Cặp khóa riêng/công khai được tạo ra cho cả Alice và Bob.

RSA dùng để:

Ký số dữ liệu âm thanh bằng khóa riêng của Alice (đảm bảo xác thực & chống giả mạo).

Mã hóa khóa AES bằng khóa công khai của Bob (đảm bảo chỉ Bob có thể giải mã).

🎧 Xử lý âm thanh:
Ghi âm trực tiếp trên trình duyệt bằng HTML5, lưu dưới dạng blob/audio file và chuyển thành dạng nhị phân để mã hóa.

File âm thanh sau ghi sẽ được mã hóa + ký số trước khi đóng gói và gửi đi.

💻 Giao diện Web:
HTML + CSS được sử dụng để thiết kế giao diện chia thành 2 phần:

Phía Người gửi (Alice): Ghi âm, tạo/gửi khóa, ký dữ liệu.

Phía Người nhận (Bob): Nhận, giải mã và xác minh dữ liệu.

Các vùng hiển thị khóa RSA, vùng nhập/ghi âm, trạng thái và kết quả xử lý đều tương tác trực tiếp qua trình duyệt.

🌐 Triển khai & chia sẻ:
Google Colab + Ngrok:

Flask server được chạy trực tiếp trên Google Colab mà không cần cài đặt gì thêm trên máy cá nhân.

Ngrok tạo ra một đường dẫn truy cập công khai, giúp dễ dàng chia sẻ hoặc demo ứng dụng từ xa

# 🖥️ Giao diện minh họa
![image](https://github.com/user-attachments/assets/ab939397-32fd-4000-a9d0-9bf9b66aca77)

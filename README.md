# 🌌 Star Core: Vũ Trụ 3D Tương Tác Bằng Cử Chỉ (Hand Gesture Control)

**Star Core** là một ứng dụng web mô phỏng vũ trụ 3D theo phong cách Sci-fi, cho phép người dùng tương tác và điều khiển góc nhìn hoàn toàn thông qua **cử chỉ tay (Hand Tracking)** từ webcam mà không cần chuột hay bàn phím.

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Tech Stack](https://img.shields.io/badge/Tech-Three.js%20|%20MediaPipe%20|%20Tailwind-blue)

## ✨ Tính Năng Nổi Bật

* **Đồ họa 3D Chân thực:** Render vũ trụ với hàng nghìn hạt (particles), tinh vân (nebula), và hiệu ứng ánh sáng (glow) sử dụng WebGL.
* **Điều khiển không chạm (Touchless):** Sử dụng AI để nhận diện bàn tay và ngón tay theo thời gian thực.
* **Giao diện HUD Sci-fi:** Thiết kế UI phong cách Glassmorphism (Kính mờ) hiện đại với các hiệu ứng neon và hoạt ảnh mượt mà.
* **Tối ưu hóa:** Chạy mượt mà trên trình duyệt web mà không cần cài đặt phần mềm bổ trợ.

## 🛠 Công Nghệ Sử Dụng

Dự án được xây dựng dựa trên các thư viện lõi sau:

1.  **[Three.js](https://threejs.org/):**
    * Xây dựng môi trường 3D, camera, ánh sáng và hệ thống hạt (Particle System).
    * Xử lý logic render và hoạt ảnh (Animation Loop).
2.  **[MediaPipe Hands](https://google.github.io/mediapipe/solutions/hands.html) (Google):**
    * Mô hình Machine Learning chạy trực tiếp trên trình duyệt.
    * Nhận diện 21 điểm mốc (landmarks) trên bàn tay với độ trễ thấp.
3.  **[Tailwind CSS](https://tailwindcss.com/):**
    * Styling giao diện người dùng (UI) nhanh chóng và hiện đại.
4.  **HTML5 & JavaScript (ES6+):**
    * Xử lý logic kết nối giữa AI và môi trường 3D.

---

## 🧠 Nguyên Lý Hoạt Động (How it Works)

Hệ thống hoạt động theo luồng dữ liệu khép kín sau:

### 1. Thu thập & Xử lý hình ảnh (Input)
* Webcam thu hình ảnh và gửi từng khung hình (frame) tới **MediaPipe Hands**.
* MediaPipe phân tích và trả về tọa độ 21 điểm khớp tay (x, y, z) đã được chuẩn hóa.

### 2. Phân tích cử chỉ (Logic Core)
Hệ thống tính toán dựa trên vị trí tương đối của các ngón tay:

* **Trạng thái Nắm tay (Fist):** Kiểm tra xem đầu ngón tay có nằm thấp hơn khớp giữa hay không. Nếu cả 4 ngón (trừ ngón cái) đều gập -> **Kích hoạt chế độ Xoay**.
* **Trạng thái Zoom (Two Fingers):** Kiểm tra nếu chỉ có ngón trỏ và ngón giữa duỗi thẳng. Tính khoảng cách Euclid giữa đầu ngón cái và ngón trỏ để xác định mức độ Zoom.
* **Góc nghiêng tay:** Tính toán góc vector tạo bởi cổ tay và ngón giữa để xác định độ nghiêng (Roll) của bàn tay.

### 3. Đồng bộ hóa 3D (Mapping)
* **Quaternion Rotation:** Sử dụng toán học Quaternion để xoay vũ trụ mượt mà theo chuyển động tay, tránh hiện tượng khóa trục (Gimbal Lock).
* **Smoothing (Lerp):** Áp dụng nội suy tuyến tính (Linear Interpolation) để chuyển động của camera không bị giật khi tín hiệu webcam bị nhiễu.

---

## 🎮 Hướng Dẫn Điều Khiển

Đưa tay bạn lên trước webcam (khoảng cách 0.5m - 1m) và thực hiện các cử chỉ sau:

| Cử Chỉ | Biểu Tượng | Hành Động | Cách Thực Hiện |
| :--- | :---: | :--- | :--- |
| **Nắm tay** | ✊ | **Xoay Vũ Trụ** | Nắm chặt bàn tay và di chuyển trái/phải/lên/xuống để xoay góc nhìn. |
| **Hai ngón** | ✌️ | **Phóng to / Thu nhỏ** | Giơ ngón trỏ và ngón giữa (như chữ V). Đưa tay lại gần hoặc ra xa camera để Zoom. |
| **Xòe tay** | 🖐 | **Nghiêng (Roll)** | Xòe bàn tay và nghiêng cổ tay sang trái hoặc phải để xoay vũ trụ theo trục Z. |

> **Lưu ý:** Giữ tay trong khung hình webcam ở góc dưới bên phải màn hình để hệ thống nhận diện tốt nhất.

---

## 🚀 Cài Đặt & Chạy Dự Án

Dự án là một file HTML duy nhất (Single File Component), tuy nhiên để truy cập Webcam, trình duyệt yêu cầu giao thức bảo mật hoặc server cục bộ.

### Cách 1: Sử dụng VS Code (Khuyên dùng)
1.  Cài đặt Extension **Live Server** trong VS Code.
2.  Mở file `index.html`.
3.  Chuột phải chọn **"Open with Live Server"**.
4.  Trình duyệt sẽ tự mở và yêu cầu cấp quyền Camera -> Chọn **Allow (Cho phép)**.

### Cách 2: Chạy trực tiếp (Có thể bị chặn)
* Chỉ cần click đúp vào file `index.html`.
* *Lưu ý:* Một số trình duyệt (như Chrome) chặn truy cập Camera khi mở file với đường dẫn `file://`.

---

## 📂 Cấu Trúc Mã Nguồn

```text
index.html
├── <head>: Import thư viện Three.js, MediaPipe, Tailwind
├── <body>
│   ├── #loader-screen: Màn hình chờ
│   ├── #canvas-container: Nơi Three.js vẽ 3D
│   ├── #ui-layer: Lớp giao diện HUD (Menu, Hướng dẫn)
│   ├── #webcam-container: Khung hiển thị camera nhỏ
│   └── <script>:
│       ├── UIManager: Quản lý hiển thị/ẩn UI
│       ├── Three.js Setup: Tạo Scene, Camera, Particles
│       ├── Logic Logic: Xử lý cử chỉ tay
│       └── Animation Loop: Vòng lặp vẽ hình

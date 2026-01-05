Dưới đây là bản dịch tiếng Việt cho file `README.md` của dự án, giữ nguyên định dạng Markdown để bạn có thể sao chép và sử dụng ngay:

***

<h1 align="center">OpenNOW</h1>

<p align="center">
  <strong>Client GeForce NOW mã nguồn mở được xây dựng từ đầu bằng Native Rust</strong>
</p>

<p align="center">
  <a href="https://github.com/zortos293/GFNClient/releases">
    <img src="https://img.shields.io/github/v/tag/zortos293/GFNClient?style=for-the-badge&label=Tải%20Xuống" alt="Tải Xuống">
  </a>
  <a href="https://github.com/zortos293/GFNClient/stargazers">
    <img src="https://img.shields.io/github/stars/zortos293/GFNClient?style=for-the-badge" alt="Sao">
  </a>
  <a href="https://discord.gg/8EJYaJcNfD">
    <img src="https://img.shields.io/badge/Discord-Tham%20Gia-7289da?style=for-the-badge&logo=discord" alt="Discord">
  </a>
</p>

---

## Tuyên bố miễn trừ trách nhiệm

Đây là một **dự án độc lập**, không liên kết với NVIDIA Corporation. Dự án được tạo ra với mục đích giáo dục. GeForce NOW là thương hiệu của NVIDIA. Người dùng tự chịu rủi ro khi sử dụng.

---

## Giới thiệu

OpenNOW là một client GeForce NOW tùy chỉnh được viết lại hoàn toàn bằng **Native Rust** (từ bỏ việc triển khai trên Tauri trước đây) nhằm đạt hiệu suất tối đa và sử dụng ít tài nguyên hơn. Nó sử dụng `wgpu` và `egui` để mang lại trải nghiệm chơi game đám mây mượt mà, hiệu năng cao.

**Tại sao chọn OpenNOW?**
- **Hiệu suất Native**: Được viết bằng Rust với các liên kết đồ họa không chi phí phụ trội (zero-overhead).
- **Tiềm năng không giới hạn**: Không có giới hạn nhân tạo về FPS, độ phân giải hoặc tốc độ bit (bitrate).
- **Tập trung vào quyền riêng tư**: Mặc định không có đo lường từ xa (telemetry).
- **Đa nền tảng**: Được thiết kế cho Windows, macOS và Linux.

---

## Hỗ trợ nền tảng

| Nền tảng | Kiến trúc | Trạng thái | Ghi chú |
|----------|--------------|--------|-------|
| **macOS** | ARM64 / x64 | ✅ Hoạt động | Nền tảng hoạt động đầy đủ. Hỗ trợ giải mã phần cứng VideoToolbox. |
| **Windows** | x64 | ✅ Hoạt động | **GPU Nvidia**: Đã kiểm tra & Hoạt động. <br> **AMD/Intel**: Chưa kiểm tra (có thể hoạt động qua D3D11). |
| **Windows** | ARM64 | ❓ Chưa kiểm tra | Có thể hoạt động nhưng chưa được xác minh. |
| **Linux** | x64 | ⚠️ Hoạt động một phần | **Cảnh báo:** Các vấn đề dai dẳng về mã hóa/giải mã có thể xảy ra tùy thuộc vào bản phân phối/driver. |
| **Linux** | ARM64 | ⚠️ Hoạt động một phần | **Raspberry Pi 4**: Hoạt động (H.264). <br> **Raspberry Pi 5**: Chưa kiểm tra. <br> **Asahi Linux**: ❌ Lỗi giải mã (Chưa có bộ giải mã phần cứng). |
| **Android** | ARM64 | 📅 Đã lên kế hoạch | Chưa có thời gian dự kiến (ETA). |
| **Apple TV** | ARM64 | 📅 Đã lên kế hoạch | Chưa có thời gian dự kiến (ETA). |

---

## Tính năng & Trạng thái triển khai

| Thành phần | Tính năng | Trạng thái | Ghi chú |
|-----------|---------|:------:|-------|
| **Cốt lõi** | Xác thực | ✅ | Quy trình đăng nhập bảo mật. |
| **Cốt lõi** | Thư viện Game | ✅ | Tìm kiếm & duyệt qua tích hợp Cloudmatch. |
| **Streaming** | RTP/WebRTC | ✅ | Triển khai phát luồng độ trễ thấp. |
| **Streaming** | Giải mã phần cứng | ✅ | Windows (D3D11), macOS (VideoToolbox), Linux (VAAPI). |
| **Đầu vào** | Chuột/Bàn phím | ✅ | Ghi nhận đầu vào thô (Raw input). |
| **Đầu vào** | Tay cầm (Gamepad) | ✅ | Hỗ trợ đa nền tảng qua `gilrs`. |
| **Đầu vào** | Dán từ Clipboard | 🚧 | Đã lên kế hoạch. |
| **Âm thanh** | Phát lại | ✅ | Âm thanh độ trễ thấp qua `cpal`. |
| **Âm thanh** | Micro | 🚧 | Đã lên kế hoạch. |
| **Giao diện** | Lớp phủ (Overlay) | ✅ | Số liệu thống kê trong luồng & cài đặt (egui). |
| **Media** | Phát lại tức thì | 🚧 | Sắp ra mắt (Giống NVIDIA). |
| **Media** | Chụp màn hình | 🚧 | Sắp ra mắt. |
| **Sửa lỗi** | Hỗ trợ iGPU | 🚧 | Đang tiến hành sửa các lỗi lạ của Intel/AMD. |

### 🎞️ Codec được hỗ trợ & Tăng tốc phần cứng

| Codec | Windows | macOS | Linux | Ghi chú |
|:---:|:---:|:---:|:---:|---|
| **H.264** | ✅ DXVA / NVDEC / QSV | ✅ VideoToolbox | ✅ VAAPI | Tiêu chuẩn cho hầu hết các luồng. |
| **HEVC (H.265)** | ✅ DXVA / NVDEC / QSV | ✅ VideoToolbox | ✅ VAAPI | Hiệu quả cao, băng thông thấp hơn. |
| **AV1** | ✅ NVDEC / QSV | ✅ VideoToolbox (M3+) | ⚠️ VAAPI | Yêu cầu dòng RTX 30/40 hoặc Intel Arc. Hoặc dòng M3+ trên macOS. |
| **Opus (Audio)** | ✅ Phần mềm | ✅ Phần mềm | ✅ Phần mềm | Âm thanh chất lượng cao, độ trễ thấp. |

> **Lưu ý:** Client sử dụng kết xuất zero-copy ở những nơi được hỗ trợ để giảm thiểu độ trễ.

### 🚀 Tính năng bổ sung (Độc quyền)
Các tính năng này không có trong client chính thức:

| Tính năng | Trạng thái | Mô tả |
|---------|:------:|-------------|
| **Hỗ trợ Plugin** | 🚧 | Thêm các tập lệnh tùy chỉnh để tương tác với điều khiển luồng/đầu vào. |
| **Giao diện (Theming)** | 🚧 | Tùy chỉnh hoàn toàn giao diện người dùng và các theme cộng đồng. |
| **Đa tài khoản** | 🚧 | Chuyển đổi giữa các tài khoản GFN một cách mượt mà. |
| **Chống treo máy (Anti-AFK)** | ✅ | Ngăn chặn hết hạn phiên (Ctrl+Shift+F10). |

### ⌨️ Điều khiển & Phím tắt

| Phím tắt | Hành động | Mô tả |
|----------|--------|-------------|
| **F11** | Keybind | Bật/Tắt toàn màn hình |
| **F3** | Keybind | Bật/Tắt Lớp phủ thống kê |
| **Ctrl+Shift+Q** | Keybind | Buộc thoát phiên |
| **Ctrl+Shift+F10**| Keybind | **Bật/Tắt Anti-AFK** (Trạng thái hiển thị trong console) |

---

## Xây dựng (Build)

**Yêu cầu:**
- Chuỗi công cụ Rust (1.75+)
- Thư viện phát triển FFmpeg (khuyên dùng v6.1+)
- `pkg-config`

```bash
git clone https://github.com/zortos293/GFNClient.git
cd GFNClient/opennow-streamer
cargo build --release
```

Để chạy ở chế độ phát triển (development mode):

```bash
cd opennow-streamer
cargo run
```

---

## Khắc phục sự cố

### macOS: "App is damaged" (Ứng dụng bị hỏng)
Nếu macOS chặn ứng dụng, hãy chạy lệnh:
```bash
xattr -d com.apple.quarantine /Applications/OpenNOW.app
```

---

## Ủng hộ dự án

OpenNOW là một dự án đam mê được phát triển hoàn toàn trong thời gian rảnh của tôi. Tôi thực sự tin tưởng vào phần mềm mở và việc trao cho người dùng quyền kiểm soát trải nghiệm của họ.

Nếu bạn thích sử dụng client này và muốn ủng hộ sự phát triển liên tục của nó (và giúp tôi luôn tỉnh táo ☕), vui lòng cân nhắc trở thành nhà tài trợ. Sự ủng hộ của bạn giúp tôi dành nhiều thời gian hơn để sửa lỗi, thêm tính năng mới và duy trì dự án.

<p align="center">
  <a href="https://github.com/sponsors/zortos293">
    <img src="https://img.shields.io/badge/Sponsor_on_GitHub-EA4AAA?style=for-the-badge&logo=github-sponsors&logoColor=white" alt="Tài trợ trên GitHub">
  </a>
</p>

---

<p align="center">
  Được thực hiện bởi <a href="https://github.com/zortos293">zortos293</a>
</p>

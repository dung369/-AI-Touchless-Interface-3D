# 🤖 AI Touchless Interface 3D

Giao diện điều khiển không chạm (touchless interface) dựa trên AI Computer Vision và đồ họa 3D. Hệ thống cho phép người dùng tương tác với các hạt 3D thông qua cử chỉ tay mà không cần chạm vào bất kỳ thiết bị nào.

![Demo](https://img.shields.io/badge/Status-Active-success)
![Tech](https://img.shields.io/badge/Tech-Three.js%20%7C%20MediaPipe-blue)
![Performance](https://img.shields.io/badge/FPS-55--60-green)

## ✨ Tính năng chính

### 🎯 Tương tác không chạm Real-time
- **Phát hiện 2 bàn tay** qua camera với MediaPipe Hands AI
- **Mở rộng/Khép tay** → Điều khiển hạt phân tán/co lại thành hình cầu
- **Giơ ngón trỏ** → Đổi màu hạt tự động (AI nhận diện cử chỉ)
- **Vẫy tay** → Kích hoạt hiệu ứng đặc biệt
- Phản hồi real-time mượt mà (55-60 FPS)

### 🎨 Hệ thống hạt 3D
- **120 hạt** với thuật toán Fibonacci Sphere (phân bố đều)
- **InstancedMesh** - rendering tối ưu (1 draw call duy nhất)
- **Trạng thái thu gọn**: Hình cầu hoàn hảo
- **Trạng thái mở rộng**: Phân tán trong không gian 3D
- Chuyển đổi mượt mà giữa các trạng thái

### 🌈 Điều khiển màu sắc
- **10 màu neon** hiện đại tích hợp sẵn
- Đổi màu bằng cử chỉ hoặc click chuột
- Hiệu ứng phát sáng emissive động

### ⚡ Hiệu ứng 3D
- **🔄 Xoay (Rotate)**: Quay liên tục quanh trục
- **💓 Nhịp (Pulse)**: Đập theo nhịp điệu
- **🌊 Sóng (Wave)**: Hiệu ứng sóng nước chuyển động

### 📊 Giao diện thông minh
- **FPS Counter**: Hiển thị hiệu suất real-time
- **Hand Tracking**: Video preview với skeleton tracking
- **Status Panel**: Số tay phát hiện, khoảng cách, trạng thái cử chỉ
- **Responsive**: Tối ưu cho cả desktop và mobile

## 🛠️ Công nghệ sử dụng

| Công nghệ | Mục đích | Phiên bản |
|-----------|----------|-----------|
| **Three.js** | Rendering đồ họa 3D | 0.152.2 |
| **MediaPipe Hands** | AI phát hiện và tracking bàn tay | Latest |
| **InstancedMesh** | Tối ưu rendering (1 draw call) | Built-in |
| **Fibonacci Sphere** | Phân bố hạt đều trên mặt cầu | Custom |
| **WebGL** | GPU acceleration | Built-in |

## 🚀 Cách sử dụng

### Yêu cầu hệ thống
- Trình duyệt: Chrome, Edge, Safari (webkit-based)
- Camera: Webcam hoặc camera tích hợp
- GPU: Khuyến nghị có GPU rời để đạt 60 FPS

### Khởi chạy
1. Mở file `touchless_interface.html` trong trình duyệt
2. Cho phép truy cập camera khi được yêu cầu
3. Đợi AI khởi động (2-3 giây)
4. Bắt đầu điều khiển bằng cử chỉ tay!

## 🎮 Hướng dẫn điều khiển

### 1️⃣ Điều khiển Co/Giãn (2 tay)
```
┌─────────────────────────────────────────┐
│  👐 MỞ RỘNG HAI TAY                     │
│  ├─ Khoảng cách > 65%                   │
│  └─ Hạt phân tán ra không gian 3D       │
├─────────────────────────────────────────┤
│  🙏 KHÉP HAI TAY LẠI                    │
│  ├─ Khoảng cách < 30%                   │
│  └─ Hạt co lại thành hình cầu hoàn hảo  │
└─────────────────────────────────────────┘
```

### 2️⃣ Đổi màu tự động (1 tay)
```
┌─────────────────────────────────────────┐
│  👆 GIƠ NGÓN TRỎ                        │
│  ├─ Ngón trỏ duỗi thẳng                 │
│  ├─ Các ngón khác khép lại              │
│  └─ Màu sẽ đổi: Cyan → Pink → Purple... │
└─────────────────────────────────────────┘
```

### 3️⃣ Kích hoạt hiệu ứng (1 tay)
```
┌─────────────────────────────────────────┐
│  👋 VẪY TAY LÊN XUỐNG                   │
│  ├─ Di chuyển cổ tay nhanh 3-4 lần     │
│  ├─ Phát hiện đổi hướng ≥3 lần         │
│  └─ Hiệu ứng đổi: Xoay → Nhịp → Sóng   │
└─────────────────────────────────────────┘
```

## 🎯 Thuật toán AI

### 1. Phát hiện cử chỉ giơ ngón trỏ
```javascript
// Kiểm tra từng ngón tay
✓ Ngón trỏ (8): Duỗi (tip.y < pip.y)
✗ Ngón giữa (12): Khép (tip.y > pip.y)
✗ Ngón áo (16): Khép
✗ Ngón út (20): Khép
→ TRUE = Giơ ngón trỏ được phát hiện
```

### 2. Phát hiện vẫy tay (Improved Algorithm)
```javascript
// Tracking 10 frames liên tục
1. Lưu vị trí Y của cổ tay qua 10 frames
2. Tính toán thay đổi hướng (lên/xuống)
3. Đếm số lần đổi hướng
4. Nếu ≥3 lần đổi hướng → Vẫy tay
5. Cooldown 15 frames để tránh lặp lại
```

### 3. Tính khoảng cách 2 tay
```javascript
// Euclidean distance 2D
distance = √[(x1 - x2)² + (y1 - y2)²]

// Smoothing với factor 0.2
smoothDist = lastDist + (currentDist - lastDist) × 0.2

// Map to scale [0, 1]
scale = (smoothDist - 0.15) / (0.65 - 0.15)
→ 0 = Hình cầu hoàn hảo
→ 1 = Phân tán tối đa
```

## ⚙️ Tối ưu hóa Performance

### Rendering
- ✅ **InstancedMesh**: 120 hạt trong 1 draw call (thay vì 120 calls)
- ✅ **Low-poly geometry**: 4×4 segments (thay vì 8×8)
- ✅ **Pixel ratio**: Cố định 1× (không dùng devicePixelRatio)
- ✅ **Disabled buffers**: Tắt stencil, depth không cần thiết

### AI Processing
- ✅ **Model complexity**: 0 (model đơn giản nhất)
- ✅ **Frame skipping**: Xử lý mỗi 3 frames (thay vì mọi frame)
- ✅ **Low resolution**: Camera 320×240 (đủ cho hand tracking)
- ✅ **Throttling**: Không xử lý chồng chéo frames

### Animation
- ✅ **Manual lerp**: Tính toán thủ công nhanh hơn lerpVectors()
- ✅ **Cached vectors**: Tái sử dụng Vector3 objects
- ✅ **Smoothing**: Factor 0.15 cho chuyển động mượt mà

### Kết quả
```
┌─────────────────────┬──────────┬──────────┐
│ Metric              │ Trước    │ Sau      │
├─────────────────────┼──────────┼──────────┤
│ FPS                 │ 15-25    │ 55-60    │
│ Draw Calls          │ 600      │ 1        │
│ Particles           │ 600      │ 120      │
│ AI Processing       │ 30 FPS   │ 20 FPS   │
│ Smoothness          │ Giật     │ Mượt     │
└─────────────────────┴──────────┴──────────┘
```

## 📝 Cấu trúc dự án

```
touchless_interface.html
├── CSS Styling (Neon theme)
│   ├── Variables (colors, gradients)
│   ├── Layout (responsive)
│   └── Animations (pulse, glow)
│
├── HTML Structure
│   ├── Header (title)
│   ├── Canvas 3D (Three.js)
│   ├── Video Preview (camera feed + overlay)
│   ├── Control Panel
│   │   ├── Gesture Status
│   │   ├── Color Palette (10 colors)
│   │   └── Effect Buttons (3 effects)
│   └── Instructions
│
└── JavaScript Logic
    ├── Three.js Setup
    │   ├── Scene, Camera, Renderer
    │   ├── InstancedMesh (120 particles)
    │   ├── Lights (ambient + 2 point lights)
    │   └── Fibonacci Sphere Generation
    │
    ├── MediaPipe Hands
    │   ├── Hand Detection & Tracking
    │   ├── Gesture Recognition
    │   │   ├── Pointing (index finger)
    │   │   └── Waving (hand movement)
    │   └── Distance Calculation
    │
    ├── Animation System
    │   ├── Particle Lerp (sphere ↔ expanded)
    │   ├── Effects (rotate, pulse, wave)
    │   └── Smooth Transitions
    │
    └── UI Updates
        ├── FPS Counter
        ├── Status Display
        └── Visual Feedback
```

## 🎨 Bảng màu Neon

| Màu | Hex | RGB | Sử dụng |
|-----|-----|-----|---------|
| Cyan | `#00f3ff` | `rgb(0, 243, 255)` | Mặc định, viền |
| Pink | `#ff006e` | `rgb(255, 0, 110)` | Accent, highlight |
| Purple | `#8b00ff` | `rgb(139, 0, 255)` | Headers |
| Green | `#39ff14` | `rgb(57, 255, 20)` | Success, active |
| Yellow | `#ffff00` | `rgb(255, 255, 0)` | Warning |
| Orange | `#ff6b35` | `rgb(255, 107, 53)` | Alternative |
| Magenta | `#ff00ff` | `rgb(255, 0, 255)` | Special |
| Emerald | `#00ff88` | `rgb(0, 255, 136)` | Fresh |
| Red | `#ff4444` | `rgb(255, 68, 68)` | Alert |

## 🔧 Tùy chỉnh

### Thay đổi số lượng hạt
```javascript
// Line ~389
const PARTICLE_COUNT = 120; // Thay đổi số này (khuyến nghị: 80-200)
```

### Điều chỉnh độ nhạy cử chỉ
```javascript
// Vẫy tay - Line ~555
if(directionChanges >= 3) { // Giảm xuống 2 để nhạy hơn

// Giơ ngón trỏ - Cooldown line ~648
if(detectPointingGesture(hand) && currentTime - lastGestureTime > 1000) {
// Giảm 1000ms xuống 500ms để nhanh hơn
```

### Thêm màu mới
```javascript
// Line ~472
const colors = [
  '#00f3ff', '#ff006e', '#8b00ff', '#39ff14', '#ffff00',
  '#ff6b35', '#00ffff', '#ff00ff', '#00ff88', '#ff4444',
  '#YOUR_COLOR_HERE' // Thêm màu tùy chỉnh
];
```

### Tạo hiệu ứng mới
```javascript
// Thêm vào animateParticles() - Line ~740
if(currentEffect === 'spiral') {
  const angle = time * 2 + i * 0.1;
  tempPosition.x += Math.cos(angle) * 2;
  tempPosition.z += Math.sin(angle) * 2;
}
```

## 🐛 Xử lý sự cố

### Camera không hoạt động
```
✓ Kiểm tra quyền truy cập camera trong browser
✓ Thử trên HTTPS hoặc localhost
✓ Kiểm tra camera có hoạt động trong app khác không
```

### FPS thấp
```
✓ Giảm PARTICLE_COUNT xuống 80-100
✓ Tắt các ứng dụng khác đang chạy
✓ Đóng các tab browser không cần thiết
✓ Cập nhật driver GPU
```

### Cử chỉ không nhận diện
```
✓ Đảm bảo đủ ánh sáng
✓ Đưa tay vào giữa khung hình
✓ Giữ tay ổn định khi thực hiện cử chỉ
✓ Chờ indicator màu xanh lá bật lên
```

### Hạt không co lại thành cầu
```
✓ Khép 2 tay gần nhau hơn (< 30% distance)
✓ Kiểm tra cả 2 tay có được phát hiện không
✓ Refresh trang và thử lại
```

## 📊 Thông số kỹ thuật

| Thông số | Giá trị | Ghi chú |
|----------|---------|---------|
| Particles | 120 | Tối ưu cho 60 FPS |
| Sphere Radius | 12 units | Bán kính hình cầu |
| Geometry | 4×4 segments | Low-poly sphere |
| Camera FOV | 60° | Góc nhìn |
| Camera Distance | 50 units | Khoảng cách Z |
| AI Resolution | 320×240 | MediaPipe input |
| AI Model | Complexity 0 | Fastest model |
| Frame Skip | 3 frames | Process every 3rd |
| Smoothing | 0.15 | Animation lerp |
| Cooldown | 1000ms | Gesture timeout |

## 🌟 Demo Use Cases

### 1. Triển lãm nghệ thuật
- Tương tác không chạm với tác phẩm số
- Không cần thiết bị đặc biệt
- Trải nghiệm sạch sẽ, hiện đại

### 2. Giáo dục STEM
- Học về AI và computer vision
- Thực hành lập trình đồ họa 3D
- Hiểu thuật toán phát hiện cử chỉ

### 3. Showroom công nghệ
- Thu hút khách hàng với công nghệ mới
- Giới thiệu sản phẩm AI
- Interactive display không cần chạm

### 4. Game & Entertainment
- Điều khiển game bằng cử chỉ
- Karaoke effects real-time
- Interactive music visualization

## 📄 License

MIT License - Tự do sử dụng, chỉnh sửa và phân phối.

## 👨‍💻 Phát triển

### Cải tiến trong tương lai
- [ ] Thêm cử chỉ nắm đấm để reset
- [ ] Nhận diện khuôn mặt để thay đổi camera angle
- [ ] Export/Import cấu hình màu
- [ ] Ghi lại và replay cử chỉ
- [ ] Multi-user support (nhiều người)
- [ ] VR mode với WebXR

### Contributing
Mọi đóng góp đều được chào đón! Hãy tạo Pull Request hoặc Issue.

## 🙏 Credits

- **Three.js** - https://threejs.org
- **MediaPipe** - https://mediapipe.dev
- **Orbitron Font** - Google Fonts

---

**Tạo bởi AI với ❤️ | Real-time Touchless 3D Interface**

🚀 Khởi chạy ngay để trải nghiệm tương tác không chạm với AI!

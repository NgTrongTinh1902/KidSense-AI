src/
├── main.jsx                                  # 🚀 Entry point (ReactDOM)
├── App.jsx                                   # 🧭 Router & phân quyền
├── index.css                                 # 🎨 Tailwind + global styles
│
├── assets/                                   # 🖼️ Static Assets
│   ├── images/                               # Hình ảnh (logo, avatar, background)
│   │   ├── logo.png
│   │   ├── kid-avatar.png
│   │   └── world-bg.png
│   │
│   └── sounds/                               # Âm thanh game
│       ├── click.mp3
│       ├── correct.mp3
│       └── wrong.mp3
│
├── components/                               # 🧩 UI Components tái sử dụng
│   │
|   ├── error/        # ErrorBoundary, EmptyState 
│   ├── ui/                                   # Atomic Components
│   │   ├── Button.jsx                        # Nút bấm chuẩn
│   │   ├── Input.jsx                         # Input form
│   │   ├── Card.jsx                          # Thẻ nội dung
│   │   └── Modal.jsx                         # Popup / Dialog
│   │
│   ├── layout/                               # Layout nhỏ
│   │   ├── Header.jsx                        # Thanh header
│   │   ├── Footer.jsx                        # Footer
│   │   └── Sidebar.jsx                       # Menu bên
│   │
│   └── game/                                 # 🎮 Component game
│       ├── Timer.jsx                         # Đếm thời gian
│       ├── ScoreBoard.jsx                    # Bảng điểm
│       └── MicrophoneButton.jsx              # Nút ghi âm
│
├── layouts/                                  # 🧱 Page Layout theo role
│   ├── AuthLayout.jsx                        # Layout đăng nhập
│   ├── ChildLayout.jsx                         # Layout cho bé
│   ├── ParentLayout.jsx                      # Layout phụ huynh
│   |── AdminLayout.jsx                       # Layout admin
│   └── GameLayout.jsx                     # Layout game
|
|
├── pages/                                    # 📄 Các màn hình chính
│   │
│   ├── auth/                                 # 🔐 Authentication
│   │   ├── ParentLogin.jsx                   # Parent
|   |   ├── ChildLogin.jsx                    # Child
|   |   |── PCLogin.jsx                         ← wrapper switch      parent + child                  
│   │   └── AdminLogin.jsx                    # Admin
|   | 
│   ├── child/                                  # 🧒 Bé
│   │   ├── ChildDashboard.jsx                  # Chọn thế giới
│   │   └── WorldSelect.jsx                   # Chọn phòng chơi
│   │
│   ├── parent/                               # 👨‍👩‍👧 Phụ huynh
│   │   ├── ParentDashboard.jsx               # Tổng quan
│   │   └── ChildManagement.jsx               # Quản lý tài khoản con
│   │
│   ├── admin/                                # 🛠️ Quản trị
│   │   ├── AdminDashboard.jsx                # Trang tổng quan admin
│   │   ├── UserManagement.jsx                # Quản lý user
│   │   ├── ContentManagement.jsx             # Nội dung game
│   │   └── ReportManagement.jsx              # Báo cáo & thống kê
│   │
│   └── game/                                 # 🎯 Các phòng game
│       ├── ImageRoom.jsx                     # Phòng hình ảnh
│       ├── AudioRoom.jsx                     # Phòng nghe
│       ├── VideoRoom.jsx                     # Phòng video
│       └── VoiceRoom.jsx                     # Phòng ghi âm (AI)
│
├── services/                                 # 🌐 API Layer
│   ├── axiosClient.js                        # Axios + JWT interceptor
│   ├── authService.js                        # Login / logout / refresh
│   ├── gameService.js                        # API game
│   └── adminService.js                      # API admin
│
├── store/                                    # 🧠 Global State (Zustand)
│   ├── authStore.js                          # Trạng thái đăng nhập
│   ├── userStore.js                          # Thông tin user
│   └── gameStore.js                          # Điểm số, trạng thái game
│
├── hooks/                                    # 🪝 Custom Hooks
│   ├── useAuth.js                            # Kiểm tra đăng nhập
│   ├── useRole.js                            # Phân quyền
│   └── useAudioRecorder.js                  # Ghi âm giọng nói
│
├── utils/                                    # 🔧 Helper Functions
│   ├── formatTime.js                         # Format thời gian
│   ├── validateInput.js                     # Validate dữ liệu
│   └── constants.js                          # Hằng số hệ thống
│
└── config/                                   # ⚙️ Cấu hình
    └── env.js                                # API URL, môi trường

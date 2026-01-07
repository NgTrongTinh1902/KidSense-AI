# Frontend Architecture – VueJS (Enterprise Style)

## 📌 Project
**Phiêu Lưu Đa Giác Quan**  
Hệ thống trò chơi giáo dục đa giác quan cho trẻ em dựa trên AI đa phương thức  
Frontend xây dựng bằng **Vue 3 + Vite + Composition API + Pinia + TailwindCSS**

---

## 🧱 Tổng quan kiến trúc Frontend

Frontend được thiết kế theo **enterprise-style architecture**, tách rõ:
- Routing
- Layout theo role
- Page (screen-level)
- Business logic (composables, stores)
- Data access (services)

Phù hợp cho:
- Nhiều role (Parent / Child / Admin)
- Phát triển MVP
- Mở rộng thành sản phẩm thực tế

---

## 📂 Cấu trúc thư mục

```txt
src/
├── main.js                         # 🚀 Entry point
├── App.vue                         # 🧭 Root component
├── index.css                       # 🎨 Tailwind + global styles
│
├── assets/                         # 🖼️ Static assets (nhẹ)
│   ├── images/
│   │   ├── logo.png
│   │   ├── avatars/
│   │   └── worlds/
│   └── sounds/
│       ├── click.mp3
│       ├── correct.mp3
│       └── wrong.mp3
│
├── router/                         # 🧭 Routing & Guards
│   ├── index.js                    # Router config
│   ├── routes.js                   # Route definitions
│   └── guards/
│       ├── auth.guard.js           # Kiểm tra đăng nhập
│       ├── role.guard.js           # Kiểm tra role
│       └── child-session.guard.js  # Child login bằng PIN
│
├── layouts/                        # 🧱 Layout theo role
│   ├── PublicLayout.vue
│   ├── AuthLayout.vue
│   ├── ParentLayout.vue
│   ├── ChildLayout.vue
│   ├── AdminLayout.vue
│   └── GameLayout.vue
│
├── pages/                          # 📄 Screen-level pages
│   ├── public/
│   │   ├── HomePage.vue
│   │   ├── AboutPage.vue
│   │   └── PrivacyPolicy.vue
│   │
│   ├── auth/
│   │   ├── LoginPage.vue           # Parent / Admin
│   │   ├── ChildPinPage.vue        # Child login
│   │   └── CallbackPage.vue        # OAuth2
│   │
│   ├── parent/
│   │   ├── ParentDashboard.vue
│   │   ├── ChildManagement.vue
│   │   ├── LearningReport.vue
│   │   └── PrivacySettings.vue
│   │
│   ├── child/
│   │   ├── ChildDashboard.vue
│   │   ├── AvatarSelect.vue
│   │   └── ProgressPage.vue
│   │
│   ├── admin/
│   │   ├── AdminDashboard.vue
│   │   ├── UserManagement.vue
│   │   ├── ContentModeration.vue
│   │   ├── SystemSettings.vue
│   │   └── LogsPage.vue
│   │
│   └── game/
│       ├── RoomSelect.vue
│       ├── image/
│       │   └── ImageRoom.vue
│       ├── audio/
│       │   └── AudioRoom.vue
│       ├── video/
│       │   └── VideoRoom.vue
│       ├── voice/
│       │   └── VoiceRoom.vue
│       ├── text/
│       │   └── TextRoom.vue
│       └── SessionSummary.vue
│
├── components/                     # 🧩 Reusable components
│   ├── ui/
│   │   ├── BaseButton.vue
│   │   ├── BaseInput.vue
│   │   ├── BaseModal.vue
│   │   ├── BaseCard.vue
│   │   └── LoadingSpinner.vue
│   │
│   ├── layout/
│   │   ├── AppHeader.vue
│   │   ├── AppSidebar.vue
│   │   └── AppFooter.vue
│   │
│   ├── game/
│   │   ├── GameTimer.vue
│   │   ├── ScoreBoard.vue
│   │   ├── HintButton.vue
│   │   ├── RewardPopup.vue
│   │   └── MicrophoneButton.vue
│   │
│   └── error/
│       ├── ErrorBoundary.vue
│       └── EmptyState.vue
│
├── composables/                    # 🪝 Business logic (Vue hooks)
│   ├── useAuth.js
│   ├── useRole.js
│   ├── useChildSession.js
│   ├── useAudioRecorder.js
│   └── useGameSession.js
│
├── stores/                         # 🧠 Global state (Pinia)
│   ├── auth.store.js
│   ├── user.store.js
│   ├── game.store.js
│   ├── report.store.js
│   └── admin.store.js
│
├── services/                       # 🌐 API layer
│   ├── http.js                     # Axios + interceptors
│   ├── auth.service.js
│   ├── child.service.js
│   ├── game.service.js
│   ├── report.service.js
│   └── admin.service.js
│
├── utils/                          # 🔧 Helper functions
│   ├── constants.js
│   ├── formatTime.js
│   ├── validate.js
│   └── permission.js
│
├── config/                         # ⚙️ App configuration
│   ├── env.js
│   ├── roles.js
│   └── game.config.js
│
└── mocks/                          # 🧪 Mock data (MVP)
    ├── auth.mock.js
    ├── game.mock.js
    └── report.mock.js

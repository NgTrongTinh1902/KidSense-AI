




src/
├── main.js
├── App.vue
├── assets/
│
├── components/
│   ├── ui/
│   ├── layout/
│   ├── game/
│   └── error/
│
├── layouts/
│   ├── AuthLayout.vue
│   ├── ChildLayout.vue
│   ├── ParentLayout.vue
│   ├── AdminLayout.vue
│   └── GameLayout.vue
│
├── views/
│   ├── auth/
│   │   ├── ParentLogin.vue
│   │   ├── ChildLogin.vue
│   │   └── AdminLogin.vue
│   │
│   ├── child/
│   ├── parent/
│   ├── admin/
│   └── game/
│
├── router/
│   └── index.js          # nested routes + guard
│
├── store/
│   ├── authStore.js      # Pinia
│   ├── userStore.js
│   └── gameStore.js
│
├── composables/
│   ├── useAuth.js
│   ├── useRole.js
│   └── useAudioRecorder.js
│
├── services/
│   ├── axiosClient.js
│   ├── authService.js
│   ├── gameService.js
│   └── adminService.js
│
├── utils/
│
└── config/

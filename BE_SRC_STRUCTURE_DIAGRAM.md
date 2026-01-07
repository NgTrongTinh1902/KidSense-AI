# Sơ đồ Cấu trúc Thư mục SRC - LinkVerse Project

## Tổng quan Kiến trúc Microservices

```
chickend/
├── api-gateway/          (Cổng API chính)
├── identity-service/     (Xác thực & Phân quyền)
├── notification-service/ (Thông báo & Email)
└── profile-service/      (Quản lý Hồ sơ)
```

---

## 1. API GATEWAY (`api-gateway/src/`)

```
api-gateway/src/
└── main/
    ├── java/com/LinkVerse/gateway/
    │   ├── ApiGatewayApplication.java              # 🚀 Main Application
    │   │
    │   ├── configuration/                          # ⚙️ Cấu hình
    │   │   ├── AuthenticationFilter.java           # Bộ lọc xác thực JWT
    │   │   └── WebClientConfiguration.java         # Cấu hình WebClient
    │   │
    │   ├── dto/                                    # 📦 Data Transfer Objects
    │   │   ├── ApiResponse.java                    # Response chuẩn
    │   │   ├── request/
    │   │   │   └── IntrospectRequest.java          # Yêu cầu kiểm tra token
    │   │   └── response/
    │   │       └── IntrospectResponse.java         # Kết quả kiểm tra token
    │   │
    │   ├── repository/                             # 🔌 HTTP Clients
    │   │   └── IdentityClient.java                 # Client gọi Identity Service
    │   │
    │   └── service/                                # 🎯 Business Logic
    │       └── IdentityService.java                # Service xác thực
    │
    └── resources/
        ├── application.properties
        └── application.yml                         # Cấu hình Gateway Routes
```

**Chức năng chính:**
- 🔐 Xác thực JWT token cho tất cả requests
- 🔀 Định tuyến requests đến các microservices
- 🛡️ Bảo vệ các endpoints

---

## 2. IDENTITY SERVICE (`identity-service/src/`)

```
identity-service/src/
└── main/
    ├── java/com/LinkVerse/
    │   ├── IdentityServiceApplication.java         # 🚀 Main Application
    │   │
    │   ├── event/                                  # 📨 Event-Driven
    │   │   └── dto/
    │   │       ├── AuthoritiesSyncRequest.java     # Đồng bộ quyền
    │   │       ├── NotificationEvent.java          # Sự kiện thông báo
    │   │       └── UserEvent.java                  # Sự kiện người dùng
    │   │
    │   └── identity/
    │       │
    │       ├── annotation/                         # 🏷️ Custom Annotations
    │       │   └── RequirePermission.java          # Annotation phân quyền
    │       │
    │       ├── configuration/                      # ⚙️ Cấu hình
    │       │   ├── AppConfig.java                  # Cấu hình chung
    │       │   ├── ApplicationInitConfig.java      # Khởi tạo ứng dụng
    │       │   ├── AuthenticationRequestInterceptor.java
    │       │   ├── AuthoritiesSyncListener.java    # Listener đồng bộ
    │       │   ├── CoopConfig.java                 # Cấu hình COOP
    │       │   ├── CustomJwtDecoder.java           # Giải mã JWT custom
    │       │   ├── CustomOAuth2User.java           # OAuth2 User
    │       │   ├── FeignConfig.java                # Cấu hình Feign Client
    │       │   ├── JwtAuthConfig.java              # Cấu hình JWT
    │       │   ├── JwtAuthenticationEntryPoint.java # Entry point JWT
    │       │   ├── OAuth2SuccessHandler.java       # Xử lý OAuth2 thành công
    │       │   ├── OpenApiConfig.java              # Swagger/OpenAPI
    │       │   ├── RedisConfig.java                # Cấu hình Redis
    │       │   ├── SecurityConfig.java             # Spring Security
    │       │   └── WebMvcConfig.java               # Web MVC
    │       │
    │       ├── constant/                           # 📌 Constants
    │       │   └── PredefinedRole.java             # Roles được định nghĩa sẵn
    │       │
    │       ├── controller/                         # 🎮 REST Controllers
    │       │   ├── AdminController.java            # Quản trị viên
    │       │   ├── AuthenticationController.java   # Xác thực
    │       │   ├── GoogleLoginController.java      # Đăng nhập Google
    │       │   ├── LoginHistoryController.java     # Lịch sử đăng nhập
    │       │   ├── PermissionController.java       # Quản lý quyền
    │       │   ├── QrController.java               # QR Code
    │       │   ├── RoleController.java             # Quản lý vai trò
    │       │   └── UserController.java             # Quản lý người dùng
    │       │
    │       ├── dto/                                # 📦 Data Transfer Objects
    │       │   ├── ApiResponse.java
    │       │   ├── request/
    │       │   │   ├── AdminPasswordChangeRequest.java
    │       │   │   ├── ApiResponse.java
    │       │   │   ├── AuthenticationRequest.java   # Đăng nhập
    │       │   │   ├── ChildCreationRequest.java    # Tạo tài khoản con
    │       │   │   ├── ChildLoginRequest.java       # Đăng nhập con
    │       │   │   ├── ChildProfileCreationRequest.java
    │       │   │   ├── ExplainRequest.java
    │       │   │   ├── IntrospectRequest.java       # Kiểm tra token
    │       │   │   ├── LoginHistoryRequest.java
    │       │   │   ├── LogoutRequest.java           # Đăng xuất
    │       │   │   ├── PasswordChangeRequest.java   # Đổi mật khẩu
    │       │   │   ├── PermissionRequest.java
    │       │   │   ├── ProfileCreationRequest.java
    │       │   │   ├── ProfileUpdateRequest.java
    │       │   │   ├── ProfileUpsertRequest.java
    │       │   │   ├── RefreshRequest.java          # Làm mới token
    │       │   │   ├── RoleRequest.java
    │       │   │   ├── UserCreationRequest.java     # Tạo user
    │       │   │   ├── UserUpdateRequest.java
    │       │   │   ├── UserUpdateRequestAdmin.java
    │       │   │   └── WrongQuestionsRequest.java
    │       │   │
    │       │   └── response/
    │       │       ├── AuthenticationResponse.java  # Kết quả xác thực
    │       │       ├── ChildProfileResponse.java
    │       │       ├── IntrospectResponse.java
    │       │       ├── PageResponse.java            # Phân trang
    │       │       ├── PermissionResponse.java
    │       │       ├── RoleResponse.java
    │       │       ├── UserProfileResponse.java
    │       │       └── UserResponse.java
    │       │
    │       ├── entity/                             # 🗃️ Database Entities
    │       │   ├── AuthenticationProvider.java     # Provider (LOCAL/GOOGLE)
    │       │   ├── DeviceInfo.java                 # Thông tin thiết bị
    │       │   ├── Gender.java                     # Giới tính enum
    │       │   ├── InvalidatedToken.java           # Token đã vô hiệu
    │       │   ├── LoginHistory.java               # Lịch sử đăng nhập
    │       │   ├── Permission.java                 # Quyền
    │       │   ├── Role.java                       # Vai trò
    │       │   ├── User.java                       # Người dùng
    │       │   ├── UserStatus.java                 # Trạng thái user
    │       │   └── UserType.java                   # Loại user
    │       │
    │       ├── exception/                          # ⚠️ Exception Handling
    │       │   ├── AppException.java               # Custom exception
    │       │   ├── ErrorCode.java                  # Mã lỗi
    │       │   ├── GlobalExceptionHandler.java     # Xử lý lỗi toàn cục
    │       │   └── MessageException.java
    │       │
    │       ├── mapper/                             # 🔄 MapStruct Mappers
    │       │   ├── LoginHistoryMapper.java
    │       │   ├── PermissionMapper.java
    │       │   ├── ProfileMapper.java
    │       │   ├── RoleMapper.java
    │       │   └── UserMapper.java
    │       │
    │       ├── repository/                         # 💾 Data Access Layer
    │       │   ├── InvalidatedTokenRepository.java
    │       │   ├── LoginHistoryRepository.java
    │       │   ├── PermissionRepository.java
    │       │   ├── RoleRepository.java
    │       │   ├── UserRepository.java
    │       │   └── httpclient/                     # Feign Clients
    │       │       ├── NotificationClient.java     # Gọi Notification Service
    │       │       └── ProfileClient.java          # Gọi Profile Service
    │       │
    │       ├── service/                            # 🎯 Business Logic
    │       │   ├── AuthenticationService.java      # Xác thực & JWT
    │       │   ├── CustomOAuth2UserService.java    # OAuth2 Service
    │       │   ├── EventListenerService.java       # Lắng nghe events
    │       │   ├── FileStorageService.java         # Upload file
    │       │   ├── GoogleLoginService.java         # Đăng nhập Google
    │       │   ├── LoginHistoryService.java        # Lịch sử đăng nhập
    │       │   ├── NotificationService.java        # Gửi thông báo
    │       │   ├── PermissionCheckAspect.java      # AOP phân quyền
    │       │   ├── PermissionService.java          # Quản lý quyền
    │       │   ├── QrTokenService.java             # QR Code token
    │       │   ├── RoleService.java                # Quản lý vai trò
    │       │   └── UserService.java                # Quản lý user
    │       │
    │       ├── util/                               # 🔧 Utilities
    │       │   ├── DeviceInfoUtil.java             # Lấy thông tin device
    │       │   └── QrUtils.java                    # Tạo QR Code
    │       │
    │       └── validator/                          # ✅ Custom Validators
    │           ├── DobValidator/
    │           │   ├── DobConstraint.java          # Annotation ngày sinh
    │           │   └── DobValidator.java           # Validator ngày sinh
    │           ├── GenderValidator/
    │           │   ├── GenderConstraint.java
    │           │   └── GenderValidator.java
    │           └── PhoneValidator/
    │               ├── PhoneConstraint.java
    │               └── PhoneValidator.java
    │
    └── resources/
        ├── abc.properties
        ├── application.gradle
        ├── application.yaml
        └── serviceAccountKey.json                  # Firebase credentials
```

**Chức năng chính:**
- 🔐 Xác thực (JWT, OAuth2 Google)
- 👥 Quản lý người dùng, vai trò, quyền
- 📱 2FA với QR Code
- 📜 Lịch sử đăng nhập
- 🔄 Token refresh & invalidation

---

## 3. NOTIFICATION SERVICE (`notification-service/src/`)

```
notification-service/src/
└── main/
    ├── java/com.LinkVerse/
    │   │
    │   ├── event/                                  # 📨 Event DTOs
    │   │   └── dto/
    │   │       ├── BillEmailRequest.java           # Email hóa đơn
    │   │       └── NotificationEvent.java          # Sự kiện thông báo
    │   │
    │   └── notification/
    │       ├── NotificationServiceApplication.java # 🚀 Main Application
    │       │
    │       ├── configuration/                      # ⚙️ Cấu hình
    │       │   ├── CustomJwtDecoder.java
    │       │   ├── JwtAuthenticationEntryPoint.java
    │       │   ├── KafkaConsumerConfig.java        # Kafka Consumer
    │       │   ├── KafkaProducerConfig.java        # Kafka Producer
    │       │   ├── MailConfig.java                 # Cấu hình Email
    │       │   ├── OpenApiConfig.java              # Swagger
    │       │   ├── RedisConfig.java                # Redis
    │       │   ├── SecurityConfig.java             # Security
    │       │   ├── WebSocketConfig.java            # WebSocket
    │       │   └── WebSocketTokenInterceptor.java  # WebSocket Auth
    │       │
    │       ├── controller/                         # 🎮 REST Controllers
    │       │   ├── EmailController.java            # Quản lý Email
    │       │   ├── NotificationController.java     # Thông báo
    │       │   ├── OtpController.java              # OTP verification
    │       │   └── TwoFactorAuthController.java    # 2FA
    │       │
    │       ├── dto/                                # 📦 DTOs
    │       │   ├── ApiResponse.java
    │       │   ├── request/
    │       │   │   ├── AuthenticationRequest.java
    │       │   │   ├── EmailRequest.java           # Gửi email
    │       │   │   ├── IntrospectRequest.java
    │       │   │   ├── LogoutRequest.java
    │       │   │   ├── Recipient.java              # Người nhận
    │       │   │   ├── RefreshRequest.java
    │       │   │   ├── SendEmailRequest.java
    │       │   │   └── Sender.java                 # Người gửi
    │       │   │
    │       │   └── response/
    │       │       ├── AuthenticationResponse.java
    │       │       ├── EmailResponse.java
    │       │       └── IntrospectResponse.java
    │       │
    │       ├── entity/                             # 🗃️ Database Entities
    │       │   ├── InvalidatedToken.java
    │       │   ├── OtpRequest.java                 # OTP requests
    │       │   ├── PasswordResetToken.java         # Token reset mật khẩu
    │       │   └── User.java
    │       │
    │       ├── exception/                          # ⚠️ Exception Handling
    │       │   ├── AppException.java
    │       │   ├── ErrorCode.java
    │       │   └── GlobalExceptionHandler.java
    │       │
    │       ├── repository/                         # 💾 Data Access
    │       │   ├── AuthenticationRepository.java
    │       │   ├── InvalidatedTokenRepository.java
    │       │   ├── OtpRequestRepository.java
    │       │   ├── UserRepository.java
    │       │   └── httpclient/
    │       │       └── EmailClient.java            # HTTP Client gửi email
    │       │
    │       ├── service/                            # 🎯 Business Logic
    │       │   ├── EmailService.java               # Gửi email
    │       │   ├── OtpService.java                 # OTP logic
    │       │   ├── OtpStorageService.java          # Lưu OTP (Redis)
    │       │   ├── TokenService.java               # Token management
    │       │   └── TwoFactorAuthStorageService.java # 2FA storage
    │       │
    │       └── utils/                              # 🔧 Utilities
    │           └── EmailTemplateUtils.java         # Template email
    │
    └── resources/
        ├── application.yaml
        └── fonts/
            └── DejaVuSans.ttf                      # Font cho PDF
```

**Chức năng chính:**
- 📧 Gửi email (welcome, OTP, reset password, bills)
- 🔢 OTP verification
- 🔐 Two-Factor Authentication (2FA)
- 📨 Kafka event processing
- 🔔 WebSocket notifications (real-time)

---

## 4. PROFILE SERVICE (`profile-service/src/`)

```
profile-service/src/
└── main/
    ├── java/com/LinkVerse/profile/
    │   ├── ProfileServiceApplication.java          # 🚀 Main Application
    │   │
    │   ├── configuration/                          # ⚙️ Cấu hình
    │   │   ├── CustomJwtDecoder.java
    │   │   ├── CustomUserDetails.java              # User details custom
    │   │   ├── JwtAuthenticationEntryPoint.java
    │   │   └── SecurityConfig.java
    │   │
    │   ├── dto/                                    # 📦 DTOs
    │   │   ├── ApiResponse.java
    │   │   ├── PageResponse.java
    │   │   ├── request/
    │   │   │   ├── ChildProfileCreationRequest.java
    │   │   │   ├── ProfileCreationRequest.java     # Tạo profile
    │   │   │   ├── ProfileUpdateRequest.java       # Update profile
    │   │   │   ├── ProfileUpsertRequest.java
    │   │   │   └── UserProfileUpdateRequest.java
    │   │   │
    │   │   └── response/
    │   │       ├── ChildProfileResponse.java
    │   │       ├── PermissionResponse.java
    │   │       ├── RoleResponse.java
    │   │       ├── UserProfileResponse.java
    │   │       └── UserProfileUpdateResponse.java
    │   │
    │   ├── entity/                                 # 🗃️ Database Entities
    │   │   ├── ChildProfile.java                   # Profile con
    │   │   ├── Gender.java                         # Giới tính
    │   │   ├── UserProfile.java                    # Profile người dùng
    │   │   └── UserStatus.java                     # Trạng thái
    │   │
    │   ├── enums/                                  # 📌 Enums
    │   │   └── AppConst.java                       # Constants
    │   │
    │   ├── exception/                              # ⚠️ Exceptions
    │   │   ├── AppException.java
    │   │   ├── ErrorCode.java
    │   │   └── GlobalExceptionHandler.java
    │   │
    │   ├── mapper/                                 # 🔄 MapStruct Mappers
    │   │   ├── ChildProfileMapper.java
    │   │   └── UserProfileMapper.java
    │   │
    │   ├── repository/                             # 💾 Data Access
    │   │   ├── ChildProfileRepository.java
    │   │   ├── UserProfileRepository.java
    │   │   └── SearchRepository/
    │   │       └── criteria/
    │   │           └── SearchCriteria.java         # Tiêu chí tìm kiếm
    │   │
    │   ├── service/                                # 🎯 Business Logic
    │   │   ├── ChildProfileService.java            # Quản lý profile con
    │   │   └── UserProfileService.java             # Quản lý profile user
    │   │
    │   └── validator/                              # ✅ Custom Validators
    │       ├── DobValidator/
    │       │   ├── DobConstraint.java
    │       │   └── DobValidator.java
    │       ├── GenderValidator/
    │       │   ├── GenderConstraint.java
    │       │   └── GenderValidator.java
    │       └── PhoneValidator/
    │           ├── PhoneConstraint.java
    │           └── PhoneValidator.java
    │
    ├── resources/
    │   ├── application.properties
    │   ├── application.yaml
    │   └── static/                                 # Static resources
    │       ├── index.html
    │       ├── css/
    │       │   └── main.css
    │       ├── img/
    │       │   └── user_icon.png
    │       └── js/
    │           └── main.js
    │
    └── test/
        └── java/com/LinkVerse/profile/
            └── ProfileServiceApplicationTests.java
```

**Chức năng chính:**
- 👤 Quản lý profile người dùng
- 👶 Quản lý profile con (parental control)
- 🔍 Tìm kiếm profile
- 📊 CRUD operations cho profiles

---

## 📊 Sơ đồ Quan hệ giữa các Services

```
┌─────────────────┐
│   API GATEWAY   │ (Port: 8888)
│  (Entry Point)  │
└────────┬────────┘
         │
         │ Routes & Authenticates
         │
    ┌────┴────┬──────────┬──────────┐
    │         │          │          │
    ▼         ▼          ▼          ▼
┌─────────┐ ┌────────┐ ┌────────┐ ┌─────────┐
│IDENTITY │ │PROFILE │ │NOTIF   │ │ OTHERS  │
│SERVICE  │ │SERVICE │ │SERVICE │ │         │
│:8080    │ │:8083   │ │:8082   │ │         │
└────┬────┘ └───┬────┘ └───┬────┘ └─────────┘
     │          │           │
     │  Feign   │   Kafka   │
     ├──────────┤           │
     │          │           │
     └──────────┴───────────┘
```

---

## 🗂️ Cấu trúc Layer chung (Mỗi Service)

```
📁 Service Root
├── 🚀 Application.java           (Main class)
│
├── ⚙️ configuration/             (Spring configs)
│   ├── SecurityConfig
│   ├── JwtDecoder
│   ├── WebConfig
│   └── ...
│
├── 🎮 controller/                (REST APIs)
│   └── *Controller.java
│
├── 📦 dto/                       (Data Transfer)
│   ├── request/
│   └── response/
│
├── 🗃️ entity/                    (JPA Entities)
│   └── *.java
│
├── ⚠️ exception/                 (Error Handling)
│   ├── AppException
│   ├── ErrorCode
│   └── GlobalExceptionHandler
│
├── 🔄 mapper/                    (MapStruct)
│   └── *Mapper.java
│
├── 💾 repository/                (Data Access)
│   ├── *Repository.java
│   └── httpclient/              (Feign)
│
├── 🎯 service/                   (Business Logic)
│   └── *Service.java
│
├── ✅ validator/                 (Custom Validators)
│   └── *Validator/
│
└── 🔧 util/                      (Utilities)
    └── *Utils.java
```

---

## 🔑 Công nghệ sử dụng

### Backend Framework
- ☕ **Java 17+**
- 🍃 **Spring Boot 3.x**
- 🔒 **Spring Security** (JWT + OAuth2)
- 🌐 **Spring Cloud Gateway**
- 🔗 **Spring Cloud OpenFeign** (Service communication)

### Database & Cache
- 🐬 **MySQL** (Primary database)
- 🔴 **Redis** (Caching, OTP, Sessions)

### Message Queue
- 📨 **Apache Kafka** (Event-driven architecture)

### Real-time
- 🔌 **WebSocket** (Real-time notifications)

### Documentation
- 📖 **Swagger/OpenAPI 3** (API docs)

### Mapping
- 🔄 **MapStruct** (Object mapping)

### Validation
- ✅ **Bean Validation** (Custom validators)

---

## 📞 Giao tiếp giữa các Services

### 1. **Synchronous (Feign Client)**
```
Identity Service → Profile Service
Identity Service → Notification Service
API Gateway → Identity Service
```

### 2. **Asynchronous (Kafka)**
```
Identity Service → (Kafka) → Notification Service
  Events: UserCreated, PasswordReset, LoginAttempt
```

### 3. **WebSocket**
```
Client ↔ Notification Service
  Real-time: Notifications, Alerts
```

---

## 🔐 Luồng Xác thực

```
1. User → API Gateway (login)
2. API Gateway → Identity Service (authenticate)
3. Identity Service → Generate JWT
4. Identity Service → Redis (cache token)
5. Identity Service → return JWT
6. User → API Gateway (with JWT)
7. API Gateway → Validate JWT → Route to Service
8. Service → Process → Return Response
```

---

## 📝 Ghi chú

- **Common Patterns**: Tất cả services đều follow cấu trúc tương tự (Controller-Service-Repository)
- **Security**: JWT-based authentication qua API Gateway
- **Error Handling**: Centralized với GlobalExceptionHandler
- **Validation**: Custom validators cho phone, dob, gender
- **Mapping**: MapStruct cho entity ↔ DTO conversion
- **Documentation**: OpenAPI/Swagger cho mỗi service

---

## 🎯 Best Practices được áp dụng

✅ **Separation of Concerns** - Tách biệt logic rõ ràng  
✅ **DRY Principle** - Tái sử dụng code  
✅ **RESTful API Design** - Thiết kế API chuẩn  
✅ **Exception Handling** - Xử lý lỗi tập trung  
✅ **DTO Pattern** - Bảo mật entity  
✅ **Microservices Pattern** - Service độc lập  
✅ **Event-Driven** - Kafka messaging  
✅ **API Gateway Pattern** - Single entry point  

---

**Ngày tạo:** 13/12/2025  
**Dự án:** LinkVerse - Microservices Platform  
**Kiến trúc:** Spring Boot Microservices với API Gateway


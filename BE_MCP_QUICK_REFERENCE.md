# 📱 Ai_Dex Project - Quick Reference Guide

**Quét Dự Án:** 19 tháng 12, 2025

---

## 🎯 Dự Án Ai_Dex Là Gì?

**Nền tảng giáo dục đa phương tiện cho trẻ em (3-12 tuổi)**
- 5 loại thử thách tương tác (Image, Audio, Video, Voice, Text)
- AI Gemini phân tích & phản hồi
- Báo cáo chi tiết cho phụ huynh
- Gamification (XP, Levels, Streaks)

---

## 🏗️ Cấu Trúc Services

| Service | Port | Database | Status |
|---------|------|----------|--------|
| **API Gateway** | 8080 | - | ✅ Ready |
| **Identity Service** | 8081 | MySQL | ⚠️ Needs update |
| **Profile Service** | 8082 | MongoDB | ⚠️ Cleanup needed |
| **Notification Service** | 8083 | MongoDB | ✅ Ready |
| **AI Service** | 8084 | Redis+GCS | 🚨 **MISSING** |

---

## 🚨 Critical Issues Found

### #1: AI Service NOT IMPLEMENTED ⚠️⚠️⚠️
- Folder exists but no source code
- **Impact:** Cannot run any challenges
- **Fix:** Implement full AI service (3-4 weeks)

### #2: Identity Service Missing Fields
- No PIN lockout tracking
- No daily play time limits
- No parental consent tracking
- **Fix:** Add 12 new database columns

### #3: Port Collision
- Notification + AI both on port 8083
- **Fix:** Move AI Service to 8084

### #4: Profile Service Cleanup
- Unused exception: `FriendRequestNotFoundException.java`
- Unclear Elasticsearch/AWS Comprehend usage

---

## 📋 Technology Stack

```
Frontend:
- React/Vue/Angular (Not in this repo)

Backend:
- Java 21 + Spring Boot 3.2.5
- 4 Microservices (need 1 more)
- Maven for build

Databases:
- MySQL 8.0 (authentication)
- MongoDB 7.0 (profiles, notifications)
- Redis (caching, sessions)

Message Queue:
- Kafka (event streaming)

AI/ML:
- Google Gemini API (image, video, text)
- Google Speech-to-Text (audio)
- Google Text-to-Speech (voice)

DevOps:
- Docker & Docker Compose
- Kubernetes ready
```

---

## 📊 Database Summary

### MySQL (Identity Service)
```
users table:
- Authentication: username, email, password
- Parent-child: parentId, childPin
- Profile ref: profileId (MongoDB)
- Roles & Permissions
- Status: ACTIVE, INACTIVE, SUSPENDED
- Missing: PIN lockout, play limits, consent, XP/Level
```

### MongoDB (Profile Service)
```
Collections:
- userprofiles (parent info + preferences)
- childprofiles (child info + achievements)
- Optional: search indexes
```

### MongoDB (Notification Service)
```
Collections:
- notificationtemplates (email templates)
- notifications (sent log)
- otps (2FA codes)
```

---

## 🔑 Key Endpoints (via API Gateway)

### Authentication
```
POST   /api/auth/login              - Parent login
POST   /api/auth/child-login        - Child login (PIN)
POST   /api/auth/google-login       - Google OAuth2
POST   /api/auth/qr-generate        - Generate QR code
POST   /api/auth/qr-verify          - Verify QR login
```

### Profiles
```
GET    /api/profile/user/{userId}   - Get parent profile
GET    /api/profile/child/{childId} - Get child profile
PUT    /api/profile/child/{childId} - Update child profile
GET    /api/profile/child/{childId}/stats - Get stats
```

### Notifications
```
POST   /api/notification/send       - Send notification
GET    /api/notification/parent/{parentId} - Get notifications
POST   /api/notification/otp/generate - Generate OTP
POST   /api/notification/otp/verify - Verify OTP
```

### AI (🚨 Missing!)
```
POST   /api/ai/challenge/image-puzzle      - Image challenge
POST   /api/ai/challenge/audio-situation   - Audio challenge
POST   /api/ai/challenge/video-reaction    - Video challenge
POST   /api/ai/challenge/voice-response    - Voice challenge
POST   /api/ai/challenge/text-puzzle       - Text challenge
POST   /api/ai/analyze/image               - Analyze image response
POST   /api/ai/analyze/voice               - Analyze voice response
POST   /api/ai/hint/generate               - Generate hint
```

---

## 💾 Databases Status

| Database | Container | Port | Status | Credentials |
|----------|-----------|------|--------|-------------|
| MySQL | mysql | 3306 | ✅ Running | root/root |
| MongoDB | mongodb | 27017 | ✅ Running | root/root |
| Redis | redis-container | 6379 | ✅ Running | - |
| Kafka | kafka | 9092 | ✅ Running | - |

**Start with:**
```bash
docker-compose up -d
```

---

## 🎯 Top 3 Priorities

### Priority 1: Build AI Service (CRITICAL)
- [ ] Create ai-service Spring Boot project
- [ ] Integrate Gemini API
- [ ] Implement 5 challenge generators
- [ ] Add response analyzer
- Timeline: 3-4 weeks

### Priority 2: Update Identity Service (HIGH)
- [ ] Add child safety database fields
- [ ] Implement PIN lockout logic
- [ ] Add daily play time enforcement
- [ ] Add gamification tracking
- Timeline: 2-3 days

### Priority 3: Cleanup & Documentation (MEDIUM)
- [ ] Fix port collision (8084 for AI)
- [ ] Add Swagger/OpenAPI documentation
- [ ] Remove unused code
- [ ] Setup monitoring
- Timeline: 1 week

---

## 📁 Important Files

### Configuration
```
docker-compose.yml              - Service definitions
mcp.json                        - MCP configuration
package.json                    - Node.js deps (minimal)
check_token_mysql.sql           - DB utilities
```

### Documentation Generated Today
```
MCP_PROJECT_SCAN_REPORT.md      - Overview (this folder)
MCP_TECHNICAL_DEEP_DIVE.md      - Architecture details
MCP_ACTION_PLAN.md              - Step-by-step plan
```

### Existing Documentation
```
Ai_Dex_Project_Overview_Vietnamese.md - Project spec
PROJECT_STRUCTURE_ANALYSIS.md         - Architecture
SERVICES_ANALYSIS_AND_RECOMMENDATIONS.md - Detailed analysis
```

### API Documentation
```
Postman_Collection_LinkVerse.json       - API endpoints
Postman_Collection_LinkVerse_COMPLETE.json - Full API
```

---

## 🔍 File Locations

### Core Services
```
api-gateway/
├── Dockerfile
├── pom.xml
└── src/main/java/com/LinkVerse/gateway/

identity-service/
├── Dockerfile
├── pom.xml
└── src/main/java/com/LinkVerse/identity/

profile-service/
├── Dockerfile
├── pom.xml
└── src/main/java/com/LinkVerse/profile/

notification-service/
├── Dockerfile
├── pom.xml
└── src/main/java/com.LinkVerse/

ai-service/ (🚨 INCOMPLETE!)
├── Dockerfile
├── pom.xml (exists but needs updating)
└── src/ (MISSING!)
```

---

## ✅ Quick Checklist

**Today's Scan Results:**
- [x] Identified all 4 services
- [x] Analyzed database schemas
- [x] Found critical issues
- [x] Created action plan
- [x] Generated 3 comprehensive reports

**Next Steps:**
- [ ] Start AI Service development
- [ ] Update Identity Service schema
- [ ] Fix port collision
- [ ] Setup Swagger documentation
- [ ] Begin integration testing

---

## 📞 Questions to Ask Team

1. **Is AI Service planned or already in progress?**
   - Currently no source code found
   - This is blocking entire project

2. **What are preferred challenge types?**
   - Image, Audio, Video, Voice, Text - or customize?

3. **Should Elasticsearch be removed from Profile Service?**
   - Unused dependency found

4. **What's the target number of concurrent users?**
   - Needed for load testing & scaling

5. **Is Kafka fully utilized?**
   - Or is it for future event streaming?

---

## 📈 Project Health Score

```
Architecture:      ████████░░  8/10 (Good, missing AI service)
Code Quality:      ███████░░░  7/10 (Needs cleanup)
Documentation:     ██████░░░░  6/10 (Good, needs API docs)
Testing:           ███░░░░░░░  3/10 (Unknown)
DevOps:            █████░░░░░  5/10 (Docker ready, needs K8s)
Security:          ██████░░░░  6/10 (Good auth, needs hardening)

Overall: 6.3/10 (Ready for sprint, but needs AI service first)
```

---

## 🚀 Getting Started

### 1. Start Services
```bash
cd D:\chickend
docker-compose up -d
```

### 2. Check Services Are Running
```bash
docker-compose ps
```

### 3. Read Documentation
```
1. MCP_PROJECT_SCAN_REPORT.md (overview)
2. MCP_TECHNICAL_DEEP_DIVE.md (architecture)
3. MCP_ACTION_PLAN.md (implementation plan)
```

### 4. Begin Development
- Start with Priority 1: Build AI Service
- Use MCP_ACTION_PLAN.md as guide

---

## 💡 Tips

1. **Use MCP reports as reference** when coding
2. **Follow action plan priorities** - don't skip ahead
3. **Test each service independently** before integration
4. **Keep documentation updated** during development
5. **Review security considerations** before deployment

---

**Reports Generated by MCP Scanner**
**Date: 2025-12-19**

For detailed information, see:
- `MCP_PROJECT_SCAN_REPORT.md` - Full overview
- `MCP_TECHNICAL_DEEP_DIVE.md` - Architecture details
- `MCP_ACTION_PLAN.md` - Implementation steps


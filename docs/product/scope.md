# Scope Document — MVP v1.0

## ✅ IN SCOPE (ما نبنيه)

### 1. Authentication & Authorization (المصادقة والتفويض)

#### ما يُبنى:
- [ ] تسجيل الدخول بـ Email + Password
- [ ] 3 أدوار: Employee, Manager, HR
- [ ] Role-Based Access Control (RBAC)
- [ ] JWT Token-based Authentication
- [ ] Middleware للتحقق من الصلاحيات

#### ما لا يُبنى (مؤجل):
- تسجيل مستخدم جديد (نستخدم Seed Data)
- Forgot Password
- Email Verification
- Two-Factor Authentication (2FA)
- Single Sign-On (SSO)
- OAuth (Google, Microsoft)

#### السبب:
المستخدمون يُنشأون بواسطة Admin/HR. لا نحتاج Self-registration في MVP.

---

### 2. Request Management — Leave Only (إدارة الطلبات — إجازات فقط)

#### ما يُبنى:
- [ ] إنشاء طلب إجازة جديد
- [ ] حقول ثابتة:
  - نوع الإجازة (سنوية، مرضية، طارئة، ...)
  - تاريخ البداية
  - تاريخ النهاية
  - السبب (نص حر)
- [ ] عرض قائمة "طلباتي" (My Requests)
- [ ] عرض تفاصيل طلب محدد
- [ ] إلغاء طلب (إذا كان قيد الانتظار فقط)

#### ما لا يُبنى:
- أنواع طلبات أخرى (مشتريات، صيانة، ...)
- حقول مخصصة (Custom Fields)
- تعديل طلب بعد الإرسال
- نسخ طلب سابق
- طلب متكرر (Recurring)

#### السبب:
نركز على سيناريو واحد مكتمل قبل التوسع.

---

### 3. Hardcoded Workflow (سير عمل ثابت)

#### ما يُبنى:
- [ ] سير عمل واحد فقط: Employee → Manager → HR
- [ ] كل خطوة: Approve أو Reject
- [ ] تعليق اختياري مع كل قرار
- [ ] الحالات:
  - PENDING (قيد الانتظار)
  - MANAGER_APPROVED (مدير وافق)
  - APPROVED (موافقة نهائية)
  - REJECTED (مرفوض)

#### ما لا يُبنى:
- UI لتخصيص السير
- سير عمل متفرع (If/Else)
- سير عمل متوازي (Parallel Approval)
- Delegation (تفويض)
- Escalation (تصعيد تلقائي)

#### السبب:
السير الثابت يُثبت المفهوم. التخصيص يأتي لاحقاً.

---

### 4. Status Tracking (تتبع الحالة)

#### ما يُبنى:
- [ ] كل مستخدم يرى حالة طلباته
- [ ] الموظف يرى: "قيد الانتظار — مدير مباشر"
- [ ] المدير يرى: "تمت الموافقة — في انتظار HR"
- [ ] HR يرى: "موافقة نهائية"
- [ ] تاريخ كل تغيير حالة

#### ما لا يُبنى:
- Timeline بصري (Visual Timeline)
- Notifications (تنبيهات فورية)
- Email Updates
- Push Notifications

#### السبب:
الحالة المرئية كافية للـMVP. التنبيهات تُضاف لاحقاً.

---

### 5. Audit Log — Basic (سجل العمليات — أساسي)

#### ما يُبنى:
- [ ] تسجيل: من فعل ماذا ومتى
- [ ] Actions: CREATED, UPDATED, STATUS_CHANGED, APPROVED, REJECTED
- [ ] عرض في Admin Panel فقط
- [ ] Immutable (لا يمكن التعديل أو الحذف)

#### ما لا يُبنى:
- Advanced Search في Audit Log
- Filtering by Date/User/Action
- Export Audit Log
- Tamper-proof (Blockchain, etc.)
- Retention Policy

#### السبب:
السجل الأساسي يُثبت المفهوم. التحليل المتقدم يأتي لاحقاً.

---

### 6. User Interface (واجهة المستخدم)

#### ما يُبنى:
- [ ] شاشة تسجيل الدخول (Login)
- [ ] Dashboard رئيسي (حسب الدور)
  - Employee: "طلباتي" + زر "طلب جديد"
  - Manager: "طلبات تنتظر موافقتي" + "طلباتي"
  - HR: "جميع الطلبات" + "سجل العمليات"
- [ ] نموذج إنشاء طلب (Create Request Form)
- [ ] صفحة تفاصيل الطلب (Request Detail)
- [ ] صفحة الموافقة/الرفض (Approval View)

#### ما لا يُبنى:
- Settings Page
- Profile Page (بسيط فقط)
- Help/Documentation inside app
- Onboarding Tutorial
- Dark Mode
- Multi-language (English فقط للـMVP)

#### السبب:
4 شاشات تُكمل السيناريو. كل إضافة = تعقيد.

---

### 7. REST API

#### ما يُبنى:
- [ ] 6 Endpoints فقط:
  1. POST /api/auth/login
  2. POST /api/requests
  3. GET /api/requests (My Requests)
  4. GET /api/requests/pending (For Approvers)
  5. PATCH /api/approvals/:id
  6. GET /api/audit-logs (Admin only)

#### ما لا يُبنى:
- Pagination (للمجموعات الصغيرة)
- Filtering/Sorting
- Advanced Search
- Rate Limiting (Basic فقط)
- API Versioning
- Public API (External Access)
- Webhooks

#### السبب:
6 Endpoints تُكمل السيناريو. التعقيد يأتي مع النمو.

---

### 8. DevOps & Deployment

#### ما يُبنى:
- [ ] Docker Compose للتطوير
- [ ] Dockerfile لـBackend
- [ ] Dockerfile لـFrontend
- [ ] GitHub Actions CI (Run Tests)
- [ ] Deployment على Render/Railway

#### ما لا يُبنى:
- Kubernetes
- Load Balancing
- Auto-scaling
- CDN
- Monitoring (Grafana, etc.)
- Logging Aggregation (ELK, etc.)
- Backup Automation

#### السبب:
Docker + Render = يكفي للـMVP. الباقي يأتي مع النمو.

## ❌ OUT OF SCOPE (ما لا نبنيه — مؤجل)

| الميزة | مؤجل لـ | السبب | التأثير إذا أُضيف الآن |
|--------|---------|-------|------------------------|
| أنواع طلبات متعددة | v1.1 | يُعقد الـSchema | +2 أسابيع |
| نماذج ديناميكية | v2.0 | يحتاج تصميم معماري معقد | +4 أسابيع |
| سير عمل ديناميكي | v2.0 | يحتاج Workflow Engine | +6 أسابيع |
| إشعارات Email | v1.1 | يحتاج خدمة خارجية | +1 أسبوع |
| إشعارات Push | v1.1 | يحتاج PWA أو Native | +3 أسابيع |
| رفع الملفات | v1.1 | يحتاج Storage | +1 أسبوع |
| البحث المتقدم | v1.2 | يحتاج Indexing | +2 أسابيع |
| لوحة تحكم ورسوم بيانية | v1.2 | يحتاج Library إضافية | +2 أسابيع |
| تصدير Excel/PDF | v1.2 | يحتاج Libraries | +1 أسبوع |
| تعدد الإيجارات (Multi-tenant) | v3.0 | يُعقد الـArchitecture | +8 أسابيع |
| تطبيق موبايل | v3.0 | منصة مختلفة | +12 أسبوع |
| API خارجي | v2.0 | يحتاج Documentation كثير | +2 أسابيع |
| SSO | v2.0 | Enterprise feature | +4 أسابيع |
| 2FA | v1.2 | Security enhancement | +2 أسابيع |
| AI Module | v2.1 | Experimental | +8 أسابيع |
| Offline Mode | v2.0 | يحتاج PWA + Sync | +6 أسابيع |
| Multi-language | v1.2 | يحتاج i18n | +2 أسابيع |
| Dark Mode | v1.2 | Cosmetic | +1 أسبوع |
| Real-time Updates | v1.1 | يحتاج WebSocket | +2 أسابيع |

## إجمالي التأثير إذا أُضيف كل شيء: +70 أسبوعاً (سنة ونصف!)
## هذا هو السبب في أننا نؤجل.

## 📊 Scope Decision Matrix

### المعايير
| المعيار | الوزن | الشرح |
|---------|-------|-------|
| قيمة للمستخدم | 30% | هل تحل مشكلة حقيقية؟ |
| ضرورة للـMVP | 25% | هل الـMVP يعمل بدونها؟ |
| تعقيد التنفيذ | 20% | كم وقت يحتاج؟ |
| مخاطر تقنية | 15% | هل تقنية جديدة/غير مستقرة؟ |
| تبعيات | 10% | هل تحتاج ميزات أخرى؟ |

### التقييم
| الميزة | القيمة | الضرورة | التعقيد | المخاطر | التبعيات | المجموع | القرار |
|--------|--------|---------|---------|---------|----------|---------|--------|
| Auth + RBAC | 9 | 10 | 6 | 3 | 2 | **8.4** | ✅ In |
| Leave Request CRUD | 10 | 10 | 4 | 2 | 2 | **8.6** | ✅ In |
| Hardcoded Workflow | 9 | 9 | 5 | 3 | 3 | **7.9** | ✅ In |
| Audit Log | 6 | 5 | 4 | 2 | 2 | **5.1** | ✅ In |
| Notifications | 8 | 4 | 6 | 5 | 4 | **5.5** | ❌ Out |
| File Upload | 5 | 3 | 5 | 4 | 3 | **4.0** | ❌ Out |
| Dynamic Forms | 9 | 2 | 9 | 7 | 6 | **5.4** | ❌ Out |
| Reports | 7 | 3 | 6 | 4 | 4 | **4.9** | ❌ Out |
| Multi-tenant | 6 | 1 | 9 | 6 | 5 | **3.8** | ❌ Out |
| AI | 7 | 1 | 9 | 8 | 7 | **4.0** | ❌ Out |

### القاعدة الذهبية
&gt; "إذا لم تكن الضرورة ≥ 5، فهي Out"
&gt; "إذا كان التعقيد ≥ 8، فهي Out إلا إذا كانت الضرورة = 10"
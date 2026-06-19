# 🔍 Phân Tích Kỹ Thuật Đặc Biệt — Website MinhThach Learning

> **Công nghệ:** HTML5 + CSS3 thuần (Zero JavaScript)
> **Font:** Inter (Google Fonts) | **Icons:** Font Awesome 6

---

## 🎯 1. ZERO JAVASCRIPT

Toàn bộ website chạy **không một dòng JavaScript** nhưng vẫn có đầy đủ:
- Menu mobile (mở/đóng)
- FAQ accordion
- Pricing toggle
- Hover effects & animations

### a) Mobile Menu — "Checkbox Hack"

```html
<input type="checkbox" id="menu-toggle" />
<label for="menu-toggle" class="menu-toggle">
  <span></span><span></span><span></span>
</label>
<ul class="nav-menu">
  <!-- menu items -->
</ul>
```

```css
/* Mặc định: menu ẩn, trượt lên trên */
.nav-menu {
  transform: translateY(-120%);
  opacity: 0;
  transition: all 0.3s ease;
}

/* Khi checkbox được checked → menu hiện ra */
#menu-toggle:checked ~ .nav-menu {
  transform: translateY(0);
  opacity: 1;
}

/* Ẩn checkbox thật */
#menu-toggle { display: none; }
```

**Nguyên lý:** Dùng `:checked` pseudo-class + sibling selector `~` để toggle trạng thái. Label hamburger kích hoạt checkbox ẩn.

---

### b) FAQ Accordion — thẻ `<details>/<summary>` Native

```html
<details class="faq-item">
  <summary class="faq-question">
    <span>MinhThach Learning là gì?</span>
    <i class="fas fa-chevron-down"></i>
  </summary>
  <div class="faq-answer">Nội dung...</div>
</details>
```

```css
/* Ẩn marker mặc định của trình duyệt */
.faq-question::-webkit-details-marker { display: none; }
.faq-question::marker { display: none; content: ''; }

/* Xoay icon khi mở */
.faq-item[open] .faq-question i {
  transform: rotate(180deg);
  color: var(--primary);
}
```

**Nguyên lý:** `<details>` là HTML element có sẵn cơ chế open/close. CSS custom giao diện (ẩn marker gốc, thêm icon xoay).

---

## ✨ 1c. Header Glass Effect (không cần JS)

```css
.header {
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--gray-100);
  transition: var(--transition);
}

/* Fallback khi trình duyệt không hỗ trợ backdrop-filter */
@supports not (backdrop-filter: blur(16px)) {
  .header {
    background: var(--white);
  }
}

.header.scrolled {
  box-shadow: 0 4px 30px rgba(120, 86, 255, 0.08);
  border-bottom-color: rgba(120, 86, 255, 0.1);
}
```

**Nguyên lý:** Dùng `backdrop-filter: blur()` để tạo hiệu ứng kính mờ cho header. `@supports` đảm bảo fallback cho trình duyệt cũ.

---

## 🎨 2. DESIGN TOKEN QUA CSS VARIABLES

```css
:root {
  /* 🎨 Scrimba-Inspired Palette */
  --primary: #7856FF;        /* Tím Scrimba */
  --primary-dark: #5C3BE8;
  --primary-light: #9679FF;
  --primary-bg: #F0ECFF;

  --secondary: #0D0B1A;
  --secondary-light: #1A1530;
  --secondary-lighter: #2D2650;

  --accent: #FF708D;         /* Hồng Scrimba */
  --accent-dark: #E85A78;

  --bg: #F5F3FF;
  --white: #FFFFFF;

  --gray-50: #EEECF8;
  --gray-100: #DDD9ED;
  --gray-200: #BFB8D8;
  --gray-300: #9B92B8;
  --gray-400: #706B88;
  --gray-500: #4F4A66;
  --gray-600: #36314D;
  --gray-700: #241F3B;
  --gray-800: #140F29;
  --gray-900: #0A0719;

  --success: #10B981;
  --error: #EF4444;
  --warning: #F59E0B;

  --shadow-sm: 0 1px 2px rgba(120, 86, 255, 0.06);
  --shadow-md: 0 4px 16px rgba(120, 86, 255, 0.12);
  --shadow-lg: 0 10px 40px rgba(120, 86, 255, 0.15);
  --shadow-xl: 0 20px 60px rgba(120, 86, 255, 0.18);

  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 20px;
  --radius-xl: 28px;
  --radius-full: 9999px;

  --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  
  /* Gradients */
  --gradient-primary: linear-gradient(135deg, #7856FF, #FF708D);
  --gradient-accent: linear-gradient(135deg, #5C3BE8, #E85A78);
  --gradient-dark: linear-gradient(135deg, #0D0B1A 0%, #1A1530 100%);
  --gradient-card: linear-gradient(135deg, rgba(120, 86, 255, 0.03), rgba(255, 112, 141, 0.03));

  /* Star rating */
  --star: #F59E0B;
}
```

**Lợi ích:** Đổi toàn bộ theme chỉ bằng cách sửa giá trị trong `:root`.

---

## 🌈 3. GRADIENT BACKGROUNDS & DECORATIVE PSEUDO-ELEMENTS

### Hero gradient tối (Scrimba-style)

```css
.hero {
  background: var(--gradient-dark);
}
```

### Vòng tròn mờ trang trí (::before / ::after) — Màu tím Scrimba

```css
.hero::before {
  content: '';
  position: absolute;
  top: -50%;
  right: -20%;
  width: 700px;
  height: 700px;
  background: radial-gradient(circle, rgba(120, 86, 255, 0.12) 0%, transparent 70%);
  border-radius: 50%;
}

.hero::after {
  content: '';
  position: absolute;
  bottom: -30%;
  left: -10%;
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(255, 112, 141, 0.08) 0%, transparent 70%);
  border-radius: 50%;
}
```

### Text gradient tím-hồng

```css
.hero-title span {
  background: linear-gradient(135deg, var(--primary), var(--accent));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

### CTA gradient tím-hồng

```css
.cta {
  background: var(--gradient-primary);
}
```

---

## 🎞️ 4. HOVER EFFECTS — Card "Lift" & Image Zoom

```css
.course-card {
  transition: var(--transition);
  border: 1px solid var(--gray-100);
}

.course-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 16px 48px rgba(120, 86, 255, 0.18);
  border-color: var(--primary);
}

.course-card:hover .course-card-image img {
  transform: scale(1.08);
}

.course-card:hover .course-card-footer {
  background: linear-gradient(135deg, rgba(120, 86, 255, 0.06), rgba(255, 112, 141, 0.06));
}
```

Áp dụng cho: `.course-card`, `.blog-card`, `.testimonial-card`, `.pricing-card`, `.instructor-profile-card`, `.category-card`, `.value-card`

---

## 🌀 4b. Animations & Hiệu ứng chuyển động

### Section fade-in khi load
```css
.section {
  animation: fadeInUp 0.5s ease both;
}
.section:nth-child(2) { animation-delay: 0.1s; }
.section:nth-child(3) { animation-delay: 0.2s; }
```

### Hero image card float
```css
.hero-image-card {
  animation: float 4s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-8px); }
}
```

### Stat items hover
```css
.stat-item:hover .stat-icon {
  transform: scale(1.1);
  box-shadow: 0 0 30px rgba(255, 112, 141, 0.2);
}
.stat-item:hover {
  transform: translateY(-4px);
}
```

---

## 🎨 4c. Custom Scrollbar

```css
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-track {
  background: var(--bg);
}
::-webkit-scrollbar-thumb {
  background: var(--gray-200);
  border-radius: var(--radius-full);
}
::-webkit-scrollbar-thumb:hover {
  background: var(--primary-light);
}
```

---

## 🌈 4d. Section Gradient Divider

```css
.section + .section::before {
  content: '';
  display: block;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--primary-light), var(--accent), transparent);
  max-width: 400px;
  margin: 0 auto 60px;
  opacity: 0.3;
}
```

---

## 📐 5. CSS GRID LINH HOẠT — Responsive Breakpoints

```css
/* Desktop: 3 cột */
.courses-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px;
}

/* Tablet (max-width: 992px): 2 cột */
@media (max-width: 992px) {
  .courses-grid { grid-template-columns: repeat(2, 1fr); }
}

/* Mobile (max-width: 768px): 1 cột */
@media (max-width: 768px) {
  .courses-grid { grid-template-columns: 1fr; }
}
```

**4 breakpoints:**
| Breakpoint | Target |
|---|---|
| >992px | Desktop |
| ≤992px | Tablet |
| ≤768px | Mobile |
| ≤480px | Small Mobile |

---

## 🧩 6. STICKY SIDEBAR (không cần JS)

```css
.course-detail-sidebar {
  position: sticky;
  top: 100px;
}
```

Dùng trên 3 trang:
- `course-detail.html` — Sidebar giá + thông tin
- `instructor-detail.html` — Profile sidebar
- `blog-detail.html` — Blog sidebar (search, categories, recent posts)

---

## 🔤 7. CLAMP TEXT — Cắt nội dung quá dài

```css
.course-card-title {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

Áp dụng cho: title (2 dòng), description (2 dòng), blog excerpt (3 dòng)

---

## 🙌 7b. Logo Hover Animation

```css
.logo-icon {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.logo:hover .logo-icon {
  transform: scale(1.05) rotate(-3deg);
  box-shadow: 0 6px 20px rgba(120, 86, 255, 0.4);
}
```

---

## 📊 8. SKILL PROGRESS BARS

```html
<div class="skill-item">
  <div class="skill-header">
    <span>HTML5 & CSS3</span>
    <span>95%</span>
  </div>
  <div class="skill-bar">
    <div class="skill-bar-fill" style="width: 95%;"></div>
  </div>
</div>
```

```css
.skill-bar {
  height: 8px;
  background: var(--gray-100);
  border-radius: var(--radius-full);
  overflow: hidden;
}

.skill-bar-fill {
  height: 100%;
  border-radius: var(--radius-full);
  background: linear-gradient(90deg, var(--primary), var(--accent));
}
```

---

## 🔘 9. BUTTON SYSTEM — Component tái sử dụng

```css
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 24px;
  border-radius: var(--radius-sm);
  font-size: 15px;
  font-weight: 600;
  border: 1px solid transparent;
  transition: var(--transition);
}

.btn-primary { background: var(--gradient-primary); color: var(--white); }
.btn-primary:hover { background: var(--gradient-accent); transform: translateY(-3px); box-shadow: 0 12px 32px rgba(120, 86, 255, 0.4); }

.btn-outline { background: transparent; color: var(--primary); border-color: var(--primary); }
.btn-outline:hover { background: var(--gradient-primary); color: var(--white); transform: translateY(-3px); box-shadow: 0 12px 32px rgba(120, 86, 255, 0.35); }

.btn-white { background: rgba(255,255,255,0.15); backdrop-filter: blur(8px); color: var(--white); }

.btn-lg  { padding: 14px 36px; font-size: 16px; }
.btn-sm  { padding: 8px 16px; font-size: 13px; }
```

---

## ♿ 10. ACCESSIBILITY

```html
<!-- aria-label cho icon-only buttons -->
<a href="#" aria-label="Facebook"><i class="fab fa-facebook-f"></i></a>

<!-- Required indicator -->
<label for="email">Email Address <span class="required">*</span></label>

<!-- aria-label cho navigation -->
<nav class="pagination" aria-label="Phân trang khóa học">

<!-- Semantic HTML -->
<header>, <nav>, <section>, <article>, <footer>

<!-- Lazy loading -->
<iframe loading="lazy" ...></iframe>
```

---

## 🧪 11. PAGINATION (UI sẵn sàng kết nối backend)

```html
<nav class="pagination" aria-label="Phân trang khóa học">
  <a href="#" class="next-prev"><i class="fas fa-chevron-left"></i> Trước</a>
  <a href="#" class="active">1</a>
  <a href="#">2</a>
  <a href="#">3</a>
  ...
  <a href="#">14</a>
  <a href="#" class="next-prev">Sau <i class="fas fa-chevron-right"></i></a>
</nav>
```

---

## 📋 12. BADGE LEVELS — 3 cấp độ khóa học

```css
.badge-beginner   { background: var(--success); }   /* Xanh lá */
.badge-intermediate { background: var(--accent); }   /* Hồng */
.badge-advanced   { background: var(--error); }      /* Đỏ */
```

```html
<span class="course-card-badge badge-beginner">Cơ bản</span>
<span class="course-card-badge badge-intermediate">Trung cấp</span>
<span class="course-card-badge badge-advanced">Nâng cao</span>
```

---

## 🧰 13. UTILITY CLASSES

```css
.text-center, .text-primary, .text-white, .text-success,
.flex, .flex-center, .flex-between, .flex-wrap,
.gap-12, .gap-16, .gap-24, .gap-40,
.grid-2,
.mb-16, .mb-24, .mb-32, .mt-24, .mt-40, .mt-50,
.p-24, .p-32,
.bg-white, .bg-gray-50,
.rounded-md, .rounded-lg
```

---

## 🏆 TỔNG KẾT — Bảng kỹ thuật đặc biệt

| Kỹ thuật | Mục đích | File |
|---|---|---|
| `:checked` + `~` selector | Menu mobile toggle | Tất cả HTML + CSS |
| `<details>/<summary>` | FAQ accordion | `faq.html` + `style.css` |
| CSS Variables (`:root`) | Design tokens tập trung | `style.css` |
| `::before` / `::after` | Vòng tròn mờ trang trí | `style.css` (hero) |
| `background-clip: text` | Text gradient | `style.css` (hero) |
| `position: sticky` | Sidebar dính khi scroll | `style.css` |
| `-webkit-line-clamp` | Cắt text quá dài | `style.css` |
| CSS Grid `repeat(3, 1fr)` | Layout cards | `style.css` |
| 4 breakpoints media queries | Responsive design | `style.css` |
| `transform: translateY()` | Hiệu ứng nâng card | `style.css` |
| `transform: scale()` | Hiệu ứng zoom ảnh | `style.css` |
| Box-shadow transitions | Đổ bóng khi hover | `style.css` |
| Gradient linear/radial | Background & decorative | `style.css` |
| Button system (`.btn`) | Component tái sử dụng | `style.css` |
| Badge system | 3 cấp độ khóa học | `style.css` |
| Skill progress bars | Kỹ năng giảng viên | `instructor-detail.html` |
| Sticky sidebar | Course/Instructor/Blog | 3 trang HTML |
| Social auth buttons | Login/Register UI | `login.html`, `register.html` |
| Pricing toggle | Monthly/Yearly | `pricing.html` |
| Google Maps embed | Liên hệ | `contact.html` |
| Frosted glass (backdrop-filter) | Hero image card | `style.css` |
| Header glass effect (backdrop-filter) | Header kính mờ | `style.css` |
| Custom scrollbar | Scrollbar tùy chỉnh | `style.css` |
| Section fadeInUp animation | Hiệu ứng section xuất hiện | `style.css` |
| Float animation | Hero image card chuyển động | `style.css` |
| Section gradient divider | Phân cách section | `style.css` |
| Footer heading gradient underline | Footer heading đẹp | `style.css` |
| `.star` class + CSS variable | Rating stars | `style.css` + 4 HTML

---

> **Kết luận:** Website vận hành hoàn chỉnh chỉ với **HTML5 + CSS3 thuần** nhờ tận dụng triệt để các tính năng CSS hiện đại và HTML native. Phong cách Scrimba với bảng màu tím-hồng (#7856FF - #FF708D). Không cần JavaScript — không cần framework.

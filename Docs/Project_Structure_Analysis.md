# Phân Tích Cấu Trúc Dự Án (Project Structure Analysis)

Dựa trên việc quét và đọc các file trong dự án, dưới đây là phân tích chi tiết về cấu trúc và công nghệ được sử dụng (ngoại trừ `node_modules`).

## 1. Công Nghệ Chính (Tech Stack)
Dự án là một **Web Portfolio 3D** hiện đại sử dụng:
- **Core:** React 18, TypeScript.
- **Build Tool:** Vite.
- **3D Graphics:** Three.js, @react-three/fiber, @react-three/drei, maath.
- **Styling:** Tailwind CSS, PostCSS.
- **Animation:** Framer Motion, React Parallax Tilt.
- **Routing:** React Router DOM.

## 2. Cấu Trúc Thư Mục (Directory Structure)

### Root Directory
- **`src/`**: Chứa mã nguồn chính.
- **`public/`**: Chứa tài nguyên tĩnh (static assets) như `herobg.png` (được tham chiếu trong tailwind config).
- **`dist/`**: Thư mục đầu ra khi build (production).
- **Configuration Files:**
    - `vite.config.js`: Cấu hình Vite, plugin React.
    - `tailwind.config.cjs`: Cấu hình theme màu sắc, fonts, background images.
    - `tsconfig.json`: Cấu hình TypeScript.
    - `.eslintrc.cjs` / `.prettierrc.cjs`: Cấu hình Linting và Formatting.

### Source Directory (`src/`)

#### `src/components/`
Thư mục quan trọng nhất chứa các thành phần giao diện:
- **`canvas/`**: Chứa các component 3D (Three.js scenes).
    - `Earth.jsx`, `Ball.jsx`, `Computers.jsx`, `Stars.jsx`: Các cảnh 3D cụ thể.
- **`sections/`**: Các phần chính của trang Landing Page.
    - `Hero.jsx`: Phần mở đầu.
    - `About.jsx`, `Experience.jsx`, `Tech.jsx`, `Works.jsx`, `Feedbacks.jsx`, `Contact.jsx`: Các section nội dung.
- **`layout/`**: Các thành phần bố cục chung.
    - `Navbar.jsx`: Thanh điều hướng.
    - `Loader.jsx`: Màn hình chờ tải 3D.
- **`atoms/`**: Các component nhỏ (có thể là nút, input...).
- **`index.ts`**: Export tập trung các component để import gọn hơn ở nơi khác.

#### `src/constants/`
Chứa dữ liệu tĩnh (hardcoded content) giúp code sạch hơn:
- **`index.ts`**: Định nghĩa menu links, danh sách services, technologies, experiences (Starbucks, Tesla...), testimonials, và projects.
- **`config.ts`**: Các cấu hình chung (ví dụ: title trang).
- **`styles.ts`**: Các định nghĩa style dùng chung (có thể là objects style hoặc class names).

#### `src/hoc/` (Higher Order Components)
- **`SectionWrapper.tsx`**: Một wrapper component dùng để bọc các section, xử lý animation xuất hiện hoặc padding chung.

#### `src/assets/`
- Chứa icons, logos, hình ảnh (web, mobile, backend, creator, company logos...).

#### `src/App.tsx`
- Component gốc, thiết lập Routing và cấu trúc trang chính.
- Kết hợp `Navbar`, `Hero` và các section khác.

#### `src/main.tsx`
- Entry point của React, mount App vào DOM.

#### `src/globals.css`
- Import Tailwind directives.

## 3. Luồng Dữ Liệu & Render
1. **Entry:** `index.html` -> gọi `main.tsx`.
2. **Main:** `main.tsx` -> render `App.tsx`.
3. **App:** `App.tsx` sử dụng `BrowserRouter` để quản lý luồng (dù hiện tại có vẻ là Single Page layout với scroll sections).
4. **Data:** Dữ liệu text/ảnh được lấy từ `src/constants/index.ts` và map vào các component trong `src/components/sections/`.

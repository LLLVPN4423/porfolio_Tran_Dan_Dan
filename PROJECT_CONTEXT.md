# Project context — Portfolio Trần Đan Đan

> File này là **nguồn sự thật ngắn gọn** cho agent. Cập nhật mục **“Trạng thái gần nhất”** khi thay đổi kiến trúc lớn; chi tiết từng lần sửa ghi ở `AGENT_CHANGELOG.md`.

## Trạng thái gần nhất

- **Live:** https://lllvpn4423.github.io/porfolio_Tran_Dan_Dan/
- **Repo:** https://github.com/LLLVPN4423/porfolio_Tran_Dan_Dan
- **Stack:** Một trang `index.html` (Tailwind CDN, Font Awesome, CSS/JS inline), ảnh trong `assets/`, album qua `assets/portfolio-galleries.json`.
- **Deploy:** `.github/workflows/deploy-pages.yml` — push `main` → artifact toàn repo → GitHub Pages.

## Cấu trúc thư mục

| Path | Vai trò |
|------|---------|
| `index.html` | Toàn bộ UI: hero, about, portfolio grid, chứng nhận, footer, modal gallery + lightbox, parallax |
| `assets/portfolio-galleries.json` | Map `gallery-id` → danh sách `src`/`alt`; badge “N ảnh” trên card |
| `assets/<tên thư mục>/` | Ảnh theo dự án (tên tiếng Việt, URL encode trong JSON) |
| `assets/ảnh profile/` | `profile-hero.jpg`, `profile-about.jpg` |
| `assets/skills-icons/` | Icon công cụ (Gemini, ChatGPT, Excel, Word, Canva) |
| `_sync_drive_assets.mjs` | **Local only** — đồng bộ folder Google Drive → `assets/` |
| `_build_portfolio_galleries.mjs` | **Local only** — có thể regenerate JSON từ thư mục |

## `index.html` — các section

| `id` | Nội dung |
|------|----------|
| (hero) | Tên, tagline, CTA |
| `#about` | Giới thiệu, học vấn, kỹ năng, công cụ |
| `#portfolio` | Filter: `all`, `event`, `content`, `quay-chup` |
| `#certificates` | Giấy chứng nhận + tài lẻ (grid HTML cố định, không qua JSON) |

Portfolio card: `.portfolio-card-wrap` + `data-category` + `data-gallery-id` + nút `data-open-gallery`.

## Gallery ID ↔ thư mục ↔ card (portfolio)

| `data-gallery-id` | Thư mục `assets/` | Ghi chú |
|-------------------|-------------------|---------|
| `velvet` | Event - Velvet 9 Nhung | |
| `tu-chien-talk` | Event - Talk show Tử chiến Talk | |
| `thuc-tap-fpt` | Thực tập FPT | **6 ảnh cặp** (`fpt-cap-*`) đầu album; `pairStartsAt: 0`, `pairEndsAt: 6`; sau đó `fpt 1–7` |
| `qua-ngot-trao-em` | Event - Quà ngọt trao em | |
| `giai-chay` | Event - Giải chạy | Card không còn placeholder vai trò |
| `whose-chance-talk` | Event - whose chance talk | |
| `ctv-khoa` | Content - CTV Khoa | Card title: **Media Recap HUTECH** |
| `saigon-image` | Content - SaiGon Image Festival | |
| `quay-chup` | Quay chụp | **Một card**, không script; album gộp ảnh quay chụp |

Card **Thực tập FPT** (featured): copy truyền thông nội bộ + block TikTok FPT Software; gallery vẫn `thuc-tap-fpt`.

JSON fetch: `./assets/portfolio-galleries.json?v=...` (query chống cache trình duyệt).

Modal: `buildPortfolioModalGridHtml()` — hỗ trợ `pairStartsAt` / `pairEndsAt` cho hàng `.portfolio-modal-pair` (2 cột full width).

## Theme (tham chiếu nhanh)

- Nền site: `#7DA7D9` (brand / parallax sections)
- Card: `surface-card`, chữ `text-sea`, accent hồng/đỏ nhẹ
- Typography: Playfair (heading), Inter (body)

## Quy trình sửa thường gặp

### Thêm / đổi ảnh một dự án

1. Copy ảnh vào đúng folder `assets/...`
2. Cập nhật `assets/portfolio-galleries.json` (thứ tự `images`, `src` URL-encoded)
3. Nếu cần: đổi thumbnail card trong `index.html` (`<img src=...>` trên card tương ứng)
4. Tăng `?v=` trên `fetch portfolio-galleries.json` nếu user báo cache
5. Ghi `AGENT_CHANGELOG.md`

### Sửa nội dung chữ card

- Chỉ sửa block HTML trong `#portfolio-grid` (tiêu đề `h3`, đoạn mô tả).

### Drive → local

- Chạy `_sync_drive_assets.mjs` (Node) trên máy dev; không đẩy script lên git trừ khi user muốn.

## Git / commit

- User thường yêu cầu **commit + push `main`** để deploy.
- Commit message ngắn, tiếng Anh hoặc Việt, mô tả **why**.

## Ngôn ngữ

- Nội dung portfolio: **tiếng Việt**.
- Agent changelog: tiếng Việt hoặc Anh, nhất quán trong từng entry.

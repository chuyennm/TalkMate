# TalkMate 💬

App học tiếng Anh cá nhân: trò chuyện với AI không sợ sai, học từ vựng bằng SRS, luyện nghe.
PWA thuần — không server, chạy bằng Gemini API key của riêng bạn. Xem kế hoạch chi tiết trong [PLAN.md](PLAN.md).

## Chạy thử trên máy tính

Mở `app/index.html` bằng Chrome/Edge. Vào ⚙️ Cài đặt → dán API key (lấy miễn phí tại [aistudio.google.com](https://aistudio.google.com) → API keys).

## Dùng trên điện thoại (GitHub Pages)

1. Đẩy code lên GitHub (xem bên dưới).
2. Trên GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: `main`, folder `/ (root)` → Save**.
3. Đợi ~1 phút, mở trên điện thoại: `https://chuyennm.github.io/TalkMate/app/`
4. Chọn **"Thêm vào màn hình chính"** (Add to Home Screen) — app sẽ có icon và chạy như app thật.
5. Dán API key trong ⚙️ Cài đặt (làm một lần cho mỗi máy).

## Đẩy code lần đầu

Mở terminal/PowerShell trong folder này:

```
git init
git add .
git commit -m "TalkMate Phase 1: chat buddy + vocab SRS (PWA)"
git branch -M main
git remote add origin https://github.com/chuyennm/TalkMate.git
git push -u origin main
```

Các lần sau chỉ cần: `git add . && git commit -m "..." && git push`

## Ghi chú

- API key chỉ lưu trong trình duyệt của bạn, không nằm trong code — repo để public cho GitHub Pages vẫn an toàn.
- Dữ liệu học lưu trong máy; dùng nút **Xuất/Nhập file** (⚙️ Cài đặt) để chuyển giữa hai điện thoại.

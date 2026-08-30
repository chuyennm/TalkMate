# TalkMate 💬

[English](README.md) · **Tiếng Việt**

App học ngoại ngữ cá nhân, chạy trên điện thoại (PWA): trò chuyện với AI **không sợ sai**, học từ vựng bằng thẻ ôn kiểu Anki, luyện nghe theo đúng trình độ, nói bằng giọng qua micro — và lộ trình tuần do AI soạn từ dữ liệu học thật của bạn.

**Ngôn ngữ hỗ trợ:** 🇬🇧 Anh · 🇨🇳 Trung · 🇯🇵 Nhật · 🇰🇷 Hàn · 🇫🇷 Pháp · 🇪🇸 Tây Ban Nha — chọn trong ⚙️ Cài đặt, mỗi ngôn ngữ có sổ từ và giọng đọc riêng. Tiếng Trung có thêm **luyện viết chữ Hán theo thứ tự nét** (tô bằng ngón tay, chấm từng nét).

Không server, không tài khoản — chạy bằng Gemini API key miễn phí của riêng bạn, dữ liệu nằm trong máy bạn.

## Tính năng chính

- **💬 Trò chuyện**: AI là bạn đồng hành kiên nhẫn, không ngắt lời sửa lỗi giữa chừng — bấm "Kết thúc buổi" mới nhận tổng kết nhẹ nhàng bằng tiếng Việt. Chạm vào từ bất kỳ trong tin nhắn AI để tra nghĩa và lưu vào sổ từ. Bí quá bấm 💡 để xem 3 gợi ý trả lời kèm nghĩa Việt. Nút 🎤 để nói bằng giọng — AI nghe audio trực tiếp, trả lời và đọc to.
- **🎧 Nghe**: AI tạo bài nghe (hội thoại / câu chuyện / bản tin) theo trình độ và chủ đề bạn thích, tự chèn các từ bạn đang học. Lời thoại làm mờ để luyện nghe "chay", chỉnh tốc độ 0.6x–1.2x, quiz 3 câu cuối bài.
- **📚 Từ vựng**: ôn thẻ theo thuật toán SM-2 (Quên / Khó / Nhớ / Dễ), tự phát âm khi lật thẻ, thêm từ thủ công. Tiếng Trung: khung ✍️ luyện viết — xem hoạt hình thứ tự nét rồi tô theo.
- **🧭 Lộ trình**: chuỗi ngày học 🔥, checklist 3 việc mỗi ngày, và nút soạn kế hoạch 7 ngày — AI đọc đúng dữ liệu học của bạn (từ hay quên, các buổi chat), cấm nhận xét chung chung.
- **🌐 Giao diện song ngữ**: chọn Tiếng Việt hoặc English trong Cài đặt — AI cũng giải thích, dịch nghĩa, soạn lộ trình theo ngôn ngữ đó, nên người nước ngoài cũng dùng được.
- **🌱 Chế độ mất gốc** (cho người mới bắt đầu lại): AI dùng câu thật đơn giản kèm dịch tiếng Việt dưới mỗi câu; gõ tiếng Việt cũng được — AI chỉ cách nói rồi trò chuyện tiếp. Cỡ chữ chỉnh tới Rất lớn.

## Chạy thử trên máy tính

Mở `app/index.html` bằng Chrome/Edge. Vào ⚙️ Cài đặt → dán API key (lấy miễn phí tại [aistudio.google.com](https://aistudio.google.com) → API keys) → bấm 🔌 Kiểm tra kết nối. Lưu ý: micro chỉ hoạt động khi chạy qua https (bản GitHub Pages).

## Cài lên điện thoại (GitHub Pages)

1. Push code lên GitHub (xem bên dưới) — repo cần để **Public**.
2. Trên GitHub: **Settings → Pages → Source: Deploy from a branch → Branch `main`, folder `/ (root)` → Save**.
3. Đợi ~1 phút, mở trên điện thoại: `https://chuyennm.github.io/TalkMate/`
4. Chọn **"Thêm vào màn hình chính"** (Add to Home Screen) — app có icon, chạy toàn màn hình như app thật.
5. Dán API key trong ⚙️ Cài đặt (một lần cho mỗi máy). Lần đầu bấm 🎤 nhớ cho phép quyền micro.

## Đẩy code

Lần đầu:

```
git init
git add .
git commit -m "TalkMate"
git branch -M main
git remote add origin https://github.com/chuyennm/TalkMate.git
git push -u origin main
```

Các lần sau: `git add . && git commit -m "..." && git push`. App đã cài trên điện thoại tự nhận bản mới sau khi mở lại 1–2 lần.

## Dữ liệu & chi phí

- API key và toàn bộ dữ liệu học chỉ lưu trong trình duyệt của máy bạn — không nằm trong code, repo để public vẫn an toàn.
- Dùng 2 điện thoại: nút **Xuất/Nhập file** trong ⚙️ Cài đặt để chuyển sổ từ + tiến độ (file JSON).
- Gemini free tier đủ cho 30–60 phút học/ngày. TTS giọng đọc của điện thoại: miễn phí. Hosting GitHub Pages: miễn phí.

## Cấu trúc

```
TalkMate/
├── index.html            ← redirect vào app/
├── PLAN.md               ← kiến trúc + lịch sử phát triển + hướng mở rộng
└── app/
    ├── index.html        ← toàn bộ app (HTML + CSS + JS, 1 file)
    ├── manifest.webmanifest
    ├── sw.js             ← service worker (cache offline)
    └── icon-192.png / icon-512.png
```

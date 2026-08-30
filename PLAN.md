# TalkMate — Kiến trúc & kế hoạch

App học ngoại ngữ cá nhân dạng template đa ngôn ngữ. Ba trụ cột: **từ vựng** (SRS), **nghe** (bài nghe AI tạo theo trình độ), **nói không sợ sai** (chat text + giọng nói). Cách dùng hằng ngày xem [README.md](README.md).

## Nguyên tắc thiết kế

- **Rẻ nhất có thể**: Gemini API (free tier), TTS của trình duyệt (miễn phí), hosting GitHub Pages (miễn phí), không server.
- **Client-only**: API key nhập một lần, lưu trong máy. Dữ liệu học trong `localStorage`. Xuất/nhập JSON để chuyển giữa các máy.
- **Không sợ sai**: AI không ngắt lời sửa lỗi giữa chừng — chỉ tổng kết nhẹ nhàng cuối buổi. Có chế độ mất gốc 🌱 cho người bắt đầu lại từ đầu.
- **PWA**: một codebase chạy cả Android và iPhone, cài lên màn hình chính như app thật.

## Kiến trúc

```
app/index.html   ← toàn bộ app trong 1 file (HTML + CSS + JS)
```

- Gọi thẳng `generativelanguage.googleapis.com` (Gemini) từ trình duyệt. Model mặc định `gemini-2.5-flash`, đổi được trong Cài đặt.
- **Cấu hình đa ngôn ngữ**: object `LANGS` (en/zh/ja/ko/fr/es) giữ tên hiển thị, mã giọng TTS, kiểu phiên âm (IPA / pinyin / romaji / romanization) và luật riêng cho prompt (ví dụ zh: luôn kèm pinyin). Mọi prompt (chat, tra từ, bài nghe, gợi ý, coach) đọc từ `L()`. Thêm một ngôn ngữ mới = thêm một dòng vào `LANGS`.
- **Sổ từ**: mỗi từ gắn `lang`, các màn hình chỉ hiện từ của ngôn ngữ đang học (`W()`). Lịch ôn SM-2 rút gọn.
- **Giọng nói**: MediaRecorder ghi âm → gửi audio trực tiếp cho Gemini (không cần dịch vụ speech-to-text riêng) → transcript + trả lời → Web Speech API đọc to.
- **Luyện chữ Hán**: thư viện [hanzi-writer](https://chanind.github.io/hanzi-writer) tải lười từ CDN khi chọn tiếng Trung — hoạt hình thứ tự nét + quiz tô nét có chấm điểm.
- **Theo dõi học**: bộ đếm hoạt động theo ngày + chuỗi ngày học; coach tuần đọc dữ liệu thật (từ yếu, tổng kết các buổi) để soạn kế hoạch 7 ngày.
- Service worker cache app shell — mở được cả khi mạng yếu (gọi AI vẫn cần mạng).

## Lịch sử phát triển (đã xong ✅)

| Phase | Nội dung |
|---|---|
| 1 | Chat buddy + tổng kết cuối buổi, chạm từ để lưu, ôn từ SRS, xuất/nhập dữ liệu, PWA |
| 2 | Luyện nghe: AI sinh bài theo trình độ + từ đang học, TTS chỉnh tốc độ, ẩn/hiện lời thoại, quiz |
| 3 | Nói bằng giọng: 🎤 ghi âm → Gemini nghe audio → trả lời + tự đọc to; 🔊 nghe lại từng tin nhắn |
| 4 | Tab 🧭 Lộ trình (streak, checklist, coach tuần); chế độ mất gốc 🌱; nút 💡 gợi ý khi bí; cỡ chữ lớn |
| 1.0 | Màn chào lần đầu, kiểm tra API key, thêm từ thủ công, phát âm khi ôn, báo lỗi tiếng Việt, vá lỗi |
| 2.0 | Template đa ngôn ngữ (Anh/Trung/Nhật/Hàn/Pháp/TBN); tiếng Trung: pinyin + chạm chữ Hán + luyện viết theo nét |

## Hướng mở rộng (chưa làm)

- **Chấm Writing theo band IELTS/HSK** khi gần thi — chỉ là một prompt + màn hình mới, không đổi kiến trúc.
- **Shadowing có nhận xét**: TTS đọc câu → người học nói lại → AI so sánh và nhận xét nhịp/từ chưa rõ.
- **Nâng cấp giọng đọc**: gọi Gemini TTS thay giọng trình duyệt cho tự nhiên hơn (vẫn trong free tier mức dùng cá nhân).
- **Chấm phát âm chi tiết từng âm**: ghép Azure Pronunciation Assessment (có free tier) — chỉ khi thật sự cần.
- **Nhắc ôn từ hằng ngày**: cần push notification → cần server nhỏ hoặc chuyển Expo; cân nhắc khi nhu cầu rõ.
- **Đồng bộ tự động giữa 2 máy**: hiện dùng xuất/nhập JSON thủ công; nếu muốn tự động cần server nhỏ (Cloudflare Workers + KV).

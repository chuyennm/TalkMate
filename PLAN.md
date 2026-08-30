# TalkMate — Kế hoạch dự án

App học tiếng Anh cá nhân: học từ vựng, luyện nghe, trò chuyện với AI để nói tự nhiên — không sợ sai. Mục tiêu dài hạn: đạt trình độ tương đương IELTS mà không cần các tính năng "chấm chuẩn" của app thương mại.

## Nguyên tắc thiết kế

- **Rẻ nhất có thể**: Gemini API (free tier qua Google AI Studio), TTS miễn phí, không server.
- **Chạy trên điện thoại** (cả Android và iPhone): PWA — một codebase web, cài lên màn hình chính như app thật.
- **Client-only**: API key nhập một lần, lưu trong máy. Dữ liệu học (từ vựng, tiến độ) lưu trong trình duyệt. Có nút xuất/nhập JSON để chuyển giữa hai điện thoại.
- **Không sợ sai**: AI đóng vai bạn trò chuyện kiên nhẫn, KHÔNG ngắt lời sửa lỗi giữa chừng — chỉ tổng kết nhẹ nhàng cuối buổi.

## Kiến trúc

```
TalkMate/
├── PLAN.md              ← file này
└── app/
    ├── index.html       ← toàn bộ app (HTML + CSS + JS trong 1 file)
    ├── manifest.webmanifest
    ├── sw.js            ← service worker (cache offline, cài PWA)
    ├── icon-192.png
    └── icon-512.png
```

- Gọi thẳng `generativelanguage.googleapis.com` (Gemini) từ trình duyệt bằng key của bạn.
- Model mặc định: `gemini-2.5-flash` (đổi được trong Cài đặt).
- Dữ liệu: `localStorage` (từ vựng + lịch ôn SM-2 + lịch sử buổi học).
- TTS Phase 2: giọng có sẵn của trình duyệt (Web Speech API) trước, nâng cấp sau nếu cần.

## Các phase

### Phase 1 — Trò chuyện + Từ vựng ✅ (prototype trong `app/`)

- **Trò chuyện**: chat text với AI buddy. Nhấn "Kết thúc buổi" → AI tổng kết tối đa 3 lỗi đáng chú ý + cách nói tự nhiên hơn + gợi ý từ mới từ chính cuộc trò chuyện.
- **Lưu từ ngay trong chat**: chạm vào từ bất kỳ trong tin nhắn của AI → AI tự tra nghĩa tiếng Việt + phiên âm + ví dụ → lưu vào sổ từ.
- **Ôn từ (SRS)**: thuật toán SM-2 kiểu Anki. Mỗi thẻ: từ → nghĩa + phiên âm + ví dụ. Bấm Quên / Khó / Nhớ / Dễ để xếp lịch ôn lại.
- **Xuất/nhập dữ liệu**: file JSON, để đồng bộ tay giữa Android ↔ iPhone.
- **Cài đặt**: API key, model, trình độ hiện tại, chủ đề yêu thích.

### Phase 2 — Luyện nghe ✅ (đã có trong `app/`, tab 🎧 Nghe)

- AI sinh đoạn hội thoại / bản tin ngắn theo trình độ + chủ đề bạn thích, **ưu tiên chèn các từ đang học trong sổ từ**.
- Đọc bằng TTS (Web Speech API — miễn phí, có sẵn trên điện thoại; chọn giọng Anh-Mỹ/Anh-Anh, chỉnh tốc độ 0.7x–1.2x).
- Nghe xong: che transcript → nghe lại → hiện transcript đối chiếu → quiz nhanh 3 câu hiểu nội dung.
- Nâng cấp tuỳ chọn: gọi Gemini TTS để có giọng tự nhiên hơn (vẫn trong free tier với mức dùng cá nhân).

### Phase 3 — Nói bằng giọng ✅ (nút 🎤 trong tab Trò chuyện)

- Ghi âm từ micro → gửi audio cho Gemini (Gemini nhận audio trực tiếp, không cần dịch vụ speech-to-text riêng) → AI trả lời → TTS đọc lên. Thành vòng hội thoại bằng giọng nói.
- Chế độ shadowing: TTS đọc câu → bạn nói lại → AI nghe và nhận xét chung (nhịp, từ nào nghe chưa rõ) — nhận xét kiểu bạn bè, không chấm điểm.
- Nếu sau này muốn chấm phát âm chi tiết từng âm: ghép thêm Azure Pronunciation Assessment (có free tier), nhưng không bắt buộc.

### Phase 4 (tuỳ chọn) — Giáo viên riêng

- Log mọi buổi học đã có sẵn từ Phase 1. Thêm nút "Tuần này học gì?": AI đọc log → nhận xét tiến bộ, đề xuất chủ đề + từ vựng tuần tới.
- Khi gần thi IELTS: thêm prompt chấm Writing Task 1/2 theo band descriptor (chỉ là một màn hình mới, không đổi kiến trúc).

## Cách chạy app (Phase 1)

1. **Trên máy tính (thử nhanh)**: mở `app/index.html` bằng Chrome/Edge là chạy.
2. **Trên điện thoại (dùng thật)**: đưa folder `app/` lên hosting tĩnh miễn phí — GitHub Pages hoặc Cloudflare Pages (kéo thả là xong). Mở link trên điện thoại → "Thêm vào màn hình chính". Chỉ cần làm một lần; về sau sửa file là cập nhật.
3. Lấy API key miễn phí tại **aistudio.google.com** → API keys → Create API key. Dán vào màn hình Cài đặt của app.

## Chi phí dự kiến

- Gemini free tier: đủ cho 30–60 phút học/ngày với Flash. Nếu vượt: Flash trả phí cũng chỉ cỡ vài nghìn–vài chục nghìn đồng/tháng cho mức dùng cá nhân.
- Hosting: 0đ (GitHub/Cloudflare Pages). TTS trình duyệt: 0đ.

# LightLAB Web 3

Bản chạy trên trình duyệt của LightLAB LITE V2.2 (cùng công thức chỉnh ảnh, icon và 16 preset).
Ảnh được xử lý ngay trên máy bạn, không tải lên server nào.

## Đưa lên GitHub Pages
1. Tạo repo mới trên GitHub, upload **toàn bộ nội dung** thư mục này (gồm `index.html`, `manifest.webmanifest`, `assets/`, `presets/`, `.nojekyll`).
2. Vào **Settings → Pages**, mục *Build and deployment*: Source = *Deploy from a branch*, Branch = `main`, thư mục `/ (root)` → Save.
3. Sau khoảng 1 phút, mở `https://<tên-github>.github.io/<tên-repo>/`.

## Cách dùng
- Dải icon ở dưới vuốt ngang; chạm icon nào thì thanh kéo của mục đó hiện ra phía trên.
- Chạm biểu tượng đầu tiên (hoặc chạm vào ảnh) để mở ảnh. Giữ ngón tay trên ảnh để xem ảnh gốc.
- Nhấn đúp vào tên thanh kéo để đưa về mặc định. Dấu chấm dưới icon = mục đã chỉnh.
- Lưu ảnh: `<tên gốc>_LL.jpg`, cạnh dài tối đa 4096 px.

## Ngôn ngữ
Chọn ở góc trên bên phải: Tiếng Việt, English, Français, 日本語, 한국어, 中文, ไทย, Deutsch, Русский (dùng bảng dịch của app). Mặc định theo ngôn ngữ trình duyệt.

## Preset: Film preset | Lut preset | Yêu thích
- Mỗi preset hiển thị bằng **ảnh thu nhỏ của ảnh đang mở** (chưa mở ảnh thì dùng ảnh nền) đã áp preset đó, tên preset nằm bên dưới. Các mục xếp trên **một hàng ngang vuốt từ trái sang phải**, ở cả 3 tab. Ảnh thu nhỏ tính theo các chỉnh sửa hiện tại (cường độ 100%) và chỉ nạp khi cuộn tới, nên LUT nặng không làm chậm lúc mở.
- **Film preset**: 16 preset màu có sẵn của LightLAB.
- **Lut preset**: đọc các file `.cube` (3D LUT, kích thước 2–129) hoặc `.llt` trong thư mục **`LUT`** của repo. Chỉ cần tải file vào thư mục `LUT` (cùng cấp với `index.html`) rồi commit; trang tự đọc danh sách qua GitHub API khi chạy trên `github.io` (chỉ đọc file ở cấp ngoài cùng của thư mục, tên thư mục viết hoa `LUT`). Nếu không dùng `github.io`, tạo `LUT/index.json` dạng `["A.cube","B.cube"]`. Hai LUT mẫu `Teal_Orange.cube` và `Mono_Warm.cube` có thể xóa.
- **Yêu thích**: ấn giữ một preset (hoặc chuột phải) thì hiện ngôi sao vàng ★ bên cạnh; chạm ★ để thêm/bỏ khỏi Yêu thích. Preset đã thích có ★ nhỏ trước tên. Danh sách được nhớ trong trình duyệt.

## Chat với Llama (chạy trên máy bạn hoặc qua API)
Bấm **✦ Meta AI** ở góc trên → bấm ⚙ → chọn **Nhà cung cấp**. Mặc định là **Ollama** chạy ngay trên máy bạn: không cần khóa API, không tốn phí.

### Ollama (khuyên dùng)
1. Cài Ollama (https://ollama.com/download) rồi tải mô hình, ví dụ `ollama pull llama3.2` (muốn gửi kèm ảnh thì dùng mô hình đọc được ảnh, ví dụ `ollama pull llama3.2-vision`).
2. Cho phép trang web này gọi Ollama: đặt biến môi trường `OLLAMA_ORIGINS` bằng địa chỉ trang, ví dụ `https://TEN.github.io` (khi thử có thể dùng `*`), rồi khởi động lại Ollama.
   - Windows: đặt biến trong Environment Variables, thoát Ollama và mở lại.
   - macOS: `launchctl setenv OLLAMA_ORIGINS "https://TEN.github.io"` rồi mở lại Ollama.
   - Linux: `sudo systemctl edit ollama`, thêm `Environment="OLLAMA_ORIGINS=https://TEN.github.io"`, rồi `sudo systemctl restart ollama`.
3. Mở trang web **trên chính máy chạy Ollama**, mở ⚙, bấm ↻: trang liệt kê mô hình đã cài và tự chọn mô hình Llama. Trang gọi `http://localhost:11434/v1/chat/completions` (giao diện tương thích OpenAI của Ollama, có sẵn lịch sử trò chuyện).
- Chrome có thể hỏi quyền truy cập thiết bị trong mạng cục bộ: chọn Cho phép.
- Nếu mô hình không đọc được ảnh, trang tự gửi lại chỉ phần chữ.

### LM Studio
Tải mô hình trong LM Studio → tab Developer → **Start Server** (cổng 1234) → bật **Enable CORS**. Chọn "LM Studio" trong ⚙ rồi bấm ↻.

### Dùng trên điện thoại
Trên điện thoại, `localhost` là chính chiếc điện thoại, không phải máy tính. Trang GitHub là HTTPS nên trình duyệt chặn gọi tới `http://192.168.x.x`. Muốn dùng mô hình chạy trên máy tính từ điện thoại, cần mở Ollama ra bằng địa chỉ HTTPS (ví dụ Tailscale Serve hoặc Cloudflare Tunnel), chọn "Khác" trong ⚙ và nhập địa chỉ đó + `/v1`.

### Qua API (cần khóa)
- **Meta Llama API** (`api.llama.com`, khóa tại https://llama.developer.meta.com), **Groq** (khóa `gsk_…`, https://console.groq.com/keys), **OpenRouter** (khóa `sk-or-…`, https://openrouter.ai/keys). Dán khóa `gsk_…` / `sk-or-…` thì trang tự chọn nhà cung cấp tương ứng; khóa Google (`AIza…`) hay OpenAI (`sk-…`) bị cảnh báo vì không dùng được với Llama.
- Lỗi 401/403: khóa bị từ chối. Lỗi "Không kết nối được API": thường do nhà cung cấp chặn gọi từ trình duyệt (CORS).
- Khóa chỉ lưu trong trình duyệt của bạn (localStorage). **Đừng ghi khóa vào mã hay đẩy lên GitHub.**

Bấm ra ngoài khung chat (hoặc phím Esc) để thu gọn.

## Mở file RAW
Bấm "Mở hình ảnh" và chọn file ARW/NEF/DNG…: trang lấy ảnh JPEG xem trước nhúng trong file (không phải dữ liệu RAW gốc).

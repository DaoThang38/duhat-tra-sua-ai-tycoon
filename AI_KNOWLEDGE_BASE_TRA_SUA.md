# THẨM ĐỊNH KỸ THUẬT & KNOWLEDGE BASE: NĂNG LỰC AI TRONG TIỆM TRÀ SỮA
## ĐẶC TẢ CHI TIẾT: CẦN AI Ở CHỖ NÀO, MA TRẬN OUTPUT, GROUP CHAT & BỘ NHỚ CONTEXT

---

## 1. PHÂN ĐỊNH RANH GIỚI: CẦN AI Ở CHỖ NÀO? (AI VS DETERMINISTIC LOGIC)

Một trong những sai lầm chết người của các dự án AI Game là để LLM tự làm kế toán (tự cộng trừ tiền, tự nhớ số dư). LLM sẽ gặp hiện tượng ảo giác (hallucination), làm sai lệch dòng tiền khiến người chơi ức chế.  
Do đó, kiến trúc bắt buộc phải tuân thủ nguyên tắc: **"Deterministic Ledger for Numbers, Generative AI for Drama & Persona"**.

```
┌────────────────────────────────────────────────────────────────────────┐
│             KIẾN TRÚC HỆ THỐNG: PHÂN TÁCH RANH GIỚI NHIỆM VỤ           │
├───────────────────────────────────┬────────────────────────────────────┤
│ 1. DETERMINISTIC CORE (CODE THUẦN)│ 2. GENERATIVE AI ENGINE (LLM)      │
├───────────────────────────────────┼────────────────────────────────────┤
│ • Sổ cái tài chính (Cộng/Trừ tiền)│ • Nhập vai NPC (Bé Trà Sữa, Công   │
│ • Điểm đánh giá Sao (1.0 - 5.0★)  │   an, Khách bóc phốt, Shipper).    │
│ • Đồng hồ Heartbeat (Cron timer)  │ • Tạo sinh bối cảnh drama hài hước │
│ • Kiểm tra điều kiện Phá sản /    │ • Phân tích ý định khi User tự do  │
│   Mở rộng chi nhánh               │   gõ chat (Free-text intent parse) │
│ • Kiểm phiếu Biểu quyết Group Chat│ • Viết lời bình trào phúng, tự sinh│
│ • Lưu trữ State Ledger dạng JSON  │   tiêu đề cho Artifacts chia sẻ    │
└───────────────────────────────────┴────────────────────────────────────┘
```

### Bảng Phân Tích 5 Điểm Chạm AI (Touchpoints):

| Điểm Chạm | Nhiệm Vụ Của AI | Input Đầu Vào | Output Sinh Ra | Vì Sao Cần AI (Thay vì IF/ELSE)? |
| :--- | :--- | :--- | :--- | :--- |
| **Touchpoint 1: Dynamic Crisis Generator** | Tạo ra biến cố dở khóc dở cười theo thời gian thực (Heartbeat). | Giờ trong ngày, Tồn kho, Số vốn hiện tại, Lịch sử biến cố gần nhất. | Tiêu đề biến cố, Lời thoại cầu cứu của Bé Quản Lý, 2 lựa chọn gợi ý. | Tạo sự bất ngờ vô tận, không bị lặp lại nhàm chán như kịch bản cố định. |
| **Touchpoint 2: Free-Text Decision Parser** | Diễn giải quyết định bất quy tắc khi người chơi không bấm nút có sẵn mà tự gõ tay. | Câu chat của User (vd: *"Cho anh công an 2 ly trà sữa trân châu full topping bảo đây là tấm lòng"*). | Phân loại thái độ (Xoa dịu / Đút lót / Cứng rắn), Lượng hóa thành delta số liệu: `d_cash`, `d_stars`, `d_morale`. | Cốt lõi của trải nghiệm Chat-First: User được tự do sáng tạo cách ứng biến. |
| **Touchpoint 3: Multi-NPC Roleplay** | Đóng vai các bên liên quan xuất hiện trong quán. | Bối cảnh Gate, Vai trò (Quản lý thị trường, Khách khó tính, Shipper). | Đoạn đối thoại sắc sảo, hài hước, phản ánh đúng "văn hóa vỉa hè/công sở" Việt Nam. | Mang lại cảm xúc chân thật, khiến người chơi cười nghiêng ngả. |
| **Touchpoint 4: Group Chat Mediator** | Điều phối thảo luận nhóm, chọc ngoáy, kích động tranh cãi giữa các cổ đông bạn bè. | Danh sách vote của các thành viên, Tin nhắn tranh cãi trong group. | Lời bình châm biếm, Tuyên bố kết quả biểu quyết, Phong danh hiệu (vd: *"Chúa tể keo kiệt"*). | Tăng tính gắn kết xã hội và tính cạnh tranh nội bộ nhóm bạn. |
| **Touchpoint 5: Viral Artifact Scribe** | Chắp bút các văn bản hài hước dựa trên toàn bộ lịch sử chơi. | Lịch sử các quyết định dại dột / khôn ngoan của chủ quán, Số tiền lỗ/lãi. | Nội dung "Bằng Khen Phá Sản", "Biên Bản Xử Phạt", "Nghị Quyết Bổ Nhiệm Chủ Tịch F&B". | Cá nhân hóa 100% chiến tích của người chơi, kích thích nhu cầu chia sẻ lên Story. |

---

## 2. MA TRẬN OUTPUT MONG MUỐN (DESIRED OUTPUT MATRIX)

Mọi phản hồi từ hệ thống (kể cả tự động hay do AI sinh ra) đều phải chuẩn hóa về một cấu trúc dữ liệu duy nhất (`GameTurnResult`):

```json
{
  "system_state": {
    "cash_vnd": 45000000,
    "rating_stars": 4.3,
    "staff_morale_pct": 82,
    "inventory_pct": 75,
    "turn_count": 14,
    "status": "OPERATING" // OPERATING | BANKRUPT_SOS | EMPIRE_EXPANSION
  },
  "ai_narrative": {
    "speaker": "Bé Cửa Hàng Trưởng 🧋",
    "tone": "PANIC_HUMOR",
    "message": "Sếp ơiii! Đội kiểm tra liên ngành vừa rút đi rồi, nhờ sếp tặng 2 ly trà đào cam sả mà các chú vui vẻ chỉ nhắc nhở nhẹ thôi! Quỹ quán -120k tiền nguyên liệu nhưng sao tăng vọt lên 4.5★ nhé sếp!",
    "newsflash": "BÁO LÁ CẢI: Tiệm trà sữa thoát án phạt nhờ tài ngoại giao bằng... trân châu hoàng kim!"
  },
  "gate_active": false,
  "viral_trigger": null
}
```

### Bảng Quy Đổi Trạng Thái & Hạn Mức Tác Động:

### 2.1. Ma Trận Chỉ Số Tối Giản (Streamlined Metrics - Tránh Nặng Nề Về Game)
Nhằm tránh biến tính năng thành một con game quản lý phức tạp (sim/strategy), hệ thống **loại bỏ các chỉ số vi mô không cần thiết** (như Tồn kho nguyên liệu %, Tinh thần nhân viên %) và **chỉ giữ lại 2 chỉ số cốt lõi phục vụ tính năng vui vẻ và đòn bẩy +1 bạn**:

| Chỉ Số (Metric) | Khởi Điểm | Ngưỡng Nguy Cấp | Ngưỡng Thịnh Vượng | Hậu Quả & Đòn Bẩy +1 Bạn |
| :--- | :--- | :--- | :--- | :--- |
| **💰 Tiền Két (Cash Flow)** | `50.000.000đ` | `< 0đ` (Vỡ nợ âm tiền) | `> 100.000.000đ` (Đại gia F&B) | **Nguy cấp:** Kéo xích niêm phong tiệm -> Rủ bạn bè vào góp vốn 20 củ cứu nét (+1 Bạn)!<br>**Thịnh vượng:** Bổ nhiệm bạn bè làm CEO Quán Phở Bò / Tiệm Nail (+1 Bạn)! |
| **⭐ Độ Uy Tín (Stars)** | `4.2 ★` | `< 2.5 ★` (Tẩy chay) | `= 5.0 ★` (Quán Hot Trend) | Thước đo danh dự và meme. Đạt 5.0★ khách chen lấn quá tải; Dưới 2.5★ dính phốt tẩy chay. |

### 2.2. Cơ Chế Xử Lý Khi Có Biến: Đôi Co Đa Kênh [A], [B], [C / Other]
Khi có biến cố ập đến (Công an PCCC, Hot Tiktoker bóc phốt, Shipper bom hàng), đối tượng liên quan (NPC) sẽ **nhảy thẳng vào khung chat buông lời khiêu khích / dọa nạt**. Chủ quán có 3 cách xử lý:
1. **Lựa chọn [A] 😇 (Ngoại giao mềm mỏng):** Xin lỗi, mời trà đào cam sả, giải thích hòa nhã (-Ít tiền, +Uy tín).
2. **Lựa chọn [B] 😈 (Cứng rắn cãi lý):** Bật camera đôi co, ăn miếng trả miếng (Bị phạt kịch khung, mất nhiều tiền nhưng mang lại tiếng cười sảng khoái).
3. **Lựa chọn [C / Other] 💬 (Tự do gõ chat đôi co):** Người chơi tự gõ câu chửi xéo hoặc câu nịnh vào khung chat. AI trích xuất ý định (Intent Parser) và để NPC phản hồi động theo đúng văn phong đường phố/công sở Việt Nam!

---

## 3. SO SÁNH TRẢI NGHIỆM: CHAT 1:1 VS GROUP CHAT

| Tiêu Chí So Sánh | Chế Độ Chat 1:1 (Solo Tycoon) | Chế Độ Group Chat (Hội Đồng Cổ Đông Góp Vốn) |
| :--- | :--- | :--- |
| **Bản chất vai vế** | **Chủ Tịch Độc Tài:** Một mình người chơi quyết định tất cả, chịu trách nhiệm tuyệt đối. | **Dân Chủ Hài Hước:** Bạn bè cùng góp vốn (mỗi người 10-20%), nắm cổ phần ngang nhau. |
| **Tương tác với AI** | Trực tiếp 1:1 với Bé Cửa Hàng Trưởng AI. Tông giọng thân mật, nịnh sếp hoặc càm ràm sếp. | AI đóng vai trò **Thư Ký Hội Đồng / Game Master**. Báo cáo trước toàn thể nhóm, chọc ngoáy sự bất đồng ý kiến giữa các bạn. |
| **Cơ chế xử lý Gate** | Người chơi bấm chọn nút hoặc gõ lệnh -> Có kết quả ngay lập tức. | Mở cuộc bỏ phiếu (Poll). Mỗi thành viên có 1 phiếu. Nếu hòa phiếu (Tie), AI kích hoạt minigame oẳn tù tì hoặc phạt cả nhóm vì chậm trễ. |
| **Yếu tố hài hước** | Hài hước đến từ sự ngây ngô hoặc liều lĩnh của cá nhân người chơi trước AI. | Hài hước đến từ việc **bạn bè cãi nhau, đổ thừa trách nhiệm**: *"Tao đã bảo đừng đút lót rồi mà mày cứ đút lót để công an phạt gấp đôi!"* |
| **Tốc độ ván chơi** | Rất nhanh (5-10 phút để vượt qua 10 biến cố). | Kéo dài tự nhiên theo ngày, phù hợp cho nhóm bạn buôn chuyện trong giờ làm việc. |

---

## 4. CHI TIẾT 3 KHOẢNH KHẮC BÙNG PHÁT (+1 BẠN TIPPING POINTS)

```
                     ┌──────────────────────────────────────┐
                     │   3 KHOẢNH KHẮC +1 BẠN CỐT LÕI       │
                     └──────────────────┬───────────────────┘
                                        │
         ┌──────────────────────────────┼──────────────────────────────┐
         ▼                              ▼                              ▼
  [1. CỨU NÉT PHÁ SẢN]          [2. MỞ RỘNG ĐẾ CHẾ]            [3. BẾ TẮC BIỂU QUYẾT]
Khi vốn < 0 hoặc sau 200 msg.   Khi vốn > 100M, 5 sao.        Gặp phốt lớn triệu view.
Khóa tiệm, cần bạn vào góp      Mở chi nhánh Quán Phở, Tiệm   Cần ít nhất 2 bạn vào
vốn 20 triệu để hồi sinh.       Nail, bổ nhiệm bạn làm CEO.   vote cứu vãn danh dự quán.
```

### Kịch bản 1: Cứu Nét Phá Sản (Bailout Hook)
- **Điều kiện kích hoạt:** Sau một chuỗi quyết định dại dột (hoặc xui xẻo), tiền két âm (`< 0đ`).
- **Thông điệp AI:** *"Alo alo sếp ơi... Thợ đòi nợ mặt bằng đang đứng trước cửa khóa xích rồi! Quán mình nợ 15 triệu! Em cho sếp 2 lựa chọn: (A) Nhận 'Bằng Khen Phá Sản' vinh quang và share lên Story; (B) Gửi link SOS rủ 1 đứa bạn thân vào góp vốn 20 củ để gỡ nợ hồi sinh tiệm!"*
- **Tác động viral:** Người chơi share link kèm caption: *"Mở quán trà sữa được 3 ngày thì âm tiền, ai vào cứu tao với!"* -> Người bạn click vào trở thành Cổ Đông Đồng Sáng Lập.

### Kịch bản 2: Mở Rộng Đế Chế F&B Đa Ngành (Scale-Up Hook)
- **Điều kiện kích hoạt:** Quán đạt doanh thu khủng, tiền mặt tích lũy `> 100.000.000đ`, sao đạt `4.8★`.
- **Thông điệp AI:** *"Chúc mừng Chủ Tịch! Tiệm trà sữa của chúng ta đang lãi như in tiền! Thương hiệu đã quá lớn, em đề xuất Tập Đoàn mở rộng sang: (1) Quán Phở Bò Tái Lăn 24h; (2) Tiệm Nail & Nối Mi Chảnh Sả! Nhưng sếp bận đếm tiền rồi, cần tuyển 1 đứa bạn làm CEO điều hành chi nhánh mới. Tag bạn bè vào nhận chức ngay!"*
- **Tác động viral:** Thẻ phong danh hiệu cực oách: *"Nghị Quyết Bổ Nhiệm Tổng Giám Đốc Chuỗi Phở Bò"* gửi thẳng vào inbox bạn bè.

### Kịch bản 3: Hội Đồng Khủng Hoảng Truyền Thông (Crisis Deadlock)
- **Điều kiện kích hoạt:** Xuất hiện biến cố cấp độ thảm họa (Khách quay video thấy "thạch thằn lằn" lên xu hướng TikTok 2 triệu view).
- **Thông điệp AI:** *"Biến căng đét sếp ơi! Cả mạng xã hội đang tràn vào đánh giá 1 sao tiệm mình! Tình huống này vượt quá thẩm quyền của 1 người, cần triệu tập Hội Đồng Cổ Đông khẩn cấp. Mời ít nhất 2 người bạn vào nhóm để biểu quyết: Đóng cửa trốn net hay Mở họp báo tặng trà sữa trọn đời cho nạn nhân?"*

---

## 5. BỘ NHỚ CONTEXT & KỊCH BẢN XỬ LÝ KHI AI BỊ QUÊN (MEMORY & SELF-HEALING)

### 5.1. Cấu trúc bộ nhớ (3-Tier Context Architecture)

1. **Tier 1: Sổ Cái Bất Biến (State Ledger - Structured DB):**
   - Lưu trữ số dư, tên quán, các sự kiện quan trọng (vd: *Đã từng hối lộ công an thất bại ở Turn 3*, *Đang thiếu nợ tiền đá*).
   - Dạng JSON cực nhẹ, luôn được tự động chèn vào đầu mọi Prompt (`System Context`).
2. **Tier 2: Cửa Sổ Trượt Hội Thoại (Sliding Window Dialogue):**
   - Chỉ giữ lại **6 - 8 tin nhắn gần nhất** trong phiên chat để đảm bảo tốc độ phản hồi siêu tốc (<1.5s) và tiết kiệm token.
3. **Tier 3: Bản Tóm Tắt Tích Lũy (Rolling Milestone Summary):**
   - Cứ sau mỗi 5 lượt chơi, AI tự sinh 1 câu tóm tắt ngắn: *"Quán 'Trà Sữa Bất Tử' hiện có 62 triệu, nổi tiếng vì pha trà ngon nhưng nhân viên hay cãi sếp."*

### 5.2. Kịch bản khi AI Quên Hoặc Ảo Giác (Self-Healing Fallback Strategy)

Trong trường hợp LLM bị "ảo giác" (nhầm tên quán, nói sai số tiền, hoặc quên mất việc vừa bị phạt):

```
┌────────────────────────────────────────────────────────────────────────┐
│             CƠ CHẾ TỰ CHỮA LÀNH KHI AI BỊ "LAG NÃO"                    │
├────────────────────────────────────────────────────────────────────────┤
│ 1. VALIDATION LAYER (Bộ lọc kiểm tra trước khi render):               │
│    Nếu phản hồi của AI chứa số liệu tài chính lệch quá 5% so với        │
│    Sổ Cái trong Database -> Kích hoạt cơ chế Đè Thoại (Override).      │
├────────────────────────────────────────────────────────────────────────┤
│ 2. IN-CHARACTER RECOVERY SCRIPT (Nhập vai chữa ngượng tự nhiên):       │
│    Thay vì báo lỗi hệ thống cứng nhắc, Cửa Hàng Trưởng AI sẽ tự "chữa   │
│    cháy" cực kỳ hài hước:                                              │
│                                                                        │
│    "Á á sếp ơiii... Em lú quá! Mới nếm thử ly trà sữa 100% đường nên   │
│     não em bị lag xíu! Em xem lại sổ sách rồi, tiền két của quán mình  │
│     chuẩn đét vẫn là 42.500.000đ nha sếp, không mất đi đồng nào đâu ạ!  │
│     Sếp đừng trừ lương em tội nghiệp! 😭🧋"                            │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 6. DANH MỤC TẠO TÁC VIRAL (VIRAL ARTIFACTS SHOWCASE)

Mỗi ván chơi kết thúc (thắng hoặc bại) đều sản xuất ra 1 ấn phẩm đồ họa độc bản chuẩn kích thước Story 9:16:

1. **Bằng Khen Phá Sản Danh Dự:**
   - *Tiêu đề:* "HIỆP HỘI F&B TRAO TẶNG: BẰNG KHEN CHỦ QUÁN DŨNG CẢM"
   - *Thành tích:* "Đã kiên cường trụ vững được 4 ngày 6 tiếng trước khi phá sản vì tặng trà sữa miễn phí cho người yêu cũ."
   - *Con dấu:* Đóng dấu đỏ chót "NGHÈO BỀN VỮNG".
2. **Biên Bản Phạt Quản Lý Thị Trường Dở Khóc Dở Cười:**
   - *Lỗi vi phạm:* "Trà sữa quá ngọt làm sâu răng cán bộ thanh tra; Nhân viên bấm điện thoại nhanh hơn bấm máy tính tiền."
   - *Mức phạt:* Tịch thu 10 ly trân جو đường đen và phạt 500k sung công quỹ.
3. **Nghị Quyết Bổ Nhiệm Chủ Tịch Đế Chế F&B:**
   - *Tiêu đề:* "TẬP ĐOÀN ĐA NGÀNH: QUYẾT ĐỊNH BỔ NHIỆM CEO QUÁN PHỞ KIÊM TIỆM NAIL"
   - *Khen thưởng:* Dành cho chủ quán có lãi trên 100 triệu, mở rộng chuỗi thành công.

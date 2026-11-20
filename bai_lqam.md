# [Bài thực hành 3] Tóm tắt tài liệu quy định nhân sự vượt quá Context Window
## Vấn đề:
Bạn là nhân viên nhân sự mới tại Công ty ABC Technology. Công ty cung cấp cho bạn một bộ tài liệu nội bộ gồm 5 chương, tổng cộng 120 trang, quy định về:

- Nội quy lao động.

- Quy định nghỉ phép.

- Chính sách làm thêm giờ.

- Quy định đánh giá nhân viên.

- Chính sách khen thưởng và kỷ luật.

Bạn cần nghiên cứu tài liệu để chuẩn bị cho buổi hướng dẫn nhân viên mới. Tuy nhiên, khi đưa toàn bộ tài liệu vào AI, hệ thống không thể xử lý hết nội dung trong một lần do giới hạn Context Window.
## Yêu cầu:
- Prompt dùng để xử lý từng phần tài liệu.

- Prompt dùng để tổng hợp các phần.

- Bảng tổng hợp gồm các cột: Chủ đề, Quy định chính, Điều kiện áp dụng, Ngoại lệ.

- Một bản tóm tắt hoàn chỉnh dài khoảng 1.000–1.500 từ.

- Ít nhất 5 câu hỏi kiểm tra thông tin được trích xuất từ tài liệu gốc, kèm câu trả lời và vị trí nội dung trong tài liệu.
## Cách làm:

## 1. Prompt dùng để xử lý từng phần tài liệu

```markdown
# ROLE (VAI TRÒ)
Bạn là một **Chuyên viên Phân tích & Chuẩn hóa Tài liệu Nhân sự (HR Document Analyst)** chính xác tuyệt đối, làm việc theo nguyên tắc **chỉ dựa trên văn bản được cung cấp** (Zero-Hallucination).

# CONTEXT (BỐI CẢNH)
Tài liệu quy định nhân sự của Công ty ABC Technology dài 120 trang (5 chương), vượt quá Context Window nên được chia thành từng phần/từng chương để xử lý độc lập, phục vụ biên soạn tài liệu hướng dẫn nhân viên mới.

# STRICT DATA CONSTRAINTS (RÀNG BUỘC DỮ LIỆU BẮT BUỘC)
1. **TUYỆT ĐỐI KHÔNG tự suy đoán, nội suy hoặc thêm quy định bên ngoài** không xuất hiện trong đoạn văn bản được cung cấp.
2. **Giữ nguyên 100% các con số, mốc thời gian, thời hạn, tỷ lệ phần trăm, hệ số, mức phạt/thưởng và điều kiện áp dụng** đúng như nguyên văn tài liệu.
3. **Không được bỏ qua bất kỳ trường hợp ngoại lệ nào** (nếu có ngoại lệ, phải liệt kê đầy đủ và ghi rõ điều kiện ngoại lệ).
4. Nếu một thông tin nào đó không xuất hiện trong phần văn bản này, hãy ghi rõ: **"Không đề cập trong phần tài liệu này"** (không tự điền).
5. Trích dẫn vị trí tương đối (tên/số chương, mục/điều, số trang nếu có) cho từng quy định quan trọng.

# TASKS FOR THIS CHUNK (NHIỆM VỤ XỬ LÝ PHẦN NÀY)
1. Tóm tắt phần tài liệu hiện tại theo đúng **Cấu trúc thống nhất** bên dưới.
2. Trích xuất danh sách **Thông tin trọng yếu & Dữ liệu cần lưu giữ** (số liệu, thời hạn, điều kiện, ngoại lệ, tham chiếu sang chương khác) để chuyển tiếp sang bước tổng hợp.
3. Liệt kê các **Mục còn thiếu / Chưa rõ / Cần kiểm tra ở chương khác** trong phần văn bản này.

# UNIFIED CHUNK OUTPUT FORMAT (ĐỊNH DẠNG ĐẦU RA THỐNG NHẤT)
## Tóm tắt phần: [Tên / Số chương - Phạm vi trang]
- **Mục tiêu & Phạm vi áp dụng:** ...
- **Các quy định chính & Số liệu/Thời hạn/Tỷ lệ:** ...
- **Điều kiện áp dụng:** ...
- **Trường hợp ngoại lệ:** ...
- **Liên kết / Tham chiếu tới nội dung hoặc chương khác (nếu có):** ...

## Key Takeaways & Memory Checkpoint (Thông tin lưu lại sau phần này)
- **Con số / Thời hạn / Tỷ lệ then chốt:** ...
- **Ngoại lệ quan trọng:** ...
- **Thông tin chưa đề cập trong phần này:** ...

# INPUT CHUNK (NỘI DUNG PHẦN TÀI LIỆU CẦN XỬ LÝ)
"""text
[DÁN NỘI DUNG TỪNG CHƯƠNG / TỪNG PHẦN TÀI LIỆU VÀO ĐÂY]
"""
```

---

## 2. Prompt dùng để tổng hợp các phần

```markdown
# ROLE (VAI TRÒ)
Bạn là một **Chuyên viên Tổng hợp & Kiểm chứng Tài liệu Nội bộ (HR Synthesis & QA Specialist)**, chuyên hợp nhất các bản tóm tắt theo từng chương thành một tài liệu hoàn chỉnh, chính xác và có tính liên kết chéo.

# CONTEXT (BỐI CẢNH)
Bạn nhận được các bản tóm tắt đã xử lý riêng lẻ từ 5 chương của tài liệu quy định nhân sự Công ty ABC Technology (120 trang):
1. Nội quy lao động
2. Quy định nghỉ phép
3. Chính sách làm thêm giờ
4. Quy định đánh giá nhân viên
5. Chính sách khen thưởng và kỷ luật

# STRICT DATA CONSTRAINTS (RÀNG BUỘC DỮ LIỆU BẮT BUỘC)
- Chỉ sử dụng thông tin có trong các bản tóm tắt/dữ liệu đầu vào đã cung cấp; **không tự suy đoán** những quy định không có trong tài liệu.
- **Giữ nguyên mọi con số, thời hạn, tỷ lệ và điều kiện** đã trích xuất; không làm tròn sai lệch hoặc tự diễn giải mở rộng.
- **Không bỏ sót trường hợp ngoại lệ** nào từ các phần.
- **Phân biệt rõ ràng** giữa:
  (a) *Thông tin có trong tài liệu*, và
  (b) *Thông tin chưa được đề cập / chưa rõ trong tài liệu*.

# SYNTHESIS & QA TASKS (NHIỆM VỤ TỔNG HỢP & KIỂM CHỨNG)
1. Hợp nhất toàn bộ các phần thành một tài liệu thống nhất theo chủ đề.
2. **Phát hiện các nội dung có liên quan giữa các chương** (ví dụ: nghỉ phép ảnh hưởng đến tính công/đánh giá; làm thêm giờ liên quan đến chế độ nghỉ bù/khen thưởng/kỷ luật; đánh giá hiệu suất gắn với khen thưởng/kỷ luật).
3. **Kiểm tra độ đầy đủ & phát hiện thông tin có thể bị bỏ sót** khi đối chiếu 5 chương với mục tiêu chuẩn bị buổi hướng dẫn nhân viên mới.
4. Xuất đủ các thành phần đầu ra theo yêu cầu:
   - **Bảng tổng hợp** gồm đúng 4 cột: `Chủ đề`, `Quy định chính`, `Điều kiện áp dụng`, `Ngoại lệ`.
   - **Bản tóm tắt hoàn chỉnh** dài khoảng **1.000–1.500 từ** (kiểm soát độ dài sát khoảng này, phân định rõ thông tin có trong tài liệu vs chưa được đề cập).
   - **Ít nhất 5 câu hỏi kiểm tra thông tin** trích xuất từ tài liệu gốc, kèm **câu trả lời** và **vị trí nội dung trong tài liệu**.

# INPUT SUMMARIES (CÁC BẢN TÓM TẮT TỪNG PHẦN)
"""markdown
[DÁN TẤT CẢ CÁC BẢN TÓM TẮT TỪNG CHƯƠNG & MEMORY CHECKPOINT VÀO ĐÂY]
"""
```

---

## 3. Bảng tổng hợp (Chủ đề, Quy định chính, Điều kiện áp dụng, Ngoại lệ)

| Chủ đề | Quy định chính | Điều kiện áp dụng | Ngoại lệ |
| :--- | :--- | :--- | :--- |
| **1. Nội quy lao động** *(Chương 1)* | Quy định giờ làm việc tiêu chuẩn, kỷ luật thời gian làm việc, tác phong/đồng phục, an toàn thông tin và bảo mật dữ liệu nội bộ của ABC Technology. *(Mọi con số/mốc giờ/mức xử lý cụ thể cần lấy đúng nguyên văn từ Chương 1 của file tài liệu).* | Áp dụng cho toàn thể người lao động làm việc tại ABC Technology, bao gồm cả nhân sự thử việc và nhân sự chính thức theo phạm vi quy định của chương. | Các trường hợp đặc thù theo ca/kíp, công tác ngoài văn phòng hoặc vị trí đặc biệt nếu được nêu rõ trong nội quy; nếu tài liệu không nêu thì ghi rõ *"Chưa được đề cập trong tài liệu"*. |
| **2. Quy định nghỉ phép** *(Chương 2)* | Quy định về phép năm, nghỉ ốm/thai sản/việc riêng, thủ tục và thời hạn báo trước/xin duyệt nghỉ phép cũng như cách tính ngày nghỉ. *(Giữ nguyên số ngày phép, thời hạn nộp đơn và tỷ lệ hưởng lương theo tài liệu).* | Áp dụng cho nhân viên đáp ứng điều kiện về thời gian làm việc, loại hợp đồng hoặc quy trình đăng ký nghỉ theo quy định từng loại phép. | Các ngoại lệ như nghỉ đột xuất khẩn cấp, quy định chuyển tiếp phép năm hoặc trường hợp đặc biệt được ghi nhận trong Chương 2; phần không có trong tài liệu phải đánh dấu *"Chưa được đề cập trong tài liệu"*. |
| **3. Chính sách làm thêm giờ (OT)** *(Chương 3)* | Quy định về điều kiện làm thêm giờ, giới hạn thời gian làm thêm (theo ngày/tháng/năm nếu có), quy trình phê duyệt trước và cách tính lương làm thêm hoặc nghỉ bù. *(Giữ nguyên mọi hệ số/tỷ lệ/giới hạn giờ theo tài liệu).* | Áp dụng khi có yêu cầu hoặc phê duyệt làm thêm giờ hợp lệ theo quy trình của bộ phận/công ty và thuộc nhóm đối tượng được áp dụng chế độ làm thêm. | Các vị trí/nhóm công việc đặc thù hoặc tình huống khẩn cấp được quy định riêng trong Chương 3; thông tin không có trong tài liệu ghi rõ *"Chưa được đề cập trong tài liệu"*. |
| **4. Quy định đánh giá nhân viên** *(Chương 4)* | Quy định về chu kỳ đánh giá (định kỳ/thử việc/dự án nếu có), tiêu chí/thang điểm đánh giá, quy trình phản hồi và xếp loại kết quả thực hiện công việc. *(Giữ nguyên chu kỳ, tỷ trọng tiêu chí và mốc thời gian theo tài liệu).* | Áp dụng cho nhân sự thuộc kỳ đánh giá theo quy định của công ty và có đủ thời gian làm việc tối thiểu theo từng kỳ đánh giá. | Trường hợp nhân viên mới vào làm chưa đủ thời gian xét đánh giá, nghỉ dài hạn hoặc trường hợp đặc biệt được quy định trong Chương 4; mục không có trong tài liệu ghi rõ *"Chưa được đề cập trong tài liệu"*. |
| **5. Chính sách khen thưởng và kỷ luật** *(Chương 5)* | Quy định các hình thức khen thưởng (thành tích, sáng kiến, định kỳ...) và các hình thức xử lý kỷ luật lao động cùng trình tự, thời hiệu/thời hạn áp dụng. *(Giữ nguyên mức thưởng, điều kiện xét và quy trình kỷ luật theo tài liệu).* | Khen thưởng áp dụng khi đạt thành tích/điều kiện theo quy định; kỷ luật áp dụng khi có hành vi vi phạm nội quy/quy định được nêu trong tài liệu. | Các tình tiết giảm nhẹ, tăng nặng, trường hợp miễn/giảm hoặc ngoại lệ đặc thù được quy định trong Chương 5; thông tin không có trong tài liệu ghi rõ *"Chưa được đề cập trong tài liệu"*. |

---

## 4. Bản tóm tắt hoàn chỉnh (khoảng 1.000–1.500 từ)

### Tổng quan tài liệu quy định nhân sự Công ty ABC Technology (120 trang – 5 chương)

Bộ tài liệu quy định nhân sự nội bộ của **Công ty ABC Technology** có tổng độ dài **120 trang**, được cấu trúc thành **5 chương** cốt lõi nhằm chuẩn hóa quản trị nguồn nhân lực và làm cơ sở triển khai chương trình hội nhập cho nhân viên mới. Do dung lượng lớn vượt quá giới hạn Context Window khi đưa toàn bộ vào một lượt xử lý, tài liệu cần được bóc tách và tổng hợp theo từng chương để đảm bảo tính chính xác, giữ nguyên các con số, thời hạn, tỷ lệ phần trăm, điều kiện áp dụng cũng như các trường hợp ngoại lệ mà không tự ý suy diễn.

#### A. Thông tin có trong cấu trúc 5 chương của tài liệu

**Chương 1 – Nội quy lao động:** Thiết lập các chuẩn mực hành vi và kỷ luật nền tảng tại nơi làm việc cho nhân sự của ABC Technology. Nội dung trọng tâm xoay quanh việc tuân thủ thời gian làm việc, tác phong chuyên nghiệp, trật tự nội bộ, bảo vệ tài sản và bảo mật thông tin công ty. Khi sử dụng cho buổi hướng dẫn nhân viên mới, phần này đóng vai trò định hình văn hóa kỷ luật ngay từ ngày đầu gia nhập, đồng thời là căn cứ đối chiếu khi phát sinh các hành vi vi phạm nội quy. Mọi mốc giờ cụ thể, quy định trang phục hay yêu cầu bảo mật đều phải được đối chiếu nguyên văn theo từng điều khoản của Chương 1.

**Chương 2 – Quy định nghỉ phép:** Quy định các chế độ nghỉ của người lao động, bao gồm nghỉ phép thường niên và các loại nghỉ có hưởng lương hoặc không hưởng lương theo quy định nội bộ. Chương này thường xác định rõ quyền lợi nghỉ phép theo thâm niên/thời gian làm việc, trình tự và thời hạn gửi đề xuất nghỉ phép, thẩm quyền phê duyệt cũng như cách xử lý ngày phép tồn đọng. Các điều kiện ràng buộc (như điều kiện đủ tháng làm việc hoặc thời hạn báo trước) và các trường hợp ngoại lệ (như trường hợp khẩn cấp hoặc quy định riêng của từng nhóm nhân sự) là những điểm nhân viên mới rất dễ nhầm lẫn nếu không được nêu rõ.

**Chương 3 – Chính sách làm thêm giờ:** Điều chỉnh hoạt động làm việc ngoài giờ tiêu chuẩn tại ABC Technology. Tài liệu quy định nguyên tắc đề xuất và phê duyệt làm thêm giờ, các giới hạn thời gian làm thêm theo từng khung thời gian (nếu có quy định trong tài liệu), cũng như cơ chế chi trả lương làm thêm giờ hoặc quy đổi nghỉ bù. Việc nắm rõ chính sách này giúp nhân viên mới hiểu rằng làm thêm giờ không tự phát mà phải tuân thủ điều kiện phê duyệt và giới hạn quy định, đồng thời nắm được quyền lợi và các ngoại lệ đi kèm nếu có.

**Chương 4 – Quy định đánh giá nhân viên:** Xác lập cơ chế đo lường và ghi nhận mức độ hoàn thành công việc của nhân sự. Nội dung chương tập trung vào chu kỳ đánh giá, bộ tiêu chí hoặc khung năng lực/kết quả, quy trình thực hiện đánh giá và xếp loại. Đây là cơ sở quan trọng để nhân viên mới hiểu cách hiệu quả công việc của mình được theo dõi, góp ý và xếp loại trong suốt quá trình làm việc tại công ty, bao gồm cả các điều kiện áp dụng cho nhân sự mới hoặc các trường hợp ngoại lệ theo quy định của chương.

**Chương 5 – Chính sách khen thưởng và kỷ luật:** Quy định hệ thống ghi nhận, khích lệ các cá nhân/tập thể đạt thành tích tốt và các biện pháp xử lý khi xảy ra vi phạm quy định. Phần khen thưởng làm rõ các hình thức và điều kiện xét thưởng; phần kỷ luật xác định các mức xử lý, điều kiện áp dụng, nguyên tắc xem xét và các trường hợp ngoại lệ. Việc trình bày song song khen thưởng và kỷ luật giúp nhân viên mới nhận thức đầy đủ cả quyền lợi ghi nhận thành tích lẫn trách nhiệm pháp lý/nội bộ khi vi phạm.

#### B. Mối liên hệ giữa các chương và kiểm tra thông tin có thể bị bỏ sót

Qua quá trình rà soát liên kết giữa 5 chương, các quy định nhân sự không tồn tại độc lập mà có sự móc nối chặt chẽ với nhau:
- **Nội quy lao động (Chương 1) ↔ Khen thưởng và kỷ luật (Chương 5):** Các hành vi tuân thủ tốt hoặc vi phạm nội quy lao động là đầu vào trực tiếp cho việc xét khen thưởng hoặc xử lý kỷ luật.
- **Nghỉ phép (Chương 2) & Làm thêm giờ (Chương 3) ↔ Đánh giá nhân viên (Chương 4):** Thời gian làm việc thực tế, việc nghỉ phép đúng/sai quy định và tần suất/hiệu quả làm thêm giờ có thể liên quan đến chấm công, mức độ sẵn sàng hoặc kết quả đánh giá tổng thể nếu tài liệu có quy định liên kết.
- **Đánh giá nhân viên (Chương 4) ↔ Khen thưởng và kỷ luật (Chương 5):** Kết quả đánh giá định kỳ hoặc đột xuất thường là căn cứ để xét khen thưởng hoặc áp dụng các biện pháp điều chỉnh/kỷ luật tương ứng theo quy định nội bộ.

Khi kiểm tra xem bản tổng hợp có bỏ sót thông tin quan trọng hay không, cần đặc biệt lưu ý các điểm dễ bị rút gọn quá mức trong quá trình tóm tắt tài liệu dài 120 trang: (1) các con số cụ thể (số ngày, số giờ, tỷ lệ %, mức tiền/điểm) và thời hạn nộp hồ sơ/phản hồi; (2) các điều kiện đi kèm ("với điều kiện...", "chỉ áp dụng khi..."); (3) các trường hợp ngoại lệ nằm rải rác ở cuối mỗi điều khoản; và (4) các phụ lục, biểu mẫu hoặc quy định chuyển tiếp nếu có trong file gốc.

#### C. Phân biệt thông tin có trong tài liệu và thông tin chưa được đề cập

Để đảm bảo tính trung thực tuyệt đối theo yêu cầu của bài thực hành:
- **Thông tin có trong tài liệu:** Là toàn bộ tên chương, phạm vi chủ đề, các điều khoản, con số, thời hạn, tỷ lệ, điều kiện áp dụng và ngoại lệ được in trực tiếp trong 5 chương của bộ tài liệu 120 trang của Công ty ABC Technology.
- **Thông tin chưa được đề cập trong tài liệu:** Bất kỳ con số cụ thể, tỷ lệ phần trăm, thời hạn xử lý, ngoại lệ đặc thù, chính sách phúc lợi bổ sung hoặc quy định pháp luật/thực tiễn ngoài văn bản nào **không xuất hiện** trong 5 chương của tài liệu đều được xếp vào nhóm *chưa được đề cập*. Trong quá trình soạn slide hoặc tài liệu hướng dẫn nhân viên mới, bộ phận nhân sự không được tự điền thay cho phần chưa có trong tài liệu mà phải đánh dấu rõ để xác minh lại với tài liệu gốc hoặc ban lãnh đạo/phòng nhân sự.

---

## 5. Câu hỏi kiểm tra thông tin trích xuất từ tài liệu gốc

> *Hướng dẫn sử dụng khi nộp bài:* Khi áp dụng lên file PDF/DOCX 120 trang thực tế, hãy thay thế các giá trị `[...]` bằng dữ liệu nguyên văn trong file và ghi rõ số trang/mục/điều chính xác.

1. **Câu hỏi 1 (Chương 1 – Nội quy lao động):** Theo Chương 1 của tài liệu, thời gian làm việc tiêu chuẩn và quy định về đi muộn/về sớm (hoặc bảo mật thông tin) của nhân viên ABC Technology được quy định cụ thể như thế nào?
   - **Câu trả lời:** `[Điền nguyên văn quy định, con số giờ/phút và điều kiện áp dụng được nêu trực tiếp trong Chương 1 của tài liệu; nếu mục này không có trong tài liệu thì ghi: "Không được đề cập trong tài liệu".]`
   - **Vị trí nội dung trong tài liệu:** Chương 1 (Nội quy lao động), Mục/Điều `[số mục/điều]`, Trang `[số trang]`.

2. **Câu hỏi 2 (Chương 2 – Quy định nghỉ phép):** Nhân viên được hưởng bao nhiêu ngày nghỉ phép năm (hoặc nghỉ chế độ) theo Chương 2, điều kiện để được hưởng và thời hạn đăng ký nghỉ phép là bao lâu?
   - **Câu trả lời:** `[Điền nguyên văn số ngày, điều kiện thâm niên/hợp đồng, thời hạn báo trước và trường hợp ngoại lệ theo đúng Chương 2; nếu không có thì ghi: "Không được đề cập trong tài liệu".]`
   - **Vị trí nội dung trong tài liệu:** Chương 2 (Quy định nghỉ phép), Mục/Điều `[số mục/điều]`, Trang `[số trang]`.

3. **Câu hỏi 3 (Chương 3 – Chính sách làm thêm giờ):** Điều kiện để một đợt làm thêm giờ được tính hợp lệ và tỷ lệ/mức quy đổi (lương hoặc nghỉ bù) cũng như giới hạn thời gian làm thêm được quy định ra sao trong Chương 3?
   - **Câu trả lời:** `[Điền nguyên văn điều kiện phê duyệt, giới hạn số giờ/tỷ lệ/hệ số và các trường hợp ngoại lệ trong Chương 3; nếu không có thì ghi: "Không được đề cập trong tài liệu".]`
   - **Vị trí nội dung trong tài liệu:** Chương 3 (Chính sách làm thêm giờ), Mục/Điều `[số mục/điều]`, Trang `[số trang]`.

4. **Câu hỏi 4 (Chương 4 – Quy định đánh giá nhân viên):** Chu kỳ đánh giá nhân viên diễn ra bao lâu một lần, tiêu chí/thang đánh giá gồm những gì và có ngoại lệ nào cho nhân viên mới vào làm chưa đủ thời gian không?
   - **Câu trả lời:** `[Điền nguyên văn chu kỳ, tiêu chí/thang điểm, điều kiện áp dụng và trường hợp ngoại lệ trong Chương 4; nếu không có thì ghi: "Không được đề cập trong tài liệu".]`
   - **Vị trí nội dung trong tài liệu:** Chương 4 (Quy định đánh giá nhân viên), Mục/Điều `[số mục/điều]`, Trang `[số trang]`.

5. **Câu hỏi 5 (Chương 5 – Chính sách khen thưởng và kỷ luật):** Các hình thức khen thưởng và hình thức kỷ luật trong Chương 5 được áp dụng trong những điều kiện nào, kèm theo thời hạn/thời hiệu hoặc trường hợp ngoại lệ nào?
   - **Câu trả lời:** `[Điền nguyên văn các hình thức khen thưởng/kỷ luật, điều kiện, thời hạn/tỷ lệ và ngoại lệ trong Chương 5; nếu không có thì ghi: "Không được đề cập trong tài liệu".]`
   - **Vị trí nội dung trong tài liệu:** Chương 5 (Chính sách khen thưởng và kỷ luật), Mục/Điều `[số mục/điều]`, Trang `[số trang]`.

6. **Câu hỏi 6 (Kiểm tra tính nhất quán & thông tin chưa đề cập):** Trong tài liệu có quy định rõ cách xử lý khi một trường hợp vừa thuộc diện làm thêm giờ/nghỉ phép vừa liên quan đến kết quả đánh giá hoặc khen thưởng/kỷ luật không?
   - **Câu trả lời:** `[Nêu chính xác điều khoản liên kết nếu có trong tài liệu; nếu tài liệu không quy định rõ sự liên kết này thì trả lời: "Không được đề cập rõ trong tài liệu" (không tự suy đoán).]`
   - **Vị trí nội dung trong tài liệu:** Đối chiếu Chương 2, Chương 3, Chương 4 và Chương 5, Trang `[số trang liên quan hoặc ghi rõ mục không có trong tài liệu]`.

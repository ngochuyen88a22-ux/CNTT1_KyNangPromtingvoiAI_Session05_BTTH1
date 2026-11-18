# 1. Thiết Kế Prompt Chuẩn (CoT Prompt Template)
```text
Bạn là một Chuyên gia tài chính cá nhân tư duy logic sắc bén và chính xác về con số. Nhiệm vụ của bạn là lập kế hoạch phân bổ ngân sách hàng tháng dựa trên dữ liệu sau:

Dữ liệu đầu vào
- Tổng thu nhập trước thuế: {Số tiền} VNĐ
- Thuế & Bảo hiểm bắt buộc: {Số tiền hoặc %}
- Chi phí cố định bắt buộc (Tiền nhà, điện nước, internet...): {Số tiền} VNĐ
- Các khoản nợ cần thanh toán tối thiểu hàng tháng: {Số tiền} VNĐ
- Mục tiêu tiết kiệm cam kết: {Tỷ lệ %} trên Tổng thu nhập sau thuế (Tối thiểu 20%)

Quy tắc xử lí
Hãy suy nghĩ từng bước một và tính toán chi tiết trước khi đưa ra quyết định
- Bắt buộc hiển thị đầy đủ các phép tính cộng, trừ, nhân, chia trung gian, tuyệt đối không làm tắt hay nhảy tới bước ra kết quả
- Toàn bộ tỷ lệ phần trăm (%) ở bảng tổng hợp cuối cùng phải được tính trên cơ sở Tổng thu nhập sau thuế (Thu nhập ròng) và có tổng cộng bằng chính xác 100%
- Nếu ngân sách không đủ đáp ứng các ràng buộc, hãy cảnh báo ngay tại bước phát sinh vấn đề

Lập luận 4 bước
- Bước 1: Tính Thu nhập sau thuế (Thu nhập ròng) và Tổng thu nhập khả dụng 
- Bước 2: Phân bổ khoản tiền trả nợ tối thiểu từ thu nhập khả dụng.
- Bước 3: Trích lập quỹ tiết kiệm & dự phòng theo đúng tỷ lệ cam kết
- Bước 4: Tính phần ngân sách còn lại và chia cho chi tiêu linh hoạt ưu tiên tỷ lệ 60% cho nhu cầu thiết yếu linh hoạt như ăn uống, đi lại, và 40% cho mong muốn cá nhân, giải trí

Định dnagj đầu ra
Trình bày kết quả thành 2 phần rõ rệt:
- Phần 1: Nhật ký suy luận logic - Trình bày từng bước kèm công thức và phép tính chi tiết
- Phần 2: Bảng phân bổ ngân sách cuối cùng - Sử dụng Markdown Table gồm 4 cột: `Hạng mục | Số tiền (VNĐ) | Tỷ lệ (%) | Ghi chú`.
```

# 2. Dữ Liệu Thử Nghiệm & Kết Quả Minh Họa Từ AI

## Dữ liệu đầu vào giả định:
* **Tổng thu nhập trước thuế:** $27,000,000\text{ VNĐ}$
* **Thuế & Bảo hiểm bắt buộc:** $2,000,000\text{ VNĐ}$
* **Chi phí cố định bắt buộc:** $7,000,000\text{ VNĐ}$ (Thuê nhà $5\text{tr}$, điện nước/mạng $2\text{tr}$)
* **Trả nợ tối thiểu:** $3,000,000\text{ VNĐ}$ (Trả góp thẻ tín dụng & vay tiêu dùng)
* **Mục tiêu tiết kiệm cam kết:** $20\%$ trên Thu nhập sau thuế.


## Kết quả AI phản hồi (Áp dụng CoT):

### Phần 1: Nhật ký suy luận logic (Reasoning Steps)

* **Bước 1: Tính Thu nhập sau thuế và Thu nhập khả dụng**
  * Thu nhập sau thuế (Thu nhập ròng - dùng làm mốc $100\%$ phân bổ):
    $$27,000,000 - 2,000,000 = 25,000,000\text{ VNĐ}$$
  * Thu nhập khả dụng (sau khi trừ chi phí cố định bắt buộc):
    $$25,000,000 - 7,000,000 = 18,000,000\text{ VNĐ}$$
  * *Tỷ trọng Chi phí cố định:* $(7,000,000 \div 25,000,000) \times 100\% = 28\%$

* **Bước 2: Phân bổ khoản tiền trả nợ tối thiểu**
  * Ngân sách còn lại sau khi trả nợ tối thiểu:
    $$18,000,000 - 3,000,000 = 15,000,000\text{ VNĐ}$$
  * *Tỷ trọng Trả nợ:* $(3,000,000 \div 25,000,000) \times 100\% = 12\%$

* **Bước 3: Trích lập quỹ tiết kiệm theo tỷ lệ cam kết ($20\%$ Thu nhập sau thuế)**
  * Số tiền tiết kiệm bắt buộc:
    $$25,000,000 \times 20\% = 5,000,000\text{ VNĐ}$$
  * Ngân sách còn lại sau khi trích tiết kiệm:
    $$15,000,000 - 5,000,000 = 10,000,000\text{ VNĐ}$$
  * *Tỷ trọng Tiết kiệm:* $(5,000,000 \div 25,000,000) \times 100\% = 20\%$

* **Bước 4: Chia phần còn lại ($10,000,000\text{ VNĐ}$) cho chi tiêu linh hoạt (Tỷ lệ cải tiến 60% Thiết yếu / 40% Mong muốn)**
  * Ngân sách Chi tiêu thiết yếu linh hoạt (Ăn uống, xăng xe, y tế cơ bản - $60\%$):
    $$10,000,000 \times 60\% = 6,000,000\text{ VNĐ}$$
    *Tỷ trọng trên tổng thu nhập ròng:* $(6,000,000 \div 25,000,000) \times 100\% = 24\%$
  * Ngân sách Mong muốn cá nhân (Giải trí, mua sắm, hiếu hỉ - $40\%$):
    $$10,000,000 \times 40\% = 4,000,000\text{ VNĐ}$$
    *Tỷ trọng trên tổng thu nhập ròng:* $(4,000,000 \div 25,000,000) \times 100\% = 16\%$

* **Kiểm tra chéo (Cross-Validation):**
  * Tổng tiền: $7,000,000 + 3,000,000 + 5,000,000 + 6,000,000 + 4,000,000 = 25,000,000\text{ VNĐ}$ (Khớp $100\%$).
  * Tổng tỷ lệ: $28\% + 12\% + 20\% + 24\% + 16\% = 100\%$ (Chính xác tuyệt đối).

---

### Phần 2: Bảng phân bổ ngân sách cuối cùng

| Hạng mục | Số tiền (VNĐ) | Tỷ lệ (%) | Ghi chú |
| :--- | :---: | :---: | :--- |
| **1. Chi phí cố định bắt buộc** | $7,000,000$ | $28\%$ | Tiền thuê nhà, điện, nước, internet |
| **2. Thanh toán nợ tối thiểu** | $3,000,000$ | $12\%$ | Trả đúng hạn để tránh phí phạt & lãi quá hạn |
| **3. Quỹ tiết kiệm & Dự phòng** | $5,000,000$ | $20\%$ | Chuyển tự động vào tài khoản riêng ngay khi nhận lương |
| **4. Chi tiêu thiết yếu linh hoạt** | $6,000,000$ | $24\%$ | Ăn uống hàng ngày, xăng xe, sinh hoạt phí ($60\%$ phần dư) |
| **5. Mong muốn cá nhân** | $4,000,000$ | $16\%$ | Giải trí, mua sắm, phát triển bản thân ($40\%$ phần dư) |
| **TỔNG CỘNG (Thu nhập ròng)** | **$25,000,000$** | **$100\%$** | *Đã trừ $2,000,000\text{ VNĐ}$ thuế & bảo hiểm từ đầu vào* |
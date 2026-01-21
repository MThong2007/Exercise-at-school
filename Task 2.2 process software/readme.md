# 📄 README – Khắc phục lỗi Notepad++ không mở được file Python lớn trên Windows

## 🎯 Mục đích

Tài liệu này hướng dẫn **từng bước cụ thể** để khắc phục lỗi **Notepad++ không mở được file Python (.py) dung lượng lớn** trên hệ điều hành Windows.

Phù hợp cho:

* Sinh viên
* Lập trình viên Python
* Người xử lý log / dữ liệu lớn

---

## ❗ Dấu hiệu lỗi thường gặp

* Notepad++ **không mở file** hoặc mở rất lâu
* Chương trình **bị treo / Not Responding**
* Mở xong nhưng **lag nặng, cuộn rất chậm**
* File chỉ có **1 dòng cực dài**

---

## 1️⃣ Kiểm tra dung lượng & cấu trúc file

### 🔍 Kiểm tra nhanh

* Chuột phải vào file `.py` → **Properties**
* Nếu:

  * > **50 MB** → có nguy cơ lỗi cao
  * > **100 MB** → Notepad++ thường không xử lý tốt

📌 Lưu ý đặc biệt:

* File có **1 dòng rất dài** (ví dụ dữ liệu JSON, log) sẽ làm Notepad++ treo

---

## 2️⃣ Tắt plugin gây nặng (RẤT QUAN TRỌNG)

### Cách thực hiện:

1. Mở **Notepad++**
2. Vào **Plugins → Plugins Admin**
3. Gỡ hoặc Disable các plugin sau (nếu có):

   * ❌ Python Script
   * ❌ Compare
   * ❌ XML Tools
   * ❌ NppFTP
4. **Restart Notepad++**

➡️ Thử mở lại file `.py`

---

## 3️⃣ Mở file ở chế độ Normal Text (không tô màu Python)

### Cách làm:

1. Mở Notepad++
2. **File → Open** → chọn file `.py`
3. Ngay khi mở xong, vào:

   ```
   Language → Normal Text
   ```

📌 Cách này giúp tránh lỗi do **syntax highlighting**

---

## 4️⃣ Tối ưu hiệu năng Notepad++

### Thiết lập khuyến nghị:

1. **Settings → Preferences → Performance**
2. Thiết lập:

   * ✔ Disable smooth scrolling
   * ✔ Disable auto-completion
   * ✔ Disable word wrap
3. Nếu có mục **Large file restriction**:

   * Đặt ≥ **200 MB**
4. **Restart Notepad++**

---

## 5️⃣ BẮT BUỘC dùng Notepad++ 64-bit

### Kiểm tra phiên bản:

* Mở Notepad++ → **? → About Notepad++**

❌ Nếu là **32-bit** → nên gỡ

✅ Cài lại **Notepad++ 64-bit**

📌 Bản 32-bit rất dễ lỗi với file lớn

---

## 6️⃣ Chia nhỏ file Python (CÁCH HIỆU QUẢ NHẤT)

### 🔹 Dùng Python để chia file:

```python
with open("file.py", "r", encoding="utf-8", errors="ignore") as f:
    for i, chunk in enumerate(iter(lambda: f.read(20_000_000), "")):
        with open(f"part_{i}.py", "w", encoding="utf-8") as out:
            out.write(chunk)
```

➡️ Mỗi file ~20MB, mở mượt trong Notepad++

---

## 7️⃣ Dùng editor khác (KHUYÊN DÙNG)

Nếu file quá lớn, **Notepad++ không còn phù hợp**.

### Editor thay thế tốt hơn:

| Công cụ      | Khả năng mở file lớn |
| ------------ | -------------------- |
| VS Code      | ⭐⭐⭐⭐                 |
| Sublime Text | ⭐⭐⭐⭐⭐                |
| EmEditor     | ⭐⭐⭐⭐⭐                |
| UltraEdit    | ⭐⭐⭐⭐⭐                |

📌 VS Code nên bật:

```json
"editor.largeFileOptimizations": true
```

---

## 8️⃣ Kiểm tra Encoding

File encoding lạ cũng gây lỗi.

### Thử:

* **Encoding → Convert to UTF-8 (without BOM)**
* Lưu file → mở lại

---

## ✅ Tổng kết nhanh

| Tình huống      | Giải pháp                      |
| --------------- | ------------------------------ |
| File < 50MB     | Tắt plugin + Normal Text       |
| File 50–200MB   | Notepad++ 64-bit + Performance |
| File rất lớn    | VS Code / EmEditor             |
| 1 dòng siêu dài | Chia file                      |

---

📌 **Khuyến nghị cuối**: Nếu bạn thường xuyên làm việc với file Python lớn → **VS Code hoặc EmEditor** là lựa chọn ổn định hơn Notepad++.

---

✍️ Tài liệu này có thể dùng làm **README.md** cho project hoặc gửi kèm khi hỗ trợ kỹ thuật.

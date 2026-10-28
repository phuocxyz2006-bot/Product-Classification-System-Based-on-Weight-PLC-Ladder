# Product-Classification-System-Based-on-Weight
# 📦 Dây Chuyền Phân Loại Sản Phẩm Theo Khối Lượng (TIA Portal)

Dự án tự động hóa dây chuyền cân và phân loại sản phẩm thành 3 phân khúc (Nhẹ, Trung bình, Nặng) sử dụng PLC Siemens, tín hiệu Analog từ Cân Loadcell và hệ thống pittong khí nén. Dự án bao gồm màn hình giám sát trực quan trên WinCC/HMI[cite: 15].

---

## 💻 1. Cấu Trúc Khối Chương Trình (Program Blocks)

Toàn bộ logic được cấu trúc hóa thông qua các khối hàm FC độc lập, giúp chương trình rành mạch và dễ kiểm tra lỗi[cite: 14]:

* **`Main [OB1]`**: Vòng quét chính, gọi các khối hàm xử lý liên tục[cite: 14].
* **`FC_MANUAL_MODE [FC1]`**: Khối điều khiển chế độ bằng tay, cho phép test riêng lẻ băng tải hoặc pittong[cite: 14].
* **`FC_AUTO_MODE [FC2]`**: Khối điều khiển chế độ tự động chạy theo chu trình phân loại[cite: 14].
* **`FC_SIMULATION [FC3]`**: Khối tạo biến ảo phục vụ mô phỏng hệ thống chạy mà không cần đấu nối thiết bị thực[cite: 14].
* **`FC_DOC_ANALOG [FC4]`**: Khối hàm xử lý đọc và scale tín hiệu Analog từ cảm biến Loadcell thành giá trị khối lượng thực[cite: 14].
* **`FC_OUTPUT [FC5]`**: Khối xử lý tín hiệu đầu ra, kích hoạt các pittong phân loại và băng tải[cite: 14].

---

## 🏷️ 2. Quản Lý Biến Hệ Thống (PLC Tags)

Biến (Tags) được phân tách gọn gàng vào các thư mục riêng biệt[cite: 14]:

* **`INPUT [9]`** / **`OUTPUT [5]`**: Tập hợp các tín hiệu ngõ vào (Cảm biến) và ngõ ra (Động cơ, Pittong) thực tế[cite: 14].
* **`AUTO_OUTPUT [5]`** / **`MANU_OUTPUT [5]`**: Tín hiệu ngõ ra tách biệt tương ứng cho chế độ Tự động và Bằng tay[cite: 14].
* **`ACTUAL [9]`**: Các biến lưu trữ giá trị thực tế (trọng lượng đang cân, số lượng sản phẩm đếm được)[cite: 14].
* **`SETTING [2]`**: Biến lưu trữ ngưỡng khối lượng cài đặt cho sản phẩm Nhẹ và Trung bình[cite: 14].
* **`MEMORY [12]`**: Vùng nhớ lưu trạng thái, cờ (flag) trung gian của chu trình[cite: 14].
* **`XUNG [9]`**: Quản lý các biến Timer và xung sườn lên/xuống[cite: 14].

---

## 🖥️ 3. Giao Diện Giám Sát HMI (WinCC)
<img width="1007" height="673" alt="image" src="https://github.com/user-attachments/assets/95bc88bb-297f-4b28-b954-64377db477db" />
Màn hình vận hành "DÂY CHUYỀN PHÂN LOẠI SẢN PHẨM THEO KHỐI LƯỢNG" được thiết kế bao gồm[cite: 15]:

* **Khu vực Điều khiển (Bảng Điều Khiển):**
  * Gạt chọn **CHẾ ĐỘ** hoạt động (MANUAL / AUTO)[cite: 15].
  * Công tắc kích hoạt **Mô phỏng** (ON/OFF)[cite: 15].
  * Nút nhấn **Reset** để đưa hệ thống về trạng thái ban đầu[cite: 15].
* **Khu vực Cài đặt (CÀI ĐẶT):**
  * Nhập ngưỡng phân loại theo khối lượng: **SP NHẸ [Kg]** và **SP TB [Kg]**[cite: 15].
* **Mô phỏng Chu trình Trực quan:**
  * Giám sát hệ thống **Băng tải sản phẩm** và tín hiệu khối lượng đo trực tiếp tại **Cân Loadcell**[cite: 15].
  * Hệ thống các cảm biến quang giám sát vị trí: **CB1, CB2, CB3, CB4** đi kèm bộ đếm hiển thị `### [SP]` tại từng trạm[cite: 15].
  * Cơ cấu gạt: **Pittong SP nhẹ** và **Pittong SP trung bình** (kèm switch test tay)[cite: 15].
  * Các thùng chứa hiển thị số lượng theo 3 phân loại: **Sản phẩm nhẹ**, **Sản phẩm trung bình**, và cuối line là **Sản phẩm nặng**[cite: 15].

---

## 🚀 4. Hướng Dẫn Chạy Mô Phỏng
1. Bật phần mềm TIA Portal, mở project.
2. Chạy **S7-PLCSIM** để giả lập PLC.
3. Bật mô phỏng màn hình HMI.
4. Trên HMI: Gạt công tắc **Mô phỏng** sang **ON**[cite: 15].
5. Cài đặt các thông số Kg cho **SP NHẸ** và **SP TB**[cite: 15].
6. Chuyển sang chế độ **AUTO**, sau đó quan sát cách băng tải chạy, cân loadcell đọc giá trị và pittong tự động đẩy sản phẩm vào đúng thùng chứa.

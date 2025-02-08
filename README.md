# **Báo cáo Kiểm Thử Hiệu Suất với Apache JMeter**

## **1. Mô tả bài tập**
Là một kiểm thử viên phần mềm, nhiệm vụ của tôi là đánh giá hiệu suất của một trang web https://reqres.in/  bằng công cụ Apache JMeter. Bài kiểm thử tập trung vào việc kiểm tra tải (Load Testing) và khả năng chịu tải (Stress Testing) của hệ thống.

## **2. Cài đặt công cụ**
- **Công cụ sử dụng:** Apache JMeter
- **Link tải:** [JMeter Official Website](https://jmeter.apache.org/)
- **Môi trường thử nghiệm:** Windows/Linux/MacOS
- **Phiên bản JMeter sử dụng:** 5.x

## **3. Thiết lập kịch bản kiểm thử hiệu suất**
### **3.1. Mô phỏng 50 người dùng đồng thời truy cập trang web trong vòng 5 phút**
- **Number of Threads (Users):** 50
- **Ramp-up Period:** 50 giây (tăng dần mỗi giây 1 user)
- **Loop Count:** 1
- **Thời gian kiểm thử:** 300 giây (5 phút)
- **Thành phần sử dụng:** HTTP Request Sampler để gửi yêu cầu đến trang chủ.
  ![image](https://github.com/user-attachments/assets/ccfa89fa-9186-465d-a22a-35be6a9873c7)


### **3.2. Kiểm thử tải (Load Testing) - Tăng dần từ 10 đến 50 user**
- **Cách thiết lập:**
  - Bắt đầu với 10 user, sau đó tăng dần lên 50 user theo từng giai đoạn.
  - Sử dụng Ultimate Thread Group để thiết lập các mức tải cụ thể.
  - Ghi nhận thời gian phản hồi trung bình và tỷ lệ lỗi.
![image](https://github.com/user-attachments/assets/2cad1929-cffb-41d3-a45c-3d0ac9e79a63)
![image](https://github.com/user-attachments/assets/7e329ab1-81c6-42d3-af4b-3e83760e836e)
![image](https://github.com/user-attachments/assets/76fb77ff-7aad-4c91-bd1d-44027b1dd509)

### **3.3. Kiểm thử khả năng chịu tải (Stress Testing)**
- **Mục tiêu:** Xác định giới hạn chịu tải của hệ thống.
- **Cách thiết lập:**
  - Tăng số lượng user từ 50 lên 100 để kiểm tra mức tối đa hệ thống có thể chịu.
  - Quan sát thời điểm hệ thống bắt đầu có dấu hiệu giảm hiệu suất nghiêm trọng.
![image](https://github.com/user-attachments/assets/ca3981b7-4eb3-41de-8908-65e763334c51)
![image](https://github.com/user-attachments/assets/eabcf150-f5a2-45c8-96fc-ddfd3805f32a)
![image](https://github.com/user-attachments/assets/8fed7daf-2acf-490c-b1cf-e35ddf1daa97)

## **4. Phân tích kết quả**
### **4.1. Xuất báo cáo từ JMeter**
- **Định dạng báo cáo:** `.csv`, `.jtl`, và biểu đồ từ JMeter
- **Chỉ số quan trọng:**
  - **Response Time:** Thời gian phản hồi trung bình
  - **Throughput:** Số lượng request xử lý mỗi giây
  - **Error Rate:** Tỷ lệ lỗi xảy ra
  - **CPU, Memory Usage:** Sử dụng công cụ giám sát để đo tài nguyên hệ thống

### **4.2. Nhận xét**
- **Dưới 50 user:** Hệ thống hoạt động ổn định, thời gian phản hồi trung bình là `0.98 Kb/s`.
- **Từ 50 đến 100 user:** Hệ thống vẫn duy trì hiệu suất tốt, thời gian phản hồi tăng nhẹ lên 1038 Kb/s, không có lỗi nào xảy ra (Error Rate = 0%)..
- **Trên 100 user:** Hệ thống bắt đầu có dấu hiệu giảm hiệu suất (nếu có), nhưng không ghi nhận lỗi..

## **5. Câu hỏi thảo luận**
### **5.1. Tại sao kiểm thử phi chức năng lại quan trọng trong phần mềm?**
- Đảm bảo hệ thống có thể xử lý tải lớn mà không gặp sự cố.
- Cải thiện trải nghiệm người dùng.
- Xác định bottleneck để tối ưu hiệu suất.

### **5.2. Các thông số quan trọng cần theo dõi trong kiểm thử hiệu suất**
- **Thời gian phản hồi (Response Time)**
- **Throughput (TPS - Transactions Per Second)**
- **Tỷ lệ lỗi (Error Rate)**
- **CPU & Memory Usage**
- **Số lượng kết nối đồng thời (Concurrent Users)**

### **5.3. Nếu hệ thống không đáp ứng yêu cầu hiệu suất, bạn sẽ đề xuất giải pháp gì?**
- Tối ưu truy vấn cơ sở dữ liệu.
- Caching dữ liệu để giảm tải cho máy chủ.
- Load Balancing để phân phối tải giữa nhiều máy chủ.
- Tăng tài nguyên phần cứng (RAM, CPU, SSD).
- Sử dụng CDN để tăng tốc độ tải trang.

## **6. Kết luận**
Sau khi kiểm thử, nhóm phát triển có thể đưa ra các cải tiến cần thiết để đảm bảo hệ thống hoạt động ổn định khi có nhiều người dùng đồng thời.

### **📌 Hướng dẫn chạy lại kiểm thử**
1. **Clone repository:**
```bash
   git clone https://github.com/tranphucnguyen/KiemthuJmeter
```
2. **Mở JMeter và tải kịch bản kiểm thử**
3. **Chạy kiểm thử và quan sát kết quả**

🚀 **Chúc bạn kiểm thử thành công!**


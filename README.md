## 1\. Thiết kế Kiến trúc Script `auto_report.ps1`

Cấu trúc script PowerShell chuẩn gồm 3 khối chính:

* Khối Header & Giao diện: Sử dụng lệnh `Write-Host` kèm tham số `-ForegroundColor` để in thông báo chào mừng và tiêu đề trực quan, chuyên nghiệp lên màn hình console.  
* Khối Xây dựng Tiêu đề Báo cáo: Sử dụng cmdlet `Get-Date` để lấy ngày tháng hiện động, kết hợp với toán tử ghi đè (`>`) để khởi tạo file báo cáo mới chứa dòng tiêu đề định danh theo ngày.  
* Khối Logic Xử lý & Ghi Log: Dùng mô hình Pipeline nối `Get-Content`, `Select-String` và toán tử ghi nối (`>>` hoặc `Add-Content`) để quét file `access.log`, lọc các dòng lỗi 404 và bổ sung trực tiếp vào tệp báo cáo mà không làm mất dữ liệu cũ.

## 2\. Mã nguồn `auto_report.ps1` hoàn chỉnh

Write-Host "--- HỆ THỐNG LỌC LOG AUTOMATION \---" \-ForegroundColor Green  
\$today \= Get-Date  
"=== LOG REPORT DATE \[\$today\] \===" \> report.txt  
Get-Content access.log | Select-String "404" \>\> report.txt  
Write-Host "Đã xuất báo cáo thành công vào file report.txt\!" \-ForegroundColor Yellow  
"# CNTT2_IT108_Session06_Ex05" 

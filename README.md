# exp-fig-bug-VIETTIN-company
các bước sau được các anh trong cty chỉ và thêm một vài tìm hiểu của bản thân mình

1. Email sending failures (Lỗi gửi email)
- Các nguyên nhân phổ biến: SMTP server lỗi, port bị chặn, SPF/DKIM/DMARC sai, relay restriction, firewall chặn, quota đầy
- Cách xử lý thực tế: Kiểm tra log (Exchange/Postfix): tail -f /var/log/maillog hoặc Event Viewer Windows.
- Test telnet SMTP: telnet smtp.gmail.com 25 hoặc 587/465.
- Kiểm tra firewall/antivirus chặn port 25, 587, 465.
- Verify DNS: SPF record, DKIM record, Reverse DNS (PTR record).
- Kiểm tra quota user/domain và relay permission.
- Giải pháp: Cấu hình Smart Host / Relay Server hoặc chuyển sang Microsoft 365 / Google Workspace.

2. User account synchronization errors (Lỗi đồng bộ tài khoản)
- Thường gặp trong Active Directory, Azure AD, LDAP sync.
- Cách xử lý:Kiểm tra log Synchronization Service (Event Viewer → Application).
- Kiểm tra kết nối network giữa 2 server (ping, port 389/636 LDAP, 5355 DNS).
- Force sync: repadmin /syncall (AD) hoặc chạy manual sync tool.
- Kiểm tra password policy, account lockout, và attribute mapping.
- Kiểm tra lỗi phổ biến: Duplicate account, SID conflict, permission trên OU.
- Xóa cache và restart synchronization service.

3. File access issues (Không truy cập được file)
- Cách xử lý:Kiểm tra Permission: NTFS Permission + Share Permission (Right-click → Properties → Security).
- Kiểm tra Effective Access (Advanced → Effective Access).
- Kiểm tra antivirus/EDR chặn file.
- Kiểm tra network share (SMB port 445 có mở không?).
- Kiểm tra Group Policy chặn access.
- Sử dụng lệnh: icacls "path\to\file" để xem quyền.
- Giải pháp: Reset permission bằng icacls /reset hoặc Ownership takeover.

4. Network connectivity problems (Mất kết nối mạng)
- Quy trình troubleshooting chuẩn
- Check Timezone
- Physical Layer: Check cable, LED switch, WiFi signal.
- IP Layer: ipconfig /release → /renew, ping 8.8.8.8, ping gateway.
- DNS: nslookup google.com, flush DNS (ipconfig /flushdns).
- Route: tracert 8.8.8.8, route print.
- Dùng Wireshark capture packet để xem gói tin có đi không, có bị drop không.
- Kiểm tra Firewall rule (pfSense / Windows Firewall).
- Kiểm tra VLAN / Port security trên Switch.

6. Slow system performance (Hệ thống chạy chậm)
- Các bước:Kiểm tra Resource Monitor / Task Manager (CPU, RAM, Disk %).
- Kiểm tra Disk (chuyển sang SSD nếu HDD, check SMART).
- Kiểm tra Startup programs và Services không cần thiết.
- Update driver & Windows patch.
- Kiểm tra Malware (quét bằng Malwarebytes + Windows Defender).
- Kiểm tra network bottleneck (iPerf test).
- Check Event Viewer lỗi.

7. Server errors (Lỗi server chung)
- Check Power Cable and Network Cable
- Xem Event Viewer (Windows) hoặc /var/log/ (Linux) trước tiên.
- Kiểm tra disk space (df -h trên Linux).
- Kiểm tra Service status (services.msc hoặc systemctl status).
- Check Application-specific log (IIS, SQL, Exchange…).


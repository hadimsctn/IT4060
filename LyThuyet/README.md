int getaddrinfo(
const char* nodename, // Tên miền hoặc địa chỉ cần phân giải
const char* servname, // Dịch vụ hoặc cổng
const struct addrinfo* hints, // Cấu trúc gợi ý
struct addrinfo** res // Kết quả
);
Giá trị trả về
• Thành công: 0
• Thất bại: mã lỗi, sử dụng hàm gai_strerror() để in ra thông báo lỗi
• Giải phóng: hàm freeaddrinfo()
_____________________
struct addrinfo {
int ai_flags; // Thường là AI_CANONNAME
int ai_family; // Thường là AF_INET
int ai_socktype; // Loại socket
int ai_protocol; // Giao thứ giao vận
socklen_t ai_addrlen; // Chiều dài của ai_addr
char* ai_canonname; // Tên miền
struct sockaddr* ai_addr; // Địa chỉ socket đã phân giải
struct addrinfo* ai_next; // Con trỏ tới cấu trúc sau
};
__________________
• Sử dụng cấu trúc gợi ý để lọc kết quả
struct addrinfo hints;
// IPv4: AF_INET
// IPv6: AF_INET6
// Không xác định: AF_UNSPEC
hints.ai_family = AF_UNSPEC;
// TCP: SOCK_STREAM
// UDP: SOCK_DGRAM
// Không xác định: 0
hints.ai_socktype = SOCK_STREAM;
// TCP: IPPROTO_TCP
// UDP: IPPROTO_UDP
// Không xác định: 0
hints.ai_protocol = IPPROTO_TCP;
________________
Truyền dữ liệu sử dụng TCP - Ứng dụng server
• Tạo socket qua hàm socket()
• Gắn socket vào một giao diện mạng thông qua hàm
bind()
• Chuyển socket sang trạng thái đợi kết nối qua hàm
listen()
• Chấp nhận kết nối từ client thông qua hàm accept()
• Gửi dữ liệu tới client thông qua hàm send()/write()
• Nhận dữ liệu từ client thông qua hàm recv()/read()
• Đóng socket khi việc truyền nhận kết thúc bằng hàm
close()
___________________
Ứng dụng client
• Tạo socket qua hàm socket()
• Điền thông tin về server vào cấu trúc sockaddr_in
• Kết nối tới server qua hàm connect()
• Gửi dữ liệu tới server thông qua hàm send()
• Nhận dữ liệu từ server thông qua hàm recv()
• Đóng socket khi việc truyền nhận kết thúc bằng hàm 
close()

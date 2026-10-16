# Báo cáo Lab A8 - Fragment

- **Họ và tên:** Nguyễn Nhật Duy
- **MSSV:** 231A010060

## Mô tả 2 bài nâng cao đã làm

### NC4. Hiệu ứng chuyển cảnh Fragment (Custom Animations)
- **Mục tiêu:** Tạo hiệu ứng hoạt họa trượt mượt mà khi người dùng điều hướng giữa các Fragment.
- **Chi tiết thực hiện:**
  - Định nghĩa 4 file hiệu ứng XML trong thư mục `res/anim/`: `slide_in_right.xml`, `slide_out_left.xml`, `slide_in_left.xml`, `slide_out_right.xml`.
  - Thiết lập phương thức `.setCustomAnimations(R.anim.slide_in_right, R.anim.slide_out_left, R.anim.slide_in_left, R.anim.slide_out_right)` trong `FragmentTransaction`:
    - Tại `MainActivity.java`: Khi chuyển đổi giữa các tab ở `BottomNavigationView`.
    - Tại `NewsListFragment.java`: Khi mở `NewsDetailFragment` và khi nhấn Back / Đã đọc để quay về (`popBackStack`).

---

### NC1. Giao diện thích ứng cho Tablet / Màn hình lớn (Adaptive Multi-pane Layout)
- **Mục tiêu:** Tối ưu hóa trải nghiệm hiển thị trên các thiết bị màn hình lớn (tablet có chiều rộng $\ge 600\text{dp}$) bằng cách chia đôi màn hình dạng Master-Detail.
- **Chi tiết thực hiện:**
  - Thêm layout riêng cho tablet tại `res/layout-sw600dp/activity_main.xml`, chia ngang thành 2 phần: `fragmentContainer` (danh sách tin tức, weight = 1) và `detailContainer` (nội dung chi tiết, weight = 2).
  - Trong `NewsListFragment.java` xử lý logic kiểm tra linh hoạt:
    - Nếu phát hiện có `detailContainer` (Tablet): Thay thế `NewsDetailFragment` trực tiếp vào khung `detailContainer` bên cạnh mà không cần đẩy vào BackStack.
    - Nếu không có (Điện thoại bình thường): Thay thế toàn màn hình trên `fragmentContainer` và đưa vào BackStack (`addToBackStack("chi_tiet")`) để bấm Back quay về danh sách tin.

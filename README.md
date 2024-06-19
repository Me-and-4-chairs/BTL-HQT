-- tác giả: ĐINH TRƯỜNG AN

-- mô tả: Sản phẩm làm về quản lý siêu thị

# Thông tin sinh viên
Mã SV : K215480106058

Họ Và Tên : Đinh Trường An

Lớp: K57KMT

Tên đề tài: Quản lý quản lý siêu thị

# Project csdl cho bài toán:
mô tả về bài toán: Để quản lý siêu thị cần thiết kế cơ sở dữ liệu bao gồm các thông tin về nhân viên, khách hàng, sản phẩm, các hóa đơn, doanh thu,....

# Chức năng:
Bài toán quản lý siêu thị nhằm đảm bảo quản lý hiệu quả và tối ưu hóa nguồn tài nguyên:

Quản lý thông tin sản phẩm : thêm , xóa , sửa thông tin, xem thông tin sản phẩm

Quản lý các chức năng tính toán: Giá nhập, Doanh thu.

Báo cáo hóa đơn, lượng hàng đã bán

Tìm mặt hàng bán chạy nhất

Sử dụng trigger để quản lý Hóa Đơn mới được cập nhật

# Tạo cơ sở dữ liệu gồm các bảng
tạo database:
```sql
CREATE DATABASE QLST;
GO
-- Sử dụng cơ sở dữ liệu QuanLy
USE QLST;
GO
```

Bảng nhân viên :
```sql
CREATE TABLE NHANVIEN (
    MaNV CHAR(6) PRIMARY KEY,
    HoTenNV NVARCHAR(30),
    GioiTinh CHAR(3),
    NgaySinh DATE,
    DiaChi NVARCHAR(255),
    DienThoai CHAR(10)
);
```

Bảng khách hàng :
```sql
CREATE TABLE KHACHHANG (
    MaKH CHAR(6) PRIMARY KEY,
    HoTenKH NVARCHAR(30),
    DiaChi NVARCHAR(255),
    DienThoai CHAR(10)
);
```
Bảng hóa đơn :
```sql
CREATE TABLE HOADON (
    MaHD CHAR(6) PRIMARY KEY,
    MaKH CHAR(6),
    MaNV CHAR(6),
    NgayLapHD DATE,
    TongTien FLOAT,
    FOREIGN KEY (MaKH) REFERENCES KHACHHANG(MaKH),
    FOREIGN KEY (MaNV) REFERENCES NHANVIEN(MaNV)
);
```

Bảng hàng :
```sql
CREATE TABLE HANG (
    MaHang CHAR(6) PRIMARY KEY,
    TenHang NVARCHAR(50),
    DiaChi NVARCHAR(255)
);
```

Bảng sản phẩm :
```sql
CREATE TABLE SANPHAM (
    MaSP CHAR(10) PRIMARY KEY,
    TenSP NVARCHAR(255),
    DonViTinh NVARCHAR(10),
    GiaBan FLOAT,
    MaHang CHAR(6),
    FOREIGN KEY (MaHang) REFERENCES HANG(MaHang)
);
```

Bảng chi tiết hóa đơn :
```sql
CREATE TABLE CHITIETHD (
    MaHD CHAR(6),
    MaSP CHAR(10),
    SoLuongMua INT,
    GiamGia FLOAT,
    PRIMARY KEY (MaHD, MaSP),
    FOREIGN KEY (MaHD) REFERENCES HOADON(MaHD),
    FOREIGN KEY (MaSP) REFERENCES SANPHAM(MaSP)
);
```

Bảng chi nhập hàng  :
```sql
CREATE TABLE NHAPHANG (
    MaNH CHAR(6) PRIMARY KEY,
    SoLuongNhap INT,
    GiaNhap FLOAT,
    NgayNhap DATE,
    MaSP CHAR(10),
    FOREIGN KEY (MaSP) REFERENCES SANPHAM(MaSP)
);
```
sơ đồ liên kết thực thể :
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/91d444f9-928d-45ca-b716-dca443912310)

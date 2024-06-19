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

Quản lý thông tin sản phẩm : thêm , xóa , sửa thông tin

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
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/f9630abe-2662-483d-8c53-ab2dab9097e4)


Thêm dữ liệu cho các bảng :
```
--- Nhập giá trị cho bảng Nhân viên :
INSERT INTO NHANVIEN (MaNV, HoTenNV, GioiTinh, NgaySinh, DiaChi, DienThoai)
VALUES
('NV001', N'Trần Văn A', 'Nam', '1990-01-01', N'Hà Nội', '0123456789'),
('NV002', N'Nguyễn Thị B', 'Nữ', '1995-05-15', N'Hồ Chí Minh', '0987654321'),
('NV003', N'Phạm Văn C', 'Nam', '1985-12-31', N'Đà Nẵng', '0364869457'),
('NV004', N'Nguyễn Văn D', 'Nam', '1992-08-20', N'Hải Phòng', '0369871234'),
('NV005', N'Lê Thị E', 'Nữ', '1998-03-10', N'Bình Dương', '0912345678'),
('NV006', N'Phan Văn F', 'Nam', '1987-05-25', N'Cần Thơ', '0354689752'),
('NV007', N'Trần Thị G', 'Nữ', '1994-12-05', N'Hồ Chí Minh', '0987654321'),
('NV008', N'Huỳnh Văn H', 'Nam', '1991-10-15', N'Đà Nẵng', '0364869457'),
('NV009', N'Ngô Thị I', 'Nữ', '1989-07-03', N'Hà Nội', '0123456789'),
('NV010', N'Đặng Văn K', 'Nam', '1996-04-18', N'TP.HCM', '0364861122');

--- Nhập giá trị cho bảng khách hàng :
INSERT INTO KHACHHANG (MaKH, HoTenKH, DiaChi, DienThoai)
VALUES
('KH001', N'Lê Thị X', N'Hải Phòng', '0369874123'),
('KH002', N'Hoàng Văn Y', N'Bình Dương', '0912345678'),
('KH003', N'Vũ Thị Z', N'Cần Thơ', '0354689752'),
('KH004', N'Trần Văn L', N'Hà Nội', '0987654321'),
('KH005', N'Lê Thị M', N'Hồ Chí Minh', '0912345678'),
('KH006', N'Nguyễn Văn N', N'Đà Nẵng', '0364869457'),
('KH007', N'Phạm Thị O', N'Hải Phòng', '0369874123'),
('KH008', N'Huỳnh Văn P', N'Bình Dương', '0354689752'),
('KH009', N'Đỗ Thị Q', N'Cần Thơ', '0123456789'),
('KH010', N'Vũ Văn R', N'TP.HCM', '0364861122');

--- Nhập giá trị cho bảng hóa đơn :
INSERT INTO HOADON (MaHD, MaKH, MaNV, NgayLapHD, TongTien)
VALUES
('HD001', 'KH001', 'NV001', '2024-02-21', 50000000),
('HD002', 'KH002', 'NV002', '2024-03-22', 14500000),
('HD003', 'KH003', 'NV003', '2024-04-01',  2500000),
('HD004', 'KH004', 'NV004', '2024-06-20', 75000000),
('HD005', 'KH005', 'NV005', '2024-06-12', 38000000),
('HD006', 'KH006', 'NV006', '2024-07-26', 15000000),
('HD007', 'KH007', 'NV007', '2024-08-28', 22000000),
('HD008', 'KH008', 'NV008', '2024-09-27', 45000000),
('HD009', 'KH009', 'NV009', '2024-11-27', 3000000),
('HD010', 'KH010', 'NV010', '2024-12-28', 6000000);

--- Nhập giá trị cho bảng hàng :
INSERT INTO HANG (MaHang, TenHang, DiaChi)
VALUES
('H001', N'Hàng điện tử', N'Hà Nội'),
('H002', N'Hàng gia dụng', N'Hồ Chí Minh'),
('H003', N'Hàng thời trang', N'Đà Nẵng'),
('H004', N'Hàng gia dụng cao cấp', N'Hà Nội'),
('H005', N'Hàng điện máy', N'Hồ Chí Minh'),
('H006', N'Hàng mỹ phẩm', N'Đà Nẵng'),
('H007', N'Hàng tiêu dùng', N'Hải Phòng'),
('H008', N'Hàng gia dụng thông thường', N'Bình Dương'),
('H009', N'Hàng thể thao', N'Cần Thơ'),
('H010', N'Hàng gia dụng gia đình', N'TP.HCM');

--- Nhập giá trị cho sản phẩm :
INSERT INTO SANPHAM (MaSP, TenSP, DonViTinh, GiaBan, MaHang)
VALUES
('SP001', N'Điện thoại iPhone 12', N'Cái', 25000000, 'H001'),
('SP002', N'Tủ lạnh Panasonic', N'Cái', 15000000, 'H002'),
('SP003', N'Áo sơ mi nam', N'Cái', 500000, 'H003'),
('SP004', N'Máy tính bảng Samsung', N'Cái', 8000000, 'H004'),
('SP005', N'Máy giặt Electrolux', N'Cái', 10000000, 'H005'),
('SP006', N'Kem dưỡng da Olay', N'Cái', 300000, 'H006'),
('SP007', N'Bia Heineken lon', N'Lon', 25000, 'H007'),
('SP008', N'Laptop Dell', N'Cái', 18000000, 'H008'),
('SP009', N'Vợt cầu lông Yonex', N'Cái', 600000, 'H009'),
('SP010', N'Tủ lạnh Hitachi', N'Cái', 20000000, 'H010');

--- Nhập giá trị cho chi tiết hóa đơn :
INSERT INTO CHITIETHD (MaHD, MaSP, SoLuongMua, GiamGia)
VALUES
('HD001', 'SP001', 2, 0),
('HD002', 'SP002', 1, 500000),
('HD003', 'SP003', 5, 0),
('HD004', 'SP004', 3, 0),
('HD005', 'SP005', 2, 0),
('HD006', 'SP006', 4, 0),
('HD007', 'SP007', 50, 0),
('HD008', 'SP008', 1, 1000000),
('HD009', 'SP009', 3, 0),
('HD010', 'SP010', 2, 0);

--- Nhập giá trị cho chi tiết nhập hàng :
INSERT INTO NHAPHANG (MaNH, SoLuongNhap, GiaNhap, NgayNhap, MaSP)
VALUES
('NH001', 20, 100000, '2024-01-15', 'SP001'),
('NH002', 10, 500000, '2024-02-16', 'SP002'),
('NH003', 15, 800000, '2024-03-17', 'SP003'),
('NH004', 30, 600000, '2024-05-18', 'SP004'),
('NH005', 20, 900000, '2024-06-19', 'SP005'),
('NH006', 40, 400000, '2024-07-20', 'SP006'),
('NH007', 200, 18000, '2024-07-21', 'SP007'),
('NH008', 5, 15000000, '2024-08-22', 'SP008'),
('NH009', 10, 300000, '2024-10-23', 'SP009'),
('NH010', 3, 25000000, '2024-12-24', 'SP010');
```

# Tạo các chức năng
1. Tạo các thủ tục đối với Sản phẩm: Xử lý chức năng thêm , xóa , sửa thông tin
```sql
--- Thêm thông tin sản phẩm mới :
-- Tạo procedure để thêm mới một sản phẩm vào bảng SANPHAM
CREATE PROCEDURE pro_ThemSanPham
    @MaSP CHAR(10),          -- Tham số: Mã sản phẩm (kiểu CHAR(10))
    @TenSP NVARCHAR(255),    -- Tham số: Tên sản phẩm (kiểu NVARCHAR(255))
    @DonViTinh NVARCHAR(10), -- Tham số: Đơn vị tính của sản phẩm (kiểu NVARCHAR(10))
    @GiaBan FLOAT,           -- Tham số: Giá bán của sản phẩm (kiểu FLOAT)
    @MaHang CHAR(6)          -- Tham số: Mã hàng (kiểu CHAR(6)), liên kết với bảng HANG
AS
BEGIN
    -- Thực hiện lệnh INSERT để chèn dữ liệu mới vào bảng SANPHAM
    INSERT INTO SANPHAM (MaSP, TenSP, DonViTinh, GiaBan, MaHang)
    VALUES (@MaSP, @TenSP, @DonViTinh, @GiaBan, @MaHang);
END;

--- Sửa thông tin sản phẩm :
-- Tạo procedure để sửa thông tin của một sản phẩm trong bảng SANPHAM
CREATE PROCEDURE pro_SuaSanPham
    @MaSP CHAR(10),          -- Tham số: Mã sản phẩm cần sửa đổi thông tin (kiểu CHAR(10))
    @TenSP NVARCHAR(255),    -- Tham số: Tên sản phẩm mới (kiểu NVARCHAR(255))
    @DonViTinh NVARCHAR(10), -- Tham số: Đơn vị tính mới của sản phẩm (kiểu NVARCHAR(10))
    @GiaBan FLOAT,           -- Tham số: Giá bán mới của sản phẩm (kiểu FLOAT)
    @MaHang CHAR(6)          -- Tham số: Mã hàng mới (kiểu CHAR(6)), liên kết với bảng HANG
AS
BEGIN
    -- Thực hiện lệnh UPDATE để cập nhật thông tin sản phẩm trong bảng SANPHAM
    UPDATE SANPHAM
    SET TenSP = @TenSP,
        DonViTinh = @DonViTinh,
        GiaBan = @GiaBan,
        MaHang = @MaHang
    WHERE MaSP = @MaSP;
END;


--- Xóa sản phẩm :
-- Tạo procedure để xóa một sản phẩm khỏi bảng SANPHAM
CREATE PROCEDURE pro_XoaSanPham
    @MaSP CHAR(10) -- Tham số: Mã sản phẩm cần xóa (kiểu CHAR(10))
AS
BEGIN
    -- Thực hiện lệnh DELETE để xóa bản ghi của sản phẩm có mã MaSP khỏi bảng SANPHAM
    DELETE FROM SANPHAM
    WHERE MaSP = @MaSP;
END;

```
Kiểm tra với các thủ tục
```
--- Thêm sản phẩm :
EXEC pro_ThemSanPham 'SP011', N'Máy giặt LG', N'Cái', 12000000, 'H002';
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/072448fe-273c-4acc-818d-2ff325a97bcc)
```
--- Sửa sản phẩm :
EXEC pro_SuaSanPham 'SP011', N'Máy giặt Panasonic', N'Cái', 16000000, 'H002';
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/b00b9c27-336e-4cec-948c-44f928f69d92)

```
--- Xóa sản phẩm :
EXEC pro_XoaSanPham 'SP011';
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/bc23642f-0389-40fc-a5ab-37fec982adfd)

Quản lý các chức năng tính toán Giá nhập trong năm 2024 :
```sql
CREATE PROCEDURE TongGiaNhapNam2024
AS
BEGIN
    -- Bật NOCOUNT để không trả về số hàng bị ảnh hưởng bởi các lệnh DML
    SET NOCOUNT ON;

    -- Truy vấn tính tổng giá nhập cho từng tháng trong năm 2024
    SELECT 
        MONTH(NgayNhap) AS Thang,                   -- Lấy tháng từ trường NgayNhap
        SUM(SoLuongNhap * GiaNhap) AS TongGiaNhapThang  -- Tính tổng giá nhập cho từng tháng
    FROM NHAPHANG                                   -- Từ bảng NHAPHANG
    WHERE YEAR(NgayNhap) = 2024                      -- Chỉ lấy dữ liệu trong năm 2024
    GROUP BY MONTH(NgayNhap)                        -- Nhóm kết quả theo tháng
    ORDER BY Thang;                                 -- Sắp xếp theo thứ tự tháng

    -- Truy vấn tính tổng giá nhập của cả năm 2024
    SELECT 
        SUM(SoLuongNhap * GiaNhap) AS TongGiaNhapNam  -- Tính tổng giá nhập của cả năm
    FROM NHAPHANG                                   -- Từ bảng NHAPHANG
    WHERE YEAR(NgayNhap) = 2024;                     -- Chỉ lấy dữ liệu trong năm 2024
END;
```
Kiểm tra thủ tục :
```
EXEC TongGiaNhapNam2024;
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/33eed777-42ea-459b-8189-4a527fd96f92)

Quản lý các chức năng tính toán Doanh thu trong năm 2024 :
```sql
CREATE PROCEDURE DoanhThuNam2024
AS
BEGIN
    -- Bật NOCOUNT để không trả về số hàng bị ảnh hưởng bởi các lệnh DML
    SET NOCOUNT ON;

    -- Truy vấn tính doanh thu cho từng tháng trong năm 2024
    SELECT 
        MONTH(NgayLapHD) AS Thang,          -- Lấy tháng từ trường NgayLapHD
        SUM(TongTien) AS DoanhThuThang     -- Tính tổng doanh thu cho từng tháng
    FROM HOADON                            -- Từ bảng HOADON
    WHERE YEAR(NgayLapHD) = 2024           -- Chỉ lấy dữ liệu trong năm 2024
    GROUP BY MONTH(NgayLapHD)              -- Nhóm kết quả theo tháng
    ORDER BY Thang;                        -- Sắp xếp theo thứ tự tháng

    -- Truy vấn tính tổng doanh thu của cả năm 2024
    SELECT 
        SUM(TongTien) AS TongDoanhThuNam   -- Tính tổng doanh thu của cả năm
    FROM HOADON                            -- Từ bảng HOADON
    WHERE YEAR(NgayLapHD) = 2024;          -- Chỉ lấy dữ liệu trong năm 2024
END;

```
Kiểm tra thủ tục:
```
EXEC DoanhThuNam2024;
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/dc2203f1-145b-481e-85db-5f93f4ba2ca1)

Báo cáo Hóa đơn trong năm 2024
```sql
CREATE PROCEDURE BaoCaoHoaDonNam2024
AS
BEGIN
    -- Bật NOCOUNT để không trả về số hàng bị ảnh hưởng bởi các lệnh DML
    SET NOCOUNT ON;

    -- Truy vấn lấy các thông tin cần thiết từ bảng HOADON, KHACHHANG và NHANVIEN
    SELECT 
        MaHD AS 'Mã hóa đơn',         -- Chọn cột MaHD và đổi tên hiển thị là 'Mã hóa đơn'
        HoTenKH AS 'Tên khách hàng',  -- Chọn cột HoTenKH từ bảng KHACHHANG và đổi tên hiển thị
        HoTenNV AS 'Tên nhân viên',   -- Chọn cột HoTenNV từ bảng NHANVIEN và đổi tên hiển thị
        NgayLapHD AS 'Ngày lập hóa đơn',  -- Chọn cột NgayLapHD
        TongTien AS 'Tổng tiền'       -- Chọn cột TongTien
    FROM HOADON h                      -- Từ bảng HOADON và đặt tên bí danh là 'h'
    INNER JOIN KHACHHANG k ON h.MaKH = k.MaKH  -- Liên kết với bảng KHACHHANG bằng MaKH
    INNER JOIN NHANVIEN nv ON h.MaNV = nv.MaNV  -- Liên kết với bảng NHANVIEN bằng MaNV
    WHERE YEAR(NgayLapHD) = 2024      -- Chỉ lấy các hóa đơn trong năm 2024
    ORDER BY NgayLapHD;               -- Sắp xếp kết quả theo NgayLapHD (ngày lập hóa đơn)
END;
```
Kiểm tra thủ tục :
```
EXEC BaoCaoHoaDonNam2024;
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/5c71d5e0-32c9-459d-8688-031f4bf66e86)

Báo cáo Lượng hàng đã bán năm 2024 :
```sql
CREATE PROCEDURE BaoCaoLuongHangDaBanNam2024
AS
BEGIN
    -- Bật NOCOUNT để không trả về số hàng bị ảnh hưởng bởi các lệnh DML
    SET NOCOUNT ON;

    -- Báo cáo lượng hàng đã bán trong năm 2024
    SELECT 
        sp.MaSP AS 'Mã sản phẩm',           -- Chọn cột MaSP từ bảng SANPHAM và đổi tên hiển thị là 'Mã sản phẩm'
        sp.TenSP AS 'Tên sản phẩm',        -- Chọn cột TenSP từ bảng SANPHAM và đổi tên hiển thị là 'Tên sản phẩm'
        sp.DonViTinh AS 'Đơn vị tính',     -- Chọn cột DonViTinh từ bảng SANPHAM và đổi tên hiển thị là 'Đơn vị tính'
        SUM(ch.SoLuongMua) AS 'Số lượng đã bán',  -- Tính tổng số lượng đã mua từ bảng CHITIETHD và đổi tên hiển thị
        sp.GiaBan AS 'Giá bán',            -- Chọn cột GiaBan từ bảng SANPHAM và đổi tên hiển thị là 'Giá bán'
        SUM(ch.SoLuongMua * sp.GiaBan) AS 'Doanh thu'  -- Tính tổng doanh thu (số lượng đã mua * giá bán) và đổi tên hiển thị
    FROM CHITIETHD ch                      -- Từ bảng CHITIETHD và đặt tên bí danh là 'ch'
    INNER JOIN SANPHAM sp ON ch.MaSP = sp.MaSP  -- Liên kết với bảng SANPHAM qua cột MaSP
    INNER JOIN HOADON hd ON ch.MaHD = hd.MaHD  -- Liên kết với bảng HOADON qua cột MaHD
    WHERE YEAR(hd.NgayLapHD) = 2024         -- Chỉ lấy các hóa đơn trong năm 2024
    GROUP BY sp.MaSP, sp.TenSP, sp.DonViTinh, sp.GiaBan  -- Nhóm kết quả theo các cột trong SANPHAM để tính tổng
    ORDER BY sp.MaSP;                      -- Sắp xếp kết quả theo Mã sản phẩm từ bảng SANPHAM
END;

```
Kiểm tra thủ tục :
```
EXEC BaoCaoLuongHangDaBanNam2024;
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/58a521db-4a06-4436-9869-6c9438d4e9ae)

Báo cáo Mặt hàng bán chạy nhất :
```sql
CREATE PROCEDURE MatHangBanChayNhat
AS
BEGIN
    -- Bật NOCOUNT để không trả về số hàng bị ảnh hưởng bởi các lệnh DML
    SET NOCOUNT ON;

    -- Báo cáo mặt hàng bán chạy nhất trong năm 2024
    SELECT TOP 1
        sp.MaSP AS 'Mã sản phẩm',           -- Chọn cột MaSP từ bảng SANPHAM và đổi tên hiển thị là 'Mã sản phẩm'
        sp.TenSP AS 'Tên sản phẩm',        -- Chọn cột TenSP từ bảng SANPHAM và đổi tên hiển thị là 'Tên sản phẩm'
        sp.DonViTinh AS 'Đơn vị tính',     -- Chọn cột DonViTinh từ bảng SANPHAM và đổi tên hiển thị là 'Đơn vị tính'
        SUM(ch.SoLuongMua) AS 'Số lượng đã bán',  -- Tính tổng số lượng đã mua từ bảng CHITIETHD và đổi tên hiển thị
        sp.GiaBan AS 'Giá bán',            -- Chọn cột GiaBan từ bảng SANPHAM và đổi tên hiển thị là 'Giá bán'
        SUM(ch.SoLuongMua * sp.GiaBan) AS 'Doanh thu'  -- Tính tổng doanh thu (số lượng đã mua * giá bán) và đổi tên hiển thị
    FROM CHITIETHD ch                      -- Từ bảng CHITIETHD và đặt tên bí danh là 'ch'
    INNER JOIN SANPHAM sp ON ch.MaSP = sp.MaSP  -- Liên kết với bảng SANPHAM qua cột MaSP
    INNER JOIN HOADON hd ON ch.MaHD = hd.MaHD  -- Liên kết với bảng HOADON qua cột MaHD
    WHERE YEAR(hd.NgayLapHD) = 2024         -- Chỉ lấy các hóa đơn trong năm 2024
    GROUP BY sp.MaSP, sp.TenSP, sp.DonViTinh, sp.GiaBan  -- Nhóm kết quả theo các cột trong SANPHAM để tính tổng
    ORDER BY SUM(ch.SoLuongMua) DESC;       -- Sắp xếp kết quả theo tổng số lượng đã bán giảm dần và chỉ lấy top 1
END;
```
Kiểm tra thủ tục
```
EXEC MatHangBanChayNhat;
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/a52623d4-e38c-4ff9-a765-d332f3dfd880)

Trigger cập nhật hóa đơn
```sql
CREATE TRIGGER trg_UpdateTongTienHoaDon
ON CHITIETHD
AFTER INSERT, UPDATE, DELETE
AS
BEGIN
    -- Khai báo biến @MaHD để lưu mã hóa đơn
    DECLARE @MaHD CHAR(6);

    -- Kiểm tra nếu có dữ liệu được thêm vào (inserted)
    IF EXISTS (SELECT * FROM inserted)
        SELECT @MaHD = MaHD FROM inserted;  -- Lấy MaHD từ bảng inserted nếu có

    -- Nếu không có dữ liệu được thêm vào, có thể đang xảy ra lệnh UPDATE hoặc DELETE
    ELSE
        SELECT @MaHD = MaHD FROM deleted;   -- Lấy MaHD từ bảng deleted nếu không có trong inserted

    -- Cập nhật tổng tiền của hóa đơn trong bảng HOADON
    UPDATE HOADON
    SET TongTien = (
        -- Tính tổng tiền mới
        SELECT SUM(sp.GiaBan * ch.SoLuongMua * (1 - ch.GiamGia)) AS TongTien
        FROM CHITIETHD ch  -- Từ bảng CHITIETHD và đặt tên bí danh là 'ch'
        INNER JOIN SANPHAM sp ON ch.MaSP = sp.MaSP  -- Liên kết với bảng SANPHAM qua cột MaSP
        WHERE ch.MaHD = @MaHD  -- Điều kiện chỉ lấy dữ liệu cho hóa đơn có mã @MaHD
        GROUP BY ch.MaHD  -- Nhóm kết quả theo MaHD để tính tổng tổng tiền
    )
    WHERE MaHD = @MaHD;  -- Áp dụng cập nhật chỉ cho hóa đơn có mã @MaHD
END;

```
Kiểm tra trigger hoạt động:
```
-- Thêm một hóa đơn mới
INSERT INTO HOADON (MaHD, MaKH, MaNV, NgayLapHD, TongTien)
VALUES ('HD011', 'KH003', 'NV005', '2024-06-25', 3000000);
```
![image](https://github.com/Me-and-4-chairs/BTL-HQT/assets/168749315/4ca30703-66c6-4610-8c57-9e36357c4bad)

```
-- Thay đổi chi tiết hóa đơn (cập nhật số lượng mua)
UPDATE CHITIETHD
SET SoLuongMua = 6
WHERE MaHD = 'HD011' AND MaSP = 'SP003';
```

```
-- Xóa một hóa đơn
DELETE FROM HOADON WHERE MaHD = 'HD011';
```

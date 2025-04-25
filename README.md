# BÀI TẬP SỐ 06 - K225480106013 - LƯỜNG VĂN HẠNH - MÔN HỆ QUẢN TRỊ CƠ SỞ DỮ LIỆU
## DEADLINE: 23:59:59 NGÀY 25/4/2025
## Chủ đề: Câu lệnh Select
# ĐỀ BÀI
**Cho file sv_tnut.sql (1.6MB)**
1. Hãy nêu các bước để import được dữ liệu trong sv_tnut.sql vào sql server của em
2. dữ liệu đầu vào là tên của sv; sđt; ngày, tháng, năm sinh của sinh viên (của sv đang làm bài tập này)
3. nhập sql để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm với em?
4. nhập sql để tìm xem có những sv nào trùng ngày và tháng sinh với em?
5. nhập sql để tìm xem có những sv nào trùng tháng và năm sinh với em?
6. nhập sql để tìm xem có những sv nào trùng tên với em?
7. nhập sql để tìm xem có những sv nào trùng họ và tên đệm với em.
8. nhập sql để tìm xem có những sv nào có sđt sai khác chỉ 1 số so với sđt của em.
9. BẢNG SV CÓ HƠN 9000 ROWS, HÃY LIỆT KÊ TẤT CẢ CÁC SV NGÀNH KMT, SẮP XẾP THEO TÊN VÀ HỌ ĐỆM, KIỂU TIẾNG  VIỆT, GIẢI THÍCH.
10. HÃY NHẬP SQL ĐỂ LIỆT KÊ CÁC SV NỮ NGÀNH KMT CÓ TRONG BẢNG SV (TRÌNH BÀY QUÁ TRÌNH SUY NGHĨ VÀ GIẢI NHỮNG VỨNG MẮC)

# BÀI LÀM
1. Hãy nêu các bước để import được dữ liệu trong sv_tnut.sql vào sql server của em
- Tạo db tên SV_TNUT
- Rồi tạo bảng vào chèn dữ liệu
  <img width="960" alt="Screenshot_2" src="https://github.com/user-attachments/assets/378f5d9c-c60c-49bb-8a1d-b84a157c1038" />

3. nhập sql để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm với em?
   
   Code truy vấn:
   
   ```sql
    declare @ngaysinhcuaem date = '2002-04-20'	
    select * 
    from SV
    where ns = @ngaysinhcuaem
   ```
   
   ![Screenshot (24)](https://github.com/user-attachments/assets/9fb7dc6f-a4d4-4290-bd05-b444a4907171)

4. nhập sql để tìm xem có những sv nào trùng ngày và tháng sinh với em?
   
   Code truy vấn:
   
   ```sql
    declare @ngaysinhcuaem date = '2002-04-20'
    select * 
    from SV
    where day(ns) = day(@ngaysinhcuaem) and month(ns) = month(@ngaysinhcuaem)
   ```
   
   ![Screenshot (25)](https://github.com/user-attachments/assets/6e5be5e6-9726-4104-ab8b-936e28e7fa34)

5. nhập sql để tìm xem có những sv nào trùng tháng và năm sinh với em?
   
   Code truy vấn:
   
```sql
   
  declare @ngaysinhcuaem date = '2002-04-20'
  select * 
  from SV
  where year(ns) = year(@ngaysinhcuaem) and month(ns) = month(@ngaysinhcuaem)
  
```

   ![Screenshot (26)](https://github.com/user-attachments/assets/9b573222-3204-4dd1-b19e-820608e3c6b7)

6. nhập sql để tìm xem có những sv nào trùng tên với em?

Code truy vấn:

   ```sql

    declare @tencuaem nvarchar(10) = N'Hạnh'
    select * 
    from SV
    where ten = @tencuaem

   ```
   ![Screenshot (27)](https://github.com/user-attachments/assets/ffcafd57-150d-44c0-b028-093a1b4c9b3e)

7. nhập sql để tìm xem có những sv nào trùng họ và tên đệm với em.

   Code truy vấn:
   
   ```sql
   
    declare @hocuaem nvarchar(10) = N'Lường', @tendemcuaem nvarchar(20) = N'Văn'
    select * 
    from SV
    where hodem = @hocuaem + ' ' + @tendemcuaem
   
   ```
   
   ![Screenshot (28)](https://github.com/user-attachments/assets/6991aea9-4849-4dc9-afd9-1398bfbc49d7)

8. nhập sql để tìm xem có những sv nào có sđt sai khác chỉ 1 số so với sđt của em.

    Code truy vấn:
   
```sql
   
  DECLARE @sdtCuaEm NVARCHAR(20) = '969756211';
  SELECT *
  FROM SV
  WHERE LEN(sdt) = LEN(@sdtCuaEm)  -- Đảm bảo độ dài giống nhau
  AND sdt <> @sdtCuaEm	--sô đấy không phải là số của em
  AND (
      sdt LIKE '%' + SUBSTRING(@sdtCuaEm, 2, 8)  -- Thay thế chữ số đầu tiên
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 1) + '%' + SUBSTRING(@sdtCuaEm, 3, 7)  -- Thay thế chữ số thứ 2
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 2) + '%' + SUBSTRING(@sdtCuaEm, 4, 6)  -- Thay thế chữ số thứ 3
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 3) + '%' + SUBSTRING(@sdtCuaEm, 5, 5)  -- Thay thế chữ số thứ 4
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 4) + '%' + SUBSTRING(@sdtCuaEm, 6, 4)  -- Thay thế chữ số thứ 5
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 5) + '%' + SUBSTRING(@sdtCuaEm, 7, 3)  -- Thay thế chữ số thứ 6
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 6) + '%' + SUBSTRING(@sdtCuaEm, 8, 2)  -- Thay thế chữ số thứ 7
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 7) + '%' + SUBSTRING(@sdtCuaEm, 9, 1)  -- Thay thế chữ số thứ 8
      OR sdt LIKE SUBSTRING(@sdtCuaEm, 1, 8) + '%'  -- Thay thế chữ số thứ 9
    )
    
```

   ![Screenshot (29)](https://github.com/user-attachments/assets/4eab7d04-238b-42af-895b-d37fc7dffe0e)

9. BẢNG SV CÓ HƠN 9000 ROWS, HÃY LIỆT KÊ TẤT CẢ CÁC SV NGÀNH KMT, SẮP XẾP THEO TÊN VÀ HỌ ĐỆM, KIỂU TIẾNG  VIỆT, GIẢI THÍCH.

Code truy vấn:

```sql

    SELECT *
    FROM SV
    WHERE SUBSTRING(lop, 4, 3) = 'KTP' OR SUBSTRING(lop, 4, 3) = 'KMT'
    --Ban đầu theo logic chuẩn là lọc theo mã ngày cắt ra từ masv nhưng kết quả lại lẫn sv của ngành khác (hơi khó hiểu)
    --Tạm thời lọc theo tên lớp vì hiện tại chỉ có lớp kmt và ktp nên kết quả tìm kiếm là chính xác ở hiện tại.
    ORDER BY 
        ten COLLATE Vietnamese_CI_AS,
        hodem COLLATE Vietnamese_CI_AS;
```

   ![Screenshot (30)](https://github.com/user-attachments/assets/4ddc2513-2578-498f-a236-c0408d383b62)

10. HÃY NHẬP SQL ĐỂ LIỆT KÊ CÁC SV NỮ NGÀNH KMT CÓ TRONG BẢNG SV (TRÌNH BÀY QUÁ TRÌNH SUY NGHĨ VÀ GIẢI NHỮNG VỨNG MẮC)

    Code truy vấn:
    
   ```sql
    --Chọn lọc theo tên phổ biến và cả tên đệm để tăng tỉ lệ tìm kiếm.
    --Tuy nhiên sẽ không thể đảm bảo tất cả đều là giới tính nữ vì có nhiều tên lạ
    --Và cũng không thể đầy đủ 100% vì có con gái tên của con trai
    SELECT *
    FROM SV
    WHERE (SUBSTRING(lop, 4, 3) = 'KTP' OR SUBSTRING(lop, 4, 3) = 'KMT')
        AND (
            RIGHT(hodem, CHARINDEX(' ', REVERSE(hodem) + ' ') - 1) IN 
                ('Thị', 'Ngọc', 'Diệu', 'Thu', 'Mai', 'Hồng', 'Bích', 'Lan', 'Tuyết', 'Phương'
    			, 'Kim', 'Ánh', 'Trà', 'Cẩm', 'Tường', 'Mỹ', 'Tố', 'Lệ', 'Thùy', 'Vân',
    			'Quỳnh', 'Như', 'Nhật', 'Hạ', 'Đoan', 'Tâm')
            or ten IN 
                ('Lan', 'Hương', 'Dung', 'Hà', 'Yến', 'Thảo', 'Hằng', 'Trang', 'Nhung', 'Trang', 'Hiền',
    			'Oanh', 'Hạnh', 'Tâm', 'Vân', 'Ngân', 'Linh', 'Loan', 'Giang', 'Tuyền', 'Diễm',
    			'Vy', 'Trinh', 'Châu', 'Tiên', 'Nhi', 'Nương', 'Tươi', 'Huệ', 'Liên', 'Thủy',
    			'Hoa', 'My', 'Sen', 'Quyên', 'Thi', 'Ly', 'Thục', 'Thuý', 'Nguyệt', 'Ánh',
    			'Băng', 'Thanh', 'Mai', 'Hân', 'Đào', 'Bảo', 'Như', 'Quyến', 'Hạnh', 'Phương')
        )
    ORDER BY 
        ten COLLATE Vietnamese_CI_AS,
        hodem COLLATE Vietnamese_CI_AS;
   ```

   ![Screenshot (32)](https://github.com/user-attachments/assets/83661ad5-b094-454d-b65d-9d4a2e913153)

<img align="right" src="https://github.com/PhucHauDeveloper/Port-Windows-11-Xiaomi-Mi-Mix-2s/blob/b71fde07677d753897aa44eaec1914f54c57cede/guide/png/Xiaomi%20Mi%20Mix%202s%20Windows.png?raw=true" width="350" alt="Windows 11 Running On A Xiaomi Mi Mix 2s">


# Chạy Windows trên điện thoại Xiaomi Mi Mix 2s

## Hướng dẫn cài đặt

## Phân vùng lại điện thoại

### Yêu cầu bắt buộc

- Tải phiên bản mới nhất, trong đó có mọi thứ từ a đến z trong việc cài!

### Notes:
> **Warning** nếu bạn xóa bất kỳ phân vùng nào qua diskpart lác nữa hoặc bây giờ, windows sẽ gửi lệnh ufs lỗi và xóa tất cả ufs của bạn
- Tất cả dữ liệu của bạn sẽ bị xóa! Sao lưu ngay nếu cần.
- Các lệnh này đã được thử nghiệm.
- Bỏ qua cảnh báo `udevadm` nếu có
- Không tắm một dòng sông 2 lần cũng như chạy cùng một lệnh hai lần
- KHÔNG KHỞI ĐỘNG LẠI ĐIỆN THOẠI nếu bạn cho rằng mình đã toan, hãy yêu cầu trợ giúp từ tôi [Facebook Hậu](fb.com/ThaiHoangPhucHau/) hoặc [kmille36](https://github.com/kmille36)

####  Hãy chắc rằng bạn đã unlock bloatware, nếu không bạn không thể làm được

#### ⚠️ Chậm mà chắc, đừng chạy tất cả các lệnh cùng một lúc, hãy thực hiện chúng theo thứ tự!

##### ⚠️ ĐỪNG MẮC SAI LẦM!!! BẠN CÓ THỂ KHIẾN CỦA MÌNH TOAN BẰNG CÁC LỆNH BÊN DƯỚI NẾU LÀM SAI!!!

#### Đầu tiên giữ shift + click chuột phải vào thư mục, chọn "Open in Terminal" nếu không muốn lỗi trong flashboot

```cmd
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\18D1D00D0100" /v "osvc" /t REG_BINARY /d "0000" /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\18D1D00D0100" /v "SkipContainerIdQuery" /t REG_BINARY /d "01000000" /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\usbflags\18D1D00D0100" /v "SkipBOSDescriptorQuery" /t REG_BINARY /d "01000000" /f
```

##### Khởi động phục hồi TWRP thông qua PC bằng lệnh
```cmd
fastboot boot <twrp.img>
```

#### Ngắt kết nối tất cả các phân vùng
Chuyển đến cài đặt TWRP và ngắt kết nối tất cả các phân vùng

#### Bắt đầu lệnh ADB
```cmd
adb shell
```

#### Thay đổi kích thước cây phân vùng
> Chuyển parted sang thư mục sbin
```sh
cp /sdcard/parted /sbin/ && chmod 755 /sbin/parted
```

> Ngắt kết nối data và sdcard
```sh
umount /data && umount /sdcard
```
#### Chạy parted
```sh
parted /dev/block/sda
```


#### Xóa phân vùng `userdata`
> Bạn có thể đảm bảo rằng 21 là số phân vùng userdata bằng cách chạy
>  `print all`
```sh
rm 21
```

#### Tạo phân vùng
> Nếu bạn nhận được bất kỳ thông báo cảnh báo nào yêu cầu bạn bỏ qua hoặc hủy, chỉ cần nhập i và nhấn enter



<details>
<summary><b><strong>Dành cho máy 64GB</strong></b></summary>

  
  - Tạo phân vùng ESP (lưu trữ bộ tải khởi động Windows và tệp EFI)
```sh
mkpart esp fat32 6559MB 7000MB
```

- Tạo phân vùng chính nơi Windows sẽ được cài đặt
```sh
mkpart win ntfs 7000MB 40GB
```
  
- Tạo phân vùng dữ liệu của Android
```sh
mkpart userdata ext4 40GB 59.1GB
```

  </summary>
</details>


<details>
<summary><b><strong>Dành cho máy 128GB</strong></b></summary>


  - Tạo phân vùng ESP (lưu trữ bộ tải khởi động Windows và tệp EFI)
```sh
mkpart esp fat32 6559MB 7000MB
```

- Tạo phân vùng chính nơi Windows sẽ được cài đặt
```sh
mkpart win ntfs 7000MB 100GB
```
  
- Tạo phân vùng dữ liệu của Android
```sh
mkpart userdata ext4 100GB 123GB
```

  </summary>
</details>


<details>
<summary><b><strong>Dành cho máy 256GB</strong></b></summary>

  
  - Tạo phân vùng ESP (lưu trữ bộ tải khởi động Windows và tệp EFI)
```sh
mkpart esp fat32 6559MB 7000MB
```

- Tạo phân vùng chính nơi Windows sẽ được cài đặt
```sh
mkpart win ntfs 7000MB 220GB
```
  
- Tạo phân vùng dữ liệu của Android
```sh
mkpart userdata ext4 220GB 251GB
```

  </summary>
</details>

#### Kích hoạt phân vùng khởi động ESP để EFI có thể phát hiện ra nó
```sh
set 21 esp on
```

#### Thoát parted
```sh
quit
```

#### Khởi động vào TWRP

#### Khởi động lại ADB trên PC của bạn
```cmd
adb shell
```

#### Định dạng phân vùng
Lưu ý NHẤT ĐỊNH PHẢI ĐẶT TÊN PHẦN VÙNG NHƯ TÔI HOẶC MÁY BẠN SẼ SOFT BRICK!!!
-  Định dạng phân vùng
```sh
mkfs.fat -F32 -s1 /dev/block/by-name/esp
```

-  Định dạng phân vùng Windows thành NTFS
```sh
mkfs.ntfs -f /dev/block/by-name/win
```

- Định dạng phân vùng userdata
```sh
mke2fs -t ext4 /dev/block/by-name/userdata
```
Hoặc vào menu Wipe(twrp) và nhấn Format Data, sau đó nhấn `yes`.

#### Kiểm tra xem Android có còn khởi động không
Chỉ cần khởi động lại điện thoại và xem Android có còn hoạt động không, không thì bạn toan rồi đấy :))


## [Bước tiếp theo: Cài đặt Windows](/guide/Vietnam/install.md)

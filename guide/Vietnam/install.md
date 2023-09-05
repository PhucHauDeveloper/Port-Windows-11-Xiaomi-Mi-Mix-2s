<img align="right" src="https://github.com/PhucHauDeveloper/Port-Windows-11-Xiaomi-Mi-Mix-2s/blob/b71fde07677d753897aa44eaec1914f54c57cede/guide/png/Xiaomi%20Mi%20Mix%202s%20Windows.png?raw=true" width="350" alt="Windows 11 Running On A Xiaomi Mi Mix 2s">

# Chạy Windows trên điện thoại Xiaomi Mi Mix 2s

## Cài đặt

## Cài đặt Windows
> Cần não

### Yêu cầu bắt buộc

- Đã có trong file, bạn không cần bất cứ thứ gì nữa cả




#### Khởi động lại vào TWRP
#Khởi động adb
```
adb shell
```
# Chép parted vào điện thoại
```
cp /sdcard/parted /sbin/ && chmod 755 /sbin/parted
umount /data && umount /sdcard
```
# Chạy parted
```
parted /dev/block/sda
```

### Gán tên phân vùng
  

#### Khởi động Windows disk manager

> Chạy lệnh sau để vào diskpart

```cmd
diskpart
```


### Gán `X` cho phân vùng Windows

#### Chọn phân vùng của Windows
> Sử dụng `list volume` để tìm, nó tên là "WIN"

```diskpart
select volume <number>
```

#### Gán tên phân vùng win thành 'X'
```diskpart
assign letter=x
```

### Gán tên phân vùng esp thành `Y`

#### Select the ESP volume of the phone
> Sử dụng `list volume` để tìm, nó tên là "ESP"

```diskpart
select volume <number>
```

#### Gán tên thành Y

```diskpart
assign letter=y
```

#### Thoát diskpart
```diskpart
exit
```

  
  

### Cài đặt

#### Cài đặt Windows arm
Đầu tiên mở DISM++, nhấn Ctrl + N, chọn Browse thứ nhất chọn tới file Windows Arm( có đuôi .ESD, .WIN, .ISO, .SWM) của bạn
Browse thứ 2 hãy chọn ổ X(ổ Windows của điện thoại bạn), chọn Format, chọn Target (nếu thích), nhân ok để bắt đầu, đừng đụng vào cáp, hãy pha tách cafe và chờ nó vì nó rất chậm

### Cài đặt Drivers
Nên cài driver bằng DIMP++, sau bước trên, chọn X:\ trong DIMP, chọn Open session, chọn Driver, chọn Add, mở tới folder driver, nó sẽ tự cài cho bạn.

### Tạo tệp Windows bootloader vào EFI

```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

## Che phép driver chưa kí

> Nếu bạn bỏ qua, bạn sẽ bị BSOD và bắt buộc phải thực hiện cài lại windows

```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set {default} testsigning on
```

## Boot vào Windows

### Copy `<uefi.img>` vào điện thoại của bạn

```cmd
adb push <uefi.img> /sdcard
```

### Thêm bản sao lưu cho Android boot image của bạn
> Sử dụng TWRP, sao lưu boot

### Cài uefi image bằng TWRP
Chọn tới file `uefi.img` và flash nó vào boot

## Khởi động về Android
> Sử dụng boot Android đã backup

## Hoàn thành!

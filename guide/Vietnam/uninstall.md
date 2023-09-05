<img align="right" src="https://github.com/PhucHauDeveloper/Port-Windows-11-Xiaomi-Mi-Mix-2s/blob/b71fde07677d753897aa44eaec1914f54c57cede/guide/png/Xiaomi%20Mi%20Mix%202s%20Windows.png?raw=true" width="350" alt="Windows 11 Running On A Xiaomi Mi Mix 2s">


# Chạy Windows trên điện thoại Xiaomi Mi Mix 2s

## Gỡ cài đặt

### Why is this needed?

Nếu bạn đã làm theo hướng dẫn cũ, thứ tự phân vùng của bạn sẽ quá khác và có thể gây ra một số hậu quả nếu bạn không khôi phục bảng phân vùng gốc của mình.

Nếu bạn muốn gỡ cài đặt windows, cách này được sử dụng thay vì xóa phân vùng theo cách thủ công để tránh lỗi của con người + viết toàn bộ hướng dẫn dành riêng cho việc gỡ cài đặt.

Nếu bạn muốn khóa lại bộ nạp khởi động, bạn sẽ cần có bảng phân vùng trong kho.

### Bắt buộc có

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

### Hãy làm tới bước thay đổi kích thước cây phân vùng
Thay vì theo cây tôi ghi, hãy làm theo cái này
#### Xóa phân vùng `userdata` và windows, esp
> Bạn có thể đảm bảo rằng 21 22 23 là số phân vùng userdata và windows, esp bằng cách chạy
>  `print all`
```sh
rm 21
rm 22
rm 23
```

#### Tạo lại phân vùng

<details>
<summary><b><strong>Dành cho máy 64GB</strong></b></summary>

- Tạo phân vùng dữ liệu của Android
```sh
mkpart userdata ext4 6559MB 59.1GB
```

  </summary>
</details>


<details>
<summary><b><strong>Dành cho máy 128GB</strong></b></summary>

- Tạo phân vùng dữ liệu của Android
```sh
mkpart userdata ext4 6559MB 123GB
```

  </summary>
</details>


<details>
<summary><b><strong>Dành cho máy 256GB</strong></b></summary>

- Tạo phân vùng dữ liệu của Android
```sh
mkpart userdata ext4 6559MB 251GB
```

  </summary>
</details>

### Dọn sạch phân vùng userdata
```cmd
fastboot -w
```

Sau khi làm, bạn nên flash lại Miui rom bằng Xiaomi Flash để trách các lỗi không cần thiết có thể xảy ra



# Báo cáo Bài 3: Viết Dockerfile 3 dòng đóng gói trang Web HTML tĩnh

## 1. Mục tiêu
- Viết tệp `Dockerfile` tối giản để tự đóng gói trang web HTML tĩnh vào Docker Image.
- Xây dựng image tùy biến `my-html-app:v1` dựa trên nền image `nginx:alpine`.
- Khởi chạy container từ image vừa tạo trên cổng 8081 và kiểm tra nội dung phản hồi bằng `curl`.

## 2. Cấu trúc mã nguồn

Thư mục bài làm bao gồm:
```text
.
├── Dockerfile
├── index.html
└── README.md
```

### Nội dung `index.html`:
```html
<h1>Hello Docker Session 09!</h1>
```

### Nội dung `Dockerfile`:
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

---

## 3. Các bước thực hiện và lệnh đã sử dụng

### Bước 1: Build Docker Image
Xây dựng Docker Image với thẻ tên (tag) là `my-html-app:v1`:
```bash
docker build -t my-html-app:v1 .
```

### Bước 2: Khởi chạy container từ Image vừa build
Khởi chạy container chạy ngầm (`-d`), đặt tên là `html-app`, ánh xạ cổng `8081:80`:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

### Bước 3: Kiểm tra nội dung trang web bằng `curl`
```bash
curl http://localhost:8081
```

### Bước 4: Dọn dẹp container sau khi hoàn tất
```bash
docker stop html-app && docker rm html-app
```

---

## 4. Nhật ký kết quả đầu ra thực tế từ Terminal

### 4.1. Kết quả lệnh `docker build -t my-html-app:v1 .`
```text
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 104B done
#1 DONE 0.1s

#2 [internal] load metadata for docker.io/library/nginx:alpine
#2 DONE 0.1s

#3 [internal] load .dockerignore
#3 transferring context: 2B done
#3 DONE 0.1s

#4 [1/2] FROM docker.io/library/nginx:alpine@sha256:df221db836e1754089190208cee7eeda94f233197056426eda74a43ab1abeac2
#4 resolve docker.io/library/nginx:alpine@sha256:df221db836e1754089190208cee7eeda94f233197056426eda74a43ab1abeac2 0.1s done
#4 DONE 0.4s

#5 [internal] load build context
#5 transferring context: 71B done
#5 DONE 0.1s

#6 [2/2] COPY index.html /usr/share/nginx/html/index.html
#6 DONE 0.1s

#7 exporting to image
#7 exporting layers 0.3s done
#7 exporting manifest sha256:a7873d6203ab6047760d291d848bb3bd50cf9180cfd9059cab301e57c01e24fb 0.0s done
#7 exporting config sha256:3862df755ef9b03807e7973e0df0acddefb207c0a36b7553bd9ef1a2337ed6c1 0.1s done
#7 exporting attestation manifest sha256:8d045d301b2533a03444a4242d9cab6c81bccd65bcd3aab0f8e029bde943ad9f 0.0s done
#7 exporting manifest list sha256:da6cc12df999c55a731d26054914be04ded0400ef4435199b2d5786c5e9d7cfd 0.0s done
#7 naming to docker.io/library/my-html-app:v1 done
#7 unpacking to docker.io/library/my-html-app:v1 0.1s done
#7 DONE 0.7s
```

### 4.2. Kết quả khởi chạy container và kiểm tra `curl`
```text
bf38e2741b97d5d92100e45de16bc0ff817aceb93c4031312f8cb8407dc8d305
<h1>Hello Docker Session 09!</h1>
```

---

## 5. Phân tích các chỉ thị trong Dockerfile

- `FROM nginx:alpine`: Chỉ định base image cho container. Ở đây sử dụng image `nginx:alpine` nhỏ gọn đã cài đặt sẵn web server Nginx.
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép file `index.html` từ thư mục build context của máy host vào thư mục web root mặc định của Nginx trong container (`/usr/share/nginx/html/index.html`), ghi đè trang chào mừng mặc định.

---

## 6. Hướng dẫn chụp ảnh minh chứng & Placeholder
1. Chạy lệnh:
   ```bash
   docker build -t my-html-app:v1 .
   docker run -d -p 8081:80 --name html-app my-html-app:v1
   curl http://localhost:8081
   ```
2. Chụp ảnh màn hình hiển thị quá trình build thành công và lệnh `curl` trả về `<h1>Hello Docker Session 09!</h1>`.
3. Dán ảnh vào vị trí placeholder bên dưới:

`ImgEx`

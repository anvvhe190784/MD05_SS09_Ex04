# Bài tập 4: Đẩy Docker Image lên Docker Hub thông qua GitLab CI (DinD)

## 1. Cấu trúc Pipeline ([`.gitlab-ci.yml`](./.gitlab-ci.yml))
- Mở rộng từ Bài 3 (`test` $\rightarrow$ `build` $\rightarrow$ `dockerize`).
- Stage `dockerize` (`dockerize_job`) nhận artifact `build/libs/*.jar` từ `build_job`, sử dụng `docker:24.0` + service `docker:24.0-dind` (Docker-in-Docker), đăng nhập bằng biến bảo mật `$DOCKER_USERNAME` và `$DOCKER_PASSWORD`, build từ [`Dockerfile`](./Dockerfile) và push lên Docker Hub (`$DOCKER_USERNAME/hr-service:$CI_COMMIT_SHORT_SHA` và `:latest`).

## 2. Hướng dẫn thiết lập CI/CD Variables trên GitLab để chụp ảnh nộp bài
1. Tạo repository trống tên `hr-service` trên Docker Hub (https://hub.docker.com/repository/create).
2. Trên GitLab Project, vào **Settings $\rightarrow$ CI/CD $\rightarrow$ Variables $\rightarrow$ Add variable**:
   - `DOCKER_USERNAME`: Tên tài khoản Docker Hub của bạn.
   - `DOCKER_PASSWORD`: Docker Hub Access Token (tích chọn **Mask variable** để ẩn token trong log CI).
3. Chụp ảnh màn hình danh sách `DOCKER_USERNAME` & `DOCKER_PASSWORD` trong mục Variables của GitLab và gửi kèm link Docker Hub Repository `https://hub.docker.com/r/<dockerhub_username>/hr-service`.

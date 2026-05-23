# Reliability Checklist — FIT4110 Lab 03

**Nhóm:** team-iot (Nhóm 8)  
**Service:** IoT Ingestion  
**Ngày hoàn thành:** 2026-05-23

## 1. Functional tests

- [x] Có test cho endpoint health.
- [x] Có test happy path cho endpoint chính (`POST /readings`).
- [x] Có kiểm tra status code 2xx.
- [x] Có kiểm tra field quan trọng trong response (`reading_id`, `accepted`, `items`).
- [x] Có ít nhất 1 test đọc dữ liệu danh sách (`GET /readings/latest`).

## 2. Auth tests

- [x] Có test thiếu token → 401.
- [x] Có test sai token (ghi chú: Prism mock có thể chấp nhận token sai khi có header Bearer).
- [x] Endpoint public (`/health`) khai báo `security: []` trong contract.
- [x] Test thể hiện expected status 401/403 cho thiếu token.

## 3. Negative tests

- [x] Có test thiếu field bắt buộc (`device_id`).
- [x] Có test sai enum (`metric=pressure`).
- [x] Có test sai query (`limit=200` vượt max 100).
- [x] Lỗi trả về theo ProblemDetails (`status`, `title`, `detail`).

## 4. Boundary tests

- [x] Có test min/max nhiệt độ (-40, 80, 81).
- [x] Có test limit/pagination (`limit=5`, `limit=200`).
- [x] Có test payload sát ngưỡng schema.
- [x] Ghi chú: mock chấp nhận 80°C; service thật có thể trả `X-Warning`.

## 5. Reliability tests cơ bản

- [x] Có kiểm tra response time (folder `06_Local_only`, chỉ chạy khi `env=local`).
- [x] SLA mục tiêu: health < 1000ms trên local.
- [x] Contract định nghĩa 429; test rate limit dùng `Prefer: code=429` trên mock.
- [x] Consumer-side smoke: `GET/POST` AI Vision mock tại `{{aiVisionMockUrl}}`.

## 6. Evidence

- [x] Collection export JSON: `postman/collections/FIT4110_lab03_iot_ingestion.postman_collection.json`
- [x] Environment mock: `postman/environments/FIT4110_lab03_mock.postman_environment.json`
- [x] Environment local: `postman/environments/FIT4110_lab03_local.postman_environment.json`
- [x] Newman report: `reports/newman-report.xml`, `reports/newman-report.html`
- [x] Test-case matrix: `templates/test-case-matrix.csv`
- [x] Handshake: `templates/consumer-provider-handshake.md`
- [x] Contract lint: `reports/contract-lint-report.txt` (0 errors)

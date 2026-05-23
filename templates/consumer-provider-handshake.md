# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 2026-05-23
- Provider team: team-vision (AI Vision)
- Consumer team: team-iot (Nhóm 8 — IoT Ingestion)
- Provider service: AI Vision API
- Consumer service: IoT Ingestion (gọi vision khi cần phân tích ảnh từ gateway)

## Contract

- Contract file: `contracts/ai-vision.openapi.yaml`
- Mock base URL: `http://localhost:4011` (biến `{{aiVisionMockUrl}}`)
- Auth method: Bearer JWT (`Authorization: Bearer {{authToken}}`)
- Endpoint được test: `GET /health`, `POST /detect`

## Smoke test

### Request

```http
POST /detect HTTP/1.1
Host: localhost:4011
Authorization: Bearer lab-token
Content-Type: application/json
```

```json
{
  "camera_id": "CAM01",
  "image_url": "https://example.com/frame.jpg"
}
```

### Expected response

```json
{
  "detection_id": "DET001",
  "camera_id": "CAM01",
  "label": "person",
  "confidence": 0.91,
  "risk_level": "medium"
}
```

## Kết quả

- [x] Consumer gọi mock thành công (Newman folder `05_Consumer_side_Smoke`).
- [x] Consumer parse được `detection_id`, `label`, `confidence`, `risk_level`.
- [x] Consumer hiểu lỗi 4xx (contract có `ProblemDetails` cho 400/401).
- [x] Có Newman report: `reports/newman-report.xml`, `reports/newman-report.html`.

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---|---|---|---|
| Không có thay đổi trong Lab 03 | Dùng contract mẫu Lab 03 | Giữ nguyên | team-iot + team-vision |

## Xác nhận

- Provider representative: team-vision (contract `ai-vision.openapi.yaml`)
- Consumer representative: team-iot — Nhóm 8

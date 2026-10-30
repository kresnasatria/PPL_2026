# Panduan Integrasi Modul M9 (Penerimaan Barang Penuh)

## 1. Tujuan Integrasi
Menyediakan mekanisme komunikasi asinkron antara Modul M11 (GRN) dan Modul M9. Saat Modul M11 selesai mencatat penerimaan barang (PO = disetujui), Modul M11 akan meneruskan data tersebut agar Modul M9 dapat memproses pencatatan aset.

## 2. Mekanisme Komunikasi (Standar Event Antarmodul)
Sistem menggunakan pendekatan **Webhook (HTTP POST)** sesuai Panduan API Bersama.
*   **Endpoint Tujuan M9:** `POST /api/m9/v1/events`
*   **Autentikasi (Header):** `X-Service-Key: <kunci modul M11>`

## 3. Struktur Payload Webhook (Event)
Modul M11 akan mengirimkan JSON dengan standar event Araya Hub berikut:

```json
{
  "event_id": "6f1c2b9e-0d4a-4f7b-9a51-1e2c3d4f5a6b",
  "event_type": "purchase_order.received",
  "source_module": "M11",
  "occurred_at": "2026-10-27T14:30:00+07:00",
  "recipient_role": null,
  "payload": {
    "purchase_order_id": 125,
    "status": "diterima",
    "received_at": "2026-10-27T14:30:00+07:00",
    "received_by": 42,
    "items": [
      {
        "product_id": 31,
        "qty_received": 50
      }
    ],
    "total_amount": 750000000
  }
}
# Panduan Integrasi Modul M9 (Penerimaan Barang Penuh)

## 1. Tujuan Integrasi
Menyediakan mekanisme komunikasi asinkron antara Modul M11 (GRN) dan Modul M9. Saat Modul M11 selesai mencatat penerimaan barang (PO = disetujui), Modul M11 akan meneruskan data tersebut agar Modul M9 dapat memproses pencatatan aset atau pergerakan inventaris.

## 2. Mekanisme Komunikasi
Sistem menggunakan pendekatan **Webhook (HTTP POST)**. Modul M11 bertindak sebagai *Publisher* (pengirim event), dan Modul M9 bertindak sebagai *Subscriber* (penerima event).
Endpoint webhook pada Modul M9 adalah `POST /api/v1/webhooks/goods-received`.

## 3. Struktur Payload Webhook
Modul M9 harus menyediakan endpoint yang mampu mengurai struktur JSON berikut:

```json
{
  "event": "goods_received",
  "timestamp": "2026-10-27T14:30:00+07:00",
  "data": {
    "purchase_order_id": "PO-001",
    "status": "received",
    "received_at": "2026-10-27T14:30:00+07:00",
    "received_by": "admin-001",
    "items": [
      {
        "id": "item-001",
        "name": "Laptop Dell Latitude 5540",
        "quantity_ordered": 50,
        "quantity_received": 50
      }
    ],
    "total_amount": 750000000
  }
}
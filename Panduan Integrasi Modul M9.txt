# Panduan Integrasi Modul M9 (Penerimaan Barang Penuh)

## 1. Tujuan Integrasi
Menyediakan mekanisme komunikasi asinkron antara Modul M11 (GRN) dan Modul M9. Saat Modul M11 selesai mencatat penerimaan barang (PO = disetujui), Modul M11 akan meneruskan data tersebut agar Modul M9 dapat memproses pencatatan aset atau pergerakan inventaris.

## 2. Mekanisme Komunikasi
Sistem menggunakan pendekatan **Webhook (HTTP POST)**. Modul M11 bertindak sebagai *Publisher* (pengirim event), dan Modul M9 bertindak sebagai *Subscriber* (penerima event)[cite: 35].

## 3. Struktur Payload Webhook
Modul M9 harus menyediakan endpoint yang mampu mengurai struktur JSON berikut[cite: 35]:

```json
{
  "event": "grn.received.full",
  "timestamp": "2026-10-24T22:56:00Z",
  "data": {
    "grn_id": "GRN-001",
    "po_id": "PO-2026-10-001",
    "supplier_id": "SUP-992",
    "status_penerimaan": "diterima",
    "items": [
      {
        "item_id": "ITM-001",
        "quantity_received": 50
      }
    ]
  }
}
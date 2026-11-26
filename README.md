# PintuSender Public API

Dokumentasi integrasi **PintuSender Public API** untuk mengirim pesan WhatsApp dari website atau aplikasi.

## Dokumentasi online

- [Postman API Documentation](https://documenter.getpostman.com/view/28290686/2sBYPv4skc)

## Base URL

`https://sender.pintu.web.id/api/v1`

## Autentikasi

Semua endpoint pada bagian Public API memerlukan API Key melalui Bearer Token:

```http
Authorization: Bearer ps_live_YOUR_API_KEY
```

API Key menggunakan prefix `ps_live_`. Simpan API Key di sisi server. Jangan menaruh API Key di kode frontend atau membagikannya kepada pihak yang tidak berwenang.

Akses API memerlukan API Key valid dan tenant dengan trial atau langganan aktif.

## Endpoint

| Method | Endpoint | Fungsi |
|---|---|---|
| POST | `/public/messages/send` | Mengirim pesan teks |
| POST | `/public/messages/send-image` | Mengirim gambar melalui upload |
| POST | `/public/messages/send-image-url` | Mengirim gambar melalui URL |
| POST | `/public/messages/send-document` | Mengirim dokumen PDF melalui upload |

Spesifikasi OpenAPI tersedia pada [openapi.yaml](./openapi.yaml).

## Format penerima

Parameter `to` dapat berisi:
- Nomor WhatsApp format internasional, angka saja tanpa tanda `+`, 8–15 digit. Contoh: `6281234567890`.
- JID grup WhatsApp yang telah disinkronkan dan berakhiran `@g.us`.

## Ketentuan file

- Gambar: JPEG, PNG, atau GIF, maksimal 5 MB.
- Dokumen: PDF valid, maksimal 5 MB.
- Upload menggunakan `multipart/form-data`. Biarkan HTTP client membuat header Content-Type dan boundary secara otomatis.

## Kode respons umum

| HTTP | Keterangan |
|---|---|
| 200 | Request berhasil diproses |
| 400 | Request atau parameter tidak valid |
| 401 | API Key tidak ada atau tidak valid |
| 403 | Akses ditolak, misalnya status trial/langganan atau kuota |
| 423 | Pengiriman dijeda (`SENDING_PAUSED`) |
| 502 | Kegagalan saat pengiriman melalui WhatsApp |

## Catatan

Status Pause akan menghentikan seluruh pengiriman outbound tenant sampai Resume dilakukan.

Untuk contoh request dan response, kunjungi [PintuSender Public API di Postman](https://documenter.getpostman.com/view/28290686/2sBYPv4skc).

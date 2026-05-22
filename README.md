# SOAR Automation with n8n

Project ini adalah automation sederhana untuk membantu SOC analyst melakukan pengecekan awal terhadap alert keamanan secara otomatis.

Workflow ini dibuat menggunakan n8n untuk mengecek reputasi IP address, hash file, dan URL phishing. Hasil pengecekan akan dikirim otomatis ke Telegram agar analyst tidak perlu melakukan pengecekan manual satu per satu.

---

## Workflow

Project ini memiliki 3 workflow utama:

1. Network Investigation  
   Mengecek reputasi IP address menggunakan AbuseIPDB atau VirusTotal.

2. File Forensics  
   Mengecek hash file untuk mengetahui apakah file terdeteksi sebagai malware menggunakan VirusTotal.

3. Phishing Triage  
   Menganalisis URL yang dicurigai phishing menggunakan URLScan.io dan mengirim hasilnya ke Telegram.

---

## Tools

Tools yang digunakan:

- n8n
- VirusTotal API
- AbuseIPDB API
- URLScan.io API
- Telegram Bot
- Postman

---

## Credentials

API key dan token tidak disimpan di GitHub.

Semua credential dimasukkan langsung melalui n8n Credentials atau pada HTTP Request node.

Credential yang dibutuhkan:

- VirusTotal API Key
- AbuseIPDB API Key
- URLScan.io API Key
- Telegram Bot Token
- Telegram Chat ID

---

## Network Investigation

Workflow ini digunakan untuk mengecek reputasi IP address.

Contoh input webhook:

    {
      "ip": "103.x.x.x"
    }

Hasil yang dikirim ke Telegram:

- IP Address
- Negara asal
- Risk score
- Status reputasi IP

Screenshot terkait:

- screenshots/01-network-workflow.png
- screenshots/01-network-webhook-test.png
- screenshots/01-network-telegram-output.png

---

## File Forensics

Workflow ini digunakan untuk mengecek hash file dan mengetahui apakah file tersebut terdeteksi sebagai malware.

Contoh input webhook:

    {
      "hash": "44d88612fea8a8f36de82e1278abb02f"
    }

Hasil yang dikirim ke Telegram:

- Hash file
- Nama file
- Jenis malware
- Jumlah deteksi
- Status file

Screenshot terkait:

- screenshots/02-file-workflow.png
- screenshots/02-file-webhook-test.png
- screenshots/02-file-telegram-output.png

---

## Phishing Triage

Workflow ini digunakan untuk menganalisis URL yang dicurigai sebagai phishing.

Contoh input webhook:

    {
      "url": "http://example.com"
    }

Hasil yang dikirim ke Telegram:

- URL
- Status malicious atau clean
- Verdict hasil scan
- Screenshot tampilan website

Screenshot terkait:

- screenshots/03-phishing-workflow.png
- screenshots/03-phishing-webhook-test.png
- screenshots/03-phishing-urlscan-result.png
- screenshots/03-phishing-telegram-output.png

---

## Cara Menjalankan

1. Buka n8n.
2. Import file workflow dari folder workflows.
3. Masukkan API key dan token pada credential n8n.
4. Aktifkan workflow.
5. Test webhook menggunakan Postman.
6. Cek hasil notifikasi di Telegram.

---

## Testing

Testing dilakukan dengan mengirim request POST ke webhook n8n menggunakan Postman.

Workflow dianggap berhasil jika:

- Webhook menerima input.
- API mengembalikan hasil enrichment.
- Workflow berjalan tanpa error.
- Telegram menerima notifikasi sesuai output yang diminta.

---

## Notes

Project ini hanya berfokus pada automation triage dan enrichment dasar.

Project ini belum melakukan response otomatis seperti block IP, isolate endpoint, atau integrasi dengan SIEM/EDR.
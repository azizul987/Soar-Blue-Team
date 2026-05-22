# SOAR Automation with n8n

Project ini membuat workflow SOAR sederhana untuk membantu SOC analyst melakukan triage dan enrichment alert keamanan secara otomatis.

## Workflow
1. Network Investigation - Cek reputasi IP address.
2. File Forensics - Cek hash malware.
3. Phishing Triage - Analisa URL dan screenshot website.

## Tools
- n8n
- VirusTotal API
- AbuseIPDB API
- URLScan.io API
- Telegram Bot
# Credentials Required

Project ini membutuhkan beberapa API key yang dimasukkan langsung melalui n8n Credentials.

## 1. VirusTotal
Dipakai untuk:
- Cek hash malware
- Cek reputasi URL/IP

Masukkan API key di HTTP Request credential/header.

## 2. AbuseIPDB
Dipakai untuk:
- Cek reputasi IP address
- Ambil country dan risk score

Masukkan API key di HTTP Request credential/header.

## 3. URLScan.io
Dipakai untuk:
- Scan URL phishing
- Ambil screenshot website
- Ambil verdict malicious/clean

Masukkan API key di HTTP Request credential/header.

## 4. Telegram Bot
Dipakai untuk:
- Mengirim hasil enrichment ke grup/channel SOC

Masukkan bot token dan chat ID di node Telegram atau HTTP Request.
## Cara Menjalankan
1. Import file JSON dari folder `workflows/` ke n8n.
2. Buat credential API sesuai `.env.example`.
3. Aktifkan workflow.
4. Trigger webhook menggunakan Postman atau script Python.
5. Cek hasil notifikasi di Telegram.
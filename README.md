# 🤖 Telegram AI RAG Chatbot (n8n Workflow)

Repositori ini berisi workflow **n8n** untuk membangun chatbot AI berbasis **Retrieval-Augmented Generation (RAG)**.  
Chatbot ini memungkinkan pengguna untuk mengunggah dokumen PDF melalui Telegram, menyimpannya ke dalam Vector Store, serta melakukan tanya jawab secara cerdas berdasarkan isi dokumen tersebut.

---

## 🚀 Fitur Utama

- 📄 **Document Ingestion**  
  Mengunduh dan memproses otomatis dokumen PDF yang dikirim melalui Telegram.

- 🔍 **Vector Search**  
  Menggunakan **Supabase Vector Store** untuk penyimpanan dan pencarian dokumen relevan.

- 🧠 **AI Engine**  
  Ditenagai oleh **Gemini 2.5 Flash Lite** untuk pemrosesan teks yang cepat dan akurat.

- 💬 **Memory History**  
  Menyimpan riwayat percakapan menggunakan PostgreSQL agar chatbot memahami konteks.

- ✅ **Validation System**  
  Memastikan hanya file dokumen (PDF) yang diproses.

---

## 🛠️ Arsitektur Workflow

Workflow ini terdiri dari **dua jalur utama**:

### 1️⃣ Jalur Ingesti Data (Knowledge Base)

- **Input Document**  
  Trigger saat pengguna mengirim file ke bot Telegram.

- **HTTP Request**  
  Mengambil file dari server Telegram API.

- **JavaScript Code**  
  Mengonversi file menjadi format yang siap dibaca (MIME Type: PDF).

- **Document Ingestion**  
  Melakukan embedding teks menggunakan model `gemini-embedding-001` dan menyimpannya ke tabel `documents` di Supabase.

---

### 2️⃣ Jalur Query (Chatting)

- **Query Receiver**  
  Trigger saat pengguna mengirim pesan teks.

- **Cognitive Core (Agent)**  
  Otak AI yang menentukan kapan perlu mengambil data dari Knowledge Base.

- **Knowledge Retrieval**  
  Mencari potongan teks paling relevan di Supabase berdasarkan query pengguna.

- **Session History**  
  Mengambil konteks percakapan sebelumnya dari PostgreSQL.

- **Answer Message**  
  Mengirimkan jawaban final kembali ke pengguna melalui Telegram.

---

## 📋 Prasyarat

Sebelum mengimpor workflow ini, pastikan Anda memiliki:

- n8n (Self-hosted atau Cloud)
- API Key Google Gemini (untuk LLM & Embeddings)
- Bot Token Telegram (dari **@BotFather**)
- Database Supabase (dengan ekstensi `pgvector`)
- Database PostgreSQL (untuk session memory)

---

## ⚙️ Cara Instalasi

1. Salin isi file `RAG.json` dari repositori ini  
2. Buka dashboard n8n Anda  
3. Pilih **Import from JSON**  
4. Tempelkan kode workflow  
5. Konfigurasikan credentials untuk:
   - Google Gemini API
   - Telegram API
   - Supabase API
   - PostgreSQL
6. Sesuaikan nama tabel pada node:
   - `Document Ingestion`
   - `Knowledge Retrieval`  
   (default: `documents`)
7. Aktifkan workflow

---

## 🤖 Instruksi System Message

Chatbot ini dikonfigurasi dengan aturan berikut:

- 📚 Hanya menjawab berdasarkan dokumen yang tersedia  
- ❌ Jika tidak ditemukan, AI akan jujur mengatakan tidak tahu (anti-halusinasi)  
- 💬 Menggunakan Bahasa Indonesia yang ramah dan sopan  
- 😊 Wajib menyertakan minimal 1 emoji yang relevan  

---

## 👨‍💻 Author

**Muhammad Habiburrahman Al-Arif**  
Student of Software Engineering  
Full-stack Developer | Automation Enthusiast

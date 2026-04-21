Telegram AI RAG Chatbot (n8n Workflow)
Repositori ini berisi workflow n8n untuk membangun Chatbot AI berbasis Retrieval-Augmented Generation (RAG). Chatbot ini memungkinkan pengguna untuk mengunggah dokumen PDF melalui Telegram, menyimpannya ke dalam Vector Store, dan melakukan tanya jawab berdasarkan isi dokumen tersebut secara cerdas.

🚀 Fitur Utama
Document Ingestion: Mengunduh otomatis dokumen PDF yang dikirim melalui Telegram.

Vector Search: Menggunakan Supabase Vector Store untuk penyimpanan dan pencarian dokumen yang relevan.

AI Engine: Ditenagai oleh Gemini 2.5 Flash Lite untuk pemrosesan teks yang cepat dan akurat.

Memory History: Menyimpan riwayat percakapan menggunakan PostgreSQL agar chatbot memahami konteks obrolan.

Validation: Sistem validasi yang memastikan hanya file dokumen yang diproses.

🛠️ Arsitektur Workflow
Workflow ini terdiri dari dua jalur utama:

1. Jalur Ingesti Data (Knowledge Base)
Input Document: Trigger saat pengguna mengirim file ke bot Telegram.

HTTP Request: Mengambil file dari server Telegram API.

JavaScript Code: Mengonversi file menjadi format yang siap dibaca (MIME Type: PDF).

Document Ingestion: Melakukan embedding teks menggunakan model gemini-embedding-001 dan menyimpannya ke tabel documents di Supabase.

2. Jalur Query (Chatting)
Query Receiver: Trigger saat pengguna mengirim pesan teks.

Cognitive Core (Agent): Otak AI yang memutuskan kapan harus mengambil data dari Knowledge Base.

Knowledge Retrieval: Mencari potongan teks paling relevan di Supabase berdasarkan query pengguna.

Session History: Mengambil konteks pesan sebelumnya dari database Postgres.

Answer Message: Mengirimkan jawaban final kembali ke pengguna di Telegram.

📋 Prasyarat
Sebelum mengimpor workflow ini, pastikan Anda memiliki:

n8n (Self-hosted atau Cloud).

API Key Google Gemini (untuk LLM dan Embeddings).

Bot Token Telegram (didapat dari @BotFather).

Database Supabase (dengan ekstensi pgvector aktif).

Database PostgreSQL (untuk menyimpan session memory).

⚙️ Cara Instalasi
Salin isi file RAG.json dari repositori ini.

Buka dashboard n8n Anda.

Pilih Import from JSON dan tempelkan kodenya.

Konfigurasikan Credentials untuk masing-masing node:

Google Gemini(PaLM) Api

Telegram Api

Supabase Api

Postgres

Sesuaikan nama tabel di node Document Ingestion dan Knowledge Retrieval (default: documents).

Aktifkan workflow.

🤖 Instruksi System Message
AI ini telah dikonfigurasi dengan aturan khusus:

Hanya menjawab berdasarkan dokumen yang tersedia.

Jika tidak ada di dokumen, AI akan jujur mengatakan tidak tahu (mencegah halusinasi).

Gaya bahasa ramah, sopan, dan menggunakan Bahasa Indonesia.

Wajib menyertakan minimal 1 emoji yang relevan.

Developed by Muhammad Habiburrahman Al-Arif
Student of Software Engineering | Full-stack Developer | Automation Enthusiast

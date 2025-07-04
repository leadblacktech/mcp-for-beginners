<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "adaf47734a5839447b5c60a27120fbaf",
  "translation_date": "2025-06-11T16:05:10+00:00",
  "source_file": "05-AdvancedTopics/README.md",
  "language_code": "id"
}
-->
# Topik Lanjutan dalam MCP

Bab ini ditujukan untuk membahas serangkaian topik lanjutan dalam implementasi Model Context Protocol (MCP), termasuk integrasi multi-modal, skalabilitas, praktik keamanan terbaik, dan integrasi perusahaan. Topik-topik ini sangat penting untuk membangun aplikasi MCP yang kuat dan siap produksi yang dapat memenuhi tuntutan sistem AI modern.

## Ikhtisar

Pelajaran ini mengeksplorasi konsep lanjutan dalam implementasi Model Context Protocol, dengan fokus pada integrasi multi-modal, skalabilitas, praktik keamanan terbaik, dan integrasi perusahaan. Topik-topik ini penting untuk membangun aplikasi MCP kelas produksi yang mampu menangani kebutuhan kompleks di lingkungan perusahaan.

## Tujuan Pembelajaran

Pada akhir pelajaran ini, Anda akan dapat:

- Menerapkan kemampuan multi-modal dalam kerangka kerja MCP  
- Merancang arsitektur MCP yang skalabel untuk skenario dengan permintaan tinggi  
- Menerapkan praktik keamanan terbaik sesuai dengan prinsip keamanan MCP  
- Mengintegrasikan MCP dengan sistem dan kerangka kerja AI perusahaan  
- Mengoptimalkan kinerja dan keandalan dalam lingkungan produksi  

## Pelajaran dan Proyek Contoh

| Link | Judul | Deskripsi |
|------|-------|-------------|
| [5.1 Integration with Azure](./mcp-integration/README.md) | Integrasi dengan Azure | Pelajari cara mengintegrasikan MCP Server Anda di Azure |
| [5.2 Multi modal sample](./mcp-multi-modality/README.md) | Contoh Multi modal MCP | Contoh untuk audio, gambar, dan respons multi modal |
| [5.3 MCP OAuth2 sample](../../../05-AdvancedTopics/mcp-oauth2-demo) | Demo MCP OAuth2 | Aplikasi Spring Boot minimal yang menunjukkan OAuth2 dengan MCP, baik sebagai Authorization dan Resource Server. Menunjukkan penerbitan token yang aman, endpoint terlindungi, deployment Azure Container Apps, dan integrasi API Management. |
| [5.4 Root Contexts](./mcp-root-contexts/README.md) | Root contexts | Pelajari lebih lanjut tentang root context dan cara mengimplementasikannya |
| [5.5 Routing](./mcp-routing/README.md) | Routing | Pelajari berbagai jenis routing |
| [5.6 Sampling](./mcp-sampling/README.md) | Sampling | Pelajari cara bekerja dengan sampling |
| [5.7 Scaling](./mcp-scaling/README.md) | Scaling | Pelajari tentang scaling |
| [5.8 Security](./mcp-security/README.md) | Security | Amankan MCP Server Anda |
| [5.9 Web Search sample](./web-search-mcp/README.md) | Web Search MCP | Server dan klien MCP Python yang mengintegrasikan SerpAPI untuk pencarian web, berita, produk, dan Q&A secara real-time. Menunjukkan orkestrasi multi-tool, integrasi API eksternal, dan penanganan error yang kuat. |
| [5.10 Realtime Streaming](./mcp-realtimestreaming/README.md) | Streaming | Streaming data real-time telah menjadi hal penting di dunia yang didorong data saat ini, di mana bisnis dan aplikasi memerlukan akses informasi secara instan untuk pengambilan keputusan tepat waktu. |

## Referensi Tambahan

Untuk informasi terbaru tentang topik MCP lanjutan, lihat:
- [MCP Documentation](https://modelcontextprotocol.io/)
- [MCP Specification](https://spec.modelcontextprotocol.io/)
- [GitHub Repository](https://github.com/modelcontextprotocol)

## Poin Penting

- Implementasi MCP multi-modal memperluas kemampuan AI di luar pemrosesan teks  
- Skalabilitas sangat penting untuk deployment perusahaan dan dapat diatasi melalui scaling horizontal dan vertikal  
- Langkah keamanan yang komprehensif melindungi data dan memastikan kontrol akses yang tepat  
- Integrasi perusahaan dengan platform seperti Azure OpenAI dan Microsoft AI Foundry meningkatkan kapabilitas MCP  
- Implementasi MCP lanjutan mendapat manfaat dari arsitektur yang dioptimalkan dan pengelolaan sumber daya yang cermat  

## Latihan

Rancang implementasi MCP kelas perusahaan untuk kasus penggunaan tertentu:

1. Identifikasi kebutuhan multi-modal untuk kasus penggunaan Anda  
2. Gariskan kontrol keamanan yang diperlukan untuk melindungi data sensitif  
3. Rancang arsitektur skalabel yang dapat menangani beban yang bervariasi  
4. Rencanakan titik integrasi dengan sistem AI perusahaan  
5. Dokumentasikan potensi hambatan kinerja dan strategi mitigasinya  

## Sumber Daya Tambahan

- [Azure OpenAI Documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/)  
- [Microsoft AI Foundry Documentation](https://learn.microsoft.com/en-us/ai-services/)  

---

## Selanjutnya

- [5.1 MCP Integration](./mcp-integration/README.md)

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berusaha untuk akurasi, harap diketahui bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber yang sahih. Untuk informasi penting, disarankan menggunakan terjemahan profesional oleh manusia. Kami tidak bertanggung jawab atas kesalahpahaman atau salah tafsir yang timbul dari penggunaan terjemahan ini.
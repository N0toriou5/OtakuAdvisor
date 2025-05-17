# OtakuAdvisor
<p align="center">
  <img src="https://github.com/user-attachments/assets/aa6a3a69-e137-4d5e-9d99-7adcc75bea66" alt="Otaku" width="600" height="600">
</p>

**OtakuAdvisor** è un assistente virtuale per collezionisti di manga, fumetti e memorabilia anni ’80–’90. Basato su modelli open‑source e su tecniche di retrieval semantico, fornisce stime di valore, consigli d’acquisto/vendita e informazioni sulle edizioni in tempo reale.

---

## 📦 Caratteristiche principali

* **Chatbot 24/7**: interfaccia conversazionale per rispondere a domande su edizioni, quotazioni, consigli di collezionismo.
* **Retrieval semantico**: ricerca intelligente all’interno del catalogo documentale (descrizioni, quotazioni storiche, guide).
* **Memoria conversazionale**: mantiene il contesto delle conversazioni per follow‑up coerenti.
* **Modello LLM locale**: utilizzo di Llama 2 tramite Hugging Face per eliminare costi API.
* **Embeddings e Vector DB**: `sentence‑transformers` + Chroma per indicizzazione e similarity search.
* **API RESTful**: server FastAPI pronto per integrazione frontend (web/mobile).

---

## 🚀 Installazione

1. **Clona il repository**

   ```bash
   git clone https://github.com/tuo-org/otakuadvisor.git
   cd otakuadvisor
   ```

2. **Crea un ambiente virtuale**

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Installa le dipendenze**

   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Prepara i dati**

   * Riempi la cartella `data_collezioni/` con file di documenti (`.txt`, `.json`, `.csv`) contenenti descrizioni, quotazioni, recensioni.

5. **Ingestione documenti**

   ```bash
   python main.py ingest
   ```

   Questo comando popolerà il database Chroma con gli embedding dei documenti.

6. **Avvia il server**

   ```bash
   python main.py serve
   ```

   Il server sarà disponibile su `http://localhost:8000`.

---

## ⚙️ Configurazione

Puoi personalizzare i parametri di esecuzione modificando `config.py`:

* `MODEL_NAME`: nome del modello Llama 2 su Hugging Face.
* `EMBEDDING_MODEL`: modello per sentence embeddings.
* `CHROMA_DIR`: percorso per il database Chroma.
* `MAX_TOKENS`, `TEMPERATURE`: parametri di generazione del testo.

---

## 📄 API

### POST `/chat`

* **Request**

  ```json
  {
    "user_id": "string",
    "message": "string"
  }
  ```

* **Response**

  ```json
  {
    "answer": "string"
  }
  ```

### Esempio di curl

```bash
curl -X POST http://localhost:8000/chat \
  -H "Content-Type: application/json" \
  -d '{"user_id":"user123","message":"Qual è il valore medio di Dragon Ball #1?"}'
```

---

## 🛠️ Architettura

```
+-------------+       +-------------+       +-------------+
|   Frontend  | <----> |   FastAPI   | <----> | LangChain   |
+-------------+       +-------------+       +-------------+
                                   |
                                   v
                            +-------------+
                            |   Chroma    |
                            +-------------+
                                   |
                                   v
                            +-------------+
                            |   Llama 2    |
                            +-------------+
```

* **FastAPI**: gestisce le richieste HTTP.
* **LangChain**: orchestration di retrieval e generazione.
* **Chroma**: vector store per similarity search.
* **Llama 2**: modello di linguaggio open‑source per generare risposte.

---

## 🤝 Contribuire

1. Fork del repository
2. Crea un branch feature (`git checkout -b feature/nome-feature`)
3. Commit delle modifiche (`git commit -m "Aggiunge nuova feature"`)
4. Push sul branch (`git push origin feature/nome-feature`)
5. Apri una Pull Request

Per guidelines dettagliate, vedi `CONTRIBUTING.md`.

---

## 📝 Licenza

Questo progetto è rilasciato sotto licenza **Apache 2.0**. Vedi `LICENSE` per maggiori dettagli.

---

*Buon collezionismo con OtakuAdvisor!*

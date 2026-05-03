# 5. Logging & Observability

If you can't measure it, you can't manage it. Structured logging is essential for production debugging.

### **Winston / Pino**
- **Why use it:** `Winston` is highly configurable (multiple transports like files, databases, consoles). `Pino` is built for extreme performance with low overhead.
- **Alternatives:** 
    - **Bunyan:** Structured JSON logging.
    - **Morgan:** Specifically for HTTP request logging.
- **Use Case:** Production monitoring, debugging, and audit trails. Always log in JSON format for easy ingestion by ELK/Splunk.

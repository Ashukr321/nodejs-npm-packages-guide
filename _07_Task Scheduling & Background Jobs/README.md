# 7. Task Scheduling & Background Jobs

Offloading heavy work from the main event loop is key to Node.js performance.

### **BullMQ**
- **Why use it:** The most robust Redis-based queue for Node.js. Handles retries, priorities, and delayed jobs with ease.
- **Alternatives:** 
    - **Agenda:** MongoDB-based task scheduling.
    - **Node-Cron:** Simple in-process cron jobs (not recommended for distributed systems).
- **Use Case:** Sending emails, processing images, generating reports, and any long-running background tasks.

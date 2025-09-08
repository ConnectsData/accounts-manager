+--------------------+       HTTPS        +--------------------+
|   Web Browser      | <----------------> |  Front‑end (React) |
|  (React SPA)       |   (REST/GraphQL)   |  (Vite/CRA)        |
+--------------------+                    +-------------------+
         |                                          |
         |   Auth (JWT in HttpOnly cookie)          |
         v                                          v
+--------------------+       HTTPS        +--------------------+
|      API GW       | <----------------> |  Backend (Node/TS) |
| (Express, Rate‑lim)|  (REST/WS)       |  (Auth, Users,    |
+--------------------+                    |   Accounts, Jobs) |
         |                                 +-------------------+
         |  +----------------------+              |
         |  |  Queue (BullMQ)      | <------------+
         |  +----------+-----------+   async jobs (PDF → TXNs)
         |             |
         v             v
+----------------+   +----------------+   +----------------+  
|   Redis (Bull) |   |   PostgreSQL   |   |   S3 (or MinIO)|
| (job store)    |   | (users, acct, |   | (PDF/CSV files)|
+----------------+   |  txns, cat)   |   +----------------+
                     +----------------+

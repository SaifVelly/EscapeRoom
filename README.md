
# 🖥️ Coding Rooms Platform

A full-stack platform for hosting **coding competitions and challenges**, built with a modern microservice architecture. It supports three distinct tracks:

- **Competitive Programming (CP)** — solve algorithmic problems, submit code, get judged automatically.  
- **Code Exercises (CE)** — practice and improve coding skills with curated problems.  
- **Capture The Flag (CTF)** — security challenges with encrypted flags and score tracking.  

Everything is containerized with **Docker Compose**, and integrates with **Judge0** for code execution.

## 🚀 Features
- 👩‍💻 **CP & CE**: Problem management, Code editor (CodeMirror) with Python/Java/C++/Rust, Automatic execution & scoring via Judge0, Leaderboards.  
- 🕵️ **CTF**: Challenge management, Encrypted flag storage (AES-256), Flag submission & scoring, Role-based user tracking.  
- 🔐 **Authentication**: Optional external Auth service (Spring Boot + JWT), proxied by the frontend.  
- 📊 **Admin Dashboard**: Configure CP/CE/CTF challenges, Upload problems & test cases, Monitor leaderboard data.  

## 🛠️ Tech Stack
**Frontend**: Next.js 15, React 19, Redux Toolkit, CodeMirror, Recharts, React Markdown + remark-math + rehype-katex, lucide-react  
**Backend (CP & CE)**: Node.js, Express, PostgreSQL, Judge0 API, dotenv, cors, multer, axios  
**Backend (CTF)**: Node.js, Express, Sequelize, PostgreSQL, bcryptjs, AES-256-CBC encryption with Node crypto  
**Auth Service (optional)**: Spring Boot, JWT authentication  
**Infra**: Docker, Docker Compose, PostgreSQL 16, External Judge0 network  

## 📂 Project Structure
```

coding_platform-main/
├── src/                 # Next.js frontend (pages, components, Redux store)
│   ├── app/             # Routes: /cp, /ce, /ctf, /leaderboard, /admin
│   ├── components/      # Code editor, markdown viewer, tables
│   └── store/           # Redux slices
├── microservices/
│   ├── microservice_CP/ # Competitive Programming service
│   ├── microservice_CE/ # Code Exercises service
│   └── microservice_CTF/# Capture The Flag service (Sequelize, encryption)
├── docker-compose.yml   # Orchestration
├── Dockerfile           # Frontend build
└── README.md            # ← You are here

````

## ⚙️ Setup & Running
### 1. Clone the repo
```bash
git clone https://github.com/saifvelly/EScapeRoom.git
cd coding_platform
````

### 2. Start services

```bash
docker-compose up --build
```

This starts: CP (5005), CE (5006), CTF (5007), UI ([http://localhost](http://localhost)), DB (5432), Auth (optional, 8080).

### 3. Run Judge0

Requires an external Judge0 instance.

```bash
docker network create judge0-v1131_default
docker network connect judge0-v1131_default competitive-programming-service
docker network connect judge0-v1131_default code-enhancement-service
```

Update `.env`:

```
JUDGE0_URL=http://judge0-v1131-server-1:2358
```

### 4. Visit the app

Open [http://localhost](http://localhost).

## 🔑 Environment Variables

Example `.env`:

```
DB_HOST=db-service
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=password
DB_NAME=coding_rooms
JUDGE0_URL=http://judge0-v1131-server-1:2358
ENCRYPTION_KEY=32_character_random_secret_key
NEXT_PUBLIC_AUTHENTICATION_URL=http://auth-service-postgres:8080
```

## 📝 Roadmap

* ✅ Encrypted flags for CTF
* ✅ Judge0 integration for CP/CE
* 🔲 Centralized Auth (JWT roles/permissions)
* 🔲 Submission rate limiting
* 🔲 CI/CD pipeline with tests
* 🔲 Better admin analytics

## 🤝 Contributing

1. Fork the repo
2. Create a branch (`git checkout -b feature/foo`)
3. Commit changes (`git commit -m 'Add foo'`)
4. Push (`git push origin feature/foo`)
5. Open a Pull Request

## 📄 License

MIT License. See [LICENSE](LICENSE) for details.

```

---

```

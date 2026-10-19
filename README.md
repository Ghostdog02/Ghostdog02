# Hi, I'm Alexander 👋

I'm a computer science student who mostly works on the backend. I enjoy following a project the whole way through: the UI, authentication and authorization, and then the less glamorous part of getting it deployed, secured, and kept running. I've been building and running my own projects end to end, and I'm still learning something new from each one.

### Where I can help

- 🚀 **Deploying web apps**: Docker, a cloud server, HTTPS, and Cloudflare, with experience across .NET, Node, Python, Angular, and React
- 🏗️ **Full-stack apps**: ASP.NET Core and Angular, with auth handled carefully (OAuth 2.0, JWT, HttpOnly cookies). **Lexiq** below is my most complete example
- 🔁 **CI/CD**: build, test, and deploy pipelines with GitHub Actions
- 🛟 **Getting AI-built apps live**: if a Lovable, Cursor, Bolt, or v0 project works in preview but isn't on a stable URL yet, I'm happy to help with that last stretch
- 🔒 **Infrastructure basics**: Terraform and Ansible, SSH hardening, firewalls, secrets management, and keeping public ports to a minimum

---

## 🔧 Technical Skills

| Category           | Technologies                                  |
| ------------------ | --------------------------------------------- |
| **Languages**      | C#, TypeScript, Bash                          |
| **Backend**        | ASP.NET Core, Node.js, Express                |
| **Frontend**       | Angular, HTML5, SCSS                          |
| **Databases**      | MS SQL Server, MongoDB                        |
| **Infrastructure** | Terraform, Ansible, Docker, Nginx             |
| **CI/CD & VCS**    | GitHub Actions, Git                           |
| **OS**             | Linux, Windows 10/11, Temple OS               |
| **Design**         | Photoshop, Illustrator                        |

<p align="left">
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/csharp/csharp-original.svg" width="42" height="42" alt="C#" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/dot-net/dot-net-original-wordmark.svg" width="42" height="42" alt=".NET" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/microsoftsqlserver/microsoftsqlserver-plain-wordmark.svg" width="42" height="42" alt="MS SQL Server" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/typescript/typescript-original.svg" width="42" height="42" alt="TypeScript" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/angular/angular-original.svg" width="42" height="42" alt="Angular" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" width="42" height="42" alt="Docker" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" width="42" height="42" alt="Linux" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/terraform/terraform-original.svg" width="42" height="42" alt="Terraform" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/ansible/ansible-original.svg" width="42" height="42" alt="Ansible" />
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nginx/nginx-original.svg" width="42" height="42" alt="Nginx" />
</p>

---

## 🚀 Projects

### Lexiq: Language Learning Platform

![.NET](https://img.shields.io/badge/.NET-10.0-512BD4)
![Angular](https://img.shields.io/badge/Angular-21-DD0031)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Tunnel%20%2B%20Zero%20Trust-F38020)

**[relexiq.com](https://relexiq.com) · [Repository](https://github.com/Ghostdog02/Lexiq)**

A language learning app (Italian for English speakers) that I built end to end, partly as a way to practice running a real production system. Users work through structured lessons, complete interactive exercises, earn XP, and compete on a leaderboard.

**Some of the things I worked on:**

- **No exposed ports**: all traffic goes through a Cloudflare Tunnel, with TLS, DDoS, WAF, and bot protection handled at the edge
- **Stateless authentication**: Google OAuth 2.0 issues a JWT stored in an HttpOnly cookie, so it's never accessible to JavaScript and the API can scale horizontally
- **CI/CD pipeline**: every push to `master` builds Docker images, runs the test suite (unit, integration, and E2E via Testcontainers), pushes to GHCR, and deploys
- **Two-layer caching**: static assets are cached at Cloudflare's edge with a 1-year immutable TTL, and API responses are cached server-side with `IMemoryCache`
- **Dependency management**: Dependabot watches Docker, npm, NuGet, and GitHub Actions, and PRs that pass tests are auto-merged
- **Security scanning**: GitHub CodeQL runs on every push and PR for both C# and TypeScript

**Infrastructure snapshot:**

```
Browser → Cloudflare Edge (TLS, DDoS, WAF, Cache)
        → cloudflared (Cloudflare Tunnel)
        → Nginx (Docker bridge, plain HTTP)
        → ASP.NET Core API : MS SQL Server
```

**Tech stack:** ASP.NET Core 10 · Angular 21 · MS SQL Server 2022 · Docker Compose · Nginx · Cloudflare Tunnel + Zero Trust · GitHub Actions · xUnit v3 + Testcontainers · CodeQL

---

### Server Infrastructure: Hetzner Cloud

![Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC)
![Ansible](https://img.shields.io/badge/Ansible-Configuration-EE0000)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Zero%20Trust%20SSH-F38020)

**[Repository](https://github.com/Ghostdog02/server-configuration)**

Infrastructure as code for provisioning and configuring the server that runs Lexiq, automated from a `git push`.

**Architecture:**

```
GitHub Actions
    ├── Terraform (Terraform Cloud) → Hetzner Cloud API → provisions server
    └── Ansible → Cloudflare Tunnel → SSH → configures server
```

> SSH port 22 isn't exposed to the public internet. Ansible connects through a Cloudflare Tunnel, authenticated with Cloudflare Access service tokens.

**What's automated:**

| Ansible Role  | What it does                                                 |
| ------------- | ------------------------------------------------------------ |
| `users`       | Creates `deploy` and `developer` system users                |
| `docker`      | Installs Docker Engine                                       |
| `directories` | Creates application directory structure                      |
| `ssh`         | Hardens SSH config (key-only auth, restricted ciphers)       |
| `security`    | Configures UFW firewall and fail2ban                         |
| `cloudflared` | Installs and runs the Cloudflare Tunnel as a systemd service |

**Decisions I made along the way:**

- Terraform state lives in **Terraform Cloud**, so there are no local state files and it works cleanly in CI
- Secrets are encrypted at rest with **Ansible Vault** and injected at deploy time
- Cloudflare Zero Trust replaces a public SSH port, which removes one of the most commonly attacked entry points

---

## 📡 What I'm Learning Next
 
I'm still building out my skills, and I'll be applying these to the projects above as I go:
 
- **AI engineering:** LLM APIs and tool use, embeddings, vector databases (pgvector, Qdrant), RAG (chunking, hybrid search, reranking).
- **C++ fundamentals:** memory management, RAII, and the STL
---

## 📊 GitHub Stats

<p align="left">
  <a href="https://github.com/ryo-ma/github-profile-trophy">
    <img src="https://github-profile-trophy.vercel.app/?username=ghostdog02&theme=onedark" alt="ghostdog02" />
  </a>
</p>

&nbsp; [![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=Ghostdog02&show_icons=true&theme=dark)](https://github.com/Ghostdog02/github-readme-stats)

&nbsp; [![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=Ghostdog02&hide=html&theme=dark)](https://github.com/Ghostdog02/github-readme-stats)

&nbsp; [![GitHub Streak](https://github-readme-streak-stats-alex-veselys-projects.vercel.app?user=Ghostdog02&theme=dark&hide_border=true&date_format=j%20M%5B%20Y%5D)](https://github.com/Ghostdog02/github-readme-streak-stats)

---

## 🤝 Connect

I'm always happy to chat, whether it's about a project, feedback on something I've built, or a possible collaboration.

📧 alex.vesely07@gmail.com

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alexander-vesely-b23367325/)
[![Discord](https://img.shields.io/badge/Discord-5865F2?logo=discord&logoColor=white)](https://discord.gg/hackblood)

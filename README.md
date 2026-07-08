# Hi, I'm Alexander 👋

Backend-focused Computer Science student who builds and ships **production-grade systems** — from secure full-stack web apps to the cloud infrastructure that runs them. I care about the whole path: a clean UI, authentication and authorization done right, and code that actually gets deployed, secured, and kept running.

> 💼 **Available for freelance — I make your app production-ready.**
> I take working code and get it *live, secure, and automated*: containerized, deployed behind Cloudflare, with a CI/CD pipeline so your next update is one `git push`.
> **[Work with me on Fiverr →](https://www.fiverr.com/s/DB8GYbV)**
> <!-- swap the link for your main Fiverr profile URL if you prefer -->

### What I can do for you

- 🚀 **Deploy & productionize your web app** — Docker, a cloud server, HTTPS, and Cloudflare security (any stack: .NET, Node, Python, Angular, React)
- 🏗️ **Build a secure full-stack web app** — ASP.NET Core + Angular with a clean, well-designed UI and authentication & authorization done properly (OAuth 2.0, JWT, HttpOnly cookies) — see **Lexiq** below for a live example
- 🔁 **Set up CI/CD** — automated build, test, and deploy pipelines with GitHub Actions
- 🛟 **Rescue AI-built / vibe-coded apps** — get your Lovable / Cursor / Bolt / v0 project off "works in preview" and onto a real, stable URL
- 🔒 **Harden & automate infrastructure** — Terraform + Ansible, SSH lockdown, firewall, secrets management, zero exposed ports

---

## 🔧 Technical Skills

| Category           | Technologies                                  |
| ------------------ | --------------------------------------------- |
| **Languages**      | C#, TypeScript, Bash                          |
| **Backend**        | ASP.NET Core, Node.js, Express                |
| **Frontend**       | Angular, HTML5, SCSS                          |
| **Databases**      | MS SQL Server, MongoDB                        |
| **Infrastructure** | Terraform, Ansible, Docker, Nginx, Cloudflare |
| **CI/CD & VCS**    | GitHub Actions, Git                           |
| **OS & Security**  | Linux (Ubuntu), UFW, fail2ban, SSH hardening  |
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

### Lexiq — Production Full-Stack Language Learning Platform

![.NET](https://img.shields.io/badge/.NET-10.0-512BD4)
![Angular](https://img.shields.io/badge/Angular-21-DD0031)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Tunnel%20%2B%20Zero%20Trust-F38020)

**[relexiq.com](https://relexiq.com) · [Repository](https://github.com/Ghostdog02/Lexiq)**

A language learning app (Italian for English speakers) built end-to-end as a production-grade technical showcase. Users progress through structured lessons, complete interactive exercises, earn XP, and compete on a leaderboard.

**What makes it production-grade:**

- **Zero exposed ports** — all traffic routed through a Cloudflare Tunnel; TLS terminated at the edge with DDoS, WAF, and bot protection included
- **Stateless authentication** — Google OAuth 2.0 issues a JWT stored in an HttpOnly cookie, never accessible to JavaScript, enabling horizontal API scalability
- **Full CI/CD pipeline** — every push to `master` builds Docker images, runs the complete test suite (unit → integration → E2E via Testcontainers), pushes to GHCR, and deploys — no manual steps
- **Two-layer caching** — static assets served from Cloudflare's global edge with a 1-year immutable TTL; API responses cached server-side via `IMemoryCache`
- **Automated dependency management** — Dependabot monitors Docker, npm, NuGet, and GitHub Actions; PRs that pass tests are auto-merged
- **Security scanning** — GitHub CodeQL runs on every push and PR for both C# and TypeScript

**Infrastructure snapshot:**

```
Browser → Cloudflare Edge (TLS, DDoS, WAF, Cache)
        → cloudflared (Cloudflare Tunnel)
        → Nginx (Docker bridge, plain HTTP)
        → ASP.NET Core API : MS SQL Server
```

**Tech stack:** ASP.NET Core 10 · Angular 21 · MS SQL Server 2022 · Docker Compose · Nginx · Cloudflare Tunnel + Zero Trust · GitHub Actions · xUnit v3 + Testcontainers · CodeQL

---

### Production Server Infrastructure — Hetzner Cloud

![Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC)
![Ansible](https://img.shields.io/badge/Ansible-Configuration-EE0000)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Zero%20Trust%20SSH-F38020)

**[Repository](https://github.com/Ghostdog02/server-configuration)**

Infrastructure-as-Code for provisioning and configuring the production server that runs Lexiq. Fully automated from a `git push`.

**Architecture:**

```
GitHub Actions
    ├── Terraform (Terraform Cloud) → Hetzner Cloud API → provisions server
    └── Ansible → Cloudflare Tunnel → SSH → configures server
```

> SSH port 22 is never exposed to the public internet. All Ansible connections are routed through a Cloudflare Tunnel authenticated via Cloudflare Access service tokens.

**What's automated:**

| Ansible Role  | What it does                                                 |
| ------------- | ------------------------------------------------------------ |
| `users`       | Creates `deploy` and `developer` system users                |
| `docker`      | Installs Docker Engine                                       |
| `directories` | Creates application directory structure                      |
| `ssh`         | Hardens SSH config (key-only auth, restricted ciphers)       |
| `security`    | Configures UFW firewall and fail2ban                         |
| `cloudflared` | Installs and runs the Cloudflare Tunnel as a systemd service |

**Key decisions:**

- Terraform state is managed remotely via **Terraform Cloud** — no local state files, safe for CI
- Secrets are encrypted at rest with **Ansible Vault** and injected at deploy time
- Cloudflare Zero Trust replaces a public SSH port entirely — the attack surface is zero

---

## 📡 Currently Expanding Into

Actively adding the operational layer that turns a running app into one you can trust at 3 a.m. — shipping into the projects above as I go:

| Area                         | Goal                                                                                |
| ---------------------------- | ----------------------------------------------------------------------------------- |
| **Prometheus + Grafana**     | Observability for production systems — metrics, dashboards, alerting                 |
| **Nginx internals**          | Beyond basic reverse proxy — rate limiting, caching, TLS tuning, upstream health     |
| **VPN server (self-hosted)** | Hands-on Linux networking: routing, tun/tap interfaces, firewall rules, WireGuard    |
| **Linux internals**          | Process management, namespaces, cgroups, systemd services, kernel parameters         |

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

📧 alex.vesely07@gmail.com

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alexander-vesely-b23367325/)
[![Fiverr](https://img.shields.io/badge/Fiverr-Hire%20me-1DBF73?logo=fiverr&logoColor=white)](https://www.fiverr.com/s/DB8GYbV)
[![Discord](https://img.shields.io/badge/Discord-5865F2?logo=discord&logoColor=white)](https://discord.gg/hackblood)

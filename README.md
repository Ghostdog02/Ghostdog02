# Hi, I'm Alexander 👋

Backend-focused Computer Science student building and shipping **production-grade systems** — from full-stack apps to the cloud infrastructure that runs them. I care about how things actually get deployed, secured, and kept running, not just how they're coded.

Currently deepening my DevOps expertise: Prometheus & Grafana for observability, Nginx tuning, and building a self-hosted VPN server to get closer to Linux internals.

---

## 🔧 Technical Skills

| Category | Technologies |
| :--- | :--- |
| **Languages** | C#, TypeScript, Bash |
| **Backend** | ASP.NET Core, Node.js, Express |
| **Frontend** | Angular, HTML5, SCSS |
| **Databases** | MS SQL Server, MongoDB |
| **Infrastructure** | Terraform, Ansible, Docker, Nginx, Cloudflare |
| **CI/CD & VCS** | GitHub Actions, Git |
| **OS & Security** | Linux (Ubuntu), UFW, fail2ban, SSH hardening |
| **Design** | Photoshop, Illustrator |

<p align="left">
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/csharp/csharp-original.svg" alt="csharp" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/dot-net/dot-net-original-wordmark.svg" alt="dotnet" width="40" height="40"/>
  <img src="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" alt="mssql" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/typescript/typescript-original.svg" alt="typescript" width="40" height="40"/>
  <img src="https://angular.io/assets/images/logos/angular/angular.svg" alt="angular" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" alt="docker" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/linux/linux-original.svg" alt="linux" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/terraform/terraform-original.svg" alt="terraform" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/ansible/ansible-original.svg" alt="ansible" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nginx/nginx-original.svg" alt="nginx" width="40" height="40"/>
</p>

---

## 🚀 Projects

### Lexiq — Production Full-Stack Language Learning Platform

[![.NET](https://img.shields.io/badge/.NET-10.0-512BD4)](https://dotnet.microsoft.com/)
[![Angular](https://img.shields.io/badge/Angular-21-DD0031)](https://angular.io/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED)](https://www.docker.com/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF)](https://github.com/features/actions)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-Tunnel%20%2B%20Zero%20Trust-F38020)](https://www.cloudflare.com/)

**[relexiq.com](https://relexiq.com) · [Repository](https://github.com/Ghostdog02/Lexiq)**

A language learning app (Italian for English speakers) built end-to-end as a production-grade technical showcase. Users progress through structured lessons, complete interactive exercises, earn XP, and compete on a leaderboard.

**What makes it production-grade:**

- **Zero exposed ports** — all traffic routed through a Cloudflare Tunnel; TLS terminated at the edge with DDoS, WAF, and bot protection included
- **Stateless authentication** — Google OAuth 2.0 issues a JWT stored in an HttpOnly cookie, never accessible to JavaScript, enabling horizontal API scalability
- **Full CI/CD pipeline** — every push to `master` builds Docker images, runs the complete test suite (unit → integration → E2E via Testcontainers), pushes to GHCR, and deploys — no manual steps
- **Two-layer caching** — static assets (JS/CSS/fonts) served from Cloudflare's global edge with 1-year immutable TTL; API responses cached server-side via `IMemoryCache`
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

[![Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC)](https://www.terraform.io/)
[![Ansible](https://img.shields.io/badge/Ansible-Configuration-EE0000)](https://www.ansible.com/)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-Zero%20Trust%20SSH-F38020)](https://www.cloudflare.com/)

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

| Ansible Role | What it does |
| :--- | :--- |
| `users` | Creates `deploy` and `developer` system users |
| `docker` | Installs Docker Engine |
| `directories` | Creates application directory structure |
| `ssh` | Hardens SSH config (key-only auth, restricted ciphers) |
| `security` | Configures UFW firewall and fail2ban |
| `cloudflared` | Installs and runs the Cloudflare Tunnel as a systemd service |

**Key decisions:**
- Terraform state is managed remotely via **Terraform Cloud** — no local state files, safe for CI
- Secrets are encrypted at rest with **Ansible Vault** and injected at deploy time
- Cloudflare Zero Trust replaces a public SSH port entirely — the attack surface is zero

---

## 📡 Currently Learning

I'm focused on the operational side of running software in production:

| Area | Goal |
| :--- | :--- |
| **Prometheus + Grafana** | Build observability into production systems — metrics, dashboards, alerting |
| **Nginx internals** | Go beyond basic reverse proxy — rate limiting, caching, TLS tuning, upstream health |
| **VPN server (self-hosted)** | Hands-on Linux networking: routing, tun/tap interfaces, firewall rules, WireGuard |
| **Linux internals** | Process management, namespaces, cgroups, systemd services, kernel parameters |

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

<p align="left">
<a href="https://www.linkedin.com/in/alexander-vesely-b23367325/" target="blank">
  <img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="LinkedIn" height="30" width="40" />
</a>
<a href="https://discord.gg/hackblood" target="blank">
  <img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/discord.svg" alt="Discord" height="30" width="40" />
</a>
</p>

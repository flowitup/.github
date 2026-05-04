<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/banner-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/banner-light.svg">
  <img alt="flowitup — Software for the people who build." src="./assets/banner-light.svg" width="100%">
</picture>

<p align="center">
  <a href="https://folio.flowitup.com">
    <img alt="Folio is live" src="https://img.shields.io/badge/Folio-live-F97316?style=for-the-badge&logo=googlechrome&logoColor=white">
  </a>
  <img alt="Made in France" src="https://img.shields.io/badge/Made_in-France-0055A4?style=for-the-badge">
  <img alt="Status: beta" src="https://img.shields.io/badge/Status-beta-525252?style=for-the-badge">
</p>

<p align="center">
  <em>A small product team in France, building software that takes the headache out of running a construction business.</em>
</p>

---

## Folio — what we ship

[**folio.flowitup.com**](https://folio.flowitup.com) is the only thing flowitup ships right now. It is a Construction Management System for small and mid-sized construction companies — the kind of business that runs on WhatsApp threads, paper attendance sheets, and Excel files mailed back and forth.

Folio is what those companies use instead.

### What you can do with it

- **Projects** — keep every site (an office tower, a riverside building, a renovation) in its own workspace, with its own team and address.
- **Team & roles** — invite people by email; each member gets a role (owner, manager, foreman, accountant, viewer) that decides what they can see and do.
- **Labor tracking** — log who worked which day, full or half day, plus extra "supplement" hours that are automatically converted into bonus days at month-end.
- **Excel & PDF exports** — labor reports for any 1-to-24-month window. French currency formatting, Vietnamese accents render correctly.
- **Invoices** — Client, Labor and Supplier invoices with line items and a print-clean view.
- **Notes & reminders** — post a note with a due date; every project member gets reminded in the bell-icon dropdown when the lead time hits.
- **Three languages** — English, French, Vietnamese. Light, dark and system theme.

---

## Stack

<p>
  <img alt="Python 3.12"  src="https://img.shields.io/badge/Python_3.12-3776AB?logo=python&logoColor=white&style=flat-square">
  <img alt="Flask 3"      src="https://img.shields.io/badge/Flask_3-000000?logo=flask&logoColor=white&style=flat-square">
  <img alt="SQLAlchemy"   src="https://img.shields.io/badge/SQLAlchemy-D71F00?logo=sqlalchemy&logoColor=white&style=flat-square">
  <img alt="RQ"           src="https://img.shields.io/badge/RQ_workers-DC382D?logo=redis&logoColor=white&style=flat-square">
  <img alt="TypeScript"   src="https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white&style=flat-square">
  <img alt="Next.js 16"   src="https://img.shields.io/badge/Next.js_16-000000?logo=nextdotjs&logoColor=white&style=flat-square">
  <img alt="Tailwind"     src="https://img.shields.io/badge/Tailwind-06B6D4?logo=tailwindcss&logoColor=white&style=flat-square">
  <img alt="shadcn/ui"    src="https://img.shields.io/badge/shadcn%2Fui-000000?logo=shadcnui&logoColor=white&style=flat-square">
  <img alt="Docker"       src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white&style=flat-square">
  <img alt="Google Cloud" src="https://img.shields.io/badge/GCP-4285F4?logo=googlecloud&logoColor=white&style=flat-square">
  <img alt="Cloudflare"   src="https://img.shields.io/badge/Cloudflare-F38020?logo=cloudflare&logoColor=white&style=flat-square">
  <img alt="GitHub Actions" src="https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white&style=flat-square">
</p>

---

## Architecture, at a glance

```mermaid
flowchart LR
  Browser["Browser<br/>EN · FR · VI"]

  subgraph FE["folio-front-end"]
    Next["Next.js 16<br/>Tailwind · shadcn"]
  end

  subgraph BE["folio-back-end"]
    Flask["Flask 3 API"]
    Worker["RQ worker<br/>emails · exports · reminders"]
    DB[("PostgreSQL")]
    Redis[("Redis")]
  end

  subgraph Umbrella["folio (umbrella + deploy)"]
    GHA["GitHub Actions"]
    GCP["GCP Compute<br/>via IAP SSH"]
  end

  Browser --> Next
  Next --> Flask
  Flask <--> DB
  Flask <--> Redis
  Worker <--> DB
  Worker <--> Redis

  FE -. tag v* .-> GHA
  BE -. tag v* .-> GHA
  GHA --> GCP
```

The umbrella `folio` repo ties together the back-end and front-end as submodules and runs the deploy workflows. A version tag in either sub-repo dispatches a deploy job in `folio` that builds an image, pushes to Artifact Registry, SSHs into the GCP VM via IAP, runs smoke tests, then bumps the submodule pointer back on `master` so the parent always reflects the SHA running in prod.

---

## Active projects

| | Repo | What it is | Stack |
|---|---|---|---|
| 🔒 | [`folio`](https://github.com/flowitup/folio) | Umbrella repo — submodules, infra, deploy workflows, docs | Shell · GitHub Actions |
| 🔒 | [`folio-back-end`](https://github.com/flowitup/folio-back-end) | The API behind Folio | Python · Flask · SQLAlchemy · RQ |
| 🔒 | [`folio-front-end`](https://github.com/flowitup/folio-front-end) | The web app you click on | TypeScript · Next.js · Tailwind · shadcn |

Repos are private while Folio is in beta. If you are a member of the org the links above will take you in; otherwise GitHub will return a 404.

---

## Team

<p align="center">
  <a href="https://github.com/ducxyz">
    <img src="https://github.com/ducxyz.png" width="80" height="80" alt="@ducxyz"><br>
    <sub><b>@ducxyz</b></sub>
  </a>
  &nbsp;&nbsp;&nbsp;&nbsp;
  <a href="https://github.com/yaiba2307">
    <img src="https://github.com/yaiba2307.png" width="80" height="80" alt="@yaiba2307"><br>
    <sub><b>@yaiba2307</b></sub>
  </a>
</p>

---

## Get in touch

Found a bug? Have a feature request? Curious about Folio?

→ [**Open an issue on `flowitup/.github`**](https://github.com/flowitup/.github/issues/new) and we will see it.

---

<p align="center">
  <sub>
    Made with care in France &middot; Source is currently closed while Folio is in beta &middot; &copy; 2026 flowitup
  </sub>
</p>

# Tournament Suite

**The connected operating system for competitive gaming.**

[Website](https://tournamentsuite.com) · [Developer Docs](https://tournamentsuite.com/developer) · [Live Demo](https://arena.tournamentsuite.com) · [Contact](https://tournamentsuite.com/contact)

---

Tournament Suite is a full-stack esports infrastructure company building the end-to-end competitive gaming platform — connecting organizers, players, and platform operators in one system. From player registration and bracket automation to live match operations, financial settlement, player engagement, and P2P cloud gaming, every layer of the competitive stack is covered.

---

## Platform

### Organizer Workspace
The command center for tournament directors, league operators, and esports organizations. Create and manage competitions across every format — Swiss, Round Robin, Single Elimination, Double Elimination, Gauntlet, Free For All, and Group Stage. Run multi-event circuits and season-long standings with cumulative qualification paths. Assign officials and referees, operate a full Broadcast Center with OBS/vMix overlay support, manage player payouts and revenue splits, handle sponsorship campaigns with impression and click analytics, and run compliance and audit workflows — all from one workspace.

### White-Label Player Portal
Deploy a fully branded esports portal on your own domain. Logo, colors, and CSS are fully customizable — zero Tournament Suite branding visible to players. The player-facing surface includes Battle Pass XP progression with AI-generated seasonal missions, skill-based Matchmaking, Fantasy esports contests, Coaching session booking with VOD review, LFG/LFT boards, a Marketplace with buyer-seller escrow, an in-platform Wallet with prize management, scrim scheduling, clan wars, social feed, streaming and highlights, and a Wellness module.

### Admin Backoffice
Multi-tenant platform control for operators. Identity verification, anti-smurf detection, reputation scoring, Guardian parental controls and consent management, transparent discipline and appeals workflows, compliance tooling, and full audit trails across all tenant activity.

### Developer API
REST and WebSocket APIs, webhook delivery with XState retry machines, a sandbox environment, and OAuth support for 8 providers. Embeddable widgets for live brackets, leaderboards, registration forms, and match schedules. Per-tenant API key management, rate-limit visibility, and a developer portal.

### P2P Cloud Gaming
A peer-to-peer cloud gaming infrastructure layer — Wolf pixel streaming (Moonlight, NVENC/VAAPI), a fleet control plane with node registry and session state machine, a stateless Fastify WebRTC/WS signaling broker with RFC 5766 TURN credential generation, and a Go daemon per host supporting both stream and dedicated modes. Node reputation scoring, tiered payout plans (per-minute, per-session, tiered-quality with p95 latency/drop multipliers), and a host enrollment portal for the Become a Host program.

### Mobile Apps
A Flutter Clubhouse app for community discovery, live event sessions, and operator-managed clubhouses — with real-time attendance via WebSocket, map-based discovery, player check-in QR passes, and biometric-gated authentication via Keycloak OIDC PKCE. A Flutter dating app powered by gaming signal weights derived from MMR, disciplines, and recent playtime to personalize matchmaking.

### Desktop Client
A Tauri anti-cheat desktop app with embedded agent — demo file upload, real-time detection events, ban bridge via NATS, and a Rust demoparser sidecar that streams round-level feature extraction to flag suspicious activity.

---

## Game Integrations

Deep integrations with automated stat ingestion, player account verification, match data population, and live API polling — no manual score entry required.

| Game | Integration Depth |
|---|---|
| **Counter-Strike 2** | Full match automation via RCON + GSI, CS2 plugin system (CounterStrikeSharp), demo upload + Rust demoparser, GOTV relay, dedicated server fleet management, cosign-verified plugin delivery via CDN, per-host Go node agent |
| **CS Legacy (1.6 / Source)** | srcds dedicated server orchestration, XState match state machine, RCON control |
| **Valorant** | Riot Games API — account verification, live stat ingestion, match data automation |
| **League of Legends** | Riot Games API — live match data, player verification, stat sync |
| **Dota 2** | Steam API + Steam lobby management via bot, match data automation |
| **Apex Legends** | Apex Legends Status API + Dedicated Game Server API, BullMQ polling, match lifecycle wiring |
| **Rocket League** | Match data ingestion, player rankings |
| **Fortnite** | Epic Games OAuth2, tournament and match data |
| **PUBG: Battlegrounds** | PUBG API with BullMQ polling, match and stat integration |
| **Team Fortress 2** | logs.tf webhook ingestion with HMAC verification, RCON server control |
| **Mobile Legends: Bang Bang** | Match data and player verification |
| **SMITE 2** | Stat ingestion and match tracking |
| **Deadlock** | Valve integration, XState match state machine |
| **Brawl Stars** | Supercell OAuth2 client_credentials with per-project token isolation, BullMQ polling |
| **Trackmania** | Nadeo dual-token auth (api.trackmania.com + Nadeo services), Meet API for competition and lobby management, BullMQ polling |

---

## Engineering

### Architecture
- **45+ microservices** — NestJS monolith core, game integration services, cloud gaming control plane, billing engine, anti-cheat pipeline, notifications, analytics, and Steam OAuth bridge
- **Real-time infrastructure** — Socket.IO namespaced rooms per tournament and match, NATS pub/sub event bus across all services, SSE delivery, WebRTC P2P signaling
- **Multi-tenant white-label engine** — per-tenant AES-256-GCM encrypted secrets, JSONB-structured config (payment, KYC, communications, AI, feature flags, game integrations), custom domain deployment
- **AI-powered engagement** — Battle Pass AI mission generation (LLM strict-JSON via AIProviderManagerService), gaming-signal-weighted dating matchmaking, scouting LAN bridge and mentorship recommendations
- **Job infrastructure** — BullMQ workers across 8+ queues: match polling, demo analysis, webhook retry, AI mission generation, moderation, discovery cache rebuild, sponsor metrics, notification delivery
- **Observability** — Sentry/Bugsink error tracking per service, TimescaleDB analytics, structured logging

### Security
- AES-256-GCM tenant secret encryption, SSRF and IDOR protection, webhook HMAC verification across all inbound integrations, GraphQL depth and complexity limits, SQL injection whitelist guards, InternalSecretGuard fail-closed on all game services, atomic NATS token replay prevention, session IDOR protection in cloud gaming, cosign-verified binary and plugin delivery

### Infrastructure
- **Staging** — Docker Compose: TimescaleDB, Valkey (Redis), NATS, Keycloak, nginx, Mailpit
- **Production** — Kubernetes, Terraform, Helm umbrella chart, self-hosted Docker registry, Gitea Actions CI/CD, `kubectl set image` zero-churn deploys

---

## Stack

**Backend** — NestJS · TypeScript · PostgreSQL (TimescaleDB) · Redis (Valkey) · NATS · BullMQ · TypeORM · XState v5 · GraphQL  
**Frontend** — Next.js 16 · Turbopack · Tailwind CSS · Zustand · TanStack Query v5 · Socket.IO · urql  
**Mobile** — Flutter · Riverpod · flutter_appauth · flutter_secure_storage · go_router  
**Desktop** — Tauri · Rust demoparser sidecar  
**Agents** — Go · NATS-over-TLS · cosign · SteamCMD  
**Infrastructure** — Kubernetes · Terraform · Helm · Docker · Cloudflare · Gitea CI  
**Auth** — Keycloak · RS256 JWT · Steam OIDC · PKCE · HttpOnly cookies  
**Payments** — Stripe · RevenueCat · PayPal  
**Streaming** — Wolf · Moonlight · NVENC · VAAPI · WebRTC · TURN/STUN  
**AI** — LLM mission generation · Sightengine · PhotoDNA content moderation  

---

**🌐 [tournamentsuite.com](https://tournamentsuite.com)**

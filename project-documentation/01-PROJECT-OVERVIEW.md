# Project Overview - Daggerfall Unity Web Port

## Executive Summary

**Project Name**: Daggerfall Unity Web Port
**Goal**: Port Daggerfall Unity to a modern web application using TypeScript and WebGL
**Timeline**: 24 months (2 years)
**Team Size**: 3 developers (Months 1-12), 4 developers (Months 13-24)
**Budget**: $720K-$940K (development) + $300-$1,200 (infrastructure)
**Target Launch**: Month 24

---

## Vision Statement

Create a modernized, web-based reimagining of Daggerfall that:
- Runs in browsers without emulation (Windows/Linux/Mac)
- Achieves 3-5 second time-to-playable
- Maintains 60 FPS on recommended hardware
- Supports ethical freemium monetization
- Provides foundation for future multiplayer/co-op

---

## Technology Stack

### Frontend
- **Language**: TypeScript 5+
- **Game Engine**: Custom ECS with bitECS
- **Rendering**: Three.js r159+ (WebGL 2, WebGPU support)
- **Physics**: Custom kinematic character controller
- **UI Framework**: React 18+
- **Build Tool**: Vite with code splitting
- **Package Manager**: pnpm

### Backend
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth (email/OAuth/magic links)
- **Storage**: Supabase Storage (cloud saves)
- **Payments**: Stripe
- **CDN**: Cloudflare
- **Monitoring**: Sentry + Custom Analytics

### Development Tools
- **Testing**: Vitest (unit), Playwright (E2E)
- **CI/CD**: GitHub Actions
- **Version Control**: Git
- **Code Quality**: ESLint, Prettier, TypeScript strict mode

---

## Team Structure

### Months 1-12 (Core Team - 3 Developers)

**Developer 1 (Lead)** - $120K-$150K/year
- Architecture and systems design
- DevOps and infrastructure
- Team leadership
- Backend integration

**Developer 2 (Graphics)** - $100K-$130K/year
- Three.js / WebGL expertise
- Rendering systems and shaders
- Visual effects and optimization
- Asset pipeline

**Developer 3 (Gameplay)** - $100K-$130K/year
- Game systems and mechanics
- ECS architecture
- AI and NPC systems
- Content creation tools

### Months 13-24 (Expanded Team - 4 Developers)

**Developer 4 (Content)** - $80K-$120K/year *(joins Month 12)*
- Procedural generation (dungeons, cities)
- Quest content creation
- 3D modeling and level design
- Balancing and polish

---

## Key Decisions

### Architectural Choices
✅ **bitECS** over other ECS libraries (10-100x faster, memory-efficient)
✅ **Custom kinematic physics** over Rapier (95% smaller, sufficient control)
✅ **Three.js** for rendering (mature, well-supported, WebGPU ready)
✅ **Supabase** for backend (free tier supports 1000 users, $25/mo Pro when needed)
✅ **Programmer art** strategy for fast MVP (5-10MB vs 450MB final assets)
✅ **Progressive loading** with 4 stages (3-5s to playable)
✅ **Freemium model** (Free full game + Premium $9.99/mo + Lifetime $149.99)

### Strategic Decisions
✅ **24 months** realistic timeline (vs 18 months initial estimate)
✅ **Hire 4th developer** in Month 12 for Phase 3B workload
✅ **Prioritize compatibility** over cutting-edge graphics
✅ **Desktop browsers first**, mobile as future enhancement
✅ **No mods initially**, focus on core experience
✅ **Future multiplayer** components built-in from start

---

## Success Metrics

### Technical (Launch - Month 24)
- 60 FPS on recommended hardware (GTX 1060, i5, 16GB RAM)
- 30 FPS on minimum hardware (Intel UHD 630, i3, 8GB RAM)
- <5 second load time to playable
- <2% crash rate
- 99.9% uptime
- <512 MB memory usage
- <100 draw calls per frame

### Business (Month 24)
- 10,000+ registered users
- 2-3% conversion rate (200-300 paying users)
- $2,000-$3,000 Monthly Recurring Revenue (MRR)
- $24,000-$36,000 Annual Recurring Revenue (ARR)
- <2% refund rate
- 40% 7-day retention
- 25% 30-day retention

### User Experience (Beta - Month 20)
- 7.5+/10 average user rating
- 80%+ would recommend to friends
- 70%+ quest completion rate
- 60%+ dungeon completion rate

---

## Major Milestones

| Month | Phase | Milestone | Deliverable |
|-------|-------|-----------|-------------|
| 4 | Phase 1 | Foundation Complete | Tech Demo (ECS + Rendering + Movement) |
| 8 | Phase 2 | Core Gameplay | Playable Prototype (Combat + Quests + Saves) |
| 13 | Phase 3A | Dungeons & Quests | Alpha - Dungeons (175 quests, procedural dungeons) |
| 17 | Phase 3B | Cities & AI | Alpha - Complete World (275 quests, all 15,000 locations) |
| 20 | Phase 4 | Polish & Effects | Beta Release (Weather, cosmetics, 1,000 testers) |
| 22 | Phase 5 | Monetization | Pre-Launch (Payments working, infrastructure scaled) |
| 24 | Phase 6 | Launch | Public Release (10,000 users, 3 post-launch updates) |

---

## Risk Management

### High-Priority Risks

**1. Timeline Slippage**
- **Mitigation**: 2-month buffer built-in, monthly milestone reviews
- **Contingency**: Cut features (cosmetics, extra quests), delay to Month 26

**2. Supabase Storage Exceeded**
- **Mitigation**: Aggressive save compression (100-150KB per save)
- **Contingency**: Upgrade to Pro ($25/mo) by Month 22

**3. Performance Budget Exceeded**
- **Mitigation**: Built-in performance monitoring, adaptive quality system
- **Contingency**: Reduce view distance, simplify effects on low-end

**4. Low User Acquisition**
- **Mitigation**: Beta testing validates demand, free tier reduces barrier
- **Contingency**: Adjust pricing, extend beta phase, focus on community growth

---

## Financial Overview

### Development Costs (24 Months)
- **Salaries**: $720K-$940K
- **Infrastructure**: $300-$1,200 (Supabase + CDN + monitoring)
- **Marketing**: $10K-$20K (launch)
- **Legal/Accounting**: $5K-$10K
- **Miscellaneous**: $10K-$20K
- **TOTAL**: $745K-$991K

### Revenue Projections

**Conservative (Month 24)**
- 10,000 users × 2% conversion = 200 paying
- 150 Premium ($9.99/mo) + 50 Lifetime ($149.99 one-time)
- **MRR**: ~$2,000/month
- **Year 1 Revenue**: ~$12,000 (Months 22-24)

**Optimistic (Month 24)**
- 20,000 users × 3% conversion = 600 paying
- 500 Premium + 100 Lifetime
- **MRR**: ~$7,000/month
- **Year 1 Revenue**: ~$35,000

**Break-Even Projection**: Year 2-3 (need 3,500+ Premium subscribers)

---

## Scope Definition

### In Scope (Launch)
✅ Full Daggerfall world (500,000 km²)
✅ 275+ quests
✅ Procedural dungeons (5 types)
✅ 15,000+ locations (cities, towns, villages)
✅ Combat (melee, ranged, magic)
✅ Character progression (skills, leveling)
✅ Inventory and equipment
✅ Guilds system (5 guilds)
✅ Save/load with cloud sync
✅ Weather system (8 types)
✅ Day/night cycle
✅ Freemium monetization
✅ 50 cosmetic items
✅ Pet system (10 pets)

### Out of Scope (Launch)
❌ Mod support (future consideration)
❌ Multiplayer/co-op (foundation built, feature post-launch)
❌ Mobile browsers (desktop first, mobile later)
❌ VR support
❌ User-generated content
❌ Streaming integration
❌ Achievements system (post-launch)

### Deferred to Year 2
🔄 Seasonal events
🔄 Leaderboards
🔄 Social features (guilds, chat)
🔄 Additional quest content (100+ quests)
🔄 New dungeon types
🔄 More cosmetics (100+ items)
🔄 Multiplayer/co-op implementation

---

## Next Steps

1. **Immediate (Week 1-2)**: Set up infrastructure
   - Create monorepo structure
   - Configure TypeScript, ESLint, Prettier
   - Set up CI/CD pipeline
   - Initialize Supabase project

2. **Month 1**: Build foundation
   - Implement ECS core with bitECS
   - Create texture atlas system
   - Build basic audio system
   - Set up Three.js renderer

3. **Month 2-4**: Complete Phase 1
   - Character controller
   - World streaming
   - Terrain generation
   - Progressive loading
   - Tech demo ready

**See [04-REVISED-24-MONTH-ROADMAP.md](./04-REVISED-24-MONTH-ROADMAP.md) for detailed timeline.**

---

## Related Documents

- [02-TECHNICAL-ARCHITECTURE.md](./02-TECHNICAL-ARCHITECTURE.md) - Technical details
- [03-CRITICAL-GAPS-ANALYSIS.md](./03-CRITICAL-GAPS-ANALYSIS.md) - Known issues
- [04-REVISED-24-MONTH-ROADMAP.md](./04-REVISED-24-MONTH-ROADMAP.md) - Detailed timeline
- [05-TESTING-STRATEGY.md](./05-TESTING-STRATEGY.md) - QA approach
- [09-MONETIZATION-SYSTEM.md](./09-MONETIZATION-SYSTEM.md) - Business model

---

**Last Updated**: 2024-11-15
**Document Version**: 1.0.0
**Status**: ✅ Planning Complete

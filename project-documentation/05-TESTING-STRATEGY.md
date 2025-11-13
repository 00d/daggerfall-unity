# Testing Strategy - Daggerfall Unity Web Port

## Overview

Comprehensive testing strategy for all 6 phases, including automation infrastructure, performance testing, and QA processes.

**Total Investment**: 1,240+ automated tests + 2,220+ hours manual testing

---

## Testing Philosophy

1. **Test Early, Test Often** - Continuous testing from Day 1
2. **Automation First** - Automate regression, manual for exploratory
3. **Performance is a Feature** - Every feature tested for performance
4. **Shift Left** - Developers write tests as they code
5. **User-Centric** - Focus on UX, not just code coverage

---

## Test Infrastructure

### Tooling Stack

**Unit Testing**:
- Vitest (fast, TypeScript-native)
- Happy-DOM (lightweight DOM)
- **Target**: 75% code coverage

**E2E Testing**:
- Playwright (cross-browser: Chrome, Firefox, Safari)
- Visual regression (screenshot comparison)

**Performance Testing**:
- Lighthouse (performance audits)
- k6 (load testing for 1,000+ concurrent users)

**CI/CD**:
- GitHub Actions (automated test runs)
- Pre-commit hooks (Husky)
- Performance regression detection

### CI/CD Pipeline

```
Commit → Fast Tests (5min) → Integration (15min) → E2E (30min) → 
  Performance (20min) → Deploy Staging → Manual Approval → Production
```

**Total Time**: ~70 minutes per commit

---

## Phase-by-Phase Testing Strategy

### Phase 1 (Months 1-4): Foundation Testing

**Focus**: Core systems, rendering, physics

**Unit Tests**: 150+
- ECS components and systems
- Character controller
- Physics collision detection
- Texture atlas packing

**Integration Tests**: 20+
- ECS + Physics integration
- Rendering sync with ECS

**E2E Tests**: 10+
- Player spawns and moves
- Terrain loads correctly
- Audio plays

**Performance Tests**: 5+
- Frame time <16.67ms (60 FPS)
- Memory <250MB
- Draw calls <100

**Manual Testing**: 20 hours
- 5 internal testers
- Test on different hardware

**Exit Criteria**:
- ✅ 0 P0 bugs, <5 P1 bugs
- ✅ 60 FPS on mid-range hardware
- ✅ 60%+ code coverage

---

### Phase 2 (Months 5-8): Core Gameplay Testing

**Focus**: Combat, inventory, saves, backend

**Unit Tests**: 300+ (cumulative)
- Combat damage calculation
- Inventory management
- Save serialization
- Backend integration

**Integration Tests**: 50+
- Combat + Health systems
- Inventory + Equipment
- Save + Load full cycle
- Supabase authentication

**E2E Tests**: 30+
- Complete combat encounter
- Pick up and equip item
- Save and reload game
- Sign up and sign in

**Performance Tests**: 10+
- Combat with 10 enemies
- Save/load under 3 seconds

**Manual Testing**: 100 hours
- 50 alpha testers (recruited from Reddit, Discord)
- Focus: Game balance, save reliability, performance

**Exit Criteria**:
- ✅ 0 P0 bugs, <10 P1 bugs
- ✅ 50 testers complete 5+ quests
- ✅ <5% crash rate
- ✅ 70%+ code coverage

---

### Phase 3A (Months 9-13): Dungeons & Quests Testing

**Focus**: Procedural generation, quest system

**Unit Tests**: 450+ (cumulative)
- Dungeon generation consistency (same seed = same layout)
- Quest condition evaluation
- Quest branching logic

**Integration Tests**: 80+
- Dungeon entrance → interior transition
- Quest progression end-to-end

**E2E Tests**: 50+
- Complete full dungeon crawl
- Accept and complete quest
- Guild questline (5 quests)

**Performance Tests**: 15+
- Dungeon generation <2 seconds
- 60 FPS in dungeons
- Memory usage with dungeons

**Manual Testing**: 200 hours
- 200 alpha testers (expanded)
- Each tester: 10 dungeons, 20 quests
- Quest testing spreadsheet (track bugs per quest)

**Exit Criteria**:
- ✅ 0 P0 bugs, <20 P1 bugs
- ✅ 150/200 testers complete 10+ quests
- ✅ <10% crash rate
- ✅ 75%+ code coverage

---

### Phase 3B (Months 14-17): Cities & AI Testing

**Focus**: City generation, NPC AI, pathfinding

**Unit Tests**: 600+ (cumulative)
- City layout generation
- Pathfinding (A* correctness)
- NPC behavior state machines

**Integration Tests**: 120+
- City generation + population
- NPC schedules (day/night cycles)
- Dialog system

**E2E Tests**: 80+
- Navigate city and enter buildings
- Shop interaction (buy/sell)
- Talk to NPC and start quest
- Fast travel between cities

**Performance Tests**: 25+
- City generation <5 seconds
- 60 FPS with 100 NPCs
- Pathfinding <16ms for 100 NPCs

**Manual Testing**: 400 hours
- 200 alpha testers
- Focus: Full game loop, 50+ quests each
- Economy balance testing

**Exit Criteria**:
- ✅ 0 P0 bugs, <30 P1 bugs
- ✅ 180/200 testers complete full game loop
- ✅ <10% crash rate
- ✅ 60 FPS in cities

---

### Phase 4 (Months 18-20): Polish & Beta Testing

**Focus**: Visual polish, weather, cosmetics, accessibility

**Unit Tests**: 700+ (cumulative)
- Weather state transitions
- Cosmetic equipment system

**E2E Tests**: 120+
- Character customization
- Purchase cosmetic item

**Visual Regression Tests**: 30+
- Skybox at different times
- Weather effects (rain, snow)
- UI elements

**Performance Tests**: 35+
- 60 FPS on low-end hardware
- Weather particle systems
- Memory leak detection

**Manual Testing**: 1,000 hours
- 1,000 beta testers (public recruitment)
- 2-week intensive testing
- Feedback surveys
- Performance telemetry

**Exit Criteria**:
- ✅ 0 P0 bugs, <50 P1 bugs
- ✅ 800/1,000 testers play 10+ hours
- ✅ <5% crash rate
- ✅ 7.5+/10 user rating

---

### Phase 5 (Months 21-22): Monetization Testing

**Focus**: Payment flows, security, load testing

**Integration Tests**: 180+ (cumulative)
- Stripe checkout flow
- Subscription webhooks
- Refund handling

**E2E Tests**: 150+
- Complete purchase flow
- Cancel subscription
- Purchase cosmetic

**Security Tests**:
- SQL injection prevention
- XSS prevention
- RLS policy enforcement
- Rate limiting

**Load Tests**:
- 100 concurrent users
- 500 concurrent users
- 1,000 concurrent users
- 5,000 concurrent users (spike test)

**Manual Testing**: 500 hours
- Payment testing (100+ test transactions)
- Security audit (external)

**Exit Criteria**:
- ✅ 0 P0 bugs, <20 P1 bugs
- ✅ Payment flow 99%+ success
- ✅ Load tested for 5,000 users
- ✅ 0 critical security vulnerabilities

---

### Phase 6 (Months 23-24): Launch Testing

**Focus**: Production monitoring, smoke tests, on-call

**Smoke Tests** (automated, run hourly during launch):
- User can sign up and play
- Save and load works
- Payment flow works

**Monitoring**:
- Real-time dashboard (FPS, errors, uptime)
- Alert thresholds (crash rate >5%, FPS <45)
- On-call rotation (12-hour shifts)

**Post-Launch**:
- Daily regression suite
- A/B testing framework
- Community bug reporting (GitHub Issues)

**Exit Criteria**:
- ✅ 10,000+ users
- ✅ <2% crash rate
- ✅ 99.9% uptime
- ✅ All P0/P1 bugs fixed

---

## Performance Budgets (Enforced in CI)

```typescript
const PERFORMANCE_BUDGETS = {
  frameTime: { target: 16.67, critical: 33.33 },    // 60 FPS → 30 FPS
  timeToPlayable: { target: 5000, critical: 10000 }, // 5s → 10s
  initialBundle: { target: 2000, critical: 5000 },   // 2MB → 5MB
  heapSize: { target: 512, critical: 1024 },         // 512MB → 1GB
  drawCalls: { target: 100, critical: 200 },
  triangles: { target: 100000, critical: 200000 },
  apiResponseTime: { target: 200, critical: 1000 },  // 200ms → 1s
}
```

**CI fails if any metric exceeds critical threshold**

---

## Test Coverage Summary

| Phase | Unit | Integration | E2E | Performance | Manual | Total |
|-------|------|-------------|-----|-------------|--------|-------|
| Phase 1 | 150+ | 20+ | 10+ | 5+ | 20h | 185+ |
| Phase 2 | 300+ | 50+ | 30+ | 10+ | 100h | 390+ |
| Phase 3A | 450+ | 80+ | 50+ | 15+ | 200h | 595+ |
| Phase 3B | 600+ | 120+ | 80+ | 25+ | 400h | 825+ |
| Phase 4 | 700+ | 150+ | 120+ | 35+ | 1000h | 1005+ |
| Phase 5 | 750+ | 180+ | 150+ | 50+ | 500h | 1130+ |
| Phase 6 | 800+ | 200+ | 180+ | 60+ | Continuous | 1240+ |

**Total Automated Tests**: 1,240+  
**Total Manual Hours**: 2,220+

---

## Quality Gates

**Cannot proceed to next phase unless:**

✅ 0 P0 bugs (game-breaking, crashes)  
✅ P1 bugs under threshold (varies by phase)  
✅ Code coverage meets target (60% → 80%)  
✅ Performance budgets met  
✅ Manual testing completion rate >75%

---

## Test Automation Examples

### Unit Test (ECS Component)
```typescript
import { describe, it, expect } from 'vitest'
import { createWorld, addEntity, addComponent } from 'bitecs'
import { Transform, Velocity } from '../components'

describe('Transform Component', () => {
  it('should store position correctly', () => {
    const world = createWorld()
    const eid = addEntity(world)
    addComponent(world, Transform, eid)
    
    Transform.x[eid] = 10.5
    expect(Transform.x[eid]).toBeCloseTo(10.5, 2)
  })
})
```

### E2E Test (Inventory)
```typescript
import { test, expect } from '@playwright/test'

test('should pick up item', async ({ page }) => {
  await page.goto('http://localhost:5173')
  
  // Move to item
  await page.keyboard.press('w')
  await page.waitForTimeout(2000)
  
  // Open inventory
  await page.keyboard.press('i')
  const itemCount = page.locator('[data-testid="item-count"]')
  await expect(itemCount).toHaveText('1')
})
```

### Performance Test
```typescript
import { describe, it, expect } from 'vitest'

describe('Rendering Performance', () => {
  it('should maintain 60 FPS with 10,000 entities', async () => {
    const renderer = new GameRenderer()
    
    // Spawn 10,000 entities
    for (let i = 0; i < 10000; i++) {
      createEntity(world)
    }
    
    // Run for 5 seconds
    const frames = []
    for (let i = 0; i < 300; i++) {
      const startTime = performance.now()
      renderer.render()
      const endTime = performance.now()
      frames.push(endTime - startTime)
    }
    
    const avgFrameTime = frames.reduce((a, b) => a + b) / frames.length
    const fps = 1000 / avgFrameTime
    
    expect(fps).toBeGreaterThanOrEqual(60)
  })
})
```

---

## Bug Severity & SLA

| Severity | Description | Response | Fix Time |
|----------|-------------|----------|----------|
| **P0** | Game-breaking, crashes | <15 min | <4 hours |
| **P1** | Major features broken | <1 hour | <1 day |
| **P2** | Minor bugs | <4 hours | <1 week |
| **P3** | Polish | <1 week | Backlog |

---

## Related Documents

- [02-TECHNICAL-ARCHITECTURE.md](./02-TECHNICAL-ARCHITECTURE.md) - Systems to test
- [04-REVISED-24-MONTH-ROADMAP.md](./04-REVISED-24-MONTH-ROADMAP.md) - Testing timeline
- [07-PERFORMANCE-BUDGETS.md](./07-PERFORMANCE-BUDGETS.md) - Performance targets

---

**Last Updated**: 2024-11-15  
**Document Version**: 1.0.0  
**Status**: Complete - Testing strategy defined for all phases

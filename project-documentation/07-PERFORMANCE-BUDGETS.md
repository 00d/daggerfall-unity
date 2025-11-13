# Performance Budgets - Daggerfall Unity Web Port

## Overview

Strict performance budgets enforced in CI/CD pipeline. Exceeding critical thresholds fails the build.

**Philosophy**: Performance is a feature, not an afterthought.

---

## Performance Budget Matrix

### Frame Time Budgets

```typescript
export const FRAME_TIME_BUDGETS = {
  // Target: 60 FPS (16.67ms per frame)
  // Critical: 30 FPS (33.33ms per frame)

  total: {
    target: 16.67,    // milliseconds
    critical: 33.33,
    test: 'Every frame must hit target 95% of time'
  },

  breakdown: {
    ecs: {
      target: 5.0,    // ECS systems
      critical: 10.0
    },
    rendering: {
      target: 8.0,    // Three.js render
      critical: 18.0
    },
    physics: {
      target: 2.0,    // Character controller + collision
      critical: 4.0
    },
    scripts: {
      target: 1.67,   // Quest logic, AI
      critical: 3.0
    }
  }
}
```

**Enforcement**: Performance tests run in CI, fail if exceeded 3 frames in 300-frame test.

---

## Loading Time Budgets

### Time to Playable (Cold Start)

```typescript
export const LOADING_BUDGETS = {
  timeToPlayable: {
    target: 5000,     // 5 seconds
    critical: 10000,  // 10 seconds
    metric: 'Time until player can move'
  },

  breakdown: {
    htmlParse: {
      target: 200,    // HTML parsing
      critical: 500
    },
    jsDownload: {
      target: 1500,   // Download JS bundles
      critical: 3000
    },
    jsEval: {
      target: 800,    // Execute JS
      critical: 2000
    },
    essentialAssets: {
      target: 1500,   // Stage 1 assets (atlases, core)
      critical: 3000
    },
    worldGeneration: {
      target: 800,    // Generate spawn chunk
      critical: 1500
    },
    firstFrame: {
      target: 200,    // Render first frame
      critical: 500
    }
  }
}
```

**Measurement**: Lighthouse CI, Playwright E2E tests

---

## Bundle Size Budgets

### JavaScript Bundles

```typescript
export const BUNDLE_SIZE_BUDGETS = {
  // Gzipped sizes

  initialBundle: {
    target: 200,      // 200 KB (critical path)
    critical: 500,    // 500 KB
    includes: ['React', 'ECS core', 'Three.js core']
  },

  totalJS: {
    target: 2000,     // 2 MB total
    critical: 5000,   // 5 MB
    includes: ['All JS after code splitting']
  },

  breakdown: {
    vendor: {
      target: 800,    // React + Three.js + bitECS
      critical: 1500
    },
    game: {
      target: 1000,   // Game code
      critical: 2500
    },
    ui: {
      target: 200,    // React UI components
      critical: 500
    }
  }
}
```

**Enforcement**: Bundlesize CI check, fails PR if exceeded

---

## Asset Size Budgets

### Texture Budgets

```typescript
export const TEXTURE_BUDGETS = {
  atlases: {
    count: 4,
    sizePerAtlas: {
      target: 400,    // 400 KB per atlas
      critical: 800   // 800 KB
    },
    totalSize: {
      target: 1600,   // 1.6 MB total
      critical: 3200  // 3.2 MB
    },
    resolution: 2048  // 2048×2048 max
  },

  individual: {
    count: 100,
    totalSize: {
      target: 800,    // 800 KB
      critical: 1500  // 1.5 MB
    }
  }
}
```

### 3D Model Budgets

```typescript
export const MODEL_BUDGETS = {
  triangleCount: {
    character: {
      high: 500,      // LOD 0
      medium: 250,    // LOD 1
      low: 100        // LOD 2
    },
    building: {
      high: 600,
      medium: 300,
      low: 150
    },
    prop: {
      high: 200,
      medium: 100,
      low: 50
    }
  },

  fileSizes: {
    character: {
      target: 100,    // 100 KB per character
      critical: 200
    },
    building: {
      target: 150,
      critical: 300
    },
    prop: {
      target: 50,
      critical: 100
    }
  },

  totalModels: {
    count: 88,
    totalSize: {
      target: 6000,   // 6 MB
      critical: 10000 // 10 MB
    }
  }
}
```

### Audio Budgets

```typescript
export const AUDIO_BUDGETS = {
  sfx: {
    count: 80,
    sizePerFile: {
      target: 100,    // 100 KB per SFX
      critical: 200
    },
    totalSize: {
      target: 8000,   // 8 MB
      critical: 15000 // 15 MB
    }
  },

  music: {
    count: 8,
    sizePerTrack: {
      target: 2000,   // 2 MB per track (streamed)
      critical: 4000
    },
    totalSize: {
      target: 16000,  // 16 MB
      critical: 32000 // 32 MB
    }
  }
}
```

---

## Memory Budgets

### Heap Memory Usage

```typescript
export const MEMORY_BUDGETS = {
  heap: {
    target: 512,      // 512 MB
    critical: 1024,   // 1 GB
    test: 'Measure after 10 minutes gameplay'
  },

  breakdown: {
    ecs: {
      target: 50,     // bitECS (very efficient)
      critical: 100
    },
    textures: {
      target: 150,    // GPU textures in VRAM
      critical: 300
    },
    geometry: {
      target: 100,    // 3D model vertices/indices
      critical: 200
    },
    audio: {
      target: 50,     // Preloaded SFX
      critical: 100
    },
    other: {
      target: 162,    // React, game state, misc
      critical: 324
    }
  }
}
```

**Memory Leak Detection**:
- Heap snapshots every 5 minutes
- Alert if growth >10% over 30 minutes

---

## Draw Call Budgets

### Rendering Performance

```typescript
export const DRAW_CALL_BUDGETS = {
  total: {
    target: 100,      // 100 draw calls per frame
    critical: 200,
    test: 'Worst-case scene (city with 100 NPCs)'
  },

  breakdown: {
    terrain: {
      target: 10,     // Terrain chunks (1-2 per chunk)
      critical: 20
    },
    billboards: {
      target: 6,      // Characters/items (batched by atlas)
      critical: 12
    },
    buildings: {
      target: 30,     // City buildings (instanced)
      critical: 60
    },
    props: {
      target: 20,     // Trees, rocks (instanced)
      critical: 40
    },
    ui: {
      target: 10,     // React UI overlays
      critical: 20
    },
    effects: {
      target: 10,     // Particles, weather
      critical: 20
    },
    skybox: {
      target: 1,      // Sky dome
      critical: 2
    }
  }
}
```

**Triangle Budget per Frame**:
```typescript
export const TRIANGLE_BUDGETS = {
  total: {
    target: 100000,   // 100K triangles
    critical: 200000  // 200K triangles
  }
}
```

---

## Network Performance Budgets

### API Response Times

```typescript
export const API_BUDGETS = {
  authentication: {
    target: 200,      // 200ms
    critical: 1000,   // 1 second
    endpoint: 'POST /auth/login'
  },

  saveGame: {
    target: 500,      // 500ms
    critical: 2000,   // 2 seconds
    endpoint: 'POST /saves'
  },

  loadGame: {
    target: 500,
    critical: 2000,
    endpoint: 'GET /saves/:id'
  },

  analytics: {
    target: 100,      // Fire and forget
    critical: 500,
    endpoint: 'POST /analytics/event'
  },

  payment: {
    target: 1000,     // Stripe checkout
    critical: 5000,
    endpoint: 'POST /payments/create-session'
  }
}
```

### Bandwidth Budgets

```typescript
export const BANDWIDTH_BUDGETS = {
  initialLoad: {
    target: 10,       // 10 MB total download
    critical: 25      // 25 MB
  },

  saveSyncUp: {
    target: 150,      // 150 KB (compressed)
    critical: 500     // 500 KB
  },

  saveSyncDown: {
    target: 150,
    critical: 500
  }
}
```

---

## Database Performance Budgets

### Supabase Query Performance

```typescript
export const DATABASE_BUDGETS = {
  saveInsert: {
    target: 100,      // 100ms
    critical: 500,
    query: 'INSERT INTO saves'
  },

  saveQuery: {
    target: 50,       // 50ms
    critical: 200,
    query: 'SELECT * FROM saves WHERE user_id'
  },

  leaderboardQuery: {
    target: 100,
    critical: 500,
    query: 'SELECT * FROM leaderboard ORDER BY score LIMIT 100'
  },

  analyticsInsert: {
    target: 50,       // Fast async insert
    critical: 200,
    query: 'INSERT INTO analytics'
  }
}
```

---

## Progressive Loading Budget

### 4-Stage Loading Performance

```typescript
export const PROGRESSIVE_LOADING_BUDGETS = {
  stage1_essential: {
    assets: ['atlases', 'core_models', 'player_sfx'],
    size: {
      target: 3000,   // 3 MB
      critical: 6000  // 6 MB
    },
    time: {
      target: 1500,   // 1.5 seconds
      critical: 3000
    }
  },

  stage2_nearby: {
    assets: ['nearby_chunks', 'environment_sfx', 'ui_assets'],
    size: {
      target: 5000,   // 5 MB
      critical: 10000
    },
    time: {
      target: 2000,   // 2 seconds (background)
      critical: 4000
    }
  },

  stage3_extended: {
    assets: ['extended_chunks', 'dungeon_assets', 'music'],
    size: {
      target: 10000,  // 10 MB
      critical: 20000
    },
    time: {
      target: 5000,   // 5 seconds (background)
      critical: 10000
    }
  },

  stage4_distant: {
    assets: ['distant_chunks', 'optional_assets'],
    size: {
      target: 15000,  // 15 MB
      critical: 30000
    },
    time: {
      target: 10000,  // 10 seconds (background)
      critical: 20000
    }
  }
}
```

---

## World Streaming Budgets

### Chunk Loading Performance

```typescript
export const CHUNK_BUDGETS = {
  generation: {
    target: 50,       // 50ms to generate chunk
    critical: 200,    // 200ms
    size: '128×128m'
  },

  loading: {
    target: 100,      // 100ms to load from cache
    critical: 500
  },

  concurrentChunks: {
    target: 3,        // Load 3 chunks simultaneously
    critical: 5
  },

  visibleChunks: {
    target: 9,        // 3×3 grid around player
    critical: 25      // 5×5 grid
  }
}
```

---

## CI/CD Performance Tests

### Automated Budget Enforcement

```typescript
// vitest.config.ts performance thresholds

export default defineConfig({
  test: {
    performance: {
      frameTime: {
        target: 16.67,
        samples: 300,
        failThreshold: 0.95  // 95% must hit target
      },
      memory: {
        maxHeap: 512,         // MB
        samples: 10,
        interval: 60000       // 1 minute
      },
      bundleSize: {
        initial: 200,         // KB
        total: 2000
      }
    }
  }
})
```

### GitHub Actions CI Check

```yaml
# .github/workflows/performance.yml

name: Performance Budget Check

on: [push, pull_request]

jobs:
  performance:
    runs-on: ubuntu-latest
    steps:
      - name: Bundle Size Check
        run: npm run bundlesize
        # Fails if any bundle exceeds critical threshold

      - name: Lighthouse CI
        run: npm run lighthouse:ci
        # Fails if time-to-playable >10s

      - name: Performance Tests
        run: npm run test:performance
        # Fails if frame time >33ms for 5% of frames

      - name: Memory Leak Test
        run: npm run test:memory
        # Fails if heap growth >10% over 30 min
```

---

## Performance Monitoring

### Real-Time Metrics (Production)

```typescript
export const PRODUCTION_MONITORING = {
  metrics: {
    fps: {
      alert: 'FPS < 45 for >5% of users',
      severity: 'high'
    },
    loadTime: {
      alert: 'Time-to-playable > 8s for >10% of users',
      severity: 'critical'
    },
    crashRate: {
      alert: 'Crash rate > 5%',
      severity: 'critical'
    },
    memoryLeaks: {
      alert: 'Memory growth >20% over 1 hour',
      severity: 'high'
    }
  },

  sampling: {
    rate: 0.1,        // Sample 10% of users
    interval: 60000   // Report every minute
  }
}
```

---

## Platform-Specific Budgets

### Hardware Tiers

**Low-End (Minimum Spec)**
- CPU: 2 cores, 2.0 GHz
- GPU: Intel HD 4000
- RAM: 4 GB
- Target: 30 FPS on Low settings

**Mid-Range (Recommended)**
- CPU: 4 cores, 2.5 GHz
- GPU: GTX 1050 / RX 560
- RAM: 8 GB
- Target: 60 FPS on Medium settings

**High-End (Optimal)**
- CPU: 6+ cores, 3.0 GHz
- GPU: RTX 2060 / RX 5700
- RAM: 16 GB
- Target: 60 FPS on High settings

### Browser-Specific Adjustments

```typescript
export const BROWSER_BUDGETS = {
  chrome: {
    frameTimeMultiplier: 1.0,   // Baseline
    memoryMultiplier: 1.0
  },
  firefox: {
    frameTimeMultiplier: 1.1,   // Slightly slower WebGL
    memoryMultiplier: 1.2       // Higher memory usage
  },
  safari: {
    frameTimeMultiplier: 1.15,  // Slower JS engine
    memoryMultiplier: 0.9       // Better memory management
  }
}
```

---

## Budget Degradation Strategy

### Adaptive Quality Settings

When budgets exceeded, automatically reduce quality:

```typescript
export const DEGRADATION_STRATEGY = {
  level1: {
    trigger: 'FPS < 55 for 10 seconds',
    actions: [
      'Reduce shadow quality',
      'Disable ambient occlusion',
      'Reduce particle count by 50%'
    ]
  },

  level2: {
    trigger: 'FPS < 45 for 10 seconds',
    actions: [
      'Disable shadows',
      'Reduce view distance by 25%',
      'Disable weather effects',
      'Reduce LOD distances'
    ]
  },

  level3: {
    trigger: 'FPS < 30 for 10 seconds',
    actions: [
      'Reduce view distance by 50%',
      'Disable all post-processing',
      'Switch to low-poly LODs',
      'Reduce NPC count in cities'
    ]
  },

  recovery: {
    trigger: 'FPS > 58 for 30 seconds',
    action: 'Restore previous quality level'
  }
}
```

---

## Testing Environments

### Performance Test Scenarios

1. **Idle Scene** (baseline)
   - Player in empty chunk
   - Target: <5ms frame time

2. **Light Load** (outdoor exploration)
   - 3×3 terrain chunks
   - 10 NPCs, 20 props
   - Target: <12ms frame time

3. **Medium Load** (town)
   - Town with 20 buildings
   - 50 NPCs
   - Target: <16ms frame time

4. **Heavy Load** (city)
   - City with 100 buildings
   - 100 NPCs, weather effects
   - Target: <16ms frame time (critical: <33ms)

5. **Stress Test** (worst case)
   - Large city + combat + weather
   - 150+ NPCs
   - Target: <33ms frame time

---

## Budget Review Schedule

### Monthly Performance Reviews

- Week 1 of each month: Run full performance test suite
- Analyze trends (improving/degrading)
- Adjust budgets if consistently exceeded
- Plan optimization sprints if needed

### Quarterly Optimization Sprints

- Dedicated 1-2 week sprints every 3 months
- Focus on biggest performance bottlenecks
- Target: 10-20% improvement per sprint

---

## Related Documents

- [02-TECHNICAL-ARCHITECTURE.md](./02-TECHNICAL-ARCHITECTURE.md) - Systems contributing to budgets
- [05-TESTING-STRATEGY.md](./05-TESTING-STRATEGY.md) - Performance testing strategy
- [06-ASSET-SPECIFICATION-SHEET.md](./06-ASSET-SPECIFICATION-SHEET.md) - Asset size budgets

---

**Last Updated**: 2024-11-15
**Document Version**: 1.0.0
**Status**: Complete - All performance budgets defined and enforceable

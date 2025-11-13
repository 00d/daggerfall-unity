# Technical Architecture - Daggerfall Unity Web Port

## Architecture Overview

This document describes the core technical architecture for the Daggerfall Unity Web Port, including all systems, technologies, and design patterns.

---

## 1. Core Technologies

### Game Engine Stack
- **ECS Framework**: bitECS v0.3.x
- **Rendering**: Three.js r159+ (WebGL 2.0, WebGPU support)
- **Physics**: Custom kinematic character controller
- **Audio**: Web Audio API
- **UI**: React 18+ with TypeScript

### Build & Development
- **Language**: TypeScript 5+ (strict mode)
- **Build Tool**: Vite 5.x with code splitting
- **Package Manager**: pnpm 8.x
- **Monorepo Structure**: pnpm workspaces
- **Testing**: Vitest (unit), Playwright (E2E)
- **CI/CD**: GitHub Actions

### Backend Services
- **Database**: Supabase (PostgreSQL 15)
- **Authentication**: Supabase Auth
- **Storage**: Supabase Storage
- **Payments**: Stripe API v2023+
- **CDN**: Cloudflare
- **Error Tracking**: Sentry
- **Analytics**: Custom (Supabase)

---

## 2. Entity-Component-System (ECS) Architecture

### Why bitECS?

**Performance Characteristics:**
- 10-100x faster than traditional ECS libraries
- Memory-efficient typed arrays (cache-friendly)
- Minimal garbage collection pressure
- Supports 100,000+ entities at 60 FPS

### Core Components

```typescript
import { defineComponent, Types } from 'bitecs'

// Transform component (position, rotation, scale)
export const Transform = defineComponent({
  x: Types.f32, y: Types.f32, z: Types.f32,
  rotX: Types.f32, rotY: Types.f32, rotZ: Types.f32, rotW: Types.f32,
  scaleX: Types.f32, scaleY: Types.f32, scaleZ: Types.f32,
})

// Velocity component (movement)
export const Velocity = defineComponent({
  x: Types.f32, y: Types.f32, z: Types.f32,
})

// Character controller component
export const CharacterController = defineComponent({
  walkSpeed: Types.f32,
  runSpeed: Types.f32,
  jumpForce: Types.f32,
  climbSpeed: Types.f32,
  swimSpeed: Types.f32,
  isGrounded: Types.ui8,
  isClimbing: Types.ui8,
  isSwimming: Types.ui8,
})

// Health component
export const Health = defineComponent({
  current: Types.ui16,
  max: Types.ui16,
  regen: Types.f32,
})

// Rendering component (links to Three.js objects)
export const RenderMesh = defineComponent({
  meshId: Types.ui32,  // ID into mesh registry
  visible: Types.ui8,
  castShadows: Types.ui8,
  receiveShadows: Types.ui8,
})
```

### System Pipeline

**Fixed Update (Physics) - 60 times/second:**
```typescript
export const FIXED_SYSTEMS = [
  InputSystem,           // Process player input
  MovementSystem,        // Apply velocity to transforms
  PhysicsSystem,         // Character controller, collision
  ClimbingMotorSystem,   // Climbing mechanics
  SwimmingMotorSystem,   // Swimming mechanics
  LevitationMotorSystem, // Levitation/flying
  FrictionSystem,        // Ground friction
  GravitySystem,         // Apply gravity
]
```

**Variable Update (Rendering) - Every frame:**
```typescript
export const RENDER_SYSTEMS = [
  RenderSystem,          // Sync ECS → Three.js
  BillboardSystem,       // Update billboards to face camera
  AnimationSystem,       // Update character animations
  ParticleSystem,        // Update particle effects
  AudioSystem,           // Update 3D audio positions
]
```

**Slow Update (Game Logic) - 10 times/second:**
```typescript
export const LOGIC_SYSTEMS = [
  NPCAISystem,           // NPC decision making
  QuestSystem,           // Quest progression
  CombatSystem,          // Damage calculation
  InventorySystem,       // Inventory management
  WeatherSystem,         // Weather changes
]
```

### Serialization Strategy

**Serializable Components** (saved to disk):
- Transform, Health, Inventory, QuestState, PlayerState

**Runtime-Only Components** (reconstructed on load):
- Velocity, RenderMesh, AudioSource, Collider

---

## 3. Physics System (Custom Kinematic)

### Why Custom Over Rapier?

| Aspect | Rapier | Custom Kinematic |
|--------|--------|------------------|
| **Bundle Size** | ~400 KB | ~5-10 KB |
| **Features** | Full physics simulation | Character movement only |
| **Complexity** | High (rigid bodies, constraints) | Low (collision checks) |
| **Control** | Less direct | Full control |
| **Suitability** | Overkill for Daggerfall | Perfect fit |

### Character Controller Implementation

```typescript
export class KinematicController {
  private raycaster = new THREE.Raycaster()
  private collisionMeshes: THREE.Mesh[] = []

  updateController(world: IWorld, eid: number, deltaTime: number): void {
    // 1. Check if grounded
    const groundCheck = this.checkGrounded(
      position,
      Collider.radius[eid],
      Collider.height[eid]
    )
    CharacterController.isGrounded[eid] = groundCheck.isGrounded ? 1 : 0

    // 2. Apply movement
    const velocity = new THREE.Vector3(
      Velocity.x[eid],
      Velocity.y[eid],
      Velocity.z[eid]
    )

    const desiredMove = velocity.clone().multiplyScalar(deltaTime)

    // 3. Collision detection (sweep test)
    const collisionResult = this.sweepTest(
      position,
      desiredMove.normalize(),
      desiredMove.length(),
      Collider.radius[eid],
      Collider.height[eid]
    )

    // 4. Slide along walls if hit
    if (collisionResult.hit) {
      const slideDirection = desiredMove
        .clone()
        .projectOnPlane(collisionResult.normal)
        .normalize()
      position.add(slideDirection.multiplyScalar(slideDistance))
    } else {
      position.add(desiredMove)
    }

    // 5. Update transform
    Transform.x[eid] = position.x
    Transform.y[eid] = position.y
    Transform.z[eid] = position.z
  }

  private sweepTest(
    start: THREE.Vector3,
    direction: THREE.Vector3,
    distance: number,
    radius: number,
    height: number
  ): CollisionResult {
    // Cast capsule shape along movement direction
    // Return hit point, normal, distance if collision detected
    // Implementation uses raycasting in multiple directions
  }
}
```

### Motor Systems

**Climbing Motor:**
- Detect climbable surfaces (ladders, walls with handholds)
- Override gravity when climbing
- Allow movement in cardinal directions

**Swimming Motor:**
- Detect water volume
- Apply buoyancy force
- Slower movement speed
- Oxygen tracking (drowning after 60s)

**Levitation Motor:**
- Allow vertical movement
- No gravity applied
- Slower than running
- Magicka cost over time

---

## 4. Rendering System (Three.js)

### Renderer Configuration

```typescript
export class GameRenderer {
  private renderer: THREE.WebGLRenderer
  private scene: THREE.Scene
  private camera: THREE.PerspectiveCamera

  constructor(config: RendererConfig) {
    this.renderer = new THREE.WebGLRenderer({
      canvas: config.canvas,
      antialias: config.antialias,
      powerPreference: 'high-performance',
      alpha: false,
      stencil: false,
      preserveDrawingBuffer: false,
    })

    // Cap pixel ratio for performance (max 1.5 on high-DPI displays)
    const pixelRatio = Math.min(window.devicePixelRatio, config.maxPixelRatio)
    this.renderer.setPixelRatio(pixelRatio)

    // Enable shadows
    this.renderer.shadowMap.enabled = config.shadows
    this.renderer.shadowMap.type = THREE.PCFSoftShadowMap

    // Tone mapping for better lighting
    this.renderer.toneMapping = THREE.ACESFilmicToneMapping
    this.renderer.toneMappingExposure = 1.0
    this.renderer.outputEncoding = THREE.sRGBEncoding
  }
}
```

### Billboard Batching System

**Problem**: Individual billboards = too many draw calls (100+ NPCs = 100 draw calls)

**Solution**: Batch by texture atlas using InstancedMesh

```typescript
export class BillboardBatcher {
  private batches = new Map<string, THREE.InstancedMesh>()

  updateBatch(atlasKey: string, entities: number[]) {
    let batch = this.batches.get(atlasKey)

    if (!batch) {
      // Create instanced mesh (max 256 instances per atlas)
      batch = new THREE.InstancedMesh(
        this.billboardGeometry,
        this.createAtlasMaterial(atlasKey),
        256
      )
      this.batches.set(atlasKey, batch)
      this.scene.add(batch)
    }

    // Update instance matrices from ECS components
    for (let i = 0; i < entities.length; i++) {
      const eid = entities[i]
      const matrix = new THREE.Matrix4()
      matrix.makeTranslation(
        Transform.x[eid],
        Transform.y[eid],
        Transform.z[eid]
      )

      // Billboard rotation (face camera)
      matrix.lookAt(
        new THREE.Vector3(Transform.x[eid], Transform.y[eid], Transform.z[eid]),
        this.camera.position,
        new THREE.Vector3(0, 1, 0)
      )

      batch.setMatrixAt(i, matrix)
    }

    batch.count = entities.length
    batch.instanceMatrix.needsUpdate = true
  }
}

// Result: 100 billboards = 4-6 draw calls (one per atlas)
```

### Material System

```typescript
export class MaterialCache {
  private cache = new Map<string, THREE.Material>()
  private lastAccess = new Map<string, number>()

  getMaterial(materialId: string): THREE.Material {
    let material = this.cache.get(materialId)

    if (!material) {
      material = this.createMaterial(materialId)
      this.cache.set(materialId, material)
    }

    // Track access time for LRU eviction
    this.lastAccess.set(materialId, Time.realtimeSinceStartup)

    return material
  }

  pruneCache(currentTime: number, threshold: number) {
    for (const [id, lastTime] of this.lastAccess) {
      if (currentTime - lastTime > threshold) {
        const material = this.cache.get(id)
        material?.dispose()
        this.cache.delete(id)
        this.lastAccess.delete(id)
      }
    }
  }
}
```

### Retro Renderer (320×200 / 640×400 Mode)

```typescript
export class RetroRenderer {
  private renderTarget: THREE.WebGLRenderTarget
  private dithering: boolean = true

  constructor(width: number, height: number) {
    // Low-res render target
    this.renderTarget = new THREE.WebGLRenderTarget(width, height, {
      minFilter: THREE.NearestFilter,
      magFilter: THREE.NearestFilter,
      format: THREE.RGBFormat,
    })
  }

  render(scene: THREE.Scene, camera: THREE.Camera) {
    // Render to low-res target
    this.renderer.setRenderTarget(this.renderTarget)
    this.renderer.render(scene, camera)

    // Apply dithering if enabled
    if (this.dithering) {
      this.applyDithering()
    }

    // Scale up to screen with nearest-neighbor filtering
    this.renderer.setRenderTarget(null)
    this.renderQuad(this.renderTarget.texture)
  }
}
```

---

## 5. World Streaming & Terrain Generation

### Chunk-Based Streaming

**Configuration:**
```typescript
export const WORLD_CONFIG = {
  chunkSize: 128,           // 128m × 128m chunks
  viewDistance: 3,          // 3 chunks radius = 7×7 grid = 49 chunks
  maxChunks: 64,            // Memory limit
  lodLevels: 3,             // LOD0, LOD1, LOD2
  floatingOriginThreshold: 10000,  // 10km
}
```

**Chunk Loading Strategy:**
```typescript
export class WorldStreamer {
  private chunks = new Map<string, TerrainChunk>()
  private loadQueue: ChunkCoord[] = []

  update(playerPosition: THREE.Vector3) {
    const playerChunk = this.worldToChunk(playerPosition)

    // Determine required chunks
    const requiredChunks = this.getChunksInRadius(
      playerChunk,
      WORLD_CONFIG.viewDistance
    )

    // Load new chunks (prioritized by distance)
    for (const coord of requiredChunks) {
      const key = this.coordToKey(coord)
      if (!this.chunks.has(key)) {
        this.queueChunkLoad(coord, playerPosition)
      }
    }

    // Unload distant chunks
    for (const [key, chunk] of this.chunks) {
      const distance = this.getChunkDistance(chunk.coord, playerChunk)
      if (distance > WORLD_CONFIG.viewDistance + 1) {
        this.unloadChunk(key)
      }
    }

    // Process load queue (max 1 per frame)
    if (this.loadQueue.length > 0) {
      const coord = this.loadQueue.shift()!
      this.loadChunk(coord)
    }

    // Check floating origin reset
    if (playerPosition.length() > WORLD_CONFIG.floatingOriginThreshold) {
      this.performFloatingOriginReset(playerPosition)
    }
  }

  private async loadChunk(coord: ChunkCoord): Promise<void> {
    // Generate terrain
    const terrain = await this.terrainGenerator.generate(coord)

    // Generate collision mesh
    const collisionMesh = this.generateCollisionMesh(terrain)

    // Check for locations (cities, dungeons)
    const locations = this.locationManager.getLocationsInChunk(coord)

    for (const location of locations) {
      if (location.type === 'city' || location.type === 'town') {
        const settlement = await this.settlementGenerator.generate(location)
        terrain.settlements.push(settlement)
      } else if (location.type === 'dungeon') {
        terrain.dungeonEntrances.push(location)
      }
    }

    // Add to scene
    this.scene.add(terrain.mesh)
    this.physics.registerCollisionMesh(collisionMesh)

    // Store chunk
    const key = this.coordToKey(coord)
    this.chunks.set(key, {
      coord,
      terrain,
      collisionMesh,
      settlements: terrain.settlements,
    })
  }
}
```

### Terrain Generation (Procedural)

```typescript
export class TerrainGenerator {
  private noise: SimplexNoise

  generate(coord: ChunkCoord): TerrainData {
    const seed = this.worldSeed + coord.x * 1000 + coord.y
    this.noise = new SimplexNoise(seed)

    // Generate height map
    const heightMap = this.generateHeightMap(coord)

    // Determine biome
    const biome = this.selectBiome(coord)

    // Generate mesh
    const geometry = this.createTerrainGeometry(heightMap, WORLD_CONFIG.chunkSize)
    const material = this.createTerrainMaterial(biome)
    const mesh = new THREE.Mesh(geometry, material)

    return {
      coord,
      heightMap,
      biome,
      mesh,
    }
  }

  private generateHeightMap(coord: ChunkCoord): Float32Array {
    const size = WORLD_CONFIG.chunkSize + 1  // 129×129 vertices
    const heightMap = new Float32Array(size * size)

    for (let y = 0; y < size; y++) {
      for (let x = 0; x < size; x++) {
        const worldX = coord.x * WORLD_CONFIG.chunkSize + x
        const worldY = coord.y * WORLD_CONFIG.chunkSize + y

        // Multi-octave Perlin noise
        let height = 0
        let amplitude = 1
        let frequency = 0.005

        for (let octave = 0; octave < 4; octave++) {
          height += this.noise.noise2D(
            worldX * frequency,
            worldY * frequency
          ) * amplitude

          amplitude *= 0.5
          frequency *= 2
        }

        // Scale to 0-100m range
        height = (height + 1) * 50

        heightMap[y * size + x] = height
      }
    }

    return heightMap
  }

  private selectBiome(coord: ChunkCoord): BiomeType {
    // Use separate noise for biome selection
    const biomeNoise = this.noise.noise2D(coord.x * 0.01, coord.y * 0.01)

    if (biomeNoise < -0.6) return 'snow'
    if (biomeNoise < -0.3) return 'mountain'
    if (biomeNoise < 0.0) return 'temperate'
    if (biomeNoise < 0.3) return 'grassland'
    if (biomeNoise < 0.6) return 'swamp'
    return 'desert'
  }
}
```

### Floating Origin System

**Problem**: JavaScript loses precision beyond ~1,000,000 units (floating point)

**Solution**: Reset world origin when player travels >10km

```typescript
function performFloatingOriginReset(playerPosition: THREE.Vector3) {
  const offset = playerPosition.clone().negate()

  // 1. Shift all ECS entities
  const entities = transformQuery(world)
  for (const eid of entities) {
    Transform.x[eid] += offset.x
    Transform.y[eid] += offset.y
    Transform.z[eid] += offset.z
  }

  // 2. Shift all Three.js objects
  scene.traverse((obj) => {
    if (obj.isObject3D) {
      obj.position.add(offset)
    }
  })

  // 3. Shift camera
  camera.position.add(offset)

  // 4. Shift physics collision meshes
  for (const mesh of physics.collisionMeshes) {
    mesh.position.add(offset)
  }

  // 5. Update chunk coordinates
  for (const [key, chunk] of worldStreamer.chunks) {
    chunk.worldOffset.add(offset)
  }
}
```

---

## 6. Progressive Loading System

### 4-Stage Loading Strategy

```typescript
export const LOADING_STAGES = {
  // Stage 0: Critical (already loaded before JS runs)
  // - index.html, critical CSS

  // Stage 1: Essential (1-3 seconds)
  stage1: {
    priority: 100,
    assets: [
      'engine-core.js',              // 500 KB
      'ecs-systems.js',              // 300 KB
      'character-controller.js',     // 50 KB
      'player-model.gltf',           // 150 KB
      'atlas-characters.webp',       // 250 KB
      'atlas-items.webp',            // 200 KB
      'atlas-environment.webp',      // 300 KB
      'ui-fonts.woff2',              // 240 KB
      'starting-chunk.bin',          // 500 KB
    ],
    totalSize: '~2.5 MB',
    targetTime: '2 seconds'
  },

  // Stage 2: Immediate (3-5 seconds)
  stage2: {
    priority: 80,
    assets: [
      'rendering-systems.js',        // 200 KB
      'audio-system.js',             // 100 KB
      'surrounding-chunks.bin',      // 2 MB
      'building-models-lod0.glb',    // 1 MB
    ],
    totalSize: '~3.3 MB',
    targetTime: '3 seconds'
  },

  // Stage 3: Playable (5 seconds) ← USER CAN START PLAYING

  // Stage 4: Background (load while playing)
  stage4: {
    priority: 20,
    assets: [
      'distant-chunks.bin',          // 10 MB
      'dungeon-blocks.glb',          // 5 MB
      'city-buildings.glb',          // 8 MB
      'music-tracks.opus',           // 24 MB
    ],
    totalSize: '~47 MB',
    targetTime: 'Background loading'
  }
}
```

---

## 7. Save System Architecture

### Save Data Structure

```typescript
interface SaveGameData {
  version: string
  timestamp: number
  playTime: number

  player: {
    position: [number, number, number]
    rotation: [number, number, number, number]
    health: { current: number, max: number }
    magicka: { current: number, max: number }
    stamina: { current: number, max: number }
    level: number
    experience: number
    skills: Record<string, number>
    gold: number
  }

  inventory: {
    items: Array<{ id: number, count: number }>
    equipped: {
      weapon: number | null
      armor: number[]
      accessories: number[]
    }
  }

  quests: {
    active: number[]
    completed: number[]
    failed: number[]
    questData: Record<number, any>
  }

  world: {
    discoveredLocations: number[]
    currentLocation: number
    timeOfDay: number
    daysPassed: number
  }

  // Only changed entities (delta from new game)
  modifiedEntities: Array<{
    id: number
    components: Record<string, any>
  }>
}
```

### Compression Strategy

```typescript
export class SaveManager {
  async saveGame(data: SaveGameData, saveName: string): Promise<void> {
    // 1. Optimize data (remove unchanged from defaults)
    const optimized = this.optimizeForStorage(data)

    // 2. Serialize to JSON
    const json = JSON.stringify(optimized)

    // 3. Compress with pako (gzip)
    const compressed = pako.gzip(json)

    // Target: 100-150 KB (vs 500 KB uncompressed)
    console.log(`Save size: ${compressed.length} bytes`)

    // 4. Upload to Supabase
    if (this.authManager.isSignedIn()) {
      await this.uploadToCloud(compressed, saveName)
    } else {
      await this.saveToLocalStorage(compressed, saveName)
    }
  }

  private optimizeForStorage(data: SaveGameData): Partial<SaveGameData> {
    return {
      // Use shorter keys
      v: data.version,
      t: data.timestamp,
      p: {
        pos: data.player.position,
        hp: data.player.health.current,  // Only current, recalc max from level
        lv: data.player.level,
      },
      // Only save discovered locations, not all 15,000
      w: {
        disc: data.world.discoveredLocations,
        loc: data.world.currentLocation,
      },
      // Delta encoding: only entities that changed
      e: data.modifiedEntities.filter(e => e.id > 1000)  // Skip static world entities
    }
  }
}
```

---

## Related Documents

- [03-CRITICAL-GAPS-ANALYSIS.md](./03-CRITICAL-GAPS-ANALYSIS.md) - Missing systems
- [04-REVISED-24-MONTH-ROADMAP.md](./04-REVISED-24-MONTH-ROADMAP.md) - Implementation timeline
- [06-ASSET-SPECIFICATION-SHEET.md](./06-ASSET-SPECIFICATION-SHEET.md) - Asset details
- [07-PERFORMANCE-BUDGETS.md](./07-PERFORMANCE-BUDGETS.md) - Performance targets

---

**Last Updated**: 2024-11-15
**Document Version**: 1.0.0

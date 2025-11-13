# Asset Specification Sheet - Daggerfall Unity Web Port

## Overview

Complete specifications for all programmer art assets used during development (Phases 1-4). These assets prioritize fast iteration, small file size, and clear visual distinction over final quality.

**Strategy**: Build with programmer art → Replace with final assets (Months 15-24)

---

## Asset Philosophy

### Why Programmer Art?

1. **Fast Iteration** - No waiting for artists
2. **Small Size** - 5-10MB total vs 450MB final assets
3. **Clear Hierarchy** - Easy to identify what needs replacement
4. **Budget Friendly** - Final art commissioned only after validation

### Replacement Timeline

| Month | Category | Budget |
|-------|----------|--------|
| 15-16 | Terrain & Environment | $5K-$8K |
| 18-19 | Characters & Items | $8K-$12K |
| 19-20 | Buildings & Props | $6K-$10K |
| 21-22 | Audio (SFX & Music) | $4K-$8K |
| 23-24 | UI & Fonts | $2K-$5K |

**Total Final Art Budget**: $25K-$43K

---

## Asset Inventory Summary

| Category | Count | Size | File Format |
|----------|-------|------|-------------|
| **Textures** (individual) | 100 | ~800 KB | WebP |
| **Texture Atlases** | 4 | ~1.5 MB | WebP |
| **3D Models** | 88 | ~6.2 MB | glTF 2.0 |
| **Audio (SFX)** | 80 | ~8 MB | OGG Vorbis |
| **Audio (Music)** | 8 | ~16 MB | OGG Vorbis (streaming) |
| **UI Elements** | 50 | ~300 KB | WebP + SVG |
| **Fonts** | 4 | ~200 KB | WOFF2 |
| **Total** | 334 assets | ~33 MB | - |

---

## TEXTURES

### Individual Textures (100 assets, ~800 KB)

**Terrain (20 textures)**

| ID | Name | Size | Colors | Description |
|----|------|------|--------|-------------|
| T001 | grass.webp | 128×128 | #4CAF50 | Bright green with noise |
| T002 | dirt.webp | 128×128 | #8D6E63 | Brown with texture |
| T003 | sand.webp | 128×128 | #FFE082 | Yellow-tan desert |
| T004 | snow.webp | 128×128 | #ECEFF1 | White with blue tint |
| T005 | stone.webp | 128×128 | #757575 | Grey rocky texture |
| T006 | mud.webp | 128×128 | #6D4C41 | Dark brown wet |
| T007 | gravel.webp | 128×128 | #9E9E9E | Mixed grey stones |
| T008 | grass_dry.webp | 128×128 | #C5A880 | Dried yellow grass |
| T009 | moss.webp | 128×128 | #558B2F | Dark green organic |
| T010 | ice.webp | 128×128 | #B3E5FC | Light blue frozen |
| T011-T020 | (variations) | 128×128 | Various | Biome variations |

**Buildings (15 textures)**

| ID | Name | Size | Colors | Description |
|----|------|------|--------|-------------|
| B001 | brick_red.webp | 256×256 | #D32F2F | Red brick pattern |
| B002 | brick_grey.webp | 256×256 | #616161 | Grey stone brick |
| B003 | wood_planks.webp | 256×256 | #8D6E63 | Brown wood horizontal |
| B004 | thatch_roof.webp | 256×256 | #FFE082 | Yellow straw |
| B005 | shingles.webp | 256×256 | #424242 | Dark grey tiles |
| B006 | plaster_white.webp | 256×256 | #FAFAFA | Off-white walls |
| B007 | plaster_beige.webp | 256×256 | #BCAAA4 | Tan walls |
| B008 | door_wood.webp | 128×128 | #6D4C41 | Dark brown door |
| B009 | window_glass.webp | 64×64 | #90CAF9 | Light blue glass |
| B010 | cobblestone.webp | 256×256 | #757575 | Grey street stones |
| B011-B015 | (variations) | Various | Various | Additional materials |

**Characters (10 textures)**

| ID | Name | Size | Colors | Description |
|----|------|------|--------|-------------|
| C001 | player_body.webp | 256×256 | #2196F3 | Blue humanoid |
| C002 | npc_male.webp | 256×256 | #4CAF50 | Green humanoid |
| C003 | npc_female.webp | 256×256 | #E91E63 | Pink humanoid |
| C004 | guard.webp | 256×256 | #F44336 | Red guard uniform |
| C005 | merchant.webp | 256×256 | #FF9800 | Orange merchant |
| C006 | enemy_goblin.webp | 128×128 | #8BC34A | Light green enemy |
| C007 | enemy_skeleton.webp | 128×128 | #EEEEEE | White bones |
| C008 | enemy_rat.webp | 64×64 | #795548 | Brown rodent |
| C009 | enemy_spider.webp | 128×128 | #424242 | Black spider |
| C010 | pet_dog.webp | 128×128 | #A1887F | Tan dog |

**Items (20 textures)**

| ID | Name | Size | Colors | Description |
|----|------|------|--------|-------------|
| I001 | sword_iron.webp | 64×64 | #9E9E9E | Grey blade |
| I002 | sword_steel.webp | 64×64 | #E0E0E0 | Silver blade |
| I003 | bow_wood.webp | 64×64 | #8D6E63 | Brown bow |
| I004 | staff_magic.webp | 64×64 | #9C27B0 | Purple staff |
| I005 | shield_wood.webp | 64×64 | #6D4C41 | Brown shield |
| I006 | armor_leather.webp | 64×64 | #795548 | Brown armor |
| I007 | armor_chain.webp | 64×64 | #BDBDBD | Grey chainmail |
| I008 | helmet_iron.webp | 64×64 | #757575 | Grey helmet |
| I009 | potion_health.webp | 32×32 | #F44336 | Red bottle |
| I010 | potion_mana.webp | 32×32 | #2196F3 | Blue bottle |
| I011 | coin_gold.webp | 32×32 | #FFD700 | Yellow coin |
| I012 | gem_ruby.webp | 32×32 | #E91E63 | Red gem |
| I013 | gem_sapphire.webp | 32×32 | #2196F3 | Blue gem |
| I014 | key_brass.webp | 32×32 | #FFA000 | Gold key |
| I015 | scroll.webp | 32×32 | #FFF9C4 | Yellow parchment |
| I016 | book.webp | 32×32 | #5D4037 | Brown book |
| I017 | food_bread.webp | 32×32 | #FFE082 | Tan bread |
| I018 | food_meat.webp | 32×32 | #D32F2F | Red meat |
| I019 | torch.webp | 32×32 | #FF5722 | Orange flame |
| I020 | rope.webp | 32×32 | #8D6E63 | Brown rope |

**Environment (15 textures)**

| ID | Name | Size | Colors | Description |
|----|------|------|--------|-------------|
| E001 | tree_bark.webp | 128×128 | #5D4037 | Brown trunk |
| E002 | tree_leaves.webp | 128×128 | #4CAF50 | Green foliage |
| E003 | rock_grey.webp | 128×128 | #757575 | Grey boulder |
| E004 | water.webp | 128×128 | #2196F3 | Blue water |
| E005 | lava.webp | 128×128 | #FF5722 | Red lava |
| E006 | crystal_blue.webp | 64×64 | #00BCD4 | Cyan crystal |
| E007 | mushroom_red.webp | 64×64 | #F44336 | Red cap |
| E008 | vine.webp | 64×64 | #558B2F | Dark green vine |
| E009 | flower_yellow.webp | 32×32 | #FFEB3B | Yellow flower |
| E010 | flower_purple.webp | 32×32 | #9C27B0 | Purple flower |
| E011-E015 | (variations) | Various | Various | Additional props |

**Effects (10 textures)**

| ID | Name | Size | Colors | Description |
|----|------|------|--------|-------------|
| FX01 | particle_smoke.webp | 32×32 | #9E9E9E | Grey smoke |
| FX02 | particle_fire.webp | 32×32 | #FF5722 | Orange fire |
| FX03 | particle_magic.webp | 32×32 | #9C27B0 | Purple sparkle |
| FX04 | particle_blood.webp | 32×32 | #D32F2F | Red splatter |
| FX05 | particle_dust.webp | 32×32 | #BCAAA4 | Tan dust |
| FX06 | lightning.webp | 64×64 | #FFEB3B | Yellow bolt |
| FX07 | explosion.webp | 64×64 | #FF9800 | Orange blast |
| FX08 | heal_glow.webp | 64×64 | #4CAF50 | Green aura |
| FX09 | shield_bubble.webp | 64×64 | #2196F3 | Blue shield |
| FX10 | teleport.webp | 64×64 | #00BCD4 | Cyan portal |

**UI (10 textures)**

| ID | Name | Size | Colors | Description |
|----|------|------|--------|-------------|
| UI01 | button_normal.webp | 128×32 | #616161 | Grey button |
| UI02 | button_hover.webp | 128×32 | #757575 | Light grey |
| UI03 | button_pressed.webp | 128×32 | #424242 | Dark grey |
| UI04 | panel_bg.webp | 256×256 | #37474F | Dark blue-grey |
| UI05 | inventory_slot.webp | 64×64 | #546E7A | Medium grey |
| UI06 | health_bar_bg.webp | 128×16 | #424242 | Dark bar |
| UI07 | health_bar_fill.webp | 128×16 | #F44336 | Red fill |
| UI08 | mana_bar_fill.webp | 128×16 | #2196F3 | Blue fill |
| UI09 | stamina_bar_fill.webp | 128×16 | #4CAF50 | Green fill |
| UI10 | cursor.webp | 32×32 | #FFFFFF | White pointer |

---

### Texture Atlases (4 atlases, ~1.5 MB)

**Atlas Configuration**

```typescript
export const ATLAS_CONFIG = {
  maxAtlasSize: 2048,
  padding: 2,
  format: 'webp',
  quality: 85,
  mipmap: true
}
```

**ATLAS 1: Characters & NPCs** (`atlas_characters.webp`)
- **Size**: 2048×2048
- **Contents**: All C001-C010 + NPC variations (50 sprites)
- **File Size**: ~450 KB
- **Usage**: Billboard batching for characters

**ATLAS 2: Items & Pickups** (`atlas_items.webp`)
- **Size**: 2048×2048
- **Contents**: All I001-I020 + loot variations (80 sprites)
- **File Size**: ~380 KB
- **Usage**: Inventory UI + world item rendering

**ATLAS 3: Environment Props** (`atlas_environment.webp`)
- **Size**: 2048×2048
- **Contents**: E001-E015, FX01-FX10, particle sprites (60 sprites)
- **File Size**: ~420 KB
- **Usage**: Trees, rocks, effects

**ATLAS 4: UI Elements** (`atlas_ui.webp`)
- **Size**: 1024×1024
- **Contents**: UI01-UI10, icons, borders (40 elements)
- **File Size**: ~250 KB
- **Usage**: React UI components

**UV Mapping JSON** (`atlas_uvmaps.json`)

```json
{
  "atlas_characters": {
    "player_body": { "x": 0, "y": 0, "w": 256, "h": 256, "u0": 0, "v0": 0, "u1": 0.125, "v1": 0.125 },
    "npc_male": { "x": 256, "y": 0, "w": 256, "h": 256, "u0": 0.125, "v0": 0, "u1": 0.25, "v1": 0.125 }
  }
}
```

---

## 3D MODELS

### Model Specifications

**Format**: glTF 2.0 (.glb binary)
**Polygon Budget**: 100-500 triangles per model
**LOD Strategy**: 3 levels (High, Medium, Low)
**Textures**: Embedded in .glb
**Rigging**: No skeletal animation (billboard sprites for characters)

### Character Models (8 models, ~800 KB)

| ID | Name | Triangles | Size | Description |
|----|------|-----------|------|-------------|
| CM01 | player_capsule.glb | 32 | 80 KB | Simple capsule (3m tall) |
| CM02 | npc_capsule.glb | 32 | 80 KB | Same as player (different texture) |
| CM03 | enemy_cube.glb | 12 | 60 KB | Hostile indicator box |
| CM04 | pet_sphere.glb | 64 | 100 KB | UV sphere (companion) |
| CM05 | horse_box.glb | 48 | 90 KB | Rectangular mount |
| CM06 | billboard_quad.glb | 2 | 50 KB | Quad for sprite billboards |
| CM07 | shadow_circle.glb | 16 | 40 KB | Circular shadow decal |
| CM08 | hitbox_wireframe.glb | 24 | 60 KB | Debug collision box |

### Building Models (15 models, ~1.8 MB)

**LOD Configuration**:
- **High**: Full detail (300-500 tri)
- **Medium**: Simplified (150-250 tri)
- **Low**: Billboard (2 tri)

| ID | Name | High | Med | Low | Total Size | Description |
|----|------|------|-----|-----|------------|-------------|
| BM01 | house_small.glb | 400 | 200 | 2 | 120 KB | Single room cottage |
| BM02 | house_medium.glb | 500 | 250 | 2 | 140 KB | Two-story house |
| BM03 | house_large.glb | 600 | 300 | 2 | 160 KB | Manor house |
| BM04 | shop_general.glb | 450 | 225 | 2 | 130 KB | General store |
| BM05 | shop_blacksmith.glb | 480 | 240 | 2 | 135 KB | Smithy with chimney |
| BM06 | shop_alchemist.glb | 420 | 210 | 2 | 125 KB | Alchemy shop |
| BM07 | tavern.glb | 550 | 275 | 2 | 150 KB | Inn/tavern |
| BM08 | temple.glb | 600 | 300 | 2 | 165 KB | Religious building |
| BM09 | guild_hall.glb | 650 | 325 | 2 | 180 KB | Large guild building |
| BM10 | guard_tower.glb | 380 | 190 | 2 | 110 KB | Defensive tower |
| BM11 | city_wall_segment.glb | 200 | 100 | 2 | 80 KB | 10m wall section |
| BM12 | city_gate.glb | 500 | 250 | 2 | 145 KB | Entry gate with arch |
| BM13 | castle_keep.glb | 700 | 350 | 2 | 190 KB | Large castle |
| BM14 | dungeon_entrance.glb | 350 | 175 | 2 | 105 KB | Cave/crypt entrance |
| BM15 | ruins.glb | 400 | 200 | 2 | 115 KB | Destroyed building |

### Environment Models (20 models, ~1.2 MB)

| ID | Name | Triangles | Size | Description |
|----|------|-----------|------|-------------|
| EM01 | tree_pine.glb | 150 | 65 KB | Conifer tree |
| EM02 | tree_oak.glb | 180 | 70 KB | Deciduous tree |
| EM03 | tree_dead.glb | 100 | 50 KB | Bare tree |
| EM04 | bush_round.glb | 64 | 40 KB | Green shrub |
| EM05 | rock_small.glb | 48 | 35 KB | Boulder (1m) |
| EM06 | rock_medium.glb | 96 | 50 KB | Boulder (2m) |
| EM07 | rock_large.glb | 200 | 75 KB | Boulder (4m) |
| EM08 | grass_clump.glb | 24 | 30 KB | Tall grass tuft |
| EM09 | flower_patch.glb | 32 | 35 KB | Small flowers |
| EM10 | mushroom_group.glb | 48 | 40 KB | 3 mushrooms |
| EM11 | crate_wood.glb | 24 | 30 KB | Wooden box |
| EM12 | barrel.glb | 64 | 45 KB | Storage barrel |
| EM13 | fence_segment.glb | 36 | 32 KB | 2m wooden fence |
| EM14 | lamp_post.glb | 80 | 48 KB | Street light |
| EM15 | well.glb | 120 | 55 KB | Water well |
| EM16 | bridge_wood.glb | 100 | 52 KB | Small bridge (5m) |
| EM17 | sign_post.glb | 40 | 33 KB | Directional sign |
| EM18 | campfire.glb | 72 | 45 KB | Fire pit |
| EM19 | tent.glb | 56 | 42 KB | Small tent |
| EM20 | cart.glb | 88 | 50 KB | Wooden cart |

### Dungeon Models (15 models, ~1.5 MB)

| ID | Name | Triangles | Size | Description |
|----|------|-----------|------|-------------|
| DM01 | dungeon_floor_10m.glb | 2 | 40 KB | Flat floor tile |
| DM02 | dungeon_wall_10m.glb | 4 | 50 KB | Straight wall |
| DM03 | dungeon_corner.glb | 4 | 50 KB | 90° corner |
| DM04 | dungeon_doorway.glb | 12 | 60 KB | Open passage |
| DM05 | dungeon_door_wood.glb | 48 | 70 KB | Closed door |
| DM06 | dungeon_stairs_up.glb | 80 | 85 KB | Ascending stairs |
| DM07 | dungeon_stairs_down.glb | 80 | 85 KB | Descending stairs |
| DM08 | dungeon_pillar.glb | 64 | 75 KB | Support column |
| DM09 | dungeon_chest.glb | 96 | 90 KB | Loot chest |
| DM10 | dungeon_torch.glb | 40 | 65 KB | Wall torch |
| DM11 | dungeon_trap_spike.glb | 72 | 80 KB | Floor trap |
| DM12 | dungeon_lever.glb | 56 | 70 KB | Wall switch |
| DM13 | dungeon_altar.glb | 120 | 100 KB | Ritual altar |
| DM14 | dungeon_cage.glb | 144 | 110 KB | Prison cell |
| DM15 | dungeon_sarcophagus.glb | 180 | 125 KB | Stone coffin |

### Item Models (30 models, ~900 KB)

**Note**: Most items use billboard sprites, these are for special cases

| ID | Name | Triangles | Size | Description |
|----|------|-----------|------|-------------|
| IM01 | sword_3d.glb | 120 | 45 KB | Equipped weapon (LOD0) |
| IM02 | bow_3d.glb | 80 | 38 KB | Equipped bow |
| IM03 | staff_3d.glb | 64 | 35 KB | Equipped staff |
| IM04 | shield_3d.glb | 96 | 42 KB | Equipped shield |
| IM05 | helmet_3d.glb | 150 | 52 KB | Worn helmet |
| IM06 | chest_armor_3d.glb | 200 | 65 KB | Worn chest piece |
| IM07 | boots_3d.glb | 100 | 40 KB | Worn boots |
| IM08 | gloves_3d.glb | 80 | 36 KB | Worn gloves |
| IM09-IM30 | (cosmetics) | 50-150 | Various | Cosmetic items |

---

## AUDIO

### Audio Specifications

**SFX Format**: OGG Vorbis, 44.1kHz, mono, 96 kbps
**Music Format**: OGG Vorbis, 44.1kHz, stereo, 128 kbps
**Loading**: SFX preloaded, music streamed

### Sound Effects (80 files, ~8 MB)

**Combat (20 SFX)**

| ID | Name | Duration | Size | Description |
|----|------|----------|------|-------------|
| SFX01 | sword_swing.ogg | 0.5s | 80 KB | Whoosh |
| SFX02 | sword_hit.ogg | 0.3s | 60 KB | Metal clang |
| SFX03 | arrow_shoot.ogg | 0.4s | 70 KB | Bow release |
| SFX04 | arrow_hit.ogg | 0.3s | 60 KB | Impact thud |
| SFX05 | spell_cast.ogg | 0.8s | 110 KB | Magic whoosh |
| SFX06 | spell_impact.ogg | 0.5s | 85 KB | Magic explosion |
| SFX07 | shield_block.ogg | 0.4s | 75 KB | Deflect clang |
| SFX08 | punch.ogg | 0.3s | 55 KB | Unarmed hit |
| SFX09 | critical_hit.ogg | 0.6s | 95 KB | Extra impact |
| SFX10 | parry.ogg | 0.4s | 70 KB | Blade clash |
| SFX11-SFX20 | (variations) | Various | Various | Additional combat |

**Movement (15 SFX)**

| ID | Name | Duration | Size | Description |
|----|------|----------|------|-------------|
| SFX21 | footstep_grass.ogg | 0.3s | 50 KB | Soft step |
| SFX22 | footstep_stone.ogg | 0.3s | 55 KB | Hard step |
| SFX23 | footstep_wood.ogg | 0.3s | 52 KB | Creaky step |
| SFX24 | footstep_water.ogg | 0.4s | 65 KB | Splash |
| SFX25 | jump.ogg | 0.5s | 75 KB | Jump grunt |
| SFX26 | land.ogg | 0.4s | 70 KB | Land thud |
| SFX27 | swim.ogg | 0.6s | 90 KB | Water movement |
| SFX28 | climb.ogg | 0.5s | 80 KB | Ledge grab |
| SFX29 | door_open.ogg | 0.8s | 105 KB | Creak open |
| SFX30 | door_close.ogg | 0.8s | 105 KB | Creak close |
| SFX31-SFX35 | (variations) | Various | Various | Additional movement |

**UI (10 SFX)**

| ID | Name | Duration | Size | Description |
|----|------|----------|------|-------------|
| SFX36 | button_click.ogg | 0.2s | 40 KB | UI click |
| SFX37 | button_hover.ogg | 0.1s | 30 KB | UI hover |
| SFX38 | inventory_open.ogg | 0.4s | 65 KB | Bag open |
| SFX39 | inventory_close.ogg | 0.4s | 65 KB | Bag close |
| SFX40 | item_pickup.ogg | 0.3s | 55 KB | Item collect |
| SFX41 | item_drop.ogg | 0.3s | 55 KB | Item release |
| SFX42 | quest_accept.ogg | 0.6s | 90 KB | Acceptance chime |
| SFX43 | quest_complete.ogg | 0.8s | 110 KB | Success fanfare |
| SFX44 | level_up.ogg | 1.0s | 130 KB | Level fanfare |
| SFX45 | error.ogg | 0.3s | 50 KB | Negative beep |

**Environment (20 SFX)**

| ID | Name | Duration | Size | Description |
|----|------|----------|------|-------------|
| SFX46 | wind_light.ogg | 2.0s | 200 KB | Gentle breeze (loop) |
| SFX47 | wind_heavy.ogg | 2.0s | 210 KB | Storm wind (loop) |
| SFX48 | rain.ogg | 2.0s | 220 KB | Rain (loop) |
| SFX49 | thunder.ogg | 1.5s | 180 KB | Thunder crack |
| SFX50 | fire_crackling.ogg | 2.0s | 200 KB | Campfire (loop) |
| SFX51 | water_flowing.ogg | 2.0s | 210 KB | Stream (loop) |
| SFX52 | birds_chirping.ogg | 3.0s | 280 KB | Daytime ambient |
| SFX53 | crickets.ogg | 3.0s | 270 KB | Night ambient |
| SFX54 | wolf_howl.ogg | 2.0s | 190 KB | Distant wolf |
| SFX55 | owl_hoot.ogg | 1.0s | 120 KB | Night bird |
| SFX56-SFX65 | (variations) | Various | Various | Additional ambient |

**NPCs (15 SFX)**

| ID | Name | Duration | Size | Description |
|----|------|----------|------|-------------|
| SFX66 | npc_greeting.ogg | 0.5s | 80 KB | Friendly hello |
| SFX67 | npc_farewell.ogg | 0.5s | 80 KB | Goodbye |
| SFX68 | npc_laugh.ogg | 0.8s | 105 KB | Chuckle |
| SFX69 | npc_angry.ogg | 0.6s | 90 KB | Annoyed grunt |
| SFX70 | npc_pain.ogg | 0.4s | 70 KB | Hurt sound |
| SFX71 | npc_death.ogg | 1.0s | 125 KB | Death cry |
| SFX72 | shop_bell.ogg | 0.6s | 85 KB | Store entrance |
| SFX73 | coins_jingle.ogg | 0.5s | 75 KB | Money sound |
| SFX74 | blacksmith_hammer.ogg | 1.0s | 120 KB | Anvil hit (loop) |
| SFX75 | crowd_murmur.ogg | 3.0s | 290 KB | City ambient (loop) |
| SFX76-SFX80 | (variations) | Various | Various | Additional NPC |

### Music Tracks (8 files, ~16 MB)

**Format**: OGG Vorbis, 44.1kHz, stereo, 128 kbps, loopable

| ID | Name | Duration | Size | Mood | Usage |
|----|------|----------|------|------|-------|
| MUS01 | overworld_day.ogg | 3:00 | 2.8 MB | Peaceful | Outdoor exploration (day) |
| MUS02 | overworld_night.ogg | 3:00 | 2.8 MB | Mysterious | Outdoor exploration (night) |
| MUS03 | dungeon_ambient.ogg | 3:30 | 3.2 MB | Tense | Dungeon exploration |
| MUS04 | combat_light.ogg | 2:00 | 1.9 MB | Energetic | Standard combat |
| MUS05 | combat_boss.ogg | 2:30 | 2.3 MB | Epic | Boss fights |
| MUS06 | town.ogg | 3:00 | 2.8 MB | Cheerful | City/settlement |
| MUS07 | tavern.ogg | 2:00 | 1.9 MB | Lively | Inn/tavern interior |
| MUS08 | menu.ogg | 1:30 | 1.4 MB | Calm | Main menu, character creation |

**Total Music Size**: ~19 MB (before streaming optimization)

---

## UI ELEMENTS

### UI Assets (50 files, ~300 KB)

**Buttons (10 SVG)**

| ID | Name | Format | Size | Description |
|----|------|--------|------|-------------|
| UI_BTN01 | button_primary.svg | SVG | 5 KB | Blue action button |
| UI_BTN02 | button_secondary.svg | SVG | 5 KB | Grey cancel button |
| UI_BTN03 | button_danger.svg | SVG | 5 KB | Red delete button |
| UI_BTN04 | button_icon.svg | SVG | 4 KB | Square icon button |
| UI_BTN05 | button_tab.svg | SVG | 5 KB | Tab navigation |
| UI_BTN06-UI_BTN10 | (variations) | SVG | 4-5 KB | Additional buttons |

**Icons (20 SVG)**

| ID | Name | Format | Size | Description |
|----|------|--------|------|-------------|
| UI_ICO01 | icon_health.svg | SVG | 3 KB | Heart |
| UI_ICO02 | icon_mana.svg | SVG | 3 KB | Star |
| UI_ICO03 | icon_stamina.svg | SVG | 3 KB | Lightning bolt |
| UI_ICO04 | icon_inventory.svg | SVG | 3 KB | Backpack |
| UI_ICO05 | icon_map.svg | SVG | 3 KB | Compass |
| UI_ICO06 | icon_quest.svg | SVG | 3 KB | Scroll |
| UI_ICO07 | icon_settings.svg | SVG | 3 KB | Gear |
| UI_ICO08 | icon_save.svg | SVG | 3 KB | Floppy disk |
| UI_ICO09 | icon_load.svg | SVG | 3 KB | Folder open |
| UI_ICO10 | icon_exit.svg | SVG | 3 KB | Door |
| UI_ICO11-UI_ICO20 | (various) | SVG | 3 KB | Additional icons |

**Panels (10 WebP)**

| ID | Name | Format | Size | Description |
|----|------|--------|------|-------------|
| UI_PAN01 | panel_dark.webp | WebP | 15 KB | Dark background |
| UI_PAN02 | panel_light.webp | WebP | 15 KB | Light background |
| UI_PAN03 | panel_border.webp | WebP | 12 KB | Frame border |
| UI_PAN04 | tooltip_bg.webp | WebP | 8 KB | Tooltip background |
| UI_PAN05 | dialog_bg.webp | WebP | 18 KB | Dialog box |
| UI_PAN06-UI_PAN10 | (variations) | WebP | Various | Additional panels |

**Progress Bars (10 WebP + SVG)**

| ID | Name | Format | Size | Description |
|----|------|--------|------|-------------|
| UI_BAR01 | healthbar_bg.webp | WebP | 5 KB | Health bar BG |
| UI_BAR02 | healthbar_fill.webp | WebP | 5 KB | Health bar fill (red) |
| UI_BAR03 | manabar_fill.webp | WebP | 5 KB | Mana bar fill (blue) |
| UI_BAR04 | staminabar_fill.webp | WebP | 5 KB | Stamina bar fill (green) |
| UI_BAR05 | xpbar_fill.webp | WebP | 5 KB | XP bar fill (yellow) |
| UI_BAR06-UI_BAR10 | (variations) | Various | Various | Additional bars |

---

## FONTS

### Font Assets (4 files, ~200 KB)

**Web Fonts (WOFF2)**

| ID | Name | Format | Size | Usage | Fallback |
|----|------|--------|------|-------|----------|
| FONT01 | retro_pixel.woff2 | WOFF2 | 50 KB | Retro UI mode | monospace |
| FONT02 | modern_sans.woff2 | WOFF2 | 60 KB | Modern UI mode | sans-serif |
| FONT03 | medieval_serif.woff2 | WOFF2 | 70 KB | Dialog/quest text | serif |
| FONT04 | numbers_bold.woff2 | WOFF2 | 20 KB | Damage numbers | sans-serif |

**Bitmap Font (Legacy Support)**

| ID | Name | Format | Size | Description |
|----|------|--------|------|-------------|
| FONT05 | retro_bitmap.png | PNG | 128×128, 30 KB | Fallback pixel font |
| FONT06 | retro_bitmap.json | JSON | 15 KB | Glyph mapping |

**Font CSS**

```css
@font-face {
  font-family: 'RetroPixel';
  src: url('/assets/fonts/retro_pixel.woff2') format('woff2');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: 'ModernSans';
  src: url('/assets/fonts/modern_sans.woff2') format('woff2');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}
```

---

## PROCEDURAL GENERATION PARAMETERS

### Terrain Generation

```typescript
export const TERRAIN_CONFIG = {
  chunkSize: 128, // meters
  heightScale: 100, // max height
  frequency: 0.02, // Perlin noise frequency
  octaves: 4,
  lacunarity: 2.0,
  persistence: 0.5,

  biomes: [
    { id: 'grassland', heightRange: [0, 0.3], color: '#4CAF50' },
    { id: 'hills', heightRange: [0.3, 0.5], color: '#8BC34A' },
    { id: 'mountains', heightRange: [0.5, 0.8], color: '#757575' },
    { id: 'peaks', heightRange: [0.8, 1.0], color: '#ECEFF1' },
    { id: 'desert', temperature: '>0.7', color: '#FFE082' },
    { id: 'snow', temperature: '<0.3', color: '#FFFFFF' }
  ]
}
```

### Dungeon Generation

```typescript
export const DUNGEON_CONFIG = {
  blockSize: 10, // meters per block
  minRooms: 8,
  maxRooms: 20,
  corridorWidth: 3,

  dungeonTypes: [
    { id: 'crypt', theme: 'undead', difficulty: 'medium' },
    { id: 'cave', theme: 'natural', difficulty: 'easy' },
    { id: 'mine', theme: 'industrial', difficulty: 'medium' },
    { id: 'castle', theme: 'military', difficulty: 'hard' },
    { id: 'laboratory', theme: 'magic', difficulty: 'very_hard' }
  ],

  prefabBlocks: [
    // 20 pre-made 10×10m room layouts
    'room_square_empty',
    'room_square_pillars',
    'room_l_shaped',
    'corridor_straight',
    'corridor_t_junction',
    // ... (15 more)
  ]
}
```

### City Generation

```typescript
export const CITY_CONFIG = {
  blockSize: 20, // meters
  minBuildings: 30,
  maxBuildings: 150,

  cityTypes: [
    { id: 'capital', population: 5000, districts: 8 },
    { id: 'city', population: 2000, districts: 5 },
    { id: 'town', population: 500, districts: 3 },
    { id: 'village', population: 100, districts: 1 }
  ],

  buildingTypes: [
    { id: 'house_small', frequency: 0.4 },
    { id: 'house_medium', frequency: 0.25 },
    { id: 'house_large', frequency: 0.1 },
    { id: 'shop_general', frequency: 0.05 },
    { id: 'shop_blacksmith', frequency: 0.03 },
    { id: 'shop_alchemist', frequency: 0.02 },
    { id: 'tavern', frequency: 0.04 },
    { id: 'temple', frequency: 0.02 },
    { id: 'guild_hall', frequency: 0.01 },
    // ... (21 more types)
  ],

  roadWidth: 6 // meters
}
```

---

## ASSET PIPELINE WORKFLOW

### Build-Time Asset Processing

```bash
# Step 1: Texture Atlas Generation
npm run build:atlases

# Step 2: 3D Model Optimization
npm run build:models

# Step 3: Audio Compression
npm run build:audio

# Step 4: Generate Asset Manifest
npm run build:manifest
```

### Asset Manifest (`assets/manifest.json`)

```json
{
  "version": "1.0.0",
  "totalSize": 33554432,
  "assets": {
    "textures": {
      "individual": { "count": 100, "size": 819200 },
      "atlases": { "count": 4, "size": 1572864 }
    },
    "models": {
      "count": 88,
      "size": 6502400,
      "lod": true
    },
    "audio": {
      "sfx": { "count": 80, "size": 8388608 },
      "music": { "count": 8, "size": 16777216 }
    },
    "ui": {
      "count": 50,
      "size": 307200
    },
    "fonts": {
      "count": 4,
      "size": 204800
    }
  }
}
```

---

## ASSET CREATION TOOLS

### Recommended Free Tools

**Textures**:
- GIMP (image editing)
- Krita (painting)
- Texture Packer (atlas generation)

**3D Models**:
- Blender (modeling)
- MeshLab (optimization)
- gltf-pipeline (compression)

**Audio**:
- Audacity (editing)
- LMMS (music creation)
- sfxr/jsfxr (retro SFX)

**UI**:
- Figma (design)
- Inkscape (SVG editing)

---

## REPLACEMENT STRATEGY

### Phase-by-Phase Replacement

**Phase 4 (Month 18-19): First Wave**
- Replace most visible assets first
- Priority: Player characters, common items, terrain

**Phase 5 (Month 21-22): Second Wave**
- Buildings, environment props, dungeon assets
- Audio (SFX and music)

**Phase 6 (Month 23-24): Final Polish**
- UI elements, fonts, particle effects
- Quality pass on all assets

### Commissioning Strategy

**Artists Needed**:
- 2D texture artist (terrain, buildings, items)
- 3D modeler (characters, props, buildings)
- Audio designer (SFX, music composition)
- UI/UX designer (interface, icons)

**Budget Allocation**:
- Textures: $8K-$12K
- 3D Models: $10K-$15K
- Audio: $4K-$8K
- UI: $3K-$8K

---

## QUALITY CHECKLIST

### Before Asset Integration

✅ File size within budget
✅ Correct format (WebP, glTF, OGG, WOFF2)
✅ Proper naming convention
✅ LODs generated (for 3D models)
✅ Texture atlases packed correctly
✅ UV maps validated
✅ Audio normalized (-14 LUFS)
✅ All assets in manifest.json

---

## RELATED DOCUMENTS

- [02-TECHNICAL-ARCHITECTURE.md](./02-TECHNICAL-ARCHITECTURE.md) - Rendering systems
- [04-REVISED-24-MONTH-ROADMAP.md](./04-REVISED-24-MONTH-ROADMAP.md) - Asset replacement timeline
- [07-PERFORMANCE-BUDGETS.md](./07-PERFORMANCE-BUDGETS.md) - Size constraints

---

**Last Updated**: 2024-11-15
**Document Version**: 1.0.0
**Status**: Complete - All programmer art specified

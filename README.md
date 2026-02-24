# slidev-theme-penjj

A modern Slidev theme with flowing dynamic backgrounds.

## Installation

```bash
npm install slidev-theme-penjj
# or
pnpm add slidev-theme-penjj
```

## Usage

Add this to your Slidev frontmatter:

```yaml
---
theme: penjj
---
```

## Dynamic Background Components

### FlowingBackground

Canvas-based flowing particles with glowing orbs and connection lines.

```md
<FlowingBackground 
  :colors="['#6366f1', '#8b5cf6', '#06b6d4', '#d946ef']"
  :blur="60"
  :speed="1"
  :particle-count="12"
  base-color="#1e1e2e"
/>
```

### AuroraBackground

CSS-based aurora effect with floating orbs.

```md
<AuroraBackground 
  :colors="['#6366f1', '#8b5cf6', '#06b6d4', '#d946ef']"
  :blur="80"
  :speed="1"
/>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| colors | Array | ['#636f1', ...] | Array of hex colors |
| speed | Number | 1 | Animation speed multiplier |
| blur | Number | 60/80 | Blur strength in pixels |
| particleCount | Number | 12 | Number of particles |
| baseColor | String | '#1e1e2e' | Background base color |

## Custom Layouts

- `cover` - Title/cover slide
- `default` - Standard slide
- `two-cols` - Two columns
- `section` - Section divider
- `end` - End slide
- `center` - Centered content

## License

MIT

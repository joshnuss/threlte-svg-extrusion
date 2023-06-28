# Threlte SVG Extrusions

This is an experiment to use SVG to create parametric 3D shapes.

## Usage

```html
<script>
  import { Canvas, T } from '@threlte/core'
  import SvgExtrusion from './SvgExtrusion.svelte'
</script>

<Canvas>
  <T.PerspectiveCamera .../>
  <T.DirectionalLight ... />
  <T.AmbientLight ... />

  <!-- Extrude an SVG to 3D!! -->
  <SvgExtrusion depth=1>
    <svg viewBox="0 0 20 20">
      <rect x=0 y=0 width=5 height=5 rx=0.5 />
      <circle cx=10 cy=10 r=5 />
    </svg>
  </SvgExtrusion>
</Canvas>
```

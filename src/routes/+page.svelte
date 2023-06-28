<script>
  import { Canvas, OrbitControls, T } from '@threlte/core'
  import { degToRad } from 'three/src/math/MathUtils'
  import SvgExtrusion from './SvgExtrusion.svelte'

  let material
</script>

<div>
  <Canvas>
    <T.PerspectiveCamera makeDefault position={[70, 70, 70]} fov={24}>
      <OrbitControls maxPolarAngle={degToRad(80)} enableZoom={true} target={{ y: 0.5 }} />
    </T.PerspectiveCamera>

    <T.DirectionalLight castShadow position={[3, 10, 10]} />
    <T.DirectionalLight position={[-3, 10, -10]} intensity={0.2} />
    <T.AmbientLight intensity={0.2} />

    <T.MeshBasicMaterial color="purple" reflectivity={0.5}  bind:ref={material}/>

    <T.Mesh>
      <SvgExtrusion depth=1 {material}>
        <svg viewBox="0 0 20 20">
          <rect x=0 y=0 width=5 height=5 rx=0.5 />
          <circle cx=10 cy=10 r=5 />
        </svg>
      </SvgExtrusion>
    </T.Mesh>
  </Canvas>
</div>

<style>
  div {
    height: 100%;
    width: 100%;
  }
</style>

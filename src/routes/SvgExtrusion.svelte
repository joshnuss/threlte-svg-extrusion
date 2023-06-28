<script>
	import * as THREE from 'three'
	import { SVGLoader } from 'three/examples/jsm/loaders/SVGLoader.js'
	import { T, useThrelte } from '@threlte/core'
	import { onMount } from 'svelte'

	const { invalidate } = useThrelte()
	const loader = new SVGLoader()

	let wrapper
	let group = new THREE.Group()

	// TODO: materials

	export let material
	export let castShadow = true
	export let receiveShadow = true
	export let depth = 2
	export let steps = 2
	export let bevelEnabled = false
	export let bevelSegments = 2
	export let bevelSize = 1
	export let bevelThickness = 2

	$: extrudeSettings = {
		depth,
		steps,
		bevelEnabled,
		bevelSegments,
		bevelSize,
		bevelThickness
	}

	onMount(() => {
		const url = dataUrl(wrapper.innerHTML)

		loader.load(url, data => {
			group.clear()

			data.paths.forEach((path) => {
				const shapes = SVGLoader.createShapes(path)

				shapes.forEach((shape) => {
					const geometry = new THREE.ExtrudeGeometry(shape, extrudeSettings)

					// fix y-axis
					geometry.applyMatrix4(new THREE.Matrix4().makeScale(1, -1, 1))

					const mesh = new THREE.Mesh(geometry)
					mesh.material = material

					mesh.castShadow = castShadow
					mesh.receiveShadow = receiveShadow

					group.add(mesh)
				})
			})

			invalidate('SVG loaded')
		})
	})

	function dataUrl(svg) {
		return `data:image/svg+xml;base64,${btoa(svg)}`
	}

	$: console.log({group, material})
</script>

<div style:visibility="none" bind:this={wrapper}>
	<slot/>
</div>

<T.Group bind:ref={group}>
</T.Group>

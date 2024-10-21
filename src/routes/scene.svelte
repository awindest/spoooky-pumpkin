<script lang="ts">
	import { T, useFrame } from '@threlte/core'
	import { OrbitControls, useGltf, Text } from '@threlte/extras'
	import Bloom from './bloom.svelte'
// text
	let text = 'Why are you looking at my bottom?'
	let bevelEnabled = true
	let bevelOffset = 0
	let bevelSegments = 20
	let bevelSize = 0.2
	let bevelThickness = 0.1
	let curveSegments = 12
	let height = 1
	let size = 20
	let smooth = 0.1

	let y = 2
	let rotation = 0

	function levitate() {
		const time = Date.now() / 1000
		const speed = 1
		const offset = 3
		y = Math.sin(time * speed) + offset
		requestAnimationFrame(levitate)
	}

	useFrame((_, delta) => {
		rotation += delta * 0.4
	})

	levitate()
</script>

<!-- <Bloom /> -->

<T.OrthographicCamera position={[10, 10, 10]} zoom={40} makeDefault>
	<!-- Controls -->
	<OrbitControls enableDamping />
</T.OrthographicCamera>

<T.AmbientLight color="#0000ff" intensity={10} />
<T.PointLight intensity={2} position={[4, 2, 4]} color="#76aac8" />

{#await useGltf('/assets/halloween_pumpkin.glb') then pumpkin}
	<T is={pumpkin.scene} position={[0, y, 0]} scale={0.005} />
{/await}

{#await useGltf('/assets/garden.glb') then garden}
	<T is={garden.scene} rotation.y={rotation} />
{/await}

<T.Mesh>
    <Text
      font={'/fonts/Inter-SemiBold.woff2'}
      {text}
      {bevelEnabled}
      {bevelOffset}
      {bevelSegments}
      {bevelSize}
      {bevelThickness}
      {curveSegments}
      {height}
      {size}
      {smooth}
    />
    <T.MeshStandardMaterial
      color="#FD3F00"
      toneMapped={false}
      metalness={1.0}
      roughness={0.1}
    />
  </T.Mesh>


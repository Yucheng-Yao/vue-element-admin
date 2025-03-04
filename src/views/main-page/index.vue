<template>
  <div class="app-container">

    <!-- Three.js Canvas -->
    <div class="wrapper">
      <div ref="canvasRef" class="canvas-container" />
      <div class="overlay">
        <h1 class="title">🚀 It's our mainpage (temporary) 🚀</h1>
      </div>
    </div>
  </div>
</template>

<script>
import * as THREE from 'three'

export default {
  name: 'Test',
  data() {
    return {
      scene: null,
      camera: null,
      renderer: null,
      cube: null
    }
  },
  mounted() {
    this.initThreeJS()
  },
  methods: {
    initThreeJS() {
      const container = this.$refs.canvasRef
      this.scene = new THREE.Scene()
      this.camera = new THREE.PerspectiveCamera(
        75,
        container.clientWidth / container.clientHeight,
        0.1,
        1000
      )
      this.renderer = new THREE.WebGLRenderer({ alpha: true })

      this.renderer.setSize(container.clientWidth, container.clientHeight)
      container.appendChild(this.renderer.domElement)

      const geometry = new THREE.BoxGeometry()
      const material = new THREE.MeshStandardMaterial({
        color: 0x00ffff,
        wireframe: true
      })
      this.cube = new THREE.Mesh(geometry, material)
      this.scene.add(this.cube)

      const light = new THREE.PointLight(0xffffff, 1, 100)
      light.position.set(2, 2, 2)
      this.scene.add(light)

      this.camera.position.z = 3
      this.animate()
    },
    animate() {
      requestAnimationFrame(this.animate)
      this.cube.rotation.x += 0.01
      this.cube.rotation.y += 0.01
      this.renderer.render(this.scene, this.camera)
    },
    startAnimation() {
      this.cube.rotation.x += 0.5
      this.cube.rotation.y += 0.5
    }
  }
}
</script>

<style scoped>
.app-container {
  padding: 20px;
}

.canvas-container {
  position: relative;
  width: 100%;
  height: 500px;
  border: 1px solid #ddd;
}

.title {
  font-size: 2rem;
  font-weight: bold;
  background: linear-gradient(90deg, #ff00ff, #00ffff, #ff0000);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-align: center;
}

.overlay {
  position: absolute;
  top: 10%;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
}
</style>

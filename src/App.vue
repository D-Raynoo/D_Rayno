<script setup>
import Main from '@/views/Main.vue'
import { ref, onMounted } from 'vue'
import { Camera, Renderer, Scene, GltfModel, AmbientLight, SpotLight } from 'troisjs'
import bg3D from '@/assets/models/bg2/scene.gltf'

const renderer = ref(null)

onMounted(() => {
  renderer.value.three.cameraCtrl.enableZoom = false
})
</script>

<template>
  <Renderer ref="renderer" resize :orbit-ctrl="{ autoRotate: true }" class="absolute h-auto w-full">
    <Camera :position="{ y: 0, z: 550 }" />
    <Scene>
      <GltfModel :src="bg3D" />
    </Scene>
  </Renderer>
  <Main />
</template>

<style scoped>
</style>

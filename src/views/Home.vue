<template>
  <div class="w-fit h-fit grid grid-cols-1 gap-y-3 m-auto auto-rows-max place-items-center">
    <h1
      class="text-3xl text-center px-5 text-neutral-100 whitespace-pre-wrap filter drop-shadow-xl"
    >
      <strong>{{ $t('message.selfPresentation') }}</strong>
    </h1>
    <div class="z-50 flex items-center justify-center">
      <v-progress-circular indeterminate v-if="modelLoading"></v-progress-circular>
      <Renderer
        class="cursor-grab hidden md:block"
        width="400"
        height="300"
        alpha
        ref="pc"
        shadow
        :orbit-ctrl="{ autoRotate: false }"
      >
        <Camera :position="{ x: 0, y: 6, z: 10 }" ref="cam" />
        <Scene>
          <GltfModel :src="pcModel" />
          <SpotLight
            :intensity="5"
            :position="{ y: 2, z: 2 }"
            :cast-shadow="true"
            :shadow-map-size="{ width: 400, height: 400 }"
            color="#24afda"
          />
        </Scene>
      </Renderer>
      <Renderer
        class="cursor-grab block md:hidden"
        width="350"
        height="260"
        alpha
        ref="pcMin"
        shadow
        :orbit-ctrl="{ autoRotate: false }"
      >
        <Camera :position="{ x: 0, y: 6, z: 10 }" ref="cam" />
        <Scene>
          <GltfModel :src="pcModel" />
          <SpotLight
            :intensity="5"
            :position="{ y: 2, z: 2 }"
            :cast-shadow="true"
            :shadow-map-size="{ width: 400, height: 400 }"
            color="#24afda"
          />
        </Scene>
      </Renderer>
    </div>

    <div class="flex w-fit h-auto items-center gap-4">
      <v-btn size="x-large" elevation="20" :loading="loading" @click="load" link to="/portfolio">
        {{ $t('message.exploreButton') }}
        <template v-slot:loader>
          <v-progress-circular indeterminate></v-progress-circular>
        </template>
      </v-btn>
      <v-select
        v-model="$i18n.locale"
        :items="$i18n.availableLocales"
        density="compact"
        variant="solo-filled"
        ref="vselect"
        bg-color="rgba(255,255,255,0.14)"
        color="rgb(212 212 212)"
        base-color="rgb(245 245 245)"
      ></v-select>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import { Camera, Renderer, Scene, GltfModel, AmbientLight, SpotLight } from 'troisjs'
import pcModel from '@/assets/models/computerV2/scene.glb'

const pc = ref(null)
const loading = ref(false)
const pcMin = ref(null)
const modelLoading = ref(null)

function load() {
  loading.value = true
}

watch(pcMin, () => {
  pcMin.value.three.cameraCtrl.enableZoom = false
})

onMounted(() => {
  pc.value.three.cameraCtrl.enableZoom = false
})
</script>

<style>
.v-input__details {
  display: none !important;
}
</style>

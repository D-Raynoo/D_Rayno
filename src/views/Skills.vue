<template>
  <div class="w-full h-full flex justify-center items-center">
    <div class="flex-col w-fit h-fit">
      <h1 class="w-fit whitespace-pre-wrap mx-auto text-4xl sm:text-5xl text-center font-bold">
        {{ $t('message.tools') }}
      </h1>
      <v-window v-model="onboarding" class="w-fit h-fit mx-auto hidden lg:block" show-arrows>
        <v-window-item class="relative w-fit px-20 mx-auto h-fit">
          <h1 class="w-fit text-3xl font-bold absolute m-auto left-0 right-0 top-12">
            {{ $t('message.toolsText.devTools') }}
          </h1>
          <div class="flex items-center justify-center">
            <ul class="text-xl font-bold">
              <li v-for="tool in devTools" :key="tool">{{ tool }}</li>
            </ul>
            <v-container>
              <Renderer
                class="cursor-grab"
                width="400"
                height="400"
                alpha
                shadow
                :orbit-ctrl="{ autoRotate: true, enableZoom: false }"
              >
                <Camera :position="{ x: 0, y: 0.5, z: 2 }" ref="cam" />
                <Scene>
                  <GltfModel
                    @progress="loading = true"
                    @load="loading = false"
                    :src="devToolsModel"
                    :position="{ x: 0, y: 0, z: 0 }"
                  />
                  <RefractionMesh
                    v-if="loading"
                    ref="mesh"
                    :position="{ x: 0, y: -20, z: 20 }"
                    auto-update
                  >
                    <TorusGeometry
                      :radius="8"
                      :tube="3"
                      :radial-segments="8"
                      :tubular-segments="6"
                    />
                    <StandardMaterial
                      color="#ffffff"
                      :props="{ metalness: 1, roughness: 0, flatShading: true }"
                    />
                  </RefractionMesh>
                  <AmbientLight />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 0, y: 2, z: 20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 0, y: 2, z: -20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: -20, y: 2, z: 0 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 20, y: 2, x: 0 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                </Scene>
              </Renderer>
            </v-container>
          </div>
        </v-window-item>
        <v-window-item class="w-fit px-20 mx-auto h-fit relative">
          <h1 class="w-fit text-3xl font-bold absolute m-auto left-0 right-0 top-12">
            {{ $t('message.toolsText.designTools') }}
          </h1>
          <div class="flex items-center justify-center">
            <ul class="text-xl font-bold">
              <li v-for="tool in designTools" :key="tool">{{ tool }}</li>
            </ul>
            <v-container>
              <Renderer
                class="cursor-grab"
                width="400"
                height="400"
                alpha
                shadow
                :orbit-ctrl="{ autoRotate: true, enableZoom: false }"
              >
                <Camera :position="{ x: 0, y: 0.5, z: 1 }" ref="cam" />
                <Scene>
                  <GltfModel
                    @progress="loading = true"
                    @load="loading = false"
                    :src="designToolsModel"
                    :position="{ x: 0, y: 0, z: 0 }"
                  />
                  <RefractionMesh
                    v-if="loading"
                    ref="mesh"
                    :position="{ x: 0, y: -20, z: 20 }"
                    auto-update
                  >
                    <TorusGeometry
                      :radius="8"
                      :tube="3"
                      :radial-segments="8"
                      :tubular-segments="6"
                    />
                    <StandardMaterial
                      color="#ffffff"
                      :props="{ metalness: 1, roughness: 0, flatShading: true }"
                    />
                  </RefractionMesh>
                  <AmbientLight />
                  <SpotLight
                    :intensity="1"
                    :position="{ x: 0, y: 2, z: -20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="1"
                    :position="{ x: 0, y: 2, z: 20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                </Scene>
              </Renderer>
            </v-container>
          </div>
        </v-window-item>
      </v-window>

      <section class="block lg:hidden w-full h-fit pb-5 py-6">
        <div class="sm:w-2/3 sm:mx-auto">
          <h1 class="w-fit text-3xl mb-4 font-bold">
            {{ $t('message.toolsText.devTools') }}
          </h1>
          <div class="flex justify-between mb-4">
            <ul class="text-xl font-bold">
              <li v-for="tool in devTools" :key="tool">{{ tool }}</li>
            </ul>
            <v-container>
              <Renderer
                class="cursor-grab sm:hidden"
                width="150"
                height="150"
                alpha
                shadow
                :orbit-ctrl="{ autoRotate: true, enableZoom: false }"
              >
                <Camera :position="{ x: 0, y: 0.5, z: 2 }" ref="cam" />
                <Scene>
                  <GltfModel
                    @progress="loading = true"
                    @load="loading = false"
                    :src="devToolsModel"
                    :position="{ x: 0, y: 0, z: 0 }"
                  />
                  <RefractionMesh
                    v-if="loading"
                    ref="mesh"
                    :position="{ x: 0, y: -20, z: 20 }"
                    auto-update
                  >
                    <TorusGeometry
                      :radius="8"
                      :tube="3"
                      :radial-segments="8"
                      :tubular-segments="6"
                    />
                    <StandardMaterial
                      color="#ffffff"
                      :props="{ metalness: 1, roughness: 0, flatShading: true }"
                    />
                  </RefractionMesh>
                  <AmbientLight />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 0, y: 2, z: 20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 0, y: 2, z: -20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: -20, y: 2, z: 0 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 20, y: 2, x: 0 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                </Scene>
              </Renderer>
            </v-container>

            <v-container>
              <Renderer
                class="cursor-grab hidden sm:block"
                width="320"
                height="320"
                alpha
                shadow
                :orbit-ctrl="{ autoRotate: true, enableZoom: false }"
              >
                <Camera :position="{ x: 0, y: 0.5, z: 2 }" ref="cam" />
                <Scene>
                  <GltfModel
                    @progress="loading = true"
                    @load="loading = false"
                    :src="devToolsModel"
                    :position="{ x: 0, y: 0, z: 0 }"
                  />
                  <RefractionMesh
                    v-if="loading"
                    ref="mesh"
                    :position="{ x: 0, y: -20, z: 20 }"
                    auto-update
                  >
                    <TorusGeometry
                      :radius="8"
                      :tube="3"
                      :radial-segments="8"
                      :tubular-segments="6"
                    />
                    <StandardMaterial
                      color="#ffffff"
                      :props="{ metalness: 1, roughness: 0, flatShading: true }"
                    />
                  </RefractionMesh>
                  <AmbientLight />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 0, y: 2, z: 20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 0, y: 2, z: -20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: -20, y: 2, z: 0 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="0.6"
                    :position="{ x: 20, y: 2, x: 0 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                </Scene>
              </Renderer>
            </v-container>
          </div>
        </div>
        <div class="sm:w-2/3 sm:mx-auto">
          <h1 class="w-fit text-3xl mb-4 font-bold">
            {{ $t('message.toolsText.designTools') }}
          </h1>
          <div class="flex justify-between">
            <ul class="text-xl font-bold">
              <li v-for="tool in designTools" :key="tool">{{ tool }}</li>
            </ul>
            <v-container>
              <Renderer
                class="cursor-grab sm:hidden"
                width="150"
                height="150"
                alpha
                shadow
                :orbit-ctrl="{ autoRotate: true, enableZoom: false }"
              >
                <Camera :position="{ x: 0, y: 0.5, z: 1 }" ref="cam" />
                <Scene>
                  <GltfModel
                    @progress="loading = true"
                    @load="loading = false"
                    :src="designToolsModel"
                    :position="{ x: 0, y: 0, z: 0 }"
                  />
                  <RefractionMesh
                    v-if="loading"
                    ref="mesh"
                    :position="{ x: 0, y: -20, z: 20 }"
                    auto-update
                  >
                    <TorusGeometry
                      :radius="8"
                      :tube="3"
                      :radial-segments="8"
                      :tubular-segments="6"
                    />
                    <StandardMaterial
                      color="#ffffff"
                      :props="{ metalness: 1, roughness: 0, flatShading: true }"
                    />
                  </RefractionMesh>
                  <AmbientLight />
                  <SpotLight
                    :intensity="1"
                    :position="{ x: 0, y: 2, z: -20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="1"
                    :position="{ x: 0, y: 2, z: 20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                </Scene>
              </Renderer>
            </v-container>

            <v-container>
              <Renderer
                class="cursor-grab hidden sm:block"
                width="320"
                height="320"
                alpha
                shadow
                :orbit-ctrl="{ autoRotate: true, enableZoom: false }"
              >
                <Camera :position="{ x: 0, y: 0.5, z: 1 }" ref="cam" />
                <Scene>
                  <GltfModel
                    @progress="loading = true"
                    @load="loading = false"
                    :src="designToolsModel"
                    :position="{ x: 0, y: 0, z: 0 }"
                  />
                  <RefractionMesh
                    v-if="loading"
                    ref="mesh"
                    :position="{ x: 0, y: -20, z: 20 }"
                    auto-update
                  >
                    <TorusGeometry
                      :radius="8"
                      :tube="3"
                      :radial-segments="8"
                      :tubular-segments="6"
                    />
                    <StandardMaterial
                      color="#ffffff"
                      :props="{ metalness: 1, roughness: 0, flatShading: true }"
                    />
                  </RefractionMesh>
                  <AmbientLight />
                  <SpotLight
                    :intensity="1"
                    :position="{ x: 0, y: 2, z: -20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                  <SpotLight
                    :intensity="1"
                    :position="{ x: 0, y: 2, z: 20 }"
                    :shadow-map-size="{ width: 2000, height: 2000 }"
                    :cast-shadow="true"
                  />
                </Scene>
              </Renderer>
            </v-container>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
import {
  AmbientLight,
  Camera,
  Renderer,
  PointLight,
  Scene,
  Sphere,
  StandardMaterial,
  Texture
} from 'troisjs'
import { ref } from 'vue'
import devToolsModel from '/src/assets/models/threeD_Logos/allInOne/devTools/optimized/scene.glb'
import designToolsModel from '/src/assets/models/threeD_Logos/allInOne/designTools/optimized/scene.glb'

const onboarding = ref(0)
const devTools = ref(['HTML&CSS', 'JavaScript', 'PHP', 'Vue JS', 'Laravel', 'TailwindCSS'])
const designTools = ref(['Adobe Photoshop', 'Adobe Illustrator'])
const loading = ref(false)
const loadingDev = ref(false)
</script>

<style>
</style>
<template>
  <div class="w-full h-full flex justify-center items-center">
    <div class="flex-col w-fit h-fit">
      <h1 class="text-center whitespace-pre-wrap text-4xl sm:text-5xl font-bold">
        {{ $t('message.tools') }}
      </h1>
      <v-window v-model="onboarding" class="w-fit h-fit mx-auto mt-4" dir="ltr" show-arrows>
        <v-window-item class="w-fit px-20 mx-auto h-fit">
          <div class="w-fit h-fit">
            <h1 class="text-center text-3xl">{{ $t('message.toolsText.devTools') }}</h1>
            <div class="flex w-fit h-fit">
              <ul class="w-36 h-fit my-auto">
                <li v-for="(tool, index) in devTools" :key="index">{{ index + 1 }}\ {{ tool }}</li>
              </ul>
              <div class="w-64 aspect-square cursor-grab flex items-center justify-center">
                <v-progress-circular
                  :rotate="360"
                  :size="100"
                  :width="15"
                  :model-value="progress"
                  color="primary"
                  v-show="!hasFinishLoading"
                >
                  {{ progress }}
                </v-progress-circular>
                <TresCanvas shadows alpha>
                  <TresPerspectiveCamera :position="[0, 0, 15]" />
                  <OrbitControls enable-damping damping-factor="0.1" :enable-zoom="false" />
                  <TresMesh ref="bgModel">
                    <Suspense>
                      <GLTFModel :path="devToolsModel" draco />
                    </Suspense>
                  </TresMesh>
                  <TresAmbientLight />
                  <TresDirectionalLight :position="[-4, 8, 4]" :intensity="3" cast-shadow />
                </TresCanvas>
              </div>
            </div>
          </div>
        </v-window-item>
        <v-window-item class="w-fit px-20 mx-auto h-fit">
          <div class="w-fit h-fit">
            <h1 class="text-center text-3xl">
              {{ $t('message.toolsText.designTools') }}
            </h1>
            <div class="flex w-fit h-fit">
              <ul class="w-36 h-fit my-auto">
                <li v-for="(tool, index) in designTools" :key="index">
                  {{ index + 1 }}\ {{ tool }}
                </li>
              </ul>
              <div class="w-64 aspect-square cursor-grab flex items-center justify-center">
                <v-progress-circular
                  :rotate="360"
                  :size="100"
                  :width="15"
                  :model-value="progress"
                  color="primary"
                  v-show="!hasFinishLoading"
                >
                  {{ progress }}
                </v-progress-circular>
                <TresCanvas shadows alpha>
                  <TresPerspectiveCamera :position="[0, 0, 15]" />
                  <OrbitControls enable-damping damping-factor="0.1" :enable-zoom="false" />
                  <TresMesh ref="bgModel">
                    <Suspense>
                      <GLTFModel :path="designToolsModel" draco />
                    </Suspense>
                  </TresMesh>
                  <TresAmbientLight />
                  <TresDirectionalLight :position="[-4, 8, 4]" :intensity="3" cast-shadow />
                </TresCanvas>
              </div>
            </div>
          </div>
        </v-window-item>
      </v-window>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import devToolsModel from '/src/assets/models/threeD_Logos/allInOne/devTools/scene.glb'
import designToolsModel from '/src/assets/models/threeD_Logos/allInOne/designTools/scene.glb'
import { OrbitControls, GLTFModel } from '@tresjs/cientos'
import { useProgress } from '@tresjs/cientos'

const { hasFinishLoading, progress } = await useProgress()

const onboarding = ref(0)
const devTools = ref(['HTML&CSS', 'JavaScript', 'PHP', 'Vue JS', 'Laravel', 'TailwindCSS'])
const designTools = ref(['Adobe Photoshop', 'Adobe Illustrator'])
</script>

<style>
</style>
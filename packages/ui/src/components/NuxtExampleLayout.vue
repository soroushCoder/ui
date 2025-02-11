<script setup lang="ts">
import NIcon from './NIcon.vue'
const props = defineProps<{
  example?: string
  showTips?: boolean
  class?: string // eslint-disable-line vue/no-reserved-props
  openPath?: string
}>()

const openInEditor = () => {
  fetch(`/__open-in-editor?file=${encodeURIComponent(props.openPath || 'app.vue')}`)
}
</script>

<template>
  <div class="relative font-sans" n="green6">
    <div class="container max-w-200 mx-auto py-10 px-4">
      <div class="flex items-end gap-3 mb-4 relative">
        <svg viewBox="0 0 221 65" fill="none" xmlns="http://www.w3.org/2000/svg" class="h-10">
          <g clip-path="url(#a)">
            <path
              fill="currentColor"
              d="M82.562 18.57h7.302l15.474 24.742V18.571h6.741v35.057h-7.252l-15.525-24.69v24.69h-6.74V18.57Zm59.645 35.058h-6.282v-3.916c-1.429 2.756-4.339 4.308-8.015 4.308-5.822 0-9.603-4.107-9.603-10.018V28.385h6.282V42.71c0 3.456 2.146 5.859 5.362 5.859 3.524 0 5.974-2.704 5.974-6.41V28.385h6.282v25.243Zm21.857-.4-6.026-8.413-6.027 8.414h-6.69l9.296-13.172-8.58-12.071h6.843l5.158 7.264 5.106-7.264h6.895l-8.632 12.07 9.295 13.173h-6.638Zm19.405-32.455v7.611h7.149v5.16h-7.149v12.53c0 .421.17.825.473 1.123.303.298.715.465 1.144.466h5.532v5.955h-4.137c-5.617 0-9.293-3.206-9.293-8.811V33.548h-5.056v-5.164h3.172c1.479 0 2.34-.864 2.34-2.293v-5.318h5.825Z"
            />
            <path
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M30.119 11.546c-1.886-3.242-6.6-3.242-8.484 0L1.087 46.875c-1.885 3.241.472 7.293 4.242 7.293h16.04c-1.61-1.408-2.207-3.844-.988-5.934L35.942 21.56l-5.824-10.013Z"
              fill="#80EEC0"
            />
            <path
              d="M43.137 19.295c1.56-2.652 5.461-2.652 7.022 0l17.004 28.906c1.56 2.652-.39 5.968-3.51 5.968h-34.01c-3.12 0-5.07-3.316-3.51-5.968l17.004-28.906ZM209.174 53.8h-10.691c0-1.85.067-3.452 0-6.02h10.641c1.868 0 3.353.1 4.354-.935 1-1.034 1.501-2.335 1.501-3.903 0-1.834-.667-3.219-2.002-4.153-1.301-.967-2.985-1.451-5.054-1.451h-2.601v-5.254h2.652c1.701 0 3.119-.4 4.253-1.2 1.134-.801 1.701-1.986 1.701-3.553 0-1.301-.434-2.336-1.301-3.103-.834-.8-2.001-1.2-3.503-1.2-1.634 0-2.918.483-3.853 1.45-.9.968-1.401 2.152-1.501 3.553h-6.254c.133-3.236 1.251-5.788 3.352-7.656 2.135-1.868 4.887-2.802 8.256-2.802 2.402 0 4.42.434 6.055 1.301 1.668.834 2.919 1.952 3.753 3.353.867 1.4 1.301 2.952 1.301 4.653 0 1.968-.551 3.636-1.651 5.004-1.068 1.334-2.402 2.235-4.004 2.702 1.969.4 3.57 1.368 4.804 2.902 1.234 1.501 1.852 3.403 1.852 5.705 0 1.934-.468 3.702-1.402 5.304-.934 1.6-2.301 2.885-4.103 3.852-1.768.968-3.953 1.452-6.555 1.452Z"
              fill="#00DC82"
            />
          </g>
        </svg>
        <div class="text-xl flex">
          <div class="op-50">
            examples/
          </div>
          <slot name="name">
            <NLink :href="`https://github.com/nuxt/framework/tree/main/examples/${example}`" target="_blank">
              {{ example }}
            </NLink>
          </slot>
        </div>
        <div flex-auto />
        <div class="op20 hover:op-100 n-transition -mb-2 -mr-1">
          <NButton
            n="borderless lg"
            class="p-2 op50"
            :to="`https://github.com/nuxt/framework/tree/main/examples/${example}`"
            target="_blank"
          >
            <NIcon icon="carbon-code" />
          </NButton>
          <NDarkToggle>
            <template #default="{ toggle }">
              <NButton n="borderless lg" p-2 op50 @click="toggle">
                <NIcon icon="dark:carbon-moon carbon-sun" />
              </NButton>
            </template>
          </NDarkToggle>
        </div>
      </div>

      <slot name="subtitle" />
      <slot name="nav" />

      <NCard class="p-6 flex flex-col gap-2 text-center" :class="$props.class">
        <slot />
      </NCard>

      <div
        v-if="$slots.tips"
        :class="showTips ? 'opacity-100' : 'opacity-0'"
        class="transition py-5 flex items-center gap-2 text-gray-400"
      >
        <NIcon icon="carbon-idea" class="text-xl flex-none" />
        <slot name="tips" />
        <NButton icon="carbon-edit" class="flex-none" @click="openInEditor">
          Open in Editor
        </NButton>
      </div>

      <slot name="footer" />
    </div>
  </div>
</template>

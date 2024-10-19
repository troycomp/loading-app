<template>
  <div class="flex flex-column justify-around h-100" :key="renderCount">
    <div class="flex justify-around">
      <div class="stack-md">
        <h2 class="montserrat lh-title fw-700 f5 tc">
          Single Suspense boundary
        </h2>
        <div class="frame stack-md">
          <div class="flex items-center justify-center h-100" v-if="error">
            <div class="f2 montserrat gray mr2">!</div>
            <div class="f6 gray">{{ error }}</div>
          </div>
          <suspense v-else>
            <template #default>
              <Left />
            </template>
            <template #fallback>
              <CommonSkeleton />
            </template>
          </suspense>
        </div>
      </div>
      <div class="stack-md">
        <h2 class="montserrat lh-title fw-700 f5 tc">
          Nested Suspense boundaries
        </h2>
        <div class="frame stack-md">
          <div class="flex items-center justify-center h-100" v-if="error">
            <div class="f2 montserrat gray mr2">!</div>
            <div class="f6 gray">{{ error }}</div>
          </div>
          <suspense v-else>
            <template #default>
              <Right />
            </template>
            <template #fallback>
              <CommonSkeleton />
            </template>
          </suspense>
        </div>
      </div>
    </div>
    <div class="flex justify-center">
      <button @click="handleReload" class="button pointer dim hover">
        Reload
      </button>
    </div>
  </div>
</template>
<script setup>
import {
  ref,
  computed,
  defineAsyncComponent,
  nextTick,
  onMounted,
  onBeforeMount,
  onActivated,
  onDeactivated,
  onErrorCaptured,
  toRaw,
} from "vue";
import CommonSkeleton from "@/components/CommonSkeleton.vue";
import Right from "@/components/Right.vue";
import Left from "@/components/Left.vue";
const renderCount = ref(0);
function handleReload() {
  renderCount.value += 1;
}

const error = ref(null);
onErrorCaptured((e) => {
        error.value = e;
        return false;
      });

</script>

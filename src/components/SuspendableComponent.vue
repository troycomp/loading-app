<template>
  <div  class="card">
    <div class="stack-lg">
      <div class="stack-sm">
        <h2 class="montserrat lh-title fw-700 f5">{{ data.title }}</h2>
        <p class="f6">{{ data.description }}</p>
      </div>
      <slot />
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
  toRefs,
  toRaw,
} from "vue";
const props = defineProps({
  dataIndex: Number,
  delay: Number,
  throwError: Boolean,
});
const { dataIndex, delay, throwError } = toRefs(props);
const data = ref(null);

const alldata = ref( [
  {
    title: "Aenean Duis",
    description: "Duis mollis luctus augue, ut interdum nisi."
  },
  {
    title: "Nunc Vestibulum",
    description: "Vestibulum at arcu quis nisi congue."
  },
  {
    title: "Donec Duis",
    description: "Duis rhoncus orci et est vulputate."
  }
]);

function fetchData(config) {
  const { dataIndex = 0, delay = 0, throwError = false } = config;
  return new Promise((resolve, reject) =>
    setTimeout(() => {
      if (throwError) reject("Something went wrong.");
      else resolve(alldata.value[dataIndex]);
    }, delay * 1000)
  );
}

onMounted(async () => {
  data.value = await fetchData({
    dataIndex: props.dataIndex,
    delay: props.delay,
    throwError: props.throwError,
  });
});
</script>

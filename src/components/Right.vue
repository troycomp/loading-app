<template>
  <div>
    <SuspendableComponent :dataIndex="0" :delay="1" />
    <SuspendableComponent :dataIndex="1" :delay="3" />
    <Suspense>
      <SuspendableComponent :dataIndex="2" :delay="5" />
      <template #fallback>
        <div class="card" data-variant="depressed">
          <Skeleton />
        </div>
      </template>
    </Suspense>
  </div>
</template>
<script setup>
import SuspendableComponent from "@/components/SuspendableComponent.vue";
import Skeleton from "@/components/Skeleton.vue";
</script>

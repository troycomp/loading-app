<template>
  <div>
    <SuspendableComponent :dataIndex="0" :delay="1" />
    <SuspendableComponent :dataIndex="1" :delay="3" />
    <SuspendableComponent :dataIndex="2" :delay="5" />
  </div>
</template>
<script setup>
import SuspendableComponent from "@/components/SuspendableComponent.vue";
</script>

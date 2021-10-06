<template>
  <div v-for="(value, key) in info" :key="key">
    <div v-if="typeof value === `object`" class="row">
      <div class="col">
        <h5>{{ key }}</h5>
        <ul>
          <li v-for="(item, index) in value" :key="index">{{ item }}</li>
        </ul>
      </div>
    </div>
    <div v-else class="row">
      <div class="col">
        <h5>{{ key }}</h5>
        <p>{{ value }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    info: {
      required: true,
      type: Object,
    },
  },
};
</script>
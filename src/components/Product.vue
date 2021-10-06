<template>
  <div class="card my-2" style="width: 500px">
    <div class="card-header">
      <h3>{{ title }}</h3>
    </div>
    <div class="card-body" style="min-height: 200px">
      <div v-if="loading">
        <div class="d-flex align-items-center">
          <strong>Loading...</strong>
          <div
            class="spinner-border ms-auto"
            role="status"
            aria-hidden="true"
          ></div>
        </div>
      </div>
      <div v-else>
        <Info :info="info" />
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import Info from "./Info.vue";

export default {
  components: { Info },
  props: {
    id: {
      required: true,
      type: String,
    },
    title: {
      required: true,
      type: String,
    },
  },
  data() {
    return {
      info: {},
    };
  },
  created() {
    this.fetchInfo();
  },
  computed: {
    loading: function () {
      return Object.keys(this.info).length === 0;
    },
    product_info_url: function () {
      return `${process.env.VUE_APP_API_URL}/api/products/${this.id}`;
    },
  },
  methods: {
    fetchInfo: function () {
      console.log(`Loading: ${this.id}`);
      axios.get(this.product_info_url).then((res) => {
        this.info = res.data[this.id];
      });
    },
  },
};
</script>
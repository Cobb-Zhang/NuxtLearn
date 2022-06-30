<template>
  <div class="container">
    <div v-if="error">
      {{ error }}
    </div>
    <div v-else>
      <div v-for="activity in Activities" :key="activity.id" >
        <div v-html="activity.attributes.content"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      Activities: [],
      error: null
    };
  },
  async mounted() {
    try {
      const response = await axios.get("http://localhost:1337/api/Activities");
      this.Activities = response.data.data;
      console.log(this.Activities[0].attributes)
    } catch (error) {
      this.error = error;
    }
  }
};
</script>

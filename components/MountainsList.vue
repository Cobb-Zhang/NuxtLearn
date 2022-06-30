<template>
  <div>
    <p v-if="$fetchState.pending">Loading....</p>
    <p v-else-if="$fetchState.error">Error while fetching mountains</p>
    <template>
      <div>
        <b-table
          striped
          hover
          :items="pages"
          :fields="fields"
          :sort-by.sync="sortBy"
        >
          <template #cell(index)="data">
            {{ data.index + 1 }}
          </template>
          <!-- Optional default data cell scoped slot -->
          <template #cell(link)="data">
            <template>
              <div>
                 <b-link :href="data.value" target="_blank">{{ data.value}}</b-link>
              </div>
            </template>
            
          </template>
        </b-table>
      </div>
    </template>
  </div>
</template>
<script>
export default {
  data() {
    return {
      pages: [],
      fields: ["index", "id", "link", "template", "modified","title","status"],
      sortBy: "link"
    };
  },
  async fetch() {
    this.pages = await fetch(
      "https://www.finereport.com/en/wp-json/wp/v2/pages?per_page=100&status=publish",
      { method: "GET" }
    ).then(res => res.json());
  }
};
</script>

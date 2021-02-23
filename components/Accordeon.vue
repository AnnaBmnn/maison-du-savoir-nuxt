<template>
  <ul class="accordeon">
    <Item
      v-for="theme in themes"
      :key="theme.UID"
      :theme="theme"
      :episodes="
        episodes
          .filter((episode) => episode.data.theme.id === theme.id)
          .sort((a, b) => {
            const orderA = a.data.order;
            const orderB = b.data.order;
            let comparison = 0;
            if (orderA > orderB) {
              comparison = 1;
            } else if (orderA < orderB) {
              comparison = -1;
            }
            return comparison;
          })
      "
      :authors="
        authors.filter((author) => {
          let isAuthor = false;
          theme.data.authors.forEach((themeAuthor) => {
            if (themeAuthor.author.id === author.id) {
              isAuthor = true;
            }
          });
          return isAuthor;
        })
      "
    />
  </ul>
</template>
<script>
export default {
  props: {
    themes: {
      type: Array,
      required: true,
    },
    episodes: {
      type: Array,
      required: true,
    },
    authors: {
      type: Array,
      required: true,
    },
  },
  computed: {},
  method: {
    compareOrder(a, b) {
      const orderA = a.data.order;
      const orderB = b.data.order;
      if (orderA > orderB) {
        comparison = 1;
      } else if (orderA < orderB) {
        comparison = -1;
      }
      return comparison;
    },
  },
  mounted() {},
  methods: {},
};
</script>
<style scoped>
.accordeon {
  margin: 5vw 0 13vw;
  padding: 0;
}
</style>

<template>
  <ul class="accordeon">
    <Item
      v-for="theme in themes"
      :key="theme.UID"
      :theme="theme"
      :episodes="episodes.filter((episode) => episode.data.theme.id === theme.id)"
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
  method: {},
  mounted() {
    // console.log(this.themes[5].data.authors[0].author);
    // console.log(this.themes[0].data.authors);
    // console.log(
    //   this.themes[0].data.authors.filter((themeAuthor) =>
    //     this.authors.filter((author) => themeAuthor.author.id === author.id)
    //   )
    // );
  },
  methods: {},
};
</script>
<style scoped>
.accordeon {
  margin: 5vw 0 13vw;
  padding: 0;
}
</style>

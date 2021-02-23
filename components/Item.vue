<template>
  <li
    v-if="episodes.length > 0"
    class="accordeon__item-container"
    :aria-label="`ouvrir les épisode du thème ${$prismic.asText(theme.data.title)}`"
  >
    <button :class="`accordeon__item ${show ? 'is-open' : ''} `" @click="showList">
      <h3>{{ $prismic.asText(theme.data.title) }}</h3>
      <img
        src="~/assets/img/cross.svg"
        alt="toggle accordeon"
        width="6vw"
        height="6vw"
        class="accordeon__icon"
      />
    </button>
    <div v-show="show && authors.length > 0" class="accordeon__author">
      par
      <span v-for="(author, index) in authors" :key="author.UID">
        {{ $prismic.asText(author.data.name) }}
        {{ index !== authors.length - 1 ? "&" : "" }}
      </span>
    </div>
    <button
      class="accordeon__btn"
      @click="showDescriptionFunc"
      v-show="show && theme.data.summary.length > 0"
    >
      <span v-show="!showDescription" class="accordeon__btn-icon accordeon__btn-icon--open">?</span>
      <span v-show="showDescription">
        <img
          src="~/assets/img/cross.svg"
          alt="toggle accordeon"
          width="2rem"
          height="2rem"
          :class="
            showDescription
              ? 'accordeon__btn-icon accordeon__btn-icon--close'
              : 'accordeon__btn-icon accordeon__btn-icon--open'
          " /></span
      >à propos
    </button>
    <p class="accordeon__txt" v-show="show && theme.data.summary.length > 0 && showDescription">
      {{ $prismic.asText(theme.data.summary) }}
    </p>
    <Cards v-show="show" :episodes="episodes" />
  </li>
</template>
<script>
export default {
  props: {
    theme: {
      type: Object,
      required: true,
    },
    episodes: {
      type: Array,
      required: false,
    },
    authors: {
      type: Array,
      required: false,
    },
  },
  data() {
    return {
      show: false,
      showDescription: false,
    };
  },
  methods: {
    showList() {
      this.show = !this.show;
    },
    showDescriptionFunc() {
      this.showDescription = !this.showDescription;
    },
  },
};
</script>
<style scoped>
.accordeon__item {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  cursor: pointer;
  margin-bottom: 0vw;
  /* margin: 2vw 0 2vw; */
  list-style: none;
  font-size: 8vw;
  border-top: 5px solid #020202;
  padding: 0.7vw 0vw 1.3vw 1vw;
}

.is-open .accordeon__icon {
  transform: rotate(45deg);
}

.accordeon__item:hover {
  font-style: italic;
}
.accordeon__btn {
  margin: 3.2rem 0 0;
  text-align: left;
  text-decoration: underline;
  font-size: 1.3rem;
}
.accordeon__btn-icon--open {
  /* border-radius: 50%;
  background-color: black;
  color: black; */
}
.accordeon__btn-icon {
  width: 1.1rem;
  height: 1.1rem;
  padding-left: 1vw;
}
.accordeon__btn-icon--close {
  transform: rotate(45deg);
  margin-right: 0.4rem;
}
.accordeon__btn:hover {
  font-style: italic;
}
.accordeon__icon {
  margin: 1.15vw 14px 0;
  width: 4.1vw;
  height: auto;
}

.accordeon__item h3 {
  margin: 0;
  text-align: left;
  font-size: 5vw;
}
.accordeon__item.is-open {
  border-bottom: none;
}

.accordeon__txt {
  text-transform: initial;
  width: 66%;
  font-size: 1.2rem;
  line-height: 1.4;
  margin: 1.6rem 0px 9vw;
}

.accordeon__item-container:last-of-type .accordeon__item {
  border-bottom: 5px solid #020202;
}
.accordeon__item-container:last-of-type
  .is-open.accordeon__item
  + .accordeon__author
  + .cards:after {
  opacity: 1;
}

.accordeon__item-container:last-of-type .is-open.accordeon__item {
  border-bottom: none;
}
.accordeon__author {
  font-size: 1.7vw;
  margin-bottom: 1vw;
  padding-left: 1vw;
}
@media screen and (max-width: 800px) {
  .accordeon__item {
    border-top: 3px solid black;
    align-items: flex-start;
    text-align: left;
  }
  .accordeon__item h3 {
    font-size: 7vw;
  }
  .accordeon__icon {
    margin: 1vw 0.6vw 14px;
    width: 8vw;
    height: 7vw;
  }
  .accordeon__author {
    font-size: 5vw;
    margin: 3vw 0;
  }
  .accordeon__item-container:last-of-type .accordeon__item {
    border-bottom: 3px solid black;
  }
}
</style>

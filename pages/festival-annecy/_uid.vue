<template>
  <section class="webgl-project">
    <h1 class="webgl-project__title">{{ $prismic.asText(title) }}</h1>
    <!-- Slices block component -->
<!--    <slices-block :slices="slices"/>-->
  </section>
</template>

<script>
// Imports for Prismic Slice components
import SlicesBlock from '~/components/SlicesBlock.vue'

export default {
  name: 'page',
  components: {
    SlicesBlock
  },
  head () {
    return {
      title: 'Prismic Nuxt.js Multi Page Website',
    }
  },
  async asyncData({ $prismic, params, error }) {
    try{
      // Query to get post content
      const document = (await $prismic.api.getByUID('festivalproject', params.uid)).data;
      return {
        // Set slices as variable
        title: document.title,
        tab: document.body1,

      }
    } catch (e) {
      // Returns error page
      error({ statusCode: 404, message: 'Page not found' })
    }
  },
}
</script>

<style lang="sass" scoped>
  .webgl-project__title
    margin: 320px auto
    text-align: center

</style>

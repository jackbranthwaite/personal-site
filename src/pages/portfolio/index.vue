<template>
  <div v-if="projects" class="container">
    <h1 class="title">portfolio</h1>
    <div
      v-for="project in projects.results"
      :key="project.id"
      class="card-container"
    >
      <portfolio-card
        :title="project.data.title[0].text"
        :description="project.data.description[0].text"
        :image="project.data.title_image.url"
        :link="project.id"
      />
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from '@vue/composition-api'
import { useContext, useAsync } from '@nuxtjs/composition-api'
import PortfolioCard from '~/components/portfolio-card/PortfolioCard.vue'

export default defineComponent({
  name: 'Portfolio',
  components: { PortfolioCard },
  setup() {
    const { $prismic } = useContext()

    const projects = useAsync(async () => {
      return await $prismic.api.query(
        $prismic.predicates.at('document.type', 'project')
      )
    })

    return { projects }
  }
})
</script>

<style lang="scss" scoped>
@import '~assets/styles/config';
.container {
  margin: auto;
  margin-top: 2vw;
  width: 80vw;
}
.card-container {
  display: grid;
  gap: 2vw;
  grid-template-columns: 1fr 1fr 1fr;
  margin-top: 2vw;
}
@include tablet {
  .card-container {
    gap: 4vw;
    grid-template-columns: 1fr 1fr;
  }
}
@include mobile-l {
  .card-container {
    gap: 50px;
    grid-template-columns: 1fr;
  }
}
</style>

<!-- <portfolio-card
        title="Workplace Employee Site"
        description="Group unversity project built with the MERN stack. "
        link="2"
      />
      <portfolio-card
        title="Android Web Browser"
        description="Web browser built in Java for a university project"
        link="3"
      />
      <portfolio-card
        title="Android Todo List"
        description="Todo list application built in Java for a university project"
        link="4"
      />
      <portfolio-card
        title="iOS Todo List"
        description="Todo list application built in Swift for a university project"
        link="5"
      /> -->
<!-- <portfolio-card
        title="Todo List Website"
        description="A simple todo list application built in Vanilla JavaScript. Based on a tutorial found on YouTube"
        link="6"
      /> -->

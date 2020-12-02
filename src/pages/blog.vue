<template>
  <Layout>
    <!-- Page Header -->
    <!-- home-bg.jpg -->
    <!-- backgroundImage: `url(${GRIDSOME_API_URL + general.cover.url})`, -->

    <header
      class="masthead"
      style="background-image: url('img/post-sample-image.jpg')"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>md文件</h1>
              <span class="subheading">自动生成</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div
            class="post-preview"
            v-for="edge in $page.posts.edges"
            :key="edge.node.id"
          >
            <div to="'/post/' + edge.node.id">
              <!-- <h2 class="post-title">
                {{ edge.node.title }}
              </h2> -->
              <div v-html="edge.node.content"></div>
            </div>
            <hr />
          </div>

          <Pager class="pager" :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query($page: Int) {
  posts: allMdblog(perPage: 5, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        title
        content
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'
export default {
  name: 'BlogMarkdownPage',
  components: {
    Pager
  },
  metaInfo: {
    title: '源为md'
  },
  computed: {
    general () {
      return this.$page.general.edges[0].node
    }
  }
}
</script>

<style>
.pager a {
  margin-right: 30px;
}
</style>

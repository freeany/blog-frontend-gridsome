<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1># {{ $page.tag.title }}</h1>
              <span class="subheading">该标签下所有文章</span>
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
            v-for="post in $page.tag.posts"
            :key="post.id"
          >
            <g-link :to="'/post/' + post.id">
              <h2 class="post-title"># {{ post.title }}</h2>
            </g-link>
            <!-- <p class="post-meta">
              Posted by
              <a href="#">{{
                edge.node.create_by.firstname + edge.node.create_by.lastname
              }}</a>
              on {{ edge.node.created_at }}
            </p> -->
          </div>
          <!-- <Pager class="pager" :info="$page.posts.pageInfo" /> -->
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query($id: ID!) {
  tag: strapiTag(id: $id) {
    id
    title
    posts {
      id
      title
      create_by
    }
  }
}
</page-query>

<script>

export default {
  name: 'tagPage',
  metaInfo: {
    title: '标签页面'
  }
}
</script>

<style>
</style>

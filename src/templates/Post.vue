<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + $page.post.cover.url})`,
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.post.title }}</h1>
              <!-- 下面是副标题 -->
              <!-- <h2 class="subheading">
                Problems look mighty small from 150 miles up
              </h2> -->
              <span class="meta"
                >Posted by
                <a href="#">{{
                  $page.post.create_by.firstname + $page.post.create_by.lastname
                }}</a>
                on {{ $page.post.created_at }}</span
              >
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div
            class="col-lg-8 col-md-10 mx-auto"
            v-html="mdToHtml($page.post.content)"
          ></div>
        </div>
      </div>
    </article>
  </Layout>
</template>

<page-query>
query($id: ID!) {
  post:strapiPost(id: $id) {
    id
    title
    content
     cover {
			url    
    }
    create_by {
      id
      lastname
      firstname
    }
    tags {
      id
      title
    }
    created_at
  }
}
</page-query>

<script>
import markdownIt from 'markdown-it'
const md = new markdownIt()
import axios from 'axios'
export default {
  name: 'postPage',
  metaInfo: {
    title: '文章详情',
    // meta: [
    //   {
    //     'http-equiv': "Content-Security-Policy",
    //     'content': "upgrade-insecure-requests"
    //   }
    // ]
  },
  mounted () {
    this.getImage()
  },
  methods: {
    mdToHtml (markdown) {
      return md.render(markdown)
    },
    async getImage () {
      const r = await axios.get('http://39.97.66.133:1337/uploads/about_bg_9153bcc02d.jpg')
      console.log(r)
    }
  }
}
</script>

<style>
</style>



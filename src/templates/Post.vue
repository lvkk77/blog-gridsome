<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + $page.strapiPost.cover.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.strapiPost.title }}</h1>
              <!-- <h2 class="subheading">Problems look mighty small from 150 miles up</h2> -->
              <span class="meta">Posted by
                <a href="#">{{ $page.strapiPost.created_by.firstname + $page.strapiPost.created_by.lastname }}</a>
                on {{ $page.strapiPost.created_at }}</span>
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
            v-html="mdToHtml($page.strapiPost.content)"
          >

          </div>
        </div>
      </div>
    </article>

    <hr>

  </Layout>
</template>

<page-query>
query ($id: ID!) {
  strapiPost (id: $id){
    id
    title
    content
    created_at
    cover {
      url
    }
    created_by{
      id
      firstname
      lastname
    }
    tags {
      id
      title
    }
  }
}
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt();

export default {
  name: 'PostPage',
  methods: {
    mdToHtml (markdown) {
      return md.render(markdown)
    }
  }
}
</script>

<style>
</style>
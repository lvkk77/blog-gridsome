<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + general.cover.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
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
            v-for=" item in $page.posts.edges"
            :key="item.node.id"
          >
            <g-link :to="'/post/'+ item.node.id">
              <h2 class="post-title">
                {{ item.node.title }}
              </h2>
              <!-- <h3 class="post-subtitle">
                Problems look mighty small from 150 miles up
              </h3> -->
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#">{{ item.node.created_by.firstname + item.node.created_by.lastname }}</a>
              on {{ item.node.created_at }}
            </p>

            <p>
              <g-link
                :to="'/tag/'+ tag.id"
                v-for="tag in item.node.tags"
                :key="tag.id"
              >
                {{ tag.title }} &nbsp;
              </g-link>
            </p>
            <hr />
          </div>

          <Pager :info="$page.posts.pageInfo" />

          <!-- Pager -->
          <!-- <div class="clearfix">
            <a
              class="btn btn-primary float-right"
              href="#"
            >Older Posts &rarr;</a>
          </div> -->
        </div>
      </div>
    </div>
    <hr />
  </Layout>
</template>

<page-query>
  query ($page: Int) {
    posts: allStrapiPost (perPage: 5, page: $page) @paginate {
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          id
          title
          content
          created_at
          tags{
            id
            title
          }
          created_by {
            id
            firstname
            lastname
          }
        }
      }
    }

    general: allStrapiGeneral{
      edges{
        node{
          id
          title
          subtitle
          cover {
            url
          }
        }
      }
    }
  }
</page-query>

<script>
import { Pager } from 'gridsome'
export default {
  name: "HomePage",
  metaInfo: {
    title: 'Hello, world!',
  },
  components: {
    Pager
  },
  computed: {
    general(){
      return this.$page.general.edges[0].node
    }
  },
}
</script>

<style></style>

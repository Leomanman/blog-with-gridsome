<template>
  <Layout>
    <!-- Page Header-->
    <header
      class="masthead"
      :style="{
        backgroundImage: `url(${GRIDSOME_API_URL + general.cover.url})`,
      }"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <!-- Post preview-->
          <div
            class="post-preview"
            v-for="edges in $page.posts.edges"
            :key="edges.node.id"
          >
            <g-link :to="`/post/${edges.node.id}`">
              <h2 class="post-title">
                {{ edges.node.title }}
              </h2>
              <!-- <h3 class="post-subtitle">
                Problems look mighty small from 150 miles up
              </h3> -->
            </g-link>
            <p class="post-meta">
              <!-- Posted by -->
              <!-- <a href="#!">Start Bootstrap</a> -->
              <g-link
                :to="`/tag/${tag.id}`"
                v-for="tag in edges.node.tags"
                :key="tag.id"
                >{{ tag.title }}</g-link
              >
              <!-- on September 24, 2022 -->
              {{ edges.node.created_at }}
            </p>
            <hr class="my-4" />
          </div>
          <!-- Divider-->

          <!-- Pager-->
          <!-- <div class="d-flex justify-content-end mb-4">
            <a class="btn btn-primary text-uppercase" href="#!"
              >Older Posts →</a
            >
          </div> -->
          <div class="page-nav">
            <Pager :info="$page.posts.pageInfo" />
          </div>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($page: Int) {
  posts: allStrapiPost(perPage:2, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    },
    edges{
      node{
        id,
        title,
        content,
        tags  {
          id,
          title
        },
        created_at
      }
    }
  },
  general: allStrapiGeneral{
    edges{
      node{
        title,
        subtitle,
        cover{
          url
        }
      }
    }
  }
}

</page-query>

<script>
import { Pager } from "gridsome";
export default {
  name: "IndexPage",
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager,
  },
  computed: {
    general() {
      return this.$page.general.edges[0].node;
    },
  },
};
</script>

<style>
.page-nav a {
  display: inline-block;
  margin-right: 10px;
  width: 30px;
  text-align: center;
  border: 1px solid #999;
}
.page-nav .active {
  background: coral;
}
</style>

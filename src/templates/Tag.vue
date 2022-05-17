a<template>
  <Layout>
    <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1># {{ $page.tag.title}}</h1>
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
            v-for="edges in $page.tag.posts"
            :key="edges.id"
          >
            <g-link :to="`/post/${edges.id}`">
              <h2 class="post-title">
                {{ edges.title }}
              </h2>
              <!-- <h3 class="post-subtitle">
                Problems look mighty small from 150 miles up
              </h3> -->
            </g-link>
            <hr class="my-4" />
          </div>
          <!-- Divider-->
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query($id: ID!){
    tag: strapiTag(id: $id) {
        id,
        title,
        posts{
            id,
            title
        }
    }
}
</page-query>

<script>
export default {
  name: "TagPage",
  metaInfo: {
    title: "tag",
  },
};
</script>

<style>
</style>

<template>
  <Layout>
    <h1 v-html="$page.drupalNodeArticle.title"></h1>

    <section v-if="$page.drupalNodeArticle.field_tags" class="article__tags">
      Tags:
      <span
        v-for="tag in $page.drupalNodeArticle.field_tags" 
        :key="tag.node.name">
          <a :href="tag.node.path">{{ tag.node.name }}</a>
      </span>
    </section>

    <g-image v-if="$page.drupalNodeArticle.field_image" :src="$page.drupalNodeArticle.field_image.node.image_style_uri[0].large" />

    <p>{{ $page.drupalNodeArticle.date }}</p>
    <p v-html="$page.drupalNodeArticle.body.processed"></p>
  </Layout>
</template>

<page-query>
  query Article ($path: String!) {
    drupalNodeArticle (path: $path) {
      title,
      date,
      body {
        processed
      }
      field_tags {
        node {
          name,
          path
        }
      },
      field_image {
        node {
          filename,
          uri {
            url
          }
          image_style_uri {
            large
          }
        },
        meta {
          alt,
          title
        }
      }
    }
  }
</page-query>

<style>
  .article__tags {
    margin-top: -20px;
    margin-bottom: 20px;
  }

  .article__tags span {
    margin-right: 5px;
  }
</style>

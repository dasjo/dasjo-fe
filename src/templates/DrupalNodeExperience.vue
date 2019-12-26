<template>
  <Layout>
    <h1 v-html="node.title"></h1>

    <section v-if="node.field_tags">
      Tags:
      <span
        v-for="tag in node.field_tags" 
        :key="tag.node.name">
          <a :href="tag.node.path">{{ tag.node.name }}</a>
      </span>
    </section>

    <span v-html="node.from"/> to <span v-html="node.to"/>

    <p>{{ node.timespan }}</p>
    <p v-html="node.body.processed"></p>
  </Layout>
</template>

<script>
  export default {
    computed: {
      node() { 
        return {
          ...this.$page.node,
          ...{
            from: this.$page.node.field_timespan.value.substring(0,7),
            to: this.$page.node.field_timespan.end_value.substring(0,7)
          }
        }
      }
    }
  }
</script>

<page-query>
  query Experience ($path: String!) {
    node: drupalNodeExperience (path: $path) {
      title,
      field_timespan {
        value
        end_value
      }
      field_link {
        uri
      }
      body {
        processed
      }
      field_tags {
        node {
          name,
          path
        }
      }
    }
  }
</page-query>

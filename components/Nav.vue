<template>
  <nav>
    <nuxt-link to="/">DevBlau</nuxt-link>
    <ul class="menu">
      <li v-for="item in menu" :key="item.node.id">
        <nuxt-link :to="item.node.path">{{ item.node.label }}</nuxt-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Nav',
  data() {
    return {
      menu: [],
    }
  },
  async fetch() {
    const menu = await fetch('http://next-js-blog.inset.com.br/api', {
      headers: { 'Content-Type': 'application/json' },
      method: 'POST',
      body: JSON.stringify({
        query: `query getMenu {
                  menu(id: "main", idType: NAME) {
                    menuItems {
                      edges {
                        node {
                          label
                          id
                          path
                        }
                      }
                    }
                  }
                }
                `,
      }),
    })
    const res = await menu.json()
    this.menu = res.data.menu.menuItems.edges
  },
}
</script>

<style></style>

<template>
  <div id="shop_wrap">
    <CatalogNavMenu/>
    <CatalogProductsView/>
    <Advertising/>
  </div>
</template>

<script>
  import CatalogNavMenu from "@/components/catalog/CatalogNavMenu";
  import CatalogProductsView from "@/components/catalog/CatalogProductsView";
  import Advertising from "@/components/catalog/Advertising";

  export default {
    components: {Advertising, CatalogProductsView, CatalogNavMenu},
    async fetch({store, params}) {
      let group = store.getters.PRODUCT_TREE.filter(el => el.value === params.group)
      if (group && group[0]) {
        await store.dispatch('USER_EVENT', `Каталог: ${group[0].label}`)
      }
    },
    methods: {},
    created() {
      this.$store.dispatch('fetchProducts') // NOTE: not in the fetch method because lastVisible object - circular
    }
  }
</script>

<style scoped lang="scss">
  #shop_wrap {
    display: flex;
    justify-content: start;
    flex-wrap: wrap;
  }
</style>

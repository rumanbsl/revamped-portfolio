<script lang="ts" setup>
const route = useRoute();
const { data: contentNavs } = await useAsyncData("navigation", () => fetchContentNavigation());

const does = computed(() => {
  const title = contentNavs.value.find((content) => content._path === route.path)?.title;
  switch (title) {
    case "Home":
      return "codes";
    default:
      return "writes";
  }
});
const baseUrl = "/";
</script>

<template>
  <main>
    <t-container class="navigation">
      <NuxtLink :to="baseUrl">
        <h1 class="navigation_title">ruman {{ does }}</h1>
      </NuxtLink>
      <p class="navigation_blog">
        <NuxtLink :to="baseUrl + 'blog'">Blog</NuxtLink>
      </p>
    </t-container>
    <NuxtPage></NuxtPage>
  </main>
</template>

<style lang="scss">
/* inject global styles */
@import "./app.scss";
</style>

<style lang="scss" scoped>
.navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  &_title {
    font-family: Library ThreeAM;
    font-weight: unset;
  }
}
</style>

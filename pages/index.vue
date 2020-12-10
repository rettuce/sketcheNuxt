<template>
  <div id="index">
    <template v-for="item in data">
      <article :id="item.id">
        <NuxtLink :to="'/test/' + item.id + '/'">
          <h3 class="first_title">
            <span>{{ item.title }}</span>
          </h3>
        </NuxtLink>
      </article>
    </template>
  </div>
</template>

<script>
export default {
  async asyncData({ params, redirect, error }) {
    const json = await import(`@/assets/data.json`);
    let data = json.post;
    return { data };
  }
};
</script>

<style lang="scss" scoped></style>

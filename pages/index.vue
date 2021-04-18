<template>
  <div class="m-8">
    <TheHeader />

    <h1 class="font-bold text-4xl mb-4">Bulenya</h1>
    <ul class="flex flex-wrap">
      <li
        v-for="article of articles"
        :key="article.slug"
        class="xs:w-full md:w-1/2 px-2 xs:mb-6 md:mb-12 article-card"
      >
        <NuxtLink
          :to="{ name: 'blog-slug', params: { slug: article.slug } }"
          class="flex transition-shadow duration-150 ease-in-out shadow-md hover:shadow-lg xxlmax:flex-col"
        >
          <ImageMd
            v-if="article.img"
            :src="article.img"
            :alt="article.alt"
            class="h-48 xxlmin:w-1/2 xxlmax:w-full object-cover"
          />

          <div
            class="p-6 flex flex-col justify-between xxlmin:w-1/2 xxlmax:w-full"
          >
            <h2 class="font-bold">{{ article.title }}</h2>
            <p>
              {{ article.description }}
            </p>
            <p class="font-bold text-gray-600 text-sm">
              {{ formatDate(article.date) }}
            </p>
          </div>
        </NuxtLink>
      </li>
    </ul>
    <h3 class="mb-4 font-bold text-2xl uppercase text-center">Topics</h3>
    <ul class="flex flex-wrap mb-4 text-center">
      <li
        v-for="tag of tags"
        :key="tag.slug"
        class="xs:w-full md:w-1/3 lg:flex-1 px-2 text-center"
      >
        <NuxtLink :to="`/blog/tag/${tag.slug}`" class="">
          <p
            class="font-bold text-gray-600 uppercase tracking-wider font-medium text-ss"
          >
            {{ tag.name }}
          </p>
        </NuxtLink>
      </li>
    </ul>
    <footer class="flex justify-center border-gray-500 border-t-2">
      <p class="mt-4">
        Written by
        <a
          href="https://www.linkedin.com/in/%F0%9F%8E%BE-pol-milian-707a214b/"
          class="font-bold hover:underline"
          target="_blank"
          rel="noopener"
          >Pol Milian</a
        >, 2021
      </p>
    </footer>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content("articles", params.slug)
      .only(["title", "description", "img", "slug", "date", "alt"])
      .where({ isDraft: false })
      .sortBy("date", "desc")
      .fetch();
    const tags = await $content("tags", params.slug)
      .only(["name", "description", "img", "slug"])
      .sortBy("createdAt", "asc")
      .fetch();
    return {
      articles,
      tags,
    };
  },
  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("en", options);
    },
  },
};
</script>

<style class="postcss">
.article-card {
  border-radius: 8px;
}
.article-card a {
  background-color: #fff;
  border-radius: 8px;
}
.article-card img div {
  border-radius: 8px;
}
</style>

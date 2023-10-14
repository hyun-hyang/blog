<template>
    <article class="relative max-w-6xl mx-auto justify-center mb-10 md:mb-10">
      <header class="flex flex-col item-start text-base justify-center text-center mt-1 mb-7">
        <nuxt-link :to="{path: '/essay'}" replace>
          <span class="text-base md:text-base text-cherry mb-2  ">{{ article.category }}</span>
          <!-- hover:drop-shadow -->
        </nuxt-link>
        <h1 class="px-5 md:px-0 mt-6 mb-5 text-3xl md:text-5xl text-center font-bold text-gray-700 break-all">
          {{ article.title }}
        </h1>
        <p class="text-base md:text-base text-gray-500 text-center">{{article.author}} {{article.datetime}}</p>
        <h1 class="px-1 md:px-0 mt-1 mb-5 text-1xl md:text-1xl text-center font-medium text-gray-700 break-all">
        </h1>
        <!-- <p class="text-base md:text-base text-gray-500 text-center">{{article.datetime}}</p>
        <h1 class="px-1 md:px-0 mt-1 mb-5 text-1xl md:text-1xl text-center font-medium text-gray-700 break-all">
          {{article.author}}
        </h1> -->
      </header>

      <div class="p-4 gap-4">
        <div>
        <!-- <div class="prose lg:prose-lg "> -->
          <!-- <div class="text-base max-w-prose"> -->
          <nuxt-content :document="article" class="prose max-w-5xl custom-text" />

          <div class="space-x-2 flex-1 mt-7 mb-3 px-6">
            <div class="inline-flex text-gray-700 text-xs md:text-base">Tags:</div>
            <div v-for="tag in article.tags" :key="{tag}" 
                    class="inline-flex text-center px-3 py-1 rounded-full bg-gray-100 text-gray-600 text-xs mb-1">#{{ tag }}
            </div>
          </div>

        </div>
        </div>

        //<div class="relative h-32 w-32 ...">
          //<div class="absolute inset-y-0 right-0 w-16 ...">06</div>
        //</div>


        <aside ref="toc" class="lg:flex lg:flex-col">
          <div class="sticky top-16">
            <h2 class="uppercase text-black font-h2 text-lg lg:mt-16 tracking-wider">
              Table of contents
            </h2>
            <nav class="mt-4">
              <ul>
                <li
                  @click="tableOfContentsHeadingClick(link)"
                  :class="{
                    'pl-4': link.depth === 3,
                  }"
                  class="toc-list"
                  v-for="link of article.toc"
                  :key="link.id"
                >
                  <a
                  :class="{
                      'text-red-500 hover:text-red-600': link.id === currentlyActiveToc,
                      'text-black hover:gray-900': link.id !== currentlyActiveToc,
                    }"
                    role="button"
                    class="transition-colors duration-75 text-sm mb-2 block"
                    :href="`#${link.id}`"
                    >{{ link.text }}</a
                  >
                </li>
              </ul>
            </nav>
          </div>
        </aside>
      
    </article>

</template>

<script>
export default {
  data() {
    return {
      currentlyActiveToc: "",
      observer: null,
      observerOptions: {
        root: this.$refs.nuxtContent,
        threshold: 0,
      },
    };
  },
  mounted() {
    this.observer = new IntersectionObserver(entries => {
      entries.forEach(entry => {
          const id = entry.target.getAttribute('id');
          if (entry.isIntersecting) {
            this.currentlyActiveToc = id;
          }
      });
    }, this.observerOptions);

    // Track all sections that have an `id` applied
    document.querySelectorAll('.nuxt-content h2[id], .nuxt-content h3[id]').forEach((section) => {
        this.observer.observe(section);
    });
  },
  beforeDestroy() {
    this.observer.disconnect();
  },
  async asyncData({ $content, params }) {
      const article = await $content('blog', params.slug).fetch();

      return { article }
      // fetch our articles here
  },
  methods: {
    tableOfContentsHeadingClick(link) {
      this.currentlyActiveToc = link.id;
    },
    formatDate(date){
        return new Date(date).toLocaleDateString('en', {year: 'numeric', month: 'long', day: 'numeric'})
    },
  }
}
</script>

<style scpoed>
    .custom-text{
        word-break: keep-all;
    }
</style>

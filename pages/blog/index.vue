<template>
    <div class="max-w-6xl mx-auto">
      <header class="pt-6 pb-9 sm:pb-16 text-center">
        <h1 class="mb-4 text-4xl sm:text-6xl tracking-tight text-slate-800 font-extrabold">
          Blog
        </h1>
        <p class="text-lg text-slate-600">
          나의 글 모음들
        </p>
      </header>

      <div class="px-5">
          <div class="pt-10 md:pt-12 text-xl md:text-2xl text-gray-700 font-semibold mb-2">모든 글보기</div>
          <div class="text-gray-600 font-normal text-sm md:text-base">블로그의 모든 글 모음입니다. 주제별로 글을 보고 싶다면 아래 태그를 선택해주세요.</div>
      </div>
  
      <div class="px-5 pt-10">
        <nuxt-link :to="{path: '/computer-architecture'}" replace><span class="tag-btn">#<span class="text-gray-600 text-sm">컴퓨터구조</span></span></nuxt-link>
      </div>

      <div class="max-w-6xl grid grid-cols-1 md:grid-cols-1 mt-11 md:mt-12 mb-8 md:mb-12 rounded-xl shadow-md overflow-hidden md:max-w-6xl">
          <div class="px-5 md:px-6 group" v-for="article of articles" :key="article">
            <nuxt-link :to='`/blog/${article.slug}`'>
                <div class="article-inner flex justify-between border-t py-6 border-gray-200">
                  <div class="w-full md:w-5/6">
                      <p class="mb-1 md:mb-1 text-sm md:text-sm font-medium text-cherry group-hover:text-gray-400">{{article.category}}</p>
                      <h3 class="mb-1 md:mb-1.5 text-lg md:text-xl font-semibold text-gray-700 transition group-hover:text-cherry group-hover:duration-500">{{ article.title }}</h3>
                      <p class="mb-1 md:mb-1.5 text-sm md:text-base text-gray-500 custom-text">{{article.description}}</p>
                      <p class="text-sm md:text-sm text-gray-400">{{ article.datetime }}</p>
                  </div>
                  <div class="hidden md:block pl-4 pr-6">
                    <div class="h-full py-10">
                      <outline-link-icon class="w-6 h-6 text-gray-400 group-hover:text-gray-700 transition duration-200" />
                    </div>            
                  </div>
                </div>
            </nuxt-link>
          </div>
      </div>
    </div>
</template>
  
<script>
export default {
    async asyncData({ $content, params }) {
      const articles = await $content('blog', params.slug)
        .sortBy("datetime", "desc")
        .fetch();
      return {
        articles
      }
    },
}
</script>

<style scoped>
    .custom-text{
        word-break: keep-all;
    }
</style>    
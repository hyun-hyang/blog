<template>
  <div class="max-w-6xl mx-auto">
     <!--블로그 소개-->
     <div class="pt-16">
      <div class="pt-14 md:pt-36 pb-0 md:pb-10 max-w-6xl mx-auto px-6">
          <h2 class="pb-6 poppins text-left md:text-left text-4xl md:text-6xl font-extrabold text-gray-800 font-title">
            Hello world, I'm <span class="highlight-sm font-title">Hyun-hyang</span> !
          </h2>
          <div class="font-normal text-sm md:text-base text-gray-600 keepall">
            나의 기록😾들을 담는 곳, <br> 주로 CS와 관련된 내용을 다룹니다.
          </div>
      </div>
    </div>
    <!-- latest articles -->
    <div class="px-5">
        <div class="pt-10 md:pt-12 text-lg md:text-xl text-gray-700 font-bold mb-2">최근 글보기</div>
        <div class="text-gray-600 font-normal text-sm md:text-base">최근 업로드 된 글 모음입니다. 주제별로 글을 보고 싶다면 아래 태그를 선택해주세요.</div>
    </div>

    <div class="px-5 pt-10">
      <nuxt-link :to="{path: '/computer-architecture'}" replace><span class="tag-btn">#<span class="text-gray-600 text-sm">컴퓨터구조</span></span></nuxt-link>
    </div>

    <div class="max-w-4xl grid grid-cols-1 md:grid-cols-1 mt-5 md:mt-6 mb-8 md:mb-12">
        <div class="px-5 md:px-6 group" v-for="article of articles" :key="article">
          <nuxt-link :to='`/blog/${article.slug}`'>
              <div class="flex justify-between border-t py-6 border-gray-200">
                <div class="w-full md:w-5/6">
                    <p class="mb-1 md:mb-1 text-sm md:text-sm font-medium text-cherry group-hover:text-gray-400">{{article.category}}</p>
                    <h3 class="custom-text mb-1 md:mb-2 text-lg md:text-xl font-bold text-gray-700 transition group-hover:text-cherry group-hover:duration-500">{{ article.title }}</h3>
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
      .limit(5)
      .fetch(); 
    return {
      articles,
    }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
  }
}
</script>

<style scoped>
  .keepall{
      word-break: keep-all;
  }
  .nthz:nth-child(1){
    background-color: #C4C9FE;
    border-radius: 0.6rem;
  }
  .nthz:nth-child(2){
    background-color: #E5F6F1;
    border-radius: 0.6rem;
  }
  .nthz:nth-child(3){
    background-color: #F5EFD0;
    border-radius: 0.6rem;
  }
  .featbox {
      width: 250px;
      height: 160px; 
      border-radius: 5%;
      overflow: hidden;
  }
  .back-purple {
    background-color: #C4C9FE;
  }
  </style>
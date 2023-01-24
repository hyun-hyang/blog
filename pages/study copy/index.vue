<template>
    <div class="max-w-6xl mx-auto">
      <header class="pt-6 pb-9 sm:pb-16 text-center">
        <h1 class="mb-4 text-4xl sm:text-6xl tracking-tight text-slate-800 font-extrabold">
          Study
        </h1>
        <p class="text-lg text-slate-600">
          나의 공부 기록
        </p>
      </header>

      <div>
        <div class="border-b border-gray-300 py-7 px-5">
          <div class="pt-10 md:pt-12 text-xl md:text-2xl text-cherry font-semibold mb-2">2023-1학기</div>
          <div class="text-gray-600 font-normal text-sm md:text-base">What I learned from Tennessee Tech</div>
        </div>

        <div class="pt-10 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-x-5 gap-y-8 mb-60 pb-12 mx-5">
          <div v-for='study of studies' :key="study" >

            <nuxt-link :to='`study/${study.slug}/0-1`'>
              <div class="group" >
                <div class="h-40 grid grid-cols-1 md:grid-cols-1 mt-11 md:mt-12 mb-8 md:mb-12 px-5 py-5 rounded-xl shadow-md overflow-hidden">

                  <div class=" mb-1.5 flex items-center keep-all" >
                    <div class="text-slate-600 text-xl font-semibold group-hover:text-violet-500 transition duration-200 logo">{{study.name}}</div> 
                    <div class="flex items-center ">
                        <div v-if="`${study.state}` == '공부 완료'"  class="ml-2 px-1.5 py-1 text-xs md:text-xs text-white bg-indigo-400 rounded font-normal">공부 완료</div> 
                        <div v-else-if="`${study.state}` == '공부 중'"  class="ml-2 px-1.5 py-1 text-xs md:text-xs text-white bg-rose-400 rounded font-normal">공부 중</div> 
                        <div v-else class="ml-2 px-1.5 py-1 text-xs md:text-xs text-white bg-rose-400 rounded font-normal"> {{study.state}} </div> 
                    </div>
                  </div>
                  <div class="keep-all text-slate-500 mb-1.5">{{study.description}}</div>
                  
                </div>
              </div>
            </nuxt-link>

          </div>
        </div>
      </div>

      <div>
        <div class="border-b border-gray-300 py-7 px-5">
          <div class="pt-10 md:pt-12 text-xl md:text-2xl text-cherry font-semibold mb-2">2022-2학기</div>
          <div class="text-gray-600 font-normal text-sm md:text-base">과목별로 학과 공부의 수업내용을 정리해두었습니다. 주로 CS지식들을 담고 있습니다.</div>
        </div>

        <div class="pt-10 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-x-5 gap-y-8 mb-60 pb-12 mx-5">
          <div v-for='study of studies' :key="study" >

            <nuxt-link :to='`study/${study.slug}/0-1`'>
              <div class="group" >
                <div class="h-40 grid grid-cols-1 md:grid-cols-1 mt-11 md:mt-12 mb-8 md:mb-12 px-5 py-5 rounded-xl shadow-md overflow-hidden">

                  <div class=" mb-1.5 flex items-center keep-all" >
                    <div class="text-slate-600 text-xl font-semibold group-hover:text-violet-500 transition duration-200 logo">{{study.name}}</div> 
                    <div class="flex items-center ">
                        <div v-if="`${study.state}` == '공부 완료'"  class="ml-2 px-1.5 py-1 text-xs md:text-xs text-white bg-indigo-400 rounded font-normal">공부 완료</div> 
                        <div v-else-if="`${study.state}` == '공부 중'"  class="ml-2 px-1.5 py-1 text-xs md:text-xs text-white bg-rose-400 rounded font-normal">공부 중</div> 
                        <div v-else class="ml-2 px-1.5 py-1 text-xs md:text-xs text-white bg-rose-400 rounded font-normal"> {{study.state}} </div> 
                    </div>
                  </div>
                  <div class="keep-all text-slate-500 mb-1.5">{{study.description}}</div>
                  
                </div>
              </div>
            </nuxt-link>

          </div>
        </div>

      </div>

    </div>

      

    
    
</template>

<script>
export default {
    async asyncData({ $content, params }) {
        const studies = await $content('studies', params.id)
        .sortBy('order', 'asc')
        .fetch();
        return { studies }
        
    },
    name: 'PageIndex',
    head: {
    title: "JiMin Lim | Study",
    meta: [
      { charset: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        hid: "description",
        name: "description",
        content: "Study Log",
      },
    ],
    link: [{ rel: "icon", type: "image/x-icon", href: "/favicon.ico" }],
  },
}
</script>

<style scoped>
.keep-all{
    word-break: keep-all;
}
.inner {
  box-sizing: border-box;
  position: relative;
}
.lead-box {
    overflow: hidden;
}
.square-box {
    overflow: hidden;
}
.profile {
    object-fit: cover;
    /* overflow: hidden; */
}
</style>
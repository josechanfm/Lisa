<template>
  <Head>
    <Title>主頁</Title>
  </Head>

  <section class="relative bg-white pt-44 overflow-hidden lg:pt-12 mb-12">
    <div
      class="max-w-7xl h-96 flex flex-col-reverse gap-12 container px-4 mx-auto items-center lg:flex-row"
    >
      <div class="flex flex-col gap-6 w-full lg:w-1/2">
        <div class="text-4xl font-bold text-orange-400">我是呂源浩</div>
        <div class="text-4xl font-bold text-orange-400">Anthony Loi</div>
        <div class="text-md">
          歡迎來到我的網頁,這個網頁是我展示自己、分享我的經驗、以及與世界各地的人們聯繫的地方。
        </div>
      </div>
      <div class="relative w-full h-full lg:w-1/2 flex items-end">
        <div class="absolute overflow-hidden w-80 ml-6">
          <img src="../public/atis-assets/person/anthonyLol.png" />
        </div>
        <div class="box rounded-l-full w-full bg-orange-500 h-56"></div>
      </div>
    </div>
  </section>
  <div class="skew skew-bottom mr-for-radius">
    <svg
      class="h-8 md:h-12 lg:h-20 w-full text-orange-50"
      viewBox="0 0 10 10"
      preserveAspectRatio="none"
    >
      <polygon fill="currentColor" points="0 0 10 0 0 10"></polygon>
    </svg>
  </div>
  <div class="skew skew-bottom ml-for-radius">
    <svg
      class="h-8 md:h-12 lg:h-20 w-full text-orange-50"
      viewBox="0 0 10 10"
      preserveAspectRatio="none"
    >
      <polygon fill="currentColor" points="0 0 10 0 10 10"></polygon>
    </svg>
  </div>
  <section class="py-24">
    <div class="max-w-7xl container px-4 mx-auto">
      <div class="w-full lg:w-2/3 mb-16">
        <h2 class="my-5 text-4xl font-bold font-heading text-orange-400">職業生涯</h2>
        <p class="text-lg text-gray-500">分享我職業生涯的重要時刻</p>
      </div>
    </div>
  </section>
  <div class="skew skew-bottom mr-for-radius">
    <svg
      class="h-8 md:h-12 lg:h-20 w-full text-orange-50"
      viewBox="0 0 10 10"
      preserveAspectRatio="none"
    >
      <polygon fill="currentColor" points="0 0 10 0 0 10"></polygon>
    </svg>
  </div>
  <div class="skew skew-bottom ml-for-radius">
    <svg
      class="h-8 md:h-12 lg:h-20 w-full text-orange-50"
      viewBox="0 0 10 10"
      preserveAspectRatio="none"
    >
      <polygon fill="currentColor" points="0 0 10 0 10 10"></polygon>
    </svg>
  </div>
  <section class="py-24">
    <div class="max-w-7xl container px-4 mx-auto">
      <div class="w-full lg:w-2/3 mb-16">
        <h2 class="my-5 text-4xl font-bold font-heading text-orange-400">專業資格</h2>
        <p class="text-lg text-gray-500">從各大機構獲得的認可</p>
      </div>
    </div>
  </section>
  <section class="relative py-24 bg-orange-500 overflow-hidden">
    <div class="max-w-7xl relative container px-4 mx-auto">
      <div class="max-w-md mb-10">
        <h2 class="mb-4 text-4xl font-bold text-white">想要聯絡我嗎？</h2>
        <p class="text-lg text-gray-50">想要和我交流想法的話可以通過以下方式聯絡我</p>
      </div>
      <div class="max-w-3xl flex justify-center flex-col -mx-4 gap-6 lg:flex-row">
        <div class="w-full lg:w-1/2 px-4">
          <div class="py-8 bg-white text-center rounded-xl h-48">
            <h3 class="mb-4 text-lg font-semibold text-orange-500">電話聯絡</h3>
            <p class="text-gray-500">香港：63994728</p>
            <p class="text-gray-500">澳門：66173263</p>
            <p class="text-gray-500">國內：13798994881</p>
          </div>
        </div>
        <div class="w-full lg:w-1/2 px-4">
          <div class="py-8 bg-white text-center rounded-xl h-48">
            <h3 class="mb-4 text-lg font-semibold text-orange-500">電子郵箱及通訊軟件</h3>
            <div class="flex items-center justify-center gap-3">
              <div class="">
                <img src="../public/atis-assets/social/mail.png" class="w-8 h-8" />
              </div>
              <div class="text-gray-500">Email : anthony_loi@yahoo.com</div>
            </div>
            <div class="flex items-center justify-center gap-3">
              <div class="">
                <img src="../public/atis-assets/social/wechat.png" class="w-8 h-8" />
              </div>
              <div class="text-gray-500">Wechat : 66173263</div>
            </div>
            <div class="flex items-center justify-center gap-3">
              <div class="">
                <img src="../public/atis-assets/social/whatsapp.png" class="w-8 h-8" />
              </div>
              <div class="text-gray-500">Whatsapp : 66173263</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup></script>

<style>
.nav-immersive {
  @apply fixed;
}

.nav-immersive #nav:not(.nav-shrink) {
  @apply bg-transparent;
}
</style>

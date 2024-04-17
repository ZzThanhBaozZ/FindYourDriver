<template>
  <div class="pb-[40vh]">
    <div
      class="mb-[100px] flex items-center justify-between px-[5rem] py-[2vh]"
    >
      <div>
        <NuxtImg src="/Superspeed.svg" class="logo" />
      </div>
      <!-- <nav>
        <ul class="flex gap-[20px]">
          <li>link 1</li>
          <li>link 2</li>
          <li>link 3</li>
          <li>link 3</li>
        </ul>
      </nav> -->
      <section class="flex">
        <NuxtLink to="/login">
          <UButton size="xl" :ui="{ rounded: 'rounded-full' }"
            >Đăng Nhập</UButton
          >
        </NuxtLink>
      </section>
    </div>
    <section class="px-[5vw]">
      <h2>
        Nhóm 9: Chào mừng bạn đến với
        <span class="gradient-text">SuperSpeed</span>
      </h2>
      <h3>Phát triển phần mềm hướng dịch vụ với đề tài</h3>
      <h1 class="my-20 text-center">
        Xây dựng ứng dụng đặt xe online bằng RESTful API <br />
        <Icon
          name="formkit:arrowdown"
          color="black"
          class="my-10 h-20 w-20 animate-bounce"
        />
      </h1>
    </section>
    <section class="p-[5vw]">
      <h2 class="leading-[3vw]">
        <span class="gradient-text">RESTful API</span>
      </h2>
      <div>
        <h3>
          <span
            ><Icon
              name="material-symbols-light:http-sharp"
              color="black"
              class="mr-2 h-10 w-10" /></span
          >Phương thức
        </h3>
        <div
          class="my-[2vw] flex justify-around rounded-lg border-4 bg-white py-[4vw]"
        >
          <h3>GET</h3>
          <h3>POST</h3>
          <h3>PUT</h3>
          <h3>DELETE</h3>
          <h3>HEAD</h3>
          <h3>CONNECT</h3>
          <h3>OPTIONS</h3>
          <h3>TRACE</h3>
          <h3>PATCH</h3>
        </div>
      </div>
    </section>
    <section class="p-[5vw]">
      <h2 class="leading-[3vw]"><span class="gradient-text">Frontend</span></h2>
      <div>
        <h3>
          <span
            ><Icon
              name="streamline:ai-technology-spark"
              color="black"
              class="mr-2 h-8 w-8" /></span
          >Công nghệ sử dụng
        </h3>
        <div
          class="my-[2vw] flex justify-around rounded-lg border-4 bg-white py-[4vw]"
        >
          <div class="flex w-1/2 justify-center">
            <a href="https://nuxt.com/">
              <NuxtImg src="/Nuxt3.svg" class="h-[80px]" />
            </a>
          </div>
          <div class="flex w-1/2 justify-center">
            <a href="https://tailwindcss.com/">
              <NuxtImg src="/Tailwind.svg" class="h-[80px]" />
            </a>
          </div>
        </div>
        <div>
          <h3>
            <span
              ><Icon
                name="clarity:host-line"
                color="black"
                class="mr-2 h-8 w-8" /></span
            >Triển khai dịch vụ lưu trữ
          </h3>
          <div
            class="my-[2vw] flex items-center justify-around rounded-lg border-4 bg-white py-[4vw]"
          >
            <div class="flex w-1/2 justify-center">
              <a href="https://www.hostinger.vn/">
                <NuxtImg src="/HostingerLogo.svg" class="h-[100px]" />
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="p-[5vw]">
      <h2 class="leading-[3vw]"><span class="gradient-text">Backend</span></h2>
      <div>
        <h3>
          <span
            ><Icon
              name="streamline:ai-technology-spark"
              color="black"
              class="mr-2 h-8 w-8" /></span
          >Công nghệ sử dụng
        </h3>
        <div
          class="my-[2vw] flex items-center justify-around rounded-lg border-4 bg-white py-[4vw]"
        >
          <div class="flex w-1/2 justify-center">
            <a href="https://expressjs.com/">
              <NuxtImg src="/Express.svg" class="h-[160px]" />
            </a>
          </div>
          <div class="flex w-1/2 justify-center">
            <a href="https://www.mongodb.com/">
              <NuxtImg src="/MongoDB.svg" class="h-[80px]" />
            </a>
          </div>
        </div>
      </div>
      <div>
        <h3>
          <span
            ><Icon
              name="clarity:host-line"
              color="black"
              class="mr-2 h-8 w-8" /></span
          >Triển khai dịch vụ lưu trữ
        </h3>
        <div
          class="my-[2vw] flex items-center justify-around rounded-lg border-4 bg-white py-[4vw]"
        >
          <div class="flex w-1/2 justify-center">
            <a href="https://railway.app/">
              <NuxtImg src="/Railway.svg" class="h-[160px]" />
            </a>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup></script>

<style>
.logo {
  width: 10vw;
  @apply p-4;
}

.gradient-text {
  display: inline-block;
  background: linear-gradient(to right, #000, #f00);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient-animation 2s ease-in-out infinite;
}

@keyframes gradient-animation {
  0% {
    background-position: 0%;
  }
  100% {
    background-position: 100%;
  }
}
</style>

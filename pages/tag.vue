<template>
  <div class="w-full min-h-screen dark-soul-blue text-white">
    <div
      class="md:grid grid-cols-2 gap-6 md:w-2/3 m-0 md:mx-auto"
      id="badge-cont"
    >
      <cld-image
        public-id="nuxtjs-confrence-tag-generator/template/blue-badge-bg-2.png"
        fetchFormat="auto"
        quality="auto"
        loading="lazy"
        width="433px"
        height="920px"
        class="text_black"
      >
        <cld-transformation
          :overlay="`${$route.query.then.replace('/', ':')}`"
          width="110"
          height="110"
          x="56"
          y="479"
          gravity="north_west"
        />
        <cld-transformation
          :overlay="`${$route.query.now.replace('/', ':')}`"
          width="150"
          height="150"
          x="63"
          y="404"
          gravity="north_east"
        />
        <cld-transformation
          :overlay="`text:Arial_36_bold_stroke_letter_spacing_2:${$route.query.name},co_rgb:FFFFFF,bo_5px_solid_black`"
          y="225"
          gravity="west"
          x="60"
        />
      </cld-image>
      <div class="pt-10">
        <img src="https://jamstackconf.com/badge/img/jamstack-conf-2021.svg" />
        <div class="text-center m-5">
          <span
            class="
              blue-sparkle
              font-bold
              text-shadow text-lg
              py-1
              px-2
              shadow
              inline-block
              transform
              -rotate-6
            "
            >how it started</span
          >
          <span
            class="
              blue-dacnis
              font-bold
              text-shadow text-lg
              py-1
              px-2
              shadow
              inline-block
              transform
              -rotate-3
            "
            >how it's going</span
          >
          <span
            class="
              pink-katydid
              font-bold
              text-shadow text-lg
              py-1
              px-2
              shadow
              inline-block
              transform
              rotate-6
            "
            >Oct 6-7</span
          >
        </div>
        <div class="pretentious-peacock-blue p-10 rounded-xl">
          <h1 class="text-4xl font-bold text-shadow text-center leading-12">
            {{ $route.query.name.split(" ")[0] }} will be lookin’ hella fly at
            Jamstack Conf this year!
          </h1>

          <div class="mt-10 text-center font-semibold leading-7">
            <p>Here's your tag. Feel free to share it with your friends!</p>
          </div>

          <div class="text-center">
            <button
              @click="download"
              class="
                laminate
                hover-pink-katydid
                text-black text-2xl
                shadow
                py-3
                px-6
                font-bold
                hover:text-white
                rounded-lg
                mx-auto
                my-10
              "
            >
              Download
            </button>
            <button
              @click="share"
              class="
                laminate
                hover-pink-katydid
                text-black text-2xl
                shadow
                py-3
                px-6
                font-bold
                hover:text-white
                rounded-lg
                mx-auto
              "
            >
              Show off your badge!
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    share() {
      const src = document.getElementById("badge-cont").children[0].src;

      const url = `https://twitter.com/intent/tweet?text=Got my badge ready for @jamstackconf 2021! See you there? ${src}`;

      window.open(url);
    },
    download() {
      const src = document.getElementById("badge-cont").children[0].src;

      window.open(src);
    },
  },
};
</script>

<style scoped>
#badge {
  width: 433px;
  height: 920px;
}
#badge #then {
  width: 112px;
  top: 479px;
  left: 56px;
  height: 112px;
  overflow: hidden;
}
#badge #now {
  width: 150px;
  top: 405px;
  left: 220px;
  height: 150px;
  overflow: hidden;
}
#badge #name {
  top: 650px;
  left: 50px;
  width: 350px;
  text-align: left;
}
.dark-soul-blue {
  background-color: rgb(17, 30, 81);
}
.blue-sparkle {
  background-color: #0077ff;
}
.blue-dacnis {
  background-color: #3fdff0;
}
.pink-katydid {
  background-color: #ff57a8;
}
.pretentious-peacock-blue {
  background-color: #4444ff;
}
.hover-blue-dacnis:hover {
  background-color: #3fdff0;
}
.hover-pink-katydid:hover {
  background: #ff57a8;
}
.shadow-mango {
  box-shadow: 5px 5px 0 #ffab2b;
}
.shadow-pink-katydid {
  box-shadow: 5px 5px 0 #ff57a8;
}
.text-shadow {
  text-shadow: -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,
    3px 3px 0 #000;
}
.shadow {
  box-shadow: 5px 5px 0 #000;
}
.laminate {
  background: linear-gradient(
    0deg,
    rgba(0, 255, 178, 1) 0%,
    rgba(136, 249, 237, 1) 100%
  );
}
</style>

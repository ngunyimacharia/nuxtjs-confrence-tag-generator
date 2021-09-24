<template>
  <div class="w-full min-h-screen dark-soul-blue text-white">
    <div class="md:grid grid-cols-2 gap-6 md:w-2/3 m-0 md:mx-auto">
      <div id="badge" class="relative">
        <img
          src="https://jamstackconf.com/badge/img/blue-badge-bg-2.png"
          class="absolute w-full"
        />
        <div id="then" class="absolute">
          <img v-if="then.url" :src="then.url" />
        </div>
        <div id="now" class="absolute">
          <img v-if="now.url" :src="now.url" />
        </div>
        <h1
          id="name"
          class="text-4xl font-bold text-shadow text-center leading-12 absolute"
        >
          {{ name ? name : "An Excited Jamstacker" }}
        </h1>
      </div>
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
            Let's customize your<br />
            virtual badge!
          </h1>
          <div class="my-10 grid grid-cols-5 m-5">
            <span class="pt-4">Name:</span>
            <input
              type="text"
              class="
                text-black
                col-span-4
                h-14
                rounded
                border-2
                pl-2
                border-black
                shadow
              "
              placeholder="Enter your full name"
              v-model="name"
            />
          </div>

          <div class="my-10 grid grid-cols-2 text-center">
            <div>
              <input
                type="file"
                class="hidden"
                ref="thenInput"
                @change="setThen"
              />
              <label
                @click="$refs.thenInput.click()"
                class="
                  block
                  w-16
                  h-16
                  m-auto
                  bg-white
                  border-2 border-black
                  shadow-mango
                  p-1
                  hover-blue-dacnis
                  cursor-pointer
                "
              >
                <img
                  src="https://jamstackconf.com/badge/img/btn-image-upload.svg"
                />
              </label>
              <p class="m-3 uppercase">How it started</p>
            </div>
            <div>
              <input
                type="file"
                class="hidden"
                ref="nowInput"
                @change="setNow"
              />
              <label
                @click="$refs.nowInput.click()"
                class="
                  block
                  w-16
                  h-16
                  m-auto
                  bg-white
                  border-2 border-black
                  shadow-pink-katydid
                  p-1
                  hover-blue-dacnis
                  cursor-pointer
                "
              >
                <img
                  src="https://jamstackconf.com/badge/img/btn-image-upload.svg"
                />
              </label>
              <p class="m-3 uppercase">How it's going</p>
            </div>
          </div>

          <div class="text-center font-semibold leading-7">
            <p>We've all been through changes in our lives!</p>
            <p>We invite you to share who you are and who you were.</p>
            <p>Square-ish images work best (2MB max).</p>
          </div>

          <div class="text-center">
            <button
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
              @click="submit"
            >
              Laminate!
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
    return {
      name: null,
      then: {
        file: null,
        url: null,
        cloudinary: null,
      },
      now: {
        file: null,
        url: null,
        cloudinary: null,
      },
      uploading: false,
    };
  },
  methods: {
    setThen(e) {
      this.then.file = e.target.files[0];
      this.then.url = URL.createObjectURL(this.then.file);
    },
    setNow(e) {
      this.now.file = e.target.files[0];
      this.now.url = URL.createObjectURL(this.now.file);
    },
    async readData(f) {
      return new Promise((resolve) => {
        const reader = new FileReader();
        reader.onloadend = () => resolve(reader.result);
        reader.readAsDataURL(f);
      });
    },
    async submit() {
      this.uploading = true;

      const thenData = await this.readData(this.then.file);

      this.then.cloudinary = await this.$cloudinary.upload(thenData, {
        upload_preset: "default-preset",
        folder: "nuxtjs-audio-track-change",
      });

      const nowData = await this.readData(this.now.file);

      this.now.cloudinary = await this.$cloudinary.upload(nowData, {
        upload_preset: "default-preset",
        folder: "nuxtjs-audio-track-change",
      });

      console.log(this.then, this.now);

      this.uploading = false;
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

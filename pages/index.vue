<template>
  <div class="flex bg-gray-200">
    <div
      class="controls h-screen bg-gray-800 w-64 text-xs relative"
      :class="{ 'hide-controls': hideControls }"
    >
      <div class=" text-indigo-100 bg-gray-900 py-1 px-5 shadow-xs">
        Settings
      </div>
      <div class="p-5 border-b border-b border-gray-900 p-5 pb-8">
        <div class="mb-4">
          <div class="flex gap-4">
            <div class="relative rounded overflow-hidden">
              <label
                for="height"
                class="input-label border-r absolute bg-white text-gray-700 tracking-tighter"
                >HEIGHT</label
              >
              <input
                class="label-overlay image-url w-full bg-indigo-100 flex-1"
                type="number"
                id="height"
                name="height"
                v-model="height"
                placeholder="FULL"
              />
            </div>
            <input
              type="range"
              id="height"
              name="height"
              min="200"
              max="1200"
              v-model="height"
              class="w-24"
            />
          </div>
        </div>

        <div>
          <div class="flex gap-4">
            <div class="relative rounded overflow-hidden">
              <label
                for="width"
                class="input-label border-r absolute bg-white text-gray-700 tracking-tighter"
                >WIDTH</label
              >
              <input
                class="label-overlay image-url w-full bg-indigo-100 flex-1"
                type="number"
                id="width"
                name="width"
                v-model="width"
                placeholder="FULL"
              />
            </div>
            <input
              type="range"
              id="width"
              name="width"
              min="200"
              max="1200"
              v-model="width"
              class="w-24"
            />
          </div>
        </div>
      </div>
      <div class=" text-indigo-100 bg-gray-900 py-1 px-5 shadow-xs">
        Slides
      </div>
      <div class="py-2 border-b border-b border-gray-900">
        <ul class="">
          <li
            class="px-5 py-3 controls-slide"
            v-for="slide in slides"
            :key="slide.id"
          >
            <div class="relative rounded overflow-hidden mb-2">
              <label
                class="input-label border-r absolute bg-white text-gray-700 tracking-tighter"
                >TITLE</label
              >
              <input
                class="label-overlay w-full bg-indigo-100"
                type="text"
                v-model="slide.title"
              />
            </div>
            <div class="relative rounded overflow-hidden">
              <label
                :for="slide.id"
                class="input-label border-r absolute bg-white text-gray-700 tracking-tighter"
                >URL</label
              >
              <input
                :id="slide.id"
                class="label-overlay image-url w-full bg-indigo-100"
                type="text"
                v-model="slide.image"
              />
            </div>
          </li>
          <div class="p-5">
            <button
              class="w-full rounded p-1 bg-indigo-500 shadow"
              @click="addNewSlide"
            >
              Add new slide
            </button>
          </div>
        </ul>
      </div>
      <div
        class="toggle-controls flex justify-center items-center cursor-pointer"
        @click="hideControls = !hideControls"
      >
        <img src="@/assets/x.svg" alt="" srcset="" />
      </div>
    </div>
    <div class="preview bg-white z-20 flex-1 flex justify-center items-center">
      <div
        class="slider"
        :style="{
          maxHeight: height ? `${height}px` : '100%',
          maxWidth: width ? `${width}px` : '100%'
        }"
      >
        <div
          v-for="(slide, i) in slides"
          :key="slide.id"
          class="slide p-12 relative"
          :class="{ 'active-slide': activeSlide === i }"
          @click="toggleActive(i)"
        >
          <div
            class=" absolute top-0 bottom-0 right-0 left-0 w-full"
            :style="{ backgroundImage: `url(${slide.image})` }"
          ></div>
          <span class="slide-title text-white whitespace-no-wrap font-light">{{
            slide.title
          }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      height: null,
      width: null,
      activeSlide: null,
      hideControls: false,
      slides: [
        {
          image:
            "https://images.unsplash.com/photo-1572091363842-ab4cc34340a8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2800&q=80",
          id: "1",
          title: "The Coast of Kerry, Ireland"
        },
        {
          image:
            "https://images.unsplash.com/photo-1519412711294-ea7265523d5a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2767&q=80",
          id: "2",
          title: "Kilkenny Castle from the air."
        },
        {
          image:
            "https://images.unsplash.com/photo-1521298355169-e5c635852ebb?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1652&q=80",
          id: "23",
          title: "A Panda chilling"
        },
        {
          image:
            "https://images.unsplash.com/photo-1446776811953-b23d57bd21aa?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2852&q=80",
          id: "4",
          title: "Ocean clouds seen from space"
        }
      ]
    };
  },
  methods: {
    addNewSlide() {
      this.slides.push({
        image: "",
        id: `${this.slides.length + 1}`,
        title: ""
      });
    },
    toggleActive(i) {
      if (this.activeSlide === i) {
        this.activeSlide = null;
      } else {
        this.activeSlide = i;
      }
    }
  }
};
</script>

<style>
.controls {
  min-width: 320px;
  max-width: 1000px;
  transition: all 300ms ease;
}
.controls .input-label {
  padding: 4px;
  width: 64px;
  text-align: center;
  top: 0;
  height: 100%;
}
.controls input {
  padding: 4px;
}
.controls .label-overlay {
  padding-left: 72px;
}

.controls input[type="range"] {
  background: #1a212c;
  appearance: none;
  border-radius: 5px;
  height: 8px;
  margin-top: 10px;
}
.controls input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  height: 16px;
  width: 16px;
  border-radius: 100%;
  background: #ffffff;
  /* cursor: pointer; */
}
.controls-slide:nth-child(even) {
  background: #252c37;
}

.toggle-controls {
  width: 32px;
  height: 32px;
  position: absolute;
  bottom: 1rem;
  right: -32px;
  background: #2d3747;
  z-index: 9999;
}
.hide-controls {
  max-width: 0;
  min-width: unset;
  transition: all 300ms ease;
}
.hide-controls img {
  transform: rotate(45deg);
}

/* SLIDER  */
.slider {
  display: flex;
  height: 100%;
  width: 100%;
  /* padding: 40px; */
}
.slide {
  flex: 1;
  transition: all 300ms ease-in-out;
  cursor: zoom-in;
  min-width: 0;
  display: flex;
  align-items: flex-end;
}
.slide > div {
  filter: saturate(0.1) brightness(0.5);
  background-size: cover;
  background-position: center;
  background-color: #2d3748;
  transition: all 300ms ease-in-out;
}
.slide:hover {
  flex: 1.25;
}
.slide:hover > div {
  filter: none;
}

.active-slide {
  /* min-width: 90%; */
  flex-grow: 100;
  cursor: zoom-out;
}
.active-slide:hover {
  flex-grow: 100;
}
.slide-title {
  transition: all 200ms ease-in-out 100ms;
  transform: rotate(-90deg) translateY(50%);
  display: inline-block;
  transform-origin: bottom left;
  z-index: 10;
  font-size: 1.25rem;
}
.active-slide .slide-title {
  transform: none;
  font-size: 1.75rem;
}
</style>

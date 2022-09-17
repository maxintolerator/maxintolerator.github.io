<template>
  <q-page
    class="flex flex-center"
    :style="'background-color: ' + backgroundColor"
  >
    <q-header
      class="q-pa-md no-shadow no-border no-outline no-box-shadow no-print"
      :style="'background-color: ' + backgroundColor"
    >
      <div class="row justify-between q-gutter-x-md transparent">
        <div class="text-black q-mt-sm transparent"></div>

        <div>
          <a href="mailto:max@intolerator.com"
            ><q-btn
              flat
              label="Email"
              no-caps
              :style="'color: ' + invertedBackgroundColor"
            >
            </q-btn
          ></a>
          <q-btn
            :style="'color: ' + invertedBackgroundColor"
            flat
            @click="github"
            label="GitHub"
            :class="$q.screen.width > 450 ? 'q-ml-md' : ''"
            no-caps
          />
          <q-btn
            :style="'color: ' + invertedBackgroundColor"
            flat
            @click="linkedin"
            label="LinkedIn"
            :class="$q.screen.width > 450 ? 'q-ml-md' : ''"
            no-caps
          />
          <q-btn
            flat
            :style="'color: ' + invertedBackgroundColor"
            @click="facebook"
            label="Facebook"
            :class="$q.screen.width > 450 ? 'q-ml-md' : ''"
            no-caps
          />
        </div>
      </div>
    </q-header>
    <div class="row justify-center items-center q-gutter-x-lg">
      <q-img
        style="width: 100px; height: 100px"
        src="https://avatars.githubusercontent.com/u/109185813?v=4"
      />
      <div :class="headlineClass" :style="'color: ' + invertedBackgroundColor">
        Hi, I'm Max.<br />I make apps that do stuff.
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { useQuasar } from "quasar";

export default defineComponent({
  name: "IndexPage",
  setup() {
    const quasar = useQuasar();
    return { quasar };
  },
  data() {
    return {
      positionX: 0,
      positionY: 0,
    };
  },
  computed: {
    headlineClass() {
      const { width } = this.quasar.screen;
      if (width < 768) {
        return "text-h5";
      }
      if (width < 992) {
        return "text-h4";
      }
      return "text-h2";
    },
    backgroundColor() {
      const { positionX, positionY } = this;
      const color = `hsl(${positionX + positionY}, ${Math.floor(
        Math.random() * 101
      )}%, ${Math.floor(Math.random() * 101)}%)`;
      return color;
    },
    invertedBackgroundColor() {
      const { backgroundColor } = this;
      const hue = parseInt(
        backgroundColor.substring(4, backgroundColor.length - 1)
      );
      const saturation = parseInt(
        backgroundColor.substring(
          backgroundColor.indexOf(",") + 1,
          backgroundColor.lastIndexOf(")")
        )
      );
      const lightness = parseInt(
        backgroundColor.substring(
          backgroundColor.lastIndexOf(",") + 1,
          backgroundColor.length - 1
        )
      );
      const color = `hsl(${360 - hue}, ${100 - saturation}%, ${
        100 - lightness
      }%)`;
      return color;
    },
  },
  mounted() {
    document.body.addEventListener("mousemove", (e) => {
      this.positionX = e.clientX;
      this.positionY = e.clientY;
    });
  },
  methods: {
    linkedin() {
      window.open("https://www.linkedin.com/in/max-weidemann/");
    },
    github() {
      window.open("https://github.com/maxintolerator");
    },
    facebook() {
      this.quasar
        .dialog({
          title: "Facebook, seriously?!",
          message:
            "Who the fuck has that. You might as well send me a telefax.",
        })
        .onOk(() => {
          // console.log('OK')
        })
        .onCancel(() => {
          // console.log('Cancel')
        })
        .onDismiss(() => {
          // console.log('I am triggered on both OK and Cancel')
        });
    },
  },
});
</script>

<template>
  <q-page
    class="flex flex-center"
    :style="'background-color: ' + backgroundColor"
  >
    <q-header
      class="q-pa-md transparent no-shadow no-border no-outline no-box-shadow no-print"
    >
      <div class="row justify-between q-gutter-x-md">
        <div class="text-black q-mt-sm" v-if="$q.screen.width > 950">
          I have no idea why this fucking header is white. CSS sucks man.
        </div>

        <div>
          <a href="mailto:max@intolerator.com"
            ><q-btn color="black" flat label="Email" class="q-ml-md" no-caps>
            </q-btn
          ></a>
          <q-btn
            color="black"
            flat
            @click="linkedin"
            label="LinkedIn"
            class="q-ml-md"
            no-caps
          />
          <q-btn
            flat
            color="black"
            @click="facebook"
            label="Facebook"
            class="q-ml-md"
            no-caps
          />
        </div>
      </div>
    </q-header>
    <div :class="headlineClass" :style="'color: ' + invertedBackgroundColor">
      Hi, I'm Max.<br />I make apps that do stuff.
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

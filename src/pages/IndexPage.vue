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
                    <q-btn
                        :style="'color: ' + invertedBackgroundColor"
                        flat
                        @click="upwork"
                        label="Hire me on Upwork"
                        :class="$q.screen.width > 450 ? 'q-ml-md' : ''"
                        no-caps
                    />
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
        <div class="vp-wrapper">
            <div class="vp-center">
                <div class="row justify-center items-center q-gutter-x-lg">
                    <q-img
                        style="width: 100px; height: 100px"
                        src="https://avatars.githubusercontent.com/u/109185813?v=4"
                    />
                    <div
                        :class="headlineClass"
                        :style="'color: ' + invertedBackgroundColor"
                    >
                        Hi, I'm Max.<br />I make apps that do stuff.
                    </div>
                </div>
                <div
                    class="row justify-center items-center q-gutter-lg q-mt-xl"
                >
                    <q-btn
                        size="20px"
                        outline
                        :style="'color: ' + invertedBackgroundColor"
                        no-caps
                        label="Get in touch"
                        @click="window.open('mailto:max@intolerator.com')"
                    />
                    <q-btn
                        size="20px"
                        outline
                        :style="'color: ' + invertedBackgroundColor"
                        no-caps
                        label="My Portfolio"
                        @click="scrollToBottom"
                    />
                </div>
            </div>
        </div>
        <div class="vp-wrapper">
            <div class="vp-center-2">
                <div class="row justify-center items-center q-gutter-x-lg">
                    <three-dim-card
                        v-for="card in cards"
                        :key="card.title"
                        :image="card.image"
                        :link="card.link"
                        :head="card.title"
                        :body="card.body"
                        :color="invertedBackgroundColor"
                        classes="transparent btn-style col-xs-12 col-sm-6 col-md-3 no-box-shadow card"
                        style="height: 600px"
                    />
                </div>
            </div>
        </div>
    </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import { useQuasar } from 'quasar'
import ThreeDimCard from '../components/ThreeDimCard.vue'

export default defineComponent({
    name: 'IndexPage',
    setup() {
        const quasar = useQuasar()
        return { quasar }
    },
    components: {
        ThreeDimCard
    },
    data() {
        return {
            positionX: 0,
            positionY: 0,
            cards: [
                {
                    title: 'millionways App',
                    image: 'images/mockup-webapp.png',
                    link: 'https://millionways.me',
                    body: 'I have built the millionways App using the Quasar Framework and Firebase. Using Cordova, I have also built the Android and iOS versions of the app. The app is a platform for people to self-reflect with the help of AI and to connect with others who are on a similar journey.'
                },
                {
                    title: 'millionways AI Chatbot',
                    image: 'images/mockup-chatbot.png',
                    link: 'https://millionways.ai',
                    body: 'I have built the millionways AI Chatbot using the Quasar Framework and Firebase. The chatbot is a virtual assistant that helps users to self-reflect and gives personalized answers using millionways and the OpenAI API.'
                },
                {
                    title: 'millionways API',
                    image: 'images/api.png',
                    link: 'https://api.millionways.org/docs',
                    body: 'I have built the millionways API using Node.js Express and MongoDB. The API is a RESTful API that provides access to the millionways core technology. It is used by B2B customers, the millionways App and the millionways AI Chatbot.'
                }
            ]
        }
    },
    computed: {
        headlineClass() {
            const { width } = this.quasar.screen
            if (width < 768) {
                return 'text-h5'
            }
            if (width < 992) {
                return 'text-h4'
            }
            return 'text-h2'
        },
        backgroundColor() {
            const { positionX, positionY } = this
            const color = `hsl(${positionX + positionY}, ${Math.floor(
                Math.random() * 101
            )}%, ${Math.floor(Math.random() * 101)}%)`
            return color
        },
        invertedBackgroundColor() {
            const { backgroundColor } = this
            const hue = parseInt(
                backgroundColor.substring(4, backgroundColor.length - 1)
            )
            const saturation = parseInt(
                backgroundColor.substring(
                    backgroundColor.indexOf(',') + 1,
                    backgroundColor.lastIndexOf(')')
                )
            )
            const lightness = parseInt(
                backgroundColor.substring(
                    backgroundColor.lastIndexOf(',') + 1,
                    backgroundColor.length - 1
                )
            )
            const color = `hsl(${360 - hue}, ${100 - saturation}%, ${
                100 - lightness
            }%)`
            return color
        }
    },
    mounted() {
        // set position x and y to a random number between 0 and 360
        this.positionX = Math.floor(Math.random() * 360)
        this.positionY = Math.floor(Math.random() * 360)
    },
    methods: {
        linkedin() {
            window.open('https://www.linkedin.com/in/max-weidemann/')
        },
        upwork() {
            window.open(
                'https://www.upwork.com/freelancers/~01568922fccea51b3d?mp_source=share'
            )
        },
        github() {
            window.open('https://github.com/maxintolerator')
        },
        facebook() {
            this.quasar
                .dialog({
                    title: 'Facebook, seriously?!',
                    message:
                        'Who the f*ck has that. You might as well send me a telefax.'
                })
                .onOk(() => {
                    // console.log('OK')
                })
                .onCancel(() => {
                    // console.log('Cancel')
                })
                .onDismiss(() => {
                    // console.log('I am triggered on both OK and Cancel')
                })
        },
        scrollToBottom() {
            //smooth scroll to bottom
            let scrollOptions = {
                top: this.$q.screen.height,
                behavior: 'smooth'
            }
            window.scrollTo(scrollOptions)
        }
    }
})
</script>

<style lang="scss">
.vp-center {
    margin: -74px 50px 0;
}
.vp-center-2 {
    margin: 0 30px 0;
}
.vp-wrapper {
    width: 100%;

    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>

<template>
    <q-page
        class="flex flex-center"
        :style="'background-color: ' + backgroundColor"
    >
        <div
            class="fixed-bottom-left q-pa-md cursor-pointer"
            v-if="isScrollArrowVisible"
        >
            <q-icon
                class="q-mr-md q-mb-md"
                name="keyboard_arrow_down"
                size="50px"
                @click="scrollToBottom"
                :style="'color: ' + invertedBackgroundColor"
            />
        </div>
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
                    <a href="mailto:max@intolerator.com"
                        ><q-btn
                            size="20px"
                            outline
                            label="Get in Touch"
                            no-caps
                            :style="'color: ' + invertedBackgroundColor"
                        >
                        </q-btn
                    ></a>
                    <q-btn
                        size="20px"
                        outline
                        :style="'color: ' + invertedBackgroundColor"
                        no-caps
                        label="My Portfolio"
                        @click="scrollToPortfolio"
                    />
                </div>
            </div>
        </div>
        <div class="vp-wrapper">
            <div class="vp-center-2" style="max-width: 1000px">
                <div
                    class="text-h3"
                    :style="'color: ' + invertedBackgroundColor"
                >
                    Bio
                </div>
                <div
                    class="text-subtitle1 q-mt-lg"
                    :style="'color: ' + invertedBackgroundColor"
                >
                    <p>
                        I am a self-taught full-stack software engineer
                        passionate about solving complex problems, making them
                        easy to understand, and helping others learn. I started
                        by teaching advanced Mathematics and Theoretical Physics
                        at German universities and worked on building e-learning
                        platforms early on.
                    </p>
                    <p>
                        After graduating, I teamed up with my half-brother
                        Martin to co-found millionways. I quickly learned the
                        skills needed to create fully fleshed-out product demos,
                        including the millionways mobile and web apps and the
                        API, and set up the technical side of the business.
                    </p>
                    <p>
                        I hold a Master's degree in Mathematics from the
                        University of Frankfurt am Main, Germany, and multiple
                        Certificates in Neural Networks and Deep Learning.
                    </p>
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
            currentScroll: 0,
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
        isScrollArrowVisible() {
            return this.currentScroll < this.$q.screen.height + 100
        },
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
            const hue = Math.floor(Math.random() * 360)
            const saturation = Math.floor(Math.random() * 61) + 20
            const lightness = Math.floor(Math.random() * 41) + 10
            const color = `hsl(${hue}, ${saturation}%, ${lightness}%)`
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
            // Ensure that inverted lightness doesn't exceed 100 or go below 0
            const invertedLightness = Math.max(
                0,
                Math.min(100, 100 - lightness)
            )
            const color = `hsl(${360 - hue}, ${
                100 - saturation
            }%, ${invertedLightness}%)`
            return color
        }
    },
    mounted() {
        // listen to scroll position and update currentScroll
        window.addEventListener('scroll', () => {
            this.currentScroll = window.scrollY
        })
    },
    methods: {
        linkedin() {
            window.open('https://www.linkedin.com/in/max-weidemann/')
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
            let scrollPosition = this.currentScroll
            if (scrollPosition < this.$q.screen.height) {
                scrollPosition = this.$q.screen.height
            } else {
                scrollPosition = this.$q.screen.height * 2
            }
            let scrollOptions = {
                top: scrollPosition,
                behavior: 'smooth'
            }
            window.scrollTo(scrollOptions)
        },
        scrollToPortfolio() {
            let scrollOptions = {
                top: 2 * this.$q.screen.height,
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

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
                    <q-btn
                        flat
                        label="Music Blog"
                        no-caps
                        :style="'color: ' + invertedBackgroundColor"
                        @click="$router.push('/music-blog')"
                    />
                    <a href="mailto:max@intolerator.com"
                        ><q-btn
                            flat
                            label="Email"
                            no-caps
                            :style="'color: ' + invertedBackgroundColor"
                            :class="$q.screen.width > 450 ? 'q-ml-md' : ''"
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
            <div class="vp-center-2" style="max-width: 1000px; width: 100%">
                <div
                    class="text-h3 q-mb-lg"
                    :style="'color: ' + invertedBackgroundColor"
                >
                    Portfolio
                </div>
                <div class="row justify-center items-stretch">
                    <portfolio-card
                        v-for="card in cards"
                        :key="card.title"
                        :kicker="card.kicker"
                        :title="card.title"
                        :body="card.body"
                        :link="card.link"
                        :link-label="card.linkLabel"
                        :color="invertedBackgroundColor"
                    />
                </div>
            </div>
        </div>
    </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import { useQuasar } from 'quasar'
import PortfolioCard from '../components/PortfolioCard.vue'

export default defineComponent({
    name: 'IndexPage',
    setup() {
        const quasar = useQuasar()
        return { quasar }
    },
    components: {
        PortfolioCard
    },
    data() {
        return {
            currentScroll: 0,
            cards: [
                {
                    kicker: 'Co-founder & CTO',
                    title: 'millionways',
                    body: 'The frontier lab for behavioral intelligence. I co-founded millionways and lead its technology: the models, the API and the apps built on them.',
                    link: 'https://millionways.ai',
                    linkLabel: 'millionways.ai'
                },
                {
                    kicker: 'Side project',
                    title: 'Quiztape',
                    body: 'Side A: stats. Side B: trivia. A music quiz cut from your own Last.fm listening history, with band facts sourced from MusicBrainz. One codebase for web, iOS and Android.',
                    link: 'https://quiztape.com',
                    linkLabel: 'quiztape.com'
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
            // Very dark background: random hue, moderate saturation, very low lightness
            const hue = Math.floor(Math.random() * 360)
            const saturation = Math.floor(Math.random() * 50) + 30 // 30-80% saturation for colorful but dark
            const lightness = Math.floor(Math.random() * 10) + 5 // 5-15% lightness for very dark
            const color = `hsl(${hue}, ${saturation}%, ${lightness}%)`
            return color
        },
        invertedBackgroundColor() {
            // Super readable light text: high lightness, low saturation for good contrast
            // We'll use a light color that contrasts well with dark backgrounds
            const lightness = Math.floor(Math.random() * 10) + 90 // 90-100% lightness for very light text
            const saturation = Math.floor(Math.random() * 15) + 5 // 5-20% saturation for subtle color
            const hue = Math.floor(Math.random() * 360) // Random hue for variety
            const color = `hsl(${hue}, ${saturation}%, ${lightness}%)`
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

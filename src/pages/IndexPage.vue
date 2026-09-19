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
                    <q-btn
                        v-if="kofiUrl"
                        flat
                        label="Ko-fi"
                        no-caps
                        :style="'color: ' + invertedBackgroundColor"
                        :class="$q.screen.width > 450 ? 'q-ml-md' : ''"
                        @click="kofi"
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
                        Co-Founder &amp; CTO of millionways, where we built
                        something that doesn't exist anywhere else: the first
                        Large Psychology Model.
                    </p>
                    <p>
                        While generative AI predicts what comes next, our
                        model, Thorsten 4, analyzes the behavioral patterns
                        that shape how decisions are actually formed. Built
                        from the ground up on longitudinal research with 50+
                        psychologists, 100,000+ hours of research hours, and
                        millions of labeled behavioral data points, Thorsten
                        surfaces decision-relevant signals that traditional AI
                        fundamentally cannot. Behavioral intelligence is the
                        missing AI layer we have built.
                    </p>
                    <p>
                        I am a self-taught full-stack engineer/entrepreneur
                        who started in advanced Mathematics and Theoretical
                        Physics at German universities before co-founding
                        millionways in New York with my half-brother Martin. I
                        am most passionate about product and engineering
                        end-to-end: from ML model development and API
                        architecture to cloud infrastructure, frontend UIs,
                        websites, business automations, and marketing
                        materials.
                    </p>
                    <p>
                        My background spans the full stack of building a
                        company: product architecture, AI/ML (PyTorch, BERT,
                        TensorFlow), cloud infrastructure (AWS, GCP, Digital
                        Ocean), frontend and backend engineering (Vue.js,
                        Next.js, Node.js, Flask, Firebase), DevOps, and
                        Business Development.
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

/** Ko-fi page name (the part after ko-fi.com/). Empty hides the widget and the header link. */
const KOFI_USERNAME = 'intolerator'

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
            kofiUsername: KOFI_USERNAME,
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
        kofiUrl() {
            return this.kofiUsername ? `https://ko-fi.com/${this.kofiUsername}` : null
        },
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
        this.mountKofiWidget()
    },
    methods: {
        kofi() {
            window.open(this.kofiUrl)
        },
        /** Ko-fi's floating button widget; loaded once, only when a page name is set. */
        mountKofiWidget() {
            if (!this.kofiUsername || document.getElementById('kofi-widget-script')) return
            const script = document.createElement('script')
            script.id = 'kofi-widget-script'
            script.src = 'https://storage.ko-fi.com/cdn/scripts/overlay-widget.js'
            script.async = true
            script.onload = () => {
                if (!window.kofiWidgetOverlay) return
                window.kofiWidgetOverlay.draw(this.kofiUsername, {
                    type: 'floating-chat',
                    // The widget's only position option is a raw style string; anchor it bottom-right.
                    'floating-chat.core.position.bottom-left':
                        'position: fixed; bottom: 24px; right: 16px; width: 160px; height: 65px;',
                    'floating-chat.donateButton.text': 'Support me',
                    'floating-chat.donateButton.background-color': '#ffffff',
                    'floating-chat.donateButton.text-color': '#0b0b10'
                })
            }
            document.body.appendChild(script)
        },
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

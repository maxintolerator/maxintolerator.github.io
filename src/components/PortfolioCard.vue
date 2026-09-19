<template>
    <a
        :href="link"
        target="_blank"
        rel="noopener"
        class="portfolio-card col-xs-12 col-sm-6 col-md-5"
        :style="'color: ' + color + '; border-color: ' + color"
    >
        <div class="text-overline portfolio-card__kicker">{{ kicker }}</div>
        <div class="text-h4 portfolio-card__title">{{ title }}</div>
        <div class="text-subtitle1 q-mt-md portfolio-card__body">{{ body }}</div>
        <div class="text-subtitle2 q-mt-lg portfolio-card__link">{{ linkLabel }} →</div>
    </a>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'PortfolioCard',
    props: {
        kicker: { type: String, default: '' },
        title: { type: String, required: true },
        body: { type: String, required: true },
        link: { type: String, required: true },
        linkLabel: { type: String, default: 'Visit' },
        color: { type: String, default: '#fff' }
    }
})
</script>

<style lang="scss">
.portfolio-card {
    display: block;
    text-decoration: none;
    border: 1px solid;
    border-radius: 16px;
    padding: 32px;
    margin: 12px;
    min-height: 260px;
    transition: transform 160ms ease, background-color 160ms ease;
    background-color: rgba(255, 255, 255, 0.03);

    &:hover,
    &:focus-visible {
        transform: translateY(-4px);
        background-color: rgba(255, 255, 255, 0.07);
        outline: none;
    }

    &__kicker {
        opacity: 0.7;
        letter-spacing: 0.2em;
    }

    &__title {
        line-height: 1.15;
    }

    &__body {
        opacity: 0.85;
        line-height: 1.5;
    }

    &__link {
        opacity: 0.8;
    }
}
</style>

<script setup lang="ts">
import { useChangeCase } from '@vueuse/integrations/useChangeCase'

const linksList = ['home', 'solutions', 'pages', 'elements', 'blog', 'contacts']

interface TLink {
  name: string
  link: string
}

const generatedLinksList: TLink[] = linksList.map((word) => ({
  name: useChangeCase(word, 'capitalCase').value,
  link: `/${useChangeCase(word, 'paramCase').value}`,
}))
</script>

<template>
  <TemplateHeader>
    <template #theme-switcher>
      <AtomToggleDarkMode></AtomToggleDarkMode>
    </template>

    <template #logo>
      <span class="icon"></span>
    </template>

    <template #links>
      <AtomHeaderLink v-for="linkItem in generatedLinksList" :key="linkItem.link" :link="linkItem.link">{{
        linkItem.name
      }}</AtomHeaderLink>
    </template>

    <template #demo>
      <AtomButton class="demo-button">
        Watch the demo
        <span class="text-2xl" i-fluent-play-circle-24-regular></span>
      </AtomButton>
    </template>
  </TemplateHeader>
</template>

<style lang="scss" scoped>
/**
  * Literally there is no another way in the universe how to change this svg color
*/
.icon {
  @apply inline-block bg-primary;
  @apply dark:(bg-white);
  width: 150px;
  height: 49px;
  mask-image: url('../../../../assets/images/svg-icons/logo_blue.svg');
  -webkit-mask-image: url('../../../../assets/images/svg-icons/logo_blue.svg');
  mask-repeat: no-repeat;
  -webkit-mask-repeat: no-repeat;
}
.demo-button {
  @apply bg-primary text-white;
  @apply hover:(bg-primary/80);
  @apply dark:(bg-white text-black);
  @apply dark:hover:(hover:bg-black hover:text-white);
}
</style>

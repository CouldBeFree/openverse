<template>
  <div class="relative max-w-[280px]" data-testid="source-list-popover">
    <VIconButton
      class="absolute top-0 border-none text-dark-charcoal-70 end-0"
      :icon-props="{ iconPath: icons.closeSmall }"
      :label="$t('modal.close')"
      @click="$emit('close')"
    />
    <h2 class="description-bold mb-2 px-4 pt-5 text-start">
      {{ $t("external-sources.title") }}
    </h2>
    <p class="caption-regular mb-4 px-4 text-start">
      {{ $t("external-sources.caption", { openverse: "Openverse" }) }}
    </p>
    <VButton
      v-for="source in externalSources"
      :key="source.name"
      as="VLink"
      variant="plain"
      size="disabled"
      class="caption-bold w-full justify-between px-4 py-3 text-dark-charcoal hover:bg-dark-charcoal-10"
      :href="source.url"
    >
      {{ source.name }}
      <VIcon
        :icon-path="icons.externalLink"
        :size="4"
        :rtl-flip="true"
        class="ms-2"
      />
    </VButton>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue"

import type { ExternalSource } from "~/types/external-source"

import VButton from "~/components/VButton.vue"
import VIcon from "~/components/VIcon/VIcon.vue"
import VIconButton from "~/components/VIconButton/VIconButton.vue"

import externalLinkIcon from "~/assets/icons/external-link.svg"
import caretDownIcon from "~/assets/icons/caret-down.svg"
import closeSmallIcon from "~/assets/icons/close-small.svg"

/**
 * This component renders a list of pre-populated links to additional sources
 * when there are insufficient or zero search results.
 */
export default defineComponent({
  name: "VExternalSourceList",
  components: { VButton, VIcon, VIconButton },
  props: {
    /**
     * the media type to use as the criteria for filtering additional sources
     */
    externalSources: {
      type: Array as PropType<ExternalSource[]>,
      required: true,
    },
  },
  setup() {
    return {
      icons: {
        externalLink: externalLinkIcon,
        caretDown: caretDownIcon,
        closeSmall: closeSmallIcon,
      },
    }
  },
})
</script>

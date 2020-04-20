<template>
  <div>
    <v-card
      v-if="showBrand"
      :to="{ name: 'index' }"
      tile
      flat
    >
      <v-card-title class="pl-1 pt-5 pb-5 justify-center">
        <img
          :alt="brand"
          :src="logo"
          class="px-3 logo"
        />
      </v-card-title>
      <v-card-subtitle class="pl-2 text-center">
        {{ $t('subtitle') }}
      </v-card-subtitle>
    </v-card>

    <governement-alert />
    <v-divider v-if="showBrand"></v-divider>
    <slot />
    <v-list>
      <v-divider></v-divider>
      <sidebar-list-item
        :title="$t('missing_shop')"
        :href="links.shopMissing"
        icon="plus"
      />
      <learn-more />
      <v-divider></v-divider>
      <change-language />
    </v-list>
    <v-btn @click="toggleColorBlind">Color blind</v-btn>
  </div>
</template>

<script>
import colors from 'vuetify/lib/util/colors'

import SidebarListItem from './sidebar_list_item';
import ChangeLanguage from './change_language';
import LearnMore from './learn_more';
import GovernementAlert from './governement_alert';
import i18nMixin from './mixins/i18n';

export default {
  components: {
    ChangeLanguage,
    GovernementAlert,
    LearnMore,
    SidebarListItem,
  },

  mixins: [i18nMixin],

  data() {
    return {
      colorblind: false
    };
  },

  props: {
    showBrand: {
      type: Boolean,
      required: false,
      default: true
    }
  },

  methods: {
    toggleColorBlind() {
      if (this.colorBlind) {
        this.$vuetify.theme.themes.light.success = '#4CAF50';
        this.$vuetify.theme.themes.light.error = '#FF5252';
        this.$vuetify.theme.themes.light.secondary = '#424242';
      } else {
        this.$vuetify.theme.themes.light.success = '#0C7BDC';
        this.$vuetify.theme.themes.light.error = '#FFC20A';
        this.$vuetify.theme.themes.light.secondary = colors.grey.base;
      }
      this.colorBlind = !this.colorBlind;
    }
  }
}
</script>

<style scoped>
.logo {
  max-width: 100%;
}
</style>

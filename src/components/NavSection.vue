<template>
  <nav :aria-label="$t('header.aria.primary')" class="navbar">
    <div class="navbar-brand has-color-white">
      <NuxtLink class="logo" to="/">
        <IconSearchLogo />
      </NuxtLink>

      <a
        role="button"
        :class="{ ['navbar-burger']: true, ['is-active']: isBurgerMenuActive }"
        :aria-label="$t('header.aria.menu')"
        aria-expanded="false"
        @click="toggleBurgerActive"
        @keyup.enter="toggleBurgerActive"
      >
        <span aria-hidden="true" />
        <span aria-hidden="true" />
        <span aria-hidden="true" />
      </a>
    </div>
    <div :class="{ ['navbar-menu']: true, ['is-active']: isBurgerMenuActive }">
      <div v-if="showNavSearch" class="margin-left-big">
        <form
          class="hero_search-form"
          role="search"
          method="post"
          @submit.prevent="onSubmit"
        >
          <input
            v-model.lazy="form.searchTerm"
            :aria-label="$t('header.aria.search')"
            class="input"
            type="search"
            :placeholder="navSearchPlaceholder"
          />
          <div class="is-sr-only">
            <button
              :aria-label="$t('header.aria.sr-search')"
              tabindex="-1"
              type="submit"
              class="button secondary"
              value="Search"
            />
          </div>
        </form>
      </div>
      <div class="navbar-end">
        <div class="navbar-item has-dropdown is-hoverable">
          <a class="navbar-link is-arrowless">
            {{ $t('header.about-tab') }}
            <i class="icon caret-down" />
          </a>
          <div class="navbar-dropdown">
            <NuxtLink class="navbar-item" to="/about">
              {{ $t('header.about') }}
            </NuxtLink>
            <NuxtLink class="navbar-item" to="/sources">
              {{ $t('header.source') }}
            </NuxtLink>
            <a
              href="https://creativecommons.org/about/cclicenses/"
              target="_blank"
              rel="noopener"
              class="navbar-item"
              >{{ $t('header.licenses') }}
              <i class="icon external-link" />
            </a>
          </div>
        </div>

        <div class="navbar-item has-dropdown is-hoverable">
          <a class="navbar-link is-arrowless">
            {{ $t('header.resources-tab') }}
            <i class="icon caret-down" />
          </a>
          <div class="navbar-dropdown">
            <NuxtLink class="navbar-item" to="/search-help">
              {{ $t('header.search-guide') }}
            </NuxtLink>
            <NuxtLink class="navbar-item" to="/meta-search">
              {{ $t('header.meta-search') }}
            </NuxtLink>
            <NuxtLink class="navbar-item" to="/feedback">
              {{ $t('header.feedback') }}
            </NuxtLink>
            <a
              href="https://api.creativecommons.engineering/"
              target="_blank"
              rel="noopener"
              class="navbar-item"
              >{{ $t('header.api') }}
              <i class="icon external-link" />
            </a>
          </div>
        </div>
        <NuxtLink class="navbar-item" to="/support">
          {{ $t('header.support') }}
        </NuxtLink>

        <a
          :aria-label="$t('header.aria.extension')"
          class="navbar-item"
          href="https://opensource.creativecommons.org/ccsearch-browser-extension/"
          target="_blank"
        >
          {{ $t('header.extension') }}
          <i class="icon external-link" />
        </a>
      </div>
    </div>
  </nav>
</template>

<script>
import IconSearchLogo from '@creativecommons/vocabulary/assets/logos/products/search.svg?inline'
import { SET_QUERY } from '~/store-modules/mutation-types'

export default {
  name: 'NavSection',
  components: { IconSearchLogo },
  props: {
    showNavSearch: {
      default: false,
    },
  },
  data: () => ({ form: { searchTerm: '' }, isBurgerMenuActive: false }),
  computed: {
    navSearchPlaceholder() {
      return this.$t('header.placeholder')
    },
  },
  methods: {
    onSubmit() {
      this.$store.commit(SET_QUERY, { query: { q: this.form.searchTerm } })
      this.$router.push({
        path: '/search',
        query: { q: this.form.searchTerm },
      })
    },
    toggleBurgerActive() {
      this.isBurgerMenuActive = !this.isBurgerMenuActive
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
/* header */
.logo {
  color: black;

  svg {
    height: 100%;
    width: auto;
  }
}

.hero_search-form {
  margin: 0 15px;

  input {
    width: 16rem;
  }
}
</style>

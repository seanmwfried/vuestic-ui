<template>
  <span class="va-breadcrumb-item">
    <router-link
      v-if="!isDisabled"
      class="va-breadcrumb-item__label va-breadcrumb-item__label--link"
      :to="to"
      :replace="replace"
      :append="append"
      :exact="exact"
      :href="hrefComputed"
      :active-class="activeClass"
      :exact-active-class="exactActiveClass"
      tag="a"
    >
      <slot>{{ label }}</slot>
    </router-link>
    <span
      v-else
      class="va-breadcrumb-item__label"
    >
      <slot>{{ label }}</slot>
    </span>
  </span>
</template>

<script lang="ts">
import { RouterLinkMixin } from '../../../mixins/RouterLinkMixin/RouterLinkMixin'
import { Options, mixins, prop, Vue } from 'vue-class-component'

class BreadcrumbsItemProps {
  disabled = prop<boolean>({
    type: Boolean,
    default: false,
  })

  label = prop<string>({
    type: String,
    default: '',
  })
}

const BreadcrumbsItemPropsMixin = Vue.with(BreadcrumbsItemProps)

@Options({
  name: 'VaBreadcrumbsItem',
})
export default class VaBreadcrumbsItem extends mixins(RouterLinkMixin, BreadcrumbsItemPropsMixin) {
  get isDisabled () {
    return this.disabled || !this.hasRouterLinkParams
  }
}
</script>

<style lang="scss">
.va-breadcrumb-item {
  display: var(--va-breadcrumb-item-display);
  color: var(--va-breadcrumb-item-color);

  &__label {
    color: inherit;

    &--link {
      cursor: pointer;

      &:hover {
        opacity: var(--va-breadcrumb-item-hover-opacity);
      }

      &:focus {
        text-decoration: var(--va-breadcrumb-item-focus-text-decoration);
      }
    }
  }
}
</style>

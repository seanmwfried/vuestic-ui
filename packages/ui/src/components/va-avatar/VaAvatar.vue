<template>
  <div
    class="va-avatar"
    ref="avatar"
    :style="computedStyle"
  >
    <slot>
      <va-progress-circle
        v-if="loading"
        indeterminate
        :size="sizeComputed"
        :color="colorComputed"
      />
      <img
        v-else-if="src"
        :src="src"
      >
      <va-icon
        v-else-if="icon"
        :name="icon"
      />
    </slot>
  </div>
</template>

<script lang="ts">
import { Options, mixins, prop, Vue } from 'vue-class-component'

import ColorMixin from '../../services/color-config/ColorMixin'
import { SizeMixin } from '../../mixins/SizeMixin'
import { LoadingMixin } from '../../mixins/LoadingMixin/LoadingMixin'
import VaIcon from '../va-icon'
import { VaProgressCircle } from '../va-progress-bar'

class AvatarProps {
  color = prop<string>({ type: String, default: 'info' })
  textColor = prop<string>({ type: String, default: 'white' })
  square = prop<boolean>({ type: Boolean, default: false })
  icon = prop<string>({ type: String, default: '' })
  src = prop<string>({ type: String, default: null })
  fontSize = prop<string>({ type: String, default: '' })
}

const AvatarPropsMixin = Vue.with(AvatarProps)

@Options({
  name: 'VaAvatar',
  components: { VaIcon, VaProgressCircle },
})
export default class VaAvatar extends mixins(
  SizeMixin,
  ColorMixin,
  LoadingMixin,
  AvatarPropsMixin,
) {
  get computedStyle () {
    return {
      color: this.theme.getColor(this.textColor, '#ffffff'),
      backgroundColor: this.loading ? 'transparent' : this.colorComputed,
      borderRadius: this.square ? 0 : '',
      fontSize: this.fontSize || this.fontSizeComputed,
      width: this.sizeComputed,
      minWidth: this.sizeComputed, // We only define width because common use case would be flex row, for column we expect user to set appropriate styling externally.
      height: this.sizeComputed,
    }
  }
}
</script>

<style lang="scss">
@import "variables";

.va-avatar {
  align-items: var(--va-avatar-align-items);
  display: var(--va-avatar-display);
  justify-content: var(--va-avatar-justify-content);
  line-height: var(--va-avatar-line-height);
  position: var(--va-avatar-position);
  text-align: var(--va-avatar-text-align);
  vertical-align: var(--va-avatar-vertical-align);
  border-radius: var(--va-avatar-border-radius);

  img,
  svg {
    border-radius: inherit;
    display: inline-flex;
    height: inherit;
    width: inherit;
    margin: auto;
  }
}
</style>

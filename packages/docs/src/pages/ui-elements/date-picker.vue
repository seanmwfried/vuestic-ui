<template>
  <docs-content :config="configComputed" />
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import DocsContent from '../../components/DocsContent.vue'
import datePickerConfig from '../../components/page-configs/ui-elements/va-date-picker/page-config'

@Options({
  name: 'DocsDatePicker',
  components: {
    DocsContent,
  },
})
export default class DatePicker extends Vue {
  get configComputed () {
    return datePickerConfig
  }
}
</script>

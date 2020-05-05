<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <input @input="updateValue" v-bind="$attrs" v-on="listeners" />
  </div>
</template>

<script>
import { formFieldMixin } from '@/mixins/formFieldMixin.js'

export default {
  mixins: [formFieldMixin],
  props: {
    value: [String, Number]
  },
  computed: {
    listeners() {
      return {
        ...this.$listeners,
        input: this.updateValue
      }
    }
  }
}
</script>

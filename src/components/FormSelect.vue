<template>
  <div class="form-select">
    <label>
      {{ label }}
      <select
        :multiple="multiple"
        :value="value"
        @change="$emit('input', selected)"
        v-model="selected"
        :required="required"
        class="form-select__select"
      >
        <option disabled value="Выберете вариант(ы)"
          >Выберете вариант(ы)</option
        >
        <option
          v-for="option in initialValue"
          :key="option.id"
          :value="option.value"
          >{{ option.text }}</option
        >
      </select>
    </label>
    <span class="form-select__error">{{ errorText }}</span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      selected: this.value,
    };
  },
  props: {
    value: [Array, String],
    label: String,
    error: String,
    required: Boolean,
    touched: Boolean,
    errorText: String,
    initialValue: Array,
    multiple: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss" scoped>
.form-select {
  padding-bottom: 2px;
  margin-top: 8px;
  display: flex;
  flex-direction: column;

  &__select {
    margin-top: 4px;
  }

  &__error {
    color: red;
    font-size: 12px;
  }
}</style
>>

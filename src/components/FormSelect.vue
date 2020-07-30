<template>
  <div>
    <label>
      {{ label }}
      <select
        :multiple="multiple"
        :value="value"
        @change="$emit('input', selected)"
        v-model="selected"
        :required="required"
      >
        <option disabled value="Выберете вариант(ы)">Выберете вариант(ы)</option>
        <option
          v-for="option in initialValue"
          :key="option.id"
          :value="option.value"
        >{{ option.text }}</option>
      </select>
    </label>
    <span>{{ errorText }}</span>
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
    placeholder: {
      type: String,
      default: "",
    },
    initialValue: Array,
    multiple: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
div {
  padding-bottom: 2px;
  margin-top: 8px;
  display: flex;
  flex-direction: column;
}
label {
  padding-bottom: 2px;
  margin-top: 8px;
}
span {
  color: red;
  font-size: 12px;
}
</style>>
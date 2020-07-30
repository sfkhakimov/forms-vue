<template>
  <div>
    <label>
      {{ label }}
      <input
        v-if="(type === 'text' || type === 'date')"
        :type="type"
        :placeholder="placeholder"
        :value="value"
        :required="required"
        @input="$emit('input', $event.target.value)"
        :name="name"
      />
      <input
        v-if="type === 'checkbox'"
        :type="type"
        :placeholder="placeholder"
        :checked="value"
        :required="required"
        @change="$emit('input', $event.target.checked)"
        :name="name"
      />
    </label>
    <span>{{ errorText }}</span>
  </div>
</template>
<script>
export default {
  props: {
    value: [String, Boolean],
    label: String,
    required: Boolean,
    touched: Boolean,
    errorText: String,
    initialValue: Array,
    name: {
      type: String,
      default: "text",
    },
    type: {
      type: String,
      default: "text",
    },
    placeholder: {
      type: String,
      default: "",
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
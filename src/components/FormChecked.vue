<template>
  <div>
    <label>
      {{ label }}
      <p v-for="input in initialValue" :key="input.id">
        {{ input.text }}
        <input
          :value="input.value"
          :type="type"
          @change="$emit('input', checked)"
          v-model="checked"
        />
      </p>
    </label>
    <span>{{ errorText }}</span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      checked: this.value,
    };
  },
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
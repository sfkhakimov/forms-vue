<template>
  <div class="form-checked">
    <label class="form-checked__label">
      {{ label }}
      <p
        v-for="input in initialValue"
        :key="input.id"
        class="form-checked__text"
      >
        {{ input.text }}
        <input
          :value="input.value"
          :type="type"
          @change="$emit('input', checked)"
          v-model="checked"
        />
      </p>
    </label>
    <span class="form-checked__error">{{ errorText }}</span>
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
    value: String,
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
  },
};
</script>

<style lang="scss" scoped>
.form-checked {
  padding-bottom: 2px;
  margin-top: 8px;
  display: flex;
  flex-direction: column;

  &__label {
    padding-bottom: 2px;
    display: flex;
  }

  &__error {
    color: red;
    font-size: 12px;
  }

  &__text {
    margin: 0;
    margin-left: 6px;
  }
}</style
>>

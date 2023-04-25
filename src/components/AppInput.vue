<template>
  <div class="app-input">
    <div class="app-input__labels-area">
      <label class="app-input__label" :for="label">
        {{ label }}
      </label>

      <div v-if="error" class="app-input__error-message">
        Can't be zero
      </div>
    </div>
    <div 
      class="app-input__input-wrapper"
      :class="{
        'green-border': inputFocus,
        'error-border': error
      }"
    >
      <img class="app-input__left-icon" :src="imagePath()" alt="icon">
      <input
        type="text"
        class="app-input__input"
        :name="label"
        :placeholder="placeholder"
        :value="modelValue"
        @input="updateValue"
        @focus="() => {
          inputFocus = true
          error = false
        }"
        @blur="(e) => {
          inputFocus = false
          error = e.target.value ? false : true
        }"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppInput',

  props: {
    label: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
    icon: {
      type: String,
      required: true,
    },
    modelValue: String
  },

  emits: ['update:modelValue'],

  data() {
    return {
      inputFocus: false,
      error: false
    }
  },

  methods: {
    updateValue(event) {
      this.$emit('update:modelValue', event.target.value);
    },

    imagePath() {
      return require(`../assets/${this.icon}`);
    }
  },
};
</script>

<style lang="scss">
  .app-input {
    width: 100%;

    &__labels-area {
      display: flex;
      justify-content: space-between;
    }

    &__label {
      color: #6A7777;
      font-size: 14px;
    }

    &__error-message {
      color: #C88877;
      font-size: 14px;
    }

    &__input-wrapper {
      display: flex;
      justify-content: space-between;
      background: #F3F8FB;
      padding: 7px 15px;
      border-radius: 2px;
    }

    &__left-icon {
      width: 10px;
      height: 15px;
      margin-top: 7px;
    }

    &__input {
      text-align: right;
      border: none;
      background-color: #F3F8FB;
      color: hsl(184, 14%, 56%);
      outline: none;
      font-family: 'Space Mono', monospace;
      font-size: 20px;
    }

    &__input::placeholder {
      color: hsl(184, 14%, 56%);
    }

    .green-border {
      border: 3px solid #35C6B3;
      border-radius: 4px;
    }

    .error-border {
      border: 3px solid #C88877;
      border-radius: 4px;
    }
  }
</style>
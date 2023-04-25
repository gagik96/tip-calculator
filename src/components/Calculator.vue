<template>
  <div class="calculator">
    <div class="calculator__details">
      <div class="calculator__details__left-part">
        <AppInput
          v-model="bill"
          icon="icon-dollar.svg" 
          label="Bill"
          placeholder="0"
        />

        <div class="calculator__details__tip-options">
          <label class="calculator__details__tip-options__label">
            Select Tip %
          </label>

          <div class="calculator__details__tip-options__tips">
            <div 
              v-for="tip in tipOptions"
              :key="tip.value"
              class="calculator__details__tip-options__tip-card"
              :class="{
                'active-tip': selectedTip === tip.value && !inputActive
              }"
              @click="() => {
                selectedTip = tip.value
                inputActive = false
                customTip = ''
              }"
            >
              {{ tip.label }}
            </div>

            <div class="calculator__details__tip-options__custom">
              <input
                v-model="customTip"
                type="text" 
                class="calculator__details__tip-options__input"
                :class="{
                  'active-input': inputActive
                }"
                placeholder="Custom"
                @focus="() => {
                  inputActive = true
                  selectedTip = null
                }"
              >
            </div>
          </div>
        </div>

        <AppInput
          v-model="people"
          icon="icon-person.svg" 
          label="Number of people"
          placeholder="0"
        />
      </div>
      <div class="calculator__details__right-part">
        <div class="calculator__details__right-part__rows-area">
          <div class="calculator__details__right-part__row">
            <div class="calculator__details__right-part__row-title-area">
              <div class="title">
                Tip Amount
              </div>
              <div class="subtitle">
                / person
              </div>
            </div>
            <div class="calculator__details__right-part__row-price">
              {{ `$${tipAmount}` }}
            </div>
          </div>

          <div class="calculator__details__right-part__row">
            <div class="calculator__details__right-part__row-title-area">
              <div class="title">
                Total
              </div>
              <div class="subtitle">
                / person
              </div>
            </div>
            <div class="calculator__details__right-part__row-price">
              {{ `$${totalAmount}` }}
            </div>
          </div>
        </div>
        
        <button class="calculator__details__right-part__reset-btn" @click="resetData()">
          RESET
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import AppInput from "./AppInput.vue"

export default {
  name: "Calculator",

  components: {
    AppInput
  },

  data() {
    return {
      bill: null,
      people: null,
      tipOptions: [
        {
          label: "5%",
          value: "5"
        },
        {
          label: "10%",
          value: "10"
        },
        {
          label: "15%",
          value: "15"
        },
        {
          label: "25%",
          value: "25"
        },
        {
          label: "50%",
          value: "50"
        }
      ],
      selectedTip: 5,
      inputActive: false,
      customTip: ''
    }
  },

  computed: {
    tipAmount() {
      if (!this.selectedTip || !this.bill) return 0

      return this.bill * this.selectedTip / 100
    },

    totalAmount() {
      if (!this.selectedTip || !this.bill || !this.people) return 0

      return this.bill * this.selectedTip * this.people / 100
    }
  },

  methods: {
    resetData() {
      this.bill = null
      this.people = null
      this.selectedTip = null
    }
  },

  watch: {
    customTip(val) {
      this.selectedTip = val
    }
  }
}
</script>

<style lang="scss">
  .calculator {
    width: 900px;
    height: 500px;
    background-color: #FFFFFF;
    border-radius: 30px;
    padding: 30px;

    &__details {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: space-between;

      &__left-part {
        width: 46%;
        display: flex;
        flex-wrap: wrap;
        align-content: space-between;
        padding: 10px 0px;
      }

      &__right-part {
        width: 40%;
        background-color: #00474B;
        border-radius: 20px;
        padding: 40px;
        display: flex;
        flex-wrap: wrap;
        align-content: space-between;

        &__rows-area {
          width: 100%;
        }

        &__row {
          width: 100%;
          display: flex;
          justify-content: space-between;
          align-items: center;
          margin-bottom: 30px;
        }

        &__row-title-area {
          .title {
            color: #EBF8F9;
            font-size: 15px;
            letter-spacing: 0.3px;
          }

          .subtitle {
            color: hsl(184, 14%, 56%);
            font-size: 12px;
          }
        }

        &__row-price {
          font-size: 40px;
          color: #35C6B3;
        }

        &__reset-btn {
          width: 100%;
          background: #35C6B3;
          color: hsl(183, 100%, 15%);
          border: none;
          border-radius: 5px;
          font-family: 'Space Mono', monospace;
          font-size: 17px;
          font-weight: bolder;
          padding: 8px 0px;
          cursor: pointer;
        }
      }

      &__tip-options {
        width: 100%;

        &__label {
          color: #6A7777;
          font-size: 14px;
        }

        &__tips {
          width: 100%;
          display: flex;
          flex-wrap: wrap;
          justify-content: space-between;
          margin-top: 10px;
        }

        &__tip-card {
          width: 30%;
          background-color: #00474B;
          color: #D7EBEB;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 18px;
          padding: 7px 0px;
          border-radius: 3px;
          margin-bottom: 10px;
          cursor: pointer;
        }

        .active-tip {
          background: #35C6B3;
          color: hsl(183, 100%, 15%);
        }

        &__custom {
          width: 30%;
        }

        &__input {
          width: 100%;
          height: 27px;
          font-family: 'Space Mono', monospace;
          font-size: 18px;
          color: hsl(183, 100%, 15%);
          padding: 5px 0px;
          text-align: center;
          border: none;
          background: #F3F8FB;
          outline: none;
        }

        .active-input {
          border: 3px solid #35C6B3;
          border-radius: 4px;
        }

        &__input::placeholder {
          color: hsl(184, 14%, 56%);
          font-weight: bold;
        }
      }
    }
  }
</style>
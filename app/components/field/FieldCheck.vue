<template>
  <div class="field">
    <label 
    class="check field__check"
    :class="{ 'check--red' :  red, 'check--disabled' :  disabled }"
    >
      <input
        type="checkbox"
        class="check__input"
        :value="checkedValue"
        :checked="checked"
        @change="handleChange"
        :disabled="disabled"
      />
      <span class="check__mark"></span>

      <span
        class="check__caption"
        :class="{
        'check__caption--s' : smallLabel
      }"
        v-html="label"
      ></span>
    </label>

    <span v-if="errorMessage && submitCount" class="field__error field-error">
      {{ errorMessage }}
    </span>
  </div>
</template>

<script setup>
  
  import { toRefs } from "vue";
import { useField } from "vee-validate";

  const props = defineProps({
    initialValue: {
      type: [ String, Number, Boolean],
    default: undefined,
  },
    name: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      default: "",
    },
    smallLabel: {
      type: Boolean,
      default: false,
    },
    checkedValue: {
      type: [String, Number],
      default: 1,
    },
    rules: {
      type: Object,
      default: () => ({}),
    },
    submitCount: {
      type: Number,
      default: 0,
    },
     red: {
    type: Boolean,
    default: false,
  },
  disabled: {
    type: Boolean,
    default: false,
  },
  });

const { red, disabled, checkedValue, name, rules } = toRefs(props);



  const { checked, errorMessage, handleChange } = useField(
    props.name,
    props.rules,
    {
      type: "checkbox",
      checkedValue: props.checkedValue,
    },
  );
</script>

<style lang="less">
.reserve {
  display: grid;
  gap: 65px 11%;
  grid-template-columns: 405px 1fr;
  // grid-template-columns: 405px calc(89% - 405px);
  grid-template-areas:
    "checks scheme"
    "order legend";
  width: 100%;
  margin-bottom: 150px;

  @media @bw1340 {
    gap: 65px 6.5%;
    grid-template-columns: 350px 1fr;
  }

  @media @bw1020 {
    gap: 60px;
    grid-template-columns: 1fr 390px;
    grid-template-areas:
      "scheme scheme"
      "checks legend"
      "checks order";
  }

  @media @bw768 {
    grid-template-columns: 100%;
    grid-template-areas:
      "scheme"
      "legend"
      "checks"
      "order";
  }

  &__book {
    box-sizing: border-box;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    min-height: 23px;
    // padding-left: 23px;

    // color: @black;
    // cursor: pointer;

    // &:last-child {
    //   margin-bottom: 0;
    // }

  }

  &__checks {
    grid-area: checks;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    // background-color: yellow;
  }

  &__check {
    margin-top: 0;
    margin-bottom: 10px;
    padding-left: 0;
  }

  &__reserve>div {
    box-sizing: border-box;
    padding: 10px;
    background-color: coral;
    text-align: center;
  }
}


</style>
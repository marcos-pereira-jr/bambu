<template>
  <div
    :class="['input-div ', { focus: isSelected }, { 'one-itens': renderIcon }]"
  >
    <div v-if="renderIcon" class="i">
      <i :class="icon"></i>
    </div>
    <div>
      <h5>{{ label }}</h5>
      <input
        @focus="onFocus"
        @blur="onBlur"
        @input="input"
        :value="value"
        class="input"
        :type="type"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: { type: [String, Number] },
    label: String,
    icon: {
      type: String,
      required: false,
    },
    type: {
      type: String,
      required: false,
      default: "text",
    },
  },
  data() {
    return {
      isFocus: false,
    };
  },
  methods: {
    input(event) {
      this.$emit("input", event.target.value);
      this.$emit("keyup", event.target.value);
    },
    onFocus() {
      this.isFocus = true;
    },
    onBlur() {
      this.isFocus = false;
    },
  },
  computed: {
    isSelected() {
      if (!this.value && this.isFocus) return true;
      if (!this.value && !this.isFocus) return false;
      if (!this.value.trim() && !this.isFocus) return false;
      return true;
    },
    renderIcon() {
      return this.icon;
    },
  },
};
</script>

<style scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
} /* retirar css padrão*/
.input-div {
  position: relative;
  display: grid;
  padding-top: 15px;
  border-bottom: 2px solid #d9d9d9;
  width: 100%;
}

.input-div.one-itens {
  grid-template-columns: 7% 93%;
}
.input-div:after,
.input-div:before {
  content: "";
  position: absolute;
  bottom: -2px;
  width: 0;
  height: 2px;
  background-color: #026702;
  transition: 0.3s;
}

.input-div::after {
  right: 50%;
}
.input-div::before {
  left: 50%;
}
.input-div.focus .i {
  color: #026702;
}
.input-div.focus div h5 {
  top: -5px;
  font-size: 15px;
}
/* Aumentar a barra abaixo do input*/
.input-div.focus:after,
.input-div.focus:before {
  width: 50%;
}
.input-div > div {
  position: relative;
  height: 45px;
}
/* tornar os filhos imediatos em uma posição absoluta para não aparecer os nomes dos campos */
.input-div > div h5 {
  position: absolute;
  left: 10px;
  top: 50%;
  transform: translateY(-50%);
  color: #999;
  font-size: 20px;
  /*display: none; */
  transition: 0.3s;
}
/* Input tornar absolute sem background */
.input {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  border: none;
  outline: none;
  background: none;
  padding: 0.5rem 0.7rem;
  font-size: 1.2rem;
  font-family: sans-serif;
  color: #555;
}
/*Tornar o incone no meio*/
.i {
  display: flex;
  justify-content: center;
  align-items: center;
}
.i i {
  color: #d9d9d9;
  transition: 0.3s;
}
</style>

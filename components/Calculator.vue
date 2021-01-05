<template>
  <div>
    <v-text-field
      v-model="current"
      name="name"
      v-bind:label="operator"
      id="id"
    ></v-text-field>
    <v-simple-table>
      <template>
        <tbody>
          <tr>
            <td><v-btn class="buttons" @click="append(7)">7</v-btn></td>
            <td><v-btn class="buttons" @click="append(8)">8</v-btn></td>
            <td><v-btn class="buttons" @click="append(9)">9</v-btn></td>
            <td><v-btn color="info" @click="sign('/')">/</v-btn></td>
          </tr>
          <tr>
            <td><v-btn class="buttons" @click="append(4)">4</v-btn></td>
            <td><v-btn class="buttons" @click="append(5)">5</v-btn></td>
            <td><v-btn class="buttons" @click="append(6)">6</v-btn></td>
            <td><v-btn color="info" @click="sign('*')">*</v-btn></td>
          </tr>
          <tr>
            <td><v-btn class="buttons" @click="append(1)">1</v-btn></td>
            <td><v-btn class="buttons" @click="append(2)">2</v-btn></td>
            <td><v-btn class="buttons" @click="append(3)">3</v-btn></td>
            <td><v-btn color="info" @click="sign('-')">-</v-btn></td>
          </tr>
          <tr>
            <td><v-btn color="error" @click="clear()">C</v-btn></td>
            <td><v-btn class="buttons" @click="append(0)">0</v-btn></td>
            <td><v-btn color="info" @click="calculate()">=</v-btn></td>
            <td><v-btn color="info" @click="sign('+')">+</v-btn></td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: 0,
      prev: null,
      operator: "",
      combo: false,
    };
  },
  methods: {
    calculate() {
      let current = parseInt(this.current);
      let prev = parseInt(this.prev);
      if (this.operator == "-") {
        this.current = prev - current;
      } else if (this.operator == "+") {
        this.current = prev + current;
      } else if (this.operator == "*") {
        this.current = prev * current;
      } else if (this.operator == "/") {
        this.current = prev / current;
      }
    //   this.combo = false;
    },
    clear() {
      this.current = 0;
      this.prev = null;
      this.operator = "";
      this.combo = false;
    },
    append(value) {
      if (this.combo) {
        this.prev = this.current;
        this.current = "";
      }
      if (this.current == 0) {
        this.current = "";
      }
      this.current += "" + value;
    },
    sign(operator) {
      if (this.prev != null) {
        this.calculate();
        this.combo = true;
      }
      this.operator = operator;
      if (!this.combo) {
        this.prev = this.current;
        this.current = 0;
      }
    },
  },
};
</script>

<style lang="css" scoped>
.buttons {
  background-color: #757575 !important;
  text-align: center;
}
</style>
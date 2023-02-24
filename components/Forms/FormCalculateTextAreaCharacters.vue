<template>
  <div class="container">
    <h4>Write Your Message ({{ maxLength }} Characters allowed)</h4>
    <textarea
      @input="countChars"
      v-model="message"
      :maxlength="maxLength"
    ></textarea>
    <span class="counter" :class="{ ' zero ': isReachZero }">
      Left | <span>{{ remainCharacters }}</span>
    </span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      maxLength: 10,
      remainCharacters: 10,
      message: null,
      isReachZero: false,
    };
  },
  methods: {
    countChars() {
      this.remainCharacters = this.maxLength - this.message.length;
      this.isReachZero = this.remainCharacters === 0;
    },
  },
};
</script>
<style>
.container {
  margin: 20px auto;
  width: 400px;
  text-align: center;
}
.container textarea {
  width: 400px;
  height: 200px;
  resize: none;
  background: #eee;
  border: 1px solid #ccc;
}
.container .counter {
  display: block;
  text-align: right;
  padding-top: 10px;
}
.zero span {
  color: red;
}
</style>

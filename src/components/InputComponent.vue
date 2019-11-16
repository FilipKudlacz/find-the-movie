<template>
    <input type="text" placeholder="Phrase" :value="value" @input="emitChange" />
</template>

<script>
export default {
    name: "InputComponent",
    props: {
        value: {
            type: String,
            required: true,
        },
    },
    methods: {
        emitChange(e) {
            this.$emit('input', e.target.value);
        },
    },
}
</script>

<style scoped>
input {
  height: 30px;
  width: 300px;
  font-size: 20px;
  text-align: center;
  border: 0;
  border-bottom: 2px solid #ff8300;
  background: none;
  margin-bottom: 20px;
  color: white;
}

input:focus {
    outline: none;
}
</style>
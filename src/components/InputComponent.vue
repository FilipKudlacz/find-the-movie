<template>
    <input type="text" placeholder="Movie Name" :value="value" @="emitChange" />
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
  background-color: #2c3e50;
  margin-bottom: 20px;
  color: white;
}
</style>
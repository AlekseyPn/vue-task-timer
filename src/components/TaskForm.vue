<template>
  <div class="container task-form">
    <label for="task-name">Name your task:</label>
    <div class="row">
      <input
        v-model="title"
        type="text"
        class="task-form__input"
        name="task-name"
        id="task-name"
        placeholder="Enter task name"
        @keyup.enter="addTask"
      >
      <div v-show="error" class="task-form__error">
        <span>Please Enter your task name</span>
      </div>
      <button @click="addTask" class="task-form__add-task">
        <i class="fas fa-plus"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      error: false
    };
  },
  methods: {
    addTask() {
      if (this.title !== "") {
        this.$emit("addTask", this.title);
        this.title = "";
        this.error = false;
      } else {
        this.error = true;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
$button-color: #7de591;
$blue-chill: #0d8a82;
.task-form {
  &__error {
    position: absolute;
    top: 57px;
    left: 25%;
    display: inline-block;
    width: 200px;
    padding: 10px 5px;
    text-align: center;
    font-size: 14px;
    border-radius: 5px;
    background-color: #f2dede;
    animation: showError 0.5s linear;
    &::before {
      content: "\25B2";
      position: absolute;
      top: -16px;
      left: calc(50% - 14px);
      color: #f2dede;
    }
  }

  &__input {
    width: 80%;
    padding-left: 5px;
    border: none;
    border-bottom: 1px solid #4e4a4a;
    border-radius: 4px;
    outline: none;
    transition: border-bottom-color 0.4s ease-in;
    &:focus {
      border-bottom-color: $blue-chill;
    }
    &:hover {
      border-bottom-color: #10b184;
    }
  }

  &__add-task {
    width: 40px;
    height: 40px;
    margin-left: 20px;
    background-color: $button-color;
    border-radius: 50%;
    border: 2px solid $button-color;
    color: #fff;
    box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.18), 0 1px 5px 0 rgba(0, 0, 0, 0.15);
    transition: all 0.2s linear;
    &:focus {
      outline: none;
      border-color: $blue-chill;
    }
    &:hover {
      box-shadow: 0 5px 11px 0 rgba(0, 0, 0, 0.18),
        0 4px 15px 0 rgba(0, 0, 0, 0.15);
      transition: box-shadow 0.4s ease-in;
    }
    &:active {
      transform: translateY(4px);
      box-shadow: 0 5px 6px 0 rgba(0, 0, 0, 0.18),
        0 4px 8px 0 rgba(0, 0, 0, 0.15);
      transition: all 0.4s ease-in;
    }
  }
}
</style>



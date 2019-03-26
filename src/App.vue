<template>
  <div id="app">
    <section class="wrapper">
      <h1 class="app__title">Task timer</h1>
      <p class="app__description">This timer will count your work time of your tasks</p>
      <task-list/>
    </section>
  </div>
</template>

<script>
import TaskList from "./components/TaskList";
export default {
  name: "App",
  components: {
    TaskList
  }
};
</script>

<style lang="scss">
html {
  height: 100%;
}
body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 16px;
  background-size: 100%;
  background-repeat: no-repeat;
  background-image: linear-gradient(
    45deg,
    rgba(157, 255, 150, 1) 0%,
    rgba(0, 128, 128, 1) 100%
  );
}
.app {
  &__title,
  &__description {
    text-align: center;
  }
}

.wrapper {
  max-width: 700px;
  min-height: 500px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
  padding: 20px 10px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 5px 8px -2px #000;
}

.container {
  display: flex;
  flex-flow: column wrap;
  width: 80%;
  margin-top: 30px;
  margin-left: auto;
  margin-right: auto;
}
.row {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0;
}

@keyframes showError {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>

<template>
  <teleport to="body">
    <section class="container">
      <div class="main">
        <header>
          <h1>{{ title }}</h1>
        </header>
        <section>
          <p>{{ message }}</p>
        </section>
        <footer>
          <slot></slot>
        </footer>
      </div>
    </section>
  </teleport>
</template>

<script>
export default {
  props: {
    title: String,
    message: String,
  },
};
</script>

<style scoped>
.container {
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  background-color: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(3px);
}
.container .main {
  display: flex;
  flex-direction: column;
  width: 95%;
  max-width: 400px;
  background-color: rgb(9, 95, 105);
  box-shadow: 0px 2px 5px 2px rgba(0, 0, 0, 0.4);
}
.container .main header {
  background-color: rgba(0, 0, 0, 0.2);
  padding: 20px;
  text-align: center;
}
.container .main section {
  padding: 20px;
  text-align: justify;
}
.container .main footer {
  text-align: center;
  padding-bottom: 15px;
}
</style>

<template>
  <Suspense>
    <CopyUrlMarkdownStyle />
  </Suspense>
</template>

<script>
import CopyUrlMarkdownStyle from "./components/CopyUrlMarkdownStyle";

export default {
  name: "App",
  components: {
    CopyUrlMarkdownStyle,
  },
};
</script>

<style>
#app {
  width: 400px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

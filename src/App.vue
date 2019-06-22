<template>
  <div id="app">
    <Tooltip
      msg="Lorem ipsum dolor amet taiyaki readymade before they sold out, artisan farm-to-table jean shorts fingerstache waistcoat church-key art party pitchfork kale chips roof party XOXO. Organic lo-fi kogi subway tile."
      :position="{x: '10px', y: '10px'}"
      background="teal"
      padding="18px"
      side="left"
      flow="down"
      header="Hello Vue!"
      linkText="You keep me coming for ya"
      :showArrow="true"
    >
      <div
        :style="{position: 'aboslute', top: '50px', left: '50%', transform: 'translate(-50%, -50%)', width: '200px', height: '100px'}"
      >test div</div>
    </Tooltip>
  </div>
</template>

<script>
import Tooltip from "./components/Tooltip";

export default {
  name: "App",
  components: {
    Tooltip
  }
};
</script>

<style>
html,
body {
  font-size: 14px;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

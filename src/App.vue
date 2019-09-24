<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
// sass 有两种语法
// (1) scss 和less 的语法比较类似的,该嵌套还是嵌套 区别:声明变量$
*{
  margin: 0;
  padding: 0;
}
html,
body,
#app{
  width: 100%;
  height: 100%;
}

</style>

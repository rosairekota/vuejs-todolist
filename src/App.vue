<template>
  <div id="app">
    <div class="nav">
      <router-link to="/">Accueil</router-link> 
      <router-link to="/about">A propos</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss" src="./App.scss"></style>

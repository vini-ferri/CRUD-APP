<template>
  <div>
    <div id="nav">
      <router-link id="logo-url" to="/">
        <img id="logo" :src="logo" :alt="alt">
      </router-link>
      <router-link to="/">Fazer Cadastro</router-link>
      <router-link to="/Cadastros">Cadastros</router-link>
    </div>
  </div>
</template>
  
  <script>
  
  export default {
    name: "Navbar",
    props: ["logo", "alt"]
  }
  </script>

<style scooped>
    #nav {
        background-color: #222;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }
    
    #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }

    #logo {
        width: 60px;
        height: 60px;
    }

    #nav a {
        color: #3cba92;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }

    #nav a:hover {
        color: #FFF;
    }
</style>
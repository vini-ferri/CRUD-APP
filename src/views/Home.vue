<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>Cadastre seu Usuário</h1>
      <UserForm />
    </div>
  </div>
</template>

<script>
  import Banner from "../components/Banner";
  import UserForm from "../components/UserForm";


  export default {
    name: "Home",
    components: {
      Banner,
      UserForm
    }
  }
</script>


<template>
  <Message :msg="msg" v-show="msg" />
  <div>
    <form id="user-form" method="POST" @submit="createUser">
      <div class="input-container">
        <label for="nome">Nome do Usuário:</label>
        <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
      </div>
      <div class="input-container">
        <label for="telefone">Telefone</label>
        <input type="text" id="telefone" name="telefone" v-model="telefone" placeholder="Digite o seu telefone">
      </div>
      <div class="input-container">
        <label for="email">Email</label>
        <input type="text" id="email" name="email" v-model="email" placeholder="Digite o seu email">
      </div>
      <div class="input-container">
        <label for="setor">Setor</label>
        <input type="text" id="setor" name="setor" v-model="setor" placeholder="Digite o seu setor">
      </div>

      <div class="input-container">
        <input class="submit-btn" type="submit" value="Criar um Usuário!">
      </div>
    </form>
  </div>
</template>

<script>
import Message from './Message'

export default {
  name: "UserForm",
  data() {
    return {
      nome: null,
      telefone: null,
      email: null,
      setor: null,
      opcionais: [],
      status: "Solicitado",
      msg: null
    }
  },
  methods: {
    async createUser(e) {

      e.preventDefault()

      const data = {
        nome: this.nome,
        telefone: this.telefone,
        email: this.email,
        setor: this.setor,

        status: "Solicitado"
      }

      const dataJson = JSON.stringify(data)    

      const req = await fetch("http://localhost:3000/users", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });

      const res = await req.json()

      console.log(res)

      this.msg = "Cadastro realizado com sucesso!"

      // clear message
      setTimeout(() => this.msg = "", 3000)

      // limpar campos
      this.nome = ""
      this.telefone = ""
      this.email = ""
      this.setor = ""
      
      this.carne = ""
      this.pao = ""
      this.opcionais = []
      
    }
  },
  mounted () {
    this.getUsers()
  },
  components: {
    Message
  }
}
</script>

<style scooped>
    
    #user-form {
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #3cba92;

    }

    input, select {
        padding: 10px 20px;
        width: 400px;
        border-radius: 50px;
        border: 1px solid #222;

    }

    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background: linear-gradient(to right, rgb(99, 233, 94), rgb(28, 91, 128));
        color: #002429;
        height: 43px;
        font-weight: bold;
        border: 0px solid;
        padding: 10px;
        border-radius: 50px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.2s;
    }

    .submit-btn:hover {
        background: linear-gradient(to right, rgb(134, 212, 88), rgb(27, 136, 146));
        box-shadow: inset 6px 4px 23px rgba(0, 0, 0, 0.2);
        transition: 0.2s;
    }

</style>
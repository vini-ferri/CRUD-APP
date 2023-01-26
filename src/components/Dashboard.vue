<template>
  <div id="user-table" v-if="users">
    <div>
      <div id="user-table-heading">
        <div class="order-id">#:</div>
        <div>Usuário:</div>
        <div>Telefone:</div>
        <div>Email:</div>
        <div>Setor:</div>
      </div>
    </div>
    <div id="user-table-rows">
      <div class="user-table-row" v-for="user in users" :key="user.id">
        <div class="order-number">{{ user.id }}</div>
        <div>{{ user.nome }}</div>
        <div>{{ user.telefone }}</div>
        <div>{{ user.email }}</div>
        <div>{{ user.setor }}</div>
        <div>
          <button class="delete-btn" @click="deleteUser(user.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há registros no momento!</h2>
  </div>
</template>
<script>
  export default {
    name: "Dashboard",
    data() {
      return {
        users: null,
        user_id: null,
      }
    },
    methods: {
      async getCadastros() {
        const req = await fetch('http://localhost:3000/users')

        const data = await req.json()

        this.users = data

        // Resgata os status de cadastros
        this.getStatus()

      },

      async deleteUser(id) {

        const req = await fetch(`http://localhost:3000/users/${id}`, {
          method: "DELETE"
        });

        const res = await req.json()

        this.getCadastros()

      },
      async updateUser(event, id) {

        const option = event.target.value;

        const dataJson = JSON.stringify({status: option});

        const req = await fetch(`http://localhost:3000/users/${id}`, {
          method: "PATCH",
          headers: { "Content-Type" : "application/json" },
          body: dataJson
        });

        const res = await req.json()

        console.log(res)

      }
    },
    mounted () {
    this.getCadastros()
    }
  }
</script>

<style scoped>
  #user-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #user-table-heading,
  #user-table-rows,
  .user-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #user-table-heading {
    font-weight: bold;
    padding: 15px 0 15px 50px;
    border-bottom: 3px solid #222;
  }

  .user-table-row {
    width: 100%;
    padding: 15px 5px 15px 50px;
    border-bottom: 1px solid #CCC;
  }

  #user-table-heading div,
  .user-table-row div {
    width: 19%;
  }

  #user-table-heading .order-id,
  .user-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: rgb(190, 7, 7);
    color:#ffffff;
    font-weight: bold;
    border: 0 solid;
    border-radius: 40px;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  
  .delete-btn:hover {
    background-color: #610000;
    color: rgb(189, 61, 22)226, 226, 226);
  }
  
</style>
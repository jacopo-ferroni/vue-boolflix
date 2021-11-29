<template>
  <div class="header">
      <div class="brand">
          <h1>BOOLFLIX</h1>
      </div>

      <div class="search">
          <input v-model="film" type="text" placeholder="Titoli, persone, generi...">
          <!-- COLLEGAMENTO $EMIT -->
          <button @click="$emit(`filmCercato`, film)">Cerca</button>
          <button @click="$emit(`resetFilm`, contatore_reset), delete_space()">Reset</button>
      </div>

      <div class="logIn">
          <button>Iscriviti</button>
          <button>Accedi</button>
      </div>
  </div>
</template>

<script>
export default {
    name : `Header`,
    data() {
        return {
            film : ``,
            contatore_reset : 0,
        }
    },

    created()  {

    },

    methods : {
        delete_space() {
            this.film = ``;
        }
    }
}
</script>

<style scoped lang="scss">
    .header {
        background-color: #e50914;
        display: flex;
        align-items: center;
        justify-content: space-between;
        .brand {
            color: white;
            padding: 20px;
            cursor: pointer;
        }
        .logIn {
            padding: 20px;
            button {
                padding: 10px;
                background-color: white;
                border-radius: 20px;
                cursor: pointer;
                margin: 0 5px;
                &:hover {
                    background-color: black;
                    color: white;
                }
            }
        }
        .search {
            input {
                padding: 10px;
                width: 300px;
                border-radius: 20px;
                border: 2px solid black;
            }
            button {
                padding: 7px;
                background-color: white;
                border: 2px solid wjite;
                border-radius: 20px;
                margin-left: 10px;
                cursor: pointer;
            }
        }
    }

</style>
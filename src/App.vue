<template>
  <div>

    <h1 v-html="this.question"></h1>

    <input type="radio" name="options" value="true">
    <label>Verdadeiro</label><br>

    <input type="radio" name="options" value="false">
    <label>Falso</label><br>

    <button class="send" type="button">Enviar</button>

  </div>
</template>

<script>
  export default {
    name: 'App',

    //propriedade de dados
    data() {
      return {
        question: undefined,
        respostaIncorreta: undefined,
        respostaCorreta: undefined
      }
    },

    computed: {
      respostas() {
        var respostas = [...this.respostaIncorreta]; //copiando o array de respostas para minha variavel
        respostas.push(this.respostaCorreta);

        return respostas;
      }
    },
    created() {
      this.axios
      .get('https://opentdb.com/api.php?amount=1&category=18&difficulty=easy&type=boolean')
      .then((response) => {
        this.question = response.data.results[0].question;
        this.respostaIncorreta = response.data.results[0].incorrect_answers;
        this.respostaCorreta = response.data.results[0].correct_answer;

        //console.log(response.data.results)  
      })
    }

  }

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto;
  max-width: 960px;

  input[type=radio] {
    margin: 12px 4px;
  }

  button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    cursor: pointer;
  }

}
</style>

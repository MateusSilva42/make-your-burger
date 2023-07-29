<template>
    <div>
        <p>Componente de Mensagem</p>
    </div>
    <div id="form-container">
        <form id="burger-form">
            <div class="input-container">
                <label for="name">Nome do cliente:</label>
                <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome" />
            </div>
            <div class="input-container">
                <label for="bread">Escolha o pão:</label>
                <select id="bread" name="bread" v-model="bread">
                    <option value="" selected disabled>Selecione o seu pão</option>
                    <option v-for="bread in breadList" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="meat">Escolha a carne do seu burger:</label>
                <select id="meat" name="meat" v-model="meat">
                    <option value="">Selecione o tipo de carne</option>
                    <option v-for="meat in meatList" :key="meat.id" :value="meat.tipo">{{ meat.tipo }}</option>
                </select>
            </div>
            <div class="input-container">
                <label id="opt-title" for="optionals">Selecione os opcionais:</label>
                <div id="opt-container" class="checkbox-container" v-for="opt in optionalList" :key="opt.id">
                    <input type="checkbox" name="optionals" v-model="optionals" :value="opt.tipo">
                    <span>{{opt.tipo}}</span>
                </div>
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar meu Burger!">
            </div>
        </form>
    </div>
</template>

<script>
export default {
  name: "BurgerForm",
  components: {
    //
  },
  data() {
    return {
        breadList: null,
        meatList: null,
        optionalList: null,
        bread: null,
        meat: null,
        optionals: [],
        name: null,   
        status: 'Solicitado',
        msg: null
     };
  },
  methods: {
    async getIngredients(){
        const req = await fetch('http://localhost:3000/ingredientes')
        const data = await req.json()

        this.breadList = data.paes
        this.meatList = data.carnes
        this.optionalList = data.opcionais
    }
  },
  mounted(){
      this.getIngredients()
  }
};
</script>


<style scoped>

    #form-container{
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 50px;
    }
    #burger-form{
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    input, select{
        padding: 5px 10px;
        width: 300px;
    }

    #opt-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opt-title{
        width: 100%;
    }

    .checkbox-container{
        display:flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span{
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn{
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover{
        background-color: transparent;
        color: #222;
    }







</style>
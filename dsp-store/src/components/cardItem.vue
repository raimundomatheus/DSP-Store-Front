<template id="login">
  <!--eslint-disable-->
  <div>
    <!-- Fixed navbar -->
    <nav class="navbar fixed-top navbar-expand-lg navbar-dark bg-dark">
      <a class="navbar-brand" href="index.html">
        <img class="logo" src="../_imagens/dspg_logo_p.png" height="40">
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbar1"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbar1">
        <ul class="navbar-nav ml-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">
              SOBRE
              <span class="sr-only">(current)</span>
            </a>
          </li>

          <li class="nav-item active">
            <a class="nav-link" href="/#/produtos">
              PRODUTOS
              <span class="sr-only">(current)</span>
            </a>
          </li>

          <ul class="nav navbar-nav navbar-right">
            <li class="nav-item dropdown">
              <a class="nav-link dropdown-toggle" href="#" data-toggle="dropdown">MATHEUS</a>
              <ul id="login-dp" class="dropdown-menu">
                <li>
                  <div class="row">
                    <div class="col-md-12">
                      Entrar com
                      <div class="social-buttons">
                        <a href="#" class="btn btn-fb">
                          <i class="fa fa-facebook"></i> Facebook
                        </a>
                      </div>ou
                      <form
                        @submit="checkform"
                        class="form"
                        role="form"
                        method="post"
                        action="login"
                        accept-charset="UTF-8"
                        id="login-nav"
                      >
                        <div class="form-group">
                          <label class="sr-only" for="email_login">email</label>
                          <input
                            v-model="email"
                            type="email"
                            class="form-control"
                            id="exampleInputEmail2"
                            placeholder="Email"
                            required
                          >
                        </div>

                        <div class="form-group">
                          <label class="sr-only" for="senha_login">senha</label>
                          <input
                            v-model="senha"
                            type="password"
                            class="form-control"
                            id="exampleInputPassword2"
                            placeholder="Senha"
                            required
                          >

                          <div class="help-block text-right">
                            <a href>Esqueceu a senha?</a>
                          </div>
                        </div>

                        <div class="form-group">
                          <button
                            type="submit"
                            value="Logar"
                            class="btn btn-primary btn-block"
                          >Entrar</button>
                        </div>

                        <div class="checkbox">
                          <label>
                            <input type="checkbox"> Permanecer logado
                          </label>
                        </div>
                      </form>
                    </div>
                    <div class="bottom text-center">
                      Novo por aqui?
                      <a href="/#/cadastro">
                        <b>Cadastre-se</b>
                      </a>
                    </div>
                  </div>
                </li>
              </ul>
            </li>
          </ul>
        </ul>
      </div>
    </nav>

    <div class="container_two">
      <div class="content top_baixo">
        <a href="/#/produtos/Camisas">
          <img id="camisa" src="../_imagens/camisa_logo_p.png">
        </a>
        <a href="/#/produtos/Bonés">
          <img id="bone" src="../_imagens/bonezinho.png">
        </a>
        <a href="/#/produtos/Copos">
          <img id="copo" src="../_imagens/copo2_logo_p.png">
        </a>
        <a href="/#/produtos/Adesivos">
          <img id="adesivo" src="../_imagens/adesivinho.png">
        </a>
      </div>
      <!--FIM DO CONTENT top_baixo -->
    </div>
    <!--FIM DO CONTAINER_Two -->

    <div id="cardItem" class="card mb-3 border-0" style="max-width: 1000px;">
      <div v-if="produto !== undefined ">
        <div class="row no-gutters">
          <div class="col-md-6">
            <img v-bind:src="produto.imagem" class="card-img" alt="...">
          </div>
          <div id="desc" class="col-md-6">
            <div class="card-body">
              <br>
              <h2 class="card-title">{{produto.nome}}</h2>
              <h2 class="card-title text-muted">_________________________</h2>
              <h2 class="card-text" id="color">R$ {{produto.valor}}</h2>
              <br>
              <h5 class="card-text">{{produto.descricao}}</h5>
              <h7 class="card-text" id="color">{{produto.estoque}} em estoque</h7>
              <h2 class="card-title text-muted">_________________________</h2>

              <a href="#" class="btn btn-primary" @click="()=>comprar(produto.id)">COMPRAR</a>
              <br>
              <br>
              <h8 class="card-text text-muted">REF: {{produto.referencia}}</h8>
              <br>
              <h8 class="card-text text-muted">Categoria: {{produto.categoria}}</h8>
            </div>
          </div>
        </div>
      </div>
      <div v-else>
        <h1>Nada encontrado</h1>
      </div>
    </div>

    <div class="content vp">
      <a id="ver_produtos" href="#" @click="()=>ver(produtos)" >Veja todos os produtos</a>
    </div>
    <!--FIM DO CONTENT VP-->

    <div class="content rdp">
      <a id="rdp" href></a>
    </div>
    <!--FIM DO CONTENT rdp-->

    <footer>
      <div class="rpe">
        <a id="rpe" href="https://www.instagram.com/calldasmatheus">DSP DEVELOPMENT</a>
      </div>
    </footer>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
import { constants } from "crypto";

export default {
  template: "#login",
  data() {
    return {
      email: "",
      senha: "",
      produtos: [],
      produto: {}
    };
  },
  created: function() {
    let id = this.$route.params.id;
    let url = "http://localhost:3000/produtos/";

    axios
      .get(url)
      .then(response => {
        this.produtos = response.data;

        this.produto = this.produtos.find(item => item.id == id);
        console.log(this.produto);
      })
      .catch(e => {
        console.log(e);
      });
  },
  updated: function() {
    let id = this.$route.params.id;
    let url = "http://localhost:3000/produtos/";

    axios
      .get(url)
      .then(response => {
        this.produtos = response.data;

        this.produto = this.produtos.find(item => item.id == id);
        console.log(this.produto);
      })
      .catch(e => {
        console.log(e);
      });
  },
  methods: {
    checkform: function(e) {
      let payload = {
        email: this.email,
        senha: this.senha
      };

      axios.post("http://localhost:3000/login", payload).then(response => {
        let token = response.data.token;
        window.localStorage.setItem("token", token);
        alert("Você está logado");
      });
      e.preventDefault();
    },

    ver: function(categoria) {
      this.$router.push("/produtos/");
    },

    comprar: function(id) {
      this.$router.push("/carrinho/" + id);
    },
    
  }
};
</script>

<style>
/* eslint-disable */

a.navbar-brand {
  margin-left: 110px;
}

.navbar {
  box-shadow: #000000;
}

.navbar-toggler-icon {
  margin-right: 110px;
}

#login-dp {
  min-width: 250px;
  padding: 14px 14px 0;
  overflow: hidden;
  background-color: rgba(255, 255, 255, 0.8);
}
#login-dp .help-block {
  font-size: 12px;
}
#login-dp .bottom {
  background-color: rgba(255, 255, 255, 0.8);
  border-top: 1px solid #ddd;
  clear: both;
  padding: 14px;
}
#login-dp .social-buttons {
  margin: 12px 0;
}
#login-dp .social-buttons a {
  width: 49%;
}
#login-dp .form-group {
  margin-bottom: 10px;
}
.btn-fb {
  color: #fff;
  background-color: #3b5998;
}
.btn-fb:hover {
  color: #fff;
  background-color: #496ebc;
}
.btn-tw {
  color: #fff;
  background-color: #55acee;
}
.btn-tw:hover {
  color: #fff;
  background-color: #59b5fa;
}
@media (max-width: 768px) {
  #login-dp {
    background-color: inherit;
    color: #fff;
  }
  #login-dp .bottom {
    background-color: inherit;
    border-top: 0 none;
  }
}

.navbar-right .dropdown-menu {
  right: 0;
  left: auto;
}

.navbar-expand-lg .navbar-nav .dropdown-menu {
  position: absolute;
}
.bg-dark {
  background-color: #152236 !important;
}
.navbar-expand-lg .navbar-nav {
  margin-right: 50px;
}

.navbar-dark .navbar-nav .nav-link {
  color: #00aeef;
  text-decoration: none;
  font-family: sans-serif; /*stratum2*/
  text-shadow: white;
  font-weight: bold;
}

.container_two {
  display: grid;
  grid-template-columns: 200px 2fr 1fr;
  grid-gap: 0px;
  grid-auto-rows: 100px;
  margin-top: 106px;
  margin-bottom: -78px;
}

.top_baixo {
  grid-column: 1/4;
  height: 62px;
  background-color: #2d4159;
  margin-top: -40px;
}

img#camisa {
  margin-top: 10px;
  height: 40px;
  width: 50px;
  margin-left: 560px;
  float: left;
}

img#bone {
  margin-top: 10px;
  height: 40px;
  width: 50px;
  margin-left: 20px;
  float: left;
}

img#copo {
  margin-top: 10px;
  height: 40px;
  margin-left: 22px;
  width: 30px;
  float: left;
}

img#adesivo {
  margin-top: 10px;
  height: 40px;
  margin-left: 20px;
  width: 40px;
  float: left;
}

.side {
  border: 0px solid #000000;
  padding: 5px 10px;
  grid-column: 1/4;
  height: 100px;
  background-color: #2d4159;
  margin-top: -5px;
}

h1#n_produtos {
  text-align: center;
  color: white;
  font-family: sans-serif;
  font-weight: bolder;
  margin-top: 23px;
}

.cont {
  display: grid;
  grid-template-columns: 200px 200px;
  grid-template-rows: 10px 10px;
  grid-template-columns: 2fr 2fr;
  grid-gap: 0px;
  margin-top: -252px;
}

.conte {
  color: #ffffff;
  background-color: #7777ff;
  padding: 5px 10px;
  margin-left: 0px;
  margin-top: 252px;
  height: 390px;
}

.vp {
  border: 0px solid #000000;
  padding: 5px 10px;
  grid-column: 1/4;
  height: 100px;
  background-color: #2d4159;
  text-align: center;
  margin-top: 50px;
  transition: 0.5s;
}

.vp:hover {
  background-color: #2a5285;
  transition: 0.8s;
}
a#ver_produtos {
  color: #fff;
  font-family: sans-serif;
  font-weight: bolder;
  font-size: 30px;
  float: right;
  margin-top: 20px;
  margin-right: 38%;
  text-decoration: none;
}

a#ver_produtos:hover {
  color: #fff;
  text-decoration: none;
  transition: 0.6s;
}

.rdp {
  border: 0px solid #000000;
  padding: 5px 10px;
  grid-column: 1/4;
  height: 400px;
  background-color: #000000ea;
  background-image: url(../_imagens/logo_N.png);
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: scroll;
  background-origin: padding-box;
  background-clip: border-box;
  background-size: 20%;
  background-position-y: 50px;

  text-align: center;
  margin-top: 0%;
}

a#rdp {
  color: #004080;
  font-family: sans-serif;
  font-weight: bolder;
  font-size: 30px;
  float: right;
  margin-top: 30px;
  margin-right: 38%;
}

.rpe {
  border: 0px solid #000000;
  padding: 5px 10px;
  grid-column: 1/4;
  height: 30px;
  background-color: #2d4159;
  text-align: center;
  margin-bottom: -7px;
}

a#rpe {
  color: white;
  font-family: sans-serif;
  font-weight: bolder;
  font-size: 15px;
  float: right;
  margin-top: -1px;
  margin-right: 44%;
}

a#rpe:hover {
  text-decoration: none;
  color: #55acee;
}

#cardItem {
  position: relative;
  margin-left: 170px;
  margin-top: 50px;
}

#desc {
  text-align: left;
}

.center {
  width: 150px;
  margin: 0px auto;
  margin-left: 0%;
}

#color {
  color: #57bf6d;
}
</style>

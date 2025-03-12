<template>
  <div class="container">
    <div class="login-container">
      <h1>Descubra a senha 💙</h1>

      <div v-if="!loginSucesso">
        <div class="tooltip-container">
          <input
            id="username"
            v-model="username"
            :disabled="usernameCorreto"
            placeholder="Digite seu nome"
          />
          <span class="tooltip" v-if="!usernameCorreto">
            Dica: O que é o que é a junção do nome do amor da minha vida com um
            fenômeno da natureza no qual no Brasil tem vários 😉
          </span>
        </div>
        <button v-if="!usernameCorreto" @click="verificarUsuario">
          Confirmar
        </button>

        <div
          v-if="usernameCorreto && perguntaAtual < enigmas.length"
          class="pergunta-container"
        >
          <h3>{{ enigmas[perguntaAtual].pergunta }}</h3>

          <div v-if="enigmas[perguntaAtual].opcoes" class="opcoes-container">
            <label
              v-for="(opcao, index) in enigmas[perguntaAtual].opcoes"
              :key="index"
              class="opcao"
            >
              <input type="radio" :value="opcao" v-model="respostaAtual" />
              {{ opcao }}
            </label>
          </div>

          <input
            v-else
            v-model="respostaAtual"
            @keyup.enter="verificarResposta"
            placeholder="Digite sua resposta"
          />

          <button @click="verificarResposta">Responder</button>
        </div>

        <p v-if="erro" class="erro">{{ erro }}</p>
        <p v-if="senhaGerada.length > 0" class="senha-parcial">
          Senha Parcial: {{ senhaGerada }}
        </p>

        <div>
          <button
            v-if="
              senhaGerada === senhaCorreta &&
              username.toLowerCase() === usuarioCorreto
            "
            @click="fazerLogin"
          >
            Entrar
          </button>
        </div>
      </div>

      <div v-else>
        <h2>
          Seja Bem-vinda, {{ username }} ou Melhor... Amor da minha vida!❤️
        </h2>
        <router-link to="/home">Ir para a Página Principal</router-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import { enigmas } from "@/data/enigmas";
import { useRouter } from "vue-router";

export default defineComponent({
  setup() {
    const router = useRouter();
    const username = ref(localStorage.getItem("username") || "");
    const usuarioCorreto = "miryarios";
    const usernameCorreto = ref(
      username.value.toLowerCase() === usuarioCorreto
    );
    const respostaAtual = ref("");
    const perguntaAtual = ref(
      parseInt(localStorage.getItem("perguntaAtual") || "0")
    );
    const senhaGerada = ref(localStorage.getItem("senhaGerada") || "");
    const senhaCorreta = "feliz2anosdenamoroeuteamomeuamor";
    const erro = ref("");
    const loginSucesso = ref(localStorage.getItem("loginSucesso") === "true");

    function verificarUsuario() {
      if (username.value.toLowerCase() === usuarioCorreto) {
        usernameCorreto.value = true;
        localStorage.setItem("username", username.value);
      } else {
        erro.value =
          "Nah esse não é o nome do amor da minha vida! Tente novamente.";
      }
    }

    function verificarResposta() {
      if (
        respostaAtual.value.toLowerCase() ===
        enigmas[perguntaAtual.value].resposta.toLowerCase()
      ) {
        senhaGerada.value += enigmas[perguntaAtual.value].parteSenha;
        perguntaAtual.value++;
        respostaAtual.value = "";
        erro.value = "";

        localStorage.setItem("perguntaAtual", perguntaAtual.value.toString());
        localStorage.setItem("senhaGerada", senhaGerada.value);
      } else {
        erro.value = "Que vacilo hein errando essa?! Tente novamente.";
      }
    }

    function fazerLogin() {
      if (
        senhaGerada.value === senhaCorreta &&
        username.value.toLowerCase() === usuarioCorreto
      ) {
        loginSucesso.value = true;
        localStorage.setItem("loginSucesso", "true");
        router.push("/home");
      }
    }

    onMounted(() => {
      username.value = "namorada 💙";
    });

    return {
      username,
      usuarioCorreto,
      usernameCorreto,
      respostaAtual,
      perguntaAtual,
      senhaGerada,
      senhaCorreta,
      erro,
      loginSucesso,
      verificarUsuario,
      verificarResposta,
      fazerLogin,
      enigmas,
    };
  },
});
</script>

<style scoped>
.login-container {
  text-align: center;
  max-width: 800px;
  margin: auto;
  padding: 50px;
  border-radius: 10px;
  background: #e8e0e0;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background: linear-gradient(to bottom, #b6988c, #a47565);
  color: #000000;
  font-family: Avenir, sans-serif;
}

input {
  display: block;
  width: 100%;
  margin: 10px 0;
  padding: 8px;
}

.pergunta-container {
  margin-top: 20px;
  padding: 100px;
  background: #e1dede;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.opcoes-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 8px;
  margin-bottom: 10px;
}

.erro {
  color: #a40000;
  margin-top: 10px;
}

.senha-parcial {
  margin-top: 10px;
  font-weight: bold;
}

.opcoes-container {
  flex-direction: column;
  gap: 12px;
  align-items: flex-start;
  margin-bottom: 20px;
}

.opcao {
  align-items: center;
  font-size: 18px;
  padding: 12px 20px;
  background-color: #524f4f;
  border-radius: 8px;
  width: 100%;
  transition: background-color 0.3s ease;
  cursor: pointer;
  color: white;
}

.opcao:hover {
  background-color: #6e6b6b;
}

input[type="radio"] {
  margin-right: 15px;
  transform: scale(1.5);
  vertical-align: middle;
}

.button-container {
  justify-content: center;
  align-items: center;
  align-content: center;
}

button {
  background-color: #4cafaf;
  color: white;
  padding: 12px;
  border: none;
  cursor: pointer;
  border-radius: 8px;
  margin-top: 20px;
  width: 100%;
  font-size: 16px;
}

button:hover {
  background-color: #3d8a8a;
}

input[type="text"] {
  margin-top: 15px;
  padding: 12px;
  font-size: 18px;
  border-radius: 8px;
  border: 1px solid #868484;
  width: 100%;
}
</style>

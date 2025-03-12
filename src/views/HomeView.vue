<template>
  <div class="home-container">
    <nav class="navbar">
      <h2>Nossos 2 anos ❤️</h2>
      <button @click="sair" class="sair-btn">Sair</button>
    </nav>

    <div class="content">
      <h1 class="title">Parabéns pra nós pelos 2 anos juntos, meu amor! 🎉</h1>
      <h2 class="subtitle">
        Seja bem-vinda, <b>{{ nomeUsuario }}</b> ou melhor, Amor da minha vida!
        Ao nosso mundinho 💖
      </h2>
      <h2 class="subtitle">Estamos juntos há:</h2>
      <p class="contador">{{ tempoJuntos }}</p>

      <div class="music-player">
        <iframe
          width="560"
          height="315"
          src="https://www.youtube.com/embed/g0QKf3VPoYY"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen
        ></iframe>
      </div>

      <button @click="abrirModal" class="mensagem-btn">
        Leia uma mensagem especial
      </button>

      <div v-if="modalAberto" class="modal">
        <div class="modal-content">
          <span @click="fecharModal" class="close">&times;</span>
          <h2>Para o Amor da Minha Vida 💖</h2>
          <p>{{ cartaRomantica }}</p>
        </div>
      </div>

      <div class="carrossel-container">
        <swiper
          :slidesPerView="1"
          :spaceBetween="20"
          :pagination="{ clickable: true }"
          :breakpoints="{
            768: { slidesPerView: 2 },
            1024: { slidesPerView: 3 },
          }"
          class="swiper"
        >
          <swiper-slide v-for="(frase, index) in frases" :key="index">
            <div class="card">
              <p>{{ frase }}</p>
            </div>
          </swiper-slide>
        </swiper>
      </div>

      <button @click="mostrarMensagemAleatoria" class="amo-voce-btn">
        💌Amo Você
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import { useRouter } from "vue-router";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/swiper-bundle.css";

export default defineComponent({
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    const router = useRouter();
    const dataInicio = new Date("2023-03-12");
    const tempoJuntos = ref("");
    const nomeUsuario = ref(localStorage.getItem("username") || "Meu Amor");
    const modalAberto = ref(false);
    const cartaRomantica = ref("");
    const mensagensAmor = ref([
      "Eu te amo mais que tudo neste mundo! 💖",
      "Você é a razão do meu sorriso todos os dias. 😊",
      "Meu coração bate mais forte por você. 💓",
      "Você é a minha vida, meu amor. ❤️",
      "Cada momento ao seu lado é um presente. 🎁",
      "Você é a melhor parte do meu dia!",
      "Suas notificações são as melhores!",
      "Amo quando você cozinha pra mim !😊",
      "Que mulher você é viu?! Que baita mulher",
      "Amo seus beijos!",
      "Amo seus abraços",
      "Amo teus carinhos",
      "Amo quando dormimos junto!",
    ]);

    const frases = ref([
      "Você é a mulher mais incrível que já conheci! 💖",
      "Meu amor por você cresce a cada dia. 🌹",
      "Você ilumina meus dias com seu sorriso. ☀️",
      "Sou grato por cada momento ao seu lado. ❤️",
      "Você é meu porto seguro em meio a tanto caos. 🌟",
      "Eu amo a forma como você me faz sentir especial. 💕",
      "Seu abraço depois de um dia cheio cura tanta coisa! ☀️",
      "O brilho dos seus olhos me encantam. 🌟",
      "Você é tão especial! Que um card não é suficiente pra detalhar isso",
      "Eu te amo mais que churrasco e o lanche de costela! (QUE LANCHE BOOOMMM)",
      "É inexplicavel a paz que sinto quando você deita no meu peito!",
    ]);

    function atualizarContador() {
      const agora = new Date();
      const diff = agora.getTime() - dataInicio.getTime();

      const dias = Math.floor(diff / (1000 * 60 * 60 * 24));
      const horas = Math.floor((diff / (1000 * 60 * 60)) % 24);
      const minutos = Math.floor((diff / (1000 * 60)) % 60);
      const segundos = Math.floor((diff / 1000) % 60);

      tempoJuntos.value = `${dias} dias, ${horas}h ${minutos}m ${segundos}s`;
    }

    function sair() {
      localStorage.clear();
      router.push("/");
    }

    function abrirModal() {
      cartaRomantica.value = `Meu amor querida ${nomeUsuario.value}, (usuária do nosso sistema kkkkk),\n\nHoje nós celebramos mais um ano das melhores decisões que poderiamos tomar nos ultimos anos...
      (Assistindo Sherek PS: Quem toma decisões assistindo um filme infantil?! kkkkkkkkk)
      Nosso relacionamento regado de muito amor, cumplicidade e parceria.
      Sei que o momento não é dos melhores porem sou extremamente grato...
      Grato a você e a Deus, por ter nos unido e mesmo que as coisas estejam complicadas eu acredito fielmente que papai do céu tem um propósito pra nós...
      Não é atoa tanta luta, tanta briga, tanta dificuldade e esse relacionamento ter nascido agora... Eu queria você não... Não era a hora, Não estávamos prontos um pro outro
      Cada novo dia ao seu lado tem sido uma bênção, um motivo novo pra agradecer... Sou tão grato por cada momento que passamos juntos sejam eles bons ou ruins.
      Você é a luz da minha vida, todos os momentos que me vejo sem você nela tudo parece vazio, sombrio, sem cor...
      A caminho do shopping falamos que odiariamos morar sozinhos kkkkk de fato eu não consigo me imaginar habitando uma casa sem você, sem nosso mundinho colorido de conto de fadas...
      Que a gente come bobeira, quando quer, sai kkkkkk como se a nossa vida fosse só aquilo ali
      Muito Obrigado Mirya Vitoria Rios Juliani, você deu cor, som cheiro e vida pro meu mundo e trouxe consigo seu jeito leveza no olhar e na forma de enxergar o mundo.
      O homem que sou hoje é só uma parte de como você me ajudou e participou de toda essa loucura chamada vida... Obrigado por dividir comigo seu tempo e sua vida!
      Não existe no mundo a possibilidade de viver e sentir tudo o que vivo e sinto contigo do meu lado!
      Te peço desculpas pelos dias caóticos e turbulentos... É uma fase, somos fortes, vamos superar isso muito em breve!
      E SIM eu quero muito morar com você nós vamos caminhar pra isso meu amor te prometo!
      Porém eu não quero só isso... Além disso eu quero você quero que seja minha mulher... Quero te dar a chance de escolher ficar com meu sobrenome (apesar que seu nome ficaria grande demais kkkk)
      Eu quero um filho ou filhos contigo não sabemos... Por aqui o meu mais sincero EU TE AMO!
      Te amo mais do que palavras podem expressar.\n\nCom todo o meu amor,\n Seu Namorado ❤️! vulgo seu Pietro ou melhor Pietrinho! Te amo Mirya`;
      modalAberto.value = true;
    }

    function fecharModal() {
      modalAberto.value = false;
    }

    function mostrarMensagemAleatoria() {
      const mensagem =
        mensagensAmor.value[
          Math.floor(Math.random() * mensagensAmor.value.length)
        ];
      alert(mensagem);
    }

    onMounted(() => {
      atualizarContador();
      setInterval(atualizarContador, 1000);
    });

    return {
      tempoJuntos,
      sair,
      nomeUsuario,
      frases,
      modalAberto,
      cartaRomantica,
      abrirModal,
      fecharModal,
      mostrarMensagemAleatoria,
    };
  },
});
</script>

<style scoped>
body {
  background-color: #f4d1c8;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.home-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 50vh;
  text-align: center;
  padding: 20px;
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #b22f2f;
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  z-index: 1000;
  margin: 0 0 0;
}

.navbar h2 {
  flex: 1;
  text-align: center;
}

.sair-btn {
  background-color: white;
  color: #b22f2f;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 8px;
  margin-right: 40px;
  transition: 0.3s ease-in-out;
}

.sair-btn:hover {
  background-color: #f8e1e1;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 900px;
  width: 100%;
  padding: 20px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-top: 80px;
}

.title {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 20px;
  line-height: 1.4;
  color: #b22f2f;
}

.subtitle {
  font-size: 20px;
  font-weight: normal;
  margin-bottom: 15px;
  line-height: 1.4;
  color: #333;
}

.contador {
  font-size: 2em;
  font-weight: bold;
  color: #b22f2f;
  margin-top: 10px;
}

.music-player {
  margin: 20px 0;
}

.mensagem-btn {
  background-color: #b22f2f;
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 8px;
  margin: 10px 0;
  transition: 0.3s ease-in-out;
}

.mensagem-btn:hover {
  background-color: #8a1f1f;
}

.amo-voce-btn {
  background-color: #ff6f61;
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 8px;
  margin: 10px 0;
  transition: 0.3s ease-in-out;
}

.amo-voce-btn:hover {
  background-color: #e65a50;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  max-width: 500px;
  width: 100%;
  text-align: center;
  position: relative;
}

.close {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 24px;
  cursor: pointer;
}

/* Estilos do carrossel */
.carrossel-container {
  width: 100%;
  margin-top: 20px;
}

.swiper {
  width: 100%;
  padding: 20px 0;
}

.card {
  background: #fff;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  font-size: 18px;
  color: #b22f2f;
}

@media (max-width: 768px) {
  .title {
    font-size: 24px;
  }

  .subtitle {
    font-size: 18px;
  }

  .contador {
    font-size: 1.5em;
  }

  .navbar {
    padding: 12px 10px;
  }

  .sair-btn {
    padding: 8px 16px;
    font-size: 14px;
  }

  .content {
    margin-top: 70px;
  }

  .swiper {
    padding: 10px 0;
  }

  .card {
    font-size: 16px;
    padding: 15px;
  }
}
</style>

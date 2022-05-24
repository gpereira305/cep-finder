<template>
  <main class="cep__main-content">
    <section class="cep__main-items">
      <!-- input -->
      <div class="cep__main-input">
        <input  
          type="text"
          placeholder="Insira o CEP"
          v-model.trim="cep"
          maxlength="8"
          @keypress="getOnlyNumbers"
        />
        <button type="button" class="cep__button" @click="getCep()">
          <img :src="plus" alt="Adicionar" />
          Adicionar endereços
        </button>
      </div>

      <div class="cep__main-cep--address" v-if="cepData.length > 0">
        <div class="cep__main-cep--item" v-for="item in cepData" :key="item.id">
          <img :src="pointer" alt="Localização" title="Localização" />
          <h3>
            cep<span>{{ item.cep }}</span>
          </h3>
        </div>
      </div>
      <div v-else style="height: 15vh"></div>

      <div class="cep__main-addresses">
        <button type="button" class="cep__button" @click="getAddresses()">
          Gerar endereços
        </button>
      </div>
      <span class="cep__main-divider"></span>

      <!-- box endereço de cep  -->
      <div v-if="cepAddress.length > 0">
        <div class="cep__main-address--box" v-for="item in cepAddress" :key="item.id">
          <img :src="pointer" alt="Localização" title="Localização" /> 
          <div class="cep__main-address--name">
            <div>
              <h4>{{ item.logradouro.length ? item.logradouro : `B. ${item.bairro}`}}</h4>
              <p>{{ item.localidade }}-{{ item.uf }}</p>
            </div> 
            <span class="cep__box-divider"></span>

            <div class="cep__main-address--number">
              <p>{{ item.cep }}</p>
              <img :src="trashcan" alt="Remover" title="Remover item" @click="removeAddress()"/>
            </div>
          </div>
        </div>
      </div>

      <div v-else class="cep__main-empty">
        <h2>Salve seus endereços aqui</h2>
      </div>
    </section>
  </main>
</template>

<script>
import pointer from "../assets/icons/icone-lugar.svg";
import trashcan from "../assets/icons/icone-lixo.svg";
import plus from "../assets/icons/icone-plus.svg";
import axios from "axios";
export default {
  name: "CepContent",
  components: {},
  data() {
    return {
      pointer,
      trashcan,
      plus,
      cep: null,
      baseUrl: "https://viacep.com.br/ws",
      cepData: [],
      cepAddress: [],
    };
  },
  // ====== methods =====
  methods: {
    getCep() {
      const url = `${this.baseUrl}/${this.cep}/json/`;
      axios
        .get(url)
        .then((res) => {
          const data = res.data;
          if (!data.erro) {
            this.response = data;
            this.cepData.push(data); 
            this.cep = null;
          } else {
            alert("CEP não encontrado");
            this.cep = null;
          }
        })
        .catch((error) => console.error(error));
    },
    getAddresses() {
      this.cepAddress.push(...this.cepData);
      this.cepData = []
    },
    removeAddress(index) {
      if (window.confirm("Deseja remover esse item?")) {
        this.cepAddress.splice(index, 1);
        localStorage.setItem("cepAddress", JSON.stringify(this.cepAddress));
      }
    },
    getOnlyNumbers(e) {
      e = e ? e : window.event;
      const charCode = e.which ? e.which : e.keyCode;
      if (
        charCode > 31 &&
        (charCode < 48 || charCode > 57) &&
        charCode !== 46
      ) {
        e.preventDefault();
      } else {
        return true;
      }
    },
  },
  // ====== mounted =====
  mounted() {
    if (localStorage.cepAddress) {
      this.cepAddress = JSON.parse(localStorage.cepAddress);
    }
  },
  // ====== watch =====
  watch: {
    cepAddress(newCeps) {
      localStorage.cepAddress = JSON.stringify(newCeps);
    },
  },
};
</script>

<style lang="css" scoped>
.cep__main-content {
  background-color: var(--white-color);
  grid-area: main;
}

.cep__main-items {
  width: 670px;
  padding: 60px 30px 10px;
}

.cep__main-input {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.cep__main-input input {
  width: 293px;
  height: 50px;
  padding: 0 25px;
  border: 2px solid var(--gray-color-2);
  border-radius: 10px;
  outline: none;
  transition: all ease 0.2s;
  font-size: 1rem;
}

.cep__main-input input::placeholder {
  color: var(--gray-color-3);
  font-size: 1rem;
}

.cep__main-input input:focus {
  border: 2px solid var(--purple-color);
}

.cep__button {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 292px;
  height: 52px;
  padding: 0 25px;
  background-color: var(--purple-color);
  outline: none;
  border-radius: 8px;
  color: var(--white-color);
  font-size: 1rem;
  cursor: pointer;
  border: 3px solid var(--purple-color);
  transition: all ease 0.2s;
}

.cep__button img {
  margin-right: 10px;
}

.cep__button:hover {
  filter: brightness(1.09);
}

.cep__main-cep--address {
  display: flex;
  flex-direction: column;
  padding: 45px 0;
}

.cep__main-cep--item {
  display: flex;
  margin-bottom: 20px;
  max-width: 185px;
  justify-content: space-between;
  align-items: center;
}

.cep__main-cep--item img {
  margin-right: 10px;
}
.cep__main-cep--item h3 {
  text-transform: uppercase;
}

.cep__main-cep--item h3 span {
  color: #c9c9c9;
  font-weight: 500;
  margin-left: 5px;
}

.cep__main-addresses {
  display: flex;
  justify-content: flex-end;
}

.cep__main-divider {
  width: 100%;
  height: 1px;
  background-color: var(--gray-color-4);
  display: flex;
  margin-top: 8%;
}

.cep__main-address--box {
  display: flex;
  border-radius: 8px;
  margin-top: 20px;
  box-shadow: rgb(149 157 165 / 37%) 0px 4px 24px;
  padding: 45px 20px;
}

.cep__main-address--box > img {
  width: 24px;
}

.cep__main-empty {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 40vh;
}

.cep__main-empty h2 {
  font-weight: 400;
  text-align: center;
  color: var(--gray-color-4);
}

.cep__main-address--name {
  display: flex;
  justify-content: space-between;
  width: 100%;
  position: relative;
}

.cep__main-address--name h4 {
  margin-bottom: 8px;
}

.cep__main-address--name > div {
  margin-left: 25px;
}

.cep__main-address--number {
  display: flex;
  width: 150px;
  justify-content: space-between;
  align-items: center;
  position: relative;
  transition: all ease 0.2s;
}

.cep__main-address--number p {
  color: var(--purple-color);
}

.cep__main-address--number::after {
  position: absolute;
  content: "";
  width: 2px;
  height: 200%;
  z-index: 1;
  background: var(--gray-color-5);
  right: 55px;
}

.cep__main-address--number:hover img {
  cursor: pointer;
  transform: scale(1.05);
}

@media (max-width: 860px) {
  .cep__main-items {
    flex-direction: column;
    align-items: start;
    width: 90%;
    margin: auto;
  }

  .cep__main-input {
    flex-direction: column;
  }

  .cep__main-input input {
    margin-bottom: 20px;
    width: 238px;
  }

  .cep__main-cep--address {
    align-items: center;
  }

  .cep__main-addresses {
    justify-content: center;
  }

  .cep__main-address--box {
    flex-direction: column;
    padding: 20px;
  }
  .cep__main-address--name {
    flex-direction: column;
  }

  .cep__main-address--name h4 {
    margin-bottom: 3px;
  }

  .cep__main-address--name > div {
    margin-left: 0;
  }

  .cep__main-address--number {
    width: 100%;
    margin-left: 0;
    margin-top: 30px;
  }

  .cep__main-address--number::after {
    display: none;
  }

  .cep__box-divider {
    position: absolute;
    width: 100%;
    height: 2px;
    background: var(--gray-color-5);
    z-index: 1;
    top: 65px;
  }
}

@media (max-width: 620px) {
  .cep__main-items {
    margin: auto;
  }
}

@media (max-width: 520px) {
  .cep__main-items {
    padding: 60px 10px;
  }
}
</style>

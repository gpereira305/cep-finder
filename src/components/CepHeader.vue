<template>
  <div class="cep__header">
    <div class="cep__header--wrapper">
      <img :src="logo" alt="Logo" title="Logo" />  
      
      <div class="cep__header--menu">
        <div class="cep__header--menu-title">
          <p>Surreal São Paulo</p>
          <span>vtex</span>
        </div>
        <img :src="bell" alt="Sino" title="Notificações" onclick="alert('Aqui será mostrado as notificações')"/>
      </div>

      <span class="border-divider"></span>

      <div class="cep__header--user">
        <p>Olá, Visitante</p>
        <img :src="user" alt="Usuário" title="Usuário" onclick="alert('Aqui será mostrado o avatar do usuário!')"/>
      </div>
    </div>
  </div>
</template>

<script>
import logo from "../assets/icons/logo.svg";
import user from "../assets/icons/usuario.svg";
import bell from "../assets/icons/icone-bell.svg";

export default {
  components: {},
  data() {
    return {
      logo,
      user,
      bell,
    };
  },
};
</script>

<style scoped lang="css">
.cep__header {
  background-color: var(--header-color);
  height: 80px;
}

.cep__header--wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
  padding: 0 3% 0 2%;
  cursor: pointer;
}

.cep__header--wrapper > img {
  margin-right: 15px;
}

.cep__header--menu {
  display: flex;
  width: 100%;
  justify-content: space-between;
  transition: all ease 0.2s;
}

.cep__header--menu img {
  margin-right: 30px;
}

.cep__header--menu img:hover {
  transform: scale(1.05);
}

.cep__header--menu-title {
  width: 230px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  border: 2px solid var(--white-color);
  border-radius: 10px;
  margin-left: 20px;
  padding: 5px 15px;
  color: var(--white-color);
}

.cep__header--menu-title span {
  text-align: left;
  text-transform: uppercase;
  font-size: 0.75rem;
}

.cep__header--user {
  min-width: 210px;
  height: 100%;
  display: flex;
  justify-content: end;
  align-items: center;
  color: var(--white-color);
  position: relative;
  border-left: 1.3px solid var(--purple-color);
}

.cep__header--user img {
  margin-left: 20px;
}

@media (max-width: 790px) {
  .cep__header {
    height: 58px;
  }

  .cep__header--menu-title {
    display: none;
  }

  .cep__header--menu {
    justify-content: flex-end;
  }

  .cep__header--menu img {
    width: 24px;
    margin-right: 20px;
  }

  .cep__header--wrapper > img,
  .cep__header--user img {
    width: 40px;
  }

  .cep__header--user {
    min-width: 150px;
  }

  .cep__header--user p {
    font-size: 0.75rem;
  }
}
</style>

<template>
  <aside class="cep__side-menu">
    <div class="cep__side-menu-top">
      <img
        :src="search"
        alt="Pesquisa"
        title="Pesquisa"
        class="search-icon"
        onclick="alert('Aqui será feito pesquisas')"
      />
      <img
        :src="folder"
        alt="Pasta"
        title="Pasta"
        class="folder-icon"
        onclick="alert('Aqui estará suas pastas')"
      />
    </div>

    <div class="cep__side-menu-bottom">
      <img
        :src="settings"
        alt="Ajustes"
        title="Ajustes"
        class="settings-icon"
        onclick="alert('Aqui será feito os ajustes')"
      />
    </div>
  </aside>
</template>
<script>
import search from "../assets/icons/icone-busca.svg";
import folder from "../assets/icons/icone-folder2.svg";
import settings from "../assets/icons/icone-ajuste.svg";
export default {
  name: "CepSideMenu",
  components: {},
  data() {
    return {
      search,
      folder,
      settings,
    };
  },
};
</script>
<style lang="css" scoped>
.cep__side-menu {
  display: flex;
  background-color: var(--gray-color);
  grid-area: aside;
  justify-content: space-between;
  flex-direction: column;
  min-height: 83vh;
  padding: 30px 0 20px;
}

.cep__side-menu-top,
.cep__side-menu-bottom {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  transition: all ease 0.2s;
}

.cep__side-menu-top {
  min-height: 140px;
  display: flex;
  justify-content: space-between;
}

.cep__side-menu-top .search-icon,
.cep__side-menu-top .folder-icon {
  transition: all ease 0.2s;
}

.cep__side-menu-top .search-icon:hover,
.cep__side-menu-top .folder-icon:hover {
  transform: scale(1.05);
}

.cep__side-menu-bottom:hover {
  transform: scale(1.05);
}

.cep__side-menu-bottom img {
  padding: 5px;
  border-radius: 5px;
  background-color: var(--dark-color);
}

@media (max-width: 790px) {
  .cep__side-menu-top .search-icon,
  .cep__side-menu-top .folder-icon,
  .cep__side-menu-bottom .settings-icon {
    width: 28px;
  }
}
</style>

<template>
  <section>
    <cep-header></cep-header>

    <div class="cep__grid">
      <cep-side-menu></cep-side-menu>
      <cep-content></cep-content>
    </div>

     <cep-footer></cep-footer>
  </section>
     
</template>

<script>
import CepHeader from "../components/CepHeader.vue";
import CepContent from "@/components/CepContent.vue";
import CepSideMenu from "@/components/CepSideMenu.vue";
import CepFooter from "@/components/CepFooter.vue";

export default {
  name: "CepFinder",
  components: {
    CepHeader,
    CepSideMenu,
    CepContent,
    CepFooter
  },
  data() {
    return {};
  },
};
</script>
<style scoped lang="css">
.cep__grid {
  display: grid;
  grid-template-areas:
    "header header header"
    "aside main main"
    "footer footer footer";
  grid-template-columns: 110px auto auto;
}

.cep__side-menu {
  display: flex;
  background-color: var(--gray-color);
  grid-area: aside;
  justify-content: space-between;
  flex-direction: column;
  padding: 60px 0 20px;
}

@media (max-width: 790px) {
  .cep__grid {
    grid-template-columns: 55px auto auto;
  }
}

@media (max-width: 420px) {
  .cep__grid {
    grid-template-columns: 50px auto auto;
  }
}
</style>

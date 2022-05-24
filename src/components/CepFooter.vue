<template lang="">
    <footer class="cep__footer">
       <div class="cep__footer-text">
           <p>&copy; All Rights Reserved | CEP Finder App <span>{{new Date().getFullYear()}}</span></p>
       </div>
    </footer>
</template>
<script>
export default {
    name: 'CepFooter', 
    
}
</script>
<style lang="css" scoped>
    
    .cep__footer{
        width: 100%;
        height: 8vh;
        background-color: var(--dark-color);
        margin-top: 3%;
        padding: 8px 0;
    }

    .cep__footer-text{
        display: flex;
        justify-content: center;
        align-items: flex-end; 
        color: var(--gray-color);
        height: 100%; 
    }

    .cep__footer-text p {
        text-align: center;
        font-size: .75rem;
    }
</style>
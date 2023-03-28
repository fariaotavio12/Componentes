<script setup lang="ts">
import Dropdow from '../components/Dropdow.vue';
import Icon from '@/components/icons/icon.vue';

</script>

<template>
  <div class="container">

  <span>
    <h1>Codigos reutilizaveis</h1>
  </span>
  
  <pre>
      Dropdown
      <div style="width:100px; margin: 0 auto;">
        <Dropdow :style-object="{ fontSize: '14px' ,borderRadius: '3px' , textAlign: 'start'}" :ativo="true" :dropdownList="[{ 'name': 'otavio', 'href': 'asdad' }, { 'name': 'otavio', 'href': 'asdad' }]" :separator="[1]">
          <template #title>Examples</template>
          <template #icon>
            <svg width="8" height="5" viewBox="0 0 8 5" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M0.497877 0.714623C0.636882 0.714623 0.775887 0.764324 0.87489 0.861154L3.999 3.9203L7.12311 0.861154C7.30512 0.682918 7.62113 0.664923 7.82913 0.820879C8.03714 0.976836 8.05814 1.24762 7.87614 1.42585L4.37601 4.85347C4.28101 4.94601 4.144 5 4 5C3.85599 5 3.71899 4.94687 3.62399 4.85347L0.123864 1.42585C-0.0581417 1.24762 -0.0371418 0.976836 0.170866 0.820879C0.265869 0.749756 0.382873 0.714623 0.499877 0.714623H0.497877Z"
              />
            </svg>
          </template>
        </Dropdow>
      </div>
      
      <code class="html">
          Responsavel por passar o stylo para componente
          :style-object="{ fontSize: '14px' }"

          responsavel por detectar se o componente e igual a pagina da rota
          :ativo="true"

          Responsavel por passar a lista de item do dropdow
          :dropdownList="[{ 'name': 'otavio', 'href': 'asdad' }, 
                          { 'name': 'otavio', 'href': 'asdad' }]" 

          responsavel por inserir um separador(pode ser varios valores)
          :separator="[1]"

          Nome do titulo
          template #title 

          Icon a ser passado para o componente
          template #icon

          caso o dropdow seja da cor diferente do componente pai voce 
          pode retirar o undergraud comentando o before
      </code>
    </pre>
  </div>
</template>

<script lang="ts" setup>
</script>
<style>
.container {
  width: 100%;
  height: 100%;

  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

pre{
  width: 80%;
  background-color: black;
  color: aliceblue;
  border-radius: 10px ;
  padding: 10px;
  margin: 20px 0 ;
  overflow: auto;
}


</style>



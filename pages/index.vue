<template>
  <div style="padding: 2rem; max-width: 800px; margin: 0 auto; font-family: system-ui, sans-serif;">
    <h1>Bem-vindo à Aplicação Nuxt 3!</h1>
    <p>Esta é a página inicial da atividade prática de Node.js, Vue.js e Nuxt.</p>

    <div style="margin-top: 1.5rem;">
      <NuxtLink 
        to="/cadastro" 
        style="background-color: #00dc82; color: #000; padding: 0.75rem 1.25rem; text-decoration: none; font-weight: bold; border-radius: 6px; display: inline-block;"
      >
        Ir para o Formulário de Cadastro →
      </NuxtLink>
    </div>
  </div>
</template>
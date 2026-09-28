<template>
  <div>
    <header style="padding: 1rem; background: #0f172a; color: white;">
      <nav style="display: flex; gap: 1rem;">
        <NuxtLink to="/" style="color: white; text-decoration: none;">Início</NuxtLink>
        <NuxtLink to="/cadastro" style="color: #00dc82; text-decoration: none;">Formulário de Cadastro</NuxtLink>
      </nav>
    </header>

    <main>
      <NuxtPage />
    </main>
  </div>
</template>
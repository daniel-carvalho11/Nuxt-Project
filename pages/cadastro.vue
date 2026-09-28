<template>
  <div class="container">
    <h1>Cadastro de Membro</h1>
    <p>Preencha os dados abaixo para se juntar à nossa comunidade.</p>

    <!-- Alerta de Sucesso -->
    <div v-if="enviado" class="alert-success">
      ✅ Cadastro realizado com sucesso! Verifique o console para ver os dados enviados.
    </div>

    <form @submit.prevent="handleSubmit" class="form-card">
      <!-- Nome Completo -->
      <div class="form-group">
        <label for="nome">Nome Completo *</label>
        <input
          id="nome"
          v-model="form.nome"
          type="text"
          placeholder="Digite seu nome completo"
          :class="{ 'input-error': erros.nome }"
        />
        <span v-if="erros.nome" class="error-text">{{ erros.nome }}</span>
      </div>

      <!-- E-mail -->
      <div class="form-group">
        <label for="email">E-mail *</label>
        <input
          id="email"
          v-model="form.email"
          type="email"
          placeholder="seu.email@exemplo.com"
          :class="{ 'input-error': erros.email }"
        />
        <span v-if="erros.email" class="error-text">{{ erros.email }}</span>
      </div>

      <!-- Curso / Área de Atuação -->
      <div class="form-group">
        <label for="curso">Curso / Área de Atuação *</label>
        <select id="curso" v-model="form.curso" :class="{ 'input-error': erros.curso }">
          <option value="">Selecione uma opção</option>
          <option value="Engenharia de Software">Engenharia de Software</option>
          <option value="Ciência da Computação">Ciência da Computação</option>
          <option value="Sistemas de Informação">Sistemas de Informação</option>
          <option value="Análise e Desenv. de Sistemas">Análise e Desenv. de Sistemas</option>
          <option value="Outro">Outro</option>
        </select>
        <span v-if="erros.curso" class="error-text">{{ erros.curso }}</span>
      </div>

      <!-- Semestre / Período -->
      <div class="form-group">
        <label for="semestre">Semestre / Período *</label>
        <input
          id="semestre"
          v-model.number="form.semestre"
          type="number"
          min="1"
          max="12"
          placeholder="Ex: 6"
          :class="{ 'input-error': erros.semestre }"
        />
        <span v-if="erros.semestre" class="error-text">{{ erros.semestre }}</span>
      </div>

      <!-- Interesses / Habilidades -->
      <div class="form-group">
        <label>Interesses / Habilidades</label>
        <div class="checkbox-group">
          <label><input type="checkbox" v-model="form.interesses" value="Front-end" /> Front-end</label>
          <label><input type="checkbox" v-model="form.interesses" value="Back-end" /> Back-end</label>
          <label><input type="checkbox" v-model="form.interesses" value="Mobile" /> Mobile</label>
          <label><input type="checkbox" v-model="form.interesses" value="UI/UX" /> UI/UX</label>
          <label><input type="checkbox" v-model="form.interesses" value="DevOps" /> DevOps</label>
        </div>
      </div>

      <!-- Bio Curta -->
      <div class="form-group">
        <label for="bio">Mensagem / Bio Curta (máx. 200 caracteres)</label>
        <textarea
          id="bio"
          v-model="form.bio"
          maxlength="200"
          rows="3"
          placeholder="Conte um pouco sobre suas expectativas..."
        ></textarea>
        <small>{{ form.bio.length }}/200 caracteres</small>
      </div>

      <!-- Botão de Submissão -->
      <button type="submit" class="btn-submit">Cadastrar</button>
    </form>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'

const form = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: null,
  interesses: [],
  bio: ''
})

const erros = reactive({
  nome: '',
  email: '',
  curso: '',
  semestre: ''
})

const enviado = ref(false)

const validarEmail = (email) => {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return re.test(email)
}

const handleSubmit = () => {
  // Limpa erros anteriores
  erros.nome = ''
  erros.email = ''
  erros.curso = ''
  erros.semestre = ''
  enviado.value = false

  let valido = true

  if (!form.nome.trim()) {
    erros.nome = 'Nome completo é obrigatório.'
    valido = false
  }

  if (!form.email.trim()) {
    erros.email = 'E-mail é obrigatório.'
    valido = false
  } else if (!validarEmail(form.email)) {
    erros.email = 'Insira um e-mail válido.'
    valido = false
  }

  if (!form.curso) {
    erros.curso = 'Selecione um curso.'
    valido = false
  }

  if (!form.semestre || form.semestre < 1) {
    erros.semestre = 'Informe um semestre válido.'
    valido = false
  }

  if (valido) {
    // 1. Log formatado no console
    console.log('🚀 [Novo Cadastro Submetido]:', JSON.parse(JSON.stringify(form)))

    // 2. Feedback visual na tela
    enviado.value = true

    // 3. Limpeza reativa dos campos
    form.nome = ''
    form.email = ''
    form.curso = ''
    form.semestre = null
    form.interesses = []
    form.bio = ''
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 0 1rem;
  font-family: system-ui, -apple-system, sans-serif;
}

.form-card {
  background: #ffffff;
  border: 1px solid #e5e7eb;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.form-group {
  margin-bottom: 1.25rem;
  display: flex;
  flex-direction: column;
}

label {
  font-weight: 600;
  margin-bottom: 0.35rem;
  font-size: 0.9rem;
}

input[type="text"],
input[type="email"],
input[type="number"],
select,
textarea {
  padding: 0.6rem;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 0.95rem;
}

.input-error {
  border-color: #ef4444 !important;
}

.error-text {
  color: #ef4444;
  font-size: 0.8rem;
  margin-top: 0.25rem;
}

.checkbox-group {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 0.25rem;
}

.checkbox-group label {
  font-weight: normal;
  display: flex;
  align-items: center;
  gap: 0.3rem;
  cursor: pointer;
}

small {
  color: #6b7280;
  font-size: 0.75rem;
  margin-top: 0.2rem;
  text-align: right;
}

.btn-submit {
  background-color: #00dc82; /* Verde padrão do Nuxt */
  color: #000;
  font-weight: bold;
  padding: 0.75rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  width: 100%;
  font-size: 1rem;
  transition: background 0.2s;
}

.btn-submit:hover {
  background-color: #00b86b;
}

.alert-success {
  background-color: #d1fae5;
  color: #065f46;
  padding: 1rem;
  border-radius: 6px;
  margin-bottom: 1rem;
  border: 1px solid #a7f3d0;
}
</style>
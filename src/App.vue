<script setup>
import { ref, computed, watch } from 'vue'

const chave = 'organizador-estudos-vue'

function lerSalvas() {
  try {
    const dados = JSON.parse(localStorage.getItem(chave) || '[]')
    return Array.isArray(dados) ? dados : []
  } catch {
    return []
  }
}

const tarefas = ref(lerSalvas())
const texto = ref('')
const prioridade = ref('Média')
const filtro = ref('Todas')

const pendentes = computed(() => tarefas.value.filter((t) => !t.concluida).length)
const concluidas = computed(() => tarefas.value.filter((t) => t.concluida).length)
const tarefasVisiveis = computed(() => {
  if (filtro.value === 'Pendentes') return tarefas.value.filter((t) => !t.concluida)
  if (filtro.value === 'Concluídas') return tarefas.value.filter((t) => t.concluida)
  return tarefas.value
})

watch(tarefas, (lista) => localStorage.setItem(chave, JSON.stringify(lista)), { deep: true })

function adicionar() {
  const nome = texto.value.trim()
  if (!nome) return

  tarefas.value.unshift({
    id: String(Date.now()) + Math.random().toString(36).slice(2),
    nome,
    prioridade: prioridade.value,
    concluida: false
  })

  texto.value = ''
}

function alternar(tarefa) {
  tarefa.concluida = !tarefa.concluida
}

function excluir(id) {
  tarefas.value = tarefas.value.filter((t) => t.id !== id)
}
</script>

<template>
  <div class="pagina">
    <header class="cabecalho">
      <div class="topo">
        <span class="marca">Vue 3 · Programação Web</span>
        <h1>Organizador de <span>Estudos</span></h1>
        <p>Suas atividades acadêmicas, prioridades e progresso em um só lugar.</p>
      </div>
    </header>

    <main class="principal">
      <section class="indicadores" aria-label="Resumo das atividades">
        <div class="indicador">
          <small>Total de tarefas</small>
          <strong>{{ tarefas.length }}</strong>
        </div>
        <div class="indicador">
          <small>Pendentes</small>
          <strong>{{ pendentes }}</strong>
        </div>
        <div class="indicador">
          <small>Concluídas</small>
          <strong>{{ concluidas }}</strong>
        </div>
      </section>

      <section class="painel">
        <h2>Adicionar uma atividade</h2>
        <p>Comece pelas tarefas que precisam de atenção.</p>
        <form class="formulario" @submit.prevent="adicionar">
          <label class="campo">
            <span>O que você precisa estudar?</span>
            <input v-model="texto" type="text" maxlength="120" placeholder="Ex.: Revisar componentes Vue" required />
          </label>
          <label class="campo prioridade-campo">
            <span>Prioridade</span>
            <select v-model="prioridade">
              <option>Alta</option>
              <option>Média</option>
              <option>Baixa</option>
            </select>
          </label>
          <button class="principal-botao" type="submit">+ Adicionar</button>
        </form>
      </section>

      <section class="painel">
        <div class="linha-titulo">
          <div>
            <h2>Minhas atividades</h2>
            <p>Marque o que já terminou e acompanhe suas pendências.</p>
          </div>
          <div class="filtros" aria-label="Filtrar tarefas">
            <button
              v-for="opcao in ['Todas', 'Pendentes', 'Concluídas']"
              :key="opcao"
              type="button"
              :class="{ ativo: filtro === opcao }"
              :aria-pressed="filtro === opcao"
              @click="filtro = opcao"
            >{{ opcao }}</button>
          </div>
        </div>

        <p v-if="tarefasVisiveis.length === 0" class="vazio">Nenhuma tarefa nesta categoria. Adicione uma atividade para começar!</p>
        <ul v-else class="lista">
          <li v-for="tarefa in tarefasVisiveis" :key="tarefa.id" :class="{ concluida: tarefa.concluida }">
            <label class="tarefa">
              <input type="checkbox" :checked="tarefa.concluida" @change="alternar(tarefa)" />
              <span>{{ tarefa.nome }}</span>
            </label>
            <div class="acoes">
              <span class="etiqueta" :class="tarefa.prioridade.toLowerCase()">{{ tarefa.prioridade }}</span>
              <button type="button" class="excluir" :aria-label="'Excluir ' + tarefa.nome" @click="excluir(tarefa.id)">Excluir</button>
            </div>
          </li>
        </ul>
      </section>
    </main>

    <footer>Projeto acadêmico · React, Angular e Vue · Aula 06</footer>
  </div>
</template>

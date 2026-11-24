# Exercício Vue — Organizador de Estudos

Projeto de base da **Atividade 06 — Programação Web**, elaborado para completar a prática de criação de projetos em React, Angular e Vue.

**Observação sobre o histórico:** este repositório estava vazio na conferência de 24/11/2026; a implementação foi acrescentada como complementação posterior. Não é apresentada como um arquivo originalmente entregue em sala.

## Aplicação

O **Organizador de Estudos** é uma página construída com **Vue 3** e **Vite**, com:

- Cadastro de tarefas acadêmicas e seleção da prioridade;
- Listagem de atividades com identificação das concluídas;
- Marcação de conclusão e remoção;
- Filtros **Todas / Pendentes / Concluídas**;
- Contador de tarefas pendentes;
- Armazenamento local no navegador (localStorage);
- Layout responsivo.

## Tecnologias

Vue 3 (Composition API), JavaScript, CSS, Vite, ref, computed, watch, v-model e renderização de listas com v-for.

## Executar localmente

Requer Node.js compatível com a versão do Vite utilizada.

~~~bash
npm install
npm run dev
~~~

Para compilar:

~~~bash
npm run build
~~~

A saída de produção será gerada na pasta **dist**.

## Publicar na Vercel

Importe este repositório no painel da Vercel, escolha Vite como framework se solicitado e utilize:

- **Build Command:** npm run build
- **Output Directory:** dist

A URL de produção ainda não foi confirmada. Antes de declarar a atividade concluída, execute a aplicação, teste as funcionalidades e registre prints reais.

## Portfólio da disciplina

[Documentação da Aula 06](https://github.com/Luizaaaaaah/Programacao_Web/blob/reorganizacao/atividades/aula-06/README.md)

**Não confundir com o projeto Vue HoennDex:** o quarto projeto está em [vue-project](https://github.com/Luizaaaaaah/vue-project).

<script setup>
import { ref } from 'vue';

const skills = ref([
  'Inteligência Artificial',
  'Machine Learning',
  'Engenharia de Dados',
  'Processamento de Dados',
  'APIs Web',
  'Desenvolvimento Mobile',
]);

const projects = ref([
  {
    name: 'Oráculo',
    description: 'Sistema de busca semântica, RAG e perguntas e respostas (QA) sobre documentos PDF.',
    techs: ['Python', 'IA', 'RAG', 'NLP'],
    link: 'https://github.com/MarcosAur/oraculo',
    featured: true
  },
  {
    name: 'Apex Workout',
    description: 'Aplicativo mobile para acompanhamento e gestão de treinos de força.',
    techs: ['Flutter', 'Dart', 'Mobile'],
    link: 'https://github.com/MarcosAur/apex'
  },
  {
    name: 'Estante Virtual - Frontend',
    description: 'Aplicação web reativa para catálogo de livros, avaliações e perfil literário.',
    techs: ['Vue.js', 'TypeScript', 'Vite', 'Frontend'],
    link: 'https://github.com/MarcosAur/estante_virtual_front',
    demo: 'https://marcosaur.github.io/estante_virtual_front/'
  },
  {
    name: 'Estante Virtual - API',
    description: 'API RESTful para gerenciamento de acervo literário e estante virtual.',
    techs: ['PHP', 'Laravel', 'API', 'Backend'],
    link: 'https://github.com/MarcosAur/estante_virtual_api'
  }
]);
</script>

<template>
  <div class="min-h-screen flex flex-col items-center">
    <!-- Navbar -->
    <nav class="w-full max-w-5xl mx-auto py-6 px-4 flex justify-between items-center border-b border-gray-800">
      <div class="flex items-center gap-3">
        <img src="/avatar_logo.jpg" alt="Marcos Aurélio" class="w-10 h-10 rounded-full border-2 border-primary-light shadow-[0_0_10px_rgba(0,229,255,0.5)]" />
        <div class="text-2xl font-bold tracking-tighter">
          Marcos<span class="text-primary-light">Aurélio</span>
        </div>
      </div>
      <div class="flex gap-6">
        <a href="#sobre" class="hover:text-primary transition-colors">Sobre</a>
        <a href="#projetos" class="hover:text-primary transition-colors">Projetos</a>
        <a href="#contato" class="hover:text-primary transition-colors">Contato</a>
      </div>
    </nav>

    <!-- Hero Section -->
    <main class="w-full max-w-5xl mx-auto px-4 flex-grow flex flex-col">
      <section class="py-20 flex flex-col md:flex-row items-center gap-12">
        <div class="flex-1 space-y-6">
          <h1 class="text-5xl font-extrabold leading-tight">
            Olá, eu sou o <br/>
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-primary-light">
              Marcos Aurélio
            </span>
          </h1>
          <p class="text-xl text-gray-400">
            Engenheiro de Dados & Desenvolvedor Web / Mobile.
            Transformando dados em soluções inteligentes e modernas.
          </p>
          <div class="flex gap-4 pt-4">
            <a href="#projetos" class="bg-primary hover:bg-primary-light text-bg-dark font-bold py-3 px-6 rounded-lg transition-all duration-300 transform hover:scale-105">
              Ver Projetos
            </a>
            <a href="https://github.com/MarcosAur" target="_blank" class="border border-gray-700 hover:border-primary text-white font-bold py-3 px-6 rounded-lg transition-all duration-300">
              GitHub
            </a>
          </div>
        </div>
      </section>

      <!-- Sobre & Skills -->
      <section id="sobre" class="py-20 border-t border-gray-800">
        <div class="grid md:grid-cols-2 gap-12">
          <div>
            <h2 class="text-3xl font-bold mb-6 flex items-center gap-2">
              <span class="w-8 h-1 bg-primary inline-block rounded"></span>
              Sobre Mim
            </h2>
            <p class="text-gray-400 leading-relaxed">
              Sou um profissional apaixonado por tecnologia, com forte atuação em 
              <strong class="text-white">Inteligência Artificial, Machine Learning e Engenharia de Dados</strong>.
              Minha trajetória no GitHub demonstra meu compromisso com a construção de 
              APIs robustas, processamento de dados e exploração de novas tecnologias de IA.
            </p>
          </div>
          <div>
            <h2 class="text-3xl font-bold mb-6 flex items-center gap-2">
              <span class="w-8 h-1 bg-primary inline-block rounded"></span>
              Principais Competências
            </h2>
            <div class="flex flex-wrap gap-3">
              <span 
                v-for="skill in skills" 
                :key="skill"
                class="bg-bg-card border border-gray-800 text-gray-300 px-4 py-2 rounded-full text-sm font-medium hover:border-primary-light hover:text-white transition-colors cursor-default"
              >
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </section>

      <!-- Projetos -->
      <section id="projetos" class="py-20 border-t border-gray-800">
        <h2 class="text-3xl font-bold mb-10 text-center">
          Projetos em <span class="text-primary-light">Destaque</span>
        </h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
          <div 
            v-for="project in projects" 
            :key="project.name"
            class="bg-bg-card p-6 rounded-xl border transition-all duration-300 group flex flex-col justify-between"
            :class="project.featured ? 'border-primary/60 shadow-[0_0_20px_rgba(0,123,255,0.25)] hover:border-primary-light' : 'border-gray-800 hover:border-primary'"
          >
            <div>
              <div class="flex items-start justify-between gap-2 mb-2">
                <h3 class="text-xl font-bold group-hover:text-primary-light transition-colors">
                  {{ project.name }}
                </h3>
                <span 
                  v-if="project.featured" 
                  class="bg-primary/20 text-primary-light border border-primary/40 text-xs px-2.5 py-1 rounded-full font-semibold flex items-center gap-1 shadow-sm shrink-0"
                >
                  ★ Destaque
                </span>
              </div>
              <p class="text-gray-400 mb-4 h-12">
                {{ project.description }}
              </p>
              <div class="flex flex-wrap gap-2 mb-6">
                <span 
                  v-for="tech in project.techs" 
                  :key="tech"
                  class="text-xs bg-gray-900 text-gray-300 px-2 py-1 rounded"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
            <div class="flex items-center gap-4 flex-wrap">
              <a 
                v-if="project.demo" 
                :href="project.demo" 
                target="_blank" 
                class="text-primary hover:text-white font-medium text-sm flex items-center gap-1"
              >
                Acessar Projeto &rarr;
              </a>
              <a :href="project.link" target="_blank" class="text-primary hover:text-white font-medium text-sm flex items-center gap-1">
                Ver no GitHub &rarr;
              </a>
            </div>
          </div>
        </div>
      </section>

    </main>

    <!-- Footer -->
    <footer id="contato" class="w-full bg-bg-card py-12 mt-12 border-t border-gray-800">
      <div class="max-w-5xl mx-auto px-4 text-center">
        <h2 class="text-2xl font-bold mb-6">Vamos Conversar?</h2>
        <p class="text-gray-400 mb-8 max-w-md mx-auto">
          Estou sempre aberto a novas oportunidades e desafios em Engenharia de Dados, IA e Desenvolvimento Web / Mobile.
        </p>
        <div class="flex justify-center flex-wrap gap-6">
          <a href="https://github.com/MarcosAur" target="_blank" class="text-gray-400 hover:text-white hover:scale-110 transition-transform">
            GitHub
          </a>
          <a href="https://www.linkedin.com/in/marcos-aur%C3%A9lio-5862a3160" target="_blank" class="text-gray-400 hover:text-primary-light hover:scale-110 transition-transform">
            LinkedIn
          </a>
          <a href="mailto:marcosaureliomendesoliveira@gmail.com" class="text-gray-400 hover:text-white hover:scale-110 transition-transform">
            Email
          </a>
          <a href="https://wa.me/5585999329263" target="_blank" class="text-gray-400 hover:text-[#25D366] hover:scale-110 transition-transform">
            WhatsApp
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

<style>
html {
  scroll-behavior: smooth;
}
</style>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

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

// Controle de menu mobile e scroll
const isMobileMenuOpen = ref(false);
const showBackToTop = ref(false);

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false;
};

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
};

const handleScroll = () => {
  showBackToTop.value = window.scrollY > 350;
};

const handleKeydown = (e) => {
  if (e.key === 'Escape' && isMobileMenuOpen.value) {
    closeMobileMenu();
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true });
  window.addEventListener('keydown', handleKeydown);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  window.removeEventListener('keydown', handleKeydown);
});
</script>

<template>
  <div class="min-h-screen flex flex-col w-full overflow-x-hidden bg-bg-dark text-white">
    <!-- Navbar fixa e responsiva -->
    <header class="sticky top-0 z-50 w-full backdrop-blur-md bg-bg-dark/90 border-b border-gray-800/80 transition-colors">
      <nav class="w-full max-w-5xl mx-auto px-4 sm:px-6 py-3.5 sm:py-4 flex justify-between items-center" aria-label="Navegação Principal">
        <!-- Logo / Identidade -->
        <a href="#" class="flex items-center gap-2.5 sm:gap-3 group focus:outline-none focus:ring-2 focus:ring-primary-light rounded-lg">
          <img 
            src="/avatar_logo.jpg" 
            alt="Foto de perfil de Marcos Aurélio" 
            class="w-9 h-9 sm:w-10 sm:h-10 rounded-full object-cover border-2 border-primary-light shadow-[0_0_12px_rgba(0,229,255,0.4)] group-hover:scale-105 transition-transform" 
          />
          <div class="text-xl sm:text-2xl font-bold tracking-tight">
            Marcos<span class="text-primary-light">Aurélio</span>
          </div>
        </a>

        <!-- Links Desktop -->
        <div class="hidden md:flex items-center gap-8">
          <a href="#sobre" class="text-sm font-medium text-gray-300 hover:text-primary-light transition-colors py-1">Sobre</a>
          <a href="#projetos" class="text-sm font-medium text-gray-300 hover:text-primary-light transition-colors py-1">Projetos</a>
          <a href="#contato" class="text-sm font-medium text-gray-300 hover:text-primary-light transition-colors py-1">Contato</a>
          <a 
            href="https://wa.me/5585999329263" 
            target="_blank" 
            rel="noopener noreferrer"
            class="text-xs font-semibold px-4 py-2 rounded-lg bg-primary/20 text-primary-light border border-primary/40 hover:bg-primary hover:text-bg-dark transition-all duration-200"
          >
            Fale Comigo
          </a>
        </div>

        <!-- Botão Menu Mobile (Hambúrguer) -->
        <button 
          type="button"
          @click="toggleMobileMenu" 
          class="md:hidden p-2 rounded-lg text-gray-300 hover:text-white hover:bg-gray-800/80 focus:outline-none focus:ring-2 focus:ring-primary-light transition-colors"
          :aria-expanded="isMobileMenuOpen"
          aria-label="Abrir menu de navegação"
        >
          <svg v-if="!isMobileMenuOpen" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
          <svg v-else class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </nav>

      <!-- Gaveta / Dropdown do Menu Mobile -->
      <transition
        enter-active-class="transition-all duration-250 ease-out"
        enter-from-class="opacity-0 -translate-y-2 max-h-0"
        enter-to-class="opacity-100 translate-y-0 max-h-96"
        leave-active-class="transition-all duration-200 ease-in"
        leave-from-class="opacity-100 translate-y-0 max-h-96"
        leave-to-class="opacity-0 -translate-y-2 max-h-0"
      >
        <div 
          v-if="isMobileMenuOpen" 
          class="md:hidden overflow-hidden border-t border-gray-800/80 bg-bg-card/95 backdrop-blur-xl px-4 py-4 space-y-2"
        >
          <a 
            href="#sobre" 
            @click="closeMobileMenu"
            class="flex items-center justify-between px-4 py-3 rounded-xl text-base font-medium text-gray-200 hover:text-white hover:bg-gray-800/70 transition-colors"
          >
            <span>Sobre Mim</span>
            <span class="text-xs text-primary-light">&rarr;</span>
          </a>
          <a 
            href="#projetos" 
            @click="closeMobileMenu"
            class="flex items-center justify-between px-4 py-3 rounded-xl text-base font-medium text-gray-200 hover:text-white hover:bg-gray-800/70 transition-colors"
          >
            <span>Projetos em Destaque</span>
            <span class="text-xs text-primary-light">&rarr;</span>
          </a>
          <a 
            href="#contato" 
            @click="closeMobileMenu"
            class="flex items-center justify-between px-4 py-3 rounded-xl text-base font-medium text-gray-200 hover:text-white hover:bg-gray-800/70 transition-colors"
          >
            <span>Contato</span>
            <span class="text-xs text-primary-light">&rarr;</span>
          </a>
          <div class="pt-2">
            <a 
              href="https://wa.me/5585999329263" 
              target="_blank" 
              rel="noopener noreferrer"
              @click="closeMobileMenu"
              class="w-full flex items-center justify-center gap-2 py-3 px-4 rounded-xl bg-gradient-to-r from-primary to-primary-light text-bg-dark font-bold text-sm shadow-[0_0_15px_rgba(0,123,255,0.3)] transition-all"
            >
              <span>Conversar pelo WhatsApp</span>
            </a>
          </div>
        </div>
      </transition>
    </header>

    <!-- Conteúdo Principal -->
    <main class="w-full max-w-5xl mx-auto px-4 sm:px-6 flex-grow flex flex-col">
      <!-- Hero Section -->
      <section class="py-10 sm:py-16 md:py-24 flex flex-col-reverse md:flex-row items-center justify-between gap-8 sm:gap-12">
        <div class="flex-1 space-y-5 sm:space-y-6 text-center md:text-left">
          <!-- Tag de status de disponibilidade -->
          <div class="inline-flex items-center gap-2 px-3 py-1.5 rounded-full text-xs font-medium bg-primary/10 text-primary-light border border-primary/25 shadow-sm">
            <span class="w-2 h-2 rounded-full bg-primary-light animate-ping"></span>
            <span>Disponível para novos projetos e desafios</span>
          </div>

          <h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-extrabold tracking-tight leading-tight">
            Olá, eu sou o <br class="hidden sm:inline" />
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-primary-light">
              Marcos Aurélio
            </span>
          </h1>

          <p class="text-base sm:text-lg md:text-xl text-gray-300/90 leading-relaxed max-w-xl mx-auto md:mx-0">
            Engenheiro de Dados & Desenvolvedor Web / Mobile. Transformando dados em soluções inteligentes, escaláveis e modernas.
          </p>

          <!-- Botões de Ação Principais -->
          <div class="flex flex-col sm:flex-row items-stretch sm:items-center justify-center md:justify-start gap-3 sm:gap-4 pt-2 sm:pt-4 w-full sm:w-auto">
            <a 
              href="#projetos" 
              class="inline-flex items-center justify-center gap-2 bg-gradient-to-r from-primary to-primary-light text-bg-dark font-bold py-3.5 px-6 rounded-xl hover:shadow-[0_0_20px_rgba(0,229,255,0.4)] transition-all duration-300 transform active:scale-95"
            >
              <span>Ver Projetos</span>
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
              </svg>
            </a>
            <a 
              href="https://github.com/MarcosAur" 
              target="_blank" 
              rel="noopener noreferrer"
              class="inline-flex items-center justify-center gap-2 border border-gray-700 hover:border-primary text-white font-semibold py-3.5 px-6 rounded-xl bg-bg-card/70 hover:bg-gray-800 transition-all duration-300 transform active:scale-95"
            >
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z" />
              </svg>
              <span>GitHub</span>
            </a>
          </div>
        </div>

        <!-- Avatar / Imagem de Apresentação -->
        <div class="relative shrink-0 flex items-center justify-center">
          <div class="relative w-36 h-36 sm:w-48 sm:h-48 md:w-56 md:h-56 lg:w-64 lg:h-64 rounded-full p-1 bg-gradient-to-tr from-primary via-primary-light to-blue-500 shadow-[0_0_35px_rgba(0,229,255,0.25)]">
            <img 
              src="/avatar_logo.jpg" 
              alt="Foto de Marcos Aurélio" 
              class="w-full h-full object-cover rounded-full border-2 border-bg-dark" 
              loading="eager"
            />
          </div>
        </div>
      </section>

      <!-- Sobre & Skills -->
      <section id="sobre" class="py-12 sm:py-16 md:py-20 border-t border-gray-800/80">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 md:gap-12">
          <!-- Sobre Mim -->
          <div>
            <h2 class="text-2xl sm:text-3xl font-bold mb-4 sm:mb-6 flex items-center gap-2.5">
              <span class="w-7 sm:w-8 h-1 bg-primary inline-block rounded"></span>
              <span>Sobre Mim</span>
            </h2>
            <div class="text-gray-300/90 text-sm sm:text-base leading-relaxed space-y-4">
              <p>
                Sou um profissional apaixonado por tecnologia, com sólida atuação em 
                <strong class="text-white font-semibold">Inteligência Artificial, Machine Learning e Engenharia de Dados</strong>.
              </p>
              <p>
                Minha trajetória prática demonstra compromisso com a criação de APIs robustas, pipelines e processamento eficiente de dados e a aplicação de arquiteturas modernas como RAG e NLP para resolver problemas reais.
              </p>
            </div>
          </div>

          <!-- Principais Competências -->
          <div>
            <h2 class="text-2xl sm:text-3xl font-bold mb-4 sm:mb-6 flex items-center gap-2.5">
              <span class="w-7 sm:w-8 h-1 bg-primary inline-block rounded"></span>
              <span>Principais Competências</span>
            </h2>
            <div class="flex flex-wrap gap-2 sm:gap-2.5">
              <span 
                v-for="skill in skills" 
                :key="skill"
                class="bg-bg-card border border-gray-800 text-gray-200 px-3.5 py-2 rounded-xl text-xs sm:text-sm font-medium hover:border-primary-light hover:text-white transition-all shadow-sm active:scale-95 cursor-default select-none"
              >
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </section>

      <!-- Projetos em Destaque -->
      <section id="projetos" class="py-12 sm:py-16 md:py-20 border-t border-gray-800/80">
        <div class="text-center mb-8 sm:mb-12">
          <h2 class="text-2xl sm:text-3xl md:text-4xl font-bold mb-3">
            Projetos em <span class="text-primary-light">Destaque</span>
          </h2>
          <p class="text-sm sm:text-base text-gray-400 max-w-lg mx-auto">
            Projetos selecionados abrangendo IA, desenvolvimento fullstack e mobile.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-5 sm:gap-6">
          <div 
            v-for="project in projects" 
            :key="project.name"
            class="bg-bg-card p-5 sm:p-6 rounded-2xl border transition-all duration-300 group flex flex-col justify-between hover:-translate-y-1"
            :class="project.featured ? 'border-primary/50 shadow-[0_0_25px_rgba(0,123,255,0.18)] hover:border-primary-light' : 'border-gray-800/90 hover:border-primary/50'"
          >
            <div>
              <div class="flex items-start justify-between gap-3 mb-2.5">
                <h3 class="text-lg sm:text-xl font-bold text-white group-hover:text-primary-light transition-colors break-words">
                  {{ project.name }}
                </h3>
                <span 
                  v-if="project.featured" 
                  class="bg-primary/20 text-primary-light border border-primary/30 text-xs px-2.5 py-1 rounded-full font-semibold flex items-center gap-1 shadow-sm shrink-0"
                >
                  ★ Destaque
                </span>
              </div>

              <!-- Descrição responsiva sem altura fixa para evitar vazamentos de texto em celulares -->
              <p class="text-gray-300/80 text-sm sm:text-base mb-4 leading-relaxed">
                {{ project.description }}
              </p>

              <!-- Tags de tecnologias -->
              <div class="flex flex-wrap gap-1.5 sm:gap-2 mb-6">
                <span 
                  v-for="tech in project.techs" 
                  :key="tech"
                  class="text-xs bg-gray-900/90 border border-gray-800 text-gray-300 px-2.5 py-1 rounded-md font-mono"
                >
                  {{ tech }}
                </span>
              </div>
            </div>

            <!-- Links de Ação com boa área de toque -->
            <div class="flex flex-wrap items-center gap-2.5 sm:gap-4 pt-4 border-t border-gray-800/60 mt-auto">
              <a 
                v-if="project.demo" 
                :href="project.demo" 
                target="_blank" 
                rel="noopener noreferrer"
                class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold bg-primary/10 hover:bg-primary text-primary-light hover:text-bg-dark border border-primary/30 transition-all active:scale-95"
              >
                <span>Acessar Projeto</span>
                <span aria-hidden="true">&rarr;</span>
              </a>
              <a 
                :href="project.link" 
                target="_blank" 
                rel="noopener noreferrer"
                class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg text-xs sm:text-sm font-medium bg-gray-900/80 hover:bg-gray-800 text-gray-300 hover:text-white border border-gray-800 hover:border-gray-700 transition-all active:scale-95"
              >
                <span>Ver no GitHub</span>
                <span aria-hidden="true">&rarr;</span>
              </a>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Footer / Contato -->
    <footer id="contato" class="w-full bg-bg-card/50 py-12 sm:py-16 mt-12 sm:mt-16 border-t border-gray-800/80">
      <div class="max-w-5xl mx-auto px-4 sm:px-6 text-center">
        <h2 class="text-2xl sm:text-3xl font-bold mb-3 sm:mb-4">Vamos Conversar?</h2>
        <p class="text-sm sm:text-base text-gray-400 mb-8 max-w-md mx-auto leading-relaxed">
          Estou sempre aberto a novas oportunidades e desafios em Engenharia de Dados, IA e Desenvolvimento Web / Mobile.
        </p>

        <!-- Redes Sociais Touch-Friendly com Ícones -->
        <div class="grid grid-cols-2 sm:flex sm:flex-wrap sm:justify-center gap-3 sm:gap-4 max-w-md sm:max-w-none mx-auto">
          <!-- GitHub -->
          <a 
            href="https://github.com/MarcosAur" 
            target="_blank" 
            rel="noopener noreferrer"
            class="flex items-center justify-center gap-2.5 px-4 py-3 rounded-xl bg-bg-card border border-gray-800 hover:border-gray-500 text-sm font-medium text-gray-300 hover:text-white transition-all active:scale-95 shadow-sm"
          >
            <svg class="w-4 h-4 shrink-0" fill="currentColor" viewBox="0 0 24 24">
              <path fill-rule="evenodd" clip-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z" />
            </svg>
            <span>GitHub</span>
          </a>

          <!-- LinkedIn -->
          <a 
            href="https://www.linkedin.com/in/marcos-aur%C3%A9lio-5862a3160" 
            target="_blank" 
            rel="noopener noreferrer"
            class="flex items-center justify-center gap-2.5 px-4 py-3 rounded-xl bg-bg-card border border-gray-800 hover:border-primary-light text-sm font-medium text-gray-300 hover:text-primary-light transition-all active:scale-95 shadow-sm"
          >
            <svg class="w-4 h-4 shrink-0" fill="currentColor" viewBox="0 0 24 24">
              <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.762-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/>
            </svg>
            <span>LinkedIn</span>
          </a>

          <!-- WhatsApp -->
          <a 
            href="https://wa.me/5585999329263" 
            target="_blank" 
            rel="noopener noreferrer"
            class="flex items-center justify-center gap-2.5 px-4 py-3 rounded-xl bg-bg-card border border-gray-800 hover:border-[#25D366] text-sm font-medium text-gray-300 hover:text-[#25D366] transition-all active:scale-95 shadow-sm"
          >
            <svg class="w-4 h-4 shrink-0" fill="currentColor" viewBox="0 0 24 24">
              <path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946.003-6.556 5.338-11.891 11.893-11.891 3.181.001 6.167 1.24 8.413 3.488 2.245 2.248 3.481 5.236 3.48 8.414-.003 6.557-5.338 11.892-11.893 11.892-1.99-.001-3.951-.5-5.688-1.448l-6.305 1.654zm6.597-3.807c1.676.995 3.276 1.591 5.392 1.592 5.448 0 9.886-4.434 9.889-9.885.002-5.462-4.415-9.89-9.881-9.892-5.452 0-9.887 4.434-9.889 9.884-.001 2.225.651 3.891 1.746 5.634l-.999 3.648 3.742-.981zm11.387-5.464c-.074-.124-.272-.198-.57-.347-.297-.149-1.758-.868-2.031-.967-.272-.099-.47-.149-.669.149-.198.297-.768.967-.941 1.165-.173.198-.347.223-.644.074-.297-.149-1.255-.462-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.297-.347.446-.521.151-.172.2-.296.3-.495.099-.198.05-.372-.025-.521-.075-.148-.669-1.611-.916-2.206-.242-.579-.487-.501-.669-.51l-.57-.01c-.198 0-.52.074-.792.372s-1.04 1.016-1.04 2.479 1.065 2.876 1.213 3.074c.149.198 2.095 3.2 5.076 4.487.709.306 1.263.489 1.694.626.712.226 1.36.194 1.872.118.571-.085 1.758-.719 2.006-1.413.248-.695.248-1.29.173-1.414z"/>
            </svg>
            <span>WhatsApp</span>
          </a>

          <!-- Email -->
          <a 
            href="mailto:marcosaureliomendesoliveira@gmail.com" 
            class="flex items-center justify-center gap-2.5 px-4 py-3 rounded-xl bg-bg-card border border-gray-800 hover:border-primary text-sm font-medium text-gray-300 hover:text-white transition-all active:scale-95 shadow-sm"
          >
            <svg class="w-4 h-4 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
            <span>Email</span>
          </a>
        </div>

        <!-- Rodapé Final -->
        <div class="mt-12 pt-8 border-t border-gray-800/60 flex flex-col sm:flex-row items-center justify-between gap-4 text-xs sm:text-sm text-gray-500">
          <p>© 2026 Marcos Aurélio. Todos os direitos reservados.</p>
          <button 
            type="button"
            @click="scrollToTop" 
            class="text-gray-400 hover:text-primary-light transition-colors flex items-center gap-1.5 focus:outline-none"
          >
            <span>Voltar ao topo</span>
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 10l7-7m0 0l7 7m-7-7v18" />
            </svg>
          </button>
        </div>
      </div>
    </footer>

    <!-- Botão Flutuante 'Voltar ao Topo' (Back to Top) no Mobile/Desktop -->
    <transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 translate-y-4 scale-90"
      enter-to-class="opacity-100 translate-y-0 scale-100"
      leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0 scale-100"
      leave-to-class="opacity-0 translate-y-4 scale-90"
    >
      <button
        v-if="showBackToTop"
        type="button"
        @click="scrollToTop"
        class="fixed bottom-5 right-5 sm:bottom-8 sm:right-8 z-40 p-3 sm:p-3.5 rounded-full bg-primary/90 text-bg-dark hover:bg-primary-light shadow-[0_4px_20px_rgba(0,123,255,0.4)] transition-all transform active:scale-90 focus:outline-none focus:ring-2 focus:ring-primary-light"
        aria-label="Voltar para o topo da página"
      >
        <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M5 15l7-7 7 7" />
        </svg>
      </button>
    </transition>
  </div>
</template>

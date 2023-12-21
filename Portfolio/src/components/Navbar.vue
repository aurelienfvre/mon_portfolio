<template>
    <nav class="fixed bottom-0 md:bottom-auto md:top-0 z-10 bg-white rounded-full shadow-lg p-4 mx-auto w-9/12 md:w-3/4 lg:w-1/2 xl:w-4/12 h-15 custom-shadow m-8">
      <ul class="flex justify-center items-center h-full" ref="navList">  
        <li v-for="section in ['accueil', 'projets', 'contact']" :key="section" class="relative flex-1 text-center">
          <a :href="'#' + section" :class="linkClasses(section)">
            {{ section.charAt(0).toUpperCase() + section.slice(1) }}
          </a>
          <div v-if="currentSection === section" class="floating"></div>
        </li>
      </ul>
    </nav>
  </template>
  
  <script>
  export default {
    name: 'Navbar',
    data() {
      return {
        currentSection: 'accueil',
      };
    },
    mounted() {
      window.addEventListener('scroll', this.handleScroll);
    },
    beforeDestroy() {
      window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
      handleScroll() {
        const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
        const sections = [
          { name: 'accueil', element: document.getElementById('accueil') },
          { name: 'projets', element: document.getElementById('projets') },
          { name: 'contact', element: document.getElementById('contact') },
        ];
        const navbarHeight = this.$el.clientHeight;
  
        for (let i = sections.length - 1; i >= 0; i--) {
          if (sections[i].element && sections[i].element.offsetTop - navbarHeight <= scrollTop) {
            this.currentSection = sections[i].name;
            break;
          }
        }
      },
      linkClasses(section) {
        return {
          'px-12 font-outfit font-bold text-base transition-colors duration-300 p-4': true,
          'text-medium': this.currentSection === section,
          'text-neutral-400': this.currentSection !== section,
        };
      },
      moveActiveIndicator() {
    this.$nextTick(() => {
      const activeLink = this.$refs.navList.querySelector('.text-medium');
      if (activeLink) {
        const activeLinkWidth = activeLink.offsetWidth;
        const floatingWidth = 80; // Assurez-vous que cela correspond à la largeur de votre indicateur flottant
        const activeLinkLeft = activeLink.getBoundingClientRect().left;
        const navListLeft = this.$refs.navList.getBoundingClientRect().left;
        const leftPosition = activeLinkLeft - navListLeft + (activeLinkWidth - floatingWidth) / 2;

        this.activeIndicatorStyle = {
          left: `${leftPosition}px`,
          zIndex: 5,
          bottom: '6px',
          // La transition doit être appliquée ici pour que l'animation fonctionne
          transition: 'left 0.5s cubic-bezier(0.34, 1.56, 0.64, 1)',
        };
        }
        });
    },
    },
  };
  </script>
  
  <style scoped>
  .custom-shadow {
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    border: 0.5px solid #e9e9e9;
  }
  
  .floating {
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  height: 44px;
  width: 114px;
  background-color: #f2f0f0;
  border-radius: 100px;
  z-index: 5;
  /* Animation avec un effet bouncy */
  transition: left 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);

  @media (max-width: 566px) {
    width: 80px;
    height: 30px;
    bottom: -5px;
  }
}

ul.flex li {
  flex: 1;
  text-align: center;
  position: relative;
  padding: 0 8px; /* Réduction du padding */
}

ul.flex li a {
  z-index: 10;
  position: relative;
  white-space: nowrap;

  @media (max-width: 566px) {
    font-size: 0.75rem; /* Taille de police plus petite */
    padding: 0 4px; /* Réduction supplémentaire du padding pour les petits écrans */
  }
}

  </style>
  
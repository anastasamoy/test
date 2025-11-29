<template>
  <div class="app">
    <Header :translations="translations" />
    <Navigation 
      :translations="translations" 
      :active-tab="activeTab"
      @tab-change="handleTabChange"
    />
    <MainContent :translations="translations" />
    <Footer :translations="translations" />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Navigation from './components/Navigation.vue'
import MainContent from './components/MainContent.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Navigation,
    MainContent,
    Footer
  },
  data() {
    return {
      activeTab: 'home',
      translations: {
        header: {
          title: "Vue.js Demo Stránka",
          subtitle: "Moderná webová aplikácia"
        },
        navigation: {
          home: "🏠 Domov",
          about: "ℹ️ O nás", 
          services: "⚙️ Služby",
          contact: "📞 Kontakt"
        },
        main: {
          welcome: "Vitajte v našej aplikácii!",
          intro: "Toto je moderná demo stránka vytvorená pomocou Vue.js 3. Všetky texty sú v slovenčine.",
          features: "Hlavné funkcie",
          contactForm: "Kontaktný formulár"
        },
        form: {
          name: "Meno a priezvisko",
          email: "Emailová adresa", 
          phone: "Telefónne číslo",
          message: "Vaša správa",
          category: "Kategória",
          categories: {
            general: "Všeobecný dotaz",
            support: "Technická podpora",
            sales: "Predaj",
            other: "Iné"
          },
          submit: "Odoslať správu",
          reset: "Vymazať formulár"
        },
        buttons: {
          primary: "Hlavná akcia",
          secondary: "Vedľajšia akcia", 
          success: "Úspech",
          danger: "Varovanie"
        },
        footer: {
          copyright: "© 2024 Vue.js Demo. Všetky práva vyhradené.",
          madeWith: "Vytvorené s Vue.js a ❤️"
        }
      }
    }
  },
  methods: {
    handleTabChange(tab) {
      this.activeTab = tab
      console.log('Aktívna záložka:', tab)
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: #2c3e50;
  background-color: #ecf0f1;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Utility classes */
.mt-1 { margin-top: 1rem; }
.mt-2 { margin-top: 2rem; }
.mb-1 { margin-bottom: 1rem; }
.mb-2 { margin-bottom: 2rem; }
.text-center { text-align: center; }
</style>